---
title: Bibliotecas do Banco de Dados do Azure para MySQL para Java
description: Documentação de referência para as bibliotecas de cliente de Java para o Banco de Dados do Azure para MySQL
keywords: Azure, Java, SDK, API, SQL, banco de dados, PostGres, MySQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.devlang: java
ms.service: mysql
ms.openlocfilehash: f3c0b84a8c6577e5a844c4084b3d9cfaf3a52323
ms.sourcegitcommit: 1b22376e4ceb3d2f2734c8fc80823a44cc5fe8fb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42703346"
---
# <a name="azure-database-for-mysql-libraries-for-java"></a><span data-ttu-id="47fcf-104">Bibliotecas do Banco de Dados do Azure para MySQL para Java</span><span class="sxs-lookup"><span data-stu-id="47fcf-104">Azure Database for MySQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="47fcf-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="47fcf-105">Overview</span></span>

<span data-ttu-id="47fcf-106">O [Banco de Dados do Azure para MySQL](/azure/sql-database/sql-database-technical-overview) é um serviço de banco de dados relacional com base no mecanismo de banco de dados [MySQL](https://www.mysql.com/) de software livre.</span><span class="sxs-lookup"><span data-stu-id="47fcf-106">[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview) is a relational database service based on the open source [MySQL](https://www.mysql.com/) Server engine.</span></span> 

<span data-ttu-id="47fcf-107">Para começar a usar o Banco de dados do Azure para MySQL, consulte [Usar Java para se conectar e consultar dados](/azure/mysql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="47fcf-107">To get started with Azure Database for MySQL, see [Use Java to connect and query data](/azure/mysql/connect-java).</span></span>

## <a name="client-jbdc-driver"></a><span data-ttu-id="47fcf-108">Driver JBDC do cliente</span><span class="sxs-lookup"><span data-stu-id="47fcf-108">Client JBDC driver</span></span>

<span data-ttu-id="47fcf-109">Conectar-se ao Banco de Dados do Azure para MySQL a partir dos seus aplicativos usando o [driver JDBC do MySQL](https://dev.mysql.com/downloads/connector/j/) de software livre.</span><span class="sxs-lookup"><span data-stu-id="47fcf-109">Connect to Azure Database for MySQL from your applications using the open-source [MySQL JDBC driver](https://dev.mysql.com/downloads/connector/j/).</span></span> <span data-ttu-id="47fcf-110">Você pode usar o [API do JDBC de Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para se conectar ao banco de dados ou usar as estruturas de acesso a dados que interagem com o banco de dados por meio do JDBC, como [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="47fcf-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="47fcf-111">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar o driver JDBC do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="47fcf-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="47fcf-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="47fcf-112">Example</span></span>

<span data-ttu-id="47fcf-113">Conectar-se ao Banco de Dados do Azure para MySQL usando o JDBC e selecionar todos os registros na tabela de vendas.</span><span class="sxs-lookup"><span data-stu-id="47fcf-113">Connect to Azure Database for MySQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="47fcf-114">Você pode obter a cadeia de conexão para o seu banco de dados no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="47fcf-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="47fcf-115">Exemplos</span><span class="sxs-lookup"><span data-stu-id="47fcf-115">Samples</span></span>

<span data-ttu-id="47fcf-116">[Compilar um aplicativo Web Java e MySQL](/azure/app-service-web/app-service-web-tutorial-java-mysql) </span><span class="sxs-lookup"><span data-stu-id="47fcf-116">[Build a Java and MySQL web app](/azure/app-service-web/app-service-web-tutorial-java-mysql) </span></span>  
[<span data-ttu-id="47fcf-117">Criar um banco de dados MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="47fcf-117">Design a MySQL database using the Azure CLI</span></span>](/azure/mysql/tutorial-design-database-using-cli)   

<span data-ttu-id="47fcf-118">Explore mais [exemplos de código Java para o Banco de Dados do Azure para MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="47fcf-118">Explore more [sample Java code for Azure Database for MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) you can use in your apps.</span></span>
