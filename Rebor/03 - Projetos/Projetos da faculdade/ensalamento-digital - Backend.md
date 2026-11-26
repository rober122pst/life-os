---
title: "ensalamento-digital — Backend"
type: doc
tipo: doc
projeto: "[[ensalamento-digital]]"
status: ativo
tags:
  - doc/projeto
  - faculdade
  - backend
  - python
  - django
  - postgresql
aliases:
  - "Backend - ensalamento-digital"
  - "Backend Ensalamento Digital"
created: 2026-11-25
updated: 2026-11-25
---

# 🖥️ Backend — Ensalamento Digital

> [!info] Projeto Pai
> Documentação técnica do backend do [[ensalamento-digital]].
> **Stack:** Python 3.13 · Django · PostgreSQL · Git

---

## ✅ O que já foi desenvolvido

- [x] API REST utilizando **Django**
- [x] Estrutura de usuários e autenticação **JWT**
- [x] Sistema de cadastros e permissões
- [x] Estrutura inicial das regras de ensalamento e alocações
- [x] Integração com **PostgreSQL**
- [x] Documentação automática da API (**OpenAPI**, **Swagger** e **ReDoc**)
- [x] Testes automatizados com suporte a **SQLite**

---

## 🚀 Como executar

### 1. Preparar o ambiente

No **PowerShell**, dentro da pasta do projeto:

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### 2. Configurar o PostgreSQL

Criar o banco e o usuário:

```sql
CREATE USER ensalamento WITH PASSWORD 'ensalamento';
CREATE DATABASE ensalamento OWNER ensalamento;
```

Configurar as variáveis de ambiente no PowerShell:

```powershell
$env:DJANGO_SECRET_KEY="sua-chave"
$env:DATABASE_ENGINE="postgresql"
$env:POSTGRES_DB="ensalamento"
$env:POSTGRES_USER="ensalamento"
$env:POSTGRES_PASSWORD="ensalamento"
$env:POSTGRES_HOST="127.0.0.1"
$env:POSTGRES_PORT="5432"
```

### 3. Inicializar o backend

```powershell
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

> [!tip] Servidor local
> Após subir o backend, a API fica disponível em `http://127.0.0.1:8000/`.

---

## 🔗 Rotas disponíveis

| Rota | Descrição |
| --- | --- |
| `/api/auth/token/` | Login JWT |
| `/api/auth/token/refresh/` | Renovação de token |
| `/api/usuarios/` | Usuários |
| `/api/ensalamento/` | Cadastros e alocações |
| `/api/docs/` | Documentação Swagger |
| `/api/redoc/` | Documentação ReDoc |

---

## 📁 Organização das pastas

| Diretório | Responsabilidade |
| --- | --- |
| `config/` | Configurações do Django |
| `contas/` | Usuários, autenticação e permissões |
| `ensalamento/` | Models, serializers e regras de ensalamento |

> [!note] Banco de dados e variáveis de ambiente
> O **PostgreSQL** é o banco padrão. O **SQLite** pode ser utilizado para testes rápidos. As variáveis de ambiente também estão documentadas no arquivo `.env.example`.

---

## 🔗 Links relacionados

- Projeto principal: [[ensalamento-digital]]
- Base técnica: [[Programação]] · [[Stack Web, Mobile, Backend e IA]]
