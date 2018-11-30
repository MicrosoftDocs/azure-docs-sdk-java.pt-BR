---
title: Ferramentas para desenvolvedores de Java do Azure | Microsoft Docs
description: Integrações do IDE, emuladores, gerenciadores de recursos e interfaces de linha de comando para desenvolvedores de Java trabalhando no Azure.
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 11/13/2018
ms.author: routlaw
ms.openlocfilehash: 9e9828540ddc678f69eab11f5a61eef8bf8e916c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339010"
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="84c12-103">Ferramentas do Azure para desenvolvedores Java</span><span class="sxs-lookup"><span data-stu-id="84c12-103">Azure tools for Java developers</span></span>

## <a name="supported-jdk-runtimes"></a><span data-ttu-id="84c12-104">Tempos de execução com suporte do JDK</span><span class="sxs-lookup"><span data-stu-id="84c12-104">Supported JDK runtimes</span></span>

<span data-ttu-id="84c12-105">Desenvolvedores de Java no Azure e Azure Stack podem compilar e executar aplicativos de Java 7, 8 e 11 de produção usando [buils de Azul Systems Zulu Enterprise do OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) sem incorrer em custos adicionais de suporte.</span><span class="sxs-lookup"><span data-stu-id="84c12-105">Java developers on Azure and Azure Stack can build and run production Java 7,8, and 11 applications using [Azul Systems Zulu Enterprise builds of OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="84c12-106">Se você estiver executando aplicativos Java com outros JDKs, considere a migração para o Zulu no Azure para obter manutenção e suporte gratuitos.</span><span class="sxs-lookup"><span data-stu-id="84c12-106">If you’re currently running Java apps with other JDKs, consider migrating to Zulu on Azure for free support and maintenance.</span></span> 

<span data-ttu-id="84c12-107">Para obter mais informações sobre os JDKs com suporte disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="84c12-107">For more information about the supported JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="84c12-108">Plug-ins Eclipse e IntelliJ</span><span class="sxs-lookup"><span data-stu-id="84c12-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="84c12-109">Gerenciar recursos do Azure e implantar aplicativos do seu IDE com o kit de ferramentas do Azure para [Eclipse](eclipse/azure-toolkit-for-eclipse.md) e [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="84c12-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![Kit de ferramentas de IntelliJ mostrando o Gerenciador do Azure](media/intelliJ-azure-explorer.png)

<span data-ttu-id="84c12-111">[Introdução ao kit de ferramentas do Azure para Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Introdução ao kit de ferramentas do Azure para IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="84c12-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="visual-studio-code"></a><span data-ttu-id="84c12-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="84c12-112">Visual Studio Code</span></span>

<span data-ttu-id="84c12-113">O [VS Code](https://code.visualstudio.com/) é um editor de código simples e poderoso disponível para MacOS, Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="84c12-113">[VS Code](https://code.visualstudio.com/) is a lightweight but powerful code editor available for MacOS, Windows, and Linux.</span></span> <span data-ttu-id="84c12-114">O VS Code oferece suporte a um fluxo de trabalho simples e moderno de desenvolvimento Java por meio de um conjunto de extensões que oferece suporte a projeto, preenchimento de código, depuração, uso de Lint e navegação.</span><span class="sxs-lookup"><span data-stu-id="84c12-114">VS Code supports a simple, modern Java development workflow through a set of extensions that provide project support, code completion, debugging, linting, and navigation.</span></span>

<span data-ttu-id="84c12-115">[Introdução ao VS Code e Java](https://code.visualstudio.com/docs/java)
[Pacote de extensão Java para VS Code](https://code.visualstudio.com/docs/java/extensions)</span><span class="sxs-lookup"><span data-stu-id="84c12-115">[Get Started with VS Code and Java](https://code.visualstudio.com/docs/java)
[Java extension pack for VS Code](https://code.visualstudio.com/docs/java/extensions)</span></span>  

## <a name="azure-cli-20"></a><span data-ttu-id="84c12-116">CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="84c12-116">Azure CLI 2.0</span></span>

<span data-ttu-id="84c12-117">A CLI do Azure 2.0 fornece uma experiência de linha de comando para gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="84c12-117">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="84c12-118">Você pode usá-lo no seu navegador com o [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) ou pode [instalá-lo](https://docs.microsoft.com/cli/azure/install-azure-cli) no macOS, Linux e Windows e executá-lo da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="84c12-118">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="84c12-119">[Introdução à CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="84c12-119">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="84c12-120">Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="84c12-120">Azure Storage Explorer</span></span> 

<span data-ttu-id="84c12-121">Gerenciar contas de armazenamento do Azure, contêineres e blobs/arquivos da área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="84c12-121">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="84c12-122">O Gerenciador de Armazenamento do Azure está atualmente em Versão prévia e funciona no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="84c12-122">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="84c12-123">Introdução ao Explorer do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="84c12-123">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)
