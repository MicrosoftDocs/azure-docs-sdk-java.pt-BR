---
title: "Bibliotecas do Gerenciador de Tráfego do Azure para Java"
description: "Documentação de referência para as bibliotecas de gerenciamento do Gerenciador de Tráfego de Java"
keywords: "Azure, Java, SDK, API, balanceamento de carga, distribuição de carga, rede, Gerenciador de Tráfego"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: a38db9a0d92d7dedc5ff49b83ad2658aa61729dd
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Bibliotecas do Gerenciador de Tráfego do Azure para Java

## <a name="overview"></a>Visão geral

Controlar a distribuição de tráfego do usuário para pontos de extremidade de serviço em datacenters diferentes com o [Gerenciador de Tráfego do Azure](/azure/traffic-manager/traffic-manager-overview).

Para se familiarizar com o Gerenciador de Tráfego do Azure, consulte [Criar um perfil do Gerenciador de Tráfego](/azure/traffic-manager/traffic-manager-create-profile).

## <a name="management-api"></a>API de Gerenciamento

Criar perfis do Gerenciador de Tráfego, definir pontos de extremidade e alterar o método de roteamento com a API de gerenciamento. 

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.2.1</version>
</dependency>
```   

## <a name="example"></a>Exemplo

Criar um perfil do Gerenciador de Tráfego e atribuir um ponto de extremidade individual.

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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/trafficmanager/managementapi)

## <a name="samples"></a>Exemplos

[Equilibrar o tráfego de aplicativo da Web entre várias regiões](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

Explore mais [exemplos de código Java para o Gerenciador de Tráfego do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) que você pode usar em seus aplicativos.
