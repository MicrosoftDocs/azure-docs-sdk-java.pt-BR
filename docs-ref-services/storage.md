---
title: Bibliotecas do Armazenamento Azure para Java
description: 
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
ms.openlocfilehash: 3c7a3a1fcf2e97202e7f38f8df5acb6637fb4b47
ms.sourcegitcommit: 2ae0d99c02f4ad7efa9e3d3fbd1db7e9de20c6e7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="azure-storage-libraries-for-java"></a>Bibliotecas do Armazenamento Azure para Java

## <a name="overview"></a>Visão geral

Ler e gravar arquivos, dados de blob (objeto), pares chave-valor e mensagens de aplicativos Java com o [Armazenamento do Azure](/azure/storage/storage-introduction).

Para começar a usar o Armazenamento do Azure, consulte [Como usar o armazenamento de Blob do Java](/azure/storage/storage-java-how-to-use-blob-storage).

## <a name="client-library"></a>Biblioteca do cliente

Usar [cadeias de conexão](/azure/storage/storage-create-storage-account#manage-your-storage-account) para se conectar a uma conta de Armazenamento do Azure, em seguida, usar as classes e métodos das bibliotecas de cliente para trabalhar com armazenamento de blob, tabela, arquivo ou fila. 

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Gravar um arquivo de imagem do sistema de arquivos local em um novo blob em um contêiner de blob de Armazenamento do Azure existente.


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
> [Explorar as APIs de cliente](/java/api/overview/azure/storage/clientlibrary)

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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/storage/managementapi)


## <a name="samples"></a>Exemplos

[Gerenciar contas de Armazenamento do Azure](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)    
[Ler e gravar objetos no armazenamento de blob](https://github.com/Azure-Samples/storage-blob-java-getting-started)   
[Ler e gravar mensagens com filas](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
[Ler arquivos de armazenamento de blob em um aplicativo Web](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

Explorar mais [exemplos de código Java para o Armazenamento do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) que você pode usar em seus aplicativos.
