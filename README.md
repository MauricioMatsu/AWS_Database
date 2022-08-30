# AWS_Database

Lista de Bancos que vamos aprender

- Relacional
-- RDS
-- Aurora
-- Redshift

- Key - Value
-- DynamoDB
--- DAX

- Document
-- DocumentDB

- In Memory
-- Elasticache
--- Redis
--- Memcached

- Graph
-- Neptune

- Search
-- Elasticsearch Service

- Time-series
-- Timestream

- Ledger (Banco de dados de logs)
-- QLDB

Migração de banco de dados com DMS

## Base

### DATA

Dados é uma coleção de valores ou informações
Database é um forma organizada de salvar os dados
existem 3 tipos de dados:
- Estruturados
- Semi-estruturados
- "Sem Estrutura"/ Desistruturado

existe um banco de dados para cada tipo de dado

#### Estruturado

Tipico dado em tabelas com estrutura bem definida (Shema)
Adequada para OLTP (Transacional) e OLAP (analytical)
Tipico em banco de dados relacionais, aonde possui tabelas com index com relacionalmento entre elas ligada por chaves
Adequado para queries complexas e analisticica

#### Semi-structured Data
Organizado , porém não existe uma estrutura
Semelhante a uma variavel programatica
Tipo nosql (banco não relacional)
bem adquado a big data e aplicações de baixa latencia
tipicamente XML ou JSON

#### Unstructured Data
Document, fotos, videos, musicas
Tipico storage ou banco de dados não relacional

### Tipo de banco de dados

#### Relacional
Tem um esquema bem definido (schema)
possui uma estrutura ACID (Atomicity, Consistency, Isolation, and Durability)
suporta joins
Tipico para OLTP e OLAP
Exemplos: MySQL, PostgreSQL, MariaDB, Oracle, Microsoft SQL Server
Serviços da AWS :
- OLTP -> Amazon RDS e Aurora
- OLAP -> Redshift

Caracterizado por multiplas tabelas e ligados por foreign key 

!Indexes para melhor a performace

##### ACID
Atomicity -> All or nothing. a transação é executada por completa ou não
Consistency -> 


