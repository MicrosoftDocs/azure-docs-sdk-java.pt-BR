---
title: Ferramentas para desenvolvedores de Java do Azure | Microsoft Docs
description: "Integrações do IDE, emuladores, gerenciadores de recursos e interfaces de linha de comando para desenvolvedores de Java trabalhando no Azure."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: ff3ea805daefb3c0a413b109e431d2235a5dc5b8
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="ce52b-103">Ferramentas do Azure para desenvolvedores Java</span><span class="sxs-lookup"><span data-stu-id="ce52b-103">Azure tools for Java developers</span></span>

## <a name="client-and-management-libraries"></a><span data-ttu-id="ce52b-104">Bibliotecas de cliente e gerenciamento</span><span class="sxs-lookup"><span data-stu-id="ce52b-104">Client and management libraries</span></span>

<span data-ttu-id="ce52b-105">Conectar-se aos serviços e gerenciar recursos do Azure a partir de seus aplicativos com as bibliotecas do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="ce52b-105">Connect to services and manage Azure resources from your applications with the Azure libraries for Java.</span></span> <span data-ttu-id="ce52b-106">Importar as bibliotecas de gerenciamento para seus projetos Maven adicionando essa dependência ao seu projeto *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="ce52b-106">Import the management libraries into your Maven projects by adding this dependency to your project *pom.xml*.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="ce52b-107">Exibição da [lista completa das bibliotecas](java-sdk-azure-install.md) e [introdução](java-sdk-azure-get-started.md) para as bibliotecas do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="ce52b-107">View the [complete list of libraries](java-sdk-azure-install.md) and [get started](java-sdk-azure-get-started.md) with the Azure libraries for Java.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="ce52b-108">Plug-ins Eclipse e IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ce52b-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="ce52b-109">Gerenciar recursos do Azure e implantar aplicativos do seu IDE com o kit de ferramentas do Azure para [Eclipse](eclipse/azure-toolkit-for-eclipse.md) e [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="ce52b-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![Kit de ferramentas de IntelliJ mostrando o Gerenciador do Azure](media/intelliJ-azure-explorer.png)

<span data-ttu-id="ce52b-111">[Introdução ao kit de ferramentas do Azure para Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Introdução ao kit de ferramentas do Azure para IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="ce52b-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="azure-cli-20"></a><span data-ttu-id="ce52b-112">CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ce52b-112">Azure CLI 2.0</span></span>

<span data-ttu-id="ce52b-113">A CLI do Azure 2.0 fornece uma experiência de linha de comando para gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce52b-113">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="ce52b-114">Você pode usá-lo no seu navegador com o [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) ou pode [instalá-lo](https://docs.microsoft.com/cli/azure/install-azure-cli) no macOS, Linux e Windows e executá-lo da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="ce52b-114">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="ce52b-115">[Introdução à CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ce52b-115">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="ce52b-116">Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ce52b-116">Azure Storage Explorer</span></span> 

<span data-ttu-id="ce52b-117">Gerenciar contas de armazenamento do Azure, contêineres e blobs/arquivos da área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ce52b-117">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="ce52b-118">O Gerenciador de Armazenamento do Azure está atualmente em Versão prévia e funciona no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="ce52b-118">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="ce52b-119">Introdução ao Explorer do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ce52b-119">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)