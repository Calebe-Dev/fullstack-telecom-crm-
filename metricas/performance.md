# Métricas de Performance e Escala — OcHub

## Escala Atual do Sistema

| Dimensão | Valor |
|---|---|
| Módulos de feature (Angular) | 32 módulos |
| Serviços Angular (core) | 34 services |
| Rotas da aplicação | 28+ rotas lazy-loaded |
| Integrações externas ativas | 3 (Backend API, Google, Freepik) |
| Containers Docker em produção | 4 |
| Versões do SDK publicadas | 4 (v1.0.2 → v1.1.0) |
| Scripts de automação/migração | 40+ scripts |
| Sub-aplicação ia_righter | Independente com 7 sub-módulos |

---

## Performance de Carregamento

### Estratégia de Otimização

O OcHub implementa **preloading seletivo**: apenas módulos marcados com `data: { preload: 'navbar' }` nas rotas são pré-carregados após o login, usando a `NavbarPreloadingStrategy` customizada.

**Módulos pré-carregados (navegação imediata):**
- `companies`, `orders`, `os`, `crm`, `marketing`, `contacts`, `consultants`
- `services`, `operators`, `partners`, `offers`, `support`, `integrations`

**Módulos carregados sob demanda:**
- `ai-agents`, `server-manager`, `entities`, `workflows`, `reports`

---

## Limites de Infraestrutura (Produção)

| Container | RAM Limit | CPU Limit |
|---|---|---|
| `ochub-web` | 1.5 GB | Sem limite |
| `ochub-server-manager` | 512 MB | Sem limite |
| `ochub-ai-agent` | 512 MB | 0.5 vCPU |
| `ochub-monitor` | 256 MB | Sem limite |

---

## Performance do Sistema RAG

| Parâmetro | Configuração |
|---|---|
| Memória máxima para ingestão | 512 MB |
| Delay entre arquivos (modo lento) | 100ms |
| Frequência de save do índice | A cada 20 arquivos |
| Backend de embeddings | `@xenova/transformers` (local) |

---

## Timeouts Configuráveis (via Variáveis de Ambiente)

| Operação | Timeout Padrão |
|---|---|
| Auditoria de site — por página | 10.000ms |
| Auditoria de site — sitemap | 8.000ms |
| Máximo de URLs por auditoria | 80 URLs |
| Batch de auditoria paralela | 3 URLs simultâneas |
| Tempo máximo do AI Worker | 15 minutos (900.000ms) |

---

## Padrões de Qualidade

- **TypeScript strict** habilitado com `noEmit` via `npm run audit`
- **Testes unitários** via Karma + Jasmine para Angular
- **Testes do SDK** via Vitest
- **Healthcheck Docker** com retry de 3 tentativas e intervalo de 30s

---

## Observações

> Os valores de escala acima são baseados na análise estrutural do código-fonte (contagem de módulos, services, rotas e scripts). Métricas de tráfego real, número de usuários e volume de dados não são divulgadas por política de privacidade do cliente.
