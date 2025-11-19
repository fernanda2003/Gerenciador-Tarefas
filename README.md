## Grupo

- Joao Pedro Silva Antunes
- Fernanda Aparecida Figueiredo da Silva
- Alan Araújo da Silveira
- Ana Cláudia Monteiro Misquita

# 🗂️ Gerenciador de Tarefas — Visão Geral do Projeto

O Gerenciador de Tarefas é uma plataforma para organização e gerenciamento de atividades. Ela permite operações CRUD (Criar, Ler, Atualizar, Deletar) sobre usuários e tarefas e foi desenvolvida com foco acadêmico usando uma arquitetura modular (MVC) para facilitar manutenção e evolução.

Este repositório contém dois módulos principais:

- `Front/` — aplicação front-end (Next.js) pronta para rodar localmente ou em container.
- `BackEnd/` — API REST desenvolvida em Flask com persistência via SQLite e documentação via Swagger (Flask-RESTX).

## Objetivos do projeto

- Fornecer uma aplicação completa com front-end e back-end que permita gerenciar tarefas (CRUD).
- Demonstrar uso de boas práticas (estrutura modular, documentação de API, containerização).

## Tecnologias principais

- Front-end: Next.js (React), Tailwind CSS (opcional), Turbopack
- Back-end: Python, Flask, Flask-RESTX (Swagger), Flask-CORS, SQLAlchemy (SQLite)
- Outros: Docker (Dockerfile disponível), Git para versionamento

## Estrutura do repositório

- `Front/` — código do front-end (Next.js). Principais paths:

  - `src/app/` — páginas e componentes (home, tasks, users)
  - `package.json`, `next.config.ts`, `tailwind.config.js` — arquivos de configuração

- `BackEnd/` — API em Flask:
  - `app.py` — inicializador da aplicação e registro de blueprints
  - `controller/` — rotas/blueprints (`usuario.py`, `agenda.py`)
  - `models/` — lógica de acesso a dados (`bancoSQL.py`, `usuario.py`, `agenda.py`)
  - `swagger/` — configuração do Swagger / namespaces

## Requisitos (Checklist)

O projeto foi desenhado para atender aos seguintes requisitos (marquei o que já está implementado):

- [x] Aplicação com front-end em Next.js (pasta `Front/`) com rotas e componentes.
- [x] Estilização com Tailwind (configuração presente em `Front/tailwind.config.js`).
- [x] CRUD na API (endpoints para usuários e tarefas no back-end).
- [x] Controle de versão (use Git/GitHub; mantenha commits descritivos).
- [x] README explicando propósito, stack e instruções para rodar (este arquivo).

## Como executar (Rápido)

Siga as instruções abaixo para executar o projeto localmente em ambiente Windows (PowerShell). As instruções cobrem o back-end (Flask) e o front-end (Next.js).

IMPORTANTE: Recomendo criar ambientes separados (virtualenv para Python / Node para front) e seguir os passos na ordem Back-end → Front-end.

### 1) Back-end (API Flask)

1. Abra um terminal e navegue para a pasta do back-end:

```powershell
cd "d:\faculdade\Nova pasta\ProjetoFull\BackEnd"
```

2. (Opcional, recomendado) Crie e ative um ambiente virtual Python:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

3. Instale as dependências necessárias (exemplo):

```powershell
pip install flask flask-cors flask-restx sqlalchemy
```

4. Inicie a API:

```powershell
python app.py
```

A API estará disponível em http://localhost:5000. A documentação Swagger (Flask-RESTX) estará em http://localhost:5000/api/docs (conforme `swaggerinit.py` configura `doc='/docs'` com prefix `/api`).

Observações sobre o banco:

- O projeto usa SQLite com o arquivo `meubanco.db` criado na pasta do back-end (veja `models/bancoSQL.py`). Se quiser resetar a base, remova `meubanco.db` e reinicie a aplicação — o schema será recriado.

### 2) Front-end (Next.js)

1. Abra outro terminal e vá para a pasta `Front`:

```powershell
cd "d:\faculdade\Nova pasta\ProjetoFull\Front"
```

2. Instale dependências Node:

```powershell
npm install
```

3. Rode em modo desenvolvimento:

```powershell
npm run dev
```

O Next.js costuma abrir em http://localhost:3000 (o terminal mostrará a porta). A aplicação do front deve consumir a API em `http://localhost:5000` (ou ajuste as URLs no código conforme necessário).

### 3) Testando o CRUD (exemplos rápidos)

Endpoints principais fornecidos pelo Back-end (pasta `controller`):

- Usuários:

  - GET /user — lista usuários
  - GET /user/<id> — obtém um usuário
  - POST /user — cria usuário (body JSON {"nome": "", "email": ""})
  - PUT /user/<id> — atualiza usuário
  - DELETE /user/<id> — deleta usuário

- Tarefas (agenda):
  - GET /task — lista tarefas
  - POST /task — cria tarefa (body JSON {"titulo":"","descricao":"","id_usuario":1,"prazo_final":"YYYY-MM-DD"})
  - PUT /task/<id> — atualiza tarefa
  - DELETE /task/<id> — deleta tarefa

Exemplo usando curl para criar usuário:

```powershell
curl -X POST http://localhost:5000/user -H "Content-Type: application/json" -d '{"nome":"João","email":"joao@example.com"}'
```

Ou usando a interface Swagger em `http://localhost:5000/api/docs` para testar interativamente.

## Docker (opção)

Ambas as pastas (`Front/` e `BackEnd/`) contêm `dockerfile` (ou `Dockerfile`) que permitem conteinerizar cada parte. Para rodar com Docker:

1. Buildar a imagem do back-end:

```powershell
cd BackEnd
docker build -t gerenciador-backend .
docker run -p 5000:5000 gerenciador-backend
```

2. Buildar e rodar o front (ajuste se necessário):

```powershell
cd Front
docker build -t gerenciador-front .
docker run -p 3000:3000 gerenciador-front
```



