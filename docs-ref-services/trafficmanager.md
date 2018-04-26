---
title: Bibliotecas do Gerenciador de Tráfego do Azure para Java
description: Documentação de referência para as bibliotecas de gerenciamento do Gerenciador de Tráfego de Java
keywords: Azure, Java, SDK, API, balanceamento de carga, distribuição de carga, rede, Gerenciador de Tráfego
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: fd78402f50df16ad7d57c0ca67815bfad5b18d51
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="1feb7-104">Bibliotecas do Gerenciador de Tráfego do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="1feb7-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="1feb7-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1feb7-105">Overview</span></span>

<span data-ttu-id="1feb7-106">Controlar a distribuição de tráfego do usuário para pontos de extremidade de serviço em datacenters diferentes com o [Gerenciador de Tráfego do Azure](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="1feb7-106">Control the distribution of user traffic for service endpoints in different datacenters with [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>

<span data-ttu-id="1feb7-107">Para se familiarizar com o Gerenciador de Tráfego do Azure, consulte [Criar um perfil do Gerenciador de Tráfego](/azure/traffic-manager/traffic-manager-create-profile).</span><span class="sxs-lookup"><span data-stu-id="1feb7-107">To get started with Azure Traffic Manager, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).</span></span>

## <a name="management-api"></a><span data-ttu-id="1feb7-108">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="1feb7-108">Management API</span></span>

<span data-ttu-id="1feb7-109">Criar perfis do Gerenciador de Tráfego, definir pontos de extremidade e alterar o método de roteamento com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1feb7-109">Create Traffic Manager profiles, define endpoints, and change the routing method with the management API.</span></span> 

<span data-ttu-id="1feb7-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="1feb7-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.3.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="1feb7-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="1feb7-111">Example</span></span>

<span data-ttu-id="1feb7-112">Criar um perfil do Gerenciador de Tráfego e atribuir um ponto de extremidade individual.</span><span class="sxs-lookup"><span data-stu-id="1feb7-112">Create a Traffic Manager profile and assign a single endpoint.</span></span>

```java
TrafficManagerProfile tmProfile = azure.trafficManagerProfiles().define("testTMProfile")
        .withNewResourceGroup(Region.US_EAST)
        .withLeafDomainLabel("testTMProfile")
        .withPriorityBasedRouting()
        .defineAzureTargetEndpoint("endpoint")
        .toResourceId(webAppId)
        .withRoutingPriority(1)
        .attach()
        .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1feb7-113">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="1feb7-113">Explore the Management APIs</span></span>](/java/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="1feb7-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1feb7-114">Samples</span></span>

[<span data-ttu-id="1feb7-115">Equilibrar o tráfego de aplicativo da Web entre várias regiões</span><span class="sxs-lookup"><span data-stu-id="1feb7-115">Balance web app traffic across multiple regions</span></span>](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

<span data-ttu-id="1feb7-116">Explore mais [exemplos de código Java para o Gerenciador de Tráfego do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1feb7-116">Explore more [sample Java code for Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) you can use in your apps.</span></span>
