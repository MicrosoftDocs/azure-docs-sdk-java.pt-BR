---
title: Bibliotecas de Banco de Dados SQL do Azure para Java
description: "Conecte-se ao banco de dados do SQL Azure usando o driver JDBC ou as instâncias de banco de dados do SQL do Azure com a API de gerenciamento."
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
ms.openlocfilehash: 3ae4015ae57e5eac4dafb30f4a42881986501853
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-sql-database-libraries-for-java"></a>Bibliotecas de Banco de Dados SQL do Azure para Java

## <a name="overview"></a>Visão geral

O [Banco de Dados SQL do Azure](/azure/sql-database/sql-database-technical-overview) é um serviço de banco de dados relacional que usa o mecanismo do Microsoft SQL Server com suporte para dados de tabela, JSON, espaciais e XML. 

Para começar a usar o Banco de Dados SQL do Azure, consulte [Banco de Dados SQL do Azure: Usar Java para se conectar e consultar dados](/azure/sql-database/sql-database-connect-query-java).

## <a name="client-jdbc-driver"></a>Driver JDBC do cliente

Conecte-se ao banco de dados do SQL Azure a partir de seus aplicativos usando o [driver JDBC do Banco de Dados SQL](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server). Você pode usar a [API do JDBC de Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para se conectar diretamente ao banco de dados ou usar as estruturas de acesso a dados que interagem com o banco de dados por meio do JDBC, como [Hibernate](http://hibernate.org/).

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar o driver JDBC do cliente em seu projeto.


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Conectar-se ao banco de dados SQL e selecionar todos os registros em uma tabela usando o JDBC.

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a>API de Gerenciamento

Criar e gerenciar recursos do Banco de Dados SQL do Azure em sua assinatura com a API de gerenciamento.   

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/sql/managementapi)

### <a name="example"></a>Exemplo

Criar um recurso de Banco de Dados SQL e restringir o acesso a um intervalo de endereços IP usando uma regra de firewall.

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a>Exemplos

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

Explorar mais [exemplos de código Java para o Banco de Dados SQL do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) que você pode usar em seus aplicativos.