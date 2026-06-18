# Módulo: Credenciais

> **Rota:** `/credentials` | **Módulo ID:** `credentials` | **Ícone:** `key`

## Responsabilidade

Gerenciamento seguro de credenciais de acesso a sistemas e portais de operadoras parceiras. Armazena tokens, logins e senhas de forma criptografada, com acesso controlado por permissão e auditoria de consulta.

---

## Padrão Arquitetural

**Secure Vault Pattern** — `CredentialsService` nunca retorna valores completos de credencial na listagem. Valores sensíveis são expostos apenas sob demanda (ação explícita do usuário) e nunca logados. Criptografia aplicada server-side antes da persistência.

---

## Entidades

| Campo | Tipo | Descrição |
|---|---|---|
| `id` | string | Identificador |
| `nome` | string | Nome descritivo da credencial |
| `tipo` | enum | login_senha, token_api, oauth, certificado |
| `operadora_id` | string | Operadora vinculada (opcional) |
| `parceiro_id` | string | Parceiro vinculado (opcional) |
| `usuario` | string | Nome de usuário (exibido mascarado) |
| `senha` | string | [OMITIDO — armazenado criptografado] |
| `token` | string | [OMITIDO — armazenado criptografado] |
| `validade` | string | Data de expiração (se aplicável) |
| `observacoes` | string | Instruções de uso |

---

## Controles de Segurança

- **Nunca expostos em listagem:** `senha`, `token`, certificados
- **Acesso por ação explícita:** botão "Revelar" com log de auditoria
- **Criptografia:** server-side antes de persistir na API backend
- **Permissão de acesso:** módulo visível apenas a roles com `credentials` liberado

---

## Pontos Fortes

- ✅ Centralização de credenciais evita arquivos de senha por e-mail ou planilha
- ✅ Alerta de validade para renovação proativa
- ✅ Rastreabilidade de quem acessou o quê e quando

## Sugestões de Melhoria

- 🔧 Integração com vault externo (HashiCorp Vault ou AWS Secrets Manager) para credenciais críticas
- 🔧 Rotação automática de tokens com prazo de expiração
- 🔧 Compartilhamento seguro de credencial por link temporário entre times

---

## Relevância para Portfolio: ⭐⭐⭐ (3/5)
