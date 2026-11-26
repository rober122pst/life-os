---
title: "Life OS — Central de Controle"
type: moc
status: ativo
cssclasses:
  - dashboard
tags:
  - dashboard
  - moc
  - life-os
aliases:
  - "Dashboard"
  - "Home"
created: 2026-11-25
updated: 2026-11-25
---

# 🧭 Life OS — Central de Controle

> [!info] Acesso rápido
> [[Comece Aqui|📖 Guia rápido]] · [[Ideias e pensamentos rápidos|📥 Inbox]] · [[Objetivos|🎯 Objetivos]] · [[Perfil - Rober|👤 Perfil]] · [[Setup e Hardware|🖥️ Setup]]

---

## 🎯 Tarefas de hoje

```tasks
not done
due today
sort by priority
```

## ⚠️ Atrasadas

```tasks
not done
due before today
sort by due
```

## 📅 Próximos 7 dias

```tasks
not done
due after today
due before in 8 days
sort by due
```

---

## 🚀 Projetos ativos

> [!tip] Limite recomendado
> Mantenha **no máximo 3 projetos ativos** ao mesmo tempo. Os demais ficam em `status: espera` para não sobrecarregar a cabeça.

```dataview
TABLE area AS "Área", prioridade AS "Prioridade", prazo AS "Prazo", progresso AS "Progresso"
FROM "03 - Projetos"
WHERE tipo = "projeto" AND status = "ativo"
SORT prazo ASC
```

### ⏸️ Projetos em espera

```dataview
LIST
FROM "03 - Projetos"
WHERE tipo = "projeto" AND status = "espera"
SORT file.name ASC
```

---

## 🧩 Áreas da vida

- [[Faculdade|🎓 Faculdade]]
- [[Estágio|💼 Estágio]]
- [[Carreira|🚀 Carreira]]
- [[Finanças|💰 Finanças]]
- [[Saúde e academia|🏋️ Saúde e academia]]
- [[Vida pessoal|🌿 Vida pessoal]]

## 📚 Conhecimento & Recursos

- **Conhecimento:** [[Programação]] · [[Game Dev]] · [[Design]] · [[AWS]]
- **Recursos:** [[Ideias de jogos]] · [[Referências]] · [[Links e materiais]]

---

## ⏱️ Rotina simples

| Momento | O que fazer | Tempo |
| --- | --- | --- |
| Ao acordar | Abrir este Dashboard + nota de hoje (3 prioridades) | 5 min |
| Durante o dia | Jogar ideias e pendências no [[Ideias e pensamentos rápidos\|Inbox]] | 30 seg |
| Antes de dormir | Marcar o que fez e limpar o Inbox | 5 min |
| Domingo | Criar nota semanal (clique no número da semana no Calendário) | 20 min |
| Início do mês | Revisar [[Objetivos]] e projetos | 30 min |
