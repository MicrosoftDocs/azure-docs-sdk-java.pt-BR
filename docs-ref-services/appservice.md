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
# <a name="azure-app-service-libraries-for-java"></a><span data-ttu-id="c4c75-104">Bibliotecas de Serviço de Aplicativo do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="c4c75-104">Azure App Service libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="c4c75-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c4c75-105">Overview</span></span>

<span data-ttu-id="c4c75-106">Implantar e gerenciar sites, aplicativos Web e APIs REST com o [Serviço de Aplicativo do Azure](/azure/app-service).</span><span class="sxs-lookup"><span data-stu-id="c4c75-106">Deploy and manage websites, web applications, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="c4c75-107">Para começar a usar o Serviço de Aplicativo do Azure, consulte [Criar seu primeiro aplicativo Web Java no Azure](/azure/app-service-web/app-service-web-get-started-java).</span><span class="sxs-lookup"><span data-stu-id="c4c75-107">To get started with Azure App Service, see [Create your first Java web app in Azure](/azure/app-service-web/app-service-web-get-started-java).</span></span>

## <a name="management-api"></a><span data-ttu-id="c4c75-108">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c4c75-108">Management API</span></span>

<span data-ttu-id="c4c75-109">Implantar, dimensionar e configurar aplicativos no Serviço de Aplicativo do Azure com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c4c75-109">Deploy, scale, and configure applications in Azure App Service with the management API.</span></span>

<span data-ttu-id="c4c75-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="c4c75-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.3.0</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4c75-111">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c4c75-111">Explore the Management APIs</span></span>](/java/api/overview/azure)

### <a name="example"></a><span data-ttu-id="c4c75-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c4c75-112">Example</span></span>

<span data-ttu-id="c4c75-113">Implantar um aplicativo Web de uma imagem do Docker em um aplicativo Web do Azure em execução no Linux.</span><span class="sxs-lookup"><span data-stu-id="c4c75-113">Deploy a webapp from a Docker image into an Azure Web App running on Linux.</span></span>

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a><span data-ttu-id="c4c75-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="c4c75-114">Samples</span></span>

<span data-ttu-id="c4c75-115">[Implantar um aplicativo Web de FTP ou GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="c4c75-115">[Deploy a web app from FTP or GitHub][1]</span></span>  
<span data-ttu-id="c4c75-116">[Alternar entre as versões do aplicativo com os slots de implantação][2]</span><span class="sxs-lookup"><span data-stu-id="c4c75-116">[Swap between app versions with deployment slots][2]</span></span>  
<span data-ttu-id="c4c75-117">[Configurar um domínio personalizado][3] </span><span class="sxs-lookup"><span data-stu-id="c4c75-117">[Configure a custom domain][3] </span></span>  
<span data-ttu-id="c4c75-118">[Dimensionar um aplicativo web entre várias regiões][4]</span><span class="sxs-lookup"><span data-stu-id="c4c75-118">[Scale a web app across multiple regions][4]</span></span>   

<span data-ttu-id="c4c75-119">Explorar mais [exemplos de código Java para o Serviço de Aplicativo do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c4c75-119">Explore more [sample Java code for Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) you can use in your apps.</span></span>

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
