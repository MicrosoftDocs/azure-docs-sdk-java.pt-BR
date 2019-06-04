---
title: Bibliotecas de DNS do Azure para Java
description: Documentação de referência para as bibliotecas de gerenciamento de Java de DNS do Azure
keywords: Azure, Java, SDK, API, domínios, DNS, nome, service, serviço de nome de domínio
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: 90751d2134b218e16415effeb336a62c6c737cb3
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626067"
---
# <a name="azure-dns-libraries-for-java"></a><span data-ttu-id="a417e-104">Bibliotecas de DNS do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="a417e-104">Azure DNS libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a417e-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a417e-105">Overview</span></span>

<span data-ttu-id="a417e-106">Fornecer resolução de nome de domínio e gerenciar seus registros DNS usando as mesmas credenciais, APIs, ferramentas e cobrança que seus outros serviços do Azure com o [DNS do Azure](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="a417e-106">Provide domain name resolution and manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services with [Azure DNS](/azure/dns/dns-overview).</span></span>

<span data-ttu-id="a417e-107">Para começar a usar o DNS do Azure, consulte [Introdução ao DNS do Azure usando a CLI do Azure 2.0](/azure/dns/dns-getstarted-cli).</span><span class="sxs-lookup"><span data-stu-id="a417e-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span></span>

## <a name="management-api"></a><span data-ttu-id="a417e-108">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="a417e-108">Management API</span></span>

<span data-ttu-id="a417e-109">Criar zonas de DNS e adicionar registros às zonas com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="a417e-109">Create DNS zones and add records to zones with the management API.</span></span>

<span data-ttu-id="a417e-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="a417e-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.22.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="a417e-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a417e-111">Example</span></span>

<span data-ttu-id="a417e-112">Criar uma zona de DNS de raiz e adicionar um registro CNAME `www` em um grupo de recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="a417e-112">Create a root DNS zone and add a `www` CNAME record in an existing resource group.</span></span>

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a417e-113">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="a417e-113">Explore the Management APIs</span></span>](/java/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="a417e-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a417e-114">Samples</span></span>

[<span data-ttu-id="a417e-115">Hospedar e gerenciar seus domínios com DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="a417e-115">Host and manage your domains with Azure DNS</span></span>](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

<span data-ttu-id="a417e-116">Explorar mais [exemplos de código Java para o DNS do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a417e-116">Explore more [sample Java code for Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) you can use in your apps.</span></span>

<!---Loc Comment: Please, refer to conversation section to check the issue. Thanks.--->
