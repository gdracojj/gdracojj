# Gabriel Draco

### Engenharia de Dados · Python · SQL · PostgreSQL

Analista de Dados em transição para **Engenharia de Dados**, estudante de Ciência de Dados e Inteligência Artificial na UVA. Construo pipelines que pegam dados de origens desorganizadas (APIs públicas, mensagens de texto livre, planilhas), validam, persistem e entregam para consumo por API e dashboard.

Atualmente em busca de oportunidades em Engenharia de Dados, Analytics Engineering e Backend com dados.

---

## Stack

| Área | Tecnologias |
|---|---|
| **Linguagens** | Python, SQL, JavaScript, HTML/CSS |
| **Engenharia de Dados** | ETL/ELT, ingestão via API, parsing e normalização, validação, idempotência (upsert), checkpoints |
| **Banco de dados** | PostgreSQL, SQLAlchemy, Alembic, JSON/JSONB |
| **Backend** | FastAPI, REST, Pydantic, Node.js |
| **Qualidade e entrega** | Pytest, Git/GitHub, GitHub Actions (CI) |
| **BI e Analytics** | Power BI, Excel, análise exploratória |
| **Ambiente** | Linux, VS Code, DBeaver |

**Em estudo:** Docker, Cloud, modelagem de dados (DW/Data Lake), Machine Learning.

---

## Projetos

### [NEXUS](https://github.com/gdracojj/nexus): ingestão e consulta de licitações públicas

Projeto independente que coleta dados do Portal Nacional de Contratações Públicas (PNCP) e os disponibiliza para analistas de licitação consultarem com filtros.

**Fluxo:** API do PNCP → cliente com retry → parser e validação → repositório → PostgreSQL → API FastAPI → interface web

- Ingestão paginada com retry, timeout, backoff exponencial e respeito ao `Retry-After`.
- Upsert idempotente com chave externa única (`numeroControlePNCP`) e lock consultivo do PostgreSQL contra coletas concorrentes.
- Hash SHA-256 para detectar alterações e payload original preservado em JSONB para rastreabilidade.
- Histórico de execuções e retomada a partir de checkpoints por página, gravados na mesma transação da persistência.
- API REST com filtros (UF, termo, prazo), validação de parâmetros e paginação limitada.
- Interface web em JavaScript puro, com visões de tabela, linha do tempo e quadro, e indicação de atualidade e completude dos dados.
- Testes de parser, cliente PNCP, CLI, rotas e integração com PostgreSQL; CI no GitHub Actions com PostgreSQL 16.

**Desenvolvimento orientado a especificação:** escrevi e validei as specs (arquitetura, ingestão, segurança, testes), decomponho em tarefas, uso Claude Code para implementar, e reviso o resultado com foco em segurança antes do CI.

**Stack:** Python · FastAPI · PostgreSQL · SQLAlchemy · Alembic · Requests · Pytest · GitHub Actions · JavaScript

**Status:** projeto independente, fora de produção. A validação operacional da coleta nacional completa ainda está pendente.

<!-- Adicionar aqui: print da interface e/ou diagrama do fluxo de ingestão
![NEXUS](docs/nexus-interface.png)
-->

---

### VTAL CCOR V2 / [ControlOps](https://github.com/gdracojj/ControlOps): pipeline de dados operacionais

Desenvolvido por mim, do início ao fim, na PD7 Technology, e rodou em produção em servidor da empresa. Transforma mensagens de WhatsApp em texto livre em registros estruturados para conferência de assunção de serviço.

**Fluxo:** mensagens do WhatsApp Web → parsing e padronização → enriquecimento com tabelas de referência (escalas, colaboradores, postos) → classificação por regras de negócio (regular, atrasada, antecipada, divergente, ausente) → persistência idempotente em PostgreSQL → dashboard operacional

- Testes automatizados.
- **Impacto:** redução de aproximadamente 1h30 por ciclo de conferência manual.
- O ControlOps é a versão de portfólio pública do mesmo projeto, com dados fictícios e sem referências à empresa.

**Stack:** Python · FastAPI · Node.js · TypeScript · PostgreSQL · RapidFuzz · Pytest

<!-- Adicionar aqui: print do dashboard do ControlOps
![ControlOps](docs/controlops-dashboard.png)
-->

---

## Experiência

**Analista de Dados** · PD7 Technology · até setembro de 2026
Projetos de dados, BI e automação. Entre eles o VTAL CCOR V2 (acima) e o CCF, dashboard financeiro que consolida a receita das verticais da empresa a partir de Google Sheets, via Google Sheets API, com atualização agendada no Power BI.

**Analista de Dados (PJ)** · RCCS Licitações · jul/2023 a fev/2026
Análise exploratória e descritiva de dados de compras, estoque, fornecedores, pedidos e licitações, com Excel e Power BI, para inteligência comercial e controle operacional.

---

## Formação

- **Ciência de Dados e Inteligência Artificial**, Universidade Veiga de Almeida (UVA), 2026–2028
- **Big Data & Analytics**, FIAP (conteúdo acadêmico: Data Mining, Machine Learning, Spark, MongoDB, Tableau, entre outros)
- **Excel e Power BI**, Fundação Bradesco

**Idiomas:** Português (nativo) · Inglês (B2) · Espanhol (básico)

---

## Como trabalho com IA

Uso Claude Code e Codex para acelerar o desenvolvimento. Quem define os requisitos, escreve as especificações e revisa o código sou eu, e nada entra sem teste e CI passando.

---

## Contato

- **GitHub:** [github.com/gdracojj](https://github.com/gdracojj)
- **LinkedIn:** [gabriel-silva2270](https://www.linkedin.com/in/gabriel-silva2270/)
- **E-mail:** gabrielmrc70@gmail.com
