---
name: jarvis-revisao-semanal
description: >-
  Executes Rober's Sunday weekly review (11:00 America/Recife) or on-demand
  weekly planning. Audits the Obsidian Inbox, overdue tasks, active projects
  (max 3), long-term goals, next 7 days in Google Calendar, unread important
  Gmail threads, and recent Google Drive files, then creates or updates the
  weekly note in 02 - Planejamento/Semanal/. Use on Sundays or when the user
  asks for a weekly review or weekly plan.
---

# JARVIS — Revisão Semanal (Domingo)

Executa a revisão semanal completa do Life OS (baseada em `99 - Sistema/Templates/Semanal.md`), unindo o panorama de domingo + planejamento estratégico da semana que começa.

## Passo a Passo

### 1. Calcular datas e identificador da semana (`America/Recife`)
- No plugin Calendar do Obsidian do Rober, `weekStart` é **domingo** e o formato do arquivo semanal é `gggg-[W]ww` (ex.: `2026-W48.md`) na pasta `02 - Planejamento/Semanal/`.
- Defina:
  - `HOJE` (domingo ou data atual, `AAAA-MM-DD`)
  - Intervalo da semana: de `HOJE` até `+6 dias` (`FIM_SEMANA`).
  - `SEGUNDA`: data da próxima segunda-feira (`AAAA-MM-DD`).

### 2. Coletar dados em paralelo
1. **Google Calendar (semana toda):**
   - Use timestamps RFC3339 completos (com fuso `-03:00`):
     - `gcalendar readonly events --start <HOJE>T00:00:00-03:00 --end <FIM_SEMANA>T23:59:59-03:00 --max 80 --json`
2. **Gmail (pendências da semana):**
   - No Windows/PowerShell, use aspas simples na query para evitar problemas com `cmd.exe`:
     - `gmail readonly search 'newer_than:7d (is:unread OR is:starred) -category:promotions -category:social' --max 15`
3. **Google Drive (arquivos recentes):**
   - `gdrive readonly recent --max 10` (para lembrar documentos da faculdade, estágio ou projetos tocados recentemente).
4. **Obsidian Life OS:**
   - Leia `01 - Inbox/Ideias e pensamentos rápidos.md` e liste todos os arquivos em `01 - Inbox/`.
   - Busque todas as tarefas atrasadas (`- [ ]` com `📅` anterior a `HOJE`) em todo o cofre.
   - Audite os projetos em `03 - Projetos/` (quais estão `status: ativo`, quais estão `status: espera`, prazos e próximas ações). Verifique a regra de **máximo 3 projetos ativos**.
   - Leia `02 - Planejamento/Objetivos.md` para checar alinhamento com metas maiores.
   - Leia as notas diárias da última semana (`02 - Planejamento/Diário/`) para resumir vitórias e padrões.

### 3. Criar ou atualizar a nota semanal
- Caminho: `02 - Planejamento/Semanal/<AAAA-Www>.md`.
- Se não existir, crie seguindo `99 - Sistema/Templates/Semanal.md`:
  - Frontmatter: `tipo: semanal`, `semana: <AAAA-Www>`.
  - `## 🎯 Foco principal da semana`: sugira 1 a 2 focos estratégicos baseados nos projetos ativos, prazos e objetivos.
  - `## 🗓️ Distribuição de foco por dia`: mantenha o mapa padrão do template (SEG–DOM) anotando ao lado os compromissos-chave encontrados no Google Calendar para cada dia.
  - `## ✅ Revisão de domingo (20 min)`: mantenha o checklist do template pronto (marcando apenas o que o JARVIS já levantou como contexto, sem fechar etapas que dependem de decisão do Rober).
  - `## 📋 Tarefas importantes da semana`: liste as entregas críticas da semana com `📅 AAAA-MM-DD`.
  - `## 📝 Anotações da semana`: inclua `### 🤖 Resumo do JARVIS` com destaques da semana anterior, status dos projetos ativos, e-mails pendentes e arquivos recentes no Drive.
- Se já existir, preserve todo conteúdo manual do Rober e apenas complemente o bloco do JARVIS.

### 4. Enviar resumo semanal no Discord e lembrete no WhatsApp (via Zapier MCP)
1. **Discord (`#privado-programar`):** envie o panorama da semana (< 2000 caracteres) com projetos ativos, agenda da semana, pendências do Inbox/Gmail e as 3 prioridades sugeridas para segunda-feira via `execute_zapier_write_action` (`selected_api: "DiscordCLIAPI"`, `action: "send_channel_message"`, `tool_name: "discord_send_channel_message"`, `params: {"channel_id": "1277453237464600626", "username": "JARVIS", "content": "<resumo semanal>"}`).
2. **WhatsApp Notifications (`+5581983332632`):** envie 1 lembrete de revisão semanal / foco de segunda-feira via `execute_zapier_write_action` (`selected_api: "WhatsAppNotificationsCLIAPI"`, `action: "send_message"`, `tool_name: "whatsapp_notifications_send_message"`, `params: {"template": "calendar_reminder", "dynamic_properties": {"event_name": "Revisão Semanal pronta + Foco da semana: <FOCO>", "date_and_time": "Domingo 11:00 (20 min)"}}`).

### 5. Entregar a Revisão Conversacional e Proativa
Apresente uma conversa estruturada, leve e estratégica (pensada para ele fechar em ~20 minutos):
1. **Retrospectiva rápida:** vitórias da semana que passou e o que merece ajuste.
2. **Saúde dos projetos ativos:** lista dos projetos em `status: ativo` (alertando se passar de 3 ou se algum estiver travado).
3. **Agenda da semana + alertas do Gmail/Drive:** compromissos críticos, prazos e e-mails que pedem resposta.
4. **Inbox & Tarefas atrasadas:** quantidade e sugestão rápida para limpar tudo hoje.
5. **Proposta das 3 prioridades de segunda-feira** (`<SEGUNDA>`) + oferta proativa para bloquear sessões de *deep work* no Google Calendar para os dias mais livres da semana.
