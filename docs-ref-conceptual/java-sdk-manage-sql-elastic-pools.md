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
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931112"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a><span data-ttu-id="fb223-103">Gerenciar bancos de dados SQL do Azure em pools elásticos a partir dos seus aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="fb223-103">Manage Azure SQL databases in elastic pools from your Java applications</span></span>

<span data-ttu-id="fb223-104">[Este exemplo](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) cria um servidor de banco de dados SQL com um [pool elástico](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para gerenciar e dimensionar os recursos para vários bancos de dados em um único plano.</span><span class="sxs-lookup"><span data-stu-id="fb223-104">[This sample](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) creates a SQL database server with an [elastic pool](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to manage and scale resources for mulitple databases in a single plan.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="fb223-105">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="fb223-105">Run the sample</span></span>

<span data-ttu-id="fb223-106">Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="fb223-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="fb223-107">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="fb223-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

[<span data-ttu-id="fb223-108">Exibição de exemplo de código completo no GitHub</span><span class="sxs-lookup"><span data-stu-id="fb223-108">View the complete code sample on GitHub</span></span>](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)

## <a name="authenticate-with-azure"></a><span data-ttu-id="fb223-109">Autenticar com o Azure</span><span class="sxs-lookup"><span data-stu-id="fb223-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a><span data-ttu-id="fb223-110">Criar um servidor de banco de dados SQL com o pool elástico</span><span class="sxs-lookup"><span data-stu-id="fb223-110">Create a SQL database server with an elastic pool</span></span>

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

<span data-ttu-id="fb223-111">Consulte a [referência da classe ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) para os valores da edição atual.</span><span class="sxs-lookup"><span data-stu-id="fb223-111">See the [ElasticPoolEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) for current edition values.</span></span> <span data-ttu-id="fb223-112">Leia a [documentação de pool elástico de banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para comparar as características de recursos de cada edição.</span><span class="sxs-lookup"><span data-stu-id="fb223-112">Review the [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to compare edition resource characteristics.</span></span> 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a><span data-ttu-id="fb223-113">Alterar as configurações de Unidade de Transação de Banco de Dados (DTU) em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="fb223-113">Change Database Transaction Unit (DTU) settings in an elastic pool</span></span>

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

<span data-ttu-id="fb223-114">Leia a [documentação de DTUs e eDTUs](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) para saber mais sobre a alocação de recursos para bancos de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="fb223-114">Review the [DTUs and eDTUs documentation](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) to learn more about allocating resources to SQL databases.</span></span>

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a><span data-ttu-id="fb223-115">Criar um novo banco de dados e adicioná-lo a um pool elástico</span><span class="sxs-lookup"><span data-stu-id="fb223-115">Create a new database and add it to an elastic pool</span></span>

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

<span data-ttu-id="fb223-116">A API cria `anotherDatabase` na [camada S0](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) na primeira instrução.</span><span class="sxs-lookup"><span data-stu-id="fb223-116">The API creates `anotherDatabase` at [S0 tier](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) in the first statement.</span></span> <span data-ttu-id="fb223-117">Mover `anotherDatabase` para o pool elástico atribui os recursos de banco de dados com base nas configurações do pool.</span><span class="sxs-lookup"><span data-stu-id="fb223-117">Moving `anotherDatabase` to the elastic pool assigns the database resources based on the pool settings.</span></span>

## <a name="remove-a-database-from-an-elastic-pool"></a><span data-ttu-id="fb223-118">Remover um banco de dados de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="fb223-118">Remove a database from an elastic pool</span></span>
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

<span data-ttu-id="fb223-119">Consulte a [referência da classe DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) para valores a serem passados para `withEdition()`.</span><span class="sxs-lookup"><span data-stu-id="fb223-119">See the [DatabaseEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) for values to pass to `withEdition()`.</span></span>

## <a name="list-current-database-activities-in-an-elastic-pool"></a><span data-ttu-id="fb223-120">Listar as atividades atuais do banco de dados em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="fb223-120">List current database activities in an elastic pool</span></span>
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

<span data-ttu-id="fb223-121">As atividades de banco de dados incluem mover um banco de dados ou para dentro ou para fora de um pool elástico e atualizar bancos de dados em um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="fb223-121">Database activities include moving a database in or out of an elastic pool and updating databases in an elastic pool.</span></span>


## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="fb223-122">Listar bancos de dados em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="fb223-122">List databases in an elastic pool</span></span>
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

<span data-ttu-id="fb223-123">Analise os métodos em [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) para consultar os bancos de dados em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="fb223-123">Review the methods in [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) to query the databases in more detail.</span></span>

## <a name="delete-an-elastic-pool"></a><span data-ttu-id="fb223-124">Excluir um pool elástico</span><span class="sxs-lookup"><span data-stu-id="fb223-124">Delete an elastic pool</span></span>
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

<span data-ttu-id="fb223-125">O pool elástico deve estar vazio antes de ser excluído.</span><span class="sxs-lookup"><span data-stu-id="fb223-125">The elastic pool must be empty before deleting it.</span></span>

## <a name="sample-code-summary"></a><span data-ttu-id="fb223-126">Resumo do exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="fb223-126">Sample code summary.</span></span>

<span data-ttu-id="fb223-127">O exemplo cria um SQL server com dois bancos de dados gerenciados em um único pool elástico.</span><span class="sxs-lookup"><span data-stu-id="fb223-127">The sample creates a SQL server with two databases managed in a single elasic pool.</span></span> <span data-ttu-id="fb223-128">Os limites de recursos do pool elástico foram atualizados, em seguida os bancos de dados adicionais são adicionados ao pool.</span><span class="sxs-lookup"><span data-stu-id="fb223-128">The elastic pool resource limits are updated, then additional databases are added to the pool.</span></span> <span data-ttu-id="fb223-129">O código, em seguida, lê a configuração e o estado do pool elástico.</span><span class="sxs-lookup"><span data-stu-id="fb223-129">The code then reads the elastic pool's configuration and state.</span></span> 

<span data-ttu-id="fb223-130">O exemplo exclui todos os recursos criados antes de sair.</span><span class="sxs-lookup"><span data-stu-id="fb223-130">The sample deletes all resources it created before exiting.</span></span>

| <span data-ttu-id="fb223-131">Classe usada no exemplo</span><span class="sxs-lookup"><span data-stu-id="fb223-131">Class used in sample</span></span> | <span data-ttu-id="fb223-132">Observações</span><span class="sxs-lookup"><span data-stu-id="fb223-132">Notes</span></span> |
|-------|-------|
| [<span data-ttu-id="fb223-133">SqlServer</span><span class="sxs-lookup"><span data-stu-id="fb223-133">SqlServer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | <span data-ttu-id="fb223-134">Banco de Dados do SQL server no Azure criados pela cadeia fluente `azure.sqlServers().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="fb223-134">SQL DB server in Azure created by `azure.sqlServers().define()...create()` fluent chain.</span></span> <span data-ttu-id="fb223-135">Fornece métodos para criar e trabalhar com bancos de dados e pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="fb223-135">Provides methods to create and work with elastic pools and databases.</span></span> 
| [<span data-ttu-id="fb223-136">SqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fb223-136">SqlDatabase</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | <span data-ttu-id="fb223-137">Objeto do lado do cliente que representa um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="fb223-137">Client side object representing a SQL database.</span></span> <span data-ttu-id="fb223-138">Criado por meio de `sqlServer().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="fb223-138">Created through `sqlServer().define()...create()`.</span></span> 
| [<span data-ttu-id="fb223-139">DatabaseEditions</span><span class="sxs-lookup"><span data-stu-id="fb223-139">DatabaseEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | <span data-ttu-id="fb223-140">Campos estáticos constantes usados para configurar recursos de banco de dados durante a criação de um banco de dados fora de um pool elástico ou ao mover um banco de dados para fora de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="fb223-140">Constant static fields used to set database resources when creating a database outside of an elastic pool or when moving a database out of an elastic pool</span></span>  
| [<span data-ttu-id="fb223-141">SqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="fb223-141">SqlElasticPool</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | <span data-ttu-id="fb223-142">Criada a partir da seção `withNewElasticPool()` da cadeia fluente que criou o SqlServer no Azure.</span><span class="sxs-lookup"><span data-stu-id="fb223-142">Created from the `withNewElasticPool()` section of the fluent chain that created the SqlServer in Azure.</span></span> <span data-ttu-id="fb223-143">Fornece métodos para definir os limites de recurso para bancos de dados em execução no pool elástico e para o pool elástico em si.</span><span class="sxs-lookup"><span data-stu-id="fb223-143">Provides methods to set resource limits for databases running in the elastic pool and for the elastic pool itself.</span></span> 
| [<span data-ttu-id="fb223-144">ElasticPoolEditions</span><span class="sxs-lookup"><span data-stu-id="fb223-144">ElasticPoolEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | <span data-ttu-id="fb223-145">Classe de campos constantes que define os recursos disponíveis para um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="fb223-145">Class of constant fields defining the resources available to an elastic pool.</span></span> <span data-ttu-id="fb223-146">Consulte [documentação de pool elástico de banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) para obter detalhes sobre a camada.</span><span class="sxs-lookup"><span data-stu-id="fb223-146">See [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) for tier details.</span></span> 
| [<span data-ttu-id="fb223-147">ElasticPoolDatabaseActivity</span><span class="sxs-lookup"><span data-stu-id="fb223-147">ElasticPoolDatabaseActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | <span data-ttu-id="fb223-148">Recuperados do `SqlElasticPool.listDatabaseActivities()`.</span><span class="sxs-lookup"><span data-stu-id="fb223-148">Retreived from `SqlElasticPool.listDatabaseActivities()`.</span></span> <span data-ttu-id="fb223-149">Cada objeto desse tipo representa uma atividade executada em um banco de dados no pool elástico.</span><span class="sxs-lookup"><span data-stu-id="fb223-149">Each object of this type represents an activity performed on a database in the elastic pool.</span></span>
| [<span data-ttu-id="fb223-150">ElasticPoolActivity</span><span class="sxs-lookup"><span data-stu-id="fb223-150">ElasticPoolActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | <span data-ttu-id="fb223-151">Recuperado em uma Lista de `SqlElasticPool.listActivities()`.</span><span class="sxs-lookup"><span data-stu-id="fb223-151">Retrieved in a List from `SqlElasticPool.listActivities()`.</span></span> <span data-ttu-id="fb223-152">Cada objeto na lista representa uma atividade executada no pool elástico (não os bancos de dados no pool elástico).</span><span class="sxs-lookup"><span data-stu-id="fb223-152">Each of object in the list represents an activity performed on the elastic pool (not the databases in the elastic pool).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb223-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb223-153">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]