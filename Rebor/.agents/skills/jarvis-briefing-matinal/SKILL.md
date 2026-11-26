---
name: jarvis-briefing-matinal
description: >-
  Executes Rober's daily morning briefing (11:00 America/Recife) or on-demand
  daily kickoff. Cross-references Google Calendar, Gmail, and the Obsidian Life
  OS vault to create or update today's daily note with commitments, overdue/due
  tasks, and up to 3 deep-work priorities. Use when running the morning
  automation or when the user asks for a daily briefing, morning plan, or daily
  checklist.
---

# JARVIS — Briefing Matinal

Prepara o dia do Rober unindo **Google Calendar + Gmail + Obsidian Life OS**, criando ou atualizando a nota diária sem perder nenhum dado manual.

## Passo a Passo

### 1. Determinar data e fuso
- Considere sempre o fuso **`America/Recife`** (`UTC-3`).
- Defina `HOJE` (`AAAA-MM-DD`, formato de título `DD/MM/AAAA`) e `AMANHA` (`AAAA-MM-DD`).

### 2. Coletar contexto em paralelo
1. **Google Calendar (`gcalendar`):**
   - Liste os eventos de hoje e de amanhã:
     - `gcalendar readonly events --date <HOJE> --max 50 --json`
     - `gcalendar readonly events --date <AMANHA> --max 20 --json`
   - Se o comando `gcalendar` ainda não estiver no `PATH`, inicialize uma vez com o script do plugin (`C:\Users\MICRO\.gemini\config\plugins\gcalendar\skills\gcalendar\scripts\gcalendar.cmd --version`) e depois use `gcalendar`.
2. **Gmail (`gmail`):**
   - Busque e-mails recentes relevantes (ignorando promoções e redes sociais; no Windows/PowerShell use aspas simples na query):
     - `gmail readonly search 'newer_than:1d -category:promotions -category:social' --max 15`
   - Leia o conteúdo completo (`gmail readonly read` ou `gmail readonly get`) **apenas** dos e-mails que pareçam exigir atenção ou ação (faculdade/UNINASSAU, estágio/Prefeitura de Paulista, AWS, vagas/Gupy/Infojobs, Santander, DETRAN/CNH, bancos/boletos, pessoas próximas ou respostas aguardadas).
   - Nunca envie e-mails nesta etapa.
3. **Obsidian Life OS:**
   - Leia a nota diária de hoje (`02 - Planejamento/Diário/<HOJE>.md`), se já existir.
   - Leia a nota diária de ontem (se existir) para ver tarefas pendentes e o campo *"Qual será meu foco amanhã?"*.
   - Leia `01 - Inbox/Ideias e pensamentos rápidos.md` para checar se há algo urgente capturado.
   - Busque tarefas não concluídas (`- [ ]`) com data `📅` igual ou anterior a `<HOJE>` em `02 - Planejamento/`, `03 - Projetos/` e `04 - Áreas da vida/`.
   - Confira os projetos ativos em `03 - Projetos/` (`status: ativo`).

### 3. Criar ou atualizar a nota diária
- Caminho: `02 - Planejamento/Diário/<HOJE>.md`.
- **Se a nota ainda não existir**, crie seguindo exatamente a estrutura de `99 - Sistema/Templates/Diário.md`:
  - Frontmatter: `tipo: diario` e `data: <HOJE>`.
  - Título: `# <DD/MM/AAAA>`.
  - `## 🎯 Três prioridades`: proponha **no máximo 3 prioridades** de maior impacto, usando sintaxe Tasks (`- [ ] ... 📅 <HOJE>` com `⏫` ou `🔼` quando fizer sentido). Respeite o foco principal do dia (se houver nota semanal vigente em `02 - Planejamento/Semanal/`).
  - `## 📅 Compromissos`: liste os eventos do Google Calendar com horário (`HH:mm–HH:mm — Título`). Se não houver compromissos, registre `- Sem compromissos fixos no Google Calendar — janela livre para deep work`.
  - `## 📋 Outras tarefas`: liste tarefas secundárias de hoje, atrasadas relevantes ou ações disparadas por e-mails importantes.
  - `## 💭 Pensamentos e anotações`: inclua um subbloco discreto `### 🤖 Notas do JARVIS` com alertas de e-mails importantes ou lembretes úteis de amanhã.
  - `## 🌙 Encerramento do dia`: mantenha os 3 prompts em branco prontos para a noite.
- **Se a nota já existir**, **NÃO apague nada** que o Rober já escreveu. Apenas complemente compromissos do Calendar que faltem, adicione alertas do Gmail em `### 🤖 Notas do JARVIS` e só sugira prioridades caso a seção ainda esteja vazia.

### 4. Enviar resumo no Discord e lembrete no WhatsApp (via Zapier MCP)
1. **Discord (`#privado-programar`):** envie o resumo estruturado (< 2000 caracteres) com agenda, as 3 prioridades e alertas críticos do Gmail usando `execute_zapier_write_action`:
   - `selected_api`: `"DiscordCLIAPI"`
   - `action`: `"send_channel_message"`
   - `tool_name`: `"discord_send_channel_message"`
   - `params`: `{"channel_id": "1277453237464600626", "username": "JARVIS", "content": "<resumo formatado>"}`
2. **WhatsApp Notifications (`+5581983332632`):** dispare 1 lembrete curto com a prioridade #1 ou próximo compromisso crítico de hoje usando `execute_zapier_write_action`:
   - `selected_api`: `"WhatsAppNotificationsCLIAPI"`
   - `action`: `"send_message"`
   - `tool_name`: `"whatsapp_notifications_send_message"`
   - `params`: `{"template": "calendar_reminder", "dynamic_properties": {"event_name": "<Prioridade #1 ou compromisso principal do dia>", "date_and_time": "<DD/MM às HH:mm (ou 'Hoje — foco principal')>"}}`

### 5. Entregar o Briefing Conversacional e Proativo
Responda em português natural, com energia boa e clareza:
1. **Saudação + Panorama rápido do dia** (agenda do Calendar + quanto tempo livre existe para *deep work*).
2. **Suas 3 prioridades sugeridas** (explicando brevemente o porquê da escolha).
3. **Radar do Gmail** (somente o que realmente importa; se não houver nada urgente, avise em 1 linha).
4. **Pendências / Atrasadas** (com destaque leve, sem gerar ansiedade; se houver muitas, sugira o que adiar).
5. **Próximo passo proativo:** sugira 1 bloco de *deep work* concreto no horário livre de hoje e pergunte se ele quer ajustar as prioridades, criar lembrete/bloco de foco no Google Calendar ou rascunhar resposta para algum e-mail.
