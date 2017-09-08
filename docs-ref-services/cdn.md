---
title: Bibliotecas CDN do Azure para Java
description: "Documentação de referência para as bibliotecas de gerenciamento CDN de Java"
keywords: "Azure, Java, SDK, API, conteúdo, distribuição, rede, CDN"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: e4605b1a7dd7fe34d191337acb2f20cbca2e7037
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cdn-libraries-for-java"></a><span data-ttu-id="32c71-104">Bibliotecas CDN do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="32c71-104">Azure CDN libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="32c71-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="32c71-105">Overview</span></span>

<span data-ttu-id="32c71-106">Armazenar em cache conteúdo Web estático em locais estrategicamente posicionados para fornecer uma taxa de transferência máxima para usuários com a [Rede de Distribuição de Conteúdo](/azure/cdn/cdn-overview) (CDN).</span><span class="sxs-lookup"><span data-stu-id="32c71-106">Cache static web content at strategically placed locations to provide maximum throughput for users with [Azure Content Delivery Network](/azure/cdn/cdn-overview) (CDN).</span></span>

<span data-ttu-id="32c71-107">Para começar a usar a CDN do Azure, consulte [Introdução à CDN do Azure](/azure/cdn/cdn-create-new-endpoint).</span><span class="sxs-lookup"><span data-stu-id="32c71-107">To get started with Azure CDN, see [Getting started with Azure CDN](/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-api"></a><span data-ttu-id="32c71-108">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="32c71-108">Management API</span></span>

<span data-ttu-id="32c71-109">Criar perfis CDN, definir pontos de extremidade e adicionar conteúdo à CDN usando a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="32c71-109">Create CDN profiles, define endpoints, and add content to the CDN using the management API.</span></span>

<span data-ttu-id="32c71-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="32c71-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.1.2</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="32c71-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="32c71-111">Example</span></span>

<span data-ttu-id="32c71-112">Criar um perfil CDN, atribuir pontos de extremidade e carregar conteúdo na CDN.</span><span class="sxs-lookup"><span data-stu-id="32c71-112">Create a CDN profile, assign endpoints, and load content into the CDN.</span></span>

```java
CdnProfile profile = azure.cdnProfiles().define("testCDN")
        .withRegion(Region.US_EAST)
        .withNewResourceGroup()
        .withStandardVerizonSku()
        .withNewEndpoint("webAppHostname1")
        .withNewEndpoint("webAppHostname2")
        .create();

List<String> contentList = new ArrayList<String>();
contentList.add("/client.js");
contentList.add("/media/fabrikam_logo.png");

for (CdnEndpoint endpoint : profile.endpoints().values()) {
    endpoint.loadContent(contentList);
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="32c71-113">Explorar as APIs de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="32c71-113">Explore the Management APIs</span></span>](/java/api/overview/azure/cdn/managementapi)

## <a name="samples"></a><span data-ttu-id="32c71-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="32c71-114">Samples</span></span>

[<span data-ttu-id="32c71-115">Gerenciar CDNs com Java</span><span class="sxs-lookup"><span data-stu-id="32c71-115">Manage CDNs with Java</span></span>](https://github.com/Azure-Samples/cdn-java-manage-cdn)

<span data-ttu-id="32c71-116">Explore mais [exemplos de código Java para a CDN do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="32c71-116">Explore more [sample Java code for Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) you can use in your apps.</span></span>