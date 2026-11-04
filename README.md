# Gabriel Draco

### Data Engineering | Data Analytics | Python | SQL | PostgreSQL

Analista de Dados em transição para **Engenharia de Dados** e estudante de **Ciência de Dados e Inteligência Artificial na Universidade Veiga de Almeida (UVA)**. Construo pipelines que recebem dados de origens desorganizadas (APIs públicas, mensagens em texto livre, planilhas), tratam, validam, persistem e disponibilizam para consumo por API e dashboard.

Meu foco é desenvolver pipelines confiáveis, estruturar dados de diferentes fontes e transformar informação bruta em recurso útil para análise e tomada de decisão. Combino fundamentos de Engenharia de Software, Engenharia de Dados e Analytics, com desenvolvimento prático, testes e validação técnica.

Em busca de oportunidades em Engenharia de Dados, Analytics Engineering e Backend com dados.

---

## Tecnologias e ferramentas

**Linguagens e desenvolvimento**
- Python, SQL, JavaScript, HTML5 e CSS3

**Engenharia de Dados**
- ETL / ELT, ingestão e integração de dados
- Consumo de APIs REST com paginação, retry, timeout e backoff exponencial
- Parsing, normalização e enriquecimento por tabelas de referência
- Validação e qualidade de dados
- Persistência idempotente (UPSERT), deduplicação por chave de negócio
- Checkpoints e retomada de processamento
- PostgreSQL, SQLAlchemy, Alembic
- JSON / JSONB, hash SHA-256 para detecção de alterações

**Backend e APIs**
- FastAPI, REST APIs, Pydantic
- Padrão Repository, arquitetura em camadas (API, serviço, repositório, persistência)
- Node.js, TypeScript

**Qualidade e entrega**
- Pytest (parser, clientes de API, CLI, rotas, integração com PostgreSQL, migrações)
- GitHub Actions (CI com PostgreSQL, `pip check`, `pip-audit`, checagem de sintaxe JS)
- Git e GitHub

**Analytics e Business Intelligence**
- Power BI, Excel
- Análise exploratória e descritiva de dados
- Indicadores e visualização de informações

**Ambiente**
- Linux, VS Code, DBeaver, pgAdmin

**Em estudo**
- Docker e conteinerização
- Cloud e serviços de infraestrutura
- Modelagem de dados (Data Warehouse, Data Lake)
- Machine Learning e aplicações de IA

---

## Projetos em destaque

### [NEXUS: Engenharia de Dados e Analytics para Licitações Públicas](https://github.com/gdracojj/nexus)

Plataforma independente que coleta, organiza e disponibiliza dados públicos do Portal Nacional de Contratações Públicas (PNCP), para que analistas de licitação consultem e acompanhem oportunidades. Nasceu de uma necessidade real de negócio.

**Fluxo de ingestão:** CLI de coleta → serviço de sincronização → cliente PNCP → parser → repositório → PostgreSQL
**Fluxo de consulta:** interface web → FastAPI → serviço → repositório

**Ingestão e resiliência**
- Integração com a API REST do PNCP com ingestão paginada, orquestração por unidade federativa e coleta nacional.
- Timeout, até 5 tentativas, backoff exponencial, tratamento de erros HTTP, respeito ao `Retry-After` e ao limite de requisições (429).
- Coleta via CLI separada do caminho de leitura HTTP.
- Lock consultivo (advisory lock) do PostgreSQL para evitar coletas concorrentes.
- Histórico de sincronização, checkpoints por página gravados na mesma transação da persistência e retomada de processos interrompidos.
- Reaproveitamento de resultados recentes.

**Dados e persistência**
- Parsing, normalização e validação de registros.
- Modelagem relacional com PostgreSQL, SQLAlchemy e migrações com Alembic.
- UPSERT transacional e idempotente, em lotes de até 250 chaves, com `numeroControlePNCP` como chave única.
- Hash SHA-256 para identificar alterações e payload original preservado em JSONB para rastreabilidade.

**API e interface**
- API REST com FastAPI: filtros por UF, termo e prazo, validação de parâmetros e paginação limitada.
- Interface web em JavaScript, HTML e CSS puros, com visões de tabela, linha do tempo e quadro, estados de carregamento e erro, cancelamento de requisição e indicação de atualidade e completude dos dados.

**Qualidade e segurança**
- Testes de parser, cliente PNCP, CLI, rotas, integração com PostgreSQL em schema isolado, migrações, concorrência de coleta e caminhos de falha.
- CI no GitHub Actions: PostgreSQL 16, Python 3.10 e 3.14, `pip check`, `pip-audit` e checagem de sintaxe JS.
- Auditoria de segurança: variáveis de ambiente e proteção do `.env`, SQL parametrizado, validação de entrada, tratamento de erros, headers HTTP de segurança e CSP.

**Desenvolvimento orientado a especificação (SDD):** escrevi e validei as especificações (arquitetura, ingestão, segurança, testes), decomponho em tarefas, implemento com apoio de Claude Code, rodo testes independentes, reviso com foco em segurança e valido no CI.

**Tecnologias:** Python · FastAPI · PostgreSQL · SQLAlchemy · Alembic · Requests · Pytest · GitHub Actions · JavaScript · HTML · CSS

**Status:** projeto independente, fora de produção. A validação operacional completa da coleta nacional ainda está pendente.

<!-- Adicionar aqui: print da interface e/ou diagrama do fluxo de ingestão
![NEXUS](docs/nexus-interface.png)
-->

---

### VTAL CCOR V2 / [ControlOps](https://github.com/gdracojj/ControlOps): Pipeline de Dados Operacionais

Solução que criei e desenvolvi do início ao fim na PD7 Technology, em produção em servidor da empresa, para automatizar a validação de informações de assunção de serviço. O fluxo transforma mensagens operacionais não estruturadas do WhatsApp em registros estruturados, compara com tabelas de referência e classifica cada ocorrência.

**Fluxo:** mensagens do WhatsApp Web → ingestão → parsing e padronização → enriquecimento por tabelas dimensão (escalas, colaboradores, postos, regras de plantão) → validação e identificação de divergências → classificação por regras de negócio → persistência idempotente em PostgreSQL → dashboard operacional

**Principais implementações**
- Parsing de mensagens em texto livre, com extração e normalização de nomes, postos e horários.
- Matching textual aproximado (RapidFuzz) e aplicação de regras de negócio.
- Classificação das ocorrências: regular, atrasada, antecipada, divergente e ausente.
- Persistência idempotente em PostgreSQL.
- Integração entre serviços (Python/FastAPI e Node.js/TypeScript) e API REST para o dashboard.
- Testes automatizados, incluindo validação do parser.

**Impacto operacional:** redução de aproximadamente 1h30 por ciclo de conferência manual.

**ControlOps:** é este mesmo projeto em refatoração para uma versão pública de portfólio, com dados mockados, sem referências à empresa. A refatoração está em andamento.

**Tecnologias:** Python · FastAPI · Node.js · TypeScript · PostgreSQL · Pydantic · Jinja2 · RapidFuzz · Pytest

<!-- Adicionar aqui: print do dashboard do ControlOps
![ControlOps](docs/controlops-dashboard.png)
-->

---

## Experiência

**Analista de Dados** · PD7 Technology · fevereiro a outubro de 2026 (promovido de Operador Predial)
Projetos de dados, BI e automação:
- **VTAL CCOR V2:** pipeline de dados operacionais (acima).
- **CCF:** dashboard financeiro que consolida a receita das verticais da empresa. Fluxo: Google Sheets → Google Sheets API (service account) → Power BI, com atualização agendada. Em produção.
- **PD7 AI First:** atuação como pesquisador de tecnologia, com entrevistas com gestores e supervisores, questionários, priorização por matriz e documentação executiva.

**Analista de Dados (PJ)** · RCCS Licitações · julho/2023 a fevereiro/2026
Análise exploratória e descritiva de dados de compras, estoque, fornecedores, pedidos e licitações, com Excel, Power BI e ERP Bling, para inteligência comercial e controle operacional. Análise histórica em Power BI.

---

## Formação

**Ciência de Dados e Inteligência Artificial**: Universidade Veiga de Almeida (UVA), 2026 a 2028

**FIAP, Big Data & Analytics (conhecimento acadêmico):** Data Mining, Text Mining, Opinion Mining, governança de Big Data, Machine Learning, R, Tableau, Spark, MongoDB, NoSQL, Hadoop e Neo4j.

**Fundação Bradesco:** Excel e Power BI.

**Idiomas:** Português (nativo) · Inglês (B2) · Espanhol (básico)

---

## Como trabalho com IA

Uso Claude Code e Codex para acelerar o desenvolvimento. Eu defino os requisitos, escrevo as especificações, decomponho as tarefas e reviso o código, e nada entra sem teste e CI passando.

---

## Contato

- **GitHub:** [github.com/gdracojj](https://github.com/gdracojj)
- **LinkedIn:** [gabriel-silva-550525337](https://www.linkedin.com/in/gabriel-silva-550525337/)
- **E-mail:** gabrielmrc70@gmail.com
