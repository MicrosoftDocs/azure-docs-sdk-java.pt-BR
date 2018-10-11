---
title: Gerenciar pools elásticos do banco de dados SQL com Java | Microsoft Docs
description: Exemplo de código para criar e configurar bancos de dados SQL do Azure usando o SDK do Azure para Java
author: rloutlaw
manager: douge
ms.assetid: 9b461de8-46bc-4650-8e9e-59531f4e2a53
ms.topic: article
ms.service: Azure
ms.devlang: java
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 9ec0cf3083b8659fa850b798ca0ecf18b2757234
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893567"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a>Gerenciar bancos de dados SQL do Azure em pools elásticos a partir dos seus aplicativos Java

[Este exemplo](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) cria um servidor de banco de dados SQL com um [pool elástico](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para gerenciar e dimensionar os recursos para vários bancos de dados em um único plano.

## <a name="run-the-sample"></a>Execute o exemplo

Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador. Em seguida, execute:

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

[Exibição de exemplo de código completo no GitHub](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)

## <a name="authenticate-with-azure"></a>Autenticar com o Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a>Criar um servidor de banco de dados SQL com o pool elástico

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    // Use ElasticPoolEditions.STANDARD as the edition
                    // and create two databases
                    .withNewElasticPool(elasticPoolName, ElasticPoolEditions.STANDARD, 
                        database1Name, database2Name)
                    .create();
```

Consulte a [referência da classe ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) para os valores da edição atual. Leia a [documentação de pool elástico de banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para comparar as características de recursos de cada edição. 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a>Alterar as configurações de Unidade de Transação de Banco de Dados (DTU) em um pool elástico

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

Leia a [documentação de DTUs e eDTUs](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) para saber mais sobre a alocação de recursos para bancos de dados SQL.

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a>Criar um novo banco de dados e adicioná-lo a um pool elástico

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

A API cria `anotherDatabase` na [camada S0](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) na primeira instrução. Mover `anotherDatabase` para o pool elástico atribui os recursos de banco de dados com base nas configurações do pool.

## <a name="remove-a-database-from-an-elastic-pool"></a>Remover um banco de dados de um pool elástico
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

Consulte a [referência da classe DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) para valores a serem passados para `withEdition()`.

## <a name="list-current-database-activities-in-an-elastic-pool"></a>Listar as atividades atuais do banco de dados em um pool elástico
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

As atividades de banco de dados incluem mover um banco de dados ou para dentro ou para fora de um pool elástico e atualizar bancos de dados em um pool elástico.


## <a name="list-databases-in-an-elastic-pool"></a>Listar bancos de dados em um pool elástico
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

Analise os métodos em [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) para consultar os bancos de dados em mais detalhes.

## <a name="delete-an-elastic-pool"></a>Excluir um pool elástico
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

O pool elástico deve estar vazio antes de ser excluído.

## <a name="sample-code-summary"></a>Resumo do exemplo de código.

O exemplo cria um SQL server com dois bancos de dados gerenciados em um único pool elástico. Os limites de recursos do pool elástico foram atualizados, em seguida os bancos de dados adicionais são adicionados ao pool. O código, em seguida, lê a configuração e o estado do pool elástico. 

O exemplo exclui todos os recursos criados antes de sair.

| Classe usada no exemplo | Observações |
|-------|-------|
| [SqlServer](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | Banco de Dados do SQL server no Azure criados pela cadeia fluente `azure.sqlServers().define()...create()`. Fornece métodos para criar e trabalhar com bancos de dados e pools elásticos. 
| [SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | Objeto do lado do cliente que representa um banco de dados SQL. Criado por meio de `sqlServer().define()...create()`. 
| [DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | Campos estáticos constantes usados para configurar recursos de banco de dados durante a criação de um banco de dados fora de um pool elástico ou ao mover um banco de dados para fora de um pool elástico  
| [SqlElasticPool](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | Criada a partir da seção `withNewElasticPool()` da cadeia fluente que criou o SqlServer no Azure. Fornece métodos para definir os limites de recurso para bancos de dados em execução no pool elástico e para o pool elástico em si. 
| [ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | Classe de campos constantes que define os recursos disponíveis para um pool elástico. Consulte [documentação de pool elástico de banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para obter detalhes sobre a camada. 
| [ElasticPoolDatabaseActivity](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | Recuperados do `SqlElasticPool.listDatabaseActivities()`. Cada objeto desse tipo representa uma atividade executada em um banco de dados no pool elástico.
| [ElasticPoolActivity](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | Recuperado em uma Lista de `SqlElasticPool.listActivities()`. Cada objeto na lista representa uma atividade executada no pool elástico (não os bancos de dados no pool elástico).

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [next-steps](includes/java-next-steps.md)]