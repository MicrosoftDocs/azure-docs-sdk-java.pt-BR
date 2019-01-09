---
title: Como usar o Spring Data JDBC com o Azure PostgreSQL
description: Saiba como usar o Spring Data JDBC com um banco de dados Azure PostgreSQL.
services: postgresql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: postgresql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 371a8c686f7ad045443328d02a32a4e65af55981
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991960"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-postgresql"></a>Como usar o Spring Data JDBC com o Azure PostgreSQL

## <a name="overview"></a>Visão geral

Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações em um banco de dados [PostgreSQL] do Azure https://www.postgresql.org/ usando [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).

## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.
* [Curl](https://curl.haxx.se/) ou utilitário HTTP semelhante para testar a funcionalidade.
* O utilitário de linha de comando [psql](https://www.postgresql.org/docs/current/app-psql.html).
* Um cliente [Git](https://git-scm.com/downloads).

## <a name="create-a-postgresql-database-for-azure"></a>Criar um banco de dados PostgreSQL para o Azure

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a>Criar um servidor de banco de dados PostgreSQL usando o Portal do Azure

> [!NOTE]
> 
> Veja informações mais detalhadas sobre a criação de bancos de dados PostgreSQL em [Criar um Banco de Dados do Azure para o servidor PostgreSQL usando o portal do Azure](/azure/postgresql/quickstart-create-server-database-portal).

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Banco de Dados do Azure para PostgreSQL**.

   ![Criar um banco de dados PostgreSQL][POSTGRESQL01]

1. Insira as seguintes informações:

   - **Nome do servidor**: Escolha um nome exclusivo para o servidor PostgreSQL. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoyspostgresql.postgres.database.azure.com*.
   - **Assinatura**: especifique a assinatura do Azure para usar.
   - **Grupo de recursos**: especifique se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.
   - **Selecionar fonte**: no caso deste tutorial, escolha `Blank` para criar um novo banco de dados.
   - **Logon de administrador do servidor**: especifique o nome do administrador do banco de dados.
   - **Senha** e **Confirmar senha**: especifique a senha para o administrador do banco de dados.
   - **Localização**: especifique a região geográfica mais próxima do banco de dados.
   - **Versão**: especifique a versão mais atualizada do banco de dados.
   - **Tipo de preço**: no caso deste tutorial, especifica o tipo de preço menos caro.

   ![Criar as propriedades do banco de dados PostgreSQL][POSTGRESQL02]

1. Após inserir todas as informações acima, clique em **Criar**.

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a>Configurar uma regra de firewall para o servidor de banco de dados PostgreSQL usando o Portal do Azure

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **Todos os Recursos** e, em seguida, clique no banco de dados PostgreSQL que acabou de criar.

   ![Escolher o banco de dados PostgreSQL][POSTGRESQL03]

1. Clique em **Segurança de conexão** e, nas **Regras de firewall** , crie uma nova regra especificando um nome exclusivo para a regra e, em seguida, insira o intervalo de endereços IP que precisarão acessar seu banco de dados e clique em **Salvar** .

   ![Configurar a segurança da conexão][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a>Recuperar a cadeia de conexão para seu Servidor PostgreSQL usando o Portal do Azure

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **Todos os Recursos** e, em seguida, clique no banco de dados PostgreSQL que acabou de criar.

   ![Escolher o banco de dados PostgreSQL][POSTGRESQL03]

1. Clique em **Cadeias de conexão** e copie o valor no campo de texto **JDBC**.

   ![Recuperar sua cadeia de conexão JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a>Criar banco de dados PostgreSQL usando o utilitário de linha de comando `psql`

1. Abra um shell de comando e conecte-se ao servidor PostgreSQL digitando um comando `psql` como no exemplo a seguir:

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   Em que:

   | Parâmetro | DESCRIÇÃO |
   |---|---|
   | `host` | Especifica o nome totalmente qualificado do servidor PostgreSQL neste artigo. |
   | `host` | Especifica a porta do servidor PostgreSQL, que é `5432` por padrão. |
   | `username` | Especifica o administrador do PostgreSQL e o nome abreviado do servidor neste artigo. |
   | `dbname` | Especifica que você deseja usar o banco de dados `postgres` padrão por enquanto. |

   Seu servidor PostgreSQL deve responder com uma exibição como o exemplo a seguir:

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. Crie um banco de dados denominado *mypgsqldb* inserindo um comando `psql` como o exemplo a seguir:

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   Seu servidor PostgreSQL deve responder com uma exibição como o exemplo a seguir:

   ```shell
   CREATE DATABASE
   ```

1. OPCIONAL: verifique se seu banco de dados foi criado inserindo um `\l` no `psql`. Seu servidor PostgreSQL deverá responder com algo semelhante ao exemplo a seguir:

   ```shell
                   List of databases
          Name        |      Owner      | Encoding
   -------------------+-----------------+----------
    azure_maintenance | azure_superuser | UTF8
    azure_sys         | azure_superuser | UTF8
    mypgsqldb         | wingtiptoysuser | UTF8
    postgres          | azure_superuser | UTF8
    template0         | azure_superuser | UTF8
    template1         | azure_superuser | UTF8
   (6 rows)
   ```

1. Insira `\q` para sair do utilitário `psql`.

## <a name="configure-the-sample-application"></a>Configurar o aplicativo de exemplo

1. Abra um shell de comando e clone o projeto de exemplo usando um comando git como no exemplo a seguir:

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. Localize o arquivo *application.properties* no diretório *recursos* do seu projeto de exemplo ou crie o arquivo se ele ainda não existe.

1. Abra o arquivo *application.properties* em um editor de texto e adicione ou configure as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   Em que:

   | Parâmetro | DESCRIÇÃO |
   |---|---|
   | `spring.datasource.url` | Especifica sua cadeia de JDBC do PostgreSQL neste artigo. |
   | `spring.datasource.username` | Especifica o nome do administrador do PostgreSQL neste artigo com o nome abreviado do servidor anexado a ele. |
   | `spring.datasource.password` | Especifica sua senha de administrador do PostgreSQL neste artigo. |

1. Salve e feche o arquivo *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Empacotar e testar o aplicativo de exemplo 

1. Crie seu aplicativo de exemplo com o Maven. Por exemplo:

   ```shell
   mvn clean package -P postgresql
   ```

1. Inicie o aplicativo de exemplo. Por exemplo:

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. Crie novos registros usando `curl` em um prompt de comando como nos exemplos a seguir:

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   Seu aplicativo deve retornar valores como os seguintes:

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. Recupere todos os registros existentes usando `curl` em um prompt de comando como nos exemplos a seguir:

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   Seu aplicativo deve retornar valores como os seguintes:

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>Resumo

Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações em um banco de dados do Azure PostgreSQL usando o JDBC.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.

> [!div class="nextstepaction"]
> [Spring no Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionais

Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].

<!-- URL List -->

[Azure para desenvolvedores Java]: /java/azure/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Como trabalhar com o Java e o Azure DevOps]: /azure/devops/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[POSTGRESQL01]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-05.png
