# Chatbot RAG para o FAQ Universitário da UFRGS

## Contexto

Calouros chegam à UFRGS sem saber onde matricular, como trancar disciplinas, como pedir bolsas, como usar o restaurante universitário ou como ativar o e-mail institucional. A informação existe, mas está espalhada entre regulamentos, sites de cursos, PROGRAD, PRAE, CPD, guia do calouro e PDFs institucionais.

Este chatbot foi desenvolvido como trabalho final da disciplina de Processamento de Linguagem Natural (PLN) — UFRGS, 2025/2 — pelos alunos **Anísio Lorentz e Arthur Camargo**. O objetivo é centralizar esse conhecimento e responder perguntas de calouros com base em documentos oficiais, não em achismo.

---

## Para que serve

O chatbot responde perguntas universitárias dentro de 5 categorias:

- **Matrícula** (`enrollment`) — como se matricular, prazos, pré-requisitos, ordenamento, aproveitamento de disciplinas
- **Trancamento** (`withdrawal`) — como trancar matrícula, cancelar disciplinas, regras de abandono e readmissão
- **Bolsas** (`scholarship`) — benefícios PRAE, Bolsa Permanência, auxílios, bolsas de aperfeiçoamento
- **Restaurante Universitário** (`university-restaurant`) — funcionamento, unidades, preços, tíquetes, regras de acesso
- **E-mail institucional** (`email`) — ativação e uso do e-mail @ufrgs.br (ChasqueMail)

Perguntas fora dessas categorias são recusadas — o bot declina em vez de inventar uma resposta.

---

## Arquitetura — RAG (Retrieval-Augmented Generation)

O chatbot usa a arquitetura **RAG**, que combina busca semântica com geração de linguagem natural. Em vez de treinar um modelo do zero ou esperar que o LLM "saiba tudo de cabeça", o sistema recupera os trechos relevantes dos documentos oficiais no momento da pergunta e os usa como contexto para gerar a resposta.

### Por que RAG e não Fine-tuning?

| | RAG | Fine-tuning |
|---|---|---|
| Atualização | Troca o documento | Retreina o modelo inteiro |
| Rastreabilidade | Cita a fonte | Responde "de memória" |
| Custo | Baixo | Alto (GPU, dados rotulados) |
| Alucinação | Reduzida | Ainda ocorre |

RAG é a escolha certa porque os documentos da UFRGS mudam todo semestre, e as respostas precisam ser rastreáveis (citar o artigo ou fonte).

---

## Pipeline completo

```
[Documentos UFRGS]
      ↓ Coleta (Firecrawl / pdf-parse / Cheerio)
[Texto limpo]
      ↓ Chunking (~300 tokens, overlap ~50)
[Chunks com metadados]
      ↓ Modelo de embedding (BGE-m3 / E5-multilingual)
[Vetores armazenados no índice]

--- em tempo real ---

[Pergunta do calouro]
      ↓ Mesmo modelo de embedding
[Vetor da pergunta]
      ↓ Similaridade de cosseno
[Top-4 chunks mais relevantes]
      ↓ Prompt = pergunta + chunks
[Claude API (Anthropic)]
      ↓
[Resposta citando a fonte]
```

---

## Etapas de desenvolvimento

### 1. Coleta e limpeza dos documentos
Extração de texto das fontes oficiais da UFRGS:

| Documento | Tipo | Ferramenta |
|---|---|---|
| Páginas da PRAE (RU, benefícios, FAQ) | HTML | Firecrawl ou Cheerio |
| Guia do calouro | PDF | pdf-parse |
| Resolução 11/2013 (Normas Básicas da Graduação) | PDF | pdf-parse |
| Portarias do RU (normativa e preços) | PDF | pdf-parse |
| Catálogo de Serviços de TI / Documentação CPD (e-mail) | HTML | Firecrawl ou Cheerio |

Output: arquivos JSON estruturados com `id`, `source`, `type`, `url`, `category`, `content` e `metadata`. Parte do conteúdo é inserida manualmente e revisada, garantindo correção de imprecisões das fontes oficiais (revisão humana sobre a curadoria dos dados).

### 2. Chunking
Divisão dos textos em pedaços de ~300 tokens com overlap de ~50 tokens. Cada chunk carrega metadados (fonte, página, URL) para permitir citação na resposta.

### 3. Indexação com Embeddings
Geração de vetores numéricos para cada chunk usando um modelo de embedding multilingual baseado em Transformer (BGE-m3 ou E5-multilingual-large), chamado via HuggingFace Inference API. Os vetores são armazenados em SQLite ou em memória para consulta.

### 4. Retrieval Semântico
A cada pergunta, o sistema gera o embedding da pergunta com o mesmo modelo, calcula a similaridade de cosseno com todos os chunks indexados, e retorna os top-4 mais relevantes.

### 5. Geração com LLM
Os top-4 chunks são enviados junto com a pergunta para a **Claude API (Anthropic)**. O prompt instrui o modelo a responder somente com base no contexto fornecido e a citar a fonte. Se o retrieval não retornar contexto útil, o bot recusa — não inventa.

---

## Dataset de avaliação

Como não existe dataset pronto para o domínio UFRGS, o benchmark é construído manualmente:

- **~100 pares pergunta/resposta** construídos manualmente
- **5 categorias** cobertas: matrícula, trancamento, bolsas, RU e e-mail institucional
- Cada par contém: pergunta, resposta esperada, chunk de referência e categoria
- Serve como **ground truth** para todas as métricas de avaliação

---

## Métricas de avaliação

### Recall@k
Avalia o retrieval: o chunk correto está entre os top-k recuperados? Calculado para K = 2, 4 e 6 para comparação.

### BERTScore
Mede a similaridade semântica entre a resposta gerada e a resposta esperada. Vai além do casamento literal de palavras — captura paráfrases e sinônimos.

### Avaliação humana
Correção factual em uma amostra do dataset — única forma robusta de capturar alucinações plausíveis que as métricas automáticas não detectam.

---

## Stack tecnológica

| Camada | Tecnologia |
|---|---|
| Linguagem | TypeScript |
| Runtime | Node.js |
| LLM | Claude API (Anthropic) |
| Embedding | BGE-m3 via HuggingFace API |
| Armazenamento | SQLite ou JSON |
| Coleta HTML | Firecrawl / Cheerio |
| Coleta PDF | pdf-parse |
| Testes | Jest |
| Auxiliares | dotenv, pino, zod |

---

## Experimentos planejados

1. **Chunking**: comparar tamanho fixo vs. por parágrafo — impacto no Recall@k
2. **Modelo de embedding**: BGE-m3 vs. E5-multilingual-large — qual performa melhor em PT-BR
3. **K no retrieval**: K = 2, 4, 6 — trade-off entre precisão e custo
4. **Metadata filtering**: RAG sem filtro de categoria vs. com filtro — impacto no Recall@k
5. **Baseline**: LLM sem RAG vs. LLM com RAG — justifica a arquitetura

---

## Conexão com os requisitos acadêmicos

| Requisito da disciplina | Como é atendido |
|---|---|
| Tópico de PLN | Chatbots + RAG (itens 2 e 14 da lista) |
| Conexão com linguagem natural | Perguntas e respostas em português sobre documentos textuais |
| Dataset anotado com ground truth | ~100 pares Q/A construídos manualmente com referência à fonte, cobrindo 5 categorias |
| Técnicas baseadas em Transformers | Modelo de embedding BGE-m3 / E5 para retrieval semântico |
| Métricas de avaliação | Recall@k, BERTScore, avaliação humana |
| Artigo científico | 8-10 páginas formato SBC |
