# Tasks Atômicas — Análise por Módulo

Este arquivo contém as tasks atômicas de análise geradas para cada módulo principal do OcHub.
Podem ser executadas por modelos menores de forma independente, com contexto mínimo.

---

## TASK_ID: crm-pipeline-analysis
**MODELO_ALVO:** gemini-flash | claude-haiku  
**MAX_TOKENS_RESPOSTA:** 800  
**CONTEXTO_NECESSÁRIO:** `src/app/features/crm/` (apenas este diretório)

**INSTRUÇÃO:**
Analise exclusivamente o módulo "CRM" localizado em `src/app/features/crm/`.
Responda APENAS no formato abaixo, sem expandir além do solicitado:

1. RESPONSABILIDADE (2 frases máximo): Gerencia o relacionamento com clientes, parceiros e histórico de negociações do grupo de distribuidoras. Controla o pipeline de vendas desde o lead inicial até a fidelização do cliente.
2. PADRÃO ARQUITETURAL (1 linha): Repository Pattern via Backend API REST API, com services Angular como camada de acesso.
3. DEPENDÊNCIAS INTERNAS (lista): core/services/google-auth, core/services/permissions, shared/components, models/crm.models.ts
4. PONTOS FORTES (máx 3 bullets): Modelo de dados rico com relacionamentos N-N entre entidades; Histórico de interações auditável; Roteamento modular com lazy-loading.
5. SUGESTÕES DE MELHORIA (máx 3 bullets): Kanban visual para pipeline; Webhooks para mudanças de status em tempo real; Métricas de conversão por consultor.
6. RELEVÂNCIA PARA PORTFOLIO (1-5): **4/5**

NÃO inclua: código, credenciais, dados de ambiente, lógica de negócio sensível.

---

## TASK_ID: os-lifecycle-analysis
**MODELO_ALVO:** gemini-flash | claude-haiku  
**MAX_TOKENS_RESPOSTA:** 800  
**CONTEXTO_NECESSÁRIO:** `src/app/features/os/` + `scripts/os-automation-logic.ts`

**INSTRUÇÃO:**
Analise exclusivamente o módulo "OS (Ordens de Serviço)" localizado em `src/app/features/os/`.
Responda APENAS no formato abaixo, sem expandir além do solicitado:

1. RESPONSABILIDADE (2 frases máximo): Gerencia o ciclo técnico de atendimento pós-venda com rastreamento de status, responsável e prazo. Automatiza criação de OS a partir de pedidos aprovados.
2. PADRÃO ARQUITETURAL (1 linha): State Machine implícita via campos de status no Backend API, com automação em script TypeScript.
3. DEPENDÊNCIAS INTERNAS (lista): features/orders, core/services, shared/components
4. PONTOS FORTES (máx 3 bullets): Histórico de mudanças de status com timestamp; Integração automática com módulo de pedidos; Filtros por técnico/status/período.
5. SUGESTÕES DE MELHORIA (máx 3 bullets): SLA automático com alertas; Mapa de calor por região; Integração Google Calendar.
6. RELEVÂNCIA PARA PORTFOLIO (1-5): **4/5**

---

## TASK_ID: marketing-pipeline-analysis
**MODELO_ALVO:** gemini-flash | claude-haiku  
**MAX_TOKENS_RESPOSTA:** 800  
**CONTEXTO_NECESSÁRIO:** `src/app/features/marketing/` + `ia_righter/src/` + `src/services/wp-sync.service.ts`

**INSTRUÇÃO:**
Analise exclusivamente o módulo "Marketing" e sua integração com o ia_righter.
Responda APENAS no formato abaixo, sem expandir além do solicitado:

1. RESPONSABILIDADE (2 frases máximo): Automatiza produção e publicação de conteúdo editorial em múltiplos sites WordPress. Integra geração com IA, revisão humana e sincronização com WordPress em pipeline único.
2. PADRÃO ARQUITETURAL (1 linha): Orchestrator + Worker Pattern com fila de tarefas no Backend API.
3. DEPENDÊNCIAS INTERNAS (lista): ia_righter (worker externo), api-server.js (/api/marketing/*), sdk/ochub-sdk, wordpress-plugin
4. PONTOS FORTES (máx 3 bullets): Pipeline completo geração→revisão→publicação; Publicação multi-site centralizada; Auditoria SEO automática pós-publicação.
5. SUGESTÕES DE MELHORIA (máx 3 bullets): Dashboard de performance por post; A/B testing de títulos; Datas ideais por tópico via ML.
6. RELEVÂNCIA PARA PORTFOLIO (1-5): **5/5**

---

## TASK_ID: ai-agents-architecture-analysis
**MODELO_ALVO:** gemini-flash | claude-haiku  
**MAX_TOKENS_RESPOSTA:** 800  
**CONTEXTO_NECESSÁRIO:** `src/app/features/ai-agents/` + `ia_righter/src/` + `scripts/ai-worker.ts`

**INSTRUÇÃO:**
Analise exclusivamente o módulo "AI Agents" e o worker ia_righter.
Responda APENAS no formato abaixo, sem expandir além do solicitado:

1. RESPONSABILIDADE (2 frases máximo): Provê interface visual para monitorar e controlar agentes de IA editoriais. O worker ia_righter executa geração de conteúdo com LLM em container isolado com sistema RAG local.
2. PADRÃO ARQUITETURAL (1 linha): Worker + Queue Pattern com container Docker dedicado e fila de tarefas no CMS.
3. DEPENDÊNCIAS INTERNAS (lista): api-server.js (/api/ai-agent/*), scripts/rag/, ia_righter/src/, docker/Dockerfile.ai-agent
4. PONTOS FORTES (máx 3 bullets): Isolamento em container com limite de CPU/RAM; RAG local preserva confidencialidade; Auditabilidade completa da fila.
5. SUGESTÕES DE MELHORIA (máx 3 bullets): WebSocket para progresso em tempo real; Score de qualidade automático pré-draft; Retry com prompt diferente.
6. RELEVÂNCIA PARA PORTFOLIO (1-5): **5/5**

---

## TASK_ID: integrations-oauth-analysis
**MODELO_ALVO:** gemini-flash | claude-haiku  
**MAX_TOKENS_RESPOSTA:** 800  
**CONTEXTO_NECESSÁRIO:** `src/app/features/integrations/` + `src/app/core/services/google-auth.service.ts`

**INSTRUÇÃO:**
Analise exclusivamente o módulo "Integrações" focando no fluxo Google OAuth.
Responda APENAS no formato abaixo, sem expandir além do solicitado:

1. RESPONSABILIDADE (2 frases máximo): Centraliza conexões OAuth com Google Workspace gerenciando tokens de Calendar, Drive e Sheets. Provê status de cada integração ativa e handle de renovação automática.
2. PADRÃO ARQUITETURAL (1 linha): Facade Pattern — google-auth.service encapsula OAuth para todos os módulos consumidores.
3. DEPENDÊNCIAS INTERNAS (lista): core/services/google-auth, core/services/google-calendar, core/services/google-drive, core/services/google-sheets, core/services/google-mirror
4. PONTOS FORTES (máx 3 bullets): Renovação de token transparente; Health check por stage de falha; Diagnóstico granular no log.
5. SUGESTÕES DE MELHORIA (máx 3 bullets): Suporte a múltiplos providers OAuth; Revogação granular de escopos; Alertas proativos de expiração.
6. RELEVÂNCIA PARA PORTFOLIO (1-5): **4/5**

---

## TASK_ID: core-infrastructure-analysis
**MODELO_ALVO:** gemini-flash | claude-haiku  
**MAX_TOKENS_RESPOSTA:** 800  
**CONTEXTO_NECESSÁRIO:** `src/app/core/` (apenas este diretório)

**INSTRUÇÃO:**
Analise exclusivamente o módulo "Core" da aplicação Angular.
Responda APENAS no formato abaixo, sem expandir além do solicitado:

1. RESPONSABILIDADE (2 frases máximo): Provê a infraestrutura transversal da aplicação: guards, interceptors, layout, logging e serviços de estado global. É o alicerce sobre o qual todos os módulos de feature operam.
2. PADRÃO ARQUITETURAL (1 linha): Functional Guards + Injectable Services seguindo Angular 17+ moderno com standalone components.
3. DEPENDÊNCIAS INTERNAS (lista): Sem dependências de features (é consumido por todas); depende de rxjs e googleapis externamente.
4. PONTOS FORTES (máx 3 bullets): Logging estruturado com persistência; Preloading seletivo customizado por rota; Métricas de navegação coletadas automaticamente.
5. SUGESTÕES DE MELHORIA (máx 3 bullets): Circuit breaker no interceptor; Correlation ID nas requisições; Signals no sistema de permissões.
6. RELEVÂNCIA PARA PORTFOLIO (1-5): **4/5**

---

## TASK_ID: sdk-distribution-analysis
**MODELO_ALVO:** gemini-flash | claude-haiku  
**MAX_TOKENS_RESPOSTA:** 800  
**CONTEXTO_NECESSÁRIO:** `sdk/ochub-sdk/src/` + `sdk/ochub-sdk/package.json`

**INSTRUÇÃO:**
Analise exclusivamente o SDK @grupooc/ochub-sdk.
Responda APENAS no formato abaixo, sem expandir além do solicitado:

1. RESPONSABILIDADE (2 frases máximo): Biblioteca TypeScript que permite sistemas externos integrarem-se ao OcHub sem acesso ao código-fonte. Encapsula chamadas ao Backend API com tipagem segura para CRM, CMS, SSG e operações estáticas.
2. PADRÃO ARQUITETURAL (1 linha): Facade + Module Pattern com cliente raiz instanciando módulos especializados.
3. DEPENDÊNCIAS INTERNAS (lista): Sem dependências internas — biblioteca independente publicada como .tgz.
4. PONTOS FORTES (máx 3 bullets): Tipagem TypeScript completa; Versionamento semântico (v1.0.2 → v1.1.0); Build otimizado com tsup e tree-shaking.
5. SUGESTÕES DE MELHORIA (máx 3 bullets): Publicação em registro NPM privado; Retry automático com backoff; Documentação via TypeDoc.
6. RELEVÂNCIA PARA PORTFOLIO (1-5): **5/5**
