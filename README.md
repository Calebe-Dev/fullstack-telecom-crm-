# OcHub — Plataforma de Gestão Operacional para Distribuidoras de Telecomunicações

> **Elevator Pitch:** Sistema web full-stack que centraliza operações de CRM, vendas, suporte técnico e marketing para distribuidoras de telecomunicações, unificando dezenas de fluxos antes dispersos em planilhas e ferramentas desconectadas.

---

## O que é o OcHub?

O OcHub é uma **plataforma administrativa interna** construída com Angular 20 (SSR) + Node/Express, projetada para orquestrar as operações de um grupo de distribuidoras de telecomunicações. Ele integra:

- **CRM completo** com gestão de clientes, empresas, contatos, parceiros e consultores
- **Gestão de Ordens de Serviço (OS)** com rastreamento de status e automação
- **Pipeline de Pedidos** com ciclo de vida completo e relatórios
- **Módulo de Marketing** com agendamento, publicação automática e auditoria de sites
- **Agentes de IA** integrados para geração de conteúdo e automação editorial
- **Painel de Saúde do Sistema** com monitoramento em tempo real
- **SDK próprio** (`@grupooc/ochub-sdk`) para integrações externas

---

## Arquitetura de Alto Nível

```
┌──────────────────────────────────────────────────────────┐
│                    OcHub Web App                          │
│           Angular 20 + SSR (server-side rendering)       │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌─────────┐  │
│  │  CRM     │  │Marketing │  │   OS     │  │  AI     │  │
│  │ Module   │  │ Module   │  │ Module   │  │ Agents  │  │
│  └──────────┘  └──────────┘  └──────────┘  └─────────┘  │
└──────────────────────────┬───────────────────────────────┘
                           │ HTTP / Proxy
┌──────────────────────────▼───────────────────────────────┐
│              api-server.js (Express 5)                    │
│   Logs · Marketing · Auditoria · Integrações · Saúde     │
└──────────────────────────┬───────────────────────────────┘
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
    [Backend API]   [Google APIs]   [Freepik API]
```

---

## Módulos Principais

| Módulo | Responsabilidade |
|---|---|
| `auth` | Autenticação via Google OAuth + controle de sessão |
| `crm` | Pipeline de leads, funil de vendas e histórico |
| `orders` | Gestão de pedidos com ciclo de vida completo |
| `os` | Ordens de Serviço técnicas com rastreamento de status |
| `marketing` | Agendamento e publicação de conteúdo em múltiplos sites |
| `ai-agents` | Interface para agentes de IA editoriais |
| `integrations` | Hub de integrações externas (Google Workspace) |
| `reports` | Relatórios operacionais e dashboards |
| `system-health` | Monitoramento e logs do sistema |
| `server-manager` | Gerenciamento de infraestrutura via UI |

---

## Tecnologias

![Angular](https://img.shields.io/badge/Angular-20-DD0031?style=flat&logo=angular)
![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=flat&logo=typescript)
![Node.js](https://img.shields.io/badge/Node.js-20-339933?style=flat&logo=node.js)
![Express](https://img.shields.io/badge/Express-5-000000?style=flat&logo=express)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat&logo=docker)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3-06B6D4?style=flat&logo=tailwindcss)

---

## Execução Local (Desenvolvimento)

```bash
npm install
npm run dev          # Sobe frontend (porta 8899) + API (porta 3001)
```

---

## Status do Projeto

🟢 **Em Produção** — Sistema ativo com deploy via Docker Compose em servidor dedicado.
