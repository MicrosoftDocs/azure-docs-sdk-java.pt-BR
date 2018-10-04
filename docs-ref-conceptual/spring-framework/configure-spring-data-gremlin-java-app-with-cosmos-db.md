---
title: Como usar o Iniciador do Spring Data Gremlin com a API SQL do Azure Cosmos DB
description: Saiba como configurar um aplicativo criado com o Inicializador do Spring Boot com a API SQL do Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.date: 08/20/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 561dba84b0c1662fa6575e1816ff3dd2f0c6093b
ms.sourcegitcommit: bb7286fad75a2bb43e6ce1a8f1b09e701147c9f9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047163"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="b9d3a-103">Como usar o Iniciador do Spring Data Gremlin com a API SQL do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b9d3a-103">How to use the Spring Data Gremlin Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="b9d3a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b9d3a-104">Overview</span></span>

<span data-ttu-id="b9d3a-105">O Iniciador do Spring Data Gremlin fornece suporte ao Spring Data para a linguagem de consulta Gremlin do Apache, que os desenvolvedores podem usar com qualquer armazenamento de dados compatíveis com Gremlin.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-105">The Spring Data Gremlin Starter provides Spring Data support for the Gremlin query language from Apache, which developers can use with any Gremlin-compatible data store.</span></span>

<span data-ttu-id="b9d3a-106">Este artigo demonstra como criar um Azure Cosmos DB usando o portal do Azure para uso com a API do Gremlin. Depois, como usar o **[Spring Initializr]** para criar um aplicativo Java personalizado e, em seguida, como adicionar a funcionalidade de Iniciador do Spring Data Gremlin ao seu aplicativo personalizado para armazenar e recuperar dados de seu Azure Cosmos DB usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-106">This article demonstrates creating an Azure Cosmos DB by using the Azure portal for use with Gremlin API, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Data Gremlin Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Gremlin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9d3a-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9d3a-107">Prerequisites</span></span>

<span data-ttu-id="b9d3a-108">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-108">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="b9d3a-109">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="b9d3a-109">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b9d3a-110">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-110">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="b9d3a-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="b9d3a-112">É necessário o Spring Boot versão 2.0 ou posterior para concluir as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a><span data-ttu-id="b9d3a-113">Criar um Azure Cosmos DB usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9d3a-113">Create an Azure Cosmos DB using the Azure portal</span></span>

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a><span data-ttu-id="b9d3a-114">Criar seu Azure Cosmos DB para uso com a API do Gremlin</span><span class="sxs-lookup"><span data-stu-id="b9d3a-114">Create your Azure Cosmos Database for use with Gremlin API</span></span>

1. <span data-ttu-id="b9d3a-115">Navegue até o Portal do Azure em <https://portal.azure.com/> e clique em **+Criar um recurso**.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Criar um recurso][AZ01]

1. <span data-ttu-id="b9d3a-117">Clique em **Bancos de Dados** e, em seguida, clique em **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Criar Azure Cosmos DB][AZ02]

1. <span data-ttu-id="b9d3a-119">Na página **Azure Cosmos DB**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="b9d3a-120">Insira uma **ID** exclusiva, que você usará como parte do URI do Gremlin para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-120">Enter a unique **ID**, which you will use as part of the Gremlin URI for your database.</span></span> <span data-ttu-id="b9d3a-121">Por exemplo: se você inseriu **wingtiptoysdata** para a **ID**, o URI do Gremlin deve ser *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-121">For example: if you entered **wingtiptoysdata** for the **ID**, the Gremlin URI would be *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span></span>
   * <span data-ttu-id="b9d3a-122">Escolha **Gremlin (Grafo)** para a API.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-122">Choose **Gremlin (Graph)** for the API.</span></span>
   * <span data-ttu-id="b9d3a-123">Escolha a **Assinatura** você deseja usar para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="b9d3a-124">Especifique se deseja criar um novo **Grupo de recursos** para seu banco de dados ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="b9d3a-125">Especifique o **Local** para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="b9d3a-126">Quando você tiver especificado essas opções, clique em **Criar** para criar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Especificar as opções do Azure Cosmos DB][AZ03]

1. <span data-ttu-id="b9d3a-128">Quando seu banco de dados for criado, ele será listado no seu **Painel** do Azure, bem como nas páginas **Todos os Recursos** e **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="b9d3a-129">Você pode clicar no banco de dados em qualquer um desses locais para abrir a página de propriedades do seu cache.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Todos os Recursos][AZ04]

1. <span data-ttu-id="b9d3a-131">Quando a página de propriedades para o banco de dados for exibida, clique em **Chaves de acesso** e copie o URI e as chaves de acesso para seu banco de dados. Você usará esses valores em seu aplicativo Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Chaves de acesso][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a><span data-ttu-id="b9d3a-133">Adicionar um grafo ao seu Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b9d3a-133">Add a graph to your Azure Cosmos Database</span></span>

1. <span data-ttu-id="b9d3a-134">Clique em **Data Explorer** e em **Novo Graph**.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-134">Click **Data Explorer**, and then click **New Graph**.</span></span>

   ![Novo grafo][AZ06]

1. <span data-ttu-id="b9d3a-136">Quando a página **Adicionar Graph** for exibida, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-136">When the **Add Graph** is displayed, enter the following information:</span></span>

   * <span data-ttu-id="b9d3a-137">Especifique uma **ID de banco de dados** exclusiva para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-137">Specify a unique **Database id** for your database.</span></span>
   * <span data-ttu-id="b9d3a-138">Especifique uma **ID do Graph** exclusiva para seu grafo.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-138">Specify a unique **Graph id** for your graph.</span></span>
   * <span data-ttu-id="b9d3a-139">Você pode optar por especificar sua **Capacidade de armazenamento** ou pode aceitar a opção padrão.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-139">You can choose to specify your **Storage capacity**, or you can accept the default.</span></span>
   * <span data-ttu-id="b9d3a-140">Especifique sua **Produtividade**, e para este exemplo, você pode escolher 400 Unidades de Solicitação (RUs).</span><span class="sxs-lookup"><span data-stu-id="b9d3a-140">Specify your **Throughput**, and for this example you can choose 400 Request Units (RUs).</span></span>
   
   <span data-ttu-id="b9d3a-141">Quando você tiver especificado essas opções, clique em **OK** para criar o grafo.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-141">When you have specified these options, click **OK** to create your graph.</span></span>

   ![Adicionar Graph][AZ07]

1. <span data-ttu-id="b9d3a-143">Após a criação do grafo, você pode usar o **Data Explorer** para visualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-143">After your graph has been created, you can use the **Data Explorer** to view it.</span></span>

   ![Exibição das propriedades do Graph][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="b9d3a-145">Criar um aplicativo Spring Boot simples com o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="b9d3a-145">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="b9d3a-146">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-146">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="b9d3a-147">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para seu aplicativo, especifique a versão do **Spring Boot** com uma versão que seja igual ou superior a 2.0 e, em seguida, clique em **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-147">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version with a version that is equal to or greater than 2.0, and then click **Generate Project**.</span></span>

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="b9d3a-149">O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote; por exemplo: \*com.example.wintiptoysdata.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-149">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: \*com.example.wintiptoysdata.</span></span>
   >

1. <span data-ttu-id="b9d3a-150">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-150">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixe o projeto personalizado do Spring Boot][SI02]

1. <span data-ttu-id="b9d3a-152">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-152">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Arquivos de projeto Spring Boot personalizados][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a><span data-ttu-id="b9d3a-154">Configure seu aplicativo Spring Boot para usar o Iniciador do Spring Data Gremlin</span><span class="sxs-lookup"><span data-stu-id="b9d3a-154">Configure your Spring Boot app to use the Spring Data Gremlin Starter</span></span>

1. <span data-ttu-id="b9d3a-155">Localize o arquivo *pom.xml* no diretório do seu aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-155">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="b9d3a-156">-ou-</span><span class="sxs-lookup"><span data-stu-id="b9d3a-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Salve o arquivo pom.xml][PM01]

1. <span data-ttu-id="b9d3a-158">Abra o arquivo *pom.xml* em um editor de texto e adicione o Iniciador do Spring Data Gremlin à lista de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-158">Open the *pom.xml* file in a text editor, and add the Spring Data Gremlin Starter to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Edição do arquivo pom.xml][PM02]

1. <span data-ttu-id="b9d3a-160">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-160">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="b9d3a-161">Configure seu aplicativo Spring Boot para usar seu Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b9d3a-161">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="b9d3a-162">Localize o diretório *resources* do seu aplicativo, e crie um novo arquivo chamado *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-162">Locate the *resources* directory of your app, and create a new file named *application.yml*.</span></span> <span data-ttu-id="b9d3a-163">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="b9d3a-163">For example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   <span data-ttu-id="b9d3a-164">-ou-</span><span class="sxs-lookup"><span data-stu-id="b9d3a-164">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Criar o arquivo application.yml][RE01]

1. <span data-ttu-id="b9d3a-166">Abra o arquivo *application.yml* em um editor de texto e adicione as seguintes linhas ao arquivo, e substitua os valores de exemplo pelas propriedades adequadas para o seu banco de dados:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-166">Open the *application.yml* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   
   <span data-ttu-id="b9d3a-167">Em que:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-167">Where:</span></span>
   
   | <span data-ttu-id="b9d3a-168">Campo</span><span class="sxs-lookup"><span data-stu-id="b9d3a-168">Field</span></span> | <span data-ttu-id="b9d3a-169">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="b9d3a-169">Description</span></span> |
   |---|---|
   | `endpoint` | <span data-ttu-id="b9d3a-170">Especifica o URI do Gremlin para o seu banco de dados, que é derivado da **ID** exclusiva que você especificou ao criar seu Azure Cosmos DB anteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-170">Specifies the Gremlin URI for your database, which is derived from the unique **ID** that you specified when you created your Azure Cosmos DB earlier in this tutorial.</span></span> |
   | `port` | <span data-ttu-id="b9d3a-171">Especifica a porta TCP/IP, que deve ser **443** para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-171">Specifies the TCP/IP port, which should be **443** for HTTPS.</span></span> |
   | `username` | <span data-ttu-id="b9d3a-172">Especifica a **ID de banco de dados** e a **ID do Graph** exclusivas usadas ao adicionar o grafo anteriormente. Essa opção deve ser inserida usando a seguinte sintaxe: “/dbs/**{ID do banco de dados}**/colls/**{Id do Graph}**”.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-172">Specifies the unique **Database id** and **Graph id** that you used when you added your graph earlier in this tutorial; this must be entered using the following syntax: "/dbs/**{Database id}**/colls/**{Graph id}**".</span></span> |
   | `password` | <span data-ttu-id="b9d3a-173">Especifica a **Chave de acesso** primária ou secundária copiada anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-173">Specifies either the primary or secondary **Access key** that you copied earlier in this tutorial.</span></span> |
   | `telemetryAllowed` | <span data-ttu-id="b9d3a-174">Especifique **true** se você quiser habilitar a telemetria; caso contrário, **false**.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-174">Specify **true** if you want to enable telemetry; otherwise, **false**.</span></span>

1. <span data-ttu-id="b9d3a-175">Salve e feche o arquivo *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-175">Save and close the *application.yml* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="b9d3a-176">Adicione o código de exemplo para implementar a funcionalidade básica de banco de dados</span><span class="sxs-lookup"><span data-stu-id="b9d3a-176">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="b9d3a-177">Nesta seção, você cria as classes Java necessárias para armazenar dados em seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-177">In this section, you create the necessary Java classes for storing data in your database.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="b9d3a-178">Modificar a classe principal do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b9d3a-178">Modify the main application class</span></span>

1. <span data-ttu-id="b9d3a-179">Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-179">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="b9d3a-180">-ou-</span><span class="sxs-lookup"><span data-stu-id="b9d3a-180">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Localize o arquivo Java do aplicativo][JV01]

1. <span data-ttu-id="b9d3a-182">Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-182">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.example.wingtiptoysdata.domain.Network;
   import com.example.wingtiptoysdata.domain.Person;
   import com.example.wingtiptoysdata.domain.Relation;
   import com.example.wingtiptoysdata.repository.NetworkRepository;
   import com.example.wingtiptoysdata.repository.PersonRepository;
   import com.example.wingtiptoysdata.repository.RelationRepository;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import javax.annotation.PostConstruct;
   import javax.annotation.PreDestroy;
   
   @SpringBootApplication
   public class WingtiptoysdataApplication {
   
       // Define several person classes to store personal data.
       private final Person person1 = new Person("01", "Nellie Hughes", "23");
       private final Person person2 = new Person("02", "Delmar Alfred", "34");
       private final Person person3 = new Person("03", "Kelley Hunter", "45");
       private final Person person4 = new Person("04", "Roscoe Guerin", "56");
       private final Person person5 = new Person("05", "Gracie Chavez", "67");
   
       // Define relationship classes to define the relationships between some of the persons.
       private final Relation relation1 = new Relation("0102", "siblings", person1, person2);
       private final Relation relation2 = new Relation("0203", "coworkers", person2, person3);
       private final Relation relation3 = new Relation("0301", "parent", person3, person1);
       private final Relation relation4 = new Relation("0302", "parent", person3, person2);
       private final Relation relation5 = new Relation("0501", "grandparent", person5, person1);
       private final Relation relation6 = new Relation("0502", "grandparent", person5, person2);
   
       // Define the network.
       private final Network network = new Network();
   
       // Autowire the repositories and factory.
       @Autowired
       private PersonRepository personRepo;
       @Autowired
       private RelationRepository relationRepo;
       @Autowired
       private NetworkRepository networkRepo;
       @Autowired
       private GremlinFactory factory;
   
       // Run the Spring application and exit.
    public static void main(String[] args) {
           SpringApplication.run(WingtiptoysdataApplication.class, args);
           System.exit(0);
    }
   
       // Perform post-construct operations.    
       @PostConstruct
       public void setup() {
           // Delete any existing data from the database.
           this.networkRepo.deleteAll();
   
           // Add the relationship classes as edges.
           this.network.getEdges().add(this.relation1);
           this.network.getEdges().add(this.relation2);
           this.network.getEdges().add(this.relation3);
           this.network.getEdges().add(this.relation4);
           this.network.getEdges().add(this.relation5);
           this.network.getEdges().add(this.relation6);
   
           // Add the person classes as vertices.
           this.network.getVertexes().add(this.person1);
           this.network.getVertexes().add(this.person2);
           this.network.getVertexes().add(this.person3);
           this.network.getVertexes().add(this.person4);
           this.network.getVertexes().add(this.person5);
   
           // Save the network.
           this.networkRepo.save(this.network);
       }
   }
   ```

1. <span data-ttu-id="b9d3a-183">Salve e feche o arquivo Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-183">Save and close the main application Java file.</span></span>

### <a name="define-a-basic-class-for-storing-configuration-information"></a><span data-ttu-id="b9d3a-184">Defina uma classe básica para armazenar informações de configuração</span><span class="sxs-lookup"><span data-stu-id="b9d3a-184">Define a basic class for storing configuration information</span></span>

1. <span data-ttu-id="b9d3a-185">Crie uma pasta chamada *config* no diretório package do seu aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-185">Create a folder named *config* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   <span data-ttu-id="b9d3a-186">-ou-</span><span class="sxs-lookup"><span data-stu-id="b9d3a-186">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. <span data-ttu-id="b9d3a-187">Crie um novo arquivo Java chamado *UserRepositoryConfiguration.java* no diretório *config* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-187">Create a new Java file named *UserRepositoryConfiguration.java* in the *config* directory, then open the file in a text editor, and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.config;

   import com.microsoft.spring.data.gremlin.common.GremlinConfiguration;
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.microsoft.spring.data.gremlin.config.AbstractGremlinConfiguration;
   import com.microsoft.spring.data.gremlin.repository.config.EnableGremlinRepositories;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.context.properties.EnableConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.context.annotation.PropertySource;
   
   @Configuration
   @EnableGremlinRepositories(basePackages = "com.example.wingtiptoysdata.repository")
   @EnableConfigurationProperties(GremlinConfiguration.class)
   @PropertySource("classpath:application.yml")
   public class UserRepositoryConfiguration extends AbstractGremlinConfiguration {
   
       @Autowired
       private GremlinConfiguration config;
   
       @Override
       public GremlinConfiguration getGremlinConfiguration() {
           return this.config;
       }
   }
   ```

1. <span data-ttu-id="b9d3a-188">Salve e feche o arquivo *UserRepositoryConfiguration.java*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-188">Save and close the *UserRepositoryConfiguration.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a><span data-ttu-id="b9d3a-189">Defina um conjunto de classes que defina os elementos do banco de dados do seu grafo</span><span class="sxs-lookup"><span data-stu-id="b9d3a-189">Define a set of classes that define the elements of your graph database</span></span>

1. <span data-ttu-id="b9d3a-190">Crie uma pasta chamada *domain* no diretório package do seu aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-190">Create a folder named *domain* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   <span data-ttu-id="b9d3a-191">-ou-</span><span class="sxs-lookup"><span data-stu-id="b9d3a-191">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. <span data-ttu-id="b9d3a-192">Crie um novo arquivo Java chamado *Person.java* no diretório *domain* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-192">Create a new Java file named *Person.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Vertex;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Vertex
   @AllArgsConstructor
   @NoArgsConstructor
   public class Person {
   
       @Id
       private String id;
   
       private String name;
   
       private String age;
   }
   ```

1. <span data-ttu-id="b9d3a-193">Salve e feche o arquivo *Person.java*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-193">Save and close the *Person.java* file.</span></span>

1. <span data-ttu-id="b9d3a-194">Crie um novo arquivo Java chamado *Relation.java* no diretório *domain* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-194">Create a new Java file named *Relation.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Edge;
   import com.microsoft.spring.data.gremlin.annotation.EdgeFrom;
   import com.microsoft.spring.data.gremlin.annotation.EdgeTo;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Edge
   @AllArgsConstructor
   @NoArgsConstructor
   public class Relation {
   
       @Id
       private String id;
   
       private String name;
   
       @EdgeFrom
       private Person personFrom;
   
       @EdgeTo
       private Person personTo;
   }
   ```

1. <span data-ttu-id="b9d3a-195">Salve e feche o arquivo *Relation.java*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-195">Save and close the *Relation.java* file.</span></span>

1. <span data-ttu-id="b9d3a-196">Crie um novo arquivo Java chamado *Network.java* no diretório *domain* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-196">Create a new Java file named *Network.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.EdgeSet;
   import com.microsoft.spring.data.gremlin.annotation.Graph;
   import com.microsoft.spring.data.gremlin.annotation.VertexSet;
   import lombok.Getter;
   import org.springframework.data.annotation.Id;
   
   import java.util.ArrayList;
   import java.util.List;
   
   @Graph
   public class Network {
   
       @Id
       private String id;
   
       public Network() {
           this.edges = new ArrayList<Object>();
           this.vertexes = new ArrayList<Object>();
       }
   
       @EdgeSet
       @Getter
       private List<Object> edges;
   
       @VertexSet
       @Getter
       private List<Object> vertexes;
   }
   ```

1. <span data-ttu-id="b9d3a-197">Salve e feche o arquivo *Network.java*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-197">Save and close the *Network.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a><span data-ttu-id="b9d3a-198">Defina um conjunto de classes que defina os repositórios do banco de dados de seu grafo</span><span class="sxs-lookup"><span data-stu-id="b9d3a-198">Define a set of classes that define the repositories for your graph database</span></span>

1. <span data-ttu-id="b9d3a-199">Crie uma pasta chamada *repository* no diretório package de seu aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-199">Create a folder named *repository* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   <span data-ttu-id="b9d3a-200">-ou-</span><span class="sxs-lookup"><span data-stu-id="b9d3a-200">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. <span data-ttu-id="b9d3a-201">Crie um novo arquivo Java chamado *NetworkRepository.java* no diretório *repository* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-201">Create a new Java file named *NetworkRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. <span data-ttu-id="b9d3a-202">Salve e feche o arquivo *NetworkRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-202">Save and close the *NetworkRepository.java* file.</span></span>

1. <span data-ttu-id="b9d3a-203">Crie um novo arquivo Java chamado *PersonRepository.java* no diretório *repository* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-203">Create a new Java file named *PersonRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. <span data-ttu-id="b9d3a-204">Salve e feche o arquivo *PersonRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-204">Save and close the *PersonRepository.java* file.</span></span>

1. <span data-ttu-id="b9d3a-205">Crie um novo arquivo Java chamado *RelationRepository.java* no diretório *repository* e, em seguida, abra o arquivo em um editor de texto e adicione as linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-205">Create a new Java file named *RelationRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. <span data-ttu-id="b9d3a-206">Salve e feche o arquivo *RelationRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-206">Save and close the *RelationRepository.java* file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="b9d3a-207">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b9d3a-207">Build and test your app</span></span>

1. <span data-ttu-id="b9d3a-208">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-208">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="b9d3a-209">-ou-</span><span class="sxs-lookup"><span data-stu-id="b9d3a-209">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="b9d3a-210">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-210">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="b9d3a-211">Seu aplicativo exibirá várias mensagens de tempo de execução e, se houver erros, você poderá usar o portal do Azure para exibir o conteúdo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-211">Your application will display several runtime messages, and if there were no errors, you can use the Azure portal to view the contents of your Azure Cosmos DB.</span></span> <span data-ttu-id="b9d3a-212">Para fazer isso, clique em **Data Explorer** na página de propriedades do banco de dados. Em seguida, clique em **Executar consulta de Gremlin** e depois selecione um item da lista de resultados para exibir os dados.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-212">To do so, click **Data Explorer** on the properties page for your database, then click **Execute Gremlin Query**, and then select an item from the list of results to view the data.</span></span>

   ![Como usar o Gerenciador de Documentos para exibir seus dados][JV03]

## <a name="next-steps"></a><span data-ttu-id="b9d3a-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9d3a-214">Next steps</span></span>

<span data-ttu-id="b9d3a-215">Confira estes artigos para obter mais informações sobre o suporte do Azure para Gremlin e API do Graph:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-215">For more information about Azure support for Gremlin and Graph API, see the following articles:</span></span>

* [<span data-ttu-id="b9d3a-216">Introdução ao Azure Cosmos DB: API do Graph</span><span class="sxs-lookup"><span data-stu-id="b9d3a-216">Introduction to Azure Cosmos DB: Graph API</span></span>](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [<span data-ttu-id="b9d3a-217">Suporte do Azure Cosmos DB para grafo do Gremlin</span><span class="sxs-lookup"><span data-stu-id="b9d3a-217">Azure Cosmos DB Gremlin graph support</span></span>](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [<span data-ttu-id="b9d3a-218">Azure Cosmos DB: Criar um banco de dados de grafo usando o Java e o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9d3a-218">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [<span data-ttu-id="b9d3a-219">Tutorial: Consultar a API do Graph do Azure Cosmos DB usando Gremlin</span><span class="sxs-lookup"><span data-stu-id="b9d3a-219">Tutorial: Query Azure Cosmos DB Graph API by using Gremlin</span></span>](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* <span data-ttu-id="b9d3a-220">[Iniciador do Spring Data Gremlin]</span><span class="sxs-lookup"><span data-stu-id="b9d3a-220">[Spring Data Gremlin Starter]</span></span>

<span data-ttu-id="b9d3a-221">Para obter mais informações sobre como usar o Azure Cosmos DB e Java, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-221">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="b9d3a-222">[Documentação do Azure Cosmos DB].</span><span class="sxs-lookup"><span data-stu-id="b9d3a-222">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="b9d3a-223">[Azure Cosmos DB: Criar um banco de dados de documento usando o Java e o Portal do Azure][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="b9d3a-223">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="b9d3a-224">[Spring Data para a API do SQL do Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="b9d3a-224">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="b9d3a-225">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b9d3a-225">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="b9d3a-226">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b9d3a-226">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="b9d3a-227">Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="b9d3a-227">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="b9d3a-228">Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b9d3a-228">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="b9d3a-229">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-229">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="b9d3a-230">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-230">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="b9d3a-231">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-231">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="b9d3a-232">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="b9d3a-232">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>


<!-- URL List -->

[Documentação do Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data para a API do SQL do Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Iniciador do Spring Data Gremlin]: https://github.com/Microsoft/spring-data-gremlin
[Spring Data Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin
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

[AZ01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ05.png
[AZ06]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ06.png
[AZ07]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ07.png
[AZ08]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ08.png

[SI01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV03.png
