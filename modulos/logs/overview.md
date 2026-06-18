# Módulo: Logs do Sistema

> **Rota:** `/logs` | **Condição:** mesma permissão de `health` | **Ícone:** `terminal`

## Responsabilidade

Interface de visualização e busca dos logs estruturados gerados pela aplicação Angular SSR e pela API backend. Permite que administradores e times de TI depurem problemas, acompanhem fluxos e auditem eventos sem acesso direto ao servidor.

---

## Padrão Arquitetural

**Log Streaming + Buffer** — os logs são gerados pelo `LoggerService` no frontend (via `console` + endpoint da API) e pelo sistema de logging da API backend. A tela de Logs consome o endpoint de streaming da API via SSE (Server-Sent Events) ou polling configurável.

---

## Estrutura de um Log

```typescript
interface LogEntry {
  timestamp: string;     // ISO 8601
  level: 'DEBUG' | 'INFO' | 'WARN' | 'ERROR';
  module: string;        // Ex: 'NAVBAR', 'CRM_SERVICE', 'AUTH'
  action: string;        // Ex: 'LOAD_STATE', 'LOGOUT_CLICK'
  message: string;       // Mensagem legível
  context?: object;      // Dados adicionais (sem dados sensíveis)
  userId?: string;       // Usuário que gerou o log
}
```

---

## Funcionalidades da Tela

| Funcionalidade | Descrição |
|---|---|
| Filtro por nível | DEBUG, INFO, WARN, ERROR |
| Filtro por módulo | Lista de módulos da aplicação |
| Busca por texto | Full-text no campo `message` |
| Streaming em tempo real | Novos logs aparecem sem recarregar |
| Exportação | Download em JSON ou CSV para análise |
| Janela de tempo | Filtro por período (última hora, hoje, etc.) |

---

## Exemplo de Logs Relevantes

```
[INFO]  NAVBAR         LOAD_STATE       Navbar carregada — 12 módulos visíveis
[INFO]  CRM_SERVICE    getTasks         Sucesso — 47 tarefas carregadas
[WARN]  AUTH           TOKEN_REFRESH    Token expirado — renovando silenciosamente
[ERROR] CRM_SERVICE    updateTask       Falha ao atualizar tarefa: 403 Forbidden
```

---

## Pontos Fortes

- ✅ Logs estruturados facilitam parsing e análise automatizada
- ✅ Módulo e ação identificados em cada log — rastreabilidade precisa
- ✅ Sem dados sensíveis nos logs — conformidade com segurança

## Sugestões de Melhoria

- 🔧 Integração com ferramentas externas (Grafana Loki, Datadog)
- 🔧 Alertas automáticos para ERRORs acima de threshold
- 🔧 Correlação de logs por request-id para rastrear fluxos completos

---

## Relevância para Portfolio: ⭐⭐⭐⭐ (4/5)
