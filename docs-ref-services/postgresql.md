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
# <a name="azure-database-for-postgresql-libraries-for-java"></a>Bibliotecas do Banco de Dados do Azure para PostgreSQL para Java

## <a name="overview"></a>Visão geral

O [Banco de Dados do Azure para PostgreSQL](/azure/sql-database/sql-database-technical-overview) é um serviço de banco de dados relacional no Azure, projetado para desenvolvedores com base na versão de comunidade do mecanismo de banco de dados [PostgreSQL](https://www.postgresql.org/) de software livre.

Para começar a usar o Banco de dados do Azure para PostgreSQL, consulte [Usar Java para se conectar e consultar dados](/azure/postgresql/connect-java).

## <a name="client-jdbc-driver"></a>Driver JDBC do cliente

Conectar-se ao Banco de Dados do Azure para PostgreSQL a partir dos seus aplicativos usando o [driver JDBC do PostgreSQL](https://jdbc.postgresql.org/) de software livre. Você pode usar o [API do JDBC de Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) para se conectar ao banco de dados ou usar as estruturas de acesso a dados que interagem com o banco de dados por meio do JDBC, como [Hibernate](http://hibernate.org/).

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar o driver JDBC do cliente em seu projeto.  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a>Exemplo

Conectar-se ao Banco de Dados do Azure para PostgreSQL usando o JDBC e selecionar todos os registros na tabela de vendas. Você pode obter a cadeia de conexão para o seu banco de dados no Portal do Azure.

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

## <a name="samples"></a>Exemplos

[Criar um banco de dados PostgreSQL usando a CLI do Azure](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

Explore mais [exemplos de código Java para o Banco de Dados do Azure para PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) que você pode usar em seus aplicativos.
