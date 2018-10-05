---
title: Como usar o Inicializador do Spring Boot para Apache Kafka com os Hubs de Eventos do Azure
description: Saiba como configurar um aplicativo criado com o Spring Boot Initializr para usar o Apache Kafka com os Hubs de Eventos do Azure.
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
ms.openlocfilehash: 00062f5442e072af30036388f2f1f066221d7316
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506258"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a><span data-ttu-id="91bef-103">Como usar o Inicializador do Spring Boot para Apache Kafka com os Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="91bef-103">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="91bef-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="91bef-104">Overview</span></span>

<span data-ttu-id="91bef-105">Este artigo demonstra como configurar um Spring Cloud Stream Binder baseado em Java criado com o Spring Boot Initializer para usar o [Apache Kafka] com os Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="91bef-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder created with the Spring Boot Initializer to use [Apache Kafka] with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91bef-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="91bef-106">Prerequisites</span></span>

<span data-ttu-id="91bef-107">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="91bef-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="91bef-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="91bef-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="91bef-109">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="91bef-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="91bef-110">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="91bef-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="91bef-111">É necessário o Spring Boot versão 2.0 ou posterior para concluir as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="91bef-111">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="91bef-112">Criar um Hub de Eventos do Azure usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="91bef-112">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="91bef-113">Criar um namespace do Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="91bef-113">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="91bef-114">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="91bef-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="91bef-115">Clique em **+Criar um recurso**, em **Internet das Coisas** e clique em **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="91bef-115">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Criar namespace do Hub de Eventos do Azure][IMG01]

1. <span data-ttu-id="91bef-117">Na página **Criar Namespace**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="91bef-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="91bef-118">Insira um **Nome** exclusivo, que se tornará parte do URI do namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="91bef-118">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="91bef-119">Por exemplo: se você inseriu **wingtiptoys** como o **nome**, o URI será *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="91bef-119">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="91bef-120">Escolha um **Tipo de preço** para o namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="91bef-120">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="91bef-121">Especifique **Habilitar Kafka** como o namespace.</span><span class="sxs-lookup"><span data-stu-id="91bef-121">Specify **Enable Kafka** for your namespace.</span></span>
   * <span data-ttu-id="91bef-122">Escolha a **Assinatura** que você deseja usar para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="91bef-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="91bef-123">Especifique se deseja criar um novo **Grupo de recursos** para o namespace ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="91bef-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="91bef-124">Especifique o **Local** do namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="91bef-124">Specify the **Location** for your event hub namespace.</span></span>
   
   ![Especificar opções de Namespace do Hub de Eventos do Azure][IMG02]

1. <span data-ttu-id="91bef-126">Quando você tiver especificado as opções listadas acima, clique em **Criar** para criar o namespace.</span><span class="sxs-lookup"><span data-stu-id="91bef-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="91bef-127">Criar um Hub de Eventos do Azure no namespace</span><span class="sxs-lookup"><span data-stu-id="91bef-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="91bef-128">Navegue até o portal do Azure em <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="91bef-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="91bef-129">Clique em **Todos os recursos**e clique no namespace criado.</span><span class="sxs-lookup"><span data-stu-id="91bef-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Selecionar namespace do Hub de Eventos do Azure][IMG03]

1. <span data-ttu-id="91bef-131">Clique em **Hubs de Eventos** e clique em **+Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="91bef-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Adicionar novo Hub de Eventos do Azure][IMG04]

1. <span data-ttu-id="91bef-133">Na página **Criar Hub de Eventos**, insira um **Nome** exclusivo para o Hub de Eventos e clique **Criar**.</span><span class="sxs-lookup"><span data-stu-id="91bef-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Criar Hub de Eventos do Azure][IMG05]

1. <span data-ttu-id="91bef-135">Quando o Hub de Eventos tiver sido criado, ele será listado na página **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="91bef-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Criar Hub de Eventos do Azure][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="91bef-137">Criar um aplicativo Spring Boot simples com o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="91bef-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="91bef-138">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="91bef-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="91bef-139">Especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="91bef-139">Specify the following options:</span></span>

   * <span data-ttu-id="91bef-140">Gere um projeto **Maven** com **Java**.</span><span class="sxs-lookup"><span data-stu-id="91bef-140">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="91bef-141">Especifique uma versão **Spring Boot** igual ou maior que 2.0.</span><span class="sxs-lookup"><span data-stu-id="91bef-141">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="91bef-142">Especifique os nomes de **Grupo** e **Artefato** para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91bef-142">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="91bef-143">Adicione a dependência da **Web**.</span><span class="sxs-lookup"><span data-stu-id="91bef-143">Add the **Web** dependency.</span></span>

      ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="91bef-145">O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote, por exemplo, *com.wintiptoys.kafka*.</span><span class="sxs-lookup"><span data-stu-id="91bef-145">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.kafka*.</span></span>
   >

1. <span data-ttu-id="91bef-146">Quando você tiver especificado as opções listadas acima, clique em **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="91bef-146">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="91bef-147">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="91bef-147">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixar projeto do Spring][SI02]

1. <span data-ttu-id="91bef-149">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="91bef-149">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a><span data-ttu-id="91bef-150">Configurar o aplicativo Spring Boot para usar os iniciadores do Spring Cloud Kafka Stream e iniciadores do Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="91bef-150">Configure your Spring Boot app to use the Spring Cloud Kafka Stream and Azure Event Hub starters</span></span>

1. <span data-ttu-id="91bef-151">Localize o arquivo *pom.xml* no diretório raiz do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-151">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\pom.xml`

   <span data-ttu-id="91bef-152">-ou-</span><span class="sxs-lookup"><span data-stu-id="91bef-152">-or-</span></span>

   `/users/example/home/kafka/pom.xml`

1. <span data-ttu-id="91bef-153">Abra o arquivo *pom.xml* em um editor de texto e adicione o iniciador do Spring Cloud Kafka Stream e os iniciadores do Hub de Eventos do Azure à lista de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="91bef-153">Open the *pom.xml* file in a text editor, and add the Spring Cloud Kafka Stream and Azure Event Hub starters to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-stream-kafka</artifactId>
      <version>2.0.1.RELEASE</version>
   </dependency>
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-starter-eventhub</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Editar o arquivo pom.xml][SI03]

1. <span data-ttu-id="91bef-155">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="91bef-155">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="91bef-156">Criar um arquivo de credencial do Azure</span><span class="sxs-lookup"><span data-stu-id="91bef-156">Create an Azure Credential File</span></span>

1. <span data-ttu-id="91bef-157">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="91bef-157">Open a command prompt.</span></span>

1. <span data-ttu-id="91bef-158">Navegue até o diretório de *recursos* do aplicativo Spring Boot, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-158">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="91bef-159">-ou-</span><span class="sxs-lookup"><span data-stu-id="91bef-159">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="91bef-160">Entre na sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="91bef-160">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="91bef-161">Liste suas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="91bef-161">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="91bef-162">O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-162">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="91bef-163">Crie seu arquivo de credencial do Azure:</span><span class="sxs-lookup"><span data-stu-id="91bef-163">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="91bef-164">Esse comando criará um arquivo *my.azureauth* no diretório *recursos* com conteúdo semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-164">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="91bef-165">Configurar o aplicativo Spring Boot para usar seu Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="91bef-165">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="91bef-166">Localize o *application.properties* no diretório *recursos* do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-166">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="91bef-167">-ou-</span><span class="sxs-lookup"><span data-stu-id="91bef-167">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

1.  <span data-ttu-id="91bef-168">Abra o arquivo *application.properties* em um editor de texto, adicione as seguintes linhas ao arquivo e substitua os valores de exemplo pelas propriedades adequadas para seu hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="91bef-168">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   <span data-ttu-id="91bef-169">Em que:</span><span class="sxs-lookup"><span data-stu-id="91bef-169">Where:</span></span>
   | <span data-ttu-id="91bef-170">Campo</span><span class="sxs-lookup"><span data-stu-id="91bef-170">Field</span></span> | <span data-ttu-id="91bef-171">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="91bef-171">Description</span></span> |
   | ---|---|
   | `spring.cloud.azure.credential-file-path` | <span data-ttu-id="91bef-172">Especifica o arquivo de credencial do Azure que você criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="91bef-172">Specifies Azure credential file that you created earlier in this tutorial.</span></span> |
   | `spring.cloud.azure.resource-group` | <span data-ttu-id="91bef-173">Especifica o grupo de recursos do Azure que contém seu Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="91bef-173">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span> |
   | `spring.cloud.azure.region` | <span data-ttu-id="91bef-174">Especifica a região geográfica que você especificou quando criou o Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="91bef-174">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.azure.eventhub.namespace` | <span data-ttu-id="91bef-175">Especifica o nome exclusivo definido quando você criou o namespace do Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="91bef-175">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span> |
   | `spring.cloud.stream.bindings.input.destination` | <span data-ttu-id="91bef-176">Especifica o destino de entrada do Hub de Eventos do Azure, que é o hub criado anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="91bef-176">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span> |
   | `spring.cloud.stream.bindings.input.group `| <span data-ttu-id="91bef-177">Especifica um grupo de consumidores do Hub de Eventos do Azure, que pode ser definido como '$Default' para usar o grupo de consumidores básico gerado quando você criou seu Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="91bef-177">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.stream.bindings.output.destination` | <span data-ttu-id="91bef-178">Especifica o destino de saída do Hub de Eventos do Azure, que, para este tutorial, será igual ao destino de entrada.</span><span class="sxs-lookup"><span data-stu-id="91bef-178">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span> |

1. <span data-ttu-id="91bef-179">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="91bef-179">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="91bef-180">Adicione o código de exemplo para implementar a funcionalidade básica de hub de eventos</span><span class="sxs-lookup"><span data-stu-id="91bef-180">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="91bef-181">Nesta seção, você criará as classes Java necessárias para enviar eventos a seu hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="91bef-181">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="91bef-182">Modificar a classe principal do aplicativo</span><span class="sxs-lookup"><span data-stu-id="91bef-182">Modify the main application class</span></span>

1. <span data-ttu-id="91bef-183">Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-183">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   <span data-ttu-id="91bef-184">-ou-</span><span class="sxs-lookup"><span data-stu-id="91bef-184">-or-</span></span>

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. <span data-ttu-id="91bef-185">Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="91bef-185">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.kafka;
   
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   @SpringBootApplication
   public class KafkaApplication {
      public static void main(String[] args) {
         SpringApplication.run(KafkaApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="91bef-186">Salve e feche o arquivo Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="91bef-186">Save and close the main application Java file.</span></span>


### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="91bef-187">Criar uma nova classe para o conector de origem</span><span class="sxs-lookup"><span data-stu-id="91bef-187">Create a new class for the source connector</span></span>

1. <span data-ttu-id="91bef-188">Crie um novo arquivo Java chamado *KafkaSource.java* no diretório do pacote de seu aplicativo; abra o arquivo em um editor de texto e adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="91bef-188">Create a new Java file named *KafkaSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;
   
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.RestController;
   
   @EnableBinding(Source.class)
   @RestController
   public class KafkaSource {
      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String sendMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```

1. <span data-ttu-id="91bef-189">Salve e feche o arquivo *KafkaSource.java*.</span><span class="sxs-lookup"><span data-stu-id="91bef-189">Save and close the *KafkaSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="91bef-190">Criar uma nova classe para o conector do coletor</span><span class="sxs-lookup"><span data-stu-id="91bef-190">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="91bef-191">Crie um novo arquivo Java chamado *KafkaSink.java* no diretório do pacote de seu aplicativo; abra o arquivo em um editor de texto e adicione as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="91bef-191">Create a new Java file named *KafkaSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   
   @EnableBinding(Sink.class)
   public class KafkaSink {
      private static final Logger LOGGER = LoggerFactory.getLogger(KafkaSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message) {
         LOGGER.info("New message received: " + message);
      }
   }
   ```

1. <span data-ttu-id="91bef-192">Salve e feche o arquivo *KafkaSink.java*.</span><span class="sxs-lookup"><span data-stu-id="91bef-192">Save and close the *KafkaSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="91bef-193">Criar e testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="91bef-193">Build and test your application</span></span>

1. <span data-ttu-id="91bef-194">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-194">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\kafka`

   <span data-ttu-id="91bef-195">-ou-</span><span class="sxs-lookup"><span data-stu-id="91bef-195">-or-</span></span>

   `cd /users/example/home/kafka`

1. <span data-ttu-id="91bef-196">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-196">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="91bef-197">Quando seu aplicativo estiver em execução, você poderá usar *curl* para testá-lo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91bef-197">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="91bef-198">Você deve ver "hello" publicado nos logs do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91bef-198">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="91bef-199">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="91bef-199">For example:</span></span>

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> <span data-ttu-id="91bef-200">Para fins de teste, você poderia modificar o *KafkaSource.java* para que contivesse um formulário HTML simples, como no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="91bef-200">For testing purposes, you could modify your *KafkaSource.java* so that it contains a simple HTML form like the following example:</span></span>
> 
> ```java
> package com.wingtiptoys.kafka;
>    
> import org.springframework.beans.factory.annotation.Autowired;
> import org.springframework.cloud.stream.annotation.EnableBinding;
> import org.springframework.cloud.stream.messaging.Source;
> import org.springframework.messaging.support.GenericMessage;
> import org.springframework.web.bind.annotation.GetMapping;
> import org.springframework.web.bind.annotation.PostMapping;
> import org.springframework.web.bind.annotation.RequestBody;
> import org.springframework.web.bind.annotation.RequestParam;
> import org.springframework.web.bind.annotation.RestController;
> 
> @EnableBinding(Source.class)
> @RestController
> public class KafkaSource {
>   @Autowired
>   private Source source;
> 
>   @GetMapping("/")
>   public String sendForm() {
>     return "<html><body>" +
>       "<form action=\"/messages\" method=\"post\">" +
>       "<input type=\"text\" name=\"text\">" +
>       "<input type=\"submit\">" +
>       "</form></body><html>";
>     }
> 
>   @PostMapping("/messages")
>   public String sendMessage(@RequestBody String message) {
>     this.source.output().send(new GenericMessage<>(message));
>     return message;
>   }
> }
> ```
> 
> <span data-ttu-id="91bef-201">Isso permitiria o uso de um navegador da Web para testar seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="91bef-201">This will allow you to use a web browser to test your application:</span></span>
> 
> ![Testando o aplicativo em um navegador da Web][TB01]
> 
> <span data-ttu-id="91bef-203">Quando você envia o formulário, o aplicativo exibe os resultados:</span><span class="sxs-lookup"><span data-stu-id="91bef-203">When you submit the form, your application will display the results:</span></span>
> 
> ![Resposta do aplicativo em um navegador da Web][TB02]
> 

## <a name="next-steps"></a><span data-ttu-id="91bef-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91bef-205">Next steps</span></span>

<span data-ttu-id="91bef-206">Para obter mais informações sobre o suporte do Azure para o Event Hub Stream Binder e para o Apache Kafka, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="91bef-206">For more information about Azure support for Event Hub Stream Binder and Apache Kafka, see the following articles:</span></span>

* [<span data-ttu-id="91bef-207">O que é Hub de Eventos do Azure?</span><span class="sxs-lookup"><span data-stu-id="91bef-207">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="91bef-208">Hubs de Eventos do Azure para Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="91bef-208">Azure Event Hubs for Apache Kafka</span></span>](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [<span data-ttu-id="91bef-209">Criar um namespace dos Hubs de Eventos e um hub de eventos usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="91bef-209">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="91bef-210">Criar hubs de eventos habilitados para Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="91bef-210">Create Apache Kafka enabled event hubs</span></span>](/azure/event-hubs/event-hubs-create-kafka-enabled)

<span data-ttu-id="91bef-211">Para obter mais informações sobre como usar o Azure com Java, veja [Azure para desenvolvedores Java] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="91bef-211">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="91bef-212">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="91bef-212">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="91bef-213">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="91bef-213">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="91bef-214">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="91bef-214">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="91bef-215">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="91bef-215">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
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

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-03.png

[TB01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-01.png
[TB02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-02.png