---
title: Bibliotecas do Azure para Java
description: Visão geral do gerenciamento do Azure e bibliotecas de serviço para Java
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892727"
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="339ae-104">Bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="339ae-104">Azure libraries for Java</span></span>

<span data-ttu-id="339ae-105">As bibliotecas do Azure para Java ajudam a gerenciar recursos do Azure e conectam-se aos serviços do seu código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="339ae-105">The Azure libraries for Java help you manage Azure resources and connect to services from your application code.</span></span> <span data-ttu-id="339ae-106">As bibliotecas estão disponíveis como [importações de Maven](java-sdk-azure-install.md) para uso em seus projetos de Java.</span><span class="sxs-lookup"><span data-stu-id="339ae-106">The libraries are available as [Maven imports](java-sdk-azure-install.md) for use in your Java projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="339ae-107">Gerenciar recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="339ae-107">Manage Azure resources</span></span>

<span data-ttu-id="339ae-108">Criar e gerenciar recursos do Azure a partir de aplicativos Java usando as [bibliotecas de gerenciamento do Azure para Java](java-sdk-azure-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="339ae-108">Create and manage Azure resources from your Java applications using the [Azure management libraries for Java](java-sdk-azure-get-started.md).</span></span> <span data-ttu-id="339ae-109">Use essas bibliotecas para criar seus próprios serviços e ferramentas de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="339ae-109">Use these libraries to build your own Azure automation tools and services.</span></span> 

<span data-ttu-id="339ae-110">Por exemplo, para criar uma VM do Linux, você deve escrever o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="339ae-110">For example, to create a Linux VM you would write the following code:</span></span>

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

<span data-ttu-id="339ae-111">Analise as [instruções de instalação](java-sdk-azure-install.md) para obter uma lista completa das bibliotecas e como importá-las para seus projetos e, em seguida, leia o [artigo de introdução](java-sdk-azure-get-started.md) para configurar a autenticação e executar o código de exemplo em relação a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="339ae-111">Review the [install instructions](java-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](java-sdk-azure-get-started.md) to set up your authentication and run sample code against your own Azure subscription.</span></span> 

## <a name="connect-to-azure-services"></a><span data-ttu-id="339ae-112">Conectar-se aos serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="339ae-112">Connect to Azure services</span></span>

<span data-ttu-id="339ae-113">Além de usar bibliotecas de Java para criar e gerenciar recursos no Azure, você também pode usar bibliotecas de Java para se conectar e usar esses recursos em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="339ae-113">In addition to using Java libraries to create and manage resources within Azure, you can also use Java libraries to connect  and use those resources in your apps.</span></span> <span data-ttu-id="339ae-114">Por exemplo, você pode atualizar um Banco de Dados SQL de tabela ou armazenar arquivos no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="339ae-114">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="339ae-115">Selecione a biblioteca necessária para um serviço específico na [lista completa das bibliotecas](java-sdk-azure-install.md) e visite a [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/) para ver os tutoriais e exemplos de código e obter ajuda para usá-las em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="339ae-115">Select the library you need for a particular service from the [complete list of libraries](java-sdk-azure-install.md) and visit the [Java developer center](https://azure.microsoft.com/develop/java/) for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="339ae-116">Por exemplo, para imprimir o conteúdo de cada blob em um contêiner de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="339ae-116">For example, to print out the contents of every blob in an Azure storage container:</span></span>

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a><span data-ttu-id="339ae-117">Referência e código de exemplo</span><span class="sxs-lookup"><span data-stu-id="339ae-117">Sample code and reference</span></span>

<span data-ttu-id="339ae-118">Os exemplos a seguir abordam tarefas comuns de automação com as bibliotecas de gerenciamento do Azure para Java e possuem códigos prontos para uso em seus próprios aplicativos:</span><span class="sxs-lookup"><span data-stu-id="339ae-118">The following samples cover common automation tasks with the Azure management libraries for Java and have code ready to use in your own apps:</span></span>

- [<span data-ttu-id="339ae-119">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="339ae-119">Virtual machines</span></span>](java-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="339ae-120">Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="339ae-120">Web apps</span></span>](java-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="339ae-121">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="339ae-121">SQL Database</span></span>](java-sdk-azure-sql-database-samples.md)
   
<span data-ttu-id="339ae-122">Uma [referência](https://docs.microsoft.com/java/api) está disponível para todos os pacotes nas bibliotecas de serviço e de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="339ae-122">A [reference](https://docs.microsoft.com/java/api) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="339ae-123">Novos recursos, alterações significativas, e instruções de migração de versões anteriores estão disponíveis nas [notas de versão](java-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="339ae-123">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](java-sdk-azure-release-notes.md).</span></span>