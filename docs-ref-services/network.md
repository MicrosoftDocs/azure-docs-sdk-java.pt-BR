---
title: Bibliotecas de Rede do Azure para Java
description: Documentação de referência para as bibliotecas de gerenciamento de Rede do Azure de Java
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
ms.openlocfilehash: bb74ccd8826df7b627e0b5f4e4ffd2da44b2642d
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893377"
---
# <a name="azure-network-libraries-for-java"></a>Bibliotecas de Rede do Azure para Java

## <a name="overview"></a>Visão geral

Conectar recursos do Azure, filtrar e balancear o tráfego e gerenciar o roteamento com a [Rede do Azure](/azure/networking/networking-overview).

Para começar a usar a Rede do Azure, consulte [Criar sua primeira rede virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-api"></a>API de gerenciamento

Criar e gerenciar [redes virtuais](/azure/virtual-network/virtual-networks-overview) do Azure , [ExpressRoutes](/azure/expressroute/) , e [Gateways de Aplicativo](/azure/application-gateway/) com a API de gerenciamento.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Criar uma rede virtual com uma sub-rede individual.

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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/networking/management)

## <a name="samples"></a>Exemplos

[Gerenciar redes virtuais](https://github.com/Azure-Samples/network-java-manage-virtual-network)   
[Gerenciar interfaces de rede](https://github.com/Azure-Samples/network-java-manage-network-interface)   
[Gerenciar Gateways de Aplicativo](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways)   
[Gerenciar balanceadores de carga para a Internet](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

Explore mais [exemplos de código Java para a Rede do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=network) que você pode usar em seus aplicativos.
