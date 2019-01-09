---
title: Como usar a API do Apache Cassandra do Spring Data com o Azure Cosmos DB
description: Saiba como usar a API do Apache Cassandra do Spring Data com o Azure Cosmos DB.
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
ms.openlocfilehash: 1f3f7a55b49d64077df9e7d4d6acc3af4495b424
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991957"
---
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a><span data-ttu-id="801c4-103">Como usar a API do Apache Cassandra do Spring Data com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="801c4-103">How to use Spring Data Apache Cassandra API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="801c4-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="801c4-104">Overview</span></span>

<span data-ttu-id="801c4-105">Este artigo demonstra a criação de um aplicativo de exemplo que usa o [Spring Data] para armazenar e recuperar informações usando a [API do Cassandra do Azure Cosmos DB](/azure/cosmos-db/cassandra-introduction).</span><span class="sxs-lookup"><span data-stu-id="801c4-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB Cassandra API](/azure/cosmos-db/cassandra-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="801c4-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="801c4-106">Prerequisites</span></span>

<span data-ttu-id="801c4-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="801c4-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="801c4-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="801c4-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="801c4-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="801c4-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="801c4-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="801c4-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="801c4-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="801c4-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="801c4-112">[Curl](https://curl.haxx.se/) ou utilitário HTTP semelhante para testar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="801c4-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="801c4-113">Um cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="801c4-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="801c4-114">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="801c4-114">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="801c4-115">Criar uma conta do Cosmos DB usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="801c4-115">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="801c4-116">Veja informações mais detalhadas sobre como criar contas do Azure Cosmos DB na [documentação do Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="801c4-116">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="801c4-117">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="801c4-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="801c4-118">Clique em **+Criar um recurso**, **Bancos de dados** e clique em **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="801c4-118">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Criar uma conta do Azure Cosmos DB][COSMOSDB01]

1. <span data-ttu-id="801c4-120">Especifique as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="801c4-120">Specify the following information:</span></span>

   - <span data-ttu-id="801c4-121">**Assinatura**: especifique a assinatura do Azure para usar.</span><span class="sxs-lookup"><span data-stu-id="801c4-121">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="801c4-122">**Grupo de recursos**: especifique se deseja criar um novo grupo de recursos ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="801c4-122">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="801c4-123">**Nome da conta**: Escolha um nome exclusivo para sua conta do Cosmos DB. Ele será usado para criar um nome de domínio totalmente qualificado, como *wingtiptoyscassandra.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="801c4-123">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoyscassandra.documents.azure.com*.</span></span>
   - <span data-ttu-id="801c4-124">**API**: Especifique `Cassandra` para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="801c4-124">**API**: Specify `Cassandra` for this tutorial.</span></span>
   - <span data-ttu-id="801c4-125">**Localização**: especifique a região geográfica mais próxima do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="801c4-125">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Especificar as configurações de conta do Cosmos DB][COSMOSDB02]
   
1. <span data-ttu-id="801c4-127">Após inserir todas as informações acima, clique em **Revisar + Criar**.</span><span class="sxs-lookup"><span data-stu-id="801c4-127">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="801c4-128">Se estiver tudo correto na página de revisão, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="801c4-128">If everything looks correct on the review page, click **Create**.</span></span>

   ![Revisar as configurações de conta do Cosmos DB][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a><span data-ttu-id="801c4-130">Adicionar um keyspace à sua conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="801c4-130">Add a keyspace to your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="801c4-131">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="801c4-131">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="801c4-132">Clique em **Todos os Recursos** e, em seguida, clique na conta do Azure Cosmos DB que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="801c4-132">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Escolher a conta do Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="801c4-134">Clique em **Data Explorer** e em **Novo Keyspace**.</span><span class="sxs-lookup"><span data-stu-id="801c4-134">Click **Data Explorer**, then click **New Keyspace**.</span></span> <span data-ttu-id="801c4-135">Insira um identificador exclusivo para sua **id do Keyspace** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="801c4-135">Enter a unique identifier for your **Keyspace id**, then click **OK**.</span></span>

   ![Criar um keyspace do Cosmos DB][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a><span data-ttu-id="801c4-137">Recuperar as configurações de conexão da conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="801c4-137">Retrieve the connection settings for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="801c4-138">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="801c4-138">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="801c4-139">Clique em **Todos os Recursos** e, em seguida, clique na conta do Azure Cosmos DB que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="801c4-139">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Escolher a conta do Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="801c4-141">Clique em **Cadeias de conexão** e copie os valores dos campos **Ponto de Contato**, **Porta**, **Nome de Usuário** e **Senha Primária**. Você usará esses valores para configurar seu aplicativo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="801c4-141">Click **Connection strings**, and copy the values for the **Contact Point**, **Port**, **Username**, and **Primary Password** fields; you will use those values to configure your application later.</span></span>

   ![Recuperar as configurações de conexão do Cosmos DB][COSMOSDB05]

## <a name="configure-the-sample-application"></a><span data-ttu-id="801c4-143">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="801c4-143">Configure the sample application</span></span>

1. <span data-ttu-id="801c4-144">Abra um shell de comando e clone o projeto de exemplo usando um comando git como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="801c4-144">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. <span data-ttu-id="801c4-145">Localize o arquivo *application.properties* no diretório *recursos* do seu projeto de exemplo ou crie o arquivo se ele ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="801c4-145">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="801c4-146">Abra o arquivo *application.properties* em um editor de texto e adicione ou configure as seguintes linhas ao arquivo e substitua os valores de exemplo pelos valores adequados do início do artigo:</span><span class="sxs-lookup"><span data-stu-id="801c4-146">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   <span data-ttu-id="801c4-147">Em que:</span><span class="sxs-lookup"><span data-stu-id="801c4-147">Where:</span></span>

   | <span data-ttu-id="801c4-148">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="801c4-148">Parameter</span></span> | <span data-ttu-id="801c4-149">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="801c4-149">Description</span></span> |
   |---|---|
   | `spring.data.cassandra.contact-points` | <span data-ttu-id="801c4-150">Especifica o **Ponto de Contato** neste artigo.</span><span class="sxs-lookup"><span data-stu-id="801c4-150">Specifies the **Contact Point** from earlier in this article.</span></span> |
   | `spring.data.cassandra.port` | <span data-ttu-id="801c4-151">Especifica a **Porta** neste artigo.</span><span class="sxs-lookup"><span data-stu-id="801c4-151">Specifies the **Port** from earlier in this article.</span></span> |
   | `spring.data.cassandra.username` | <span data-ttu-id="801c4-152">Especifica seu **Nome de Usuário** neste artigo.</span><span class="sxs-lookup"><span data-stu-id="801c4-152">Specifies your **Username** from earlier in this article.</span></span> |
   | `spring.data.cassandra.password` | <span data-ttu-id="801c4-153">Especifica sua **Senha Primária** neste artigo.</span><span class="sxs-lookup"><span data-stu-id="801c4-153">Specifies your **Primary Password** from earlier in this article.</span></span> |

1. <span data-ttu-id="801c4-154">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="801c4-154">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="801c4-155">Empacotar e testar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="801c4-155">Package and test the sample application</span></span> 

1. <span data-ttu-id="801c4-156">Crie seu aplicativo de exemplo com o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="801c4-156">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="801c4-157">Inicie o aplicativo de exemplo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="801c4-157">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="801c4-158">Crie novos registros usando `curl` em um prompt de comando como nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="801c4-158">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="801c4-159">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="801c4-159">Your application should return values like the following:</span></span>

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. <span data-ttu-id="801c4-160">Recupere todos os registros existentes usando `curl` em um prompt de comando como nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="801c4-160">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="801c4-161">Seu aplicativo deve retornar valores como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="801c4-161">Your application should return values like the following:</span></span>

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="801c4-162">Resumo</span><span class="sxs-lookup"><span data-stu-id="801c4-162">Summary</span></span>

<span data-ttu-id="801c4-163">Neste tutorial, você criou um aplicativo Java de exemplo que usa o Spring Data para armazenar e recuperar informações usando a API do Cassandra do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="801c4-163">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB Cassandra API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="801c4-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="801c4-164">Next steps</span></span>

<span data-ttu-id="801c4-165">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="801c4-165">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="801c4-166">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="801c4-166">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="801c4-167">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="801c4-167">Additional Resources</span></span>

<span data-ttu-id="801c4-168">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="801c4-168">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
