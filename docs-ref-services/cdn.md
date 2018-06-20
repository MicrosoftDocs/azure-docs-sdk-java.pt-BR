---
title: Bibliotecas CDN do Azure para Java
description: Documentação de referência para as bibliotecas de gerenciamento CDN de Java
keywords: Azure, Java, SDK, API, conteúdo, distribuição, rede, CDN
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: 199e9b4b2b2431e23954d24e4adeb4326eb4741c
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823729"
---
# <a name="azure-cdn-libraries-for-java"></a>Bibliotecas CDN do Azure para Java

## <a name="overview"></a>Visão geral

Armazenar em cache conteúdo Web estático em locais estrategicamente posicionados para fornecer uma taxa de transferência máxima para usuários com a [Rede de Distribuição de Conteúdo](/azure/cdn/cdn-overview) (CDN).

Para começar a usar a CDN do Azure, consulte [Introdução à CDN do Azure](/azure/cdn/cdn-create-new-endpoint).

## <a name="management-api"></a>API de gerenciamento

Criar perfis CDN, definir pontos de extremidade e adicionar conteúdo à CDN usando a API de gerenciamento.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Criar um perfil CDN, atribuir pontos de extremidade e carregar conteúdo na CDN.

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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/cdn/management)

## <a name="samples"></a>Exemplos

[Gerenciar CDNs com Java](https://github.com/Azure-Samples/cdn-java-manage-cdn)

Explore mais [exemplos de código Java para a CDN do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) que você pode usar em seus aplicativos.