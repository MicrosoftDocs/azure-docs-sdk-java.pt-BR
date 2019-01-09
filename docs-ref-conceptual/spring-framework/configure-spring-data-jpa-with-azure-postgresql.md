---
title: Como usar o Spring Data JPA com o Azure PostgreSQL
description: Saiba como usar o Spring Data JPA com um banco de dados Azure PostgreSQL.
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
ms.openlocfilehash: 1849e03674534882a579f85b2654a628bd867487
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991961"
---
# <a name="how-to-use-spring-data-jpa-with-azure-postgresql"></a><span data-ttu-id="04119-103">Como usar o Spring Data JPA com o Azure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="04119-103">How to use Spring Data JPA with Azure PostgreSQL</span></span>

## <a name="overview"></a><span data-ttu-id="04119-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="04119-104">Overview</span></span>

<span data-ttu-id="04119-105">Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações em um banco de dados [PostgreSQL]https://www.postgresql.org/ do Azure usando [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span><span class="sxs-lookup"><span data-stu-id="04119-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [PostgreSQL]https://www.postgresql.org/ database using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04119-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="04119-106">Prerequisites</span></span>

<span data-ttu-id="04119-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="04119-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="04119-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="04119-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="04119-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="04119-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="04119-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="04119-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="04119-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="04119-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="04119-112">[Curl](https://curl.haxx.se/) ou utilitário HTTP semelhante para testar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="04119-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span> <span data-ttu-id="04119-113">ou utilitário HTTP semelhante para testar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="04119-113">or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="04119-114">O utilitário de linha de comando [psql](https://www.postgresql.org/docs/current/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="04119-114">The [psql](https://www.postgresql.org/docs/current/app-psql.html) command-line utility.</span></span>
* <span data-ttu-id="04119-115">Um cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="04119-115">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-postgresql-database-for-azure"></a><span data-ttu-id="04119-116">Criar um banco de dados PostgreSQL para o Azure</span><span class="sxs-lookup"><span data-stu-id="04119-116">Create a PostgreSQL database for Azure</span></span>

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="04119-117">Criar um servidor de banco de dados PostgreSQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="04119-117">Create a PostgreSQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="04119-118">Veja informações mais detalhadas sobre a criação de bancos de dados PostgreSQL em [Criar um Banco de Dados do Azure para o servidor PostgreSQL usando o portal do Azure](/azure/postgresql/quickstart-create-server-database-portal).</span><span class="sxs-lookup"><span data-stu-id="04119-118">You can read more detailed information about creating PostgreSQL databases in [Create an Azure Database for PostgreSQL server by using the Azure portal](/azure/postgresql/quickstart-create-server-database-portal).</span></span>

1. <span data-ttu-id="04119-119">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="04119-119">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="04119-120">Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Banco de Dados do Azure para PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="04119-120">Click **+Create a resource**, then **Databases**, and then click **Azure Database for PostgreSQL**.</span></span>

   ![Criar um banco de dados PostgreSQL][POSTGRESQL01]

1. <span data-ttu-id="04119-122">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="04119-122">Enter the following information:</span></span>

   - <span data-ttu-id="04119-123">**Nome do servidor**: Escolha um nome exclusivo para o servidor PostgreSQL. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoyspostgresql.postgres.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="04119-123">**Server name**: Choose a unique name for your PostgreSQL server; this will be used to create a fully-qualified domain name like *wingtiptoyspostgresql.postgres.database.azure.com*.</span></span>
   - <span data-ttu-id="04119-124">**Assinatura**: especifica a assinatura do Azure para usar.</span><span class="sxs-lookup"><span data-stu-id="04119-124">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="04119-125">**Grupo de recursos**: especifica se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="04119-125">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="04119-126">**Selecionar fonte**: no caso deste tutorial, escolha `Blank` para criar um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04119-126">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="04119-127">**Logon de administrador do servidor**: especifica o nome do administrador do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04119-127">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="04119-128">**Senha** e **Confirmar senha**: especifica a senha para o administrador do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04119-128">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="04119-129">**Localização**: especifica a região geográfica mais próxima do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04119-129">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="04119-130">**Versão**: especifica a versão mais atualizada do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04119-130">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="04119-131">**Tipo de preço**: no caso deste tutorial, especifica o tipo de preço menos dispendioso.</span><span class="sxs-lookup"><span data-stu-id="04119-131">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Criar as propriedades do banco de dados PostgreSQL][POSTGRESQL02]

1. <span data-ttu-id="04119-133">Após inserir todas as informações acima, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="04119-133">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="04119-134">Configurar uma regra de firewall para o servidor de banco de dados PostgreSQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="04119-134">Configure a firewall rule for your PostgreSQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="04119-135">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="04119-135">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="04119-136">Clique em **Todos os Recursos** e, em seguida, clique no banco de dados PostgreSQL que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="04119-136">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Escolher o banco de dados PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="04119-138">Clique em **Segurança de conexão** e, nas **Regras de firewall** , crie uma nova regra especificando um nome exclusivo para a regra e, em seguida, insira o intervalo de endereços IP que precisarão acessar seu banco de dados e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="04119-138">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configurar a segurança da conexão][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a><span data-ttu-id="04119-140">Recuperar a cadeia de conexão para seu Servidor PostgreSQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="04119-140">Retrieve the connection string for your PostgreSQL server using the Azure Portal</span></span>

1. <span data-ttu-id="04119-141">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="04119-141">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="04119-142">Clique em **Todos os Recursos** e, em seguida, clique no banco de dados PostgreSQL que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="04119-142">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Escolher o banco de dados PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="04119-144">Clique em **Cadeias de caracteres de Conexão** e copie o valor no campo de texto **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="04119-144">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Recuperar sua cadeia de conexão JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a><span data-ttu-id="04119-146">Criar banco de dados PostgreSQL usando o utilitário de linha de comando `psql`</span><span class="sxs-lookup"><span data-stu-id="04119-146">Create PostgreSQL database using the `psql` command-line utility</span></span>

1. <span data-ttu-id="04119-147">Abra um shell de comando e conecte-se ao servidor PostgreSQL digitando um comando `psql` como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="04119-147">Open a command shell and connect to your PostgreSQL server by entering a `psql` command like the following example:</span></span>

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   <span data-ttu-id="04119-148">Em que:</span><span class="sxs-lookup"><span data-stu-id="04119-148">Where:</span></span>

   | <span data-ttu-id="04119-149">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="04119-149">Parameter</span></span> | <span data-ttu-id="04119-150">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="04119-150">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="04119-151">Especifica o nome totalmente qualificado do servidor PostgreSQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="04119-151">Specifies your fully qualified PostgreSQL server name from earlier in this article.</span></span> |
   | `host` | <span data-ttu-id="04119-152">Especifica a porta do servidor PostgreSQL, que é `5432` por padrão.</span><span class="sxs-lookup"><span data-stu-id="04119-152">Specifies the PostgreSQL server port, which is `5432` by default.</span></span> |
   | `username` | <span data-ttu-id="04119-153">Especifica o administrador do PostgreSQL e o nome abreviado do servidor neste artigo.</span><span class="sxs-lookup"><span data-stu-id="04119-153">Specifies your PostgreSQL administrator and shortened server name from earlier in this article.</span></span> |
   | `dbname` | <span data-ttu-id="04119-154">Especifica que você deseja usar o banco de dados `postgres` padrão por enquanto.</span><span class="sxs-lookup"><span data-stu-id="04119-154">Specifies that you want to use the default `postgres` database for now.</span></span> |

   <span data-ttu-id="04119-155">Seu servidor PostgreSQL deve responder com uma exibição como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="04119-155">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. <span data-ttu-id="04119-156">Crie um banco de dados denominado *mypgsqldb* inserindo um comando `psql` como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="04119-156">Create a database named *mypgsqldb* by entering a `psql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   <span data-ttu-id="04119-157">Seu servidor PostgreSQL deve responder com uma exibição como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="04119-157">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   CREATE DATABASE
   ```

1. <span data-ttu-id="04119-158">OPCIONAL: verifique se seu banco de dados foi criado inserindo um `\l` no `psql`. Seu servidor PostgreSQL deverá responder com algo semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="04119-158">OPTIONAL: You can verify that your database was created by entering a `\l` at the `psql`; your PostgreSQL server should respond with something like the following example:</span></span>

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

1. <span data-ttu-id="04119-159">Insira `\q` para sair do utilitário `psql`.</span><span class="sxs-lookup"><span data-stu-id="04119-159">Enter `\q` to exit the `psql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="04119-160">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="04119-160">Configure the sample application</span></span>

1. <span data-ttu-id="04119-161">Abra um shell de comando e clone o projeto de exemplo usando um comando git como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="04119-161">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. <span data-ttu-id="04119-162">Localize o arquivo *application.properties* no diretório *recursos* do seu projeto de exemplo ou crie o arquivo se ele ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="04119-162">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="04119-163">Abra o arquivo *application.properties* em um editor de texto e adicione ou configure as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:</span><span class="sxs-lookup"><span data-stu-id="04119-163">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   <span data-ttu-id="04119-164">Em que:</span><span class="sxs-lookup"><span data-stu-id="04119-164">Where:</span></span>

   | <span data-ttu-id="04119-165">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="04119-165">Parameter</span></span> | <span data-ttu-id="04119-166">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="04119-166">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="04119-167">Especifica sua cadeia de JDBC do PostgreSQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="04119-167">Specifies your PostgreSQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="04119-168">Especifica o nome do administrador do PostgreSQL neste artigo com o nome abreviado do servidor anexado a ele.</span><span class="sxs-lookup"><span data-stu-id="04119-168">Specifies your PostgreSQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="04119-169">Especifica sua senha de administrador do PostgreSQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="04119-169">Specifies your PostgreSQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="04119-170">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="04119-170">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="04119-171">Empacotar e testar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="04119-171">Package and test the sample application</span></span> 

1. <span data-ttu-id="04119-172">Crie seu aplicativo de exemplo com o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04119-172">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P postgresql
   ```

1. <span data-ttu-id="04119-173">Inicie o aplicativo de exemplo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04119-173">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="04119-174">Crie novos registros usando `curl` em um prompt de comando como os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="04119-174">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="04119-175">Seu aplicativo deve retornar valores com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="04119-175">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="04119-176">Recupere todos os registros existentes usando `curl` em um prompt de comando como os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="04119-176">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="04119-177">Seu aplicativo deve retornar valores com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="04119-177">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="04119-178">Resumo</span><span class="sxs-lookup"><span data-stu-id="04119-178">Summary</span></span>

<span data-ttu-id="04119-179">Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações em um banco de dados do Azure PostgreSQL usando o JPA.</span><span class="sxs-lookup"><span data-stu-id="04119-179">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure PostgreSQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04119-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04119-180">Next steps</span></span>

<span data-ttu-id="04119-181">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="04119-181">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="04119-182">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="04119-182">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="04119-183">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="04119-183">Additional Resources</span></span>

<span data-ttu-id="04119-184">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="04119-184">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Azure para desenvolvedores Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Como trabalhar com o Java e o Azure DevOps]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[POSTGRESQL01]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-05.png
