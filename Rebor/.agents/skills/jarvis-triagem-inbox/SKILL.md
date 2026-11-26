---
name: jarvis-triagem-inbox
description: >-
  Processes and organizes Rober's Obsidian Inbox (01 - Inbox/Ideias e pensamentos
  rápidos.md and any loose notes inside 01 - Inbox/), classifying items into
  dated tasks, project notes, knowledge base, resources, or Google Calendar
  reminders. Use when the user asks to empty, clean, triage, or process the Inbox.
---

# JARVIS — Triagem do Inbox

Ajuda o Rober a esvaziar `01 - Inbox/` rapidamente, mantendo o Life OS limpo sem perder boas ideias.

## Passo a Passo

1. **Ler todo o Inbox:**
   - Leia `01 - Inbox/Ideias e pensamentos rápidos.md`.
   - Liste e leia quaisquer outros arquivos `.md` soltos em `01 - Inbox/`.
2. **Classificar cada item capturado** usando a estrutura do cofre:
   - **Ação rápida (< 2 min):** sinalizar para fazer na hora.
   - **Tarefa com prazo/data:** mover para a nota diária (`02 - Planejamento/Diário/AAAA-MM-DD.md`) ou para a nota do projeto correspondente em `03 - Projetos/` com sintaxe `- [ ] ... 📅 AAAA-MM-DD`.
   - **Compromisso com hora marcada / lembrete no celular:** propor criar evento no Google Calendar via `gcalendar mutate create`.
   - **Ideia de jogo:** mover para `06 - Recursos/Ideias de jogos/Ideias de jogos.md`.
   - **Link ou material de estudo:** mover para `06 - Recursos/Links e materiais/Links e materiais.md` ou para a trilha certa em `05 - Conhecimento/` (`AWS`, `Design`, `Game Dev`, `Programação`).
   - **Novo projeto:** sugerir criar nota com `99 - Sistema/Templates/Projeto.md` em `03 - Projetos/` com `status: espera` (respeitando o limite de 3 projetos ativos).
   - **Descarte / Não faz mais sentido:** propor remover.
3. **Confirmar antes de apagar:**
   - Apresente a tabela/lista com o destino sugerido de cada item e pergunte se Rober aprova aplicar tudo de uma vez (ou ajustar algum item).
   - Só limpe as linhas do `Ideias e pensamentos rápidos.md` ou mova arquivos após a confirmação (a menos que o usuário já tenha dito explicitamente *"organiza e limpa tudo direto"*).
4. **Confirmar conclusão:** informe exatamente para onde cada item foi movido com links clicáveis.
