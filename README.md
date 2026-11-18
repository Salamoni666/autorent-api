# AutoRent API – Entrega Projeto P2 (Back-End)

API REST de locação de veículos (Node.js + TypeScript + Express + Prisma + MySQL).
FATEC – Tecnologia em Sistemas para Internet – 3º Termo – Prof. Vinícius Hungaro.

O código-fonte está no arquivo **`BackEnd-ProjetoP2.zip`** deste repositório.

## Pré-requisitos

- [Node.js](https://nodejs.org/) v20 ou superior
- [Git](https://git-scm.com/)
- [Docker Desktop](https://www.docker.com/) (para subir o MySQL) **ou** um MySQL 8 local

## Instalação

### 1. Baixar o repositório e extrair o zip

```bash
git clone https://github.com/SEU_USUARIO/SEU_REPOSITORIO.git
cd SEU_REPOSITORIO
```

Extraia o `BackEnd-ProjetoP2.zip` (botão direito → "Extrair tudo" no Windows) ou, pelo terminal:

```bash
# Linux / macOS / Git Bash
unzip BackEnd-ProjetoP2.zip

# Windows (PowerShell)
Expand-Archive BackEnd-ProjetoP2.zip -DestinationPath .
```

Entre na pasta extraída:

```bash
cd BackEnd-ProjetoP2
```

### 2. Instalar as dependências

```bash
npm install
```

### 3. Configurar as variáveis de ambiente

```bash
# Linux / macOS / Git Bash
cp .env.example .env

# Windows (PowerShell ou CMD)
copy .env.example .env
```

O `.env.example` já vem com valores prontos para o Docker (usuário `root`, senha `root`, banco `autorent_db`).

### 4. Subir o banco de dados MySQL

**Opção A – Docker (recomendado):**

```bash
docker compose up -d
```

**Opção B – MySQL já instalado na máquina:** crie o banco `autorent_db` e ajuste a
`DATABASE_URL` no `.env` (`mysql://USUARIO:SENHA@localhost:3306/autorent_db`).
Se a porta 3306 já estiver em uso por outro MySQL, não suba o Docker: use esta opção.

### 5. Criar as tabelas e popular o banco

```bash
npm run prisma:migrate
npm run prisma:seed
```

### 6. Iniciar a API

```bash
npm run dev
```

- API: http://localhost:3000
- Documentação Swagger: http://localhost:3000/docs

## Credenciais de teste (criadas pelo seed)

| Perfil    | E-mail                  | Senha          |
| --------- | ----------------------- | -------------- |
| Gestor    | `gestor@autorent.com`   | `admin123`     |
| Atendente | `atendente@autorent.com`| `atendente123` |

## Testes com Postman

Importe o arquivo `autorent.postman_collection.json` (dentro da pasta extraída).

## Problemas comuns

- **`Can't reach database server`**: confirme que o container está de pé (`docker ps`) e que a `DATABASE_URL` do `.env` está correta.
- **Porta 3306 ou 3000 ocupada**: encerre o serviço que está usando a porta ou altere `PORT` no `.env`.
- **Erro de Prisma Client**: rode `npx prisma generate`.
