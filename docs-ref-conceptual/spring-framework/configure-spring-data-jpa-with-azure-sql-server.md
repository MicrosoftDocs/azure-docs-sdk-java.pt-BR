---
title: Como usar o Spring Data JPA com o Banco de Dados SQL do Azure
description: Saiba como usar o Spring Data JPA com um banco de dados SQL do Azure.
services: sql-database
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: sql-database
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 02b6eff059c8b7dff1c7473d0460ca44e76f6f2e
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64673953"
---
# <a name="how-to-use-spring-data-jpa-with-azure-sql-database"></a><span data-ttu-id="60fe2-103">Como usar o Spring Data JPA com o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="60fe2-103">How to use Spring Data JPA with Azure SQL Database</span></span>

## <a name="overview"></a><span data-ttu-id="60fe2-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="60fe2-104">Overview</span></span>

<span data-ttu-id="60fe2-105">Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações em um [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/) usando [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span><span class="sxs-lookup"><span data-stu-id="60fe2-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60fe2-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="60fe2-106">Prerequisites</span></span>

<span data-ttu-id="60fe2-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="60fe2-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="60fe2-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="60fe2-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="60fe2-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="60fe2-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="60fe2-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="60fe2-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="60fe2-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="60fe2-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="60fe2-112">[Curl](https://curl.haxx.se/) ou utilitário HTTP semelhante para testar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="60fe2-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="60fe2-113">Um cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="60fe2-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="60fe2-114">Criar um Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="60fe2-114">Create an Azure SQL Database</span></span>

### <a name="create-a-sql-database-server-using-the-azure-portal"></a><span data-ttu-id="60fe2-115">Criar um servidor do banco de dados SQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60fe2-115">Create a SQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="60fe2-116">Você pode ler informações mais detalhadas sobre como criar bancos de dados SQL do Azure em [Criar um banco de dados SQL do Azure no portal do Azure](/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="60fe2-116">You can read more detailed information about creating Azure SQL databases in [Create an Azure SQL database in the Azure portal](/azure/sql-database/sql-database-get-started-portal).</span></span>

1. <span data-ttu-id="60fe2-117">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="60fe2-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="60fe2-118">Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="60fe2-118">Click **+Create a resource**, then **Databases**, and then click **SQL Database**.</span></span>

   ![Criar um banco de dados SQL][SQL01]

1. <span data-ttu-id="60fe2-120">Especifique as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="60fe2-120">Specify the following information:</span></span>

   - <span data-ttu-id="60fe2-121">**Nome do banco de dados**: escolha um nome exclusivo para seu banco de dados SQL. Ele será criado no SQL Server que você especificará posteriormente.</span><span class="sxs-lookup"><span data-stu-id="60fe2-121">**Database name**: Choose a unique name for your SQL database; this will be created in the SQL server that you will specify later.</span></span>
   - <span data-ttu-id="60fe2-122">**Assinatura**: especifique a assinatura do Azure para usar.</span><span class="sxs-lookup"><span data-stu-id="60fe2-122">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="60fe2-123">**Grupo de recursos**: especifique se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="60fe2-123">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="60fe2-124">**Selecionar fonte**: No caso deste tutorial, escolha `Blank database` para criar um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60fe2-124">**Select source**: For this tutorial, select `Blank database` to create a new database.</span></span>

   ![Especificar as propriedades do banco de dados SQL][SQL02]
   
1. <span data-ttu-id="60fe2-126">Clique em **Servidor**, **Criar um novo servidor** e especifique as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="60fe2-126">Click **Server**, then **Create a new server**, and then specify the following information:</span></span>

   - <span data-ttu-id="60fe2-127">**Nome do servidor**: Escolha um nome exclusivo para seu SQL Server. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoyssql.database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="60fe2-127">**Server name**: Choose a unique name for your SQL server; this will be used to create a fully-qualified domain name like *wingtiptoyssql.database.windows.net*.</span></span>
   - <span data-ttu-id="60fe2-128">**Logon de administrador do servidor**: especifique o nome do administrador do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60fe2-128">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="60fe2-129">**Senha** e **Confirmar senha**: especifique a senha para o administrador do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60fe2-129">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="60fe2-130">**Localização**: especifique a região geográfica mais próxima do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60fe2-130">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Especificar o SQL Server][SQL03]

1. <span data-ttu-id="60fe2-132">Após inserir todas as informações acima, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="60fe2-132">When you have entered all of the above information, click **Select**.</span></span>

1. <span data-ttu-id="60fe2-133">No caso deste tutorial, especifique o **Tipo de preço** menos caro e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="60fe2-133">For this tutorial, specify the least-expensive **Pricing tier**, and then click **Create**.</span></span>

   ![Criar o banco de dados SQL][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="60fe2-135">Configurar uma regra de firewall para o SQL Server usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60fe2-135">Configure a firewall rule for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="60fe2-136">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="60fe2-136">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="60fe2-137">Clique em **Todos os Recursos** e, em seguida, clique no SQL Server que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="60fe2-137">Click **All Resources**, then click the SQL server you just created.</span></span>

   ![Escolher o SQL Server][SQL05]

1. <span data-ttu-id="60fe2-139">Na seção **Visão geral**, clique em **Mostrar configurações de firewall**</span><span class="sxs-lookup"><span data-stu-id="60fe2-139">In the **Overview** section, click **Show firewall settings**</span></span>

   ![Mostrar configurações de firewall][SQL06]

1. <span data-ttu-id="60fe2-141">Na seção **Firewalls e redes virtuais**, crie uma nova regra especificando um nome exclusivo para a regra, insira o intervalo de endereços IP que precisarão acessar seu banco de dados e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="60fe2-141">In the **Firewalls and virtual networks** section, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Definir configurações de firewall][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="60fe2-143">Recuperar a cadeia de conexão para seu SQL Server usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60fe2-143">Retrieve the connection string for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="60fe2-144">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="60fe2-144">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="60fe2-145">Clique em **Todos os Recursos** e, em seguida, clique no banco de dados SQL que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="60fe2-145">Click **All Resources**, then click the SQL database you just created.</span></span>

   ![Escolher o banco de dados SQL][SQL08]

1. <span data-ttu-id="60fe2-147">Clique em **Cadeias de conexão**, clique em **JDBC** e copie o valor no campo de texto JDBC.</span><span class="sxs-lookup"><span data-stu-id="60fe2-147">Click **Connection strings**, then click **JDBC**, and copy the value in the JDBC text field.</span></span>

   ![Recuperar sua cadeia de conexão JDBC][SQL09]

## <a name="configure-the-sample-application"></a><span data-ttu-id="60fe2-149">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="60fe2-149">Configure the sample application</span></span>

1. <span data-ttu-id="60fe2-150">Abra um shell de comando e clone o projeto de exemplo usando um comando git como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="60fe2-150">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="60fe2-151">Localize o arquivo *application.properties* no diretório *recursos* do seu projeto de exemplo ou crie o arquivo se ele ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="60fe2-151">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="60fe2-152">Abra o arquivo *application.properties* em um editor de texto e adicione ou configure as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:</span><span class="sxs-lookup"><span data-stu-id="60fe2-152">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   <span data-ttu-id="60fe2-153">Em que:</span><span class="sxs-lookup"><span data-stu-id="60fe2-153">Where:</span></span>

   | <span data-ttu-id="60fe2-154">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="60fe2-154">Parameter</span></span> | <span data-ttu-id="60fe2-155">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="60fe2-155">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="60fe2-156">Especifica a versão editada da cadeia de JDBC do SQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="60fe2-156">Specifies an edited version of your SQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="60fe2-157">Especifica o nome do administrador do SQL neste artigo com o nome abreviado do servidor anexado a ele.</span><span class="sxs-lookup"><span data-stu-id="60fe2-157">Specifies your SQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="60fe2-158">Especifica sua senha de administrador do SQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="60fe2-158">Specifies your SQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="60fe2-159">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="60fe2-159">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="60fe2-160">Empacotar e testar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="60fe2-160">Package and test the sample application</span></span> 

1. <span data-ttu-id="60fe2-161">Crie seu aplicativo de exemplo com o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="60fe2-161">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P sql
   ```

1. <span data-ttu-id="60fe2-162">Inicie o aplicativo de exemplo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="60fe2-162">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="60fe2-163">Crie novos registros usando `curl` em um prompt de comando como nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="60fe2-163">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="60fe2-164">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="60fe2-164">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="60fe2-165">Recupere todos os registros existentes usando `curl` em um prompt de comando como nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="60fe2-165">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="60fe2-166">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="60fe2-166">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="60fe2-167">Resumo</span><span class="sxs-lookup"><span data-stu-id="60fe2-167">Summary</span></span>

<span data-ttu-id="60fe2-168">Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações em um banco de dados SQL do Azure usando o JPA.</span><span class="sxs-lookup"><span data-stu-id="60fe2-168">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure SQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60fe2-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60fe2-169">Next steps</span></span>

<span data-ttu-id="60fe2-170">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="60fe2-170">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60fe2-171">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="60fe2-171">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="60fe2-172">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="60fe2-172">Additional Resources</span></span>

<span data-ttu-id="60fe2-173">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="60fe2-173">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[SQL01]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-09.png
