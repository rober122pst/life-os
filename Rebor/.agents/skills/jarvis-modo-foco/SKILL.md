---
name: jarvis-modo-foco
description: >-
  Launches a Deep Work session for Rober by blocking uninterrupted focus time in
  Google Calendar, starting focus music/brown noise on Spotify via Zapier MCP,
  and optionally dispatching a summary or reminder via WhatsApp Notifications or
  Discord. Use when Rober asks to enter focus mode, start deep work, play coding
  music, or protect a work session.
---

# JARVIS — Modo Foco (Deep Work + Spotify + Alertas)

Ativa uma sessão de *deep work* alinhada ao perfil do Rober (blocos longos em uma única tarefa, com áudio de fundo como música, ASMR ou *brown noise*).

## Passo a Passo

1. **Definir a tarefa única e a duração:**
   - Se Rober não informou a duração, sugira **90 min ou 2h** (evite micro-blocos fragmentados).
   - Se ele não informou a tarefa, consulte a nota diária de hoje (`02 - Planejamento/Diário/AAAA-MM-DD.md`) e proponha a prioridade #1 aberta.

2. **Bloquear na agenda (Google Calendar):**
   - Verifique conflitos primeiro com `gcalendar readonly events --date <HOJE> --max 50 --json`.
   - Crie o bloco solo com `gcalendar mutate create --summary "Deep Work — <TAREFA>" --start <INICIO_RFC3339> --end <FIM_RFC3339> --send-updates none` e informe o link do evento.

3. **Ligar a trilha de foco no Spotify (via Zapier MCP — `SpotifyV2CLIAPI`):**
   - Antes de executar, verifique se há conexão padrão com `inspect_zapier_actions` (`selected_api: "SpotifyV2CLIAPI"`).
   - Busque a playlist/faixa pedida (ex.: *brown noise*, *lofi*, ou playlist salva do Rober) com `execute_zapier_read_action` (`search_item` ou `new_playlist` / `get_recently_played`).
   - Inicie a reprodução com `execute_zapier_write_action` (`start_playback` passando `context_uri` ou `uris`).
   - *Nota:* o `start_playback` do Spotify exige um dispositivo Spotify aberto/ativo; se retornar erro de dispositivo inativo, avise Rober para abrir o app do Spotify por 1 segundo e dê retry.

4. **Notificações / Lembretes (WhatsApp Notifications ou Discord via Zapier MCP):**
   - **WhatsApp Notifications (`WhatsAppNotificationsCLIAPI` -> `send_message`, `tool_name: "whatsapp_notifications_send_message"`):**
     - Conta padrão: `+5581983332632`.
     - Template `calendar_reminder`: `params: {"template": "calendar_reminder", "dynamic_properties": {"event_name": "<nome do bloco/lembrete>", "date_and_time": "<DD/MM às HH:mm>"}}` — ideal para lembretes de blocos de *deep work* ou prazos.
     - Template `message_reminder`: `params: {"template": "message_reminder", "dynamic_properties": {"name": "<assunto/remetente>", "link_to_reply": "<URL>"}}` — ideal para alertas de PRs ou e-mails importantes.
   - **Discord (`DiscordCLIAPI` -> `send_channel_message`, `tool_name: "discord_send_channel_message"`):**
     - Servidor padrão: `uau (rober122)`. Sempre use `"username": "JARVIS"` para mensagens do assistente.
     - Ideal para briefings longos, checklists completos e links do GitHub/Obsidian (até 2000 caracteres).
   - **Segurança:** sempre confirme com Rober o canal/destino e o conteúdo antes de disparar escritas externas pela primeira vez (ou quando não estiver explicitamente autorizado na automação).

5. **Check-in pós-bloco:**
   - Ao final (quando Rober voltar), pergunte como rendeu, marque a tarefa concluída (`- [x] ... ✅ AAAA-MM-DD`) na nota diária e sugira o próximo passo ou pausa real.
