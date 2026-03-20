# Digital Store Backend - Projeto GTech3

Esta é uma API completa para e-commerce desenvolvida como parte do projeto **GTech3**. A aplicação fornece uma base sólida para gerenciamento de usuários, categorias e produtos, incluindo autenticação segura e filtros avançados de busca.

## 🚀 Tecnologias Utilizadas

O projeto foi construído utilizando as seguintes tecnologias e bibliotecas:

- **[Node.js](https://nodejs.org/)** - Ambiente de execução JavaScript.
- **[Express](https://expressjs.com/)** - Framework web para Node.js.
- **[Sequelize](https://sequelize.org/)** - ORM para Node.js (PostgreSQL).
- **[PostgreSQL](https://www.postgresql.org/)** - Banco de dados relacional.
- **[JWT (JSON Web Token)](https://jwt.io/)** - Autenticação segura.
- **[Bcryptjs](https://www.npmjs.com/package/bcryptjs)** - Hash de senhas.
- **[Jest](https://jestjs.io/)** & **[Supertest](https://github.com/ladjs/supertest)** - Testes automatizados e de integração.
- **[CORS](https://www.npmjs.com/package/cors)** - Configuração de segurança para acesso externo.

## 📋 Pré-requisitos

Antes de começar, você precisará ter instalado em sua máquina:
- [Node.js](https://nodejs.org/) (versão 16 ou superior recomendada)
- [PostgreSQL](https://www.postgresql.org/) (ou acesso a uma instância remota)

## 🔧 Instalação e Configuração

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/carimbamba/projeto-backend-gtech3.git
   cd projeto-backend-gtech3/project-root
   ```

2. **Instale as dependências:**
   ```bash
   npm install
   ```

3. **Configure as variáveis de ambiente:**
   Crie um arquivo `.env` na pasta `project-root` (ou renomeie o existente) e preencha com suas credenciais:
   ```env
   PORT=3001
   JWT_SECRET=sua_chave_secreta_aqui
   JWT_EXPIRES_IN=1d

   DB_HOST=seu_host_db
   DB_USER=seu_usuario_db
   DB_PASSWORD=sua_senha_db
   DB_NAME=seu_nome_db
   DB_PORT=5432
   DB_DIALECT=postgres
   ```

## 🏃 Executando o Projeto

- **Modo de Desenvolvimento (com Nodemon):**
  ```bash
  npm run dev
  ```

- **Modo de Produção:**
  ```bash
  npm start
  ```

- **Executar Testes:**
  ```bash
  npm test
  ```

## 🛣️ Endpoints da API

A API está versionada sob o prefixo `/v1`.

### Usuários (`/v1/usuario`)
- `POST /token` - Gera token de autenticação (Login).
- `POST /` - Cria um novo usuário.
- `GET /:id` - Retorna dados de um usuário específico.
- `PUT /:id` - Atualiza dados do usuário (Requer Autenticação).
- `DELETE /:id` - Remove um usuário (Requer Autenticação).

### Categorias (`/v1/categoria`)
- `GET /pesquisa` - Lista categorias com filtros (ex: `use_in_menu`).
- `GET /:id` - Retorna uma categoria específica.
- `POST /` - Cria uma nova categoria.
- `PUT /:id` - Atualiza uma categoria.
- `DELETE /:id` - Remove uma categoria.

### Produtos (`/v1/produto`)
- `GET /pesquisa` - Busca avançada de produtos.
  - **Parâmetros de Query:**
    - `limit` (número): Limite de resultados por página (padrão: 12).
    - `page` (número): Número da página (padrão: 1).
    - `fields` (string): Campos a serem retornados, separados por vírgula (ex: `id,nome,preco`).
    - `match` (string): Busca por texto livre no `nome` e `description` do produto.
    - `category_ids` (string): IDs de categorias, separados por vírgula (ex: `1,2,3`).
    - `price-range` (string): Faixa de preço (ex: `10-100`).
    - `option[ID]` (string): Filtra por opções de produto. `ID` é o ID da opção e o valor são os valores da opção, separados por vírgula (ex: `option[1]=vermelho,azul`).
- `GET /:id` - Retorna detalhes completos do produto, incluindo imagens e opções associadas.
- `POST /` - Cria um novo produto (Requer Autenticação).
  - **Payload esperado:** Inclui `category_ids` (array de IDs), `images` (array de objetos `{ content: base64, type: 'image/jpeg' }`) e `options` (array de objetos `{ title: 'Cor', value: ['Vermelho', 'Azul'] }`).
- `PUT /:id` - Atualiza um produto existente (Requer Autenticação).
  - **Payload esperado:** Similar ao `POST`, permite atualizar campos do produto e suas associações. Para imagens e opções, é possível adicionar novas, atualizar existentes ou marcar para exclusão (`{ id: 1, deleted: true }`).
- `DELETE /:id` - Remove um produto (Requer Autenticação).

## 🗄️ Banco de Dados

O projeto utiliza o Sequelize para gerenciar o banco de dados. Ao iniciar o servidor, a aplicação tenta sincronizar automaticamente os modelos com o banco de dados usando `sync({ alter: true })`.

**Modelos principais:**
- `User`: Gerenciamento de usuários e autenticação.
- `Category`: Categorização de produtos.
- `Product`: Dados centrais do produto.
- `ProductImage`: Imagens associadas aos produtos.
- `ProductOption`: Opções customizáveis (tamanho, cor, etc).

## 🧪 Testes

Os testes de integração cobrem os fluxos principais de criação e manipulação de dados, garantindo que as regras de negócio e autenticação estejam funcionando corretamente.

---
Desenvolvido por [carimbamba](https://github.com/carimbamba).
