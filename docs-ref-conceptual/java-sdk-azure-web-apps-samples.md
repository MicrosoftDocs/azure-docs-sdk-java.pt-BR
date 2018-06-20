---
title: Bibliotecas de gerenciamento do Azure para exemplos de aplicativo Web de Java
description: Obter o código de exemplo para criação e atualização de aplicativos Web do Azure hospedados no Serviço de Aplicativo usando as bibliotecas de gerenciamento do Azure para Java
keywords: Azure, Java, SDK, API, Maven, Gradle, aplicativos Web, serviço de aplicativo
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 43633e5c-9fb1-4807-ba63-e24c126754e2
ms.openlocfilehash: 2f1e43f3835ffcdb138bf7e29a1656b7ee381281
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930892"
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a><span data-ttu-id="95ca6-104">Bibliotecas de gerenciamento do Azure para exemplos de Java para aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="95ca6-104">Azure management libraries for Java samples for web apps</span></span>

| <span data-ttu-id="95ca6-105">**Criar um aplicativo**</span><span class="sxs-lookup"><span data-stu-id="95ca6-105">**Create an app**</span></span> ||
|---|---|
| <span data-ttu-id="95ca6-106">[Criar um aplicativo Web e implantar a partir do FTP ou GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="95ca6-106">[Create a web app and deploy from FTP or GitHub][1]</span></span> | <span data-ttu-id="95ca6-107">Implantar aplicativos Web do Git local, FTP e integração contínua do GitHub.</span><span class="sxs-lookup"><span data-stu-id="95ca6-107">Deploy web apps from local Git, FTP, and continuous integration from GitHub.</span></span> |
| <span data-ttu-id="95ca6-108">[Criar um aplicativo Web e gerenciar os slots de implantação][2]</span><span class="sxs-lookup"><span data-stu-id="95ca6-108">[Create a web app and manage deployment slots][2]</span></span> | <span data-ttu-id="95ca6-109">Criar um aplicativo Web e implantar para slots de preparo e, em seguida, alternar as implantações entre os slots.</span><span class="sxs-lookup"><span data-stu-id="95ca6-109">Create a web app and deploy to staging slots, and then swap deployments between slots.</span></span> |
| <span data-ttu-id="95ca6-110">**Como configurar o aplicativo**</span><span class="sxs-lookup"><span data-stu-id="95ca6-110">**Configure app**</span></span> ||
| <span data-ttu-id="95ca6-111">[Criar um aplicativo Web e configurar um domínio personalizado][3]</span><span class="sxs-lookup"><span data-stu-id="95ca6-111">[Create a web app and configure a custom domain][3]</span></span> | <span data-ttu-id="95ca6-112">Criar um aplicativo Web com um domínio personalizado e o certificado SSL autoassinado.</span><span class="sxs-lookup"><span data-stu-id="95ca6-112">Create a web app with a custom domain and self-signed SSL certificate.</span></span> |
| <span data-ttu-id="95ca6-113">**Dimensionar aplicativos**</span><span class="sxs-lookup"><span data-stu-id="95ca6-113">**Scale apps**</span></span> ||
| <span data-ttu-id="95ca6-114">[Dimensionar um aplicativo Web com alta disponibilidade em várias regiões][4]</span><span class="sxs-lookup"><span data-stu-id="95ca6-114">[Scale a web app with high availability across multiple regions][4]</span></span> | <span data-ttu-id="95ca6-115">Criar um aplicativo Web em três regiões geográficas diferentes e os disponibilizar por meio de um único ponto de extremidade usando o Gerenciador de Tráfego do Azure.</span><span class="sxs-lookup"><span data-stu-id="95ca6-115">Scale a web app in three different geographical regions and make them available through a single endpoint using Azure Traffic Manager.</span></span> | 
| <span data-ttu-id="95ca6-116">**Como conectar o aplicativo aos recursos**</span><span class="sxs-lookup"><span data-stu-id="95ca6-116">**Connect app to resources**</span></span> ||
| <span data-ttu-id="95ca6-117">[Conectar um aplicativo Web a uma conta de armazenamento][5]</span><span class="sxs-lookup"><span data-stu-id="95ca6-117">[Connect a web app to a storage account][5]</span></span> | <span data-ttu-id="95ca6-118">Criar uma conta de armazenamento do Azure e adicionar a cadeia de conexão de armazenamento às configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95ca6-118">Create an Azure storage account and add the storage account connection string to the app settings.</span></span> |
| <span data-ttu-id="95ca6-119">[Conectar um aplicativo Web a um Banco de Dados SQL][6]</span><span class="sxs-lookup"><span data-stu-id="95ca6-119">[Connect a web app to a SQL database][6]</span></span> | <span data-ttu-id="95ca6-120">Criar um aplicativo Web e um Banco de Dados SQL e, em seguida, adicionar a cadeia de conexão do banco de dados às configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95ca6-120">Create a web app and SQL database, and then add the SQL database connection string to the app settings.</span></span> |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/