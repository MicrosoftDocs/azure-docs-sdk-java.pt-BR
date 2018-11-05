---
title: Bibliotecas do Armazenamento Azure para Java
description: ''
keywords: Azure, Java, SDK, API, Armazenamento
author: douge
ms.author: seguler
manager: dineshm
ms.date: 10/29/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 68a5fdbf8e2fbfe83f9ea09112d64488e0c11d08
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235214"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="f67f3-103">Bibliotecas do Armazenamento Azure para Java</span><span class="sxs-lookup"><span data-stu-id="f67f3-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="f67f3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f67f3-104">Overview</span></span>

<span data-ttu-id="f67f3-105">Ler e gravar, dados de blob (objeto), arquivos e mensagens de aplicativos Java com o [Armazenamento do Azure](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="f67f3-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="f67f3-106">Para começar a usar o Armazenamento do Azure, veja [Como usar o armazenamento de Blobs do SDK do Java v7](/azure/storage/blobs/storage-quickstart-blobs-java).</span><span class="sxs-lookup"><span data-stu-id="f67f3-106">To get started with Azure Storage, see [How to use Blob storage from Java SDK v7](/azure/storage/blobs/storage-quickstart-blobs-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="f67f3-107">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="f67f3-107">Client library</span></span>

<span data-ttu-id="f67f3-108">Use uma chave compartilhada, token SAS ou um token OAuth do Azure Active Directory para autorização com os serviços de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f67f3-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="f67f3-109">Em seguida, use classes e métodos de bibliotecas de cliente para trabalhar com blob, arquivo ou armazenamento de filas.</span><span class="sxs-lookup"><span data-stu-id="f67f3-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="f67f3-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f67f3-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="f67f3-111">**Dependência para V7 do SDK de Armazenamento do Azure herdado**:</span><span class="sxs-lookup"><span data-stu-id="f67f3-111">**Dependency for the legacy Azure Storage SDK v7**:</span></span>
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="f67f3-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f67f3-112">Example</span></span>

<span data-ttu-id="f67f3-113">Gravar um arquivo de imagem do sistema de arquivos local em um novo blob em um contêiner de blob de Armazenamento do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="f67f3-113">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f67f3-114">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="f67f3-114">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="f67f3-115">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="f67f3-115">Management API</span></span>

<span data-ttu-id="f67f3-116">Criar e gerenciar contas de Armazenamento do Azure e as chaves de conexão com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="f67f3-116">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="f67f3-117">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f67f3-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="f67f3-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="f67f3-118">Example</span></span>

<span data-ttu-id="f67f3-119">Criar uma nova conta de Armazenamento do Azure em sua assinatura e recuperar suas chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="f67f3-119">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="f67f3-120">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="f67f3-120">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="f67f3-121">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f67f3-121">Samples</span></span>

<span data-ttu-id="f67f3-122">[SDK de Armazenamento do Azure para Java](https://github.com/azure/azure-storage-java)
[Ler e gravar objetos no armazenamento de Blobs](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="f67f3-122">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="f67f3-123">Ler e gravar mensagens com filas</span><span class="sxs-lookup"><span data-stu-id="f67f3-123">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
