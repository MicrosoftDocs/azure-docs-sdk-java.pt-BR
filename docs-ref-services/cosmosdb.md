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
ms.openlocfilehash: 6fc9f90cb3c8130aa82b20554a94a8b5ab78c083
ms.sourcegitcommit: 33c70f921f1524c8bdb69ad5a1a3c1b4b1de97ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37026788"
---
# <a name="azure-cosmos-db-libraries-for-java"></a>Bibliotecas do Azure Cosmos DB para Java

## <a name="overview"></a>Visão geral

Armazenar e consultar o valor-chave, documento JSON, gráfico e dados de colunas em um banco de dados globalmente distribuído com o [Azure Cosmos DB](/azure/cosmos-db/introduction).

Para começar a usar o Azure Cosmos DB, consulte [Azure Cosmos DB: Criar um aplicativo de API com o Java e o Portal do Azure](/azure/cosmos-db/create-sql-api-java).

## <a name="client-library"></a>Biblioteca do cliente

Conecte o Azure Cosmos DB usando a biblioteca de clientes [API do SQL](/azure/cosmos-db/sql-api-introduction) para trabalhar com os dados JSON e a [sintaxe de consulta do SQL](/azure/cosmos-db/sql-api-sql-query).

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente de Cosmos DB em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a>Exemplo

Selecionar documentos JSON correspondentes no Cosmos DB usando a sintaxe de consulta SQL.

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
> [Explorar as APIs de cliente](/java/api/overview/azure/cosmosdb/client)


## <a name="samples"></a>Exemplos

[Desenvolver um aplicativo Java usando a API do MongoDB do Azure Cosmos DB][2]   
[Desenvolver um aplicativo Java usando a API do Graph do Azure Cosmos DB][3]   
[Desenvolver um aplicativo Java usando a API SQL do Azure Cosmos DB][4]        

Explore mais [exemplos de código Java para o Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) que você pode usar em seus aplicativos.

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
