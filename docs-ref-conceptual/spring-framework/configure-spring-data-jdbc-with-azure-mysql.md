---
title: Como usar o Spring Data JDBC com o MySQL do Azure
description: Saiba como usar o Spring Data JDBC com um Banco de Dados MySQL do Azure.
services: mysql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: mysql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 5ec89194c72cef81c79d21382e41b33ebe91d3d0
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991958"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-mysql"></a><span data-ttu-id="6ee39-103">Como usar o Spring Data JDBC com o MySQL do Azure</span><span class="sxs-lookup"><span data-stu-id="6ee39-103">How to use Spring Data JDBC with Azure MySQL</span></span>

## <a name="overview"></a><span data-ttu-id="6ee39-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6ee39-104">Overview</span></span>

<span data-ttu-id="6ee39-105">Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações em um [banco de dados MySQL do Azure](https://www.mysql.com/) usando [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span><span class="sxs-lookup"><span data-stu-id="6ee39-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [MySQL](https://www.mysql.com/) database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ee39-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ee39-106">Prerequisites</span></span>

<span data-ttu-id="6ee39-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="6ee39-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="6ee39-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="6ee39-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="6ee39-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="6ee39-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="6ee39-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="6ee39-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="6ee39-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6ee39-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="6ee39-112">[Curl](https://curl.haxx.se/) ou utilitário HTTP semelhante para testar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="6ee39-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="6ee39-113">O utilitário de linha de comando [mysql](https://dev.mysql.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6ee39-113">The [mysql](https://dev.mysql.com/downloads/) command-line utility.</span></span>
* <span data-ttu-id="6ee39-114">Um cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="6ee39-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-mysql-database-for-azure"></a><span data-ttu-id="6ee39-115">Criar um banco de dados MySQL para o Azure</span><span class="sxs-lookup"><span data-stu-id="6ee39-115">Create a MySQL database for Azure</span></span>

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="6ee39-116">Criar um servidor de banco de dados MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6ee39-116">Create a MySQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6ee39-117">Veja informações mais detalhadas sobre a criação de bancos de dados MySQL em [Criar um servidor de Banco de Dados do Azure para MySQL usando o portal do Azure](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="6ee39-117">You can read more detailed information about creating MySQL databases in [Create an Azure Database for MySQL server by using the Azure portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span></span>

1. <span data-ttu-id="6ee39-118">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="6ee39-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="6ee39-119">Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Banco de Dados do Azure para MySQL**.</span><span class="sxs-lookup"><span data-stu-id="6ee39-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for MySQL**.</span></span>

   ![Criar um banco de dados MySQL][MYSQL01]

1. <span data-ttu-id="6ee39-121">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="6ee39-121">Enter the following information:</span></span>

   - <span data-ttu-id="6ee39-122">**Nome do servidor**: Escolha um nome exclusivo para o servidor MySQL. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoysmysql.mysql.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="6ee39-122">**Server name**: Choose a unique name for your MySQL server; this will be used to create a fully-qualified domain name like *wingtiptoysmysql.mysql.database.azure.com*.</span></span>
   - <span data-ttu-id="6ee39-123">**Assinatura**: especifique a assinatura do Azure para usar.</span><span class="sxs-lookup"><span data-stu-id="6ee39-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="6ee39-124">**Grupo de recursos**: especifique se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="6ee39-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="6ee39-125">**Selecionar fonte**: no caso deste tutorial, escolha `Blank` para criar um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6ee39-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="6ee39-126">**Logon de administrador do servidor**: especifique o nome do administrador do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6ee39-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="6ee39-127">**Senha** e **Confirmar senha**: especifique a senha para o administrador do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6ee39-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="6ee39-128">**Localização**: especifique a região geográfica mais próxima do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6ee39-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="6ee39-129">**Versão**: especifique a versão mais atualizada do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6ee39-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="6ee39-130">**Tipo de preço**: no caso deste tutorial, especifica o tipo de preço menos caro.</span><span class="sxs-lookup"><span data-stu-id="6ee39-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Criar as propriedades do banco de dados MySQL][MYSQL02]

1. <span data-ttu-id="6ee39-132">Após inserir todas as informações acima, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6ee39-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="6ee39-133">Configurar uma regra de firewall para o servidor de banco de dados MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6ee39-133">Configure a firewall rule for your MySQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="6ee39-134">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="6ee39-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="6ee39-135">Clique em **Todos os Recursos** e, em seguida, clique no banco de dados MySQL que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="6ee39-135">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Escolher seu banco de dados MySQL][MYSQL03]

1. <span data-ttu-id="6ee39-137">Clique em **Segurança de conexão** e, nas **Regras de firewall** , crie uma nova regra especificando um nome exclusivo para a regra e, em seguida, insira o intervalo de endereços IP que precisarão acessar seu banco de dados e clique em **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6ee39-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configurar a segurança da conexão][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a><span data-ttu-id="6ee39-139">Recuperar a cadeia de conexão para seu servidor MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6ee39-139">Retrieve the connection string for your MySQL server using the Azure Portal</span></span>

1. <span data-ttu-id="6ee39-140">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="6ee39-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="6ee39-141">Clique em **Todos os Recursos** e, em seguida, clique no banco de dados MySQL que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="6ee39-141">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Escolher seu banco de dados MySQL][MYSQL03]

1. <span data-ttu-id="6ee39-143">Clique em **Cadeias de conexão** e copie o valor no campo de texto **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="6ee39-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Recuperar sua cadeia de conexão JDBC][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a><span data-ttu-id="6ee39-145">Criar banco de dados MySQL usando o utilitário de linha de comando `mysql`</span><span class="sxs-lookup"><span data-stu-id="6ee39-145">Create MySQL database using the `mysql` command-line utility</span></span>

1. <span data-ttu-id="6ee39-146">Abra um shell de comando e conecte-se ao servidor MySQL digitando um comando `mysql` como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-146">Open a command shell and connect to your MySQL server by entering a `mysql` command like the following example:</span></span>

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   <span data-ttu-id="6ee39-147">Em que:</span><span class="sxs-lookup"><span data-stu-id="6ee39-147">Where:</span></span>

   | <span data-ttu-id="6ee39-148">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6ee39-148">Parameter</span></span> | <span data-ttu-id="6ee39-149">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="6ee39-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="6ee39-150">Especifica o nome totalmente qualificado do servidor MySQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6ee39-150">Specifies your fully qualified MySQL server name from earlier in this article.</span></span> |
   | `user` | <span data-ttu-id="6ee39-151">Especifica o administrador do MySQL e o nome abreviado do servidor neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6ee39-151">Specifies your MySQL administrator and shortened server name from earlier in this article.</span></span> |
   | `p` | <span data-ttu-id="6ee39-152">Especifica uma espera até que uma senha seja solicitada.</span><span class="sxs-lookup"><span data-stu-id="6ee39-152">Specifies to wait until prompted for a password.</span></span> |

   <span data-ttu-id="6ee39-153">O servidor MySQL deve responder com uma exibição como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-153">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 64552
   Server version: 5.6.39.0 MySQL Community Server (GPL)
   
   Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   
   mysql>
   ```

1. <span data-ttu-id="6ee39-154">Crie um banco de dados denominado *mysqldb* inserindo um comando `mysql`, como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-154">Create a database named *mysqldb* by entering a `mysql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   <span data-ttu-id="6ee39-155">O servidor MySQL deve responder com uma exibição como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-155">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. <span data-ttu-id="6ee39-156">OPCIONAL: verifique se seu banco de dados foi criado inserindo um comando `mysql` como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-156">OPTIONAL: You can verify that your database was created by entering a `mysql` command like the following example:</span></span>

   ```SQL
   SHOW DATABASES;
   ```

   <span data-ttu-id="6ee39-157">O servidor MySQL deve responder com uma exibição como o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-157">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   +--------------------+
   | Database           |
   +--------------------+
   | information_schema |
   | mysql              |
   | mysqldb            |
   | performance_schema |
   | sys                |
   +--------------------+
   ```

1. <span data-ttu-id="6ee39-158">Insira `\q` para sair do utilitário `mysql`.</span><span class="sxs-lookup"><span data-stu-id="6ee39-158">Enter `\q` to exit the `mysql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="6ee39-159">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="6ee39-159">Configure the sample application</span></span>

1. <span data-ttu-id="6ee39-160">Abra um shell de comando e clone o projeto de exemplo usando um comando git como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="6ee39-161">Localize o arquivo *application.properties* no diretório *recursos* do seu projeto de exemplo ou crie o arquivo se ele ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="6ee39-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="6ee39-162">Abra o arquivo *application.properties* em um editor de texto e adicione ou configure as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:</span><span class="sxs-lookup"><span data-stu-id="6ee39-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false&serverTimezone=UTC
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   <span data-ttu-id="6ee39-163">Em que:</span><span class="sxs-lookup"><span data-stu-id="6ee39-163">Where:</span></span>

   | <span data-ttu-id="6ee39-164">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6ee39-164">Parameter</span></span> | <span data-ttu-id="6ee39-165">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="6ee39-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="6ee39-166">Especifica sua cadeia de JDBC do MySQL neste artigo, com o fuso horário incluído.</span><span class="sxs-lookup"><span data-stu-id="6ee39-166">Specifies your MySQL JDBC string from earlier in this article, with the time zone added.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="6ee39-167">Especifica o nome do administrador do MySQL neste artigo com o nome abreviado do servidor anexado a ele.</span><span class="sxs-lookup"><span data-stu-id="6ee39-167">Specifies your MySQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="6ee39-168">Especifica sua senha de administrador do MySQL neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6ee39-168">Specifies your MySQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="6ee39-169">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="6ee39-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="6ee39-170">Empacotar e testar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="6ee39-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="6ee39-171">Crie seu aplicativo de exemplo com o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6ee39-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P mysql
   ```

1. <span data-ttu-id="6ee39-172">Inicie o aplicativo de exemplo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6ee39-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="6ee39-173">Crie novos registros usando `curl` em um prompt de comando como nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="6ee39-174">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6ee39-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="6ee39-175">Recupere todos os registros existentes usando `curl` em um prompt de comando como nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ee39-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="6ee39-176">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6ee39-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="6ee39-177">Resumo</span><span class="sxs-lookup"><span data-stu-id="6ee39-177">Summary</span></span>

<span data-ttu-id="6ee39-178">Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações em um banco de dados do Azure MySQL usando o JDBC.</span><span class="sxs-lookup"><span data-stu-id="6ee39-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure MySQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ee39-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ee39-179">Next steps</span></span>

<span data-ttu-id="6ee39-180">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ee39-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ee39-181">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="6ee39-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="6ee39-182">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6ee39-182">Additional Resources</span></span>

<span data-ttu-id="6ee39-183">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="6ee39-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[MYSQL01]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-05.png
