# Apresentação Cassandra

Este projeto contém os arquivos e um tutorial de instalação e casos de uso simples do Banco de dados Cassandra.

## 🔌 Instalação

Utilizaremos um contêiner docker para a instalação e execução do Cassandra.

A instalação do Docker varia de acordo com o Sistema Operacional utilizado, portanto acesse a [documentação](https://docs.docker.com/engine/install/ubuntu/) oficial para a instalação correta.

### 🐋 Instalação do Cassandra com Docker

1. Baixe a última versão da imagem do Cassandra:
```shell
$ docker pull cassandra:latest
```
2. Para iniciar uma instância do Cassandra execute:
```shell
$ docker run -d --name cassandra-node -p 9842:9842 cassandra
```
3. Acesse o bash do container:
```shell
$ docker exec -it cassandra-node bash
```

4. Execute acesse o shell do banco de dados:
```shell
$ cqlsh
```
