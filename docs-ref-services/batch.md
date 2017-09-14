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
# <a name="azure-batch-libraries-for-java"></a><span data-ttu-id="76f7d-104">Bibliotecas do Lote do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="76f7d-104">Azure Batch libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="76f7d-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="76f7d-105">Overview</span></span>

<span data-ttu-id="76f7d-106">Execute aplicativos paralelos em grande escala e aplicativos de computação de alto desempenho com eficiência na nuvem com o [Lote do Azure](/azure/batch/batch-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="76f7d-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>   

<span data-ttu-id="76f7d-107">Para se familiarizar com o Lote do Azure, consulte [Criar uma conta de Lote com o portal do Azure](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="76f7d-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="client-library"></a><span data-ttu-id="76f7d-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="76f7d-108">Client library</span></span>

<span data-ttu-id="76f7d-109">As bibliotecas de cliente do Lote do Azure permitem configurar nós de computação e pools, definir tarefas e configurá-los para execução em trabalhos e configurar um gerenciador de trabalho para controlar e monitorar a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="76f7d-109">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="76f7d-110">[Saiba mais](/azure/batch/batch-api-basics) sobre como usar esses objetos para executar soluções de computação paralela em grande escala.</span><span class="sxs-lookup"><span data-stu-id="76f7d-110">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

<span data-ttu-id="76f7d-111">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="76f7d-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="76f7d-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="76f7d-112">Example</span></span>

<span data-ttu-id="76f7d-113">Configurar um conjunto de nós de computação do Linux em uma conta de lote:</span><span class="sxs-lookup"><span data-stu-id="76f7d-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="76f7d-114">Explorar as APIs de Cliente</span><span class="sxs-lookup"><span data-stu-id="76f7d-114">Explore the Client APIs</span></span>](/java/api/overview/azure/batch/clientlibrary)


## <a name="management-api"></a><span data-ttu-id="76f7d-115">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="76f7d-115">Management API</span></span>

<span data-ttu-id="76f7d-116">Use as bibliotecas de gerenciamento do Lote do Azure para criar e excluir contas em lotes, ler e regenerar chaves de conta de lote e gerenciar o armazenamento de conta do lote.</span><span class="sxs-lookup"><span data-stu-id="76f7d-116">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

<span data-ttu-id="76f7d-117">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="76f7d-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="76f7d-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="76f7d-118">Example</span></span>

<span data-ttu-id="76f7d-119">Criar uma conta de Lote do Azure e configurar um novo aplicativo e uma conta de armazenamento do Azure para ela.</span><span class="sxs-lookup"><span data-stu-id="76f7d-119">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

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
> [<span data-ttu-id="76f7d-120">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="76f7d-120">Explore the Management APIs</span></span>](/java/api/overview/azure/batch/managementapi)


## <a name="samples"></a><span data-ttu-id="76f7d-121">Exemplos</span><span class="sxs-lookup"><span data-stu-id="76f7d-121">Samples</span></span>

<span data-ttu-id="76f7d-122">[Gerenciar contas de Lote][1]</span><span class="sxs-lookup"><span data-stu-id="76f7d-122">[Manage Batch accounts][1]</span></span>   

<span data-ttu-id="76f7d-123">Explore mais [exemplos de código Java para o Lote do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="76f7d-123">Explore more [sample Java code for Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) you can use in your apps.</span></span>

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts