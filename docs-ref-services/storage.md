---
title: Bibliotecas do Armazenamento Azure para Java
description: ''
keywords: Azure, Java, SDK, API, Armazenamento
author: douge
ms.author: douge
manager: douge
ms.date: 02/07/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: ec06e79374176b5a4795d27c5fbbb2260e65cd8c
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823649"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="63c9e-103">Bibliotecas do Armazenamento Azure para Java</span><span class="sxs-lookup"><span data-stu-id="63c9e-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="63c9e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="63c9e-104">Overview</span></span>

<span data-ttu-id="63c9e-105">Ler e gravar arquivos, dados de blob (objeto), pares chave-valor e mensagens de aplicativos Java com o [Armazenamento do Azure](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="63c9e-105">Read and write files, blob (object) data, key-value pairs, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="63c9e-106">Para começar a usar o Armazenamento do Azure, consulte [Como usar o armazenamento de Blob do Java](/azure/storage/storage-java-how-to-use-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="63c9e-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/storage-java-how-to-use-blob-storage).</span></span>

## <a name="client-library"></a><span data-ttu-id="63c9e-107">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="63c9e-107">Client library</span></span>

<span data-ttu-id="63c9e-108">Usar [cadeias de conexão](/azure/storage/storage-create-storage-account#manage-your-storage-account) para se conectar a uma conta de Armazenamento do Azure, em seguida, usar as classes e métodos das bibliotecas de cliente para trabalhar com armazenamento de blob, tabela, arquivo ou fila.</span><span class="sxs-lookup"><span data-stu-id="63c9e-108">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span> 

<span data-ttu-id="63c9e-109">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="63c9e-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="63c9e-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="63c9e-110">Example</span></span>

<span data-ttu-id="63c9e-111">Gravar um arquivo de imagem do sistema de arquivos local em um novo blob em um contêiner de blob de Armazenamento do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="63c9e-111">Write a image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
String storageConnectionString = "DefaultEndpointsProtocol=https;" + 
"AccountName=fabrikamblobstorage;" + 
"AccountKey=keyvalue;EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient serviceClient = account.createCloudBlobClient();
CloudBlobContainer container = serviceClient.getContainerReference(blobContainer);

// write a blob from a local filesystem path to the container as logo.png
CloudBlockBlob blob = container.getBlockBlobReference("logo.png");
blob.uploadFromFile("/Users/raisa/fabrikam.png");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="63c9e-112">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="63c9e-112">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="63c9e-113">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="63c9e-113">Management API</span></span>

<span data-ttu-id="63c9e-114">Criar e gerenciar contas de Armazenamento do Azure e as chaves de conexão com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="63c9e-114">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="63c9e-115">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="63c9e-115">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="63c9e-116">Exemplo</span><span class="sxs-lookup"><span data-stu-id="63c9e-116">Example</span></span>

<span data-ttu-id="63c9e-117">Criar uma nova conta de Armazenamento do Azure em sua assinatura e recuperar suas chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="63c9e-117">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="63c9e-118">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="63c9e-118">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="63c9e-119">Exemplos</span><span class="sxs-lookup"><span data-stu-id="63c9e-119">Samples</span></span>

<span data-ttu-id="63c9e-120">[Gerenciar contas de Armazenamento do Azure](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span><span class="sxs-lookup"><span data-stu-id="63c9e-120">[Manage Azure Storage accounts](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span></span>  
<span data-ttu-id="63c9e-121">[Ler e gravar objetos no armazenamento de blob](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="63c9e-121">[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span></span>  
<span data-ttu-id="63c9e-122">[Ler e gravar mensagens com filas](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="63c9e-122">[Read and write messages with queues](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span></span>  
[<span data-ttu-id="63c9e-123">Ler arquivos de armazenamento de blob em um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="63c9e-123">Read files from blob storage in a web app</span></span>](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

<span data-ttu-id="63c9e-124">Explorar mais [exemplos de código Java para o Armazenamento do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="63c9e-124">Explore more [sample Java code for Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) you can use in your apps.</span></span>
