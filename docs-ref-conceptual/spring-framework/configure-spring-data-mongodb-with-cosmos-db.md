---
title: Como usar a API do MongoDB do Spring Data com o Azure Cosmos DB
description: Saiba como usar a API do MongoDB do Spring Data com o Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 55fb356820e2cc5eb8d1fe4030053d9e580583af
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991976"
---
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a><span data-ttu-id="80289-103">Como usar a API do MongoDB do Spring Data com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="80289-103">How to use Spring Data MongoDB API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="80289-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="80289-104">Overview</span></span>

<span data-ttu-id="80289-105">Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações usando a [API do MongoDB do Azure Cosmos DB](/azure/cosmos-db/mongodb-introduction).</span><span class="sxs-lookup"><span data-stu-id="80289-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB MongoDB API](/azure/cosmos-db/mongodb-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80289-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80289-106">Prerequisites</span></span>

<span data-ttu-id="80289-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="80289-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="80289-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="80289-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="80289-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="80289-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="80289-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="80289-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="80289-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="80289-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="80289-112">Um cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="80289-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="80289-113">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="80289-113">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="80289-114">Criar uma conta do Cosmos DB usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="80289-114">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="80289-115">Veja informações mais detalhadas sobre como criar contas do Azure Cosmos DB na [documentação do Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="80289-115">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="80289-116">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="80289-116">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="80289-117">Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="80289-117">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Criar uma conta do Azure Cosmos DB][COSMOSDB01]

1. <span data-ttu-id="80289-119">Especifique as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="80289-119">Specify the following information:</span></span>

   - <span data-ttu-id="80289-120">**Assinatura**: especifique a assinatura do Azure para usar.</span><span class="sxs-lookup"><span data-stu-id="80289-120">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="80289-121">**Grupo de recursos**: especifique se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="80289-121">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="80289-122">**Nome da conta**: Escolha um nome exclusivo para sua conta do Cosmos DB. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoysmongodb.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="80289-122">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoysmongodb.documents.azure.com*.</span></span>
   - <span data-ttu-id="80289-123">**API**: Especifique `Azure Cosmos DB for MongoDB API` para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="80289-123">**API**: Specify `Azure Cosmos DB for MongoDB API` for this tutorial.</span></span>
   - <span data-ttu-id="80289-124">**Localização**: especifique a região geográfica mais próxima do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="80289-124">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Especificar as configurações de conta do Cosmos DB][COSMOSDB02]
   
1. <span data-ttu-id="80289-126">Após inserir todas as informações acima, clique em **Revisar + Criar**.</span><span class="sxs-lookup"><span data-stu-id="80289-126">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="80289-127">Se estiver tudo correto na página de revisão, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="80289-127">If everything looks correct on the review page, click **Create**.</span></span>

   ![Revisar as configurações de conta do Cosmos DB][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a><span data-ttu-id="80289-129">Recuperar a cadeia de conexão da conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="80289-129">Retrieve the connection string for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="80289-130">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="80289-130">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="80289-131">Clique em **Todos os Recursos** e, em seguida, clique na conta do Azure Cosmos DB que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="80289-131">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Escolher a conta do Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="80289-133">Clique em **Cadeias conexão** e copie o valor para o campo **Cadeia de conexão primária**; você usará esse valor para configurar seu aplicativo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="80289-133">Click **Connection strings**, and copy the value for the **Primary Connection String** field; you will use that value to configure your application later.</span></span>

   ![Recuperar a cadeia de conexão do Cosmos DB][COSMOSDB06]

## <a name="configure-the-sample-application"></a><span data-ttu-id="80289-135">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="80289-135">Configure the sample application</span></span>

1. <span data-ttu-id="80289-136">Abra um shell de comando e clone o projeto de exemplo usando um comando git como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="80289-136">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. <span data-ttu-id="80289-137">Crie um diretório *recursos* no diretório *&lt;raiz do projeto&gt;/complete/src/main* do exemplo de projeto e crie um arquivo *application.properties*  no diretório *recursos*.</span><span class="sxs-lookup"><span data-stu-id="80289-137">Create a *resources* directory in the *&lt;project root&gt;/complete/src/main* directory of the sample project, and create an *application.properties* file in the *resources* directory.</span></span>

1. <span data-ttu-id="80289-138">Abra o arquivo *application.properties* em um editor de texto e adicione as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:</span><span class="sxs-lookup"><span data-stu-id="80289-138">Open the *application.properties* file in a text editor, and add the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   <span data-ttu-id="80289-139">Em que:</span><span class="sxs-lookup"><span data-stu-id="80289-139">Where:</span></span>

   | <span data-ttu-id="80289-140">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="80289-140">Parameter</span></span> | <span data-ttu-id="80289-141">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="80289-141">Description</span></span> |
   |---|---|
   | `spring.data.mongodb.database` | <span data-ttu-id="80289-142">Especifica o nome da sua conta do Cosmos DB referida anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="80289-142">Specifies the name of your Cosmos DB account from earlier in this article.</span></span> |
   | `spring.data.mongodb.uri` | <span data-ttu-id="80289-143">Especifica a **Cadeia de conexão primária** referida anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="80289-143">Specifies the **Primary Connection String** from earlier in this article.</span></span> |

1. <span data-ttu-id="80289-144">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="80289-144">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="80289-145">Empacotar e testar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="80289-145">Package and test the sample application</span></span> 

1. <span data-ttu-id="80289-146">Compile o aplicativo de exemplo com o Maven e configure o Maven para ignorar os testes. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="80289-146">Build the sample application with Maven, and configure Maven to skip tests; for example:</span></span>

   ```shell
   mvn clean package -DskipTests
   ```

1. <span data-ttu-id="80289-147">Inicie o aplicativo de exemplo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="80289-147">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   <span data-ttu-id="80289-148">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="80289-148">Your application should return values like the following:</span></span>

   ```json
   Customers found with findAll():
   -------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   
   Customer found with findByFirstName('Alice'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customers found with findByLastName('Smith'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   ```

## <a name="summary"></a><span data-ttu-id="80289-149">Resumo</span><span class="sxs-lookup"><span data-stu-id="80289-149">Summary</span></span>

<span data-ttu-id="80289-150">Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações usando a API do MongoDB do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="80289-150">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB MongoDB API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80289-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80289-151">Next steps</span></span>

<span data-ttu-id="80289-152">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="80289-152">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="80289-153">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="80289-153">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="80289-154">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="80289-154">Additional Resources</span></span>

<span data-ttu-id="80289-155">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="80289-155">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB06]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-06.png
