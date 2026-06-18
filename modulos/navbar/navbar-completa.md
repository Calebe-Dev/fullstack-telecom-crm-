# Navbar — Mapa Completo de Opções

## Visão Geral

A navbar do OcHub é uma sidebar fixa lateral esquerda (`w-64`, `h-screen`) com gradiente azul-índigo, implementada em [`navbar.component.ts`](file:///Users/calebearaujo/Documents/GitHub/ochub-static-web-microservice/src/app/core/layout/navbar/navbar.component.ts). Todas as opções são controladas por **RBAC via `PermissionsService`** — cada item só aparece se o usuário tiver acesso ao módulo correspondente (`canNav(moduleId)`).

---

## Mecanismo de Controle de Acesso

```
perms.canViewNav()(moduleId) → true/false
```

Cada item de menu verifica `canNav('module.id')` antes de renderizar. Se o usuário não tiver nenhum item visível em um grupo, o **cabeçalho do grupo também some** (`showAnyNav([...])`). Isso garante que usuários sem permissão vejam apenas o que é relevante.

---

## Estrutura da Sidebar

```
┌─────────────────────────────────┐
│  [Header] OcHub logo + Notif.   │
├─────────────────────────────────┤
│  ── PRINCIPAL ──                │
│   Clientes                      │
│   Tarefas                       │
│   Compromissos *(Google)        │
│   Times                         │
│   Adesivos                      │
│   Leads                         │
│   Ordens de Serviço             │
├─────────────────────────────────┤
│  ── GESTÃO ──                   │
│   Relatórios                    │
│   Pedidos                       │
│   Contratos                     │
│   Documentos                    │
│   Histórico                     │
│   Contatos                      │
│   Consultores                   │
│   Operadoras                    │
│   Credenciais                   │
│   Parceiros                     │
│   Usuários                      │
├─────────────────────────────────┤
│  ── RECURSOS ──                 │
│   Serviços                      │
│   Ofertas                       │
│     └─ Apps *(sub-item)         │
│   Suporte                       │
├─────────────────────────────────┤
│  ── MARKETING ──                │
│   Sites                         │
│   Artigos                       │
│   Ferramentas SEO               │
│   Marketing/SEO                 │
│   Auditoria de Sites            │
│   Agentes de IA                 │
│   Integrações                   │
│     ├─ Widgets & Scripts        │
│     ├─ Identidade Visual        │
│     ├─ Banners Personalizados   │
│     └─ Formulários de Captura   │
├─────────────────────────────────┤
│  ── SISTEMA ──                  │
│   Empresas (PJ)                 │
│   Filiais                       │
│   Pessoas (PF)                  │
│   Endereços                     │
│   Workflows                     │
│   Diagnóstico                   │
│   Logs do Sistema               │
├─────────────────────────────────┤
│  ── ADMINISTRAÇÃO DE TI ──      │
│   Servidor e Infra              │
├─────────────────────────────────┤
│  [Footer]                       │
│   Profile Widget                │
│   Status do Usuário             │
│   Modo Claro/Escuro             │
│   Trilhas de Conhecimento       │
│   Sair do Sistema               │
└─────────────────────────────────┘
```

---

## Grupo PRINCIPAL

### 🏢 Clientes
- **Rota:** `/companies`
- **Módulo ID:** `companies`
- **Ícone:** `building-2`
- **Responsabilidade:** Cadastro e gestão de empresas e pessoas físicas clientes do grupo. Ponto de entrada para o CRM — a partir do cliente, acessa-se contratos, pedidos, OS e histórico.
- **Doc:** [`modulos/crm/overview.md`](./modulos/crm/overview.md)

### ✅ Tarefas
- **Rota:** `/crm` (exact match)
- **Módulo ID:** `crm.tasks`
- **Ícone:** `check-square`
- **Responsabilidade:** Central de tarefas com visualização Kanban, Lista, Semana e Mês. Controla o ciclo de vida de atividades internas — criação, atribuição, priorização, recorrência e arquivamento.
- **Doc:** [`modulos/navbar/tarefas.md`](./modulos/navbar/tarefas.md)

### 📅 Compromissos *(condicional — requer Google conectado)*
- **Rota:** `/compromissos`
- **Condição:** `perms.hasGoogleEnabled()`
- **Ícone:** `calendar`
- **Responsabilidade:** Visualização de eventos do Google Calendar do usuário. Só aparece se o usuário tiver a integração Google ativa.

### 👥 Times
- **Rota:** `/crm/teams`
- **Módulo ID:** `crm.teams`
- **Ícone:** `users`
- **Responsabilidade:** Gerenciamento de equipes que recebem tarefas coletivas. Times podem ser atribuídos a tarefas, e membros do time herdam visibilidade dessas tarefas.

### 🏷️ Adesivos
- **Rota:** `/crm/stickers`
- **Módulo ID:** `crm.stickers`
- **Ícone:** `tag`
- **Responsabilidade:** CRUD de etiquetas coloridas (`CrmAdesivo`) usadas para categorizar e filtrar tarefas visualmente.

### 🎯 Leads
- **Rota:** `/crm/leads`
- **Módulo ID:** `crm.leads`
- **Ícone:** `target`
- **Responsabilidade:** Pipeline de oportunidades de venda. Leads passam por funil de qualificação → negociação → conversão em pedido.

### 📄 Ordens de Serviço
- **Rota:** `/os`
- **Módulo ID:** `os`
- **Ícone:** `file-text`
- **Responsabilidade:** Gestão do ciclo técnico de atendimento pós-venda: instalações, manutenções, portabilidades.
- **Doc:** [`modulos/os/overview.md`](./modulos/os/overview.md)

---

## Grupo GESTÃO

### 📊 Relatórios
- **Rota:** `/reports`
- **Módulo ID:** `reports`
- **Ícone:** `bar-chart-2`
- **Responsabilidade:** Dashboards e relatórios consolidados de performance operacional.

### 📦 Pedidos
- **Rota:** `/orders`
- **Módulo ID:** `orders`
- **Ícone:** `package`
- **Responsabilidade:** Ciclo de vida de pedidos comerciais — criação, aprovação, conclusão e cancelamento.

### 📝 Contratos
- **Rota:** `/contracts`
- **Módulo ID:** `contracts`
- **Ícone:** `file-signature`
- **Responsabilidade:** Gestão de contratos vigentes com clientes e parceiros.

### 📁 Documentos
- **Rota:** `/documents`
- **Módulo ID:** `documents`
- **Ícone:** `folder`
- **Responsabilidade:** Repositório de documentos vinculados a clientes e processos.

### 🕰️ Histórico
- **Rota:** `/negotiation-history`
- **Módulo ID:** `negotiation-history`
- **Ícone:** `history`
- **Responsabilidade:** Registro cronológico de negociações e interações comerciais.

### 👤 Contatos
- **Rota:** `/contacts`
- **Módulo ID:** `contacts`
- **Ícone:** `user-plus`
- **Responsabilidade:** Pessoas físicas de contato associadas a empresas clientes.

### 🤝 Consultores
- **Rota:** `/consultants`
- **Módulo ID:** `consultants`
- **Ícone:** `user-check`
- **Responsabilidade:** Consultores de vendas do grupo — perfil, especialidade e filial.

### 📡 Operadoras
- **Rota:** `/operators`
- **Módulo ID:** `operators`
- **Ícone:** `radio`
- **Responsabilidade:** Cadastro de operadoras de telecomunicações parceiras (Vivo, Claro, etc.) e seus planos.

### 🔑 Credenciais
- **Rota:** `/credentials`
- **Módulo ID:** `credentials`
- **Ícone:** `key`
- **Responsabilidade:** Gerenciamento de credenciais de acesso a sistemas de parceiros.

### 🤜 Parceiros
- **Rota:** `/partners`
- **Módulo ID:** `partners`
- **Ícone:** `handshake`
- **Responsabilidade:** Empresas parceiras com configurações comerciais e de acesso.

### 🛡️ Usuários
- **Rota:** `/users`
- **Módulo ID:** `users`
- **Ícone:** `shield`
- **Responsabilidade:** Administração de usuários do OcHub com roles e permissões.

---

## Grupo RECURSOS

### 🔧 Serviços
- **Rota:** `/services`
- **Módulo ID:** `services`
- **Ícone:** `wrench`
- **Responsabilidade:** Catálogo de serviços técnicos oferecidos.

### 🏷️ Ofertas
- **Rota:** `/offers`
- **Módulo ID:** `offers`
- **Ícone:** `tag`
- **Responsabilidade:** Planos e ofertas comerciais por operadora.
  - **Sub-item: Apps** (`/offers/apps`, módulo `offers.apps`) — Listagem de aplicativos incluso nas ofertas.

### 🎧 Suporte
- **Rota:** `/support`
- **Módulo ID:** `support`
- **Ícone:** `headphones`
- **Responsabilidade:** Configurações e operação do módulo de suporte técnico.

---

## Grupo MARKETING

### 🌐 Sites
- **Rota:** `/marketing/sites`
- **Módulo ID:** `marketing.sites`
- **Ícone:** `globe`
- **Responsabilidade:** Listagem e status dos sites WordPress gerenciados.

### ✍️ Artigos
- **Rota:** `/marketing/articles`
- **Módulo ID:** `marketing.articles`
- **Ícone:** `pen-tool`
- **Responsabilidade:** Fila de artigos: gerados por IA, em revisão ou publicados.

### 📈 Ferramentas SEO
- **Rota:** `/marketing/seo`
- **Módulo ID:** `marketing.seo`
- **Ícone:** `trending-up`
- **Responsabilidade:** Ferramentas de análise e otimização SEO.

### 🚀 Marketing/SEO
- **Rota:** `/marketing/seo-strategist`
- **Módulo ID:** `marketing.seo-strategist`
- **Ícone:** `rocket`
- **Responsabilidade:** Estrategista de marketing e SEO com visão consolidada.

### 🛡️ Auditoria de Sites
- **Rota:** `/marketing/site-audit`
- **Condição:** Mesma permissão de `marketing.seo`
- **Ícone:** `shield-check`
- **Responsabilidade:** Análise técnica de sites (scraping, SEO, performance) com histórico.

### 🤖 Agentes de IA
- **Rota:** `/ai-agents`
- **Módulo ID:** `ai-agents`
- **Ícone:** `bot`
- **Condição:** `canNav('ai-agents')` ou acesso `all`
- **Responsabilidade:** Interface para controle e monitoramento dos workers de geração de conteúdo.
- **Doc:** [`modulos/ai-agents/overview.md`](./modulos/ai-agents/overview.md)

### 🔌 Integrações *(grupo expansível)*
- **Rota base:** `/integrations/widgets`
- **Ícone:** `plug`
- **Sub-itens:**
  - **Widgets & Scripts** (`/integrations/widgets`, módulo `integrations.widgets`)
  - **Identidade Visual** (`/integrations/styles`, módulo `integrations.styles`)
  - **Banners Personalizados** (`/integrations/banners`, módulo `integrations.banners`)
  - **Formulários de Captura** (`/integrations/forms`, módulo `integrations.forms`)
- **Responsabilidade:** Ativos digitais (widgets, banners, formulários, estilos) embutidos nos sites WordPress dos clientes.

---

## Grupo SISTEMA

### 🏢 Empresas (PJ)
- **Rota:** `/entities/pj`
- **Módulo ID:** `entities.pj`
- **Ícone:** `building`
- **Responsabilidade:** Registro de pessoas jurídicas como entidade base (não necessariamente cliente).

### 🏭 Filiais
- **Rota:** `/branches`
- **Módulo ID:** `branches`
- **Ícone:** `factory`
- **Responsabilidade:** Gerenciamento de filiais do grupo com configurações regionais.

### 👤 Pessoas (PF)
- **Rota:** `/entities/pf`
- **Módulo ID:** `entities.pf`
- **Ícone:** `user`
- **Responsabilidade:** Registro de pessoas físicas como entidade base.

### 📍 Endereços
- **Rota:** `/entities/addresses`
- **Módulo ID:** `entities.addresses`
- **Ícone:** `map-pin`
- **Responsabilidade:** Cadastro centralizado de endereços vinculados a PJ/PF.

### ⚡ Workflows
- **Rota:** `/workflows`
- **Módulo ID:** `workflows`
- **Ícone:** `zap`
- **Responsabilidade:** Configuração de fluxos automatizados de trabalho.

### 📊 Diagnóstico
- **Rota:** `/health`
- **Módulo ID:** `health`
- **Ícone:** `activity`
- **Responsabilidade:** Dashboard de saúde do sistema — status de Backend API, Google, AI Worker.

### 💻 Logs do Sistema
- **Rota:** `/logs`
- **Módulo ID:** `health` *(mesma permissão)*
- **Ícone:** `terminal`
- **Responsabilidade:** Visualização e busca dos logs estruturados da aplicação.

---

## Grupo ADMINISTRAÇÃO DE TI *(acesso `all` somente)*

### 🖥️ Servidor e Infra
- **Rota:** `/server-manager`
- **Condição:** `perms.canAccess()('all')`
- **Ícone:** `server`
- **Responsabilidade:** Painel de gerenciamento de servidor — serviços Docker, deploy, configurações de infraestrutura.

---

## Footer da Sidebar

| Elemento | Comportamento |
|---|---|
| **Profile Widget** | Avatar + nome + email do usuário logado |
| **Status do Usuário** | Seletor de status (disponível, reunião, pausa, offline) |
| **Modo Claro/Escuro** | Toggle de tema via `ThemeService` |
| **Trilhas de Conhecimento** | Abre modal `KnowledgeHub` (via `LayoutService.openKnowledgeHub`) |
| **Sair do Sistema** | Chama `authService.logout()` + log estruturado |

---

## Comportamentos Especiais

### Mobile (< 1024px)
A sidebar fecha automaticamente após qualquer clique de navegação:
```typescript
handleNavClick() {
  if (window.innerWidth < 1024) {
    this.sidebar.close();
  }
}
```

### Logging de Estado
A navbar usa um `effect()` reativo que registra no logger toda vez que o estado muda (usuário, role, módulos visíveis, sidebar):
```typescript
// Só loga se a assinatura mudou — evita log de re-renders desnecessários
if (signature === this.lastVisibilitySignature) return;
```

### Preloading Strategy
Módulos marcados com `data: { preload: 'navbar' }` nas rotas são pré-carregados pela `NavbarPreloadingStrategy` logo após o login, garantindo navegação instantânea nos itens mais usados.
