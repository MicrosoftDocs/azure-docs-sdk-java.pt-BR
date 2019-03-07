---
title: Bibliotecas do Armazenamento Azure para Java
description: ''
keywords: Azure, Java, SDK, API, Armazenamento
author: douge
ms.author: douge
manager: douge
ms.date: 10/19/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: ee54e92ee0084cd2fc5e827764cfe094434ea784
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335369"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="11a14-103">Bibliotecas do Armazenamento Azure para Java</span><span class="sxs-lookup"><span data-stu-id="11a14-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="11a14-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="11a14-104">Overview</span></span>

<span data-ttu-id="11a14-105">Ler e gravar, dados de blob (objeto), arquivos e mensagens de aplicativos Java com o [Armazenamento do Azure](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="11a14-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="11a14-106">Para começar a usar o Armazenamento do Azure, consulte [Como usar o armazenamento de Blob do Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span><span class="sxs-lookup"><span data-stu-id="11a14-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span></span>

## <a name="client-library"></a><span data-ttu-id="11a14-107">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="11a14-107">Client library</span></span>

<span data-ttu-id="11a14-108">Use uma chave compartilhada, token SAS ou um token OAuth do Azure Active Directory para autorização com os serviços de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="11a14-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="11a14-109">Em seguida, use classes e métodos de bibliotecas de cliente para trabalhar com blob, arquivo ou armazenamento de filas.</span><span class="sxs-lookup"><span data-stu-id="11a14-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="11a14-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="11a14-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="11a14-111">**Dependência para serviço Blob**:</span><span class="sxs-lookup"><span data-stu-id="11a14-111">**Dependency for Blob service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
    <version>10.1.0</version>
</dependency>
```

<span data-ttu-id="11a14-112">**Dependência para serviço Fila**:</span><span class="sxs-lookup"><span data-stu-id="11a14-112">**Dependency for Queue service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-queue</artifactId>
    <version>10.0.0-Preview</version>
</dependency>
```


### <a name="example"></a><span data-ttu-id="11a14-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="11a14-113">Example</span></span>

<span data-ttu-id="11a14-114">Gravar um arquivo de imagem do sistema de arquivos local em um novo blob em um contêiner de blob de Armazenamento do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="11a14-114">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Retrieve the credentials and initialize SharedKeyCredentials
String accountName = System.getenv("AZURE_STORAGE_ACCOUNT");
String accountKey = System.getenv("AZURE_STORAGE_ACCESS_KEY");

// Create a BlockBlobURL to run operations on Block Blobs. Alternatively create a ServiceURL, or ContainerURL for operations on Blob service, and Blob containers
SharedKeyCredentials creds = new SharedKeyCredentials(accountName, accountKey);

// We are using a default pipeline here, you can learn more about it at https://github.com/Azure/azure-storage-java/wiki/Azure-Storage-Java-V10-Overview
final BlockBlobURL blobURL = new BlockBlobURL(
    new URL("https://" + accountName + ".blob.core.windows.net/mycontainer/myimage.jpg"), 
        StorageURL.createPipeline(creds, new PipelineOptions())
);

AsynchronousFileChannel fileChannel = AsynchronousFileChannel.open(Paths.get("myimage.jpg"));
TransferManager.uploadFileToBlockBlob(fileChannel, blobURL,0, null).blockingGet();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="11a14-115">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="11a14-115">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="11a14-116">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="11a14-116">Management API</span></span>

<span data-ttu-id="11a14-117">Crie e gerencie contas do Armazenamento do Azure e chaves de conexão com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="11a14-117">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="11a14-118">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="11a14-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="11a14-119">Exemplo</span><span class="sxs-lookup"><span data-stu-id="11a14-119">Example</span></span>

<span data-ttu-id="11a14-120">Criar uma nova conta de Armazenamento do Azure em sua assinatura e recuperar suas chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="11a14-120">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

```java
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
        .withRegion(Region.US_EAST)
        .withNewResourceGroup(rgName)
        .create();

// get a list of storage account keys related to the account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="11a14-121">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="11a14-121">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="11a14-122">Exemplos</span><span class="sxs-lookup"><span data-stu-id="11a14-122">Samples</span></span>

<span data-ttu-id="11a14-123">[SDK de Armazenamento do Azure para Java](https://github.com/azure/azure-storage-java)
[Ler e gravar objetos no armazenamento de Blobs](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="11a14-123">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="11a14-124">Ler e gravar mensagens com filas</span><span class="sxs-lookup"><span data-stu-id="11a14-124">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
