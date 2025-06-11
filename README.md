# 🔐 Autenticação e Autorização com Keycloak + Node.js

Este projeto é um exemplo prático de como integrar o Keycloak em uma aplicação Node.js utilizando `express`, com autenticação de usuários.

## 🚀 Tecnologias utilizadas

- Node.js
- Express
- Keycloak Connect
- Express-session
- CORS
- Dotenv
- Axios

---

## 📦 1. Inicializando o projeto Node.js

```bash
npm init -y
```

## 📚 2. Instalando dependências

```bash
npm install express cors express-session keycloak-connect dotenv axios
```

## 📁 3. Estrutura básica do projeto

```
exemplo-keycloak/
├── src/
│   ├── routes/
│   │   └── index.js
│   └── server.js
├── .env
├── .gitignore
└── README.md
```

## 🔧 4. Configurando o Keycloak

### 4.1. Instalando o Keycloak localmente (via container)

```bash
docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:24.0.3 start-dev
```

Acesse: [http://localhost:8080](http://localhost:8080)

### 4.2. Criando Realm, Client e Usuário

1. Acesse o painel do Keycloak: http://localhost:8080/
2. Crie um novo **Realm**: `meu-realm`
3. Crie um novo **Client**:
   - Client ID: `meu-app-node`
   - Client Type: `Public`
   - Root URL: `http://localhost:3000`
   - Ative: `Standard Flow`
   - Desative: `Direct Access Grants` se não for necessário
   - Habilite o campo `Web Origins` com `*` (ou seu domínio real)
4. Crie um **usuário** com senha e marque como “Habilitado”
   - Role: `user` ou personalizada
   - Defina senha no menu "Credenciais"

---

## 🔐 5. Protegendo rotas com Keycloak

A função `keycloak.protect()` pode aceitar:
- Sem argumento → qualquer usuário autenticado
- Com argumento → uma role específica


## 🔄 6. Rodando o projeto

```bash
node src/server.js
```

ou se tiver configurado no package.json
```bash
npm run dev
```

---

## 🧪 Testando a aplicação

1. Acesse: `http://localhost:3000/` → Página pública
2. Acesse: `http://localhost:3000/protegido` → Redireciona para o login do Keycloak
3. Faça login com o usuário criado → Retorna conteúdo da rota protegida

---

