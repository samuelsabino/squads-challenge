# squads-challenge

<!-- ABOUT THE PROJECT -->
## Sobre o Projeto

O Squads Challenge é uma API desenvolvida para controle de produtos no geral. A interface fornece o gerenciamento de produtos forma geral, podendo criar, buscar, atualizar e apagar produtos dentro da base.

## Pré-requisitos

* NodeJS 12+
* Docker

### Feito Com

- [Express](https://expressjs.com/pt-br/)
- [TypeScript](https://www.typescriptlang.org/)
- [Docker](https://www.docker.com/)
- [MongoDB](https://www.mongodb.com/)
- [TypeORM](https://typeorm.io/)
- [Jest](https://jestjs.io/)

## Começando

Para conseguir a aplicação com cópia local dos arquivos, siga os passos abaixo.

### Instalação

1. Clone o repositório com o comando `git clone https://github.com/SamuelSabino/squads-challenge.git`.

2. Depois de clonado, na raiz do projeto, execute o comando abaixo para a instalação das dependências.


```text
npm install
```

3. Com o docker instalado, execute o comando abaixo para inicialização do servidor:

```text
npm run dcup
```
Apos executado o comando, o projeto era buildar e rodar tanto o projeto quanto um container do mongoDB para execução e utilização da aplicação.

## Utilizando a aplicação

## Criação de produto

 - **`POST /products`**: Para cadastrar um produto a rota precisa receber, dentro do corpo da requisição, um objeto em formato JSON contendo os campos `name`, `description` e `value`:

URL:

 ```
 [POST] http://localhost:8080/products
 ```

Objeto que será enviado no corpo da requisição:

 ```
{
  "name": "Nome do produto",
  "description": "Descrição do produto",
  "value": "100"
}
 ```

 Será retornado o produto cadastrado juntamente com o seu identificador único:
 ```
{
  "error": false,
  "result": {
    "active": true,
    "_id": "602abc58fbfe92002165e515",
    "name": "Nome do produto",
    "description": "Descrição do produto",
    "value": "100",
    "created": "2021-02-01T15:00:00.000Z",
    "__v": 0
  },
  "message": "Product successfully created."
}
 ```

 ## Busca um produto

 - **`GET /products/:id`**: Para buscar um produto em especifico a rota precisa receber na sua URL o identificador do produto:

URL:

 ```
 [GET] http://localhost:8080/products/602abc58fbfe92002165e515
 ```

 Será retornado o produto correspondente aquele identificador:
 ```
{
  "error": false,
  "result": {
    "active": true,
    "_id": "602abc58fbfe92002165e515",
    "name": "Nome do produto",
    "description": "Descrição do produto",
    "value": "100",
    "created": "2021-02-01T15:00:00.000Z",
    "__v": 0
  }
}
 ```
 ## Busca de vários produtos (lista de produtos)

 - **`GET /products/`**: Para buscar uma lista de produtos basta apontar para a rota padrão definida:

URL:

 ```
 [GET] http://localhost:8080/products/
 ```

 Será retornado uma lista de produtos cadastrados:
 ```
{
  "error": false,
  "result": [
    {
      "active": true,
      "_id": "602abc58fbfe92002165e515",
      "name": "Nome do produto",
      "description": "Descrição do produto",
      "value": "100",
      "created": "2021-02-01T15:00:00.000Z",
      "__v": 0
    }
  ]
}
 ```

 ## Atualizar um produto

 - **`PATCH /products/id`**: Para atualizar um produto a rota precisa receber, dentro do corpo da requisição, um objeto em formato JSON contendo os campos `name`, `description` e `value` com os valores que serão atualizados dentro do dado já armazenado:

URL:

 ```
 [PATCH] http://localhost:8080/products/602abc58fbfe92002165e515
 ```

Objeto que será enviado no corpo da requisição:

 ```
{
  "name": "Nome do produto atualizado",
  "description": "Descrição do produto atualizado",
  "value": "500"
}
 ```

 Será retornado uma lista de produtos cadastrados:
 ```
{
  "error": false,
  "result": [
    {
      "active": true,
      "_id": "602abc58fbfe92002165e515",
      "name": "Nome do produto atualizado",
      "description": "Descrição do produto atualizado",
      "value": "500"
      "created": "2021-02-01T15:00:00.000Z",
      "__v": 0
    }
  ]
}
 ```

  ## Deletar um produto

 - **`DELETE /products/id`**: Para deletar um produto em especifico a rota precisa receber na sua URL o identificador do produto:

URL:

 ```
 [DELETE] http://localhost:8080/products/602abc58fbfe92002165e515
 ```

 Será retornado uma lista de produtos cadastrados:
 ```
{
  "error": false,
  "result": "Product successfully deleted"
}
 ```

 ## Convenções
 ### Estilo

* eslint com o padrão de regras [standard](https://standardjs.com).

### Nomenclatura das Pastas

* utilização do estilo de escrita kebab-case para todas as pastas.

### Arquivos
* kebab-case utilizado para todos os arquivos.
* arquivos de testes utilizando o padrão *.spec.ts (para testes de unidade) e *.test.ts (para testes de integração).

## Visão Geral da Arquitetura

```text
├── src/
│   ├── modules/
│   │   └── products/
|   │   │   └── dtos/
|   |   │   │   └── *DTO.interface.ts
|   │   │   └── infra/
|   |   │   │   └── fake/
|   |   |   │   │   └── repositories/
|   |   |   |   │   │   └── *.repository.ts
|   |   │   │   └── http/
|   |   |   │   │   └── controllers/
|   |   |   |   │   │   └── *.controller.ts
|   |   |   │   │   └── routers/
|   |   |   |   │   │   └── *.router.ts
|   |   |   │   │   └── schemas/
|   |   |   |   │   │   └── *.schema.ts
|   |   │   │   └── mongo/
|   |   |   │   │   └── models/
|   |   |   |   │   │   └── *.model.ts
|   |   |   │   │   └── repositories/
|   |   |   |   │   │   └── *.repository.ts
|   │   │   └── interfaces/
|   |   │   │   └── *.interface.ts/
|   │   │   └── services/
|   |   │   │   └── *.service.ts/
│   ├── shared/
|   │   ├── errors/
|   |   │   ├── *.error.ts
|   │   ├── infra/
|   |   │   └── http/
|   |   │   │   └── routers/
|   |   |   │   │   └── index.router.ts
|   |   │   │   └── app.ts
|   |   │   │   └── server.ts
|   │   │   └── mongo/
|   |   │   │   └── interfaces/
|   |   |   │   │   └── *.interface.ts
|   |   │   │   └── repositories/
|   |   |   │   │   └── *.repository.ts
|   |   │   │   └── index.ts
|   |   │   │   └── transaction.ts
├── .dockerignore
├── .eslintignore
├── .eslintrc.js
├── .gitignore
├── babel.config.js
├── docker-compose.yml
├── dockerfile
├── jest.config.ts
├── nodemon.json
├── package.json
├── tsconfig.json
└── README.md
```