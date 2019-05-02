---
title: Publicar um aplicativo Spring Boot como um contêiner do Docker usando o Kit de Ferramentas do Azure para Eclipse
description: Saiba como publicar um aplicativo Web para o Microsoft Azure como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 5f70d8dd7e9b59c365d83c185f430a5a9c75e838
ms.sourcegitcommit: 4f1acf05e3bbb7eb6bca9b65300c1c5b9772185a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456331"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="9766b-103">Publicar um aplicativo Spring Boot como um contêiner do Docker usando o Kit de Ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="9766b-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="9766b-104">O [Spring Framework] é uma solução de software livre que ajuda os desenvolvedores do Java a criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="9766b-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="9766b-105">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="9766b-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="9766b-106">O [Docker] é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação, o dimensionamento e o gerenciamento de seus aplicativos executados em contêineres.</span><span class="sxs-lookup"><span data-stu-id="9766b-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="9766b-107">Este tutorial explica as etapas para implantação de um aplicativo Spring Boot como um contêiner do Docker no Microsoft Azure usando o Kit de Ferramentas do Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9766b-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a><span data-ttu-id="9766b-108">Clonar o repositório padrão do Spring Boot Docker</span><span class="sxs-lookup"><span data-stu-id="9766b-108">Clone the default Spring Boot Docker repository</span></span>

### <a name="import-the-public-repository"></a><span data-ttu-id="9766b-109">Importar o repositório público</span><span class="sxs-lookup"><span data-stu-id="9766b-109">Import the public repository</span></span>

<span data-ttu-id="9766b-110">As etapas a seguir explicam a clonagem do repositório do Spring Boot Docker para o computador local usando o IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="9766b-110">The following steps walk you through cloning the Spring Boot Docker repository to your local computer by using IntelliJ.</span></span> <span data-ttu-id="9766b-111">Se desejar usar uma linha de comando, consulte [Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure][Deploy Spring Boot on Linux in AKS].</span><span class="sxs-lookup"><span data-stu-id="9766b-111">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="9766b-112">Abra o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9766b-112">Open Eclipse.</span></span>

1. <span data-ttu-id="9766b-113">Clique em **Arquivo** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="9766b-113">Click **File** > **Import**.</span></span>

   ![Menu de Importação de Arquivo][CL01]

1. <span data-ttu-id="9766b-115">Quando a caixa de diálogo **Importação** se abrir:</span><span class="sxs-lookup"><span data-stu-id="9766b-115">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="9766b-116"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-116">a.</span></span> <span data-ttu-id="9766b-117">Expanda **Git**.</span><span class="sxs-lookup"><span data-stu-id="9766b-117">Expand **Git**.</span></span>

   <span data-ttu-id="9766b-118">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-118">b.</span></span> <span data-ttu-id="9766b-119">Selecione **Projetos do Git**.</span><span class="sxs-lookup"><span data-stu-id="9766b-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="9766b-120">c.</span><span class="sxs-lookup"><span data-stu-id="9766b-120">c.</span></span> <span data-ttu-id="9766b-121">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9766b-121">Click **Next**.</span></span>

   ![Caixa de diálogo de Importação][CL02]

1. <span data-ttu-id="9766b-123">Na página **Selecionar a Origem do Repositório**:</span><span class="sxs-lookup"><span data-stu-id="9766b-123">On the **Select Repository Source** page:</span></span>

   <span data-ttu-id="9766b-124"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-124">a.</span></span> <span data-ttu-id="9766b-125">Selecione **Clonar URI**.</span><span class="sxs-lookup"><span data-stu-id="9766b-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="9766b-126">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-126">b.</span></span> <span data-ttu-id="9766b-127">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9766b-127">Click **Next**.</span></span>

   ![Página Selecionar Origem do Repositório][CL03]

1. <span data-ttu-id="9766b-129">Na página **Repositório Git de Origem**:</span><span class="sxs-lookup"><span data-stu-id="9766b-129">On the **Source Git Repository** page:</span></span>

   <span data-ttu-id="9766b-130"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-130">a.</span></span> <span data-ttu-id="9766b-131">Em **URI**, insira `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="9766b-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="9766b-132">Essa etapa deve popular automaticamente os campos **Host** e **Caminho do repositório** com os valores corretos.</span><span class="sxs-lookup"><span data-stu-id="9766b-132">This step should automatically populate the **Host** and **Repository path** fields with the correct values.</span></span>
   
   <span data-ttu-id="9766b-133">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-133">b.</span></span> <span data-ttu-id="9766b-134">O repositório Spring Boot é público, assim, você não precisa inserir seu nome de usuário e senha do Git.</span><span class="sxs-lookup"><span data-stu-id="9766b-134">The Spring Boot repository is public, so you should not have to enter your Git username and password.</span></span>
   
   <span data-ttu-id="9766b-135">c.</span><span class="sxs-lookup"><span data-stu-id="9766b-135">c.</span></span> <span data-ttu-id="9766b-136">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9766b-136">Click **Next**.</span></span>

   ![Página Repositório Git de Origem][CL04]

1. <span data-ttu-id="9766b-138">Na página **Seleção de Branch**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9766b-138">On the **Branch Selection** page, click **Next**.</span></span>

   ![Página Seleção de Branch][CL05]

1. <span data-ttu-id="9766b-140">Na página **Destino Local**:</span><span class="sxs-lookup"><span data-stu-id="9766b-140">On the **Local Destination** page:</span></span>

   <span data-ttu-id="9766b-141"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-141">a.</span></span> <span data-ttu-id="9766b-142">Especifique a pasta local em que você deseja colocar seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="9766b-142">Specify the local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="9766b-143">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-143">b.</span></span> <span data-ttu-id="9766b-144">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9766b-144">Click **Next**.</span></span>

   ![Página Destino Local][CL06]

1. <span data-ttu-id="9766b-146">Na página **Selecionar um assistente a usar para importar projetos**:</span><span class="sxs-lookup"><span data-stu-id="9766b-146">On the **Select a wizard to use for importing projects** page:</span></span>

   <span data-ttu-id="9766b-147"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-147">a.</span></span> <span data-ttu-id="9766b-148">Selecione **Importar como um projeto geral**.</span><span class="sxs-lookup"><span data-stu-id="9766b-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="9766b-149">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-149">b.</span></span> <span data-ttu-id="9766b-150">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9766b-150">Click **Next**.</span></span>

   ![Página “Selecionar um assistente a ser usado para a importação de projetos”][CL07]

1. <span data-ttu-id="9766b-152">Na página **Importar Projetos**:</span><span class="sxs-lookup"><span data-stu-id="9766b-152">On the **Import Projects** page:</span></span>

   <span data-ttu-id="9766b-153"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-153">a.</span></span> <span data-ttu-id="9766b-154">Especifique o nome do projeto.</span><span class="sxs-lookup"><span data-stu-id="9766b-154">Specify your project name.</span></span>
   
   <span data-ttu-id="9766b-155">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-155">b.</span></span> <span data-ttu-id="9766b-156">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="9766b-156">Click **Finish**.</span></span>

   ![Página Importar Projetos][CL08]

1. <span data-ttu-id="9766b-158">Quando o repositório for clonado com êxito, você verá todos os arquivos listados no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9766b-158">When the repository is cloned successfully, you see all the files listed in Eclipse.</span></span>

   ![Repositório local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="9766b-160">Criar um projeto do Maven por meio do repositório local</span><span class="sxs-lookup"><span data-stu-id="9766b-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="9766b-161">O repositório do Spring Boot Docker contém um projeto completo do Maven, que será usado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="9766b-161">The Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="9766b-162">Clique em **Arquivo** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="9766b-162">Click **File** > **Import**.</span></span>

   ![Comando Importar no menu Arquivo][CL01]

1. <span data-ttu-id="9766b-164">Quando a caixa de diálogo **Importação** se abrir:</span><span class="sxs-lookup"><span data-stu-id="9766b-164">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="9766b-165"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-165">a.</span></span> <span data-ttu-id="9766b-166">Expanda **Maven**.</span><span class="sxs-lookup"><span data-stu-id="9766b-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="9766b-167">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-167">b.</span></span> <span data-ttu-id="9766b-168">Selecione **Projetos Existentes do Maven**.</span><span class="sxs-lookup"><span data-stu-id="9766b-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="9766b-169">c.</span><span class="sxs-lookup"><span data-stu-id="9766b-169">c.</span></span> <span data-ttu-id="9766b-170">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="9766b-170">Click **Next**.</span></span>

   ![Caixa de diálogo de Importação][MV01]

1. <span data-ttu-id="9766b-172">Na página **Projetos Maven**:</span><span class="sxs-lookup"><span data-stu-id="9766b-172">On the **Maven Projects** page:</span></span>

   <span data-ttu-id="9766b-173"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-173">a.</span></span> <span data-ttu-id="9766b-174">Em **Diretório Raiz**, especifique a pasta **complete** no repositório local.</span><span class="sxs-lookup"><span data-stu-id="9766b-174">For **Root Directory**, specify the **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="9766b-175">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-175">b.</span></span> <span data-ttu-id="9766b-176">Expanda a seção **Avançado** e insira um nome personalizado para o **Modelo de nome**.</span><span class="sxs-lookup"><span data-stu-id="9766b-176">Expand the **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="9766b-177">c.</span><span class="sxs-lookup"><span data-stu-id="9766b-177">c.</span></span> <span data-ttu-id="9766b-178">Marque a caixa do arquivo **pom.xml** no projeto.</span><span class="sxs-lookup"><span data-stu-id="9766b-178">Select the box for the **pom.xml** file in the project.</span></span>
   
   <span data-ttu-id="9766b-179">d.</span><span class="sxs-lookup"><span data-stu-id="9766b-179">d.</span></span> <span data-ttu-id="9766b-180">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="9766b-180">Click **Finish**.</span></span>

   ![Página Projetos do Maven][MV02]

1. <span data-ttu-id="9766b-182">Quando o projeto do Maven for aberto com êxito, você verá um segundo projeto listado no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9766b-182">When the Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Projeto do Maven local][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="9766b-184">Criar o aplicativo Spring Boot usando o Maven</span><span class="sxs-lookup"><span data-stu-id="9766b-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="9766b-185">No Eclipse Project Explorer, selecione o projeto do Maven.</span><span class="sxs-lookup"><span data-stu-id="9766b-185">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="9766b-186">Clique em **Executar** > **Executar Como** > **Build do Maven**.</span><span class="sxs-lookup"><span data-stu-id="9766b-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Comandos a serem executados como build do Maven][BU01]

1. <span data-ttu-id="9766b-188">Quando o aplicativo é criado com êxito, a janela do console mostra o status.</span><span class="sxs-lookup"><span data-stu-id="9766b-188">When your application is successfully built, the console window shows the status.</span></span>

   ![Build bem-sucedido do Maven][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="9766b-190">Publicar seu aplicativo Web no Azure usando um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="9766b-190">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="9766b-191">No Eclipse Project Explorer, selecione o projeto do Maven.</span><span class="sxs-lookup"><span data-stu-id="9766b-191">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="9766b-192">Clique no menu **Publicar** do Azure e, em seguida, clique em **Publicar como Contêiner do Docker**.</span><span class="sxs-lookup"><span data-stu-id="9766b-192">Click the Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Comando Publicar como Contêiner do Docker][PU01]

1. <span data-ttu-id="9766b-194">Quando a caixa de diálogo **Implantando Contêiner do Docker no Azure** for exibida:</span><span class="sxs-lookup"><span data-stu-id="9766b-194">When the **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="9766b-195"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-195">a.</span></span> <span data-ttu-id="9766b-196">Insira um nome de imagem do Docker personalizado.</span><span class="sxs-lookup"><span data-stu-id="9766b-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="9766b-197">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-197">b.</span></span> <span data-ttu-id="9766b-198">Para **Artefato a ser implantado**, especifique o caminho para o arquivo **gs-spring-boot-docker-0.1.0.jar** que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="9766b-198">For **Artifact to deploy**, specify the path to the **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Especificar opções do Docker][PU02]

   <span data-ttu-id="9766b-200">Os hosts existentes do Docker são exibidos.</span><span class="sxs-lookup"><span data-stu-id="9766b-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="9766b-201">Se você optar por implantar em um host existente, vá para a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="9766b-201">If you choose to deploy to an existing host, you can skip to step 5.</span></span> <span data-ttu-id="9766b-202">Caso contrário, use as seguintes etapas para criar um host:</span><span class="sxs-lookup"><span data-stu-id="9766b-202">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="9766b-203"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-203">a.</span></span> <span data-ttu-id="9766b-204">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9766b-204">Click **Add**.</span></span>

      ![Adicionar um novo host do Docker][PU03]

   <span data-ttu-id="9766b-206">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-206">b.</span></span> <span data-ttu-id="9766b-207">Quando a caixa de diálogo **Criar Host do Docker** for exibida, você poderá optar por aceitar os padrões ou especificar configurações personalizadas para o novo host do Docker.</span><span class="sxs-lookup"><span data-stu-id="9766b-207">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="9766b-208">(Para obter descrições detalhadas das várias configurações, consulte [Publicar um aplicativo Web como um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ][Publish Container with Azure Toolkit].) Clique em **Próximo** quando tiver especificado as configurações a serem usadas.</span><span class="sxs-lookup"><span data-stu-id="9766b-208">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Especificar opções de host do Docker][PU04]

   <span data-ttu-id="9766b-210">c.</span><span class="sxs-lookup"><span data-stu-id="9766b-210">c.</span></span> <span data-ttu-id="9766b-211">Você pode optar por usar as credenciais de logon existentes de um Azure Key Vault ou inserir novas credenciais de logon do Docker.</span><span class="sxs-lookup"><span data-stu-id="9766b-211">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="9766b-212">Clique em **Concluir** quando tiver especificado suas opções.</span><span class="sxs-lookup"><span data-stu-id="9766b-212">Click **Finish** when you have specified your options.</span></span>

      ![Especificar as credenciais de host do Docker][PU05]

1. <span data-ttu-id="9766b-214">Selecione o host do Docker e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9766b-214">Select your Docker host, and then click **Next**.</span></span>

   ![Selecione o host do Docker a usar][PU06]

1. <span data-ttu-id="9766b-216">Na última página da caixa de diálogo **Implantando o Contêiner do Docker no Azure**, especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="9766b-216">On the last page of the **Deploying Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="9766b-217"> a.</span><span class="sxs-lookup"><span data-stu-id="9766b-217">a.</span></span> <span data-ttu-id="9766b-218">Você pode optar por especificar um nome personalizado para o contêiner que hospedará o contêiner do Docker ou aceitar o padrão.</span><span class="sxs-lookup"><span data-stu-id="9766b-218">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="9766b-219">b.</span><span class="sxs-lookup"><span data-stu-id="9766b-219">b.</span></span> <span data-ttu-id="9766b-220">Insira as portas TCP do host do Docker usando a seguinte sintaxe: *[external port]*:*[internal port]*.</span><span class="sxs-lookup"><span data-stu-id="9766b-220">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="9766b-221">Por exemplo, **80:8080** especifica uma porta externa 80 e a porta interna padrão 8080 do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="9766b-221">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="9766b-222">Se você tiver personalizado a porta interna (por exemplo, editando o arquivo application.yml), precisará especificar o número da porta para o roteamento correto ocorrer no Azure.</span><span class="sxs-lookup"><span data-stu-id="9766b-222">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="9766b-223">c.</span><span class="sxs-lookup"><span data-stu-id="9766b-223">c.</span></span> <span data-ttu-id="9766b-224">Depois de configurar essas opções, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="9766b-224">After you configure these options, click **Finish**.</span></span>

   ![Implantar um contêiner do Docker no Azure][PU07]

1. <span data-ttu-id="9766b-226">Quando o Kit de Ferramentas do Azure concluir a publicação, o Log de Atividades do Azure exibirá **Publicado** como o status.</span><span class="sxs-lookup"><span data-stu-id="9766b-226">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Host do Docker implantado com êxito][PU08]

## <a name="next-steps"></a><span data-ttu-id="9766b-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9766b-228">Next steps</span></span>

<span data-ttu-id="9766b-229">Para obter recursos adicionais para o Docker, consulte o [site do Docker](https://www.docker.com/) oficial.</span><span class="sxs-lookup"><span data-stu-id="9766b-229">For additional resources for Docker, see the official [Docker website](https://www.docker.com/).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: azure-toolkit-for-eclipse-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
