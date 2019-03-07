---
title: Como usar o iniciador do Spring Boot para Armazenamento do Azure
description: Saiba como configurar um aplicativo inicializador do Spring Boot com o inicializador do Armazenamento do Azure.
services: storage
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: a1f35df5939a51fa5ce50c29752226b6c7649a9d
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335379"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="3af2d-103">Como usar o iniciador do Spring Boot para Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3af2d-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="3af2d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3af2d-104">Overview</span></span>

<span data-ttu-id="3af2d-105">Este artigo explica como criar um aplicativo personalizado usando o **Spring Initializr**, como adicionar o iniciador do armazenamento do Azure ao aplicativo e como usá-lo para carregar um blob em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af2d-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3af2d-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3af2d-106">Prerequisites</span></span>

<span data-ttu-id="3af2d-107">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="3af2d-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para uma [conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3af2d-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3af2d-109">A[CLI (interface de linha de comando) do Azure](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3af2d-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="3af2d-110">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="3af2d-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="3af2d-111">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="3af2d-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="3af2d-112">[Maven](http://maven.apache.org/) do Apache, versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3af2d-112">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="3af2d-113">É necessário o Spring Boot versão 2.0 ou posterior para concluir as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3af2d-113">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="3af2d-114">Criar uma conta do Armazenamento do Azure e um contêiner de blob para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="3af2d-114">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="3af2d-115">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="3af2d-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="3af2d-116">Clique em **+Criar um recurso**, em **Armazenamento**e clique em **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="3af2d-116">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Criar uma Conta de Armazenamento do Azure][IMG01]

1. <span data-ttu-id="3af2d-118">Na página **Criar Namespace**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3af2d-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="3af2d-119">Insira um **Nome** exclusivo, que se tornará parte do URI da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3af2d-119">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="3af2d-120">Por exemplo: se você inseriu **wingtiptoysstorage** como o **Nome**, o URI será *wingtiptoysstorage.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="3af2d-120">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="3af2d-121">Escolha **Armazenamento de Blobs** como o **Tipo de conta**.</span><span class="sxs-lookup"><span data-stu-id="3af2d-121">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="3af2d-122">Especifique o **Local** da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3af2d-122">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="3af2d-123">Escolha a **Assinatura** que você deseja usar para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3af2d-123">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="3af2d-124">Especifique se deseja criar um novo **Grupo de recursos** para a conta de armazenamento ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="3af2d-124">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Especificar opções da Conta de Armazenamento do Azure][IMG02]

1. <span data-ttu-id="3af2d-126">Quando você tiver especificado as opções listadas acima, clique em **Criar** para criar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3af2d-126">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="3af2d-127">Quando o portal do Azure tiver criado sua conta de armazenamento, clique em **Blobs** e em **+Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="3af2d-127">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Criar contêiner de blobs][IMG03]

1. <span data-ttu-id="3af2d-129">Insira um **Nome** para o contêiner de blob e depois clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3af2d-129">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Especificar opções do contêiner de blob][IMG04]

1. <span data-ttu-id="3af2d-131">O portal do Azure lista seu contêiner de blob depois que ele for criado.</span><span class="sxs-lookup"><span data-stu-id="3af2d-131">The Azure portal will list your blob container after is has been created.</span></span>

   ![Revisando a lista de contêineres de blob][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="3af2d-133">Criar um aplicativo Spring Boot simples com o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="3af2d-133">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="3af2d-134">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="3af2d-134">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="3af2d-135">Especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="3af2d-135">Specify the following options:</span></span>

   * <span data-ttu-id="3af2d-136">Gere um projeto **Maven** com **Java**.</span><span class="sxs-lookup"><span data-stu-id="3af2d-136">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="3af2d-137">Especifique uma versão **Spring Boot** igual ou maior que 2.0.</span><span class="sxs-lookup"><span data-stu-id="3af2d-137">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="3af2d-138">Especifique os nomes de **Grupo** e **Artefato** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3af2d-138">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="3af2d-139">Adicione a dependência da **Web**.</span><span class="sxs-lookup"><span data-stu-id="3af2d-139">Add the **Web** dependency.</span></span>

      ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="3af2d-141">O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote, por exemplo, *com.wintiptoys.storage*.</span><span class="sxs-lookup"><span data-stu-id="3af2d-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="3af2d-142">Quando você tiver especificado as opções listadas acima, clique em **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="3af2d-142">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="3af2d-143">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="3af2d-143">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixar projeto do Spring][SI02]

1. <span data-ttu-id="3af2d-145">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="3af2d-145">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="3af2d-146">Configurar o aplicativo Spring Boot para usar o Iniciador do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3af2d-146">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="3af2d-147">Localize o arquivo *pom.xml* no diretório-raiz do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-147">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="3af2d-148">-ou-</span><span class="sxs-lookup"><span data-stu-id="3af2d-148">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="3af2d-149">Abra o arquivo *pom.xml* em um editor de texto e adicione o iniciador do Spring Cloud Azure Storage à lista de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="3af2d-149">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Editar o arquivo pom.xml][SI03]

1. <span data-ttu-id="3af2d-151">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="3af2d-151">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="3af2d-152">Criar um arquivo de credencial do Azure</span><span class="sxs-lookup"><span data-stu-id="3af2d-152">Create an Azure Credential File</span></span>

1. <span data-ttu-id="3af2d-153">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="3af2d-153">Open a command prompt.</span></span>

1. <span data-ttu-id="3af2d-154">Navegue até o diretório de *recursos* do aplicativo Spring Boot, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-154">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="3af2d-155">-ou-</span><span class="sxs-lookup"><span data-stu-id="3af2d-155">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="3af2d-156">Entre na sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="3af2d-156">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="3af2d-157">Liste suas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="3af2d-157">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="3af2d-158">O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-158">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="3af2d-159">Especifique o GUID para a assinatura que quer usar no Azure; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-159">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="3af2d-160">Crie seu arquivo de credencial do Azure:</span><span class="sxs-lookup"><span data-stu-id="3af2d-160">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="3af2d-161">Esse comando criará um arquivo *my.azureauth* no diretório *recursos* com conteúdo semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-161">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="3af2d-162">Configurar o aplicativo Spring Boot para usar sua conta do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3af2d-162">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="3af2d-163">Localize *application.properties* no diretório *recursos* do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-163">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="3af2d-164">-ou-</span><span class="sxs-lookup"><span data-stu-id="3af2d-164">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

2. <span data-ttu-id="3af2d-165">Abra o arquivo *application.properties* em um editor de texto, adicione as seguintes linhas ao arquivo e substitua os valores de exemplo pelas propriedades adequadas para sua conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="3af2d-165">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="3af2d-166">Em que:</span><span class="sxs-lookup"><span data-stu-id="3af2d-166">Where:</span></span>

   |                   <span data-ttu-id="3af2d-167">Campo</span><span class="sxs-lookup"><span data-stu-id="3af2d-167">Field</span></span>                   |                                            <span data-ttu-id="3af2d-168">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="3af2d-168">Description</span></span>                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            <span data-ttu-id="3af2d-169">Especifica o arquivo de credencial do Azure que você criou anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3af2d-169">Specifies Azure credential file that you created earlier in this tutorial.</span></span>             |
   |    `spring.cloud.azure.resource-group`    |           <span data-ttu-id="3af2d-170">O nome do grupo de recursos do Azure que contém a conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af2d-170">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span>            |
   |        `spring.cloud.azure.region`        | <span data-ttu-id="3af2d-171">Especifica a região geográfica que você especificou quando criou a conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af2d-171">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   |   `spring.cloud.azure.storage.account`    |            <span data-ttu-id="3af2d-172">Especifica a conta do Armazenamento do Azure que você criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3af2d-172">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>             |


3. <span data-ttu-id="3af2d-173">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="3af2d-173">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="3af2d-174">Adicionar código de exemplo para implementar a funcionalidade básica do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3af2d-174">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="3af2d-175">Nesta seção, você criará as classes Java necessárias para armazenar um blob em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af2d-175">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="3af2d-176">Modificar a classe principal do aplicativo</span><span class="sxs-lookup"><span data-stu-id="3af2d-176">Modify the main application class</span></span>

1. <span data-ttu-id="3af2d-177">Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-177">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="3af2d-178">-ou-</span><span class="sxs-lookup"><span data-stu-id="3af2d-178">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="3af2d-179">Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-179">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class StorageApplication {
      public static void main(String[] args) {
         SpringApplication.run(StorageApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="3af2d-180">Salve e feche o arquivo Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="3af2d-180">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="3af2d-181">Adicionar uma classe de controlador da Web</span><span class="sxs-lookup"><span data-stu-id="3af2d-181">Add a web controller class</span></span>

1. <span data-ttu-id="3af2d-182">Crie um novo arquivo Java chamado *WebController.java* no diretório do pacote do aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-182">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="3af2d-183">-ou-</span><span class="sxs-lookup"><span data-stu-id="3af2d-183">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="3af2d-184">Abra o arquivo Java do controlador da Web em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-184">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.core.io.Resource;
   import org.springframework.core.io.WritableResource;
   import org.springframework.util.StreamUtils;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   import java.io.IOException;
   import java.io.OutputStream;
   import java.nio.charset.Charset;

   @RestController
   public class WebController {

      @Value("blob://test/myfile.txt")
      private Resource blobFile;

      @GetMapping(value = "/")
      public String readBlobFile() throws IOException {
         return StreamUtils.copyToString(
            this.blobFile.getInputStream(),
            Charset.defaultCharset()) + "\n";
      }

      @PostMapping(value = "/")
      public String writeBlobFile(@RequestBody String data) throws IOException {
         try (OutputStream os = ((WritableResource) this.blobFile).getOutputStream()) {
            os.write(data.getBytes());
         }
         return "File was updated.\n";
      }
   }
   ```

   <span data-ttu-id="3af2d-185">Em que a sintaxe `@Value("blob://[container]/[blob]")` define respectivamente os nomes do contêiner e do blob onde você deseja armazenar os dados.</span><span class="sxs-lookup"><span data-stu-id="3af2d-185">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="3af2d-186">Salve e feche o arquivo Java do controlador da Web.</span><span class="sxs-lookup"><span data-stu-id="3af2d-186">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="3af2d-187">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-187">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="3af2d-188">-ou-</span><span class="sxs-lookup"><span data-stu-id="3af2d-188">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="3af2d-189">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-189">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="3af2d-190">Quando seu aplicativo estiver em execução, você poderá usar *curl* para testá-lo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-190">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="3af2d-191"> a.</span><span class="sxs-lookup"><span data-stu-id="3af2d-191">a.</span></span> <span data-ttu-id="3af2d-192">Envie uma solicitação POST para atualizar o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-192">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="3af2d-193">Você deverá ver uma resposta indicando que o arquivo foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="3af2d-193">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="3af2d-194">b.</span><span class="sxs-lookup"><span data-stu-id="3af2d-194">b.</span></span> <span data-ttu-id="3af2d-195">Envie uma solicitação GET para verificar o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="3af2d-195">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="3af2d-196">Você deverá ver o texto "Olá, Mundo" publicado.</span><span class="sxs-lookup"><span data-stu-id="3af2d-196">You should see the "Hello World" text that you posted.</span></span>

## <a name="summary"></a><span data-ttu-id="3af2d-197">Resumo</span><span class="sxs-lookup"><span data-stu-id="3af2d-197">Summary</span></span>

<span data-ttu-id="3af2d-198">Nesse tutorial, você criou um novo aplicativo do Java usando o **[Spring Initializr]**, adicionou o iniciador do armazenamento do Azure ao aplicativo, em seguida, configurou o aplicativo para carregar um blob em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af2d-198">In this tutorial, you created a new Java application using the **[Spring Initializr]**, added the Azure storage starter to your application, and then configured your application to upload a blob to your Azure storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3af2d-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3af2d-199">Next steps</span></span>

<span data-ttu-id="3af2d-200">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af2d-200">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3af2d-201">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="3af2d-201">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="3af2d-202">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3af2d-202">Additional Resources</span></span>

<span data-ttu-id="3af2d-203">Para obter mais informações sobre os iniciadores adicionais do Spring Boot disponíveis para o Microsoft Azure, consulte [Iniciadores do Spring Boot para o Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3af2d-203">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="3af2d-204">Para obter informações detalhadas sobre APIs adicionais do armazenamento do Azure adicional que podem ser chamadas de seus aplicativos Spring Boot, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="3af2d-204">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="3af2d-205">Como usar o armazenamento do Blob do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="3af2d-205">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="3af2d-206">Como usar o armazenamento de Fila do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="3af2d-206">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="3af2d-207">Como usar o armazenamento de Tabela do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="3af2d-207">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="3af2d-208">Como usar o armazenamento de Arquivo do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="3af2d-208">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
