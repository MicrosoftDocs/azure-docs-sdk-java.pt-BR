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
# <a name="partner-center-libraries-for-java"></a>Bibliotecas do Partner Center para Java

## <a name="overview"></a>Visão geral

As bibliotecas do Partner Center para Java formam um SDK que fornece a capacidade de interagir com o serviço do Partner Center da Microsoft. Isso permite que os parceiros executem as operações do Partner Center programaticamente. É a adição mais recente ao portfólio existente de APIs REST e do SDK do .NET.

## <a name="client-library"></a>Biblioteca do cliente

Gerencie os recursos no Partner Center usando a biblioteca de clientes.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Recupera uma lista completa de clientes associados ao revendedor autenticado.

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

## <a name="samples"></a>Exemplos

[Cenários com suporte](https://docs.microsoft.com/partner-center/develop/scenarios)
[Aplicativo de console de exemplo](https://github.com/Microsoft/Partner-Center-Java-Samples)  