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
# <a name="how-to-use-spring-data-jdbc-with-azure-postgresql"></a><span data-ttu-id="76d81-103">Como usar o Spring Data JDBC com o Azure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="76d81-103">How to use Spring Data JDBC with Azure PostgreSQL</span></span>

## <a name="overview"></a><span data-ttu-id="76d81-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="76d81-104">Overview</span></span>

<span data-ttu-id="76d81-105">Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações em um banco de dados [PostgreSQL] do Azure https://www.postgresql.org/ usando [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span><span class="sxs-lookup"><span data-stu-id="76d81-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [PostgreSQL]https://www.postgresql.org/ database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76d81-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="76d81-106">Prerequisites</span></span>

<span data-ttu-id="76d81-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="76d81-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="76d81-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="76d81-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="76d81-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="76d81-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="76d81-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="76d81-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="76d81-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="76d81-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="76d81-112">[Curl](https://curl.haxx.se/) ou utilitário HTTP semelhante para testar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="76d81-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="76d81-113">O utilitário de linha de comando [psql](https://www.postgresql.org/docs/current/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="76d81-113">The [psql](https://www.postgresql.org/docs/current/app-psql.html) command-line utility.</span></span>
* <span data-ttu-id="76d81-114">Um cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="76d81-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-postgresql-database-for-azure"></a><span data-ttu-id="76d81-115">Criar um banco de dados PostgreSQL para o Azure</span><span class="sxs-lookup"><span data-stu-id="76d81-115">Create a PostgreSQL database for Azure</span></span>

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="76d81-116">Criar um servidor de banco de dados PostgreSQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="76d81-116">Create a PostgreSQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="76d81-117">Veja informações mais detalhadas sobre a criação de bancos de dados PostgreSQL em [Criar um Banco de Dados do Azure para o servidor PostgreSQL usando o portal do Azure](/azure/postgresql/quickstart-create-server-database-portal).</span><span class="sxs-lookup"><span data-stu-id="76d81-117">You can read more detailed information about creating PostgreSQL databases in [Create an Azure Database for PostgreSQL server by using the Azure portal](/azure/postgresql/quickstart-create-server-database-portal).</span></span>

1. <span data-ttu-id="76d81-118">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="76d81-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="76d81-119">Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Banco de Dados do Azure para PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="76d81-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for PostgreSQL**.</span></span>

   ![Criar um banco de dados PostgreSQL][POSTGRESQL01]

1. <span data-ttu-id="76d81-121">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="76d81-121">Enter the following information:</span></span>

   - <span data-ttu-id="76d81-122">**Nome do servidor**: Escolha um nome exclusivo para o servidor PostgreSQL. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoyspostgresql.postgres.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="76d81-122">**Server name**: Choose a unique name for your PostgreSQL server; this will be used to create a fully-qualified domain name like *wingtiptoyspostgresql.postgres.database.azure.com*.</span></span>
   - <span data-ttu-id="76d81-123">**Assinatura**: especifique a assinatura do Azure para usar.</span><span class="sxs-lookup"><span data-stu-id="76d81-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="76d81-124">**Grupo de recursos**: especifique se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="76d81-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="76d81-125">**Selecionar fonte**: no caso deste tutorial, escolha `Blank` para criar um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="76d81-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="76d81-126">**Logon de administrador do servidor**: especifique o nome do administrador do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="76d81-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="76d81-127">**Senha** e **Confirmar senha**: especifique a senha para o administrador do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="76d81-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="76d81-128">**Localização**: especifique a região geográfica mais próxima do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="76d81-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="76d81-129">**Versão**: especifique a versão mais atualizada do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="76d81-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="76d81-130">**Tipo de preço**: no caso deste tutorial, especifica o tipo de preço menos caro.</span><span class="sxs-lookup"><span data-stu-id="76d81-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Criar as propriedades do banco de dados PostgreSQL][POSTGRESQL02]

1. <span data-ttu-id="76d81-132">Após inserir todas as informações acima, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="76d81-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="76d81-133">Configurar uma regra de firewall para o servidor de banco de dados PostgreSQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="76d81-133">Configure a firewall rule for your PostgreSQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="76d81-134">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="76d81-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="76d81-135">Clique em **Todos os Recursos** e, em seguida, clique no banco de dados PostgreSQL que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="76d81-135">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Escolher o banco de dados PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="76d81-137">Clique em **Segurança de conexão** e, nas **Regras de firewall** , crie uma nova regra especificando um nome exclusivo para a regra e, em seguida, insira o intervalo de endereços IP que precisarão acessar seu banco de dados e clique em **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="76d81-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configurar a segurança da conexão][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a><span data-ttu-id="76d81-139">Recuperar a cadeia de conexão para seu Servidor PostgreSQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="76d81-139">Retrieve the connection string for your PostgreSQL server using the Azure Portal</span></span>

1. <span data-ttu-id="76d81-140">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="76d81-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="76d81-141">Clique em **Todos os Recursos** e, em seguida, clique no banco de dados PostgreSQL que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="76d81-141">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Escolher o banco de dados PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="76d81-143">Clique em **Cadeias de conexão** e copie o valor no campo de texto **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="76d81-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Recuperar sua cadeia de conexão JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a><span data-ttu-id="76d81-145">Criar banco de dados PostgreSQL usando o utilitário de linha de comando `psql`</span><span class="sxs-lookup"><span data-stu-id="76d81-145">Create PostgreSQL database using the `psql` command-line utility</span></span>

1. <span data-ttu-id="76d81-146">Abra um shell de comando e conecte-se ao servidor PostgreSQL digitando um comando `psql` como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="76d81-146">Open a command shell and connect to your PostgreSQL server by entering a `psql` command like the following example:</span></span>

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   <span data-ttu-id="76d81-147">Em que:</span><span class="sxs-lookup"><span data-stu-id="76d81-147">Where:</span></span>

   | <span data-ttu-id="76d81-148">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="76d81-148">Parameter</span></span> | <span data-ttu-id="76d81-149">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="76d81-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="76d81-150">Especifica o nome totalmente qualificado do servidor PostgreSQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="76d81-150">Specifies your fully qualified PostgreSQL server name from earlier in this article.</span></span> |
   | `host` | <span data-ttu-id="76d81-151">Especifica a porta do servidor PostgreSQL, que é `5432` por padrão.</span><span class="sxs-lookup"><span data-stu-id="76d81-151">Specifies the PostgreSQL server port, which is `5432` by default.</span></span> |
   | `username` | <span data-ttu-id="76d81-152">Especifica o administrador do PostgreSQL e o nome abreviado do servidor neste artigo.</span><span class="sxs-lookup"><span data-stu-id="76d81-152">Specifies your PostgreSQL administrator and shortened server name from earlier in this article.</span></span> |
   | `dbname` | <span data-ttu-id="76d81-153">Especifica que você deseja usar o banco de dados `postgres` padrão por enquanto.</span><span class="sxs-lookup"><span data-stu-id="76d81-153">Specifies that you want to use the default `postgres` database for now.</span></span> |

   <span data-ttu-id="76d81-154">Seu servidor PostgreSQL deve responder com uma exibição como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="76d81-154">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. <span data-ttu-id="76d81-155">Crie um banco de dados denominado *mypgsqldb* inserindo um comando `psql` como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="76d81-155">Create a database named *mypgsqldb* by entering a `psql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   <span data-ttu-id="76d81-156">Seu servidor PostgreSQL deve responder com uma exibição como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="76d81-156">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   CREATE DATABASE
   ```

1. <span data-ttu-id="76d81-157">OPCIONAL: verifique se seu banco de dados foi criado inserindo um `\l` no `psql`. Seu servidor PostgreSQL deverá responder com algo semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="76d81-157">OPTIONAL: You can verify that your database was created by entering a `\l` at the `psql`; your PostgreSQL server should respond with something like the following example:</span></span>

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

1. <span data-ttu-id="76d81-158">Insira `\q` para sair do utilitário `psql`.</span><span class="sxs-lookup"><span data-stu-id="76d81-158">Enter `\q` to exit the `psql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="76d81-159">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="76d81-159">Configure the sample application</span></span>

1. <span data-ttu-id="76d81-160">Abra um shell de comando e clone o projeto de exemplo usando um comando git como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="76d81-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="76d81-161">Localize o arquivo *application.properties* no diretório *recursos* do seu projeto de exemplo ou crie o arquivo se ele ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="76d81-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="76d81-162">Abra o arquivo *application.properties* em um editor de texto e adicione ou configure as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:</span><span class="sxs-lookup"><span data-stu-id="76d81-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   <span data-ttu-id="76d81-163">Em que:</span><span class="sxs-lookup"><span data-stu-id="76d81-163">Where:</span></span>

   | <span data-ttu-id="76d81-164">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="76d81-164">Parameter</span></span> | <span data-ttu-id="76d81-165">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="76d81-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="76d81-166">Especifica sua cadeia de JDBC do PostgreSQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="76d81-166">Specifies your PostgreSQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="76d81-167">Especifica o nome do administrador do PostgreSQL neste artigo com o nome abreviado do servidor anexado a ele.</span><span class="sxs-lookup"><span data-stu-id="76d81-167">Specifies your PostgreSQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="76d81-168">Especifica sua senha de administrador do PostgreSQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="76d81-168">Specifies your PostgreSQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="76d81-169">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="76d81-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="76d81-170">Empacotar e testar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="76d81-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="76d81-171">Crie seu aplicativo de exemplo com o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="76d81-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P postgresql
   ```

1. <span data-ttu-id="76d81-172">Inicie o aplicativo de exemplo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="76d81-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="76d81-173">Crie novos registros usando `curl` em um prompt de comando como nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="76d81-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="76d81-174">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="76d81-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="76d81-175">Recupere todos os registros existentes usando `curl` em um prompt de comando como nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="76d81-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="76d81-176">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="76d81-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="76d81-177">Resumo</span><span class="sxs-lookup"><span data-stu-id="76d81-177">Summary</span></span>

<span data-ttu-id="76d81-178">Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações em um banco de dados do Azure PostgreSQL usando o JDBC.</span><span class="sxs-lookup"><span data-stu-id="76d81-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure PostgreSQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76d81-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="76d81-179">Next steps</span></span>

<span data-ttu-id="76d81-180">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="76d81-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="76d81-181">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="76d81-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="76d81-182">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="76d81-182">Additional Resources</span></span>

<span data-ttu-id="76d81-183">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="76d81-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[POSTGRESQL01]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-05.png
