# Módulo: Consultores

> **Rota:** `/consultants` | **Módulo ID:** `consultants` | **Ícone:** `user-check`

## Responsabilidade

Cadastro e gestão dos consultores de vendas do grupo. Cada consultor possui perfil com especialidade, filial de atuação e carteira de clientes. O módulo permite visualizar performance individual e gerenciar a distribuição de leads e pedidos.

---

## Padrão Arquitetural

**Service Layer** — `ConsultantsService` gerencia o CRUD de consultores. A vinculação com pedidos e leads é feita via `consultor_id` nos respectivos registros.

---

## Entidades

| Campo | Tipo | Descrição |
|---|---|---|
| `id` | string | Identificador |
| `nome` | string | Nome do consultor |
| `email` | string | E-mail corporativo |
| `filial_id` | string | Filial de atuação |
| `especialidade` | string | Área de foco (B2B, B2C, enterprise) |
| `ativo` | boolean | Status de atividade |
| `meta_mensal` | number | Meta de vendas do período |

---

## Vínculo com Outros Módulos

| Módulo | Relacionamento |
|---|---|
| Pedidos | `consultor_id` em cada pedido |
| Leads | `responsavel_id` no funil |
| Relatórios | Performance individual por consultor |
| Usuários | Pode ter login associado no sistema |

---

## Pontos Fortes

- ✅ Distribuição de leads por consultor com rastreabilidade
- ✅ Perfil com especialidade para matching com tipo de cliente
- ✅ Meta mensal para base de cálculo em relatórios de performance

## Sugestões de Melhoria

- 🔧 Dashboard individual de consultor com meta x realizado em tempo real
- 🔧 Regra de distribuição automática de leads (round-robin, por especialidade)
- 🔧 Ranking de performance para gamificação de equipe comercial

---

## Relevância para Portfolio: ⭐⭐ (2/5)
