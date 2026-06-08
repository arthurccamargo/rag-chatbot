# Chatbot UFRGS — Escopos Deixados de Lado

Documento de rastreamento de conteúdos identificados durante a coleta de dados mas **não indexados** no knowledge base do chatbot. Serve para retomada futura, menção como limitação no artigo acadêmico, ou expansão do escopo do chatbot.

---

## 1. Cardápio semanal dos RUs

**Decisão:** não indexar  
**Motivo:** o cardápio muda toda semana e estaria desatualizado em dias. O chatbot redireciona o usuário para o link oficial.  
**Link de origem:** https://www.ufrgs.br/prae/cardapio-ru/  
**Conteúdo deixado de lado:** pratos de almoço e jantar de cada RU (segunda a sexta), por semana. Inclui proteína animal, proteína vegetal, acompanhamentos, saladas, sobremesas e molhos para cada unidade (RU01 a RU06).  
**Como retomar:** implementar scraping semanal automático da página e re-indexar os chunks a cada semana, substituindo os anteriores.

---

## 2. Moradia Estudantil (Casas de Estudantes)

**Decisão:** fora do escopo das 5 categorias definidas  
**Motivo:** o chatbot cobre apenas matrícula, trancamento, bolsas, RU e e-mail institucional. Moradia é um benefício PRAE separado.  
**Link de origem:** https://www.ufrgs.br/prae/perguntas-frequentes/ (seção "Moradia Estudantil")  
**Conteúdo deixado de lado:**
- O que é a Moradia Estudantil e quem pode solicitar
- As 4 casas de estudante: CEU (Campus Centro), CEUFRGS (Campus Saúde), CEFAV (Campus Vale), CEI (Casa dos Estudantes Indígenas)
- Processo seletivo e editais de cada casa
- Procedimentos internos: manutenção, visitantes, troca de quarto, correspondências, coleta de lixo, chaves
- Recálculo de tempo de permanência na CEU ao trocar de curso
- Contatos: ceu.adm@ufrgs.br, manutencao-casas@ufrgs.br

---

## 3. Esportes Universitários

**Decisão:** fora do escopo  
**Motivo:** não está entre as 5 categorias do chatbot.  
**Link de origem:** https://www.ufrgs.br/prae/perguntas-frequentes/ (seção "Esportes")  
**Conteúdo deixado de lado:**
- Como organizar campeonatos e solicitar suporte da DPSD
- Equipes competitivas da UFRGS (Futsal, Basquete, Voleibol, Handebol, Futebol)
- Competições oficiais: JUGS, JUBs, Copa Unisinos
- Comprovante de participação em atividades esportivas
- Contato: esportesuniversitarios@prae.ufrgs.br, (51) 3308.3714

---

## 4. Auxílio Participação em Eventos (detalhamento completo)

**Decisão:** indexado apenas parcialmente em `scholarship-faq.json`  
**Motivo:** as perguntas mais operacionais (prazo, devolução, prestação de contas) foram deixadas de fora por serem específicas demais e não serem dúvidas de calouro.  
**Link de origem:** https://www.ufrgs.br/prae/perguntas-frequentes/ (seção "Auxílio Participação em Eventos")  
**Conteúdo deixado de lado:**
- O que fazer se a data do evento mudar (não precisa ajustar, salvo cancelamento)
- O que fazer se solicitou para evento X mas tem certificado do evento Y (deve devolver)
- Regras de acumulação com auxílios de outros órgãos
- Eventos no exterior (verificar lista de destinos no edital)
- Recurso administrativo em caso de rejeição do pedido

---

## 5. Programa Saúde e Auxílio Saúde Mental (detalhamento)

**Decisão:** indexado apenas superficialmente em `scholarship-faq.json`  
**Motivo:** é um benefício PRAE, mas com fluxos operacionais complexos que vão além do escopo de calouro.  
**Link de origem:** https://www.ufrgs.br/prae/perguntas-frequentes/ (seção "Benefícios PRAE")  
**Conteúdo deixado de lado:**
- Diferença entre Programa Saúde e Auxílio Saúde Mental
- Atendimento nutricional: agendamento por nutricao@prae.ufrgs.br (suspensas novas solicitações no momento)
- Acolhimento em saúde mental: psicologiaprae@prae.ufrgs.br
- Atividades esportivas: dpsd@prae.ufrgs.br
- Como restituir valor não utilizado do Auxílio Saúde Mental (via GRU, e-mail prae@prae.ufrgs.br)

---

## 6. Detalhamento de Pagamentos e Dados Bancários (bolsas)

**Decisão:** indexado de forma resumida em `scholarship-faq.json`  
**Motivo:** os fluxos mais operacionais (cancelar taxas bancárias, impedimento de abrir conta, informe de rendimentos para IR) são detalhes que calouros raramente precisam no primeiro contato.  
**Link de origem:** https://www.ufrgs.br/prae/perguntas-frequentes/ (seção "Pagamentos de Bolsas e Benefícios")  
**Conteúdo deixado de lado:**
- Como cancelar taxas mensais do Banco do Brasil pelo caixa eletrônico
- O que fazer se estiver impedido de abrir conta bancária
- Como obter o Comprovante de Rendimentos (Informe de IR): e-mail dcf@ufrgs.br
- Como obter Declaração de pagamentos de benefícios: e-mail creg@prae.ufrgs.br
- Distinção entre bolsas pagas pela UFRGS vs. por Fundações de Apoio (FAURGS, FAPERGS etc.)

---

## 7. Portaria nº 6868/2025 — Capítulos não indexados integralmente

**Decisão:** indexados apenas os artigos mais relevantes para calouros  
**Motivo:** os capítulos abaixo tratam de situações administrativas ou disciplinares que raramente são dúvida de primeiro acesso.  
**Link de origem:** PDF `6868-portaria-normativa-rus-2025.pdf`  
**Conteúdo deixado de lado:**
- **Cap. III - Da Administração (Art. 5º e 6º):** detalhes sobre a gestão contratual da DAL e obrigações das empresas terceirizadas
- **Cap. XII - Das Penalidades Disciplinares (Art. 25):** aplicação do Código Disciplinar Discente para uso indevido do cartão, desacato a servidores etc.
- **Art. 11 (cardápios):** diretrizes nutricionais, valorização da agricultura familiar e sazonalidade — não é dúvida operacional de calouro
- **Art. 14:** acesso gratuito em caso de falta de energia elétrica com documento institucional
- **Art. 27:** colaboração dos RUs com pesquisas e reportagens (mínimo 5 dias úteis de antecedência)
- **Art. 28:** isenção de responsabilidade da DAL por pertences esquecidos

---

## 8. Convênio IFRS (encerrado)

**Decisão:** não indexado  
**Motivo:** o convênio com o Instituto Federal (IFRS) foi encerrado em janeiro de 2023. Indexar isso poderia confundir estudantes que tentassem usar o RU.  
**Link de origem:** https://www.ufrgs.br/prae/perguntas-frequentes/  
**Conteúdo deixado de lado:** "Sou aluno do IFRS, como faço para comer no RU? — Não é mais possível, pois o convênio encerrou em janeiro/2023."  
**Observação:** pode ser útil indexar como resposta negativa para evitar que o bot invente uma resposta incorreta se perguntado.

---

## 9. RU07 - Campus Litoral Norte (cardápio específico)

**Decisão:** não indexado  
**Motivo:** mesma decisão do cardápio geral — muda semanalmente.  
**Link de origem:** https://www.ufrgs.br/litoral/cardapio-ru/  
**Conteúdo deixado de lado:** cardápio semanal específico do Campus Litoral Norte.  
**Como retomar:** mesmo approach do item 1 — scraping semanal.

---

## 10. Página principal PRAE - Restaurantes Universitários (estava offline)

**Decisão:** parcialmente coberta por outras fontes  
**Motivo:** a página retornou erro 503 durante a coleta. O conteúdo institucional foi recuperado manualmente pelo Arthur. Podem existir informações adicionais não capturadas.  
**Link de origem:** https://www.ufrgs.br/prae/restaurantes-universitarios/  
**Conteúdo possivelmente deixado de lado:** informações sobre a Divisão de Alimentação (DAL), histórico dos RUs, documentos oficiais vinculados à página.  
**Como retomar:** acessar a página quando estiver disponível e comparar com o que já foi indexado.

---

## 11. Guia do Calouro — conteúdo específico da Faculdade de Arquitetura

**Decisão:** não indexado  
**Motivo:** o chatbot é para toda a UFRGS, não para um curso específico.  
**Fonte:** PDF `Arquitetura-guia-calouro.pdf`  
**Conteúdo deixado de lado:**
- Calendário Acadêmico com links do COMGRAD-ARQ e COMGRAD-DSG
- Horários de disciplinas dos cursos de Arquitetura, Design Visual e Design de Produto
- Biblioteca da Faculdade de Arquitetura (térreo): https://www.ufrgs.br/bibarq/
- Equipe do Núcleo Acadêmico da FA (Airton Darold, Marcelo Goulart, Miriam Nunes)
- Contatos específicos da FA: arqacademico@ufrgs.br, (51) 3308-4002

---

## 12. Guia do Calouro — conteúdo fora das 5 categorias do chatbot

**Decisão:** não indexado  
**Motivo:** temas fora do escopo definido (matrícula, trancamento, bolsas, RU, e-mail institucional).  
**Fonte:** PDF `Arquitetura-guia-calouro.pdf`  
**Conteúdo deixado de lado:**
- **TUA UFRGS:** central de atendimento ao aluno — https://www.ufrgs.br/tuaufrgs/
- **Biblioteca Central:** catálogo SABI, portal de periódicos CAPES, empréstimo domiciliar — www.biblioteca.ufrgs.br
- **Casa do Estudante:** CEU (Av. João Pessoa 41, tel. 3308-4206), CEFAV (Av. Bento Gonçalves 7.712, tel. 3308-6250), CEUFRGS (Rua São Manoel 573, tel. 3331-3335)
- **Colônia de Férias:** em Tramandaí, diária R$5 para estudantes, reservas na CEU sala 15, tel. 33084036
- **Esporte:** equipes universitárias (voleibol, futsal, basquete etc.), Campus Olímpico/ESEF — esportesufrgs@gmail.com, tel. 3308-3799
- **Intercâmbio:** acordos com instituições internacionais, dois tipos (com bolsa e independente conveniada) — Secretaria Relinter: http://www.ufrgs.br/relinter/portugues
- **Comunicação:** Jornal da Universidade, Rádio da Universidade, UFRGS TV
- **Programa de Línguas (NELE):** cursos de alemão, espanhol, francês, inglês, italiano, japonês — http://www.ufrgs.br/nele/
- **Pesquisa e extensão:** bolsas de iniciação científica (PROPESQ tel. 3308-3209), bolsas de extensão (PROREXT tel. 3308-3020)
- **Estágios:** regras da Lei do Estágio, requisitos de créditos, DEMA/Decordi — estagios@prograd.ufrgs.br, tel. 3308-3371
- **Monitorias:** inscrição pelo Portal do Aluno, aba Aluno > Monitoria
- **Transporte:** cartão TRI — https://www.tripoa.net.br/
- **Vacinação:** Departamento de Atenção à Saúde, Av. Protásio Alves 297 — tel. 3308-2004
- **Assistência médica e odontológica:** consultas para beneficiários SAE/saúde — tel. 3308-2014 ou 3308-2016
- **Abono de faltas por doença:** resolução 017/2007 do CEPE/UFRGS, atestado médico com CID — tel. 3308-2014
- **Desempenho acadêmico:** Resolução 19/2011 (desligamento por insuficiência) e Resolução 11/2013 (normas de graduação)
- **Programas Culturais:** https://www.ufrgs.br/difusaocultural/

---

## 13. Resolução 11/2013 — capítulos não indexados

**Decisão:** indexados apenas os artigos centrais de matrícula e trancamento  
**Motivo:** a resolução é extensa (91 artigos); muitos tratam de situações administrativas raras ou específicas demais para dúvidas de calouro.  
**Fonte:** PDF `Res-11-NORMAS-Basicas-da-Graduacao.pdf` / http://www.ufrgs.br/cepe/legislacao/resolucao-no-11-2013-de-24-04-2013  
**Conteúdo deixado de lado (potencialmente reaproveitável depois):**
- **Modalidades de ingresso (Arts. 7º-14):** transferência voluntária, ingresso de diplomado, transferência interna, transferência compulsória, PEC-G, discente cortesia — podem ir para `enrollment` se o escopo crescer
- **Regime didático (Arts. 32-43):** tipos de Atividades de Ensino, carga horária, hora-aula (50 min), crédito (15h), Plano de Ensino
- **Desempenho acadêmico (Arts. 44-51):** conceitos A/B/C/D/FF, reprovação por falta (FF acima de 25%), parâmetros TIM/TIMD/CID/CTC, revisão de conceito, recuperação
- **Diplomação e colação de grau (Arts. 54-59)**
- **Láurea Acadêmica (Art. 60):** critérios (80% conceitos A etc.)
- **Licenças e afastamentos acadêmicos (Arts. 61-64):** afastamento para estudos, complementação
- **Licenças por força maior (Arts. 65-70):** licença maternidade (120+60 dias), paternidade (8 dias), tratamento de saúde
- **Licenças por motivo de crença (Arts. 70-A a 70-C)**
- **Discente visitante e mobilidade acadêmica (Arts. 73-74)** — parcialmente relevante para `enrollment`
- **Dupla diplomação, revalidação de diplomas, controle de informações (Arts. 75-91)**

**Observação:** vários desses artigos (especialmente desempenho acadêmico, licenças e modalidades de ingresso) são candidatos naturais a uma expansão futura das categorias `enrollment` e `withdrawal`.

---

*Documento gerado durante a fase de coleta de dados do chatbot RAG para FAQ universitário da UFRGS.*  
*Autores: Anísio Lorentz e Arthur Camargo — Disciplina de PLN, UFRGS 2025/2.*
