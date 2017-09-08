---
title: Bibliotecas de Rede do Azure para Java
description: "Documentação de referência para as bibliotecas de gerenciamento de Rede do Azure de Java"
keywords: Azure, Java, SDK, API, rede, balanceamento de carga, rede virtual, sub-rede
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: networking
ms.openlocfilehash: 7be23ba896887cc88ccdf0fb049cb5f579d496c3
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-network-libraries-for-java"></a><span data-ttu-id="1e638-104">Bibliotecas de Rede do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="1e638-104">Azure Network libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="1e638-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1e638-105">Overview</span></span>

<span data-ttu-id="1e638-106">Conectar recursos do Azure, filtrar e balancear o tráfego e gerenciar o roteamento com a [Rede do Azure](/azure/networking/networking-overview).</span><span class="sxs-lookup"><span data-stu-id="1e638-106">Connect Azure resources, filter and balance traffic, and manage routing with [Azure Networking](/azure/networking/networking-overview).</span></span>

<span data-ttu-id="1e638-107">Para começar a usar a Rede do Azure, consulte [Criar sua primeira rede virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="1e638-107">To get started with Azure Networking, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-api"></a><span data-ttu-id="1e638-108">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="1e638-108">Management API</span></span>

<span data-ttu-id="1e638-109">Criar e gerenciar [redes virtuais](/azure/virtual-network/virtual-networks-overview) do Azure , [ExpressRoutes](/azure/expressroute/) , e [Gateways de Aplicativo](/azure/application-gateway/) com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1e638-109">Create and manage Azure [virtual networks](/azure/virtual-network/virtual-networks-overview) , [ExpressRoutes](/azure/expressroute/) , and [Application Gateways](/azure/application-gateway/) with the management API.</span></span>

<span data-ttu-id="1e638-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="1e638-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.1.2</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="1e638-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="1e638-111">Example</span></span>

<span data-ttu-id="1e638-112">Criar uma rede virtual com uma sub-rede individual.</span><span class="sxs-lookup"><span data-stu-id="1e638-112">Create a new virtual network with a single subnet.</span></span>

```java
Network virtualNetwork1 = azure.networks().define(vnetName1)
        .withRegion(Region.US_EAST)
        .withExistingResourceGroup("myResourceGroup")
        .withAddressSpace("192.168.0.0/16")
        .defineSubnet("myVirtualNetwork")
            .withAddressPrefix("192.168.2.0/24")
            .attach()
        .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e638-113">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="1e638-113">Explore the Management APIs</span></span>](/java/api/overview/azure/networking/managementapi)

## <a name="samples"></a><span data-ttu-id="1e638-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1e638-114">Samples</span></span>

<span data-ttu-id="1e638-115">[Gerenciar redes virtuais](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span><span class="sxs-lookup"><span data-stu-id="1e638-115">[Manage virtual networks](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span></span>  
<span data-ttu-id="1e638-116">[Gerenciar interfaces de rede](https://github.com/Azure-Samples/network-java-manage-network-interface) </span><span class="sxs-lookup"><span data-stu-id="1e638-116">[Manage network interfaces](https://github.com/Azure-Samples/network-java-manage-network-interface) </span></span>  
<span data-ttu-id="1e638-117">[Gerenciar Gateways de Aplicativo](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span><span class="sxs-lookup"><span data-stu-id="1e638-117">[Manage Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span></span>  
[<span data-ttu-id="1e638-118">Gerenciar balanceadores de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="1e638-118">Manage internet facing load balancers</span></span>](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

<span data-ttu-id="1e638-119">Explore mais [exemplos de código Java para a Rede do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=network) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1e638-119">Explore more [sample Java code for Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) you can use in your apps.</span></span>
