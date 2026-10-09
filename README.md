 # Sistema de Estacionamento - Back-end

Back-end do sistema de estacionamento desenvolvido para a disciplina **Programacao para Dispositivos Moveis II**.

A API permite cadastrar, consultar, alterar e excluir proprietarios e veiculos. Cada veiculo pode ser associado a um proprietario por meio do campo `fk_proprietario`.

## Tecnologias

- Node.js
- Express
- Sequelize
- MySQL
- CORS
- Body-parser

## Pre-requisitos

- Node.js instalado
- MySQL instalado e em execucao
- Banco de dados chamado `estacionamento`

Crie o banco de dados no MySQL:

```sql
CREATE DATABASE estacionamento;
```

O projeto esta configurado para acessar o MySQL local com:

| Configuracao | Valor |
| --- | --- |
| Host | `localhost` |
| Banco | `estacionamento` |
| Usuario | `root` |
| Senha | `root` |

Esses valores estao definidos em `Model/db.js` e devem ser alterados caso sejam diferentes no ambiente local.

## Instalacao e execucao

Instale as dependencias:

```bash
npm install
```

Inicie a API:

```bash
node index.js
```

O servidor sera iniciado em:

```text
http://localhost:8081
```

O projeto nao possui scripts npm configurados. Os comandos `sync` dos models tambem estao comentados; por isso, o banco e as tabelas devem estar preparados conforme o material da atividade antes dos testes.

## Estrutura do projeto

```text
EstacionamentoBackend/
├── Controller/
│   ├── ProprietarioController.js
│   └── VeiculoController.js
├── Model/
│   ├── db.js
│   ├── Proprietario.js
│   └── Veiculo.js
├── index.js
├── package.json
└── README.md
```

- `index.js`: configura o Express, o CORS, o recebimento de JSON e as rotas da API.
- `Model/db.js`: cria a conexao com o MySQL usando Sequelize.
- `Model/Proprietario.js`: define a tabela e os campos de proprietarios.
- `Model/Veiculo.js`: define a tabela e os campos de veiculos.
- `Controller/ProprietarioController.js`: implementa o CRUD de proprietarios.
- `Controller/VeiculoController.js`: implementa o CRUD de veiculos.

## Endpoints

### Proprietarios

| Metodo | Rota | Descricao |
| --- | --- | --- |
| GET | `/proprietario/` | Lista todos os proprietarios |
| GET | `/proprietario/:id` | Busca um proprietario pelo ID |
| POST | `/proprietario/` | Cadastra um proprietario |
| PUT | `/proprietario/:id` | Atualiza um proprietario |
| DELETE | `/proprietario/:id` | Exclui um proprietario |

Exemplo de dados para `POST` e `PUT`:

```json
{
	"nome": "Maria da Silva",
	"cpf": "12345678900"
}
```

### Veiculos

| Metodo | Rota | Descricao |
| --- | --- | --- |
| GET | `/veiculo/` | Lista todos os veiculos |
| GET | `/veiculo/:id` | Busca um veiculo pelo ID |
| POST | `/veiculo/` | Cadastra um veiculo |
| PUT | `/veiculo/:id` | Atualiza um veiculo |
| DELETE | `/veiculo/:id` | Exclui um veiculo |

Exemplo de dados para `POST` e `PUT`:

```json
{
	"placa": "ABC1D23",
	"ano": 2024,
	"mensalidade": 150.00,
	"fk_proprietario": 1
}
```

O valor de `fk_proprietario` deve corresponder ao `id_proprietario` de um proprietario cadastrado.

## Teste rapido

Com o servidor em execucao, acesse:

```text
GET http://localhost:8081/
```

A resposta esperada e:

```text
Estou aqui
```

As demais rotas podem ser testadas com ferramentas como Postman, Insomnia ou pelo aplicativo React Native.

## Front-end e integracao

O front-end em React Native esta em um repositorio separado:

[sistema-de-estacionamento-frontend](https://github.com/Felipe-SMZ/sistema-de-estacionamento-frontend)

Ele consome esta API usando HTTP, por exemplo, com Axios. O fluxo de comunicacao e:

```text
React Native -> API Express -> Sequelize -> MySQL
```

Este repositorio contem somente o back-end da aplicacao. A organizacao do front-end nas pastas `app`, `components`, `constants` e `hooks` esta documentada e implementada no repositorio do front-end.
