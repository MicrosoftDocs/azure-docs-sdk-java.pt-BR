---
title: Bibliotecas do Lote do Azure para Java
description: "Documentação de referência para as bibliotecas do Lote de Java"
keywords: "Azure, Java, SDK, API, Lote, processamento, agendamento, execução longa"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: ebf86e358ff541632e2d1f9503ebae593bdbdb3c
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-batch-libraries-for-java"></a>Bibliotecas do Lote do Azure para Java

## <a name="overview"></a>Visão geral

Execute aplicativos paralelos em grande escala e aplicativos de computação de alto desempenho com eficiência na nuvem com o [Lote do Azure](/azure/batch/batch-technical-overview).   

Para se familiarizar com o Lote do Azure, consulte [Criar uma conta de Lote com o portal do Azure](/azure/batch/batch-account-create-portal).

## <a name="client-library"></a>Biblioteca do cliente

As bibliotecas de cliente do Lote do Azure permitem configurar nós de computação e pools, definir tarefas e configurá-los para execução em trabalhos e configurar um gerenciador de trabalho para controlar e monitorar a execução do trabalho. [Saiba mais](/azure/batch/batch-api-basics) sobre como usar esses objetos para executar soluções de computação paralela em grande escala.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Configurar um conjunto de nós de computação do Linux em uma conta de lote:

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [Explorar as APIs de Cliente](/java/api/overview/azure/batch/clientlibrary)


## <a name="management-api"></a>API de Gerenciamento

Use as bibliotecas de gerenciamento do Lote do Azure para criar e excluir contas em lotes, ler e regenerar chaves de conta de lote e gerenciar o armazenamento de conta do lote.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="example"></a>Exemplo

Criar uma conta de Lote do Azure e configurar um novo aplicativo e uma conta de armazenamento do Azure para ela.

```java
BatchAccount batchAccount = azure.batchAccounts().define("newBatchAcct")
    .withRegion(Region.US_EAST)
    .withNewResourceGroup("myResourceGroup")
    .defineNewApplication("batchAppName")
        .defineNewApplicationPackage(applicationPackageName)
        .withAllowUpdates(true)
        .withDisplayName(applicationDisplayName)
        .attach()
    .withNewStorageAccount("batchStorageAcct")
    .create();
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/batch/managementapi)


## <a name="samples"></a>Exemplos

[Gerenciar contas de Lote][1]   

Explore mais [exemplos de código Java para o Lote do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) que você pode usar em seus aplicativos.

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts