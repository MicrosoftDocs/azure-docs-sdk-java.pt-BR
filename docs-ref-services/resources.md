---
title: Biblioteca do Azure Resource Manager para Java
description: Documentação de referência para as bibliotecas do Gerenciador de Recursos de Java
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
ms.openlocfilehash: 326357e5b4667cc06a6058cb29e9685428174dee
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892997"
---
# <a name="azure-resource-manager-libraries-for-java"></a><span data-ttu-id="a3e8b-104">Biblioteca do Azure Resource Manager para Java</span><span class="sxs-lookup"><span data-stu-id="a3e8b-104">Azure Resource Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a3e8b-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a3e8b-105">Overview</span></span>

<span data-ttu-id="a3e8b-106">Implantar, monitorar e gerenciar recursos em grupos com o [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="a3e8b-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="a3e8b-107">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="a3e8b-107">Management API</span></span>

<span data-ttu-id="a3e8b-108">Use a API de gerenciamento para criar grupos de recursos e implantar recursos de modelos.</span><span class="sxs-lookup"><span data-stu-id="a3e8b-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

<span data-ttu-id="a3e8b-109">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="a3e8b-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="a3e8b-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a3e8b-110">Example</span></span>

<span data-ttu-id="a3e8b-111">Criar um novo grupo de recursos na região Leste dos EUA do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e8b-111">Create a new resource group in the Azure Eastern US region.</span></span>

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3e8b-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="a3e8b-112">Explore the Management APIs</span></span>](/java/api/overview/azure/resources/management)

## <a name="samples"></a><span data-ttu-id="a3e8b-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a3e8b-113">Samples</span></span>

<span data-ttu-id="a3e8b-114">[Gerenciar Grupos de Recursos do Azure com Java][1] 
[Implantar recursos usando um modelo do ARM][2]</span><span class="sxs-lookup"><span data-stu-id="a3e8b-114">[Manage Azure Resource Groups with Java][1] 
[Deploy resources using an ARM template][2]</span></span>

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

<span data-ttu-id="a3e8b-115">Exibir a [lista completa](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) de amostras do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a3e8b-115">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) of Azure Resource Manager samples.</span></span>
