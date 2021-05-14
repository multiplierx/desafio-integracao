<p align="center">
  <img src="https://multiplier.com.br/assets/multiplier.svg" width="320" alt="Nest Logo" />
</p>

## Seja Bem vindo à Multiplier!

Estamos felizes de ter você no nosso processo seletivo para Equipe de Integração!

Neste processo, vamos analisar seu conhecimento sobre APIs Rest, Banco de Dados, Javascript (e/ou Typescript) e Git!

### Como enviar o desafio
Crie um repositório público no [Github](https://github.com/). Assim que finalizar seu desafio, envie o link do repositório para o endereço de email `talentos@multiplier.com.br`

Lembre-se que estamos analisando seu conhecimento Git também, então utilize [Commits Semânticos](https://blog.geekhunter.com.br/o-que-e-commit-e-como-usar-commits-semanticos/) no processo de desenvolvimento do desafio.

ex: 
- Caso for esteja desenvolvendo o endpoint de Produtos, crie uma branch chamada `feature/endpoint-produtos`.
- Faça os commits semânticos nela, ex: `feat(Produtos): Criado endpoint GET de produtos`.
- Quando finalizar, realize o merge para a branch `main`


#### A seguir, está seu desafio, boa sorte! 


## DESAFIO

**Resumo:**

- Criar um Banco de dados PostgreSQL
- Criar um Banco de dados MySQL
- Criar uma api para consumir o banco de dados Mysql utilizando Sequelize como ORM
- Criar um serviço cron utilizando [node-schedule](https://www.npmjs.com/package/node-schedule) para buscar dados na API e salvar no banco de dados PostgreSQL

**Diferenciais:**

Aqui na Multiplier, utilizamos a framework [NestJS](https://nestjs.com/) para desenvolver nossos serviços de integração. **Você não precisa utilizar esta mesma framework**, você é livre para escolher a forma que deseja executar o desafio, porém utilizando o **NestJS** você já se familiariza com nossos processos, e requere menos configuração para executar o desafio 😉

Caso opte por utilizar a framework NestJS (preferencialmente), você deve utilizar typescript. Você deverá usar o pacote npm `sequelize-typescript`. Consulte as [docs do NestJs](https://docs.nestjs.com/recipes/sql-sequelize) para maiores informações.

Caso opte por não utilizar a framework, você deverá usar o [`express`](https://expressjs.com/pt-br/starter/hello-world.html) como servidor e o [`sequelize`](https://sequelize.org/master/) como ORM. Você poderá usar ou não typescript se seguir esta opção. Fica ao seu critério.

### Instruções:

## 1. Criar um banco MySQL
### 1.1. Criar as tabelas:

#### Categorias
| coluna | tipo    | descrição                  |
|--------|---------|----------------------------|
| id     | int     | Chave primária da tabela   |
| codigo | varchar | Código da Categoria (slug) |
| titulo | varchar | Título da Categoria        |
| status | int     | 0 - Inativo, 1 - Ativo     |

#### Produtos
| coluna      | tipo    | descrição                |
|-------------|---------|--------------------------|
| id          | int     | Chave primária da tabela |
| idCategoria | int     | id da Categoria (fk)     |
| codigo      | varchar | SKU do Produto           |
| nome        | varchar | Nome do Produto          |
| descricao   | text    | Descrição do Produto     |
| valor       | decimal | Valor do Produto         |
| status      | int     | 0 - Inativo, 1 - Ativo   |

#### Estoque
| coluna     | tipo    | descrição                |
|------------|---------|--------------------------|
| id         | int     | Chave primária da tabela |
| idProduto  | int     | id do Produto (fk)       |
| quantidade | int     | Quantidade em estoque    |
| reserva    | int     | Quantidade reservada     |
| status     | int     | 0 - Inativo, 1 - Ativo   |


<br>

## 2. Desenvolver uma API Restful para cada resource:
	
	- Categorias
	
	[GET] 	 /categorias 		- Lista todas as Categorias
	[GET] 	 /categorias/:id 	- Busca uma Categoria por id
	[POST] 	 /categorias 		- Cria uma Categoria
	[PATCH]  /categorias/:id 	- Edita uma Categoria
	[DELETE] /categorias/:id	- Deleta uma Categoria (deve atualizar o produto setando idCategoria como NULL para produtos que utilizam essa categoria)

	- Produtos
	
	[GET] 	 /produtos 		- Lista todos os Produtos
	[GET] 	 /produtos/:id 		- Busca um Produto por id
	[POST] 	 /produtos 		- Cria um Produto
	[PATCH]  /produtos/:id 		- Edita um Produto
	[DELETE] /produtos/:id		- Deleta um Produto (e seu estoque)

	- Estoque
		* Quando um produto é criado, deve ser criado um estoque com quantidade 0 para o Produto
		* Só pode haver 1 estoque para um mesmo Produto
	
	[GET] 	 /produtos/:id/estoque 	- Lista o estoque para o Produto pelo id
	[PATCH]  /produtos/:id/estoque 	- Edita o Estoque para o Produto pelo id
	[DELETE] /produtos/:id/estoque	- Deve retornar o status [501] - Not Implemented. (não se pode deletar um estoque)

## 3. Criar um banco de dados PostgreSQL com as mesmas tabelas anteriores

## 4. Criar o serviço Cron
Crie um serviço que consome os dados dos endpoints e execute uma determinada função que realize a integração dos dados MySQL => PostgreSQL.

A função deve consumir os endpoints criados anteriormente em um determinado intervalo de tempo (utilizando o [node-cron](https://www.npmjs.com/package/node-schedule)) e salvar os dados no banco PostgreSQL.

Dica: Você pode utilizar o site [Crontab.guru](https://crontab.guru/) para melhor visualizar o formato cron.

# Boa sorte!

-- Equipe Multiplier
