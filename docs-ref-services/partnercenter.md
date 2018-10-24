---
title: SDK do Java do Partner Center
description: Documentação de referência para o SDK de Java do Partner Center
keywords: API, CSP, Provedor de Soluções de Nuvem, Java, Partner Center, SDK
author: iswillia
ms.author: iswillia
manager: lesliep
ms.date: 10/09/2018
ms.topic: reference
ms.prod: partnercenter
ms.technology: partnercenter
ms.devlang: java
ms.openlocfilehash: 2adfbdbd37d6eb91e48ee37091f951b3f7d59eb9
ms.sourcegitcommit: 4da7d2f470331feb7d76a1658f5825f365cdba9a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121636"
---
# <a name="partner-center-libraries-for-java"></a><span data-ttu-id="effea-104">Bibliotecas do Partner Center para Java</span><span class="sxs-lookup"><span data-stu-id="effea-104">Partner Center libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="effea-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="effea-105">Overview</span></span>

<span data-ttu-id="effea-106">As bibliotecas do Partner Center para Java formam um SDK que fornece a capacidade de interagir com o serviço do Partner Center da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="effea-106">The Partner Center libraries for Java is a SDK that provides the ability to interact with Microsoft's Partner Center service.</span></span> <span data-ttu-id="effea-107">Isso permite que os parceiros executem as operações do Partner Center programaticamente.</span><span class="sxs-lookup"><span data-stu-id="effea-107">This enables partners to perform the Partner Center operations programmatically.</span></span> <span data-ttu-id="effea-108">É a adição mais recente ao portfólio existente de APIs REST e do SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="effea-108">This is the latest addition to existing portfolio of REST APIs and the .NET SDK.</span></span>

## <a name="client-library"></a><span data-ttu-id="effea-109">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="effea-109">Client library</span></span>

<span data-ttu-id="effea-110">Gerencie os recursos no Partner Center usando a biblioteca de clientes.</span><span class="sxs-lookup"><span data-stu-id="effea-110">Manage resources in Partner Center using the client library.</span></span>

<span data-ttu-id="effea-111">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="effea-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="effea-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="effea-112">Example</span></span>

<span data-ttu-id="effea-113">Recupera uma lista completa de clientes associados ao revendedor autenticado.</span><span class="sxs-lookup"><span data-stu-id="effea-113">Retrieves a complete list of customer associated with the authenticated reseller.</span></span>

```java
IPartnerCredentials appCredentials = PartnerCredentials.getInstance().generateByApplicationCredentials('YOUR_APP_ID', 'YOUR_APP_SECRET', 'YOUR_TENANT_ID');
IAggregatePartner partnerOperations = PartnerService.getInstance().createPartnerOperations(appCredentials);

// Query the customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(100));
this.getContext().getConsoleHelper().stopProgress();

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while ( customersEnumerator.hasValue() )
{
    /*
     * Perform some operation with the current page of customers using 
     * customersEnumerator.getCurrent()  
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="samples"></a><span data-ttu-id="effea-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="effea-114">Samples</span></span>

<span data-ttu-id="effea-115">[Cenários com suporte](https://docs.microsoft.com/partner-center/develop/scenarios)
[Aplicativo de console de exemplo](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="effea-115">[Supported scenarios](https://docs.microsoft.com/partner-center/develop/scenarios)
[Sample console application](https://github.com/Microsoft/Partner-Center-Java-Samples)</span></span>  