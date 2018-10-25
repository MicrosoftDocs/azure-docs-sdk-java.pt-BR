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
ms.date: 09/10/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: dfc3b6121bddcb637735047e2e7bc7485da9a4fe
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799942"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a><span data-ttu-id="e0843-103">Como criar um aplicativo Spring Cloud Stream Binder com os Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="e0843-103">How to create a Spring Cloud Stream Binder application with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="e0843-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e0843-104">Overview</span></span>

<span data-ttu-id="e0843-105">Este artigo demonstra como configurar um aplicativo Spring Cloud Stream Binder baseado em Java criado com o Spring Boot Initializr e os Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0843-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializer with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0843-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0843-106">Prerequisites</span></span>

<span data-ttu-id="e0843-107">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="e0843-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="e0843-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="e0843-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e0843-109">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e0843-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="e0843-110">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e0843-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="e0843-111">É necessário o Spring Boot versão 2.0 ou posterior para concluir as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e0843-111">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="e0843-112">Criar um Hub de Eventos do Azure usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e0843-112">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="e0843-113">Criar um Namespace do Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="e0843-113">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="e0843-114">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="e0843-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="e0843-115">Clique em **+Criar um recurso**, **Internet das Coisas** e em **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="e0843-115">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Criar Namespace do Hub de Eventos do Azure][IMG01]

1. <span data-ttu-id="e0843-117">Na página **Criar Namespace**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="e0843-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="e0843-118">Insira um **Nome** exclusivo, que se tornará parte da URI do namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e0843-118">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="e0843-119">Por exemplo: se você inseriu **wingtiptoys** como o **Nome**, a URI será *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="e0843-119">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="e0843-120">Escolha um **Tipo de preço** para o namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e0843-120">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="e0843-121">Escolha a **Assinatura** que você deseja usar para o namespace.</span><span class="sxs-lookup"><span data-stu-id="e0843-121">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="e0843-122">Especifique se deseja criar um novo **Grupo de recursos** para o namespace ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="e0843-122">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="e0843-123">Especifique o **Local** do namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e0843-123">Specify the **Location** for your event hub namespace.</span></span>

   ![Especificar opções de Namespace do Hub de Eventos do Azure][IMG02]

1. <span data-ttu-id="e0843-125">Quando você tiver especificado as opções listadas acima, clique em **Criar** para criar o namespace.</span><span class="sxs-lookup"><span data-stu-id="e0843-125">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="e0843-126">Criar um Hub de Eventos do Azure no namespace</span><span class="sxs-lookup"><span data-stu-id="e0843-126">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="e0843-127">Navegue até o portal do Azure em <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="e0843-127">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="e0843-128">Clique em **Todos os recursos** e no namespace criado.</span><span class="sxs-lookup"><span data-stu-id="e0843-128">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Selecionar Namespace do Hub de Eventos do Azure][IMG03]

1. <span data-ttu-id="e0843-130">Clique em **Hubs de Eventos** e **+Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="e0843-130">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Adicionar novo Hub de Eventos do Azure][IMG04]

1. <span data-ttu-id="e0843-132">Na página **Criar Hub de Eventos**, insira um **Nome** exclusivo para o Hub de Eventos e clique **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e0843-132">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Criar Hub de Eventos do Azure][IMG05]

1. <span data-ttu-id="e0843-134">Quando o Hub de Eventos tiver sido criado, ele será listado na página **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="e0843-134">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Criar Hub de Eventos do Azure][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a><span data-ttu-id="e0843-136">Criar uma Conta de Armazenamento do Azure para seus pontos de verificação do Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="e0843-136">Create an Azure Storage Account for your Event Hub checkpoints</span></span>

1. <span data-ttu-id="e0843-137">Navegue até o portal do Azure em <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="e0843-137">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="e0843-138">Clique em **+Criar um recurso**, **Armazenamento** e **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="e0843-138">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Criar uma Conta de Armazenamento do Azure][IMG07]

1. <span data-ttu-id="e0843-140">Na página **Criar Namespace**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="e0843-140">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="e0843-141">Insira um **Nome** exclusivo, que se tornará parte da URI da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e0843-141">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="e0843-142">Por exemplo: se você inseriu **wingtiptoys** para o **Nome**, a URI será *wingtiptoys.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="e0843-142">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.core.windows.net*.</span></span>
   * <span data-ttu-id="e0843-143">Escolha **Armazenamento de Blobs** para o **Tipo de conta**.</span><span class="sxs-lookup"><span data-stu-id="e0843-143">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="e0843-144">Especifique o **Local** da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e0843-144">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="e0843-145">Escolha a **Assinatura** que você deseja usar para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e0843-145">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="e0843-146">Especifique se deseja criar um novo **Grupo de recursos** para a conta de armazenamento ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="e0843-146">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Especificar opções da Conta de Armazenamento do Azure][IMG08]

1. <span data-ttu-id="e0843-148">Quando você tiver especificado as opções listadas acima, clique em **Criar** para criar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e0843-148">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="e0843-149">Criar um aplicativo Spring Boot simples com o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="e0843-149">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="e0843-150">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e0843-150">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e0843-151">Especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="e0843-151">Specify the following options:</span></span>

   * <span data-ttu-id="e0843-152">Gere um projeto **Maven** com **Java**.</span><span class="sxs-lookup"><span data-stu-id="e0843-152">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="e0843-153">Especifique uma versão **Spring Boot** igual ou maior que 2.0.</span><span class="sxs-lookup"><span data-stu-id="e0843-153">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="e0843-154">Especifique os nomes de **Grupo** e **Artefato** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0843-154">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="e0843-155">Adicione a dependência da **Web**.</span><span class="sxs-lookup"><span data-stu-id="e0843-155">Add the **Web** dependency.</span></span>

      ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="e0843-157">O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote, por exemplo, *com.wintiptoys.eventhub*.</span><span class="sxs-lookup"><span data-stu-id="e0843-157">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.eventhub*.</span></span>
   >

1. <span data-ttu-id="e0843-158">Quando você tiver especificado as opções listadas acima, clique em **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="e0843-158">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="e0843-159">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="e0843-159">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixar projeto do Spring][SI02]

1. <span data-ttu-id="e0843-161">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="e0843-161">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a><span data-ttu-id="e0843-162">Configurar seu aplicativo Spring Boot para usar o iniciador do Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="e0843-162">Configure your Spring Boot app to use the Azure Event Hub starter</span></span>

1. <span data-ttu-id="e0843-163">Localize o arquivo *pom.xml* no diretório-raiz do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-163">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\pom.xml`

   <span data-ttu-id="e0843-164">-ou-</span><span class="sxs-lookup"><span data-stu-id="e0843-164">-or-</span></span>

   `/users/example/home/eventhub/pom.xml`

1. <span data-ttu-id="e0843-165">Abra o arquivo *pom.xml* em um editor de texto e adicione o iniciador Spring Cloud Azure Event Hub Stream Binder à lista`<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="e0843-165">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Event Hub Stream Binder starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Editar o arquivo pom.xml][SI03]

1. <span data-ttu-id="e0843-167">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="e0843-167">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="e0843-168">Criar um arquivo de credencial do Azure</span><span class="sxs-lookup"><span data-stu-id="e0843-168">Create an Azure Credential File</span></span>

1. <span data-ttu-id="e0843-169">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="e0843-169">Open a command prompt.</span></span>

1. <span data-ttu-id="e0843-170">Navegue até o diretório de *recursos* do aplicativo Spring Boot, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-170">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="e0843-171">-ou-</span><span class="sxs-lookup"><span data-stu-id="e0843-171">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="e0843-172">Entre na sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="e0843-172">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="e0843-173">Liste suas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="e0843-173">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="e0843-174">O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-174">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. Specify the GUID for the subscription you want to use with Azure; for example:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="e0843-175">Crie seu arquivo de credencial do Azure:</span><span class="sxs-lookup"><span data-stu-id="e0843-175">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="e0843-176">Esse comando criará um arquivo *my.azureauth* no diretório *recursos* com conteúdo semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-176">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="e0843-177">Configurar aplicativo Spring Boot para usar seu Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="e0843-177">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="e0843-178">Localize *application.properties* no diretório *recursos* do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-178">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="e0843-179">-ou-</span><span class="sxs-lookup"><span data-stu-id="e0843-179">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="e0843-180">Abra o arquivo *application.properties* em um editor de texto, adicione as seguintes linhas e substitua os valores de exemplo pelas propriedades adequadas de seu hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="e0843-180">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

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
   <span data-ttu-id="e0843-181">Em que:</span><span class="sxs-lookup"><span data-stu-id="e0843-181">Where:</span></span>

   |                          <span data-ttu-id="e0843-182">Campo</span><span class="sxs-lookup"><span data-stu-id="e0843-182">Field</span></span>                           |                                                                                   <span data-ttu-id="e0843-183">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="e0843-183">Description</span></span>                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    <span data-ttu-id="e0843-184">Especifica o arquivo de credencial do Azure que você criou anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e0843-184">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      <span data-ttu-id="e0843-185">Especifica o Grupo de Recursos do Azure que contém seu Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0843-185">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |               `spring.cloud.azure.region`                |                                           <span data-ttu-id="e0843-186">Especifica a região geográfica definida quando você criou o Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0843-186">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          <span data-ttu-id="e0843-187">Especifica o nome exclusivo definido quando você criou o namespace do Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0843-187">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    <span data-ttu-id="e0843-188">Especifica a Conta de Armazenamento do Azure criada neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e0843-188">Specifies Azure Storage Account that you created earlier in this tutorial.</span></span>                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            <span data-ttu-id="e0843-189">Especifica o destino de entrada do Hub de Eventos do Azure, que é o hub criado anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e0843-189">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |       `spring.cloud.stream.bindings.input.group `        | <span data-ttu-id="e0843-190">Especifica um Grupo de Consumidores do Hub de Eventos do Azure, que pode ser definido para “$Default” para usar o grupo de consumidores básico gerado quando você criou seu Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0843-190">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   |    `spring.cloud.stream.bindings.output.destination`     |                               <span data-ttu-id="e0843-191">Especifica o destino de saída do Hub de Eventos do Azure que, para este tutorial, será igual ao destino de entrada.</span><span class="sxs-lookup"><span data-stu-id="e0843-191">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="e0843-192">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="e0843-192">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="e0843-193">Adicionar código de exemplo para implementar a funcionalidade básica do hub de eventos</span><span class="sxs-lookup"><span data-stu-id="e0843-193">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="e0843-194">Nesta seção, você criará as classes Java necessárias para enviar eventos ao hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e0843-194">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="e0843-195">Modificar a classe principal do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e0843-195">Modify the main application class</span></span>

1. <span data-ttu-id="e0843-196">Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-196">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   <span data-ttu-id="e0843-197">-ou-</span><span class="sxs-lookup"><span data-stu-id="e0843-197">-or-</span></span>

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. <span data-ttu-id="e0843-198">Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="e0843-198">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="e0843-199">Salve e feche o arquivo Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="e0843-199">Save and close the main application Java file.</span></span>

### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="e0843-200">Criar uma nova classe para o conector de origem</span><span class="sxs-lookup"><span data-stu-id="e0843-200">Create a new class for the source connector</span></span>

1. <span data-ttu-id="e0843-201">Crie um novo arquivo Java chamado *EventhubSource.java* no diretório do pacote de seu aplicativo. Abra o arquivo em um editor de texto e adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="e0843-201">Create a new Java file named *EventhubSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

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
1. <span data-ttu-id="e0843-202">Salve e feche o arquivo *EventhubSource.java*.</span><span class="sxs-lookup"><span data-stu-id="e0843-202">Save and close the *EventhubSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="e0843-203">Criar uma nova classe para o conector do coletor</span><span class="sxs-lookup"><span data-stu-id="e0843-203">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="e0843-204">Crie um novo arquivo Java chamado *EventhubSink.java* no diretório do pacote de seu aplicativo. Abra o arquivo em um editor de texto e adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="e0843-204">Create a new Java file named *EventhubSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

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

1. <span data-ttu-id="e0843-205">Salve e feche o arquivo *EventhubSink.java*.</span><span class="sxs-lookup"><span data-stu-id="e0843-205">Save and close the *EventhubSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="e0843-206">Criar e testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="e0843-206">Build and test your application</span></span>

1. <span data-ttu-id="e0843-207">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-207">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\eventhub`

   <span data-ttu-id="e0843-208">-ou-</span><span class="sxs-lookup"><span data-stu-id="e0843-208">-or-</span></span>

   `cd /users/example/home/eventhub`

1. <span data-ttu-id="e0843-209">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-209">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="e0843-210">Quando seu aplicativo estiver em execução, você poderá usar *curl* para testá-lo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e0843-210">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="e0843-211">Você deverá ver "olá" publicado nos logs do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0843-211">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="e0843-212">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="e0843-212">For example:</span></span>

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a><span data-ttu-id="e0843-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0843-213">Next steps</span></span>

<span data-ttu-id="e0843-214">Para obter mais informações sobre o suporte do Azure para o Event Hub Stream Binder, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="e0843-214">For more information about Azure support for Event Hub Stream Binder, see the following articles:</span></span>

* [<span data-ttu-id="e0843-215">O que é Hub de Eventos do Azure?</span><span class="sxs-lookup"><span data-stu-id="e0843-215">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="e0843-216">Criar um namespace dos Hubs de Eventos e um hub de eventos usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e0843-216">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="e0843-217">Como usar o Inicializador do Spring Boot para Apache Kafka com os Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="e0843-217">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)

<span data-ttu-id="e0843-218">Para obter mais informações sobre como usar o Azure com Java, veja [Azure para Desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e0843-218">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e0843-219">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="e0843-219">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e0843-220">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="e0843-220">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="e0843-221">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="e0843-221">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="e0843-222">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="e0843-222">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

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
