---
title: Instalar o Kit de Ferramentas do Azure para Eclipse
description: Saiba como instalar o Kit de Ferramentas do Azure para o plug-in Eclipse para criar e implantar aplicativos de nuvem no Azure.
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 81a784a09c07e0ace4d12989c745c80f55cd70cd
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="a6f68-103">Instalar o Kit de Ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="a6f68-103">Install the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="a6f68-104">O Kit de Ferramentas do Azure para Eclipse fornece modelos e funcionalidades que permitem criar, desenvolver, testar e implantar facilmente aplicativos de nuvem para o Azure a partir do ambiente de desenvolvimento do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a6f68-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy cloud applications to Azure from the Eclipse development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a6f68-105">O Kit de Ferramentas do Azure para Eclipse é um projeto de código-fonte aberto, cujo código-fonte está disponível de acordo com a Licença do MIT no site do projeto no GitHub na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="a6f68-105">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <span data-ttu-id="a6f68-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="a6f68-106"><https://github.com/microsoft/azure-tools-for-java></span></span> 
> 

<span data-ttu-id="a6f68-107">As etapas a seguir mostram como instalar o Kit de Ferramentas do Azure para o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a6f68-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="a6f68-108">Para instalar o Kit de Ferramentas do Azure para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="a6f68-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="a6f68-109">Inicie o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a6f68-109">Start Eclipse.</span></span>

1. <span data-ttu-id="a6f68-110">Clique no menu **Ajuda** e, em seguida, clique em **Instalar Novo Software**, conforme mostrado na ilustração a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6f68-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][01]

1. <span data-ttu-id="a6f68-112">Na caixa de diálogo **Software Disponível** na caixa de texto **Trabalhar com**, digite `http://dl.microsoft.com/eclipse/` seguido pela tecla **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a6f68-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="a6f68-113">No painel **Nome**, marque **Kit de Ferramentas do Azure para o Eclipse** e desmarque **Entrar em contato com todos os sites de atualização durante a instalação para encontrar o software necessário**.</span><span class="sxs-lookup"><span data-stu-id="a6f68-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="a6f68-114">Sua tela será semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="a6f68-114">Your screen should appear similar to the following:</span></span>
   
   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][02]

1. <span data-ttu-id="a6f68-116">Se você expandir o **Kit de Ferramentas do Azure para Eclipse**, verá uma lista de componentes que serão instalados; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a6f68-116">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="a6f68-117">Recurso</span><span class="sxs-lookup"><span data-stu-id="a6f68-117">Feature</span></span> | <span data-ttu-id="a6f68-118">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="a6f68-118">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="a6f68-119">**Plug-in do Application Insights para Java**</span><span class="sxs-lookup"><span data-stu-id="a6f68-119">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="a6f68-120">Permite que você use os serviços de registro em log e análise de telemetria do Azure para seus aplicativos e instâncias do servidor.</span><span class="sxs-lookup"><span data-stu-id="a6f68-120">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="a6f68-121">**Plug-in Comum do Azure**</span><span class="sxs-lookup"><span data-stu-id="a6f68-121">**Azure Common Plugin**</span></span> | <span data-ttu-id="a6f68-122">fornece a funcionalidade comum necessária para outros componentes do kit de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="a6f68-122">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="a6f68-123">**Ferramentas de Contêiner do Azure para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="a6f68-123">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="a6f68-124">Permite que você crie e implante um .WAR como um contêiner do Docker em uma máquina do docker.</span><span class="sxs-lookup"><span data-stu-id="a6f68-124">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="a6f68-125">**Contêineres do Azure para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="a6f68-125">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="a6f68-126">Permite que você implante um artefato .WAR ou .JAR como um contêiner do Docker em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f68-126">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="a6f68-127">**Gerenciador do Azure para Eclipse**</span><span class="sxs-lookup"><span data-stu-id="a6f68-127">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="a6f68-128">Fornece uma interface do gerenciador para gerenciar os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f68-128">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="a6f68-129">**Microsoft JDBC Driver 6.1 para SQL Server**</span><span class="sxs-lookup"><span data-stu-id="a6f68-129">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="a6f68-130">Fornece a API JDBC para o SQL Server e o Banco de Dados SQL do Microsoft Azure para o Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="a6f68-130">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="a6f68-131">**Pacote para as Bibliotecas do Microsoft Azure para Java**</span><span class="sxs-lookup"><span data-stu-id="a6f68-131">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="a6f68-132">Fornece APIs para acessar os serviços do Microsoft Azure, como armazenamento, barramento de serviço, execução do serviço etc.</span><span class="sxs-lookup"><span data-stu-id="a6f68-132">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="a6f68-133">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="a6f68-133">Click **Next**.</span></span> <span data-ttu-id="a6f68-134">(Se você experimentar atrasos incomuns ao instalar o kit de ferramentas, certifique-se de que a opção **Contatar todos os sites de atualização durante a instalação para encontrar o software necessário** está desmarcada.)</span><span class="sxs-lookup"><span data-stu-id="a6f68-134">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="a6f68-135">No diálogo **Instalar Detalhes**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="a6f68-135">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Revisão dos detalhes de instalação][03]

1. <span data-ttu-id="a6f68-137">No diálogo **Examinar Licenças** , leia os termos dos contratos de licença.</span><span class="sxs-lookup"><span data-stu-id="a6f68-137">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="a6f68-138">Se você aceitar os termos dos contratos de licença, clique em **Aceito os termos dos contratos de licença** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a6f68-138">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="a6f68-139">(As etapas restantes supõem que você aceite os termos dos contratos de licença.</span><span class="sxs-lookup"><span data-stu-id="a6f68-139">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="a6f68-140">Se você não aceitar os termos dos contratos de licença, saia do processo de instalação.)</span><span class="sxs-lookup"><span data-stu-id="a6f68-140">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Examinar Licenças][04]
   
   <span data-ttu-id="a6f68-142">O Eclipse baixará e instalará os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="a6f68-142">Eclipse will download and install the requisite packages.</span></span>
   
   ![Progresso da Instalação][05]

1. <span data-ttu-id="a6f68-144">Se for solicitado a reiniciar o Eclipse para concluir a instalação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a6f68-144">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Reinicie o prompt][06]

## <a name="next-steps"></a><span data-ttu-id="a6f68-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6f68-146">Next steps</span></span>

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
