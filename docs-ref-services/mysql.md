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
# <a name="azure-database-for-mysql-libraries-for-java"></a>Bibliotecas do Banco de Dados do Azure para MySQL para Java

## <a name="overview"></a>Visão geral

O [Banco de Dados do Azure para MySQL](/azure/sql-database/sql-database-technical-overview) é um serviço de banco de dados relacional com base no mecanismo de banco de dados [MySQL](https://www.mysql.com/) de software livre. 

Para começar a usar o Banco de dados do Azure para MySQL, consulte [Usar Java para se conectar e consultar dados](/azure/mysql/connect-java).

## <a name="client-jbdc-driver"></a>Driver JBDC do cliente

Conectar-se ao Banco de Dados do Azure para MySQL a partir dos seus aplicativos usando o [driver JDBC do MySQL](https://dev.mysql.com/downloads/connector/j/) de software livre. Você pode usar o [API do JDBC de Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para se conectar ao banco de dados ou usar as estruturas de acesso a dados que interagem com o banco de dados por meio do JDBC, como [Hibernate](http://hibernate.org/).

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar o driver JDBC do cliente em seu projeto.  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a>Exemplo

Conectar-se ao Banco de Dados do Azure para MySQL usando o JDBC e selecionar todos os registros na tabela de vendas. Você pode obter a cadeia de conexão para o seu banco de dados no Portal do Azure.

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a>Exemplos

[Compilar um aplicativo Web Java e MySQL](/azure/app-service-web/app-service-web-tutorial-java-mysql)   
[Criar um banco de dados MySQL usando a CLI do Azure](/azure/mysql/tutorial-design-database-using-cli)   

Explore mais [exemplos de código Java para o Banco de Dados do Azure para MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) que você pode usar em seus aplicativos.
