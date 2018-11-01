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
ms.openlocfilehash: fba48dfa04f223dce72a0ee54da967565ebd3687
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235212"
---
# <a name="azure-storage-libraries-for-java"></a>Bibliotecas do Armazenamento Azure para Java

## <a name="overview"></a>Visão geral

Ler e gravar, dados de blob (objeto), arquivos e mensagens de aplicativos Java com o [Armazenamento do Azure](/azure/storage/storage-introduction).

Para começar a usar o Armazenamento do Azure, consulte [Como usar o armazenamento de Blob do Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).

## <a name="client-library"></a>Biblioteca do cliente

Use uma chave compartilhada, token SAS ou um token OAuth do Azure Active Directory para autorização com os serviços de Armazenamento do Azure. Em seguida, use classes e métodos de bibliotecas de cliente para trabalhar com blob, arquivo ou armazenamento de filas. 

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.   

**Dependência para serviço Blob**:
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
    <version>10.1.0</version>
</dependency>
```

**Dependência para serviço Fila**:
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-queue</artifactId>
    <version>10.0.0-Preview</version>
</dependency>
```


### <a name="example"></a>Exemplo

Gravar um arquivo de imagem do sistema de arquivos local em um novo blob em um contêiner de blob de Armazenamento do Azure existente.


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
> [Explorar as APIs de cliente](/java/api/overview/azure/storage/client)

## <a name="management-api"></a>API de gerenciamento

Criar e gerenciar contas de Armazenamento do Azure e as chaves de conexão com a API de gerenciamento.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a>Exemplo

Criar uma nova conta de Armazenamento do Azure em sua assinatura e recuperar suas chaves de acesso.

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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/storage/management)


## <a name="samples"></a>Exemplos

[SDK de Armazenamento do Azure para Java](https://github.com/azure/azure-storage-java)
[Ler e gravar objetos no armazenamento de Blobs](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart)   
[Ler e gravar mensagens com filas](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
