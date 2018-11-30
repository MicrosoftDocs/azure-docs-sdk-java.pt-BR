---
title: Como usar o Inicializador do Spring Boot com a API do Armazenamento do Azure
description: Saiba como configurar um aplicativo iniciador do Spring Boot com a API do Armazenamento do Azure.
services: storage
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 94f7b1148d9282d33bc67da0e0d97a284a81d4d4
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339050"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-storage-api"></a><span data-ttu-id="c2d0e-103">Como usar o Inicializador do Spring Boot com a API do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c2d0e-103">How to use the Spring Boot Starter with the Azure Storage API</span></span>

## <a name="overview"></a><span data-ttu-id="c2d0e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c2d0e-104">Overview</span></span>

<span data-ttu-id="c2d0e-105">Este artigo orienta em relação à criação de um aplicativo personalizado usando o **Spring Initializr** e depois usando esse aplicativo para acessar o Armazenamento do Azure usando a API do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-105">This article walks you through creating a custom application using the **Spring Initializr**, and then using that application to access Azure storage by using the Azure Storage API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2d0e-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c2d0e-106">Prerequisites</span></span>

<span data-ttu-id="c2d0e-107">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="c2d0e-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para uma [conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2d0e-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c2d0e-109">A[CLI (interface de linha de comando) do Azure](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c2d0e-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="c2d0e-110">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c2d0e-111">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c2d0e-112">[Maven](http://maven.apache.org/) do Apache, versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-112">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="c2d0e-113">Criar um aplicativo personalizado usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="c2d0e-113">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="c2d0e-114">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-114">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="c2d0e-115">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-115">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Opções básicas do Initializr Basic](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > <span data-ttu-id="c2d0e-117">O Spring Initializr usará os nomes de **Grupo** e **Artefato** para criar o nome do pacote, por exemplo: *com.contoso.wingtiptoysdemo*.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-117">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.contoso.wingtiptoysdemo*.</span></span>
   >

1. <span data-ttu-id="c2d0e-118">Role para baixo, até a seção **Azure** e marque a caixa do **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-118">Scroll down to the **Azure** section and check the box for **Azure Storage**.</span></span>

   ![Opções do Spring Initilializr Completo](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. <span data-ttu-id="c2d0e-120">Role até a parte inferior da página e clique no botão **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-120">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Opções do Spring Initilializr Completo](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. <span data-ttu-id="c2d0e-122">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-122">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixe o projeto personalizado do Spring Boot](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="c2d0e-124">Entre no Azure e selecione a assinatura a ser usada</span><span class="sxs-lookup"><span data-stu-id="c2d0e-124">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="c2d0e-125">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-125">Open a command prompt.</span></span>

1. <span data-ttu-id="c2d0e-126">Entre em sua conta do Azure usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-126">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="c2d0e-127">Siga as instruções na tela para concluir o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-127">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="c2d0e-128">Liste suas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-128">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="c2d0e-129">O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-129">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="c2d0e-130">Especifique o GUID para a conta que quer usar no Azure; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-130">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="c2d0e-131">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c2d0e-131">Create an Azure Storage account</span></span>

1. <span data-ttu-id="c2d0e-132">Crie um grupo de recursos para os recursos do Azure que serão usados neste artigo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-132">Create a resource group for the Azure resources you will use in this article; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="c2d0e-133">Em que:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-133">Where:</span></span>

   | <span data-ttu-id="c2d0e-134">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c2d0e-134">Parameter</span></span> | <span data-ttu-id="c2d0e-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d0e-135">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="c2d0e-136">Especifica um nome exclusivo para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-136">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="c2d0e-137">Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual seu grupo de recursos será hospedado.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-137">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="c2d0e-138">A CLI do Azure exibirá os resultados da criação do grupo de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-138">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

2. <span data-ttu-id="c2d0e-139">Crie uma conta de armazenamento do Azure no grupo de recursos para seu aplicativo Spring Boot. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-139">Create an Azure storage account in the in the resource group for your Spring Boot app; for example:</span></span>
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   <span data-ttu-id="c2d0e-140">Em que:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-140">Where:</span></span>

   | <span data-ttu-id="c2d0e-141">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c2d0e-141">Parameter</span></span> | <span data-ttu-id="c2d0e-142">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="c2d0e-142">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="c2d0e-143">Especifica um nome exclusivo para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-143">Specifies a unique name for your storage account.</span></span> |
   | `resource-group` | <span data-ttu-id="c2d0e-144">Especifica o nome do grupo de recursos que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-144">Specifies the name of the resource group group you created in the previous step.</span></span> |
   | `location` | <span data-ttu-id="c2d0e-145">Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual sua conta de armazenamento será hospedada.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-145">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your storage account will be hosted.</span></span> |
   | `sku` | <span data-ttu-id="c2d0e-146">Especifica um dos seguintes: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-146">Specifies one of the following: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span></span> |

   <span data-ttu-id="c2d0e-147">O Azure retornará uma cadeia de caracteres JSON longa, a qual contém o estado de provisionamento. Por exemplo: |</span><span class="sxs-lookup"><span data-stu-id="c2d0e-147">Azure will return a long JSON string which contains the provisioning state; for example: |</span></span>

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "identity": null,
     "kind": "Storage"
       ...
       ... (A long list of values will be displayed here.)
       ...
     "statusOfPrimary": "available",
     "statusOfSecondary": null,
     "tags": {},
     "type": "Microsoft.Storage/storageAccounts"
   }
   ```

3. <span data-ttu-id="c2d0e-148">Recuperar a cadeia de conexão para sua conta de armazenamento. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-148">Retrieve the connection string for your storage account; for example:</span></span>
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   <span data-ttu-id="c2d0e-149">Em que:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-149">Where:</span></span>

   | <span data-ttu-id="c2d0e-150">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c2d0e-150">Parameter</span></span> | <span data-ttu-id="c2d0e-151">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="c2d0e-151">Description</span></span> |
   | ---|---|
   | `name` | <span data-ttu-id="c2d0e-152">Especifica um nome exclusivo da conta de armazenamento que você criou nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-152">Specifies a unique name of the storage account you created in previous steps.</span></span> |
   | `resource-group` | <span data-ttu-id="c2d0e-153">Especifica o nome do grupo de recursos que você criou em etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-153">Specifies the name of the resource group you created in previous steps.</span></span> |

   <span data-ttu-id="c2d0e-154">O Azure retornará uma cadeia de caracteres JSON que contém a cadeia de conexão para sua conta de armazenamento. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-154">Azure will return a JSON string which contains the connection string for your storage account; for example:</span></span>

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="c2d0e-155">Configurar e compilar seu aplicativo Spring Boot</span><span class="sxs-lookup"><span data-stu-id="c2d0e-155">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="c2d0e-156">Extraia em um diretório os arquivos do projeto baixado.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-156">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="c2d0e-157">Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-157">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="c2d0e-158">Adicione a chave da sua conta de armazenamento. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-158">Add the key for your storage account; for example:</span></span>
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. <span data-ttu-id="c2d0e-159">Navegue até a pasta */src/main/java/com/example/wingtiptoysdemo* no seu projeto e abra o arquivo *WingtiptoysdemoApplication.java* em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-159">Navigate to the */src/main/java/com/example/wingtiptoysdemo* folder in your project and open the *WingtiptoysdemoApplication.java* file in a text editor.</span></span>

1. <span data-ttu-id="c2d0e-160">Substitua o código existente do Java com o exemplo a seguir, o qual lista os blobs em um contêiner:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-160">Replace the existing Java code with the following example that lists the blobs in a container:</span></span>

   ```java
   package com.example.wingtiptoysdemo;

   import com.microsoft.azure.storage.*;
   import com.microsoft.azure.storage.blob.*;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   import java.net.URISyntaxException;

   @SpringBootApplication
   public class WingtiptoysdemoApplication implements CommandLineRunner {

      @Autowired
      private CloudStorageAccount cloudStorageAccount;

      final String containerName = "mycontainer";

      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysdemoApplication.class, args);
      }

      public void run(String... var1)
             throws URISyntaxException, StorageException {
          // Create a container (if it does not exist).
          createContainerIfNotExists(containerName);
          // Upload a blob to the container.
          uploadTextBlob(containerName);
      }

      private void createContainerIfNotExists(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Create the container if it does not exist.
            container.createIfNotExists();
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }

      private void uploadTextBlob(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Get a blob reference for a text file.
            CloudBlockBlob blob = container.getBlockBlobReference("test.txt");
            // Upload some text into the blob.
            blob.uploadText("Hello World!");
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }
   }
   ```
   > [!NOTE]
   >
   > <span data-ttu-id="c2d0e-161">Os exemplo acima transmite automaticamente as configurações do armazenamento de conta que você definiu no arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="c2d0e-161">The above example autowires the storage account settings that you defined in the *application.properties* file.</span></span>
   >

1. <span data-ttu-id="c2d0e-162">Compile e execute o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-162">Compile and run the application:</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

   <span data-ttu-id="c2d0e-163">O aplicativo criará um contêiner e carregará um arquivo de texto como um blob ao contêiner, o qual será listado na sua conta de armazenamento no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c2d0e-163">The application will create a container and upload a text file as a blob to the container, which will be listed under your storage account in the [Azure portal](https://portal.azure.com).</span></span>

   ![Listar blobs no portal do Azure](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > <span data-ttu-id="c2d0e-165">Quando você compila seu aplicativo, a seguinte mensagem de erro poderá ser exibida:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-165">When you compile your application, you might see the following error message:</span></span>
   > 
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] BUILD FAILURE`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] Total time: 2.616 s`<br/>
   > `[INFO] Finished at: 2017-11-11T13:14:15Z`<br/>
   > `[INFO] Final Memory: 26M/213M`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2`<br/>
   > `.18.1:test (default-test) on project wingtiptoysdemo: Execution default-test of`<br/>
   > `goal org.apache.maven.plugins:maven-surefire-plugin:2.18.1:test failed: The for`<br/>
   > `ked VM terminated without properly saying goodbye. VM crash or System.exit called?`<br/>
   > `[ERROR] Command was /bin/sh -c cd /home/robert/SpringBoot/wingtiptoysdemo && /u`<br/>
   > `sr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar /home/robert/SpringBoot/wingt`<br/>
   > `iptoysdemo/target/surefire/surefirebooter6371623993063346766.jar /home/robert/S`<br/>
   > `pringBoot/wingtiptoysdemo/target/surefire/surefire5107893623933537917tmp /home/`<br/>
   > `robert/SpringBoot/wingtiptoysdemo/target/surefire/surefire_01414159391084128068tmp`<br/>
   > `[ERROR] -> [Help 1]`<br/>
   > 
   > <span data-ttu-id="c2d0e-166">Se isso acontecer, talvez queira desabilitar teste do Maven Surefire. Para isso, adicione a seguinte entrada de plug-in no seu arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-166">If this happens, you might want to disable the Maven Surefire testing; to do so, add the following plugin entry in your *pom.xml* file:</span></span>
   > 
   > ```xml
   > <plugin>
   >   <groupId>org.apache.maven.plugins</groupId>
   >   <artifactId>maven-surefire-plugin</artifactId>
   >   <version>2.20.1</version>
   >   <configuration>
   >     <skipTests>true</skipTests>
   >   </configuration>
   > </plugin>
   > ```
   > 

## <a name="next-steps"></a><span data-ttu-id="c2d0e-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2d0e-167">Next steps</span></span>

<span data-ttu-id="c2d0e-168">Para obter mais informações sobre os iniciadores adicionais do Spring Boot disponíveis para o Microsoft Azure, consulte [Iniciadores do Spring Boot para o Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="c2d0e-168">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="c2d0e-169">Para obter informações adicionais sobre como integrar a funcionalidade do Azure em seus aplicativos baseados no Spring, consulte [Estrutura do Spring no Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="c2d0e-169">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="c2d0e-170">Para obter informações detalhadas sobre APIs adicionais do armazenamento do Azure adicional que podem ser chamadas de seus aplicativos Spring Boot, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="c2d0e-170">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="c2d0e-171">Como usar o armazenamento do Blob do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="c2d0e-171">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="c2d0e-172">Como usar o armazenamento de Fila do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="c2d0e-172">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="c2d0e-173">Como usar o armazenamento de Tabela do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="c2d0e-173">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="c2d0e-174">Como usar o armazenamento de Arquivo do Azure a partir do Java</span><span class="sxs-lookup"><span data-stu-id="c2d0e-174">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)
