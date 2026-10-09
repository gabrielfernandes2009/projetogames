# Projeto Games

Este repositório contém uma atividade de desenvolvimento web com integração de banco de dados PostgreSQL e API em PHP. O objetivo principal é cadastrar e consultar jogos em um catálogo, armazenando os dados em um banco relacional e expondo operações por meio de endpoints HTTP.

A estrutura também inclui um script em Python que consulta informações de endereço por CEP usando a API do ViaCEP, funcionando como atividade complementar de consumo de API externa.

---

## 🧩 Objetivo da atividade

O projeto simula um sistema simples de gerenciamento de jogos, com as seguintes operações:

- Cadastro de jogos
- Consulta de todos os jogos cadastrados
- Persistência dos dados em PostgreSQL
- Comunicação backend em PHP
- Consumo de API externa em Python

---

## 🛠️ Tecnologias utilizadas

- PHP 8+
- PostgreSQL
- Python 3+
- Biblioteca `requests` do Python
- PDO (PHP Data Objects) para conexão com o banco

---

## 📁 Estrutura do repositório

```text
projetogames/
├── README.md                     # Documentação do projeto
├── conexao.php                   # Configuração da conexão com o PostgreSQL
├── games.php                     # API em PHP para cadastro e listagem de jogos
├── projeto.py                    # Script em Python para consulta de endereço por CEP
├── CREATE TABLE produtos(.pgsql  # Script SQL de criação da tabela de jogos
├── .gitignore                    # Arquivos ignorados pelo Git
└── Untitled-2.pgsql              # Arquivo auxiliar/SQL de apoio
```

---

## 🗃️ Estrutura da tabela de jogos

O banco de dados utilizado pelo projeto possui uma tabela chamada `games`, com os campos abaixo:

```sql
CREATE TABLE games (
    id SERIAL PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    plataforma VARCHAR(80) NOT NULL,
    genero VARCHAR(80) NOT NULL,
    desenvolvedora VARCHAR(150) NOT NULL,
    ano_lancamento INTEGER NOT NULL,
    preco NUMERIC(10, 2) NOT NULL,
    estoque INTEGER NOT NULL DEFAULT 0
);
```

> O arquivo `CREATE TABLE produtos(.pgsql` contém a estrutura equivalente, adaptada ao nome do projeto.

---

## ⚙️ Pré-requisitos

Antes de executar o projeto, certifique-se de ter instalado:

- PHP 8.x ou superior
- Python 3.x
- PostgreSQL
- A biblioteca Python `requests`

Para instalar a dependência do Python:

```bash
pip install requests
```

---

## 🧱 Configuração do banco de dados

1. Crie um banco PostgreSQL com o nome desejado.
2. Ajuste as credenciais de acesso no arquivo `conexao.php`:

```php
$host = "192.168.10.92";
$usuario = "postgres";
$banco = "levelup";
$senha = "1234";
```

3. Execute o script SQL para criar a tabela:

```sql
CREATE TABLE games (
    id SERIAL PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    plataforma VARCHAR(80) NOT NULL,
    genero VARCHAR(80) NOT NULL,
    desenvolvedora VARCHAR(150) NOT NULL,
    ano_lancamento INTEGER NOT NULL,
    preco NUMERIC(10, 2) NOT NULL,
    estoque INTEGER NOT NULL DEFAULT 0
);
```

---

## 🚀 Executando a API em PHP

Na raiz do projeto, inicie o servidor embutido do PHP:

```bash
php -S localhost:8000
```

### Listar jogos

Acesse no navegador ou via `curl`:

```bash
curl http://localhost:8000/games.php
```

Esse endpoint retorna todos os jogos em formato JSON.

### Cadastrar jogo

Exemplo de requisição `POST` com JSON:

```bash
curl -X POST http://localhost:8000/games.php \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "The Legend of Zelda",
    "plataforma": "Nintendo Switch",
    "genero": "Aventura",
    "desenvolvedora": "Nintendo",
    "ano_lancamento": 2017,
    "preco": 299.90,
    "estoque": 15
  }'
```

A API salva o registro no banco PostgreSQL e responde com uma mensagem de sucesso.

---

## 🐍 Executando o script em Python

O arquivo `projeto.py` faz uma consulta a uma API pública do ViaCEP, solicitando o CEP informado pelo usuário.

```bash
python projeto.py
```

Exemplo de execução:

```text
Digite o seu CEP: 01001000
```

O script retorna informações como logradouro e bairro com base no CEP informado.

---

## 📌 Observações

- O projeto é uma atividade prática de integração entre banco de dados, backend em PHP e consumo de API externa em Python.
- Para funcionar corretamente em outra máquina, é necessário ajustar as credenciais do banco e verificar se a máquina local ou servidor PostgreSQL está acessível.
- O arquivo `projeto.py` depende da biblioteca `requests`, então ela deve estar instalada antes da execução.

---

## 📄 Licença

Este projeto foi desenvolvido para fins de estudo e aprendizado em integração de sistemas e manipulação de dados.