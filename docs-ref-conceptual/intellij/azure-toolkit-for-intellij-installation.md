---
title: Instalação do Kit de Ferramentas do Azure para IntelliJ
description: Saiba como instalar o Kit de Ferramentas do Azure para o plug-in IntelliJ para criar e implantar aplicativos de nuvem no Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 86cef07873ae7a2ba75aab1044fe4d241cd5b13e
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270878"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="ffafd-103">Instalação do Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ffafd-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="ffafd-104">O Kit de Ferramentas do Azure para IntelliJ fornece modelos e funcionalidade que permitem criar, desenvolver, testar e implantar com facilidade aplicativos de nuvem ao Azure usando o ambiente de desenvolvimento IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ffafd-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ffafd-105">O Kit de Ferramentas do Azure para IntelliJ é um projeto de código-fonte aberto, cujo código-fonte está disponível de acordo com a Licença do MIT no site do projeto no GitHub na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="ffafd-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="ffafd-106">Há dois métodos de instalação do Kit de Ferramentas do Azure para IntelliJ: usando a caixa de diálogo **Configurações** e o menu **Configurar** na tela inicial.</span><span class="sxs-lookup"><span data-stu-id="ffafd-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="ffafd-107">Ambos os métodos de instalação serão demonstrados nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ffafd-107">Both installation methods will be demonstrated in the following steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffafd-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ffafd-108">Prerequisites</span></span>

<span data-ttu-id="ffafd-109">O Azure Toolkit for IntelliJ requer os seguintes componentes de software:</span><span class="sxs-lookup"><span data-stu-id="ffafd-109">The Azure Toolkit for IntelliJ requires to the following software components:</span></span>

* <span data-ttu-id="ffafd-110">Um JDK (Java Development Kit) 8+ instalado, por exemplo: [OpenJDK](https://openjdk.java.net/) ou [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="ffafd-110">An Java Development Kit (JDK) 8+ installed, for example: [OpenJDK](https://openjdk.java.net/) or [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span></span>
* <span data-ttu-id="ffafd-111">Um [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition ou Community Edition instalado</span><span class="sxs-lookup"><span data-stu-id="ffafd-111">An [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition or Community Edition installed</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ffafd-112">A página [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) no repositório de plug-in JetBrains lista as compilações compatíveis com o kit de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="ffafd-112">The [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) page at the JetBrains Plugin Repository lists the builds that are compatible with the toolkit.</span></span>
> 

<!--
> [!IMPORTANT]
> 
> If you are using the Azure Toolkit for IntelliJ on Windows, the toolkit requires installing the Azure SDK 2.9.6 or later in order to use the Azure emulator. You have two options for installing the Azure SDK:
> 
> * You can download and install the Azure SDK by using the [Web Platform Installer (WebPI)](http://go.microsoft.com/fwlink/?LinkID=252838).
> * If you do not have the Azure SDK installed when you create your first Azure deployment project, you will be prompted to automatically download install the requisite version of the Azure SDK.
> 
> Note that the Azure SDK is only required on Windows.
> 
-->


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="ffafd-113">Para instalar o Kit de Ferramentas do Azure para IntelliJ na caixa de diálogo de configurações</span><span class="sxs-lookup"><span data-stu-id="ffafd-113">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="ffafd-114">Inicie o IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ffafd-114">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="ffafd-115">Quando o IDEA do IntelliJ é aberto, clique em **Arquivo**, em seguida, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-115">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Abra a caixa de diálogo Configurações do IDEA do IntelliJ][01a]

1. <span data-ttu-id="ffafd-117">Na caixa de diálogo Configurações, clique em **Plug-ins** e, em seguida, clique em **Procurar repositórios**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-117">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Caixa de diálogo Configurações do IDEA do IntelliJ][02a]

1. <span data-ttu-id="ffafd-119">Na caixa de diálogo **Procurar repositórios** , digite "Azure" na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="ffafd-119">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="ffafd-120">Realce **Kit de Ferramentas do Azure para IntelliJ** e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-120">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Procure o Kit de Ferramentas do Azure para IntelliJ][03]
   
   <span data-ttu-id="ffafd-122">O IDEA do IntelliJ exibe o progresso da instalação em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffafd-122">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Progresso da instalação][04]

1. <span data-ttu-id="ffafd-124">Quando a instalação for concluída, clique em **Reiniciar IDEA do IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-124">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Reiniciar IDEA do IntelliJ][05]

1. <span data-ttu-id="ffafd-126">Clique em **OK** para fechar a caixa de diálogo Configurações.</span><span class="sxs-lookup"><span data-stu-id="ffafd-126">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Feche a caixa de diálogo Configurações do IDEA do IntelliJ][06]

1. <span data-ttu-id="ffafd-128">Quando for solicitado a reiniciar o IDEA do IntelliJ ou adiar, clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-128">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="ffafd-129">1</span><span class="sxs-lookup"><span data-stu-id="ffafd-129">1</span></span>   ![Reiniciar IDEA do IntelliJ][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="ffafd-131">Para instalar o Kit de Ferramentas do Azure para IntelliJ a partir da tela inicial</span><span class="sxs-lookup"><span data-stu-id="ffafd-131">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="ffafd-132">Inicie o IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ffafd-132">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="ffafd-133">Quando for exibida a tela inicial do IDEA do IntelliJ, clique em **Configurar**, em seguida, clique em **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-133">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![Instale os plug-ins do IDEA do IntelliJ][01b]

1. <span data-ttu-id="ffafd-135">Na caixa de diálogo **Plug-ins**, clique em **Procurar repositórios**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-135">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Procure os repositórios de plug-in do IDEA do IntelliJ][02b]

1. <span data-ttu-id="ffafd-137">Na caixa de diálogo **Procurar repositórios** , digite "Azure" na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="ffafd-137">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="ffafd-138">Realce **Kit de Ferramentas do Azure para IntelliJ** e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-138">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Procure o Kit de Ferramentas do Azure para IntelliJ][03]
   
   <span data-ttu-id="ffafd-140">O IDEA do IntelliJ exibirá o progresso da instalação em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ffafd-140">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Progresso da instalação][04]

1. <span data-ttu-id="ffafd-142">Quando a instalação for concluída, clique em **Reiniciar IDEA do IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-142">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Reiniciar IDEA do IntelliJ][05]

1. <span data-ttu-id="ffafd-144">Quando for solicitado a reiniciar o IDEA do IntelliJ ou adiar, clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="ffafd-144">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Reiniciar IDEA do IntelliJ][07]

## <a name="next-steps"></a><span data-ttu-id="ffafd-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ffafd-146">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[01a]: media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
