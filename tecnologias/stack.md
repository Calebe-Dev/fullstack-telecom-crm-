# Stack Técnica — OcHub

## Framework Principal

### Angular 20 (com SSR)
**Versão:** `^20.3.0`
**Justificativa:** Framework enterprise-grade com suporte nativo a SSR via `@angular/ssr`. A versão 20 introduz signals e standalone components como padrão, reduzindo boilerplate. Escolhido pela tipagem forte, ecosystem maduro e CLI poderosa.

**Recursos Angular utilizados:**
- Standalone Components (sem NgModule tradicional)
- Lazy loading por rota com `loadChildren` e `loadComponent`
- Server-Side Rendering via `@angular/ssr`
- Angular CDK para componentes de UI sem opinião

---

## Backend / API

### Node.js 20 + Express 5
**Justificativa:** Express 5 traz suporte nativo a async/await sem wrappers, melhor tratamento de erros e performance ligeiramente superior. Node 20 está na versão LTS ativa.

**Uso:** API companion (`api-server.js`) responsável por:
- Webhooks e cron jobs de marketing
- Proxy de requisições Freepik (proteção de chave)
- Auditoria de sites (scraping, análise SEO)
- Streaming de logs
- Health check centralizado

### node-cron `^3.0.3`
**Justificativa:** Agendamento de tarefas sem dependência de infraestrutura externa (sem Redis, sem Celery). Adequado para volume de jobs do projeto.

---

## CMS / Backend-as-a-Service

### Backend API (Headless CMS)
**Justificativa:** Elimina a necessidade de um backend customizado para CRUD. Oferece API REST e GraphQL gerada automaticamente a partir do schema do banco. O sistema de permissões por role reduz código de autorização no frontend.

**Integração:** Via variáveis de ambiente (`BACKEND_URL`, `BACKEND_TOKEN`). O Angular consome diretamente os endpoints `/items/*`, `/auth/*` e `/users/*` via proxy.

---

## Banco de Dados e ORM

Gerenciado inteiramente pelo Backend API (sem acesso direto ao banco no código da aplicação). O banco subjacente é configurado no ambiente Backend API.

---

## Linguagem

### TypeScript 5.9
**Justificativa:** Tipagem estática obrigatória em todo o projeto. Interfaces de modelo definidas em `src/app/models/` e `src/app/features/*/models/` garantem contratos claros entre camadas.

---

## Estilização

### TailwindCSS 3
**Justificativa:** Utility-first CSS com purge automático. Integrado via `postcss.config.cjs`. Permite prototipagem rápida de UI sem criar arquivos CSS customizados para cada componente.

---

## Containerização

### Docker + Docker Compose
**Justificativa:** Garantia de paridade entre ambientes de desenvolvimento e produção. O `docker-compose.yml` orquestra 4 serviços independentes com limites de memória configuráveis via variáveis de ambiente.

**Serviços:**
- `ochub-web` — Aplicação principal (Angular SSR + API Express)
- `ochub-monitor` — Health check de infraestrutura
- `ochub-server-manager` — Painel de gerenciamento de servidor (:9090)
- `ochub-ai-agent` — Worker isolado para tarefas de IA

---

## Integrações Externas

| Serviço | Biblioteca | Categoria |
|---|---|---|
| Google OAuth 2.0 | `googleapis ^170` | auth |
| Google Calendar | `googleapis` | api |
| Google Drive | `googleapis` | api |
| Google Sheets | `googleapis` | api |
| Backend API REST API | Fetch nativo | db/cms |
| Freepik | axios (proxy interno) | api/media |
| WordPress | Plugin PHP customizado | api/cms |

---

## Ferramentas de Desenvolvimento

| Ferramenta | Uso |
|---|---|
| `tsx ^4.21` | Execução direta de TypeScript no Node sem build |
| `concurrently ^9.2` | Rodar frontend + API em paralelo no dev |
| `papaparse ^5.5` | Parsing de CSVs para importação de dados |
| `xlsx ^0.18` | Leitura de planilhas Excel em scripts de migração |
| `@xenova/transformers ^2.17` | Geração de embeddings local para o sistema RAG |
| `lucide-angular ^0.563` | Ícones consistentes em toda a interface |
| Karma + Jasmine | Testes unitários do Angular |

---

## RAG (Retrieval-Augmented Generation)

Sistema de indexação semântica local do codebase:
- **Ingestão:** `scripts/rag/ingest.js` gera embeddings via `@xenova/transformers`
- **Consulta:** `scripts/rag/query.js` realiza busca semântica no índice local
- **Propósito:** Permite que agentes de IA consultem contexto do projeto sem expor código a APIs externas

---

## SDK Próprio

### @grupooc/ochub-sdk v1.1.0
**Repositório:** `sdk/ochub-sdk/`
**Distribuição:** `.tgz` (pacote local e distribuição para parceiros)
**Conteúdo:** Clientes tipados para CRM, CMS, SSG e operações estáticas

---

## Módulo de IA Editorial (ia_righter)

Sub-aplicação independente com seu próprio `package.json` e estrutura:
- `src/core/` — Motor de geração
- `src/scrapers/` — Coleta de conteúdo
- `src/skills/` — Prompts e habilidades especializadas
- `src/workflows/` — Orquestração de pipelines editoriais
- `src/config/` — Configuração por site
