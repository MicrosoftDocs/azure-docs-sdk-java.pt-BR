---
title: Instalação do Kit de Ferramentas do Azure para o Eclipse
description: Saiba como instalar o Kit de Ferramentas do Azure para o plug-in Eclipse para criar e implantar aplicativos de nuvem no Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 8e6630f7e019d950249e7e84024ac800a0f2f136
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270842"
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="024f2-103">Instalação do Kit de Ferramentas do Azure para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="024f2-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="024f2-104">Há duas maneiras de instalar o Azure Toolkit for Eclipse:</span><span class="sxs-lookup"><span data-stu-id="024f2-104">There are two ways to install Azure Toolkit for Eclipse:</span></span>

  - [<span data-ttu-id="024f2-105">Marketplace do Eclipse</span><span class="sxs-lookup"><span data-stu-id="024f2-105">Eclipse marketplace</span></span>](#eclipse-marketplace)
  - [<span data-ttu-id="024f2-106">Instalar novo software</span><span class="sxs-lookup"><span data-stu-id="024f2-106">Install new software</span></span>](#install-new-software)

> [!NOTE] 
> 
> <span data-ttu-id="024f2-107">O Kit de Ferramentas do Azure para Eclipse é um projeto de código-fonte aberto, cujo código-fonte está disponível de acordo com a Licença do MIT no site do projeto no GitHub na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="024f2-107">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

[!INCLUDE [azure-toolkit-for-eclipse-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="eclipse-marketplace"></a><span data-ttu-id="024f2-108">Marketplace do Eclipse</span><span class="sxs-lookup"><span data-stu-id="024f2-108">Eclipse marketplace</span></span>

1. <span data-ttu-id="024f2-109">Arraste o botão a seguir para seu workspace do Eclipse em execução.</span><span class="sxs-lookup"><span data-stu-id="024f2-109">Drag the following button to your running Eclipse workspace.</span></span>

    <span data-ttu-id="024f2-110">[![Arraste para seu workspace do Eclipse* em execução. *Requer o Cliente do Eclipse Marketplace](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Arraste para seu workspace do Eclipse* em execução. *Requer o Cliente do Eclipse Marketplace")</span><span class="sxs-lookup"><span data-stu-id="024f2-110">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

2. <span data-ttu-id="024f2-111">Caso contrário, também será possível pesquisar e instalar o **plug-in Azure Toolkit for Eclipse** em **Ajuda/Marketplace do Eclipse**.</span><span class="sxs-lookup"><span data-stu-id="024f2-111">Otherwise, it is also possible to search and install the **Azure Toolkit for Eclipse plugin** at **Help/Eclipse Marketplace**.</span></span>

    ![Marketplace](./media/azure-toolkit-for-eclipse-installation/marketplace.png)

## <a name="install-new-software"></a><span data-ttu-id="024f2-113">Instalar novo software</span><span class="sxs-lookup"><span data-stu-id="024f2-113">Install new software</span></span>

1. <span data-ttu-id="024f2-114">Inicie o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="024f2-114">Start Eclipse.</span></span>

1. <span data-ttu-id="024f2-115">Clique no menu **Ajuda** e, em seguida, clique em **Instalar Novo Software**, conforme mostrado na ilustração a seguir.</span><span class="sxs-lookup"><span data-stu-id="024f2-115">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>

   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][01]

1. <span data-ttu-id="024f2-117">Na caixa de diálogo **Software Disponível** na caixa de texto **Trabalhar com**, digite `http://dl.microsoft.com/eclipse/` seguido pela tecla **Enter**.</span><span class="sxs-lookup"><span data-stu-id="024f2-117">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="024f2-118">No painel **Nome**, marque **Kit de Ferramentas do Azure para Java** e desmarque **Entrar em contato com todos os sites de atualização durante a instalação para encontrar o software necessário**.</span><span class="sxs-lookup"><span data-stu-id="024f2-118">In the **Name** pane, check **Azure Toolkit for Java**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="024f2-119">Sua tela será semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="024f2-119">Your screen should appear similar to the following:</span></span>

   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][02]

1. <span data-ttu-id="024f2-121">Se você expandir o **Kit de Ferramentas do Azure para Eclipse**, verá uma lista de componentes que serão instalados; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="024f2-121">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="024f2-122">Recurso</span><span class="sxs-lookup"><span data-stu-id="024f2-122">Feature</span></span> | <span data-ttu-id="024f2-123">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="024f2-123">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="024f2-124">**Plug-in do Application Insights para Java**</span><span class="sxs-lookup"><span data-stu-id="024f2-124">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="024f2-125">Permite que você use os serviços de registro em log e análise de telemetria do Azure para seus aplicativos e instâncias do servidor.</span><span class="sxs-lookup"><span data-stu-id="024f2-125">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="024f2-126">**Plug-in Comum do Azure**</span><span class="sxs-lookup"><span data-stu-id="024f2-126">**Azure Common Plugin**</span></span> | <span data-ttu-id="024f2-127">fornece a funcionalidade comum necessária para outros componentes do kit de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="024f2-127">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="024f2-128">**Ferramentas de Contêiner do Azure para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="024f2-128">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="024f2-129">Permite que você crie e implante um .WAR como um contêiner do Docker em uma máquina do docker.</span><span class="sxs-lookup"><span data-stu-id="024f2-129">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="024f2-130">**Contêineres do Azure para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="024f2-130">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="024f2-131">Permite que você implante um artefato .WAR ou .JAR como um contêiner do Docker em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="024f2-131">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="024f2-132">**Gerenciador do Azure para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="024f2-132">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="024f2-133">Fornece uma interface do gerenciador para gerenciar os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="024f2-133">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="024f2-134">**Microsoft JDBC Driver 6.1 para SQL Server**</span><span class="sxs-lookup"><span data-stu-id="024f2-134">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="024f2-135">Fornece a API JDBC para o SQL Server e o Banco de Dados SQL do Microsoft Azure para o Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="024f2-135">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="024f2-136">**Pacote para as Bibliotecas do Microsoft Azure para Java**</span><span class="sxs-lookup"><span data-stu-id="024f2-136">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="024f2-137">Fornece APIs para acessar os serviços do Microsoft Azure, como armazenamento, barramento de serviço, execução do serviço etc.</span><span class="sxs-lookup"><span data-stu-id="024f2-137">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="024f2-138">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="024f2-138">Click **Next**.</span></span> <span data-ttu-id="024f2-139">(Se você experimentar atrasos incomuns ao instalar o kit de ferramentas, certifique-se de que a opção **Contatar todos os sites de atualização durante a instalação para encontrar o software necessário** está desmarcada.)</span><span class="sxs-lookup"><span data-stu-id="024f2-139">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="024f2-140">No diálogo **Instalar Detalhes**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="024f2-140">In the **Install Details** dialog, click **Next**.</span></span>

   ![Revisão dos detalhes de instalação][03]

1. <span data-ttu-id="024f2-142">No diálogo **Examinar Licenças** , leia os termos dos contratos de licença.</span><span class="sxs-lookup"><span data-stu-id="024f2-142">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="024f2-143">Se você aceitar os termos dos contratos de licença, clique em **Aceito os termos dos contratos de licença** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="024f2-143">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="024f2-144">(As etapas restantes supõem que você aceite os termos dos contratos de licença.</span><span class="sxs-lookup"><span data-stu-id="024f2-144">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="024f2-145">Se você não aceitar os termos dos contratos de licença, saia do processo de instalação.)</span><span class="sxs-lookup"><span data-stu-id="024f2-145">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>

   ![Examinar Licenças][04]

   <span data-ttu-id="024f2-147">O Eclipse baixará e instalará os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="024f2-147">Eclipse will download and install the requisite packages.</span></span>

   ![Progresso da Instalação][05]

1. <span data-ttu-id="024f2-149">Se for solicitado a reiniciar o Eclipse para concluir a instalação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="024f2-149">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>

   ![Reinicie o prompt][06]

## <a name="next-steps"></a><span data-ttu-id="024f2-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="024f2-151">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->
[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
