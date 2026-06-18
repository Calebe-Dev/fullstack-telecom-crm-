# Módulo: System Health (Monitoramento)

## Overview

O módulo System Health provê dashboards e ferramentas de diagnóstico da plataforma OcHub em tempo real. Inclui visualização de logs estruturados, status de conectividade com serviços externos e monitoramento de métricas de performance do sistema.

**Por que existe:** Em produção, falhas transitórias com o Backend API, Google APIs ou o worker de IA precisam ser diagnosticadas rapidamente sem acesso ao terminal do servidor.

---

## Entidades Principais

| Entidade | Tipo | Atributos Públicos |
|---|---|---|
| `HealthStatus` | model | servico, status, latencia_ms, ultima_verificacao |
| `LogEntry` | model | timestamp, nivel, mensagem, modulo, request_id |
| `MetricaNavegacao` | model | rota, tempo_carregamento_ms, timestamp |

---

## Fluxo: Dashboard de Saúde

```mermaid
flowchart TD
    Dashboard["HealthDashboardComponent"] --> APIHealth["GET /api/health"]
    APIHealth --> Backend API{{"Backend API\nStatus"}}
    APIHealth --> Google{{"Google API\nStatus"}}
    APIHealth --> AIAgent{{"AI Worker\nStatus"}}
    Backend API --> Dashboard
    Google --> Dashboard
    AIAgent --> Dashboard
    Dashboard --> Display["Exibir cards\ncom status + latência"]
```

---

## Padrão Arquitetural

**Polling leve** — O dashboard realiza polling periódico ao endpoint `/api/health` para manter status atualizado sem necessidade de WebSocket. Os logs são carregados via `GET /api/logs` com paginação.

---

## Pontos Fortes

- ✅ Diagnóstico granular por estágio de falha (ex: `stage: users_me`)
- ✅ Logs estruturados com level, módulo e request_id para rastreabilidade
- ✅ Visibilidade de performance de navegação coletada automaticamente

---

## Sugestões de Melhoria

- 🔧 Substituir polling por WebSocket para atualizações em tempo real
- 🔧 Adicionar alertas automáticos por e-mail/Slack quando serviço fica offline
- 🔧 Histórico de uptime com gráfico de disponibilidade por período

---

## Relevância para Portfolio: ⭐⭐⭐ (3/5)

Demonstra preocupação com observabilidade em produção, diferenciando projetos maduros de MVPs.
