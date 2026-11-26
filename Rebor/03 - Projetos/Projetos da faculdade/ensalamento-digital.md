---
title: "ensalamento-digital"
type: projeto
tipo: projeto
status: ativo
area: Faculdade
prioridade: alta
prazo: 2026-12
progresso: ""
tags:
  - projeto/ativo
  - faculdade
  - uninassau
  - web
  - react
  - typescript
aliases:
  - "Ensalamento Digital"
  - "ensalamento-digital (UNINASSAU)"
created: 2026-11-25
updated: 2026-11-25
---

# 🏫 ensalamento-digital (UNINASSAU)

> [!info] Projeto Ativo
> Plataforma web de **Digital Signage** e **agendamento de salas de aula** para a UNINASSAU Paulista. Rober atua como **co-Scrum Master** ao lado de [[Pessoas e Vínculos#Bia|Bia]].

---

## 🎯 Objetivo

Fornecer uma plataforma web para exibição em painéis (*Digital Signage*) e gerenciamento/agendamento de salas de aula da UNINASSAU.

---

## 🛠️ Stack Técnica

| Camada | Tecnologias |
| --- | --- |
| **Frontend** | React, TypeScript |
| **Estilização** | Tailwind CSS, Lucide React |
| **Estado & Rotas** | Zustand, React Router |
| **Comunicação HTTP** | Axios |
| **Backend** | Python 3.13, Django, JWT, PostgreSQL (SQLite para testes), OpenAPI / Swagger / ReDoc |

---

## 👥 Papéis e Equipe

- **Co-Scrum Masters:** [[Perfil - Rober|Rober]] e [[Pessoas e Vínculos#Bia|Bia]]
- **Contexto:** [[Faculdade]] (4º semestre de ADS — UNINASSAU Paulista)

---

## ⚡ Próxima ação

- [ ] <!-- A completar -->

## 📋 Tarefas

- [ ] Acompanhar sprints e entregas com [[Pessoas e Vínculos#Bia|Bia]]
- [ ] <!-- A completar -->

## ✅ Critérios de conclusão

> [!note] Escopo Front Web (baseado em [[Documento_de_Requisitos_Ensalamento_v0.6_beta (3).pdf]] e [[ensalamento-digital - Backend]])
> Cobre **Web Administrativo** (coordenação), **Web Público/Professor** e **Painel da Sala dos Professores (TV em modo quiosque)**. Itens marcados com **(S — confirmar)** são suposições do Cap. 10 da v0.6 beta e não devem ser implementados antes do alinhamento com a equipe/orientadores.

### 🔐 Autenticação, Perfis e Integração com API
- [x] Login de professor e coordenação integrado a `/api/auth/token/` com erro genérico para credencial inválida e aviso de conta desativada (`RF005`, `NF010`) ✅ 2026-11-25
- [ ] Renovação automática de JWT via `/api/auth/token/refresh/`, logout limpando sessão e controle de rotas/UI por perfil (`RF006`, `RF009`, `RF010`, `RN008`)
- [ ] Fluxos de primeiro acesso com definição de senha e recuperação de senha por e-mail institucional — *Importante* (`RF007`, `RF008` — confirmar se haverá login institucional)
- [ ] Front Web e Painel 100% integrados à API Django real (`/api/usuarios/`, `/api/ensalamento/`) seguindo o contrato OpenAPI/Swagger (`/api/docs/` e `/api/redoc/`) sobre HTTPS (`NF013`, `NF025`)

### 🗂️ Web Administrativo — Cadastros Base (Coordenação)
- [ ] CRUD completo de **blocos**, **salas** (bloco, andar, capacidade, tipo, recursos), **cursos**, **turmas** (nº de alunos), **disciplinas** (recursos exigidos), **professores**, **grade de horários** e **semestre letivo vigente** (`RF011`–`RF018`, `RN012`), usando desativação em vez de exclusão quando houver vínculo
- [ ] Gestão de usuários autenticados: cadastrar, editar, definir perfil e desativar/reativar sem exclusão definitiva (`RF072`)
- [ ] *(S — confirmar, Importante)* Telas de calendário acadêmico (`RF019`/`RN011`), bloqueio de sala por manutenção/evento (`RF020`/`RN006`) e importação inicial por planilha (`RF021`)

### 📅 Web Administrativo — Alocação, Conflitos e Trocas
- [ ] Tela de alocação de turma/disciplina/professor em sala, dia e horário exibindo o registro exato em caso de conflito bloqueante de sala, professor ou turma (`RF022`–`RF025`, `RN001`–`RN003`)
- [ ] Avisos não bloqueantes com confirmação explícita para capacidade insuficiente da sala e ausência de recursos exigidos (`RF026`, `RF027`, `RN004`, `RN005`)
- [x] Grade do ensalamento com filtros por curso, período, turno, bloco, professor e semestre, além de estado vazio com ação de limpar filtros (`RF029`) ✅ 2026-11-25
- [ ] Fluxo de troca de sala em alocação publicada (pontual para uma data ou restante do semestre) com motivo, validação de conflitos e geração de histórico/aviso (`RF033`–`RF035`, `RN007`)
- [ ] Exportação do ensalamento em formato imprimível com filtros por curso, turno e bloco e **data de geração impressa** — *Importante, Documentado* (`RF069`)
- [ ] *(S — confirmar)* Fluxo **rascunho → publicar ensalamento** com resumo de pendências (`RF030`, `RN010` — *Essencial*, aguarda Figura 13 no Figma), bloqueio em sala indisponível (`RF028`), repetição em vários horários (`RF032`), cancelamento de aula (`RF040`) e fila de decisão de pedidos de troca/reserva (`RF038`)
- [ ] *(S — confirmar, Desejável)* Duplicar ensalamento do semestre anterior (`RF031`), registrar professor substituto (`RF041`), tela de consulta ao histórico (`RF042`) e relatório de ocupação de salas (`RF071`)

### 📺 Painel da Sala dos Professores (TV — Modo Quiosque)
- [ ] Exibição sem login e sem interação do ensalamento do turno corrente (turma, disciplina, professor, horário e sala) com hora da última atualização visível e mensagem quando não houver aulas (`RF053`)
- [ ] Atualização automática do painel sem recarregamento manual dentro do intervalo definido (`RF054`, `NF006`)
- [ ] Modo de falha / degradação controlada: com a API indisponível, nunca exibir erro ou tela em branco — manter o último quadro recebido sinalizando claramente o horário da última atualização (`RF056`, `NF009`)
- [ ] Legibilidade à distância e compatibilidade validadas no navegador/proporção da TV da sala dos professores (`NF002`, `NF020`, `NF023`)
- [ ] *(S — confirmar, Importante)* Destaque visual para aulas alteradas ou canceladas no dia (`RF055`)

### 🌐 Web Público (Aluno) e Professor
- [ ] Consulta das próprias aulas do dia e da semana pelo professor autenticado (`RF048`, `RF049`) e busca por sala, disciplina, professor ou turma respeitando permissões do perfil (`RF061`)
- [ ] Tratamento explícito de carregamento, estados vazios e mensagens de erro amigáveis (sem códigos técnicos nem tela em branco) em todas as telas (`RF060`)
- [ ] Termos de uso e política de privacidade acessíveis na web (inclusive sem login), declarando que nenhum dado pessoal de aluno é coletado (`RF066`, `NF019`, `RN009`)
- [ ] *(S — confirmar)* Consulta pública do aluno **sem login** com seleção de curso + período + turno salva localmente no navegador, troca rápida, aulas do dia/semana e destaque de alterações recentes (`RF001`–`RF004`, `RF043`, `RF044`, `RF047`, `NF016`, `NF017` — aguarda Figuras 1 e 4 no Figma) e pedido/acompanhamento de troca ou reserva pelo professor (`RF036`, `RF037`, `RF039` — aguarda Figura 7)

### 🚀 Qualidade, Deploy e Homologação Final (Entrega: 01/12/2026)
- [ ] Interface em português do Brasil (fuso de Recife), consistente com o glossário do projeto, compatível com navegadores atuais, responsiva (desktop, mobile e TV) sem rolagem horizontal e atendendo WCAG 2.1 AA no escopo aplicável (`NF001`, `NF004`, `NF022`–`NF024`, `NF027`)
- [ ] Front Web e Painel publicados e estáveis no ambiente de demonstração na Microsoft Azure (`NF028`)
- [ ] Roteiro obrigatório de homologação da Seção 11.2 validado ponta a ponta na parte web sem intervenção manual no banco: login coordenação (`RF005`) → cadastros base (`RF011`–`RF016`) → alocação e recusa de conflito (`RF022`, `RF023`) → publicação (`RF030`) → decisão de pedido e troca de sala (`RF038`, `RF033`) → atualização automática e resiliência offline do painel da TV (`RF054`, `RF056`) → histórico de alteração (`RF034`)

## 📄 Documentação

- [[ensalamento-digital - Backend|🖥️ Documentação do Backend (Django + PostgreSQL)]]
- Stack de referência: [[Stack Web, Mobile, Backend e IA]] · [[Programação]]

## 🧭 Decisões tomadas

- Adoção de Zustand para gerenciamento de estado e Axios para integração com APIs.

## 🚧 Problemas e bloqueios

<!-- A completar -->

## 🔗 Links e referências

- GitHub: [Repositório](https://github.com/Gabriel-Oliveira-Prado/ensalamento-digital)
- Figma: [Protótipo]([https://www.figma.com/design/vw0nO1QIAHjhwJATDHIRNc/Untitled?node-id=0-1&t=QaNaSZxaWBSH5uAg-1](https://www.figma.com/design/vw0nO1QIAHjhwJATDHIRNc/Untitled?node-id=0-1&t=QaNaSZxaWBSH5uAg-1 "https://www.figma.com/design/vw0nO1QIAHjhwJATDHIRNc/Untitled?node-id=0-1&t=QaNaSZxaWBSH5uAg-1")
- Requisitos: [[Documento_de_Requisitos_Ensalamento_v0.6_beta (3).pdf]]