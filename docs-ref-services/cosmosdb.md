---
title: Bibliotecas do Azure Cosmos DB para Java
description: "Documentação de referência para as bibliotecas de cliente de Java para o Azure Cosmos DB"
keywords: Azure, Java, SDK, API, SQL, banco de dados, MongoDB, Cosmos DB, NoSQL, DocumentDB
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 393f57df0ea2076c6ee7045b56883ee088716fad
ms.sourcegitcommit: 93107ca9ed76a29573a5faf8f39737c85e6bbaff
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2017
---
# <a name="azure-cosmos-db-libraries-for-java"></a>Bibliotecas do Azure Cosmos DB para Java

## <a name="overview"></a>Visão geral

Armazenar e consultar chave-valor, documento JSON, grafo e dados de colunas em um banco de dados globalmente distribuído com [Cosmos DB](/azure/cosmos-db/introduction).

Para começar a usar o Cosmos DB, consulte [Azure Cosmos DB: Criar um aplicativo de API com o Java e o portal do Azure](/azure/cosmos-db/create-documentdb-java).

## <a name="client-library"></a>Biblioteca do cliente

Conectar-se ao Cosmos DB usando a biblioteca de cliente [DocumentDB](/azure/cosmos-db/documentdb-introduction) para trabalhar com dados JSON com [sintaxe de consulta SQL](/azure/cosmos-db/documentdb-sql-query).

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
> [Explorar as APIs de cliente](/java/api/overview/azure/cosmosdb/clientlibrary)


## <a name="samples"></a>Exemplos

[Desenvolver um aplicativo Java usando a API do MongoDB do Azure Cosmos DB][2]   
[Desenvolver um aplicativo Java usando a API do Graph do Azure Cosmos DB][3]   
[Desenvolver um aplicativo Java usando a API do DocumentDB do Azure Cosmos DB][4]        

Explore mais [exemplos de código Java para o Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) que você pode usar em seus aplicativos.

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started