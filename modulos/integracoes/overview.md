# Módulo: Integrações (integrations)

## Overview

O módulo Integrações centraliza as conexões do OcHub com serviços externos, especialmente o ecossistema Google Workspace. Gerencia tokens OAuth, provê interfaces de configuração e expõe status de cada integração ativa.

**Por que existe:** Diferentes features do OcHub (calendário de compromissos, sincronização de planilhas, armazenamento de documentos) dependem de APIs Google. O módulo centraliza o fluxo de autenticação e refresh de tokens.

---

## Entidades Principais

| Entidade | Tipo | Atributos Públicos |
|---|---|---|
| `IntegracaoGoogle` | model | usuario_id, status, escopos_ativos, data_conexao |
| `CalendarioConfig` | model | calendario_id_publico, nome_exibicao, sincronizado |
| `DriveConfig` | model | pasta_raiz, status_sync |

> Campos omitidos: [OMITIDO] access_token, refresh_token, client_secret — todos redactados por política de segurança.

---

## Fluxo Principal: Google OAuth 2.0

```mermaid
sequenceDiagram
    participant User as Usuário
    participant Angular as OcHub Angular
    participant API as api-server.js
    participant Google as Google OAuth

    User->>Angular: Clicar "Conectar Google"
    Angular->>API: GET /api/integrations/google/auth-url
    API-->>Angular: URL de autorização
    Angular->>Google: Redirecionar para OAuth consent
    Google-->>Angular: Callback com code
    Angular->>API: POST /api/integrations/google/callback {code}
    API->>Google: Trocar code por tokens
    Google-->>API: access_token + refresh_token
    API->>Backend API: Salvar tokens (criptografados)
    API-->>Angular: Status de integração ativa
```

---

## Fluxo: Renovação Automática de Token

```mermaid
flowchart TD
    Chamada["Chamada a API Google"] --> ChecaToken{Token válido?}
    ChecaToken -->|Sim| Executa["Executa operação"]
    ChecaToken -->|Expirado| Refresh["Solicita refresh\nvia googleapis"]
    Refresh --> Salva["Salva novo token\nno Backend API"]
    Salva --> Executa
    Executa --> Resposta["Retorna resultado"]
```

---

## Padrão Arquitetural

**Facade Pattern** — O `google-auth.service.ts` e o `google-mirror.service.ts` encapsulam toda a complexidade do OAuth e das APIs Google, expondo métodos simples para os módulos consumidores (Calendar, Drive, Sheets).

---

## Serviços Core Envolvidos

- `google-auth.service.ts` — Gestão de autenticação e tokens
- `google-calendar.service.ts` — Operações de calendário
- `google-drive.service.ts` — Upload e leitura de arquivos
- `google-sheets.service.ts` — Leitura/escrita em planilhas
- `google-mirror.service.ts` — Proxy intermediário para chamadas Google

---

## Pontos Fortes

- ✅ Renovação de token transparente sem logout do usuário
- ✅ Health check específico para o status da integração Google (`GET /api/health`)
- ✅ Diagnóstico detalhado por stage em caso de falha (stage: `users_me` | `integration_lookup`)

---

## Sugestões de Melhoria

- 🔧 Suporte a múltiplos provedores OAuth (Microsoft 365, Slack)
- 🔧 Tela de gerenciamento de escopos ativos com revogação granular
- 🔧 Alertas proativos quando integração está próxima de expirar

---

## Relevância para Portfolio: ⭐⭐⭐⭐ (4/5)

Implementação completa de fluxo OAuth 2.0 com renovação automática de token e múltiplos serviços Google integrados. Padrão comum em produtos SaaS empresariais.
