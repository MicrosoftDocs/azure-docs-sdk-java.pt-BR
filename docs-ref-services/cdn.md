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
ms.openlocfilehash: db9fb8a9a8f9f21061f1e16b77e3145d1fb1b119
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-cdn-libraries-for-java"></a>Bibliotecas CDN do Azure para Java

## <a name="overview"></a>Visão geral

Armazenar em cache conteúdo Web estático em locais estrategicamente posicionados para fornecer uma taxa de transferência máxima para usuários com a [Rede de Distribuição de Conteúdo](/azure/cdn/cdn-overview) (CDN).

Para começar a usar a CDN do Azure, consulte [Introdução à CDN do Azure](/azure/cdn/cdn-create-new-endpoint).

## <a name="management-api"></a>API de Gerenciamento

Criar perfis CDN, definir pontos de extremidade e adicionar conteúdo à CDN usando a API de gerenciamento.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.2.1</version>
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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/cdn/managementapi)

## <a name="samples"></a>Exemplos

[Gerenciar CDNs com Java](https://github.com/Azure-Samples/cdn-java-manage-cdn)

Explore mais [exemplos de código Java para a CDN do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) que você pode usar em seus aplicativos.