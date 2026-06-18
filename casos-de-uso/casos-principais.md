# Casos de Uso — OcHub

## UC-01: Consultor cadastra nova empresa e inicia negociação

**Ator:** Consultor de vendas  
**Pré-condição:** Consultor está autenticado no OcHub

**Fluxo principal:**
1. Consultor acessa módulo `/companies`
2. Preenche dados da empresa (razão social, segmento, cidade)
3. Sistema valida e cria registro no Backend API
4. Consultor acessa tab "Contatos" e adiciona responsável da empresa
5. Consultor cria nova negociação vinculada à empresa
6. Sistema registra abertura no histórico de interações
7. Negociação aparece no funil CRM com status "Em prospecção"

**Resultado:** Empresa e negociação cadastradas, visíveis no pipeline de vendas.

---

## UC-02: Técnico atualiza status de Ordem de Serviço

**Ator:** Técnico de campo (acesso via mobile)  
**Pré-condição:** OS atribuída ao técnico com status "Em andamento"

**Fluxo principal:**
1. Técnico acessa `/os` e filtra suas OS do dia
2. Abre OS específica
3. Registra observação sobre execução
4. Altera status para "Concluída"
5. Sistema registra timestamp e cria entrada no histórico da OS
6. Pedido vinculado tem seu status atualizado automaticamente

**Resultado:** OS fechada com histórico completo auditável.

---

## UC-03: Agente de IA gera lote de posts para sites de marketing

**Ator:** Sistema (automação via cron)  
**Pré-condição:** Fila de conteúdo preenchida pelo gestor de marketing

**Fluxo principal:**
1. Cron job dispara às 02h00 (horário configurado)
2. Worker `ia_righter` consulta fila pendente no Backend API
3. Para cada post pendente:
   - Consulta RAG local para contexto do site
   - Gera conteúdo HTML com LLM
   - Busca imagem temática via Freepik
   - Injeta imagem no HTML
   - Salva como draft no Backend API
4. Gestor de marketing recebe lista de drafts para revisão
5. Após aprovação, sincronização com WordPress ocorre via plugin

**Resultado:** Conteúdo editorial gerado, revisado e publicado sem intervenção manual na geração.

---

## UC-04: Administrador verifica saúde da plataforma após deploy

**Ator:** Administrador de sistema  
**Pré-condição:** Novo deploy realizado via Docker Compose

**Fluxo principal:**
1. Admin acessa `/health`
2. Dashboard exibe status de: Backend API, Google API, AI Worker, DB
3. Admin verifica logs em `/logs` filtrando por "ERROR" e últimos 30 min
4. Se tudo verde: considera deploy bem-sucedido
5. Se algum serviço vermelho: verifica `stage` do erro para diagnóstico rápido

**Resultado:** Validação de deploy sem necessidade de acesso ao servidor.

---

## UC-05: Site WordPress captura lead e sincroniza com CRM

**Ator:** Visitante do site de uma distribuidora parceira  
**Pré-condição:** Plugin OcHub Connector instalado e configurado no WordPress

**Fluxo principal:**
1. Visitante preenche formulário "Fale conosco" no WordPress
2. Plugin chama `sdk.crm.createLead(formData)`
3. SDK envia dados ao Backend API via REST
4. Lead aparece no módulo CRM do OcHub com origem "Site [nome]"
5. Consultor responsável recebe notificação
6. Consultor inicia follow-up pelo OcHub

**Resultado:** Lead capturado do site sem acesso manual, rastreado desde a origem.

---

## UC-06: Gestor importa planilha Excel de clientes

**Ator:** Gestor operacional  
**Pré-condição:** Planilha Excel padronizada com lista de clientes

**Fluxo principal:**
1. Gestor executa script `scripts/sync-excel-clients.ts`
2. Script lê planilha via `xlsx`
3. Para cada linha, valida campos obrigatórios
4. Cria ou atualiza registro no Backend API (`upsert` por CNPJ/CPF)
5. Gera relatório de importação (sucessos, falhas, duplicatas)

**Resultado:** Base de clientes sincronizada com planilha operacional sem entrada manual.
