---
title: Biblioteca do Azure Resource Manager para Java
description: "Documentação de referência para as bibliotecas do Gerenciador de Recursos de Java"
keywords: Azure, Java, SDK, API, grupos de recursos, arm, gerenciador de recursos
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 56199b87fa64e9cbf0a14716a58c01f11f0e433b
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2017
---
# <a name="azure-resource-manager-libraries-for-java"></a><span data-ttu-id="fc028-104">Biblioteca do Azure Resource Manager para Java</span><span class="sxs-lookup"><span data-stu-id="fc028-104">Azure Resource Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="fc028-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fc028-105">Overview</span></span>

<span data-ttu-id="fc028-106">Implantar, monitorar e gerenciar recursos em grupos com o [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="fc028-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="fc028-107">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="fc028-107">Management API</span></span>

<span data-ttu-id="fc028-108">Use a API de gerenciamento para criar grupos de recursos e implantar recursos de modelos.</span><span class="sxs-lookup"><span data-stu-id="fc028-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

<span data-ttu-id="fc028-109">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="fc028-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="fc028-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fc028-110">Example</span></span>

<span data-ttu-id="fc028-111">Criar um novo grupo de recursos na região Leste dos EUA do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc028-111">Create a new resource group in the Azure Eastern US region.</span></span>

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc028-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="fc028-112">Explore the Management APIs</span></span>](/java/api/overview/azure/resources/managementapi)

## <a name="samples"></a><span data-ttu-id="fc028-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="fc028-113">Samples</span></span>

<span data-ttu-id="fc028-114">[Gerenciar Grupos de Recursos do Azure com Java][1] 
[Implantar recursos usando um modelo do ARM][2]</span><span class="sxs-lookup"><span data-stu-id="fc028-114">[Manage Azure Resource Groups with Java][1] 
[Deploy resources using an ARM template][2]</span></span>

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

<span data-ttu-id="fc028-115">Exibir a [lista completa](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) de amostras do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc028-115">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) of Azure Resource Manager samples.</span></span>
