---
name: jarvis-fechamento-dia
description: >-
  Executes Rober's nightly wrap-up (23:00 America/Recife) or on-demand end-of-day
  review. Reviews today's completed vs. pending tasks, checks the Obsidian Inbox,
  scans late-day important Gmail messages, previews tomorrow's Google Calendar,
  and updates the day's closing section while drafting tomorrow's focus. Use when
  running the nightly automation or when the user asks to wrap up or review the day.
---

# JARVIS — Fechamento do Dia

Fecha o ciclo diário do Rober às **23h** (ou sob demanda), consolidando conquistas, destravando pendências sem culpa e deixando o dia seguinte encaminhado.

## Passo a Passo

### 1. Determinar datas (fuso `America/Recife`)
- Defina `HOJE` (`AAAA-MM-DD`) e `AMANHA` (`AAAA-MM-DD`).

### 2. Coletar contexto em paralelo
1. **Nota diária de hoje:** leia `02 - Planejamento/Diário/<HOJE>.md` (se existir) e conte o que foi concluído (`- [x]`) vs. o que ficou aberto (`- [ ]`).
2. **Inbox do Obsidian:** leia `01 - Inbox/Ideias e pensamentos rápidos.md` e liste eventuais arquivos soltos criados hoje dentro de `01 - Inbox/`.
3. **Google Calendar de amanhã:** rode `gcalendar readonly events --date <AMANHA> --max 30 --json` para antecipar compromissos, horários de sair cedo ou janelas de foco de amanhã.
4. **Gmail do dia:** rode `gmail readonly search 'newer_than:1d is:unread -category:promotions -category:social' --max 10` (use aspas simples no PowerShell) para ver se chegou algo urgente à tarde/noite que impacte amanhã.

### 3. Atualizar o encerramento na nota diária (preservando texto manual)
- Se `02 - Planejamento/Diário/<HOJE>.md` existir e a seção `## 🌙 Encerramento do dia` ainda não tiver sido preenchida pelo Rober:
  - Preencha de forma limpa e editável:
    - **O que consegui fazer?** resumo objetivo das tarefas marcadas como `[x]`.
    - **O que ficou pendente?** lista curta do que ficou em `[ ]` (sem remorso, apenas clareza).
    - **Qual será meu foco amanhã?** sugestão inicial conectada às pendências + compromissos de amanhã.
- **Nunca** mova ou apague itens do `01 - Inbox/` automaticamente sem permissão; apenas liste e sugira o destino na conversa.

### 4. Enviar resumo noturno no Discord e lembrete de amanhã no WhatsApp (via Zapier MCP)
1. **Discord (`#privado-programar`):** envie o fechamento resumido (< 2000 caracteres) com o que avançou hoje, pendências, itens no Inbox e o radar de amanhã via `execute_zapier_write_action` (`selected_api: "DiscordCLIAPI"`, `action: "send_channel_message"`, `tool_name: "discord_send_channel_message"`, `params: {"channel_id": "1277453237464600626", "username": "JARVIS", "content": "<resumo noturno>"}`).
2. **WhatsApp Notifications (`+5581983332632`):** se houver um compromisso importante ou foco principal já definido para amanhã, envie 1 lembrete curto via `execute_zapier_write_action` (`selected_api: "WhatsAppNotificationsCLIAPI"`, `action: "send_message"`, `tool_name: "whatsapp_notifications_send_message"`, `params: {"template": "calendar_reminder", "dynamic_properties": {"event_name": "<Foco principal / 1º compromisso de amanhã>", "date_and_time": "<DD/MM às HH:mm>"}}`).

### 5. Entregar o Check-in Noturno Conversacional
Responda com tom leve, humano e proativo:
1. **Reconhecimento do que foi feito hoje** (destaque real para o progresso, mesmo em dias corridos).
2. **Pendências de hoje:** para cada tarefa aberta, sugira se vale jogar para amanhã, mover para outra data da semana ou descartar.
3. **Itens no Inbox:** se houver capturas em `01 - Inbox/`, apresente uma proposta rápida de triagem (1 linha por item) para ele só aprovar.
4. **Radar de amanhã:** compromissos do Google Calendar + sugestão das **3 prioridades de amanhã** (e qualquer alerta do Gmail que mereça atenção logo cedo).
5. **Fechamento proativo:** pergunte se ele quer já reagendar as pendências para amanhã, limpar o Inbox agora ou criar algum lembrete matinal no Calendar — e deseje um bom descanso.
