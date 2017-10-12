---
title: "Bibliotecas de Serviço de Aplicativo do Azure para Java"
description: "Implantação automática de aplicativos Web no Serviço de Aplicativo do Azure usando as APIs de gerenciamento do Azure."
keywords: "Azure, Java, SDK, API, aplicativos Web, móvel, Serviço de Aplicativo"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/09/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appservice
ms.openlocfilehash: 7e1d7eed9d8fa8d2f872f2902e2ce3f2b3dab7b6
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-app-service-libraries-for-java"></a>Bibliotecas de Serviço de Aplicativo do Azure para Java

## <a name="overview"></a>Visão geral

Implantar e gerenciar sites, aplicativos Web e APIs REST com o [Serviço de Aplicativo do Azure](/azure/app-service).

Para começar a usar o Serviço de Aplicativo do Azure, consulte [Criar seu primeiro aplicativo Web Java no Azure](/azure/app-service-web/app-service-web-get-started-java).

## <a name="management-api"></a>API de Gerenciamento

Implantar, dimensionar e configurar aplicativos no Serviço de Aplicativo do Azure com a API de gerenciamento.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.3.0</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/java/api/overview/azure)

### <a name="example"></a>Exemplo

Implantar um aplicativo Web de uma imagem do Docker em um aplicativo Web do Azure em execução no Linux.

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a>Exemplos

[Implantar um aplicativo Web de FTP ou GitHub][1]  
[Alternar entre as versões do aplicativo com os slots de implantação][2]  
[Configurar um domínio personalizado][3]   
[Dimensionar um aplicativo web entre várias regiões][4]   

Explorar mais [exemplos de código Java para o Serviço de Aplicativo do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) que você pode usar em seus aplicativos.

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
