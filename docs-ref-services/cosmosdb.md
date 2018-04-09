---
title: Bibliotecas do Azure Cosmos DB para Java
description: Documentação de referência para as bibliotecas de cliente de Java para o Azure Cosmos DB
keywords: Azure, Java, SDK, API, SQL, banco de dados, MongoDB, Cosmos DB, NoSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 845106b773de03aba8dd5edb9a18c6b036cf3215
ms.sourcegitcommit: 61030d025614b084e897809e603b2ec79900ec8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="azure-cosmos-db-libraries-for-java"></a><span data-ttu-id="fa6c3-104">Bibliotecas do Azure Cosmos DB para Java</span><span class="sxs-lookup"><span data-stu-id="fa6c3-104">Azure Cosmos DB libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="fa6c3-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fa6c3-105">Overview</span></span>

<span data-ttu-id="fa6c3-106">Armazenar e consultar o valor-chave, documento JSON, gráfico e dados de colunas em um banco de dados globalmente distribuído com o [Azure Cosmos DB](/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="fa6c3-106">Store and query key-value, JSON document, graph, and columnar data in a globally distributed database with [Azure Cosmos DB](/azure/cosmos-db/introduction).</span></span>

<span data-ttu-id="fa6c3-107">Para começar a usar o Azure Cosmos DB, consulte [Azure Cosmos DB: Criar um aplicativo de API com o Java e o Portal do Azure](/azure/cosmos-db/create-sql-api-java).</span><span class="sxs-lookup"><span data-stu-id="fa6c3-107">To get started with Azure Cosmos DB, see [Azure Cosmos DB: Build an API app with Java and the Azure portal](/azure/cosmos-db/create-sql-api-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="fa6c3-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="fa6c3-108">Client library</span></span>

<span data-ttu-id="fa6c3-109">Conecte o Azure Cosmos DB usando a biblioteca de clientes [API do SQL](/azure/cosmos-db/sql-api-introduction) para trabalhar com os dados JSON e a [sintaxe de consulta do SQL](/azure/cosmos-db/sql-api-sql-query).</span><span class="sxs-lookup"><span data-stu-id="fa6c3-109">Connect to Azure Cosmos DB using the [SQL API](/azure/cosmos-db/sql-api-introduction) client library to work with JSON data with [SQL query syntax](/azure/cosmos-db/sql-api-sql-query).</span></span>

<span data-ttu-id="fa6c3-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente de Cosmos DB em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="fa6c3-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the Cosmos DB client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="fa6c3-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fa6c3-111">Example</span></span>

<span data-ttu-id="fa6c3-112">Selecionar documentos JSON correspondentes no Cosmos DB usando a sintaxe de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="fa6c3-112">Select matching JSON documents in Cosmos DB using SQL query syntax.</span></span>

```java
DocumentClient client = new DocumentClient("https://contoso.documents.azure.com:443",
                "contosoCosmosDBKey", 
                new ConnectionPolicy(),
                ConsistencyLevel.Session);

List<Document> results = client.queryDocuments("dbs/" + DATABASE_ID + "/colls/" + COLLECTION_ID,
        "SELECT * FROM myCollection WHERE myCollection.email = 'allen [at] contoso.com'",
        null)
    .getQueryIterable()
    .toList();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fa6c3-113">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="fa6c3-113">Explore the Client APIs</span></span>](/java/api/overview/azure/cosmosdb/clientlibrary)


## <a name="samples"></a><span data-ttu-id="fa6c3-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="fa6c3-114">Samples</span></span>

<span data-ttu-id="fa6c3-115">[Desenvolver um aplicativo Java usando a API do MongoDB do Azure Cosmos DB][2] </span><span class="sxs-lookup"><span data-stu-id="fa6c3-115">[Develop a Java app using Azure Cosmos DB MongoDB API][2] </span></span>  
<span data-ttu-id="fa6c3-116">[Desenvolver um aplicativo Java usando a API do Graph do Azure Cosmos DB][3] </span><span class="sxs-lookup"><span data-stu-id="fa6c3-116">[Develop a Java app using Azure Cosmos DB Graph API][3] </span></span>  
<span data-ttu-id="fa6c3-117">[Desenvolver um aplicativo Java usando a API SQL do Azure Cosmos DB][4]</span><span class="sxs-lookup"><span data-stu-id="fa6c3-117">[Develop a Java app using Azure Cosmos DB SQL API][4]</span></span>        

<span data-ttu-id="fa6c3-118">Explore mais [exemplos de código Java para o Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fa6c3-118">Explore more [sample Java code for Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) you can use in your apps.</span></span>

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
