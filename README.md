# Apresentação Cassandra

Este projeto contém um tutorial de instalação simples do Banco de dados Cassandra.

## 🔌 Instalação

Utilizaremos um contêiner docker para a instalação e execução do Cassandra.

A instalação do Docker varia de acordo com o Sistema Operacional utilizado, portanto acesse
a [documentação](https://docs.docker.com/engine/install/ubuntu/) oficial para a instalação correta.

### 🐋 Instalação do Cassandra com Docker

1. Baixe a última versão da imagem do Cassandra:

```shell
$ docker pull cassandra:latest
```

2. Para iniciar uma instância do Cassandra execute:

```shell
$ docker run -d --name cassandra-node -p 9842:9842 cassandra
```

3. Acesse o bash do contêiner:

```shell
$ docker exec -it cassandra-node bash
```

4. Acesse o shell do banco de dados:

```shell
$ cqlsh
```

### :girl: :boy: Responsáveis pelo projeto

- Gabriel Yassunaga
- Victória Lemos
- Lucas Hipólito
- Rodrigo Touriño
- Amanda Elisa
- Millena Moura

## :gear: Operações no DB

### Criação de tabelas

1. Criando um keyspace

Um keyspace funciona como um schema em um DB SQL comum. Porém, por Cassandra ser um banco distribuído, o keyspace
definirá o agrupamento de tabelas que será replicado em outros DBs.

```cassandraql
CREATE KEYSPACE blog WITH replication = {'class': 'SimpleStrategy', 'replication_factor' : 3};
```

Acesse o KEYSPACE usando:

```cassandraql
USE blog
```

O nome 'blog' pode ser substituído pelo nome do keyspace que desejar.

2. Criando uma tabela

```cassandraql
CREATE TABLE post
(
    id_post       int,
    nome_usuario  text,
    corpo         text,
    PRIMARY KEY (id_post)
);
```

```cassandraql
CREATE TABLE usuario
(
    id_usuario   int,
    nome_usuario text,
    senha        text,
    PRIMARY KEY (nome_usuario)
);
```

Para remover uma tabela utilize:
```cassandraql
DROP TABLE usuario;
```

Para visualizar seu keyspace após a criação, utilize:

```cassandraql
SELECT *
FROM system_schema.tables
WHERE keyspace_name = 'blog';
```

### Inserindo Registros

A inserção se assemelha bastante com a inserção SQL.

Para inserir um registro de usuário utilize:

```cassandraql
INSERT INTO usuario (id_usuario, nome_usuario, senha)
VALUES (1, 'Rose', 'xpto');
```

```cassandraql
INSERT INTO usuario (id_usuario, nome_usuario, senha)
VALUES (2, 'Jose', 'xpto');
```

```cassandraql
INSERT INTO usuario (id_usuario, nome_usuario, senha)
VALUES (3, 'Davi', 'xptt');
```

```cassandraql
INSERT INTO usuario (id_usuario, nome_usuario, senha)
VALUES (4, 'Ana', 'xptt');
```

Inserindo posts:
```cassandraql
INSERT INTO post (id_post, nome_usuario, corpo)
VALUES (1, 'Ana', 'Cassandra é muito bom!');
```

```cassandraql
INSERT INTO post (id_post, nome_usuario, corpo)
VALUES (2, 'Davi', 'Vontade de capinar um lote');
```

```cassandraql
INSERT INTO post (id_post, nome_usuario, corpo)
VALUES (3, 'Davi', 'Passou');
```

### Recuperando registros
Para buscar os usuários:

```cassandraql
SELECT * FROM usuario;
```

Para buscar os posts:
```cassandraql
SELECT * FROM post;
```

Para buscar usando filtros:
```cassandraql
SELECT * FROM post WHERE nome_usuario = 'Davi' ALLOW FILTERING ;
```

Buscando em um escopo específico de IDs:
```cassandraql
SELECT * FROM post WHERE id_post IN (1, 3);
```

### Atualizando registros

```cassandraql
UPDATE post
   SET corpo   = 'Não passou'
 WHERE id_post = 3;
```

### Removendo registros
```cassandraql
DELETE FROM post where id_post = 3;
```

# Para saber mais

Para mais informações sobre a linguagem CQL, acesse a [documentação oficial](https://cassandra.apache.org/doc/latest/cql/index.html)