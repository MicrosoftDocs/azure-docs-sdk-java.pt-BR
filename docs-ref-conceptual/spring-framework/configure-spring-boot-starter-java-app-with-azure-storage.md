---
title: Como usar o iniciador do Spring Boot para Armazenamento do Azure
description: Saiba como configurar um aplicativo inicializador do Spring Boot com o inicializador do Armazenamento do Azure.
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 1a219a066f0f89adbf3f541856b36b842520bfbb
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46505914"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="3db01-103">Como usar o iniciador do Spring Boot para Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3db01-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="3db01-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3db01-104">Overview</span></span>

<span data-ttu-id="3db01-105">Este artigo explica como criar um aplicativo personalizado usando o **Spring Initializr**, como adicionar o iniciador do armazenamento do Azure ao aplicativo e como usá-lo para carregar um blob em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db01-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3db01-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3db01-106">Prerequisites</span></span>

<span data-ttu-id="3db01-107">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="3db01-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="3db01-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para uma [conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3db01-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3db01-109">A[CLI (interface de linha de comando) do Azure](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3db01-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="3db01-110">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) atualizado, versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3db01-110">An up-to-date [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="3db01-111">[Maven](http://maven.apache.org/) do Apache, versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3db01-111">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="3db01-112">É necessário o Spring Boot versão 2.0 ou posterior para concluir as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3db01-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="3db01-113">Criar uma conta do Armazenamento do Azure e um contêiner de blob para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="3db01-113">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="3db01-114">Navegue até o portal do Azure em <https://portal.azure.com/> e entre.</span><span class="sxs-lookup"><span data-stu-id="3db01-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="3db01-115">Clique em **+Criar um recurso**, em **Armazenamento**e clique em **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="3db01-115">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Criar uma Conta de Armazenamento do Azure][IMG01]

1. <span data-ttu-id="3db01-117">Na página **Criar Namespace**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3db01-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="3db01-118">Insira um **Nome** exclusivo, que se tornará parte do URI da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3db01-118">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="3db01-119">Por exemplo: se você inseriu **wingtiptoysstorage** como o **Nome**, o URI será *wingtiptoysstorage.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="3db01-119">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="3db01-120">Escolha **Armazenamento de Blobs** como o **Tipo de conta**.</span><span class="sxs-lookup"><span data-stu-id="3db01-120">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="3db01-121">Especifique o **Local** da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3db01-121">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="3db01-122">Escolha a **Assinatura** que você deseja usar para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3db01-122">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="3db01-123">Especifique se deseja criar um novo **Grupo de recursos** para a conta de armazenamento ou escolher um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="3db01-123">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>
   
   ![Especificar opções de conta do Armazenamento do Azure][IMG02]

1. <span data-ttu-id="3db01-125">Quando você tiver especificado as opções listadas acima, clique em **Criar** para criar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3db01-125">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="3db01-126">Quando o portal do Azure tiver criado sua conta de armazenamento, clique em **Blobs** e em **+Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="3db01-126">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Criar contêiner de blobs][IMG03]

1. <span data-ttu-id="3db01-128">Insira um **Nome** para o contêiner de blob e depois clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3db01-128">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Especificar opções do contêiner de blob][IMG04]

1. <span data-ttu-id="3db01-130">O portal do Azure lista seu contêiner de blob depois que ele for criado.</span><span class="sxs-lookup"><span data-stu-id="3db01-130">The Azure portal will list your blob container after is has been created.</span></span>

   ![Revisando a lista de contêineres de blob][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="3db01-132">Criar um aplicativo Spring Boot simples com o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="3db01-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="3db01-133">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="3db01-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="3db01-134">Especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="3db01-134">Specify the following options:</span></span>

   * <span data-ttu-id="3db01-135">Gere um projeto **Maven** com **Java**.</span><span class="sxs-lookup"><span data-stu-id="3db01-135">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="3db01-136">Especifique uma versão **Spring Boot** igual ou maior que 2.0.</span><span class="sxs-lookup"><span data-stu-id="3db01-136">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="3db01-137">Especifique os nomes de **Grupo** e **Artefato** para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3db01-137">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="3db01-138">Adicione a dependência da **Web**.</span><span class="sxs-lookup"><span data-stu-id="3db01-138">Add the **Web** dependency.</span></span>

      ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="3db01-140">O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote, por exemplo, *com.wintiptoys.storage*.</span><span class="sxs-lookup"><span data-stu-id="3db01-140">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="3db01-141">Quando você tiver especificado as opções listadas acima, clique em **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="3db01-141">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="3db01-142">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="3db01-142">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixar projeto do Spring][SI02]

1. <span data-ttu-id="3db01-144">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="3db01-144">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="3db01-145">Configurar o aplicativo Spring Boot para usar o Iniciador do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3db01-145">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="3db01-146">Localize o arquivo *pom.xml* no diretório raiz do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-146">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="3db01-147">-ou-</span><span class="sxs-lookup"><span data-stu-id="3db01-147">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="3db01-148">Abra o arquivo *pom.xml* em um editor de texto e adicione o iniciador do Spring Cloud Azure Storage à lista de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="3db01-148">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Editar o arquivo pom.xml][SI03]

1. <span data-ttu-id="3db01-150">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="3db01-150">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="3db01-151">Criar um arquivo de credencial do Azure</span><span class="sxs-lookup"><span data-stu-id="3db01-151">Create an Azure Credential File</span></span>

1. <span data-ttu-id="3db01-152">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="3db01-152">Open a command prompt.</span></span>

1. <span data-ttu-id="3db01-153">Navegue até o diretório de *recursos* do aplicativo Spring Boot, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-153">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="3db01-154">-ou-</span><span class="sxs-lookup"><span data-stu-id="3db01-154">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="3db01-155">Entre na sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="3db01-155">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="3db01-156">Liste suas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="3db01-156">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="3db01-157">O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-157">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="3db01-158">Crie seu arquivo de credencial do Azure:</span><span class="sxs-lookup"><span data-stu-id="3db01-158">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="3db01-159">Esse comando criará um arquivo *my.azureauth* no diretório *recursos* com conteúdo semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-159">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="3db01-160">Configurar o aplicativo Spring Boot para usar sua conta do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3db01-160">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="3db01-161">Localize o *application.properties* no diretório *recursos* do aplicativo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-161">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="3db01-162">-ou-</span><span class="sxs-lookup"><span data-stu-id="3db01-162">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

1.  <span data-ttu-id="3db01-163">Abra o arquivo *application.properties* em um editor de texto, adicione as seguintes linhas ao arquivo e substitua os valores de exemplo pelas propriedades adequadas para sua conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="3db01-163">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="3db01-164">Em que:</span><span class="sxs-lookup"><span data-stu-id="3db01-164">Where:</span></span>
   | <span data-ttu-id="3db01-165">Campo</span><span class="sxs-lookup"><span data-stu-id="3db01-165">Field</span></span> | <span data-ttu-id="3db01-166">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="3db01-166">Description</span></span> |
   | ---|---|
   | `spring.cloud.azure.credential-file-path` | <span data-ttu-id="3db01-167">Especifica o arquivo de credencial do Azure que você criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3db01-167">Specifies Azure credential file that you created earlier in this tutorial.</span></span> |
   | `spring.cloud.azure.resource-group` | <span data-ttu-id="3db01-168">O nome do grupo de recursos do Azure que contém a conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db01-168">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span> |
   | `spring.cloud.azure.region` | <span data-ttu-id="3db01-169">Especifica a região geográfica que você especificou quando criou a conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db01-169">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   | `spring.cloud.azure.storage.account` | <span data-ttu-id="3db01-170">Especifica a conta do Armazenamento do Azure que você criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3db01-170">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>

1. <span data-ttu-id="3db01-171">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="3db01-171">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="3db01-172">Adicionar código de exemplo para implementar a funcionalidade básica do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3db01-172">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="3db01-173">Nesta seção, você criará as classes Java necessárias para armazenar um blob em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3db01-173">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="3db01-174">Modificar a classe principal do aplicativo</span><span class="sxs-lookup"><span data-stu-id="3db01-174">Modify the main application class</span></span>

1. <span data-ttu-id="3db01-175">Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-175">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="3db01-176">-ou-</span><span class="sxs-lookup"><span data-stu-id="3db01-176">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="3db01-177">Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="3db01-177">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="3db01-178">Salve e feche o arquivo Java do aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="3db01-178">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="3db01-179">Adicionar uma classe de controlador da Web</span><span class="sxs-lookup"><span data-stu-id="3db01-179">Add a web controller class</span></span>

1. <span data-ttu-id="3db01-180">Crie um novo arquivo Java chamado *WebController.java* no diretório do pacote do aplicativo; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-180">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="3db01-181">-ou-</span><span class="sxs-lookup"><span data-stu-id="3db01-181">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="3db01-182">Abra o arquivo Java do controlador da Web em um editor de texto e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="3db01-182">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

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
   
   <span data-ttu-id="3db01-183">Em que a sintaxe `@Value("blob://[container]/[blob]")` define respectivamente os nomes do contêiner e do blob onde você deseja armazenar os dados.</span><span class="sxs-lookup"><span data-stu-id="3db01-183">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="3db01-184">Salve e feche o arquivo Java do controlador da Web.</span><span class="sxs-lookup"><span data-stu-id="3db01-184">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="3db01-185">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-185">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="3db01-186">-ou-</span><span class="sxs-lookup"><span data-stu-id="3db01-186">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="3db01-187">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-187">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="3db01-188">Quando seu aplicativo estiver em execução, você poderá usar *curl* para testá-lo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3db01-188">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="3db01-189">a.</span><span class="sxs-lookup"><span data-stu-id="3db01-189">a.</span></span> <span data-ttu-id="3db01-190">Envie uma solicitação POST para atualizar o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="3db01-190">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="3db01-191">Você deverá ver uma resposta indicando que o arquivo foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="3db01-191">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="3db01-192">b.</span><span class="sxs-lookup"><span data-stu-id="3db01-192">b.</span></span> <span data-ttu-id="3db01-193">Envie uma solicitação GET para verificar o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="3db01-193">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="3db01-194">Você deverá ver o texto "Olá, Mundo" publicado.</span><span class="sxs-lookup"><span data-stu-id="3db01-194">You should see the "Hello World" text that you posted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3db01-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3db01-195">Next steps</span></span>

<span data-ttu-id="3db01-196">Para obter mais informações sobre os iniciadores adicionais do Spring Boot disponíveis para o Microsoft Azure, consulte [Iniciadores do Spring Boot para o Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3db01-196">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="3db01-197">Para obter informações adicionais sobre como integrar a funcionalidade do Azure em seus aplicativos baseados no Spring, consulte [Estrutura do Spring no Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="3db01-197">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="3db01-198">Para obter informações detalhadas sobre APIs adicionais do armazenamento do Azure adicional que podem ser chamadas de seus aplicativos Spring Boot, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="3db01-198">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="3db01-199">Como usar o armazenamento do Blob do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="3db01-199">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="3db01-200">Como usar o armazenamento de Fila do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="3db01-200">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="3db01-201">Como usar o armazenamento de Tabela do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="3db01-201">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="3db01-202">Como usar o armazenamento de Arquivo do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="3db01-202">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
