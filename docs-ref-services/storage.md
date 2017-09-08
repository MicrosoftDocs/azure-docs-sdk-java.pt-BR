---
title: Bibliotecas do Armazenamento Azure para Java
description: 
keywords: Azure, Java, SDK, API, Armazenamento
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 7c8b6958d5e2892f35af8771d9d53eda28c430ef
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
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
    <version>5.3.1</version>
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
> [Explorar as APIs de Cliente](/java/api/overview/azure/storage/clientlibrary)

## <a name="management-api"></a>API de Gerenciamento

Criar e gerenciar contas de Armazenamento do Azure e as chaves de conexão com a API de gerenciamento.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.1.2</version>
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
> [Explorar as APIs de Gerenciamento](/java/api/overview/azure/storage/managementapi)


## <a name="samples"></a>Exemplos

[Gerenciar contas de Armazenamento do Azure](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)    
[Ler e gravar objetos no armazenamento de blob](https://github.com/Azure-Samples/storage-blob-java-getting-started)   
[Ler e gravar mensagens com filas](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
[Ler arquivos de armazenamento de blob em um aplicativo Web](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

Explorar mais [exemplos de código Java para o Armazenamento do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) que você pode usar em seus aplicativos.