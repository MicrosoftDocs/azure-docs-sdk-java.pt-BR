---
title: Bibliotecas do Banco de Dados do Azure para PostgreSQL para Java
description: Documentação de referência para as bibliotecas de cliente de Java para o Banco de Dados do Azure para PostgreSQL
keywords: Azure, Java, SDK, API, SQL, banco de dados, PostGres, PostgreSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: postgresql
ms.openlocfilehash: d6fa2acb9a2f44b157ae52ba6e41f6777a43b574
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930972"
---
# <a name="azure-database-for-postgresql-libraries-for-java"></a><span data-ttu-id="1090a-104">Bibliotecas do Banco de Dados do Azure para PostgreSQL para Java</span><span class="sxs-lookup"><span data-stu-id="1090a-104">Azure Database for PostgreSQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="1090a-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1090a-105">Overview</span></span>

<span data-ttu-id="1090a-106">O [Banco de Dados do Azure para PostgreSQL](/azure/sql-database/sql-database-technical-overview) é um serviço de banco de dados relacional no Azure, projetado para desenvolvedores com base na versão de comunidade do mecanismo de banco de dados [PostgreSQL](https://www.postgresql.org/) de software livre.</span><span class="sxs-lookup"><span data-stu-id="1090a-106">[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview) is a relational database service in Azure built for developers based on the community version of open source [PostgreSQL](https://www.postgresql.org/) database engine.</span></span>

<span data-ttu-id="1090a-107">Para começar a usar o Banco de dados do Azure para PostgreSQL, consulte [Usar Java para se conectar e consultar dados](/azure/postgresql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="1090a-107">To get started with Azure Database for PostgreSQL, see [Use Java to connect and query data](/azure/postgresql/connect-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="1090a-108">Driver JDBC do cliente</span><span class="sxs-lookup"><span data-stu-id="1090a-108">Client JDBC driver</span></span>

<span data-ttu-id="1090a-109">Conectar-se ao Banco de Dados do Azure para PostgreSQL a partir dos seus aplicativos usando o [driver JDBC do PostgreSQL](https://jdbc.postgresql.org/) de software livre.</span><span class="sxs-lookup"><span data-stu-id="1090a-109">Connect to Azure Database for PostgreSQL from your applications using the open-source [PostgreSQL JDBC driver](https://jdbc.postgresql.org/).</span></span> <span data-ttu-id="1090a-110">Você pode usar o [API do JDBC de Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para se conectar ao banco de dados ou usar as estruturas de acesso a dados que interagem com o banco de dados por meio do JDBC, como [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="1090a-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="1090a-111">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar o driver JDBC do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="1090a-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="1090a-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="1090a-112">Example</span></span>

<span data-ttu-id="1090a-113">Conectar-se ao Banco de Dados do Azure para PostgreSQL usando o JDBC e selecionar todos os registros na tabela de vendas.</span><span class="sxs-lookup"><span data-stu-id="1090a-113">Connect to Azure Database for PostgreSQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="1090a-114">Você pode obter a cadeia de conexão para o seu banco de dados no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1090a-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:postgresql://mypostgresdb.postgres.database.azure.com:5432/mydb?user=frank@mypostgresdb&password=AbCdEfGhIjK&ssl=true");
Connection connection = null;
try {
    connection = DriverManager.getConnection(url);
    String selectSql = "SELECT * FROM SALES";
    Statement statement = connection.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="1090a-115">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1090a-115">Samples</span></span>

[<span data-ttu-id="1090a-116">Criar um banco de dados PostgreSQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1090a-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

<span data-ttu-id="1090a-117">Explore mais [exemplos de código Java para o Banco de Dados do Azure para PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1090a-117">Explore more [sample Java code for Azure Database for PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) you can use in your apps.</span></span>
