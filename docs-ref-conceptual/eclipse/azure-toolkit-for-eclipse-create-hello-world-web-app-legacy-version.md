---
title: ''
description: Este tutorial mostra como usar a versão 3.0.6 (ou anterior) do Kit de Ferramentas do Azure para Eclipse para criar um aplicativo Web Olá, Mundo para o Azure.
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
ms.openlocfilehash: 8b831f4545be9162d28f8ba86eb7271ffa4391af
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954737"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a><span data-ttu-id="90311-102">Criar um aplicativo Web Olá, Mundo para o Azure usando o kit de ferramentas herdado do Eclipse</span><span class="sxs-lookup"><span data-stu-id="90311-102">Create a Hello World web app for Azure using the legacy toolkit for Eclipse</span></span>

<span data-ttu-id="90311-103">Este tutorial mostra como criar e implantar um aplicativo Olá, Mundo básico para o Azure como um aplicativo Web usando a versão 3.0.6 (ou anterior) do [Kit de Ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="90311-103">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="90311-104">Para obter uma versão deste artigo que usa o [Kit de Ferramentas do Azure para IntelliJ], consulte [Criar um aplicativo Web Olá, Mundo para o Azure usando o IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="90311-104">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="90311-105">O Kit de Ferramentas do Azure para Eclipse foi atualizado em agosto de 2017, com um fluxo de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="90311-105">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="90311-106">Este artigo mostra a criação de um aplicativo Web Olá, Mundo usando a versão 3.0.6 (ou anterior) do Kit de Ferramentas do Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="90311-106">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="90311-107">Se você estiver usando a versão 3.0.7 (ou posterior) do kit de ferramentas, precisará seguir as etapas em [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse][Updated Version].</span><span class="sxs-lookup"><span data-stu-id="90311-107">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse][Updated Version].</span></span>
>

<span data-ttu-id="90311-108">Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="90311-108">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Visualização do aplicativo Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="90311-110">Criar um novo projeto do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="90311-110">Create a new web app project</span></span>

1. <span data-ttu-id="90311-111">Inicie o Eclipse e entre em sua conta do Azure usando as instruções no artigo [Instruções de entrada do Azure para o Kit de Ferramentas do Azure para Eclipse][eclipse-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="90311-111">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="90311-112">Clique em **Arquivo**, **Novo**, em seguida, clique em **Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="90311-112">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="90311-113">(Se você não vir o **Projeto Web Dinâmico** listado como um projeto disponível depois de clicar em **Arquivo** e em **Novo**, faça o seguinte: clique em **Arquivo**, clique em **Novo**, clique em **Projeto...**, expanda **Web**, clique em **Projeto Web Dinâmico** e clique em **Avançar**.)</span><span class="sxs-lookup"><span data-stu-id="90311-113">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="90311-114">Para o objetivo deste tutorial, nomeie o projeto **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="90311-114">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="90311-115">Sua tela será semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="90311-115">Your screen will appear similar to the following:</span></span>
   
   ![Criando um novo projeto Web dinâmico][02]

3. <span data-ttu-id="90311-117">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="90311-117">Click **Finish**.</span></span>

4. <span data-ttu-id="90311-118">Na exibição **Gerenciador de Projetos** do Eclipse, expanda **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="90311-118">Within Eclipse's **Project Explorer** view, expand **MyWebApp**.</span></span> <span data-ttu-id="90311-119">Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="90311-119">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="90311-120">Na caixa de diálogo **Novo Arquivo JSP**, nomeie o arquivo **index.jsp**, mantenha a pasta pai como **MyWebApp/WebContent** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="90311-120">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="90311-121">Na caixa de diálogo **Selecionar Modelo JSP**, para a finalidade deste tutorial, escolha **Novo Arquivo JSP (html)** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="90311-121">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="90311-122">Quando o arquivo index.jsp for aberto no Eclipse, adicione o texto para exibir dinamicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="90311-122">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="90311-123">dentro do elemento existente `<body>`.</span><span class="sxs-lookup"><span data-stu-id="90311-123">within the existing `<body>` element.</span></span> <span data-ttu-id="90311-124">Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="90311-124">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="90311-125">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="90311-125">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="90311-126">Implante seu aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="90311-126">Deploy your web app to Azure</span></span>

<span data-ttu-id="90311-127">Há várias maneiras pelas quais você pode implantar um aplicativo Web Java no Azure.</span><span class="sxs-lookup"><span data-stu-id="90311-127">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="90311-128">Este tutorial descreve uma das mais simples: o aplicativo será implantado em um contêiner de aplicativos Web do Azure, e não há a necessidade de qualquer tipo de projeto especial nem de ferramentas adicionais.</span><span class="sxs-lookup"><span data-stu-id="90311-128">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="90311-129">O JDK e o software do contêiner da Web serão fornecidos a você pelo Azure, portanto, não é necessário carregar seu próprio; tudo o que você precisa é de seu aplicativo Web Java.</span><span class="sxs-lookup"><span data-stu-id="90311-129">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="90311-130">Como resultado, o processo de publicação de seu aplicativo demorará segundos, e não minutos.</span><span class="sxs-lookup"><span data-stu-id="90311-130">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="90311-131">No Gerenciador de Projetos do Eclipse, clique com o botão direito do mouse em **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="90311-131">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="90311-132">No menu de contexto, selecione **Azure** e clique em **Publicar como Aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="90311-132">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Publicar como Aplicativo Web do Azure][03]
   
   <span data-ttu-id="90311-134">Como alternativa, enquanto o projeto do aplicativo Web é selecionado no Explorador de Projeto, é possível clicar no botão suspenso **Publicar** na barra de ferramentas e selecionar **Publicar como Aplicativo Web do Azure** lá:</span><span class="sxs-lookup"><span data-stu-id="90311-134">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Publicar como Aplicativo Web do Azure][14]

3. <span data-ttu-id="90311-136">Se você ainda não entrou no Azure por meio do Eclipse, será solicitado que você entre em sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="90311-136">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Caixa de diálogo Entrar no Azure][04]
   
   <span data-ttu-id="90311-138">Se você tiver várias contas do Azure, alguns dos avisos mostrados durante o processo de entrada poderão ser exibidos mais de uma vez, mesmo se forem aparentemente os mesmos.</span><span class="sxs-lookup"><span data-stu-id="90311-138">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="90311-139">Quando isso acontecer, continue seguindo as instruções de entrada.</span><span class="sxs-lookup"><span data-stu-id="90311-139">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="90311-140">Após o logon bem-sucedido em sua conta do Azure, a caixa de diálogo **Gerenciar Assinaturas** exibirá uma lista de assinaturas associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="90311-140">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="90311-141">Se houver várias assinaturas listadas e se você quiser trabalhar com apenas um subconjunto específico delas, poderá, opcionalmente, desmarcar as que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="90311-141">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="90311-142">Depois de selecionar suas assinaturas, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="90311-142">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Caixa de diálogo Gerenciar Assinaturas][05]

5. <span data-ttu-id="90311-144">Quando a caixa de diálogo **Implantar no Contêiner do Aplicativo Web do Azure** for mostrada, ela exibirá todos os contêineres do Aplicativo Web criados anteriormente por você; se você não tiver criado nenhum contêiner, a lista estará vazia.</span><span class="sxs-lookup"><span data-stu-id="90311-144">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][06]

6. <span data-ttu-id="90311-146">Se você nunca tiver criado um contêiner de aplicativos Web do Azure, ou se quiser publicar seu aplicativo em um novo contêiner, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="90311-146">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="90311-147">Caso contrário, selecione um Contêiner de Aplicativo Web existente e pule para a etapa 7 abaixo.</span><span class="sxs-lookup"><span data-stu-id="90311-147">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="90311-148">a.</span><span class="sxs-lookup"><span data-stu-id="90311-148">a.</span></span> <span data-ttu-id="90311-149">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="90311-149">Click **New...**</span></span>
      
      ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][15]

   <span data-ttu-id="90311-151">b.</span><span class="sxs-lookup"><span data-stu-id="90311-151">b.</span></span> <span data-ttu-id="90311-152">A caixa de diálogo **Novo Contêiner do Aplicativo Web** será exibida:</span><span class="sxs-lookup"><span data-stu-id="90311-152">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![Caixa de diálogo Novo contêiner do aplicativo Web][07a]

   <span data-ttu-id="90311-154">c.</span><span class="sxs-lookup"><span data-stu-id="90311-154">c.</span></span> <span data-ttu-id="90311-155">Insira um **Rótulo DNS** para seu Contêiner do Aplicativo Web; isso formará o rótulo DNS folha da URL do host de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="90311-155">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="90311-156">(Observe que o nome deve estar disponível e de acordo com os requisitos de nomenclatura de aplicativo Web do Azure.)</span><span class="sxs-lookup"><span data-stu-id="90311-156">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="90311-157">d.</span><span class="sxs-lookup"><span data-stu-id="90311-157">d.</span></span> <span data-ttu-id="90311-158">No menu suspenso **Contêiner da Web** , selecione o software apropriado ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90311-158">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="90311-159">No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="90311-159">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="90311-160">Uma distribuição recente do software selecionado será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="90311-160">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="90311-161">e.</span><span class="sxs-lookup"><span data-stu-id="90311-161">e.</span></span> <span data-ttu-id="90311-162">No menu suspenso **Assinatura** , selecione a assinatura que deseja usar para essa implantação.</span><span class="sxs-lookup"><span data-stu-id="90311-162">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="90311-163">f.</span><span class="sxs-lookup"><span data-stu-id="90311-163">f.</span></span> <span data-ttu-id="90311-164">No menu suspenso **Grupo de Recursos** , selecione o Grupo de Recursos com o qual deseja associar seu Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="90311-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="90311-165">(Os Grupos de Recursos do Azure lhe permitem agrupar recursos relacionados para que, por exemplo, possam ser excluídos juntos.)</span><span class="sxs-lookup"><span data-stu-id="90311-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="90311-166">Você pode selecionar um Grupo de Recursos existente (se houver) e ignorar a etapa g abaixo ou usar as seguintes etapas para criar um novo Grupo de Recursos:</span><span class="sxs-lookup"><span data-stu-id="90311-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="90311-167">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="90311-167">Click **New...**</span></span>
      * <span data-ttu-id="90311-168">A caixa de diálogo **Novo Grupo de Recursos** será exibida:</span><span class="sxs-lookup"><span data-stu-id="90311-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Caixa de diálogo Novo Grupo de Recursos][08]
      * <span data-ttu-id="90311-170">Na caixa de texto **Nome** , especifique um nome para o novo Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="90311-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="90311-171">No menu suspenso **Região** , selecione a localização do data center do Azure apropriada ao Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="90311-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="90311-172">OPCIONAL: por padrão, uma distribuição recente de Java 8 será implantada pelo Azure automaticamente no contêiner de aplicativo Web como sua JVM.</span><span class="sxs-lookup"><span data-stu-id="90311-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="90311-173">No entanto, você pode especificar uma versão e uma distribuição da JVM diferentes se for necessário para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="90311-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="90311-174">Para especificar o JDK do seu aplicativo Web, clique na guia **JDK** e selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="90311-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
         * <span data-ttu-id="90311-175">**Implantar o JDK oferecido pelo Serviço de Aplicativos Web do Azure padrão**: essa opção implantará uma distribuição recente do Java 8.</span><span class="sxs-lookup"><span data-stu-id="90311-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
         * <span data-ttu-id="90311-176">**Implantar um JDK de terceiro disponível no Azure**: essa opção permite que você escolha na lista de JDKs que são fornecidos pelo Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="90311-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
         * <span data-ttu-id="90311-177">**Meu próprio JDK deste local de download**: essa opção permite que você especifique sua própria distribuição de JDK, que deve ser empacotada como um arquivo ZIP e carregada em um local de download disponível publicamente ou em uma conta de armazenamento do Azure à qual você tenha acesso.</span><span class="sxs-lookup"><span data-stu-id="90311-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
         ![Caixa de diálogo Novo contêiner do aplicativo Web][07b]

   <span data-ttu-id="90311-179">g.</span><span class="sxs-lookup"><span data-stu-id="90311-179">g.</span></span> <span data-ttu-id="90311-180">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="90311-180">Click **OK**.</span></span>

   <span data-ttu-id="90311-181">h.</span><span class="sxs-lookup"><span data-stu-id="90311-181">h.</span></span> <span data-ttu-id="90311-182">O menu suspenso **Plano do Serviço de Aplicativo** lista os planos do serviço de aplicativo associados ao Grupo de Recursos selecionado.</span><span class="sxs-lookup"><span data-stu-id="90311-182">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="90311-183">(Os Planos do Serviço de Aplicativo especificam informações como o local de seu Aplicativo Web, o tipo de preço e o tamanho da instância de computação.</span><span class="sxs-lookup"><span data-stu-id="90311-183">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="90311-184">Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)</span><span class="sxs-lookup"><span data-stu-id="90311-184">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="90311-185">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="90311-185">Click **New...**</span></span>
      * <span data-ttu-id="90311-186">A caixa de diálogo **Novo Plano do Serviço de Aplicativo** será exibida:</span><span class="sxs-lookup"><span data-stu-id="90311-186">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Caixa de diálogo Novo Plano do Serviço de Aplicativo][09]
      * <span data-ttu-id="90311-188">Na caixa de texto **Nome** , especifique um nome para o novo Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="90311-188">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="90311-189">No menu suspenso **Localização** , selecione a localização do data center do Azure apropriada ao plano.</span><span class="sxs-lookup"><span data-stu-id="90311-189">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="90311-190">No menu suspenso **Tipo de Preço** , selecione o preço apropriado ao plano.</span><span class="sxs-lookup"><span data-stu-id="90311-190">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="90311-191">Para fins de teste, é possível escolher **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="90311-191">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="90311-192">No menu suspenso **Tamanho da Instância** , selecione o tamanho de instância apropriado ao plano.</span><span class="sxs-lookup"><span data-stu-id="90311-192">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="90311-193">Para fins de teste, é possível escolher **Pequeno**.</span><span class="sxs-lookup"><span data-stu-id="90311-193">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="90311-194">i.</span><span class="sxs-lookup"><span data-stu-id="90311-194">i.</span></span> <span data-ttu-id="90311-195">Depois de concluir todas as etapas acima, a caixa de diálogo New Web App Container (Novo Contêiner de Aplicativos Web) deve ser semelhante à ilustração a seguir:</span><span class="sxs-lookup"><span data-stu-id="90311-195">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Caixa de diálogo Novo contêiner do aplicativo Web][10]

   <span data-ttu-id="90311-197">j.</span><span class="sxs-lookup"><span data-stu-id="90311-197">j.</span></span> <span data-ttu-id="90311-198">Clique em **OK** para concluir a criação do novo contêiner do Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="90311-198">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="90311-199">Aguarde alguns segundos para a lista de contêineres de Aplicativo Web ser atualizada. O contêiner do aplicativo Web recém-criado agora deve ser selecionado na lista.</span><span class="sxs-lookup"><span data-stu-id="90311-199">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="90311-200">Agora você está pronto para concluir a implantação inicial de seu Aplicativo Web no Azure:</span><span class="sxs-lookup"><span data-stu-id="90311-200">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][11]
   
   <span data-ttu-id="90311-202">Clique em **OK** para implantar o aplicativo Java no contêiner do Aplicativo Web selecionado.</span><span class="sxs-lookup"><span data-stu-id="90311-202">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="90311-203">Por padrão, o aplicativo será implantado como um subdiretório do servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="90311-203">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="90311-204">Se desejar implantá-lo como o aplicativo raiz, marque a caixa de seleção **Implantar na raiz** antes de clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="90311-204">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="90311-205">Em seguida, você deverá ver o modo de exibição do **Log de Atividades do Azure** , que indicará o status da implantação de seu Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="90311-205">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Log de Atividades do Azure][12]
   
   <span data-ttu-id="90311-207">O processo de implantação de seu aplicativo Web no Azure deve demorar apenas alguns segundos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="90311-207">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="90311-208">Quando seu aplicativo estiver pronto, você verá um link chamado **Publicada** in the **Status** .</span><span class="sxs-lookup"><span data-stu-id="90311-208">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="90311-209">Ao clicar no link, você será levado à home page do Aplicativo Web implantado.</span><span class="sxs-lookup"><span data-stu-id="90311-209">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="90311-210">Atualização de seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="90311-210">Updating your web app</span></span>

<span data-ttu-id="90311-211">A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:</span><span class="sxs-lookup"><span data-stu-id="90311-211">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="90311-212">Você pode atualizar a implantação de um aplicativo Web Java existente.</span><span class="sxs-lookup"><span data-stu-id="90311-212">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="90311-213">Você pode publicar um aplicativo Java adicional no mesmo contêiner de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="90311-213">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="90311-214">Em ambos os casos, o processo é idêntico e demora apenas alguns segundos:</span><span class="sxs-lookup"><span data-stu-id="90311-214">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="90311-215">No explorador de projetos do Eclipse, clique com o botão direito do mouse no aplicativo Java que você deseja atualizar ou adicionar a um contêiner de aplicativos Web existente.</span><span class="sxs-lookup"><span data-stu-id="90311-215">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="90311-216">Quando o menu de contexto for exibido, selecione **Azure** e, em seguida, **Publicar como Aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="90311-216">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="90311-217">Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes.</span><span class="sxs-lookup"><span data-stu-id="90311-217">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="90311-218">Selecione aquele no qual deseja publicar ou publicar novamente o aplicativo Java e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="90311-218">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="90311-219">Após alguns segundos, o modo de exibição do **Log de Atividades do Azure** mostrará a implantação atualizada como **Publicada** e será possível verificar o aplicativo atualizado em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="90311-219">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="90311-220">Iniciar, parar ou reiniciar o aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="90311-220">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="90311-221">Para iniciar ou parar um contêiner do Aplicativo Web do Azure existente, (incluindo todos os aplicativos Java implantados nele), é possível usar o modo de exibição do **Azure Explorer** .</span><span class="sxs-lookup"><span data-stu-id="90311-221">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="90311-222">Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Janela** no Eclipse, clicando em **Mostrar Modo de Exibição**, em **Outros...**, em **Azure** e em **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="90311-222">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="90311-223">Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="90311-223">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="90311-224">Quando o modo de exibição do **Azure Explorer** for exibido, use estas etapas para iniciar ou parar o Aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="90311-224">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="90311-225">Expanda o nó **Azure** .</span><span class="sxs-lookup"><span data-stu-id="90311-225">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="90311-226">Expanda o nó **Aplicativos Web** .</span><span class="sxs-lookup"><span data-stu-id="90311-226">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="90311-227">Clique com botão direito do mouse no Aplicativo Web desejado.</span><span class="sxs-lookup"><span data-stu-id="90311-227">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="90311-228">Quando o menu de contexto for exibido, clique em **Iniciar**, **Parar** ou **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="90311-228">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="90311-229">Observe que as opções de menu são sensíveis ao contexto, para que você só possa parar um aplicativo Web que esteja em execução ou iniciar um aplicativo Web que não esteja em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="90311-229">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Interromper um aplicativo Web existente][13]

## <a name="next-steps"></a><span data-ttu-id="90311-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90311-231">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="90311-232">Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="90311-232">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de Ferramentas do Azure para Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Visão geral de Aplicativos Web]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-eclipse-create-hello-world-web-app.md
[eclipse-sign-in-instructions]: azure-toolkit-for-eclipse-sign-in-instructions.md


<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/15-New-Azure-Web-Container.png
