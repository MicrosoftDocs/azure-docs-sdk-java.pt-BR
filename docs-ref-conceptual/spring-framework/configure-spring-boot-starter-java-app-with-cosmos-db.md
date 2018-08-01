---
title: Como usar o Inicializador do Spring Boot com a API SQL do Azure Cosmos DB
description: Saiba como configurar um aplicativo criado com o Inicializador do Spring Boot com a API SQL do Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;yungez;kevinzha
ms.date: 07/05/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 3306f3ef66ec1b53ab004765b8fb7aef04de9077
ms.sourcegitcommit: 1ff4654193404415841252a130b87a8b53b7c6d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39235970"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="5e6f5-103">Como usar o Inicializador do Spring Boot com a API SQL do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5e6f5-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="5e6f5-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5e6f5-104">Overview</span></span>

<span data-ttu-id="5e6f5-105">O Azure Cosmos DB é um serviço de banco de dados distribuído globalmente que permite aos desenvolvedores trabalhar com os dados usando várias APIs padrão, como as APIs SQL, MongoDB, Graph e de Tabela.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="5e6f5-106">O Inicializador do Spring Boot da Microsoft permite aos desenvolvedores usar aplicativos Spring Boot que se integram facilmente ao Azure Cosmos DB por meio da API SQL.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="5e6f5-107">Este artigo demonstra como criar um Azure Cosmos DB usando o Portal do Azure, então, usar o **[Spring Initializr]** para criar um aplicativo java personalizado e adicionar a funcionalidade do Inicializador do Spring Boot ao seu aplicativo personalizado para armazenar e recuperar dados em seu Azure Cosmos DB usando a API SQL.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e6f5-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5e6f5-108">Prerequisites</span></span>

<span data-ttu-id="5e6f5-109">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="5e6f5-110">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="5e6f5-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="5e6f5-111">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-111">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="5e6f5-112">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-112">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="5e6f5-113">Criar um Azure Cosmos DB usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5e6f5-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="5e6f5-114">Navegue até o Portal do Azure em <https://portal.azure.com/> e clique em **+Criar um recurso**.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Portal do Azure][AZ01]

1. <span data-ttu-id="5e6f5-116">Clique em **Bancos de Dados** e, em seguida, clique em **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portal do Azure][AZ02]

1. <span data-ttu-id="5e6f5-118">Na página **Azure Cosmos DB**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="5e6f5-119">Insira uma **ID** exclusiva, que você usará como o URI para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-119">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="5e6f5-120">Por exemplo: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-120">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="5e6f5-121">Escolha **SQL** para a API.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-121">Choose **SQL** for the API.</span></span>
   * <span data-ttu-id="5e6f5-122">Escolha a **Assinatura** você deseja usar para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-122">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="5e6f5-123">Especifique se deseja criar um novo **Grupo de recursos** para seu banco de dados ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-123">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="5e6f5-124">Especifique o **Local** para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-124">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="5e6f5-125">Quando você tiver especificado essas opções, clique em **Criar** para criar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-125">When you have specified these options, click **Create** to create your database.</span></span>

   ![Portal do Azure][AZ03]

1. <span data-ttu-id="5e6f5-127">Quando seu banco de dados for criado, ele será listado no seu **Painel** do Azure, bem como nas páginas **Todos os Recursos** e **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="5e6f5-128">Você pode clicar no banco de dados em qualquer um desses locais para abrir a página de propriedades do seu cache.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Portal do Azure][AZ04]

1. <span data-ttu-id="5e6f5-130">Quando a página de propriedades para o banco de dados for exibida, clique em **Chaves de acesso** e copie o URI e as chaves de acesso para seu banco de dados. Você usará esses valores em seu aplicativo Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-130">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portal do Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="5e6f5-132">Criar um aplicativo Spring Boot simples com o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="5e6f5-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="5e6f5-133">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="5e6f5-134">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para seu aplicativo, especifique a versão do **Spring Boot** e, em seguida, clique no botão para **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-134">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version, and then click the button to **Generate Project**.</span></span>

   > [!IMPORTANT]
   >
   > <span data-ttu-id="5e6f5-135">Houve várias alterações da falha para as APIs na versão do Spring Boot 2.0.n. Como resultado, você precisará de uma das versões 1.5.n do Spring Boot para concluir as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-135">There were several breaking changes to the APIs in Spring Boot version 2.0.n, as a result, you will need to one of the Spring Boot 1.5.n versions to complete the steps in this tutorial.</span></span>
   >

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="5e6f5-137">O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote; por exemplo: *com.example.wintiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-137">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="5e6f5-138">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-138">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixe o projeto personalizado do Spring Boot][SI02]

1. <span data-ttu-id="5e6f5-140">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-140">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Arquivos de projeto Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="5e6f5-142">Configure seu aplicativo Spring Boot para usar o Iniciador do Azure Spring Boot</span><span class="sxs-lookup"><span data-stu-id="5e6f5-142">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="5e6f5-143">Localize o arquivo *pom.xml* no diretório do seu aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-143">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="5e6f5-144">-ou-</span><span class="sxs-lookup"><span data-stu-id="5e6f5-144">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Salve o arquivo pom.xml][PM01]

1. <span data-ttu-id="5e6f5-146">Abra o arquivo *pom.xml* em um editor de texto e adicione as seguintes linhas à lista de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-146">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Edição do arquivo pom.xml][PM02]

1. <span data-ttu-id="5e6f5-148">Verifique se a versão do Spring Boot é uma das versões 1.5.n; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-148">Verify that the Spring Boot version is one of the 1.5.n versions; for example:</span></span>

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>1.5.14.RELEASE</version>
      <relativePath/>
   </parent>
   ```

1. <span data-ttu-id="5e6f5-149">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-149">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="5e6f5-150">Configure seu aplicativo Spring Boot para usar seu Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5e6f5-150">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="5e6f5-151">Localize o arquivo *application.properties* no diretório *recursos* do seu aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-151">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="5e6f5-152">-ou-</span><span class="sxs-lookup"><span data-stu-id="5e6f5-152">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Localize o arquivo application.properties][RE01]

1. <span data-ttu-id="5e6f5-154">Abra o arquivo *application.properties* em um editor de texto e adicione as seguintes linhas ao arquivo, então substitua os valores de exemplo pelas propriedades adequadas para seu banco de dados:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-154">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Edição do arquivo application.properties][RE02]

1. <span data-ttu-id="5e6f5-156">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-156">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="5e6f5-157">Adicione o código de exemplo para implementar a funcionalidade básica de banco de dados</span><span class="sxs-lookup"><span data-stu-id="5e6f5-157">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="5e6f5-158">Nesta seção, você criará duas classes Java para armazenamento de dados de usuário e, em seguida, modificará sua classe de aplicativo principal para criar uma instância da classe de usuário e salvá-la no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-158">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="5e6f5-159">Definir uma classe básica para armazenar dados do usuário</span><span class="sxs-lookup"><span data-stu-id="5e6f5-159">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="5e6f5-160">Criar um novo arquivo denominado *User.java* no mesmo diretório que o arquivo Java do seu aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-160">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="5e6f5-161">Abra o arquivo *User.java* em um editor de texto e adicione as seguintes linhas ao arquivo para definir uma classe de usuário genérica que armazena e recupera valores no seu banco de dados:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-161">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   // Define a generic User class.
   public class User {
      private String id;
      private String firstName;
      private String lastName;
   
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }
   
      public void setId(String id) {
         this.id = id;
      }
   
      public String getFirstName() {
         return firstName;
      }
   
      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }
   
      public String getLastName() {
         return lastName;
      }
   
      public void setLastName(String lastName) {
         this.lastName = lastName;
      }
   
      @Override
      public String toString() {
         return String.format("User: %s %s %s", id, firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="5e6f5-162">Salve e feche o arquivo *User.java*.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-162">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="5e6f5-163">Defina uma interface de repositório de dados</span><span class="sxs-lookup"><span data-stu-id="5e6f5-163">Define a data repository interface</span></span>

1. <span data-ttu-id="5e6f5-164">Criar um novo arquivo denominado *UserRepository.java* no mesmo diretório que o arquivo Java do seu aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-164">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="5e6f5-165">Abra o arquivo *UserRepository.java* em um editor de texto e adicione as seguintes linhas ao arquivo para definir uma interface de repositório do usuário que estende a interface do repositório do DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-165">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. <span data-ttu-id="5e6f5-166">Salve e feche o arquivo *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-166">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="5e6f5-167">Modificar a classe principal do aplicativo</span><span class="sxs-lookup"><span data-stu-id="5e6f5-167">Modify the main application class</span></span>

1. <span data-ttu-id="5e6f5-168">Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-168">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="5e6f5-169">-ou-</span><span class="sxs-lookup"><span data-stu-id="5e6f5-169">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Localize o arquivo Java do aplicativo][JV01]

1. <span data-ttu-id="5e6f5-171">Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-171">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;
   
   // These imports are only used to create an ID for this example.
   import java.util.Date;
   import java.text.SimpleDateFormat;
   
   @SpringBootApplication
   public class wingtiptoysdataApplication implements CommandLineRunner {
   
      @Autowired
      private UserRepository repository;
   
      public static void main(String[] args) {
         // Execute the command line runner.
         SpringApplication.run(wingtiptoysdataApplication.class, args);
      }
   
      public void run(String... args) throws Exception {
         // Create a simple date/time ID.
         SimpleDateFormat userId = new SimpleDateFormat("yyyyMMddHHmmssSSS");
         Date currentDate = new Date();
   
         // Create a new User class.
         final User testUser = new User(userId.format(currentDate), "Gena", "Soto");
   
         // For this example, remove all of the existing records.
         repository.deleteAll();
   
         // Save the User class to the Azure database.
         repository.save(testUser);
         
         // Retrieve the database record for the User class you just saved by ID.
         final User result = repository.findOne(testUser.getId());
   
         // Display the results of the database record retrieval.
         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="5e6f5-172">Salve e feche o arquivo Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-172">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="5e6f5-173">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="5e6f5-173">Build and test your app</span></span>

1. <span data-ttu-id="5e6f5-174">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-174">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="5e6f5-175">-ou-</span><span class="sxs-lookup"><span data-stu-id="5e6f5-175">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="5e6f5-176">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-176">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="5e6f5-177">Seu aplicativo exibirá várias mensagens de tempo de execução e você deverá ver a mensagem `User: testFirstName testLastName` exibida para indicar valores foram armazenados e recuperados com êxito do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-177">Your application will display several runtime messages, and you should see the message `User: testFirstName testLastName` displayed to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Saída bem-sucedida do aplicativo][JV02]

1. <span data-ttu-id="5e6f5-179">OPCIONAL: você pode usar o portal do Azure para exibir o conteúdo do Azure Cosmos DB na página de propriedades do seu banco de dados. Basta clicar em **Data Explorer** e selecionar um item na lista para exibir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-179">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Como usar o Gerenciador de Documentos para exibir seus dados][JV03]

## <a name="next-steps"></a><span data-ttu-id="5e6f5-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e6f5-181">Next steps</span></span>

<span data-ttu-id="5e6f5-182">Para obter mais informações sobre como usar o Azure Cosmos DB e Java, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-182">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="5e6f5-183">[Documentação do Azure Cosmos DB].</span><span class="sxs-lookup"><span data-stu-id="5e6f5-183">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="5e6f5-184">[Azure Cosmos DB: Criar um banco de dados de documento usando o Java e o Portal do Azure][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="5e6f5-184">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="5e6f5-185">[Spring Data para a API do SQL do Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="5e6f5-185">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="5e6f5-186">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="5e6f5-186">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="5e6f5-187">[Inicialização do Document DB do Spring Boot para Azure]</span><span class="sxs-lookup"><span data-stu-id="5e6f5-187">[Spring Boot Document DB Starter for Azure]</span></span>

* [<span data-ttu-id="5e6f5-188">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="5e6f5-188">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="5e6f5-189">Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="5e6f5-189">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="5e6f5-190">Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="5e6f5-190">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="5e6f5-191">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-191">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="5e6f5-192">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-192">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="5e6f5-193">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-193">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="5e6f5-194">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="5e6f5-194">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentação do Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data para a API do SQL do Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Inicialização do Document DB do Spring Boot para Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[Spring Boot Document DB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Benefícios do assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV03.png
