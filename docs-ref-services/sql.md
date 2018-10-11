---
title: Bibliotecas de Banco de Dados SQL do Azure para Java
description: Conecte-se ao banco de dados do SQL Azure usando o driver JDBC ou as instâncias de banco de dados do SQL do Azure com a API de gerenciamento.
keywords: Azure, Java, SDK, API, SQL, banco de dados, JDBC
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/05/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: sql-database
ms.openlocfilehash: 37f7d3caf10e6b709cee2452c63a543d49e0ead8
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893307"
---
# <a name="azure-sql-database-libraries-for-java"></a><span data-ttu-id="2a464-104">Bibliotecas de Banco de Dados SQL do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="2a464-104">Azure SQL Database libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="2a464-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2a464-105">Overview</span></span>

<span data-ttu-id="2a464-106">O [Banco de Dados SQL do Azure](/azure/sql-database/sql-database-technical-overview) é um serviço de banco de dados relacional que usa o mecanismo do Microsoft SQL Server com suporte para dados de tabela, JSON, espaciais e XML.</span><span class="sxs-lookup"><span data-stu-id="2a464-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) is a relational database service using the Microsoft SQL Server engine that supports table, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="2a464-107">Para começar a usar o Banco de Dados SQL do Azure, consulte [Banco de Dados SQL do Azure: Usar Java para se conectar e consultar dados](/azure/sql-database/sql-database-connect-query-java).</span><span class="sxs-lookup"><span data-stu-id="2a464-107">To get started with Azure SQL Database, see [Azure SQL Database: Use Java to connect and query data](/azure/sql-database/sql-database-connect-query-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="2a464-108">Driver JDBC do cliente</span><span class="sxs-lookup"><span data-stu-id="2a464-108">Client JDBC driver</span></span>

<span data-ttu-id="2a464-109">Conecte-se ao banco de dados do SQL Azure a partir de seus aplicativos usando o [driver JDBC do Banco de Dados SQL](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span><span class="sxs-lookup"><span data-stu-id="2a464-109">Connect to Azure SQL Database from your applications using the [SQL Database JDBC driver](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span></span> <span data-ttu-id="2a464-110">Você pode usar a [API do JDBC de Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para se conectar diretamente ao banco de dados ou usar as estruturas de acesso a dados que interagem com o banco de dados por meio do JDBC, como [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="2a464-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect with the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="2a464-111">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar o driver JDBC do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="2a464-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="2a464-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2a464-112">Example</span></span>

<span data-ttu-id="2a464-113">Conectar-se ao banco de dados SQL e selecionar todos os registros em uma tabela usando o JDBC.</span><span class="sxs-lookup"><span data-stu-id="2a464-113">Connect to SQL database and select all records in a table using JDBC.</span></span>

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a><span data-ttu-id="2a464-114">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="2a464-114">Management API</span></span>

<span data-ttu-id="2a464-115">Criar e gerenciar recursos do Banco de Dados SQL do Azure em sua assinatura com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="2a464-115">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span>   

<span data-ttu-id="2a464-116">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="2a464-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a464-117">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="2a464-117">Explore the Management APIs</span></span>](/java/api/overview/azure/sql/management)

### <a name="example"></a><span data-ttu-id="2a464-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2a464-118">Example</span></span>

<span data-ttu-id="2a464-119">Criar um recurso de Banco de Dados SQL e restringir o acesso a um intervalo de endereços IP usando uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="2a464-119">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a><span data-ttu-id="2a464-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="2a464-120">Samples</span></span>

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

<span data-ttu-id="2a464-121">Explorar mais [exemplos de código Java para o Banco de Dados SQL do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2a464-121">Explore more [sample Java code for Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) you can use in your apps.</span></span>