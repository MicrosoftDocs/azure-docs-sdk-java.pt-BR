---
title: Como criar um aplicativo Spring Cloud Stream Binder com os Hubs de Eventos do Azure
description: Saiba como configurar um aplicativo Spring Cloud Stream Binder baseado em Java criado com o Spring Boot Initializr e os Hubs de Eventos do Azure.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: 98b3dc1243bf293ede121eafd51b041649d165db
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991420"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a><span data-ttu-id="1ef6f-103">Como criar um aplicativo Spring Cloud Stream Binder com os Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-103">How to create a Spring Cloud Stream Binder application with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="1ef6f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1ef6f-104">Overview</span></span>

<span data-ttu-id="1ef6f-105">Este artigo demonstra como configurar um aplicativo Spring Cloud Stream Binder baseado em Java criado com o Spring Boot Initializr e os Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializer with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ef6f-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1ef6f-106">Prerequisites</span></span>

<span data-ttu-id="1ef6f-107">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="1ef6f-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="1ef6f-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1ef6f-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="1ef6f-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="1ef6f-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="1ef6f-112">É necessário o Spring Boot versão 2.0 ou posterior para concluir as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="1ef6f-113">Criar um Hub de Eventos do Azure usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-113">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="1ef6f-114">Criar um Namespace do Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-114">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="1ef6f-115">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1ef6f-116">Clique em **+Criar um recurso**, **Internet das Coisas** e em **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-116">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Criar Namespace do Hub de Eventos do Azure][IMG01]

1. <span data-ttu-id="1ef6f-118">Na página **Criar Namespace**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="1ef6f-119">Insira um **Nome** exclusivo, que se tornará parte da URI do namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-119">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="1ef6f-120">Por exemplo: se você inseriu **wingtiptoys** como o **Nome**, a URI será *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-120">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="1ef6f-121">Escolha um **Tipo de preço** para o namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-121">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="1ef6f-122">Escolha a **Assinatura** que você deseja usar para o namespace.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="1ef6f-123">Especifique se deseja criar um novo **Grupo de recursos** para o namespace ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="1ef6f-124">Especifique o **Local** do namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-124">Specify the **Location** for your event hub namespace.</span></span>

   ![Especificar opções de Namespace do Hub de Eventos do Azure][IMG02]

1. <span data-ttu-id="1ef6f-126">Quando você tiver especificado as opções listadas acima, clique em **Criar** para criar o namespace.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="1ef6f-127">Criar um Hub de Eventos do Azure no namespace</span><span class="sxs-lookup"><span data-stu-id="1ef6f-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="1ef6f-128">Navegue até o portal do Azure em <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="1ef6f-129">Clique em **Todos os recursos** e no namespace criado.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Selecionar Namespace do Hub de Eventos do Azure][IMG03]

1. <span data-ttu-id="1ef6f-131">Clique em **Hubs de Eventos** e **+Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Adicionar novo Hub de Eventos do Azure][IMG04]

1. <span data-ttu-id="1ef6f-133">Na página **Criar Hub de Eventos**, insira um **Nome** exclusivo para o Hub de Eventos e clique **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Criar Hub de Eventos do Azure][IMG05]

1. <span data-ttu-id="1ef6f-135">Quando o Hub de Eventos tiver sido criado, ele será listado na página **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Criar Hub de Eventos do Azure][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a><span data-ttu-id="1ef6f-137">Criar uma Conta de Armazenamento do Azure para seus pontos de verificação do Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="1ef6f-137">Create an Azure Storage Account for your Event Hub checkpoints</span></span>

1. <span data-ttu-id="1ef6f-138">Navegue até o portal do Azure em <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-138">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="1ef6f-139">Clique em **+Criar um recurso**, **Armazenamento** e **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-139">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Criar uma Conta de Armazenamento do Azure][IMG07]

1. <span data-ttu-id="1ef6f-141">Na página **Criar Namespace**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-141">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="1ef6f-142">Insira um **Nome** exclusivo, que se tornará parte da URI da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-142">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="1ef6f-143">Por exemplo: se você inseriu **wingtiptoys** para o **Nome**, a URI será *wingtiptoys.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-143">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.core.windows.net*.</span></span>
   * <span data-ttu-id="1ef6f-144">Escolha **Armazenamento de Blobs** para o **Tipo de conta**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-144">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="1ef6f-145">Especifique o **Local** da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-145">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="1ef6f-146">Escolha a **Assinatura** que você deseja usar para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-146">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="1ef6f-147">Especifique se deseja criar um novo **Grupo de recursos** para a conta de armazenamento ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-147">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Especificar opções da Conta de Armazenamento do Azure][IMG08]

1. <span data-ttu-id="1ef6f-149">Quando você tiver especificado as opções listadas acima, clique em **Criar** para criar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-149">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="1ef6f-150">Criar um aplicativo Spring Boot simples com o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="1ef6f-150">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="1ef6f-151">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-151">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="1ef6f-152">Especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-152">Specify the following options:</span></span>

   * <span data-ttu-id="1ef6f-153">Gere um projeto **Maven** com **Java**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-153">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="1ef6f-154">Especifique uma versão **Spring Boot** igual ou maior que 2.0.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-154">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="1ef6f-155">Especifique os nomes de **Grupo** e **Artefato** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-155">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="1ef6f-156">Adicione a dependência da **Web**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-156">Add the **Web** dependency.</span></span>

      ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="1ef6f-158">O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote, por exemplo, *com.wintiptoys.eventhub*.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-158">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.eventhub*.</span></span>
   >

1. <span data-ttu-id="1ef6f-159">Quando você tiver especificado as opções listadas acima, clique em **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-159">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="1ef6f-160">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-160">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixar projeto do Spring][SI02]

1. <span data-ttu-id="1ef6f-162">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-162">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a><span data-ttu-id="1ef6f-163">Configurar seu aplicativo Spring Boot para usar o iniciador do Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-163">Configure your Spring Boot app to use the Azure Event Hub starter</span></span>

1. <span data-ttu-id="1ef6f-164">Localize o arquivo *pom.xml* no diretório-raiz do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-164">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\pom.xml`

   <span data-ttu-id="1ef6f-165">-ou-</span><span class="sxs-lookup"><span data-stu-id="1ef6f-165">-or-</span></span>

   `/users/example/home/eventhub/pom.xml`

1. <span data-ttu-id="1ef6f-166">Abra o arquivo *pom.xml* em um editor de texto e adicione o iniciador Spring Cloud Azure Event Hub Stream Binder à lista`<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-166">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Event Hub Stream Binder starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Editar o arquivo pom.xml][SI03]

1. <span data-ttu-id="1ef6f-168">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-168">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="1ef6f-169">Criar um arquivo de credencial do Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-169">Create an Azure Credential File</span></span>

1. <span data-ttu-id="1ef6f-170">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-170">Open a command prompt.</span></span>

1. <span data-ttu-id="1ef6f-171">Navegue até o diretório de *recursos* do aplicativo Spring Boot, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-171">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="1ef6f-172">-ou-</span><span class="sxs-lookup"><span data-stu-id="1ef6f-172">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="1ef6f-173">Entre na sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-173">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="1ef6f-174">Liste suas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-174">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="1ef6f-175">O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-175">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```
1. <span data-ttu-id="1ef6f-176">Especifique o GUID para a assinatura que quer usar no Azure; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-176">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="1ef6f-177">Crie seu arquivo de credencial do Azure:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-177">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="1ef6f-178">Esse comando criará um arquivo *my.azureauth* no diretório *recursos* com conteúdo semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-178">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="1ef6f-179">Configurar aplicativo Spring Boot para usar seu Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-179">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="1ef6f-180">Localize *application.properties* no diretório *recursos* do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-180">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="1ef6f-181">-ou-</span><span class="sxs-lookup"><span data-stu-id="1ef6f-181">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="1ef6f-182">Abra o arquivo *application.properties* em um editor de texto, adicione as seguintes linhas e substitua os valores de exemplo pelas propriedades adequadas de seu hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-182">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace
   spring.cloud.azure.eventhub.checkpoint-storage-account=wingtiptoysstorage
   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   spring.cloud.stream.eventhub.bindings.input.consumer.checkpoint-mode=MANUAL
   ```
   <span data-ttu-id="1ef6f-183">Em que:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-183">Where:</span></span>

   |                          <span data-ttu-id="1ef6f-184">Campo</span><span class="sxs-lookup"><span data-stu-id="1ef6f-184">Field</span></span>                           |                                                                                   <span data-ttu-id="1ef6f-185">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="1ef6f-185">Description</span></span>                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    <span data-ttu-id="1ef6f-186">Especifica o arquivo de credencial do Azure que você criou anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-186">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      <span data-ttu-id="1ef6f-187">Especifica o Grupo de Recursos do Azure que contém seu Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-187">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |               `spring.cloud.azure.region`                |                                           <span data-ttu-id="1ef6f-188">Especifica a região geográfica definida quando você criou o Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-188">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          <span data-ttu-id="1ef6f-189">Especifica o nome exclusivo definido quando você criou o namespace do Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-189">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    <span data-ttu-id="1ef6f-190">Especifica a Conta de Armazenamento do Azure criada neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-190">Specifies Azure Storage Account that you created earlier in this tutorial.</span></span>                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            <span data-ttu-id="1ef6f-191">Especifica o destino de entrada do Hub de Eventos do Azure, que é o hub criado anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-191">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |       `spring.cloud.stream.bindings.input.group `        | <span data-ttu-id="1ef6f-192">Especifica um Grupo de Consumidores do Hub de Eventos do Azure, que pode ser definido para “$Default” para usar o grupo de consumidores básico gerado quando você criou seu Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-192">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   |    `spring.cloud.stream.bindings.output.destination`     |                               <span data-ttu-id="1ef6f-193">Especifica o destino de saída do Hub de Eventos do Azure que, para este tutorial, será igual ao destino de entrada.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-193">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="1ef6f-194">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-194">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="1ef6f-195">Adicionar código de exemplo para implementar a funcionalidade básica do hub de eventos</span><span class="sxs-lookup"><span data-stu-id="1ef6f-195">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="1ef6f-196">Nesta seção, você criará as classes Java necessárias para enviar eventos ao hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-196">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="1ef6f-197">Modificar a classe principal do aplicativo</span><span class="sxs-lookup"><span data-stu-id="1ef6f-197">Modify the main application class</span></span>

1. <span data-ttu-id="1ef6f-198">Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-198">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   <span data-ttu-id="1ef6f-199">-ou-</span><span class="sxs-lookup"><span data-stu-id="1ef6f-199">-or-</span></span>

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. <span data-ttu-id="1ef6f-200">Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-200">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class EventhubApplication {
      public static void main(String[] args) {
         SpringApplication.run(EventhubApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="1ef6f-201">Salve e feche o arquivo Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-201">Save and close the main application Java file.</span></span>

### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="1ef6f-202">Criar uma nova classe para o conector de origem</span><span class="sxs-lookup"><span data-stu-id="1ef6f-202">Create a new class for the source connector</span></span>

1. <span data-ttu-id="1ef6f-203">Crie um novo arquivo Java chamado *EventhubSource.java* no diretório do pacote de seu aplicativo. Abra o arquivo em um editor de texto e adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-203">Create a new Java file named *EventhubSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class EventhubSource {

      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String postMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```
1. <span data-ttu-id="1ef6f-204">Salve e feche o arquivo *EventhubSource.java*.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-204">Save and close the *EventhubSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="1ef6f-205">Criar uma nova classe para o conector do coletor</span><span class="sxs-lookup"><span data-stu-id="1ef6f-205">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="1ef6f-206">Crie um novo arquivo Java chamado *EventhubSink.java* no diretório do pacote de seu aplicativo. Abra o arquivo em um editor de texto e adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-206">Create a new Java file named *EventhubSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import com.microsoft.azure.spring.integration.core.AzureHeaders;
   import com.microsoft.azure.spring.integration.core.api.Checkpointer;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   import org.springframework.messaging.handler.annotation.Header;

   @EnableBinding(Sink.class)
   public class EventhubSink {

      private static final Logger LOGGER = LoggerFactory.getLogger(EventhubSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message, @Header(AzureHeaders.CHECKPOINTER) Checkpointer checkpointer) {
         LOGGER.info("New message received: '{}'", message);
         checkpointer.success().handle((r, ex) -> {
            if (ex == null) {
               LOGGER.info("Message '{}' successfully checkpointed", message);
            }
            return null;
         });
      }
   }
   ```

1. <span data-ttu-id="1ef6f-207">Salve e feche o arquivo *EventhubSink.java*.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-207">Save and close the *EventhubSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="1ef6f-208">Criar e testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="1ef6f-208">Build and test your application</span></span>

1. <span data-ttu-id="1ef6f-209">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-209">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\eventhub`

   <span data-ttu-id="1ef6f-210">-ou-</span><span class="sxs-lookup"><span data-stu-id="1ef6f-210">-or-</span></span>

   `cd /users/example/home/eventhub`

1. <span data-ttu-id="1ef6f-211">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-211">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="1ef6f-212">Quando seu aplicativo estiver em execução, você poderá usar *curl* para testá-lo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-212">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="1ef6f-213">Você deverá ver "olá" publicado nos logs do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-213">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="1ef6f-214">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="1ef6f-214">For example:</span></span>

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a><span data-ttu-id="1ef6f-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ef6f-215">Next steps</span></span>

<span data-ttu-id="1ef6f-216">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-216">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ef6f-217">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-217">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="1ef6f-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1ef6f-218">Additional Resources</span></span>

<span data-ttu-id="1ef6f-219">Para obter mais informações sobre o suporte do Azure para o Event Hub Stream Binder, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="1ef6f-219">For more information about Azure support for Event Hub Stream Binder, see the following articles:</span></span>

* [<span data-ttu-id="1ef6f-220">O que é Hub de Eventos do Azure?</span><span class="sxs-lookup"><span data-stu-id="1ef6f-220">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="1ef6f-221">Criar um namespace dos Hubs de Eventos e um hub de eventos usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-221">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="1ef6f-222">Como usar o Inicializador do Spring Boot para Apache Kafka com os Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="1ef6f-222">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)

<span data-ttu-id="1ef6f-223">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Trabalhando com o Java e Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="1ef6f-223">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="1ef6f-224">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-224">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="1ef6f-225">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-225">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="1ef6f-226">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-226">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="1ef6f-227">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="1ef6f-227">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Trabalhando com o Java e Azure DevOps]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-03.png
