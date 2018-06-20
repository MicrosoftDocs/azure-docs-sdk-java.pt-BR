---
title: Criar um aplicativo Web Olá, Mundo para o Azure usando o kit de ferramentas herdado do IntelliJ
description: Este tutorial mostra como usar a versão 3.0.6 (ou anterior) do Kit de Ferramentas do Azure para IntelliJ para criar um aplicativo Web Olá, Mundo para o Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ebe98a604b52dc9a4b5a47cbf65a4c68a5c86fe3
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954777"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a><span data-ttu-id="0fcff-103">Criar um aplicativo Web Olá, Mundo para o Azure usando o kit de ferramentas herdado do IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0fcff-103">Create a Hello World web app for Azure using the legacy toolkit for IntelliJ</span></span>

<span data-ttu-id="0fcff-104">Este tutorial mostra como criar e implantar um aplicativo Olá, Mundo básico para o Azure como um aplicativo Web usando a versão 3.0.6 (ou anterior) do [Kit de Ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="0fcff-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="0fcff-105">Para obter uma versão deste artigo que usa o [Kit de Ferramentas do Azure para Eclipse], consulte [Criar um aplicativo Web Olá, Mundo para o Azure usando o Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="0fcff-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="0fcff-106">O Kit de Ferramentas do Azure para IntelliJ foi atualizado em agosto de 2017 com um fluxo de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="0fcff-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="0fcff-107">Este artigo mostra a criação de um aplicativo Web Olá, Mundo usando a versão 3.0.6 (ou anterior) do Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0fcff-107">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="0fcff-108">Se você estiver usando a versão 3.0.7 (ou posterior) do kit de ferramentas, precisará seguir as etapas em [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ][Updated Version].</span><span class="sxs-lookup"><span data-stu-id="0fcff-108">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ][Updated Version].</span></span>
>

<span data-ttu-id="0fcff-109">Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="0fcff-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Visualização do aplicativo Hello World][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="0fcff-111">Criar um novo projeto do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="0fcff-111">Create a new web app project</span></span>

1. <span data-ttu-id="0fcff-112">Inicie o IntelliJ e entre em sua conta do Azure usando as instruções no artigo [Instruções de entrada do Azure para o Kit de Ferramentas do Azure para IntelliJ][intelliJ-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="0fcff-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="0fcff-113">Clique menu **Arquivo**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Arquivo Novo Projeto][02]

2. <span data-ttu-id="0fcff-115">Na caixa de diálogo **Novo Projeto**, selecione **Java**, **Aplicativo Web** e clique em **Avançar** para adicionar um SDK do Projeto.</span><span class="sxs-lookup"><span data-stu-id="0fcff-115">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![Caixa de diálogo Novo Projeto][03a]
   
3. <span data-ttu-id="0fcff-117">Na caixa de diálogo Selecionar o Diretório Base para o JDK, selecione a pasta onde o JDK está instalado e clique **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-117">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="0fcff-118">Clique em **Avançar** na caixa de diálogo Novo Projeto para continuar.</span><span class="sxs-lookup"><span data-stu-id="0fcff-118">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![Especificar o diretório base do JDK][03b]

4. <span data-ttu-id="0fcff-120">Para a finalidade deste tutorial, nomeie o projeto como **Java-Web-App-On-Azure** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-120">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![Caixa de diálogo Novo Projeto][04]

5. <span data-ttu-id="0fcff-122">Na exibição do Explorador de Projetos do IntelliJ, expanda **Java-Web-App-On-Azure**, expanda **Web** e clique duas vezes em **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-122">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![Abrir Índice de Página][05c]

6. <span data-ttu-id="0fcff-124">Quando o arquivo index.jsp for aberto no IntelliJ, adicione o texto para exibir dinamicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="0fcff-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="0fcff-125">dentro do elemento existente `<body>`.</span><span class="sxs-lookup"><span data-stu-id="0fcff-125">within the existing `<body>` element.</span></span> <span data-ttu-id="0fcff-126">Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0fcff-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="0fcff-127">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="0fcff-127">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="0fcff-128">Implante seu aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="0fcff-128">Deploy your web app to Azure</span></span>

<span data-ttu-id="0fcff-129">Há várias maneiras pelas quais você pode implantar um aplicativo Web Java no Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcff-129">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="0fcff-130">Este tutorial descreve uma das mais simples: o aplicativo será implantado em um contêiner de aplicativos Web do Azure, e não há a necessidade de qualquer tipo de projeto especial nem de ferramentas adicionais.</span><span class="sxs-lookup"><span data-stu-id="0fcff-130">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="0fcff-131">O JDK e o software do contêiner da Web serão fornecidos a você pelo Azure, portanto, não é necessário carregar seu próprio; tudo o que você precisa é de seu aplicativo Web Java.</span><span class="sxs-lookup"><span data-stu-id="0fcff-131">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="0fcff-132">Como resultado, o processo de publicação de seu aplicativo demorará segundos, e não minutos.</span><span class="sxs-lookup"><span data-stu-id="0fcff-132">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="0fcff-133">Antes de publicar seu aplicativo, você precisa definir as configurações de módulo.</span><span class="sxs-lookup"><span data-stu-id="0fcff-133">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="0fcff-134">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0fcff-134">To do so, use the following steps:</span></span>

1. <span data-ttu-id="0fcff-135">No Explorador de Projetos do IntelliJ, clique com o botão direito do mouse no projeto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="0fcff-135">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="0fcff-136">Quando o menu de contexto for exibido, clique em **Abrir Configurações do Módulo**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-136">When the context menu appears, click **Open Module Settings**.</span></span>

   ![Abrir configurações do módulo][05a]

2. <span data-ttu-id="0fcff-138">Quando a caixa de diálogo Estrutura do Projeto aparece:</span><span class="sxs-lookup"><span data-stu-id="0fcff-138">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="0fcff-139">a.</span><span class="sxs-lookup"><span data-stu-id="0fcff-139">a.</span></span> <span data-ttu-id="0fcff-140">Clique em **Artefatos** na lista de **Configurações do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-140">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="0fcff-141">b.</span><span class="sxs-lookup"><span data-stu-id="0fcff-141">b.</span></span> <span data-ttu-id="0fcff-142">Altere o nome do artefato na caixa **Nome** de modo que ele não contenha caracteres especiais ou espaços em branco. Isso é necessário porque o nome será usado no URI (Uniform Resource Identifier).</span><span class="sxs-lookup"><span data-stu-id="0fcff-142">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="0fcff-143">c.</span><span class="sxs-lookup"><span data-stu-id="0fcff-143">c.</span></span> <span data-ttu-id="0fcff-144">Altere o **Tipo** para **Aplicativo Web: arquivo**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-144">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="0fcff-145">d.</span><span class="sxs-lookup"><span data-stu-id="0fcff-145">d.</span></span> <span data-ttu-id="0fcff-146">Clique em **OK** para fechar a caixa de diálogo Estrutura de Projeto.</span><span class="sxs-lookup"><span data-stu-id="0fcff-146">Click **OK** to close the Project Structure dialog box.</span></span>

   ![Abrir configurações do módulo][05b]

<span data-ttu-id="0fcff-148">Quando você tiver definido suas configurações de módulo, poderá publicar seu aplicativo no Azure usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0fcff-148">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="0fcff-149">No Explorador de Projetos do IntelliJ, clique com o botão direito do mouse no projeto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="0fcff-149">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="0fcff-150">Quando o menu de contexto for exibido, selecione **Azure** e clique em **Publicar como Aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="0fcff-150">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Menu de Contexto de Publicação do Azure][06]

2. <span data-ttu-id="0fcff-152">Se você ainda não tiver entrado no Azure pelo IntelliJ, será solicitada a entrada em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcff-152">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="0fcff-153">(Se você tiver várias contas do Azure, alguns dos avisos mostrados durante o processo de entrada poderão ser exibidos mais de uma vez, mesmo se forem aparentemente os mesmos.</span><span class="sxs-lookup"><span data-stu-id="0fcff-153">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="0fcff-154">Quando isso acontecer, continue seguindo as instruções de entrada.)</span><span class="sxs-lookup"><span data-stu-id="0fcff-154">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Caixa de diálogo Login do Azure][07]

3. <span data-ttu-id="0fcff-156">Após a conexão bem-sucedida em sua conta do Azure, a caixa de diálogo **Gerenciar Assinaturas** exibirá uma lista de assinaturas associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="0fcff-156">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="0fcff-157">(Se houver várias assinaturas listadas e você quiser trabalhar com apenas um subconjunto específico, será possível desmarcar as que não deseja usar.) Depois de selecionar suas assinaturas, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-157">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Gerenciar Assinaturas][08]

4. <span data-ttu-id="0fcff-159">Quando a caixa de diálogo **Implantar no Contêiner do Aplicativo Web do Azure** for mostrada, ela exibirá todos os contêineres do Aplicativo Web criados anteriormente por você; se você não tiver criado nenhum contêiner, a lista estará vazia.</span><span class="sxs-lookup"><span data-stu-id="0fcff-159">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Contêineres de Aplicativo][09]

5. <span data-ttu-id="0fcff-161">Se você nunca tiver criado um contêiner de aplicativos Web do Azure, ou se quiser publicar seu aplicativo em um novo contêiner, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fcff-161">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="0fcff-162">Caso contrário, selecione um Contêiner de Aplicativo Web existente e pule para a etapa 6 abaixo.</span><span class="sxs-lookup"><span data-stu-id="0fcff-162">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="0fcff-163">a.</span><span class="sxs-lookup"><span data-stu-id="0fcff-163">a.</span></span> <span data-ttu-id="0fcff-164">Clique no sinal **+**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-164">Click the **+** sign.</span></span>
      
      ![Adicionar Contêiner de Aplicativo][10]

   <span data-ttu-id="0fcff-166">b.</span><span class="sxs-lookup"><span data-stu-id="0fcff-166">b.</span></span> <span data-ttu-id="0fcff-167">A caixa de diálogo **Novo Contêiner de Aplicativo Web** será exibida e será usada nas próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="0fcff-167">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![Novo Contêiner de Aplicativo][11a]
   
   <span data-ttu-id="0fcff-169">c.</span><span class="sxs-lookup"><span data-stu-id="0fcff-169">c.</span></span> <span data-ttu-id="0fcff-170">Insira um **Rótulo DNS** para seu Contêiner do Aplicativo Web; isso formará o rótulo DNS folha da URL do host de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcff-170">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="0fcff-171">Observe que o nome deve estar disponível e de acordo com os requisitos de nomenclatura de aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcff-171">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="0fcff-172">d.</span><span class="sxs-lookup"><span data-stu-id="0fcff-172">d.</span></span> <span data-ttu-id="0fcff-173">No menu suspenso **Contêiner da Web** , selecione o software apropriado ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0fcff-173">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="0fcff-174">No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="0fcff-174">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="0fcff-175">Uma distribuição recente do software selecionado será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcff-175">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="0fcff-176">e.</span><span class="sxs-lookup"><span data-stu-id="0fcff-176">e.</span></span> <span data-ttu-id="0fcff-177">No menu suspenso **Assinatura** , selecione a assinatura que deseja usar para essa implantação.</span><span class="sxs-lookup"><span data-stu-id="0fcff-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="0fcff-178">f.</span><span class="sxs-lookup"><span data-stu-id="0fcff-178">f.</span></span> <span data-ttu-id="0fcff-179">No menu suspenso **Grupo de Recursos** , selecione o Grupo de Recursos com o qual deseja associar seu Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0fcff-179">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="0fcff-180">(Os Grupos de Recursos do Azure lhe permitem agrupar recursos relacionados para que, por exemplo, possam ser excluídos juntos.)</span><span class="sxs-lookup"><span data-stu-id="0fcff-180">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="0fcff-181">Você pode selecionar um Grupo de Recursos existente (se houver) e ignorar a etapa g abaixo ou usar as seguintes etapas para criar um novo Grupo de Recursos:</span><span class="sxs-lookup"><span data-stu-id="0fcff-181">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="0fcff-182">Selecione **&lt;&lt; Criar novo grupo de recursos &gt;&gt;** no menu suspenso **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-182">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="0fcff-183">A caixa de diálogo **Novo Grupo de Recursos** será exibida:</span><span class="sxs-lookup"><span data-stu-id="0fcff-183">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![Novo grupo de recursos][12]

      * <span data-ttu-id="0fcff-185">Na caixa de texto **Nome**, especifique um nome para o novo Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="0fcff-185">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="0fcff-186">No menu suspenso **Região**, selecione a localização do data center do Azure apropriada ao Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="0fcff-186">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="0fcff-187">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-187">Click **OK**.</span></span>

   <span data-ttu-id="0fcff-188">g.</span><span class="sxs-lookup"><span data-stu-id="0fcff-188">g.</span></span> <span data-ttu-id="0fcff-189">O menu suspenso **Plano do Serviço de Aplicativo** lista os planos do serviço de aplicativo associados ao Grupo de Recursos selecionado.</span><span class="sxs-lookup"><span data-stu-id="0fcff-189">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="0fcff-190">(Um Plano do Serviço de Aplicativo especifica informações como o local de seu Aplicativo Web, o tipo de preço e o tamanho da instância de computação.</span><span class="sxs-lookup"><span data-stu-id="0fcff-190">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="0fcff-191">Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)</span><span class="sxs-lookup"><span data-stu-id="0fcff-191">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="0fcff-192">Você pode selecionar um Plano do Serviço de Aplicativo existente (se houver) e ignorar a etapa h abaixo ou usar as seguintes etapas para criar um novo Plano do Serviço de Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="0fcff-192">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="0fcff-193">Selecione **&lt;&lt; Criar novo plano do Serviço de Aplicativo &gt;&gt;** no menu suspenso **Plano do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-193">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="0fcff-194">A caixa de diálogo **Novo Plano do Serviço de Aplicativo** será exibida:</span><span class="sxs-lookup"><span data-stu-id="0fcff-194">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![Novo Plano do Serviço de Aplicativo][13]

      * <span data-ttu-id="0fcff-196">Na caixa de texto **Nome**, especifique um nome para o novo Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0fcff-196">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="0fcff-197">No menu suspenso **Localização**, selecione a localização do data center do Azure apropriada ao plano.</span><span class="sxs-lookup"><span data-stu-id="0fcff-197">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="0fcff-198">No menu suspenso **Tipo de Preço**, selecione o preço apropriado ao plano.</span><span class="sxs-lookup"><span data-stu-id="0fcff-198">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="0fcff-199">Para fins de teste, é possível escolher **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-199">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="0fcff-200">No menu suspenso **Tamanho da Instância**, selecione o tamanho de instância apropriado ao plano.</span><span class="sxs-lookup"><span data-stu-id="0fcff-200">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="0fcff-201">Para fins de teste, é possível escolher **Pequeno**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-201">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="0fcff-202">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-202">Click **OK**.</span></span>

   <span data-ttu-id="0fcff-203">h.</span><span class="sxs-lookup"><span data-stu-id="0fcff-203">h.</span></span> <span data-ttu-id="0fcff-204">(Opcional) Por padrão, uma distribuição recente de Java 8 será implantada automaticamente como sua JVM pelo Azure no contêiner do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0fcff-204">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="0fcff-205">No entanto, você pode selecionar uma versão diferente e uma distribuição da JVM.</span><span class="sxs-lookup"><span data-stu-id="0fcff-205">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="0fcff-206">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0fcff-206">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="0fcff-207">Clique na guia **JDK** na caixa de diálogo **Novo Contêiner do Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-207">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="0fcff-208">Você pode escolher entre uma das duas seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="0fcff-208">You can choose from one of the following options:</span></span>
        
         * <span data-ttu-id="0fcff-209">Implantar o JDK padrão, que é oferecido pelo Azure</span><span class="sxs-lookup"><span data-stu-id="0fcff-209">Deploy the default JDK which is offered by Azure</span></span>
         * <span data-ttu-id="0fcff-210">Implantar um JDK de terceiros de uma lista suspensa de JDKs adicionais que estão disponíveis no Azure</span><span class="sxs-lookup"><span data-stu-id="0fcff-210">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
         * <span data-ttu-id="0fcff-211">Implantar um JDK personalizado, que deve ser empacotado como um arquivo ZIP e ser publicamente disponível ou em sua conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0fcff-211">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
      ![Guia Novo JDK de Contêiner de Aplicativo][11b]

   <span data-ttu-id="0fcff-213">i.</span><span class="sxs-lookup"><span data-stu-id="0fcff-213">i.</span></span> <span data-ttu-id="0fcff-214">Depois de concluir todas as etapas acima, a caixa de diálogo New Web App Container (Novo Contêiner de Aplicativos Web) deve ser semelhante à ilustração a seguir:</span><span class="sxs-lookup"><span data-stu-id="0fcff-214">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Novo Contêiner de Aplicativo][14]
   
   <span data-ttu-id="0fcff-216">j.</span><span class="sxs-lookup"><span data-stu-id="0fcff-216">j.</span></span> <span data-ttu-id="0fcff-217">Clique em **OK** para concluir a criação do novo contêiner do Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0fcff-217">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="0fcff-218">Aguarde alguns segundos para a lista de contêineres de Aplicativo Web ser atualizada. O contêiner do aplicativo Web recém-criado agora deve ser selecionado na lista.</span><span class="sxs-lookup"><span data-stu-id="0fcff-218">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="0fcff-219">Agora você está pronto para concluir a implantação inicial do seu aplicativo Web no Azure. Clique em **OK** para implantar seu aplicativo Java no contêiner do aplicativo Web selecionado.</span><span class="sxs-lookup"><span data-stu-id="0fcff-219">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="0fcff-220">Por padrão, o aplicativo será implantado como um subdiretório do servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0fcff-220">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="0fcff-221">Se desejar implantá-lo como o aplicativo raiz, marque a caixa de seleção **Implantar na raiz** antes de clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-221">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![Implantar no Azure][15]

7. <span data-ttu-id="0fcff-223">Em seguida, você deverá ver o modo de exibição do **Log de Atividades do Azure** , que indicará o status da implantação de seu Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0fcff-223">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Indicador de Progresso][16]
   
   <span data-ttu-id="0fcff-225">O processo de implantação de seu aplicativo Web no Azure deve demorar apenas alguns segundos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="0fcff-225">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="0fcff-226">Quando seu aplicativo estiver pronto, você verá um link chamado **Publicado** na coluna **Status**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-226">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="0fcff-227">Quando você clicar no link, ele o levará à página inicial do seu aplicativo Web implantado, ou você pode usar as etapas da seção a seguir para navegar até o seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0fcff-227">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="0fcff-228">Navegando até seu aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="0fcff-228">Browsing to your Web App on Azure</span></span>

<span data-ttu-id="0fcff-229">Para navegar até o aplicativo Web no Azure, você poderá usar o modo de exibição do **Azure Explorer** .</span><span class="sxs-lookup"><span data-stu-id="0fcff-229">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="0fcff-230">Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Exibir** no IntelliJ, clicando em **Janelas de Ferramentas** e em **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-230">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="0fcff-231">Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="0fcff-231">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="0fcff-232">Quando o modo de exibição do **Azure Explorer** for exibido, use estas etapas para navegar pelo aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="0fcff-232">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="0fcff-233">Expanda o nó **Azure** .</span><span class="sxs-lookup"><span data-stu-id="0fcff-233">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="0fcff-234">Expanda o nó **Aplicativos Web** .</span><span class="sxs-lookup"><span data-stu-id="0fcff-234">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="0fcff-235">Clique com botão direito do mouse no Aplicativo Web desejado.</span><span class="sxs-lookup"><span data-stu-id="0fcff-235">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="0fcff-236">Quando o menu de contexto for exibido, clique em **Abrir no Navegador**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-236">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![Procurar o Aplicativo Web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="0fcff-238">Atualizando seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="0fcff-238">Updating your web app</span></span>

<span data-ttu-id="0fcff-239">A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:</span><span class="sxs-lookup"><span data-stu-id="0fcff-239">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="0fcff-240">Você pode atualizar a implantação de um aplicativo Web Java existente.</span><span class="sxs-lookup"><span data-stu-id="0fcff-240">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="0fcff-241">Você pode publicar um aplicativo Java adicional no mesmo contêiner de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0fcff-241">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="0fcff-242">Em ambos os casos, o processo é idêntico e demora apenas alguns segundos:</span><span class="sxs-lookup"><span data-stu-id="0fcff-242">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="0fcff-243">No explorador de projetos do IntelliJ, clique com o botão direito do mouse no aplicativo Java que você deseja atualizar ou adicionar a um contêiner de aplicativos Web existente.</span><span class="sxs-lookup"><span data-stu-id="0fcff-243">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="0fcff-244">Quando o menu de contexto for exibido, selecione **Azure** e, em seguida, **Publicar como Aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="0fcff-244">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="0fcff-245">Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes.</span><span class="sxs-lookup"><span data-stu-id="0fcff-245">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="0fcff-246">Selecione aquele no qual deseja publicar ou publicar novamente o aplicativo Java e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-246">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="0fcff-247">Após alguns segundos, o modo de exibição do **Log de Atividades do Azure** mostrará a implantação atualizada como **Publicada** e será possível verificar o aplicativo atualizado em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="0fcff-247">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="0fcff-248">Iniciar, parar ou reiniciar o aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="0fcff-248">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="0fcff-249">Para iniciar ou parar um contêiner do Aplicativo Web do Azure existente, (incluindo todos os aplicativos Java implantados nele), é possível usar o modo de exibição do **Azure Explorer** .</span><span class="sxs-lookup"><span data-stu-id="0fcff-249">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="0fcff-250">Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Exibir** no IntelliJ, clicando em **Janelas de Ferramentas** e em **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-250">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="0fcff-251">Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="0fcff-251">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="0fcff-252">Quando o modo de exibição do **Azure Explorer** for exibido, siga estas etapas para iniciar ou parar o Aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="0fcff-252">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="0fcff-253">Expanda o nó **Azure** .</span><span class="sxs-lookup"><span data-stu-id="0fcff-253">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="0fcff-254">Expanda o nó **Aplicativos Web** .</span><span class="sxs-lookup"><span data-stu-id="0fcff-254">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="0fcff-255">Clique com botão direito do mouse no Aplicativo Web desejado.</span><span class="sxs-lookup"><span data-stu-id="0fcff-255">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="0fcff-256">Quando o menu de contexto for exibido, clique em **Iniciar**, **Parar** ou **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="0fcff-256">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="0fcff-257">Observe que as opções de menu são sensíveis ao contexto, para que você só possa parar um aplicativo Web que esteja em execução ou iniciar um aplicativo Web que não esteja em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="0fcff-257">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Parar Aplicativo Web][18]

## <a name="next-steps"></a><span data-ttu-id="0fcff-259">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fcff-259">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="0fcff-260">Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="0fcff-260">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de Ferramentas do Azure para IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Kit de Ferramentas do Azure para Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Visão geral de Aplicativos Web]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-intellij-create-hello-world-web-app.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/18-Stop-Web-App.png
