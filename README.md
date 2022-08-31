# AWS_Database

Lista de Bancos que vamos aprender

- Relacional
    - RDS
    - Aurora
    - Redshift
- Key - Value
    - DynamoDB
        - DAX
- Document
    - DocumentDB
- In Memory
    - Elasticache
        - Redis
        - Memcached
- Graph
    - Neptune
- Search
    - Elasticsearch Service
- Time-series
    - Timestream
- Ledger (Banco de dados de logs)
    - QLDB

Migração de banco de dados com DMS

## Basico

### Tipos de Dados

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

#### Non Relacional Database

Chamado de NoSql
Adequado para dados semi estruturado ou não estruturado
Single table contendo todos os dados, as vezes duplicando o dado
Adequado para Big Data -> High Volume, High Velocity, High Varety
Adequado para baixa latencia.
Modele de dados flexivel (i.e. trades some ACID properties)

nao indicado para OLAP applications
Exemplos:
- Key-Value
    - DynamoDB
-Document
    - DocumentDB
- In-Memory
    - ElastiCache
- Graph
    - Neptune

##### BASE compliance

**B**asically **A**vailable
**S**oft state
**E**ventual consistency

**Basically Available**

O conceito de “Basicamente Disponível” tem a ver com a durabilidade e disponibilidade de uma alteração.

Em um banco de dados com dados distribuídos, todos os nós são considerados disponíveis e é possível que duas aplicações alterem uma determinada informação, simultaneamente, cada uma em um nó diferente.

Ao executar a replicação, o banco percebe uma inconsistência e precisa resolver o problema.

Imaginemos uma informação com conteúdo ‘A’, sendo alterada de ‘A’ para ‘B’, no nó 1, pela aplicação 1 e, simultaneamente, sendo alterada de ‘A’ para ‘C’, no nó 2, pela aplicação 2.

Qual deveria ser o resultado final, após a “convergência” dos dados? ‘B’ ou ‘C’?

Uma das informações deverá ser descartada, fazendo com que o dado não permaneça disponível.

Além disso, um dado recém inserido em um dos nós e ainda não replicado, também não pode ser lido através do outro nó, tornando-o temporariamente indisponível.

**Soft state**

O segundo conceito envolvido no modelo BASE é o conceito de “Soft State”.

Se imaginarmos os estados pelos quais uma transação passa, podemos ter períodos em que está ativa, em processo de finalização, sendo abortada ou concluída.

Seguindo o mesmo princípio, uma transação distribuída só pode ser considerada “concluída” quando de fato a alteração foi replicada para todos os nós.

Antes que isso ocorra, a leitura da informação a partir de todos os nós pode retornar dados inconsistentes e não temos como saber se: 1 – a alteração falhou no segundo nó ou 2 – devido à alta latência, o dado ainda não tenha sido replicado.

Ao não podermos afirmar em que estado a transação se encontra, temos o “Soft State”

**Eventual consistency**

O primeiro conceito que precisa ser entendido no modelo BASE é o conceito de “Consistência Eventual”. Para entender como isso funciona, vamos imaginar que um database possui 2 nós e que todo dado gravado em um dos nós é replicado para o outro.

Com esta configuração, passamos a ter duas opções de leitura da informação, dobrando o desempenho da leitura.

Porém, para não prejudicar o desempenho da escrita, a aplicação faz alterações em apenas um dos nós e, através de um processo independente, estas alterações são replicadas para o outro nó.

Como esta replicação não ocorre instantaneamente (não atômica), existe a possibilidade de que uma aplicação lendo a mesma informação a partir dos dois nós obtenha valores distintos, sendo considerados inconsistentes.

Entretanto, se uma informação não sofre alterações por algum tempo, podemos esperar que ao termino da replicação, os dados fiquem iguais, voltando a ser consistentes.

| Banco relacional | No SQL|
|---|---|
| Armazenamentos por varias tabelas ligadas por chaves | Armazenamento de coleções ou chave valor |
| Fundamento ACID | Fundamento BASE |
| Esquema fixo (schema) | Semi estruturado ou desestruturado |
| Escalonamento Vertical | Escalonamento Horizontal |
| Uses SQL | Uses Object based APIs|
| OLTP e OLAP | OLTP |

## RDS
RDS é Relational Database Service, um serviço da AWS que diponibiliza banco de dados relacionais como serviço, suportanto atualmente 6 engines:
- PostgreSQL
- MySQL
- MariaDB
- Oracle
- SQL Server
- Aurora

O Ultimo é um banco de dados da propria AWS

é um serviço que normalmente roda em uma VPC em uma subnet privada e somente é dada o acesso usando security group . Isso é importante principalmente com lambda.

O sistema de armazenamento é um EBS (gp2 ou io1)
possui backups automaticos com pontos de recuperação, esses backups podem ser configurados para expirar

Você pode fazer snapshots manual, e esses snapshots podem ser copiados entre regioes da AWS

o monitoramento é feito pelo cloudwatch

RDS Events get notified via SNS for events (<n style="color:red"> estudar! </n>)

Escrever: Diferença entre utilizar BD no onpremisse, na AWS, mas gerenciado em um EC2 por exemplo, ou RDS)


### Precificação

Quando vc cria um banco de dados vc escolhe pela tipo de instancia (on-demand ou reservada)
pelo tipo de engine ( Postgre, mysql, mariadb, ...)
e pela classe da instancia ( baseado em memoria, cpu, I/O capacity)

forma de pagamento
------
on demand paga por hora
reservada pode escolher o 1 ou 3 anos 

Além disso vc paga armazenamento (GB/month)

Backups

Snapshot export to S3

I/O per million requests

Data transfer


