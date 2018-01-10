---
title: "Instalação do Kit de Ferramentas do Azure para IntelliJ"
description: Saiba como instalar o Kit de Ferramentas do Azure para o plug-in IntelliJ para criar e implantar aplicativos de nuvem no Azure.
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 88476142dbd6fbe05d3d59d14cf71c83893e6452
ms.sourcegitcommit: 9c354a65b0f8ad49a528f40ddee647b091f7d246
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2018
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="1da09-103">Instalação do Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="1da09-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="1da09-104">O Kit de Ferramentas do Azure para IntelliJ fornece modelos e funcionalidade que permitem criar, desenvolver, testar e implantar com facilidade aplicativos de nuvem ao Azure usando o ambiente de desenvolvimento IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="1da09-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1da09-105">O Kit de Ferramentas do Azure para IntelliJ é um projeto de código-fonte aberto, cujo código-fonte está disponível de acordo com a Licença do MIT no site do projeto no GitHub na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="1da09-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <span data-ttu-id="1da09-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="1da09-106"><https://github.com/microsoft/azure-tools-for-java></span></span> 
> 

<span data-ttu-id="1da09-107">Há dois métodos de instalação do Kit de Ferramentas do Azure para IntelliJ: usando a caixa de diálogo **Configurações** e o menu **Configurar** na tela inicial.</span><span class="sxs-lookup"><span data-stu-id="1da09-107">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="1da09-108">Ambos os métodos de instalação serão demonstrados nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="1da09-108">Both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="1da09-109">Para instalar o Kit de Ferramentas do Azure para IntelliJ na caixa de diálogo de configurações</span><span class="sxs-lookup"><span data-stu-id="1da09-109">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="1da09-110">Inicie o IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="1da09-110">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="1da09-111">Quando o IDEA do IntelliJ é aberto, clique em **Arquivo**, em seguida, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="1da09-111">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Abra a caixa de diálogo Configurações do IDEA do IntelliJ][01a]

1. <span data-ttu-id="1da09-113">Na caixa de diálogo Configurações, clique em **Plug-ins** e, em seguida, clique em **Procurar repositórios**.</span><span class="sxs-lookup"><span data-stu-id="1da09-113">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Caixa de diálogo Configurações do IDEA do IntelliJ][02a]

1. <span data-ttu-id="1da09-115">Na caixa de diálogo **Procurar repositórios** , digite "Azure" na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="1da09-115">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="1da09-116">Realce **Kit de Ferramentas do Azure para IntelliJ** e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="1da09-116">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Procure o Kit de Ferramentas do Azure para IntelliJ][03]
   
   <span data-ttu-id="1da09-118">O IDEA do IntelliJ exibe o progresso da instalação em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1da09-118">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Progresso da instalação][04]

1. <span data-ttu-id="1da09-120">Quando a instalação for concluída, clique em **Reiniciar IDEA do IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="1da09-120">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Reiniciar IDEA do IntelliJ][05]

1. <span data-ttu-id="1da09-122">Clique em **OK** para fechar a caixa de diálogo Configurações.</span><span class="sxs-lookup"><span data-stu-id="1da09-122">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Feche a caixa de diálogo Configurações do IDEA do IntelliJ][06]

1. <span data-ttu-id="1da09-124">Quando for solicitado a reiniciar o IDEA do IntelliJ ou adiar, clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="1da09-124">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="1da09-125">1</span><span class="sxs-lookup"><span data-stu-id="1da09-125">1</span></span>   ![Reiniciar IDEA do IntelliJ][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="1da09-127">Para instalar o Kit de Ferramentas do Azure para IntelliJ a partir da tela inicial</span><span class="sxs-lookup"><span data-stu-id="1da09-127">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="1da09-128">Inicie o IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="1da09-128">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="1da09-129">Quando for exibida a tela inicial do IDEA do IntelliJ, clique em **Configurar**, em seguida, clique em **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="1da09-129">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![Instale os plug-ins do IDEA do IntelliJ][01b]

1. <span data-ttu-id="1da09-131">Na caixa de diálogo **Plug-ins**, clique em **Procurar repositórios**.</span><span class="sxs-lookup"><span data-stu-id="1da09-131">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Procure os repositórios de plug-in do IDEA do IntelliJ][02b]

1. <span data-ttu-id="1da09-133">Na caixa de diálogo **Procurar repositórios** , digite "Azure" na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="1da09-133">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="1da09-134">Realce **Kit de Ferramentas do Azure para IntelliJ** e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="1da09-134">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Procure o Kit de Ferramentas do Azure para IntelliJ][03]
   
   <span data-ttu-id="1da09-136">O IDEA do IntelliJ exibirá o progresso da instalação em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1da09-136">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Progresso da instalação][04]

1. <span data-ttu-id="1da09-138">Quando a instalação for concluída, clique em **Reiniciar IDEA do IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="1da09-138">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Reiniciar IDEA do IntelliJ][05]

1. <span data-ttu-id="1da09-140">Quando for solicitado a reiniciar o IDEA do IntelliJ ou adiar, clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="1da09-140">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Reiniciar IDEA do IntelliJ][07]

## <a name="next-steps"></a><span data-ttu-id="1da09-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1da09-142">Next steps</span></span>

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
