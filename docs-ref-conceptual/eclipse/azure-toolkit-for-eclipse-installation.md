---
title: "Instalação do Kit de Ferramentas do Azure para o Eclipse"
description: Saiba como instalar o Kit de Ferramentas do Azure para o Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 59a8bfb6ab4db8ea8c6c9025ca3ced8a13192628
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="eab65-103">Instalação do Kit de Ferramentas do Azure para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="eab65-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="eab65-104">O Kit de Ferramentas do Azure para Eclipse fornece modelos e funcionalidade que permitem criar, desenvolver, testar e implantar com facilidade aplicativos Azure usando o ambiente de desenvolvimento do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eab65-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="eab65-105">O Kit de Ferramentas do Azure para Eclipse é um projeto de software livre.</span><span class="sxs-lookup"><span data-stu-id="eab65-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="eab65-106">O código-fonte está disponível sob a licença do MIT em <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="eab65-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="eab65-107">As etapas a seguir mostram como instalar o Kit de Ferramentas do Azure para o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eab65-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="eab65-108">Para instalar o Kit de Ferramentas do Azure para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="eab65-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="eab65-109">Inicie o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eab65-109">Start Eclipse.</span></span>

1. <span data-ttu-id="eab65-110">Clique no menu **Ajuda** e, em seguida, clique em **Instalar Novo Software**, conforme mostrado na ilustração a seguir.</span><span class="sxs-lookup"><span data-stu-id="eab65-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][01]

1. <span data-ttu-id="eab65-112">Na caixa de diálogo **Software Disponível** na caixa de texto **Trabalhar com**, digite `http://dl.microsoft.com/eclipse/` seguido pela tecla **Enter**.</span><span class="sxs-lookup"><span data-stu-id="eab65-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="eab65-113">No painel **Nome**, marque **Kit de Ferramentas do Azure para o Eclipse** e desmarque **Entrar em contato com todos os sites de atualização durante a instalação para encontrar o software necessário**.</span><span class="sxs-lookup"><span data-stu-id="eab65-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="eab65-114">Sua tela será semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="eab65-114">Your screen should appear similar to the following:</span></span>
   
   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][02]

1. <span data-ttu-id="eab65-116">Se você expandir o **Kit de Ferramentas do Azure para Eclipse**, verá uma lista de itens como um exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="eab65-116">If you expand the **Azure Toolkit for Eclipse**, you will see a list of items like following example:</span></span>
   
   * <span data-ttu-id="eab65-117">**Plug-in do Application Insights para Java**: este componente permite que você use os serviços de registro em log e análise de telemetria do Azure para seus aplicativos e instâncias de servidor.</span><span class="sxs-lookup"><span data-stu-id="eab65-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="eab65-118">**Filtro dos Serviços de Controle de Acesso do Azure**: esse componente oferece suporte para autenticar usuários de aplicativo com o Azure ACS, habilitar cenários de logon únicos e externalização lógica da identidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eab65-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="eab65-119">**Plug-in comum do Azure**: esse componente fornece a funcionalidade comum necessária para outros componentes do kit de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="eab65-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="eab65-120">**Azure Explorer para Eclipse**: esse componente fornece a funcionalidade comum necessária para outros componentes do kit de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="eab65-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="eab65-121">**Plug-in do azure para Eclipse com Java**: esse componente oferece suporte para o desenvolvimento de projetos que ajudam a criar, testar e implantar aplicativos Java para a nuvem do Microsoft Azure no Eclipse e via linha de comando.</span><span class="sxs-lookup"><span data-stu-id="eab65-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="eab65-122">**Plug-in de aplicativos Web do Azure com Java**: esse componente oferece suporte para implantar os aplicativos Web Java para contêineres de aplicativo Web do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eab65-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="eab65-123">**Microsoft JDBC Driver 4.2 para SQL Server**: esse componente fornece a API JDBC para SQL Server e Banco de Dados SQL do Microsoft Azure para Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="eab65-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="eab65-124">**Pacote para Bibliotecas de Cliente do Apache Qpid para JMS**: esse componente fornece o componente de cliente JMS a partir do projeto do Apache Qpid para habilitar seu aplicativo a usar o sistema de mensagens baseado no protocolo AMQP no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eab65-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="eab65-125">**Pacote para Bibliotecas do Microsoft Azure para Java**: esse componente fornece APIs para acessar serviços do Microsoft Azure, como armazenamento, barramento de serviço, tempo de execução do serviço, etc.</span><span class="sxs-lookup"><span data-stu-id="eab65-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>

1. <span data-ttu-id="eab65-126">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="eab65-126">Click **Next**.</span></span> <span data-ttu-id="eab65-127">(Se você experimentar atrasos incomuns ao instalar o kit de ferramentas, certifique-se de que a opção **Contatar todos os sites de atualização durante a instalação para encontrar o software necessário** está desmarcada.)</span><span class="sxs-lookup"><span data-stu-id="eab65-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="eab65-128">No diálogo **Instalar Detalhes**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="eab65-128">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Revisão dos detalhes de instalação][03]

1. <span data-ttu-id="eab65-130">No diálogo **Examinar Licenças** , leia os termos dos contratos de licença.</span><span class="sxs-lookup"><span data-stu-id="eab65-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="eab65-131">Se você aceitar os termos dos contratos de licença, clique em **Aceito os termos dos contratos de licença** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="eab65-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="eab65-132">(As etapas restantes supõem que você aceite os termos dos contratos de licença.</span><span class="sxs-lookup"><span data-stu-id="eab65-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="eab65-133">Se você não aceitar os termos dos contratos de licença, saia do processo de instalação.)</span><span class="sxs-lookup"><span data-stu-id="eab65-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Examinar Licenças][04]
   
   <span data-ttu-id="eab65-135">O Eclipse baixará e instalará os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="eab65-135">Eclipse will download and install the requisite packages.</span></span>
   
   ![Progresso da Instalação][05]

1. <span data-ttu-id="eab65-137">Se for solicitado a reiniciar o Eclipse para concluir a instalação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="eab65-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Reinicie o prompt][06]

## <a name="next-steps"></a><span data-ttu-id="eab65-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eab65-139">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
