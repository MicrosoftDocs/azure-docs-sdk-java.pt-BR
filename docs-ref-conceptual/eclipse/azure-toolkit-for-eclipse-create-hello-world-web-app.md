---
title: "Criar um aplicativo web básico do Azure usando o Eclipse"
description: Este tutorial mostra como usar o Kit de Ferramentas do Azure para Eclipse para criar um aplicativo Web Hello World para o Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: dcab31ad99fb79a91374d95c2b8b0d9d10346f5f
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="3ebcc-103">Criar um aplicativo web básico do Azure usando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="3ebcc-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="3ebcc-104">Este tutorial mostra como criar e implantar um aplicativo Hello World básico para o Azure como um aplicativo Web usando o [Kit de Ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3ebcc-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="3ebcc-105">Um exemplo básico de JSP é exibido para manter a simplicidade, mas etapas semelhantes podem ser apropriadas para um servlet Java quando o assunto é a implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="3ebcc-106">Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Visualização do aplicativo Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="3ebcc-108">Para criar um aplicativo Hello World</span><span class="sxs-lookup"><span data-stu-id="3ebcc-108">To create a Hello World application</span></span>
<span data-ttu-id="3ebcc-109">Primeiro, vamos começar com a criação de um projeto Java.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-109">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="3ebcc-110">Inicie o Eclipse, no menu clique em **Arquivo**, clique em **Novo** e depois em **Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-110">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="3ebcc-111">(Se você não vir o **Projeto Web Dinâmico** listado como um projeto disponível depois de clicar em **Arquivo** e em **Novo**, faça o seguinte: clique em **Arquivo**, clique em **Novo**, clique em **Projeto...**, expanda **Web**, clique em **Projeto Web Dinâmico** e clique em **Avançar**.)</span><span class="sxs-lookup"><span data-stu-id="3ebcc-111">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="3ebcc-112">Para o objetivo deste tutorial, nomeie o projeto **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-112">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="3ebcc-113">Sua tela será semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-113">Your screen will appear similar to the following:</span></span>
   
   ![Criando um novo projeto Web dinâmico][02]

3. <span data-ttu-id="3ebcc-115">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-115">Click **Finish**.</span></span>

4. <span data-ttu-id="3ebcc-116">No modo de exibição do Gerenciador de Projeto do Eclipse, expanda **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-116">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="3ebcc-117">Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-117">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="3ebcc-118">Na caixa de diálogo **Novo Arquivo JSP**, nomeie o arquivo **index.jsp**, mantenha a pasta pai como **MyWebApp/WebContent** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-118">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="3ebcc-119">Na caixa de diálogo **Selecionar Modelo JSP**, para a finalidade deste tutorial, escolha **Novo Arquivo JSP (html)** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-119">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="3ebcc-120">Quando o arquivo index.jsp for aberto no Eclipse, adicione o texto para exibir dinamicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="3ebcc-120">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="3ebcc-121">dentro do elemento existente `<body>`.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-121">within the existing `<body>` element.</span></span> <span data-ttu-id="3ebcc-122">Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-122">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="3ebcc-123">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-123">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="3ebcc-124">Para implantar seu aplicativo em um contêiner de aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="3ebcc-124">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="3ebcc-125">Há várias maneiras pelas quais você pode implantar um aplicativo Web Java no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-125">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="3ebcc-126">Este tutorial descreve uma das mais simples: o aplicativo será implantado em um contêiner de aplicativos Web do Azure, e não há a necessidade de qualquer tipo de projeto especial nem de ferramentas adicionais.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-126">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="3ebcc-127">O JDK e o software do contêiner da Web serão fornecidos a você pelo Azure, portanto, não é necessário carregar seu próprio; tudo o que você precisa é de seu aplicativo Web Java.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-127">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="3ebcc-128">Como resultado, o processo de publicação de seu aplicativo demorará segundos, e não minutos.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-128">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="3ebcc-129">No Gerenciador de Projetos do Eclipse, clique com o botão direito do mouse em **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-129">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="3ebcc-130">No menu de contexto, selecione **Azure** e clique em **Publicar como Aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="3ebcc-130">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Publicar como Aplicativo Web do Azure][03]
   
   <span data-ttu-id="3ebcc-132">Como alternativa, enquanto o projeto do aplicativo Web é selecionado no Explorador de Projeto, é possível clicar no botão suspenso **Publicar** na barra de ferramentas e selecionar **Publicar como Aplicativo Web do Azure** lá:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-132">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Publicar como Aplicativo Web do Azure][14]

3. <span data-ttu-id="3ebcc-134">Se você ainda não entrou no Azure por meio do Eclipse, será solicitado que você entre em sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-134">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Caixa de diálogo Entrar no Azure][04]
   
   <span data-ttu-id="3ebcc-136">Se você tiver várias contas do Azure, alguns dos avisos mostrados durante o processo de entrada poderão ser exibidos mais de uma vez, mesmo se forem aparentemente os mesmos.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-136">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="3ebcc-137">Quando isso acontecer, continue seguindo as instruções de entrada.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-137">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="3ebcc-138">Após o logon bem-sucedido em sua conta do Azure, a caixa de diálogo **Gerenciar Assinaturas** exibirá uma lista de assinaturas associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-138">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="3ebcc-139">Se houver várias assinaturas listadas e se você quiser trabalhar com apenas um subconjunto específico delas, poderá, opcionalmente, desmarcar as que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-139">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="3ebcc-140">Depois de selecionar suas assinaturas, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-140">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Caixa de diálogo Gerenciar Assinaturas][05]

5. <span data-ttu-id="3ebcc-142">Quando a caixa de diálogo **Implantar no Contêiner do Aplicativo Web do Azure** for mostrada, ela exibirá todos os contêineres do Aplicativo Web criados anteriormente por você; se você não tiver criado nenhum contêiner, a lista estará vazia.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-142">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][06]

6. <span data-ttu-id="3ebcc-144">Se você nunca tiver criado um contêiner de aplicativos Web do Azure, ou se quiser publicar seu aplicativo em um novo contêiner, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-144">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="3ebcc-145">Caso contrário, selecione um Contêiner de Aplicativo Web existente e pule para a etapa 7 abaixo.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-145">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="3ebcc-146">a.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-146">a.</span></span> <span data-ttu-id="3ebcc-147">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="3ebcc-147">Click **New...**</span></span>
      
      ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][15]

   <span data-ttu-id="3ebcc-149">b.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-149">b.</span></span> <span data-ttu-id="3ebcc-150">A caixa de diálogo **Novo Contêiner do Aplicativo Web** será exibida:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-150">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![Caixa de diálogo Novo contêiner do aplicativo Web][07a]

   <span data-ttu-id="3ebcc-152">c.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-152">c.</span></span> <span data-ttu-id="3ebcc-153">Insira um **Rótulo DNS** para seu Contêiner do Aplicativo Web; isso formará o rótulo DNS folha da URL do host de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-153">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="3ebcc-154">(Observe que o nome deve estar disponível e de acordo com os requisitos de nomenclatura de aplicativo Web do Azure.)</span><span class="sxs-lookup"><span data-stu-id="3ebcc-154">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="3ebcc-155">d.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-155">d.</span></span> <span data-ttu-id="3ebcc-156">No menu suspenso **Contêiner da Web** , selecione o software apropriado ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-156">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="3ebcc-157">No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-157">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="3ebcc-158">Uma distribuição recente do software selecionado será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-158">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="3ebcc-159">e.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-159">e.</span></span> <span data-ttu-id="3ebcc-160">No menu suspenso **Assinatura** , selecione a assinatura que deseja usar para essa implantação.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-160">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="3ebcc-161">f.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-161">f.</span></span> <span data-ttu-id="3ebcc-162">No menu suspenso **Grupo de Recursos** , selecione o Grupo de Recursos com o qual deseja associar seu Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-162">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="3ebcc-163">(Os Grupos de Recursos do Azure lhe permitem agrupar recursos relacionados para que, por exemplo, possam ser excluídos juntos.)</span><span class="sxs-lookup"><span data-stu-id="3ebcc-163">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="3ebcc-164">Você pode selecionar um Grupo de Recursos existente (se houver) e ignorar a etapa g abaixo ou usar as seguintes etapas para criar um novo Grupo de Recursos:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-164">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="3ebcc-165">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="3ebcc-165">Click **New...**</span></span>
      * <span data-ttu-id="3ebcc-166">A caixa de diálogo **Novo Grupo de Recursos** será exibida:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-166">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Caixa de diálogo Novo Grupo de Recursos][08]
      * <span data-ttu-id="3ebcc-168">Na caixa de texto **Nome** , especifique um nome para o novo Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-168">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="3ebcc-169">No menu suspenso **Região** , selecione a localização do data center do Azure apropriada ao Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-169">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="3ebcc-170">OPCIONAL: por padrão, uma distribuição recente de Java 8 será implantada pelo Azure automaticamente no contêiner de aplicativo Web como sua JVM.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-170">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="3ebcc-171">No entanto, você pode especificar uma versão e uma distribuição da JVM diferentes se for necessário para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-171">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="3ebcc-172">Para especificar o JDK do seu aplicativo Web, clique na guia **JDK** e selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-172">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
         * <span data-ttu-id="3ebcc-173">**Implantar o JDK oferecido pelo Serviço de Aplicativos Web do Azure padrão**: essa opção implantará uma distribuição recente do Java 8.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-173">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
         * <span data-ttu-id="3ebcc-174">**Implantar um JDK de terceiro disponível no Azure**: essa opção permite que você escolha na lista de JDKs que são fornecidos pelo Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-174">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
         * <span data-ttu-id="3ebcc-175">**Meu próprio JDK deste local de download**: essa opção permite que você especifique sua própria distribuição de JDK, que deve ser empacotada como um arquivo ZIP e carregada em um local de download disponível publicamente ou em uma conta de armazenamento do Azure à qual você tenha acesso.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-175">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
         ![Caixa de diálogo Novo contêiner do aplicativo Web][07b]

   <span data-ttu-id="3ebcc-177">g.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-177">g.</span></span> <span data-ttu-id="3ebcc-178">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-178">Click **OK**.</span></span>

   <span data-ttu-id="3ebcc-179">h.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-179">h.</span></span> <span data-ttu-id="3ebcc-180">O menu suspenso **Plano do Serviço de Aplicativo** lista os planos do serviço de aplicativo associados ao Grupo de Recursos selecionado.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="3ebcc-181">(Os Planos do Serviço de Aplicativo especificam informações como o local de seu Aplicativo Web, o tipo de preço e o tamanho da instância de computação.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="3ebcc-182">Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)</span><span class="sxs-lookup"><span data-stu-id="3ebcc-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="3ebcc-183">Clique em **Novo...**</span><span class="sxs-lookup"><span data-stu-id="3ebcc-183">Click **New...**</span></span>
      * <span data-ttu-id="3ebcc-184">A caixa de diálogo **Novo Plano do Serviço de Aplicativo** será exibida:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-184">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Caixa de diálogo Novo Plano do Serviço de Aplicativo][09]
      * <span data-ttu-id="3ebcc-186">Na caixa de texto **Nome** , especifique um nome para o novo Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-186">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="3ebcc-187">No menu suspenso **Localização** , selecione a localização do data center do Azure apropriada ao plano.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-187">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="3ebcc-188">No menu suspenso **Tipo de Preço** , selecione o preço apropriado ao plano.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-188">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="3ebcc-189">Para fins de teste, é possível escolher **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-189">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="3ebcc-190">No menu suspenso **Tamanho da Instância** , selecione o tamanho de instância apropriado ao plano.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-190">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="3ebcc-191">Para fins de teste, é possível escolher **Pequeno**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-191">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="3ebcc-192">i.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-192">i.</span></span> <span data-ttu-id="3ebcc-193">Depois de concluir todas as etapas acima, a caixa de diálogo New Web App Container (Novo Contêiner de Aplicativos Web) deve ser semelhante à ilustração a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Caixa de diálogo Novo contêiner do aplicativo Web][10]

   <span data-ttu-id="3ebcc-195">j.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-195">j.</span></span> <span data-ttu-id="3ebcc-196">Clique em **OK** para concluir a criação do novo contêiner do Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-196">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="3ebcc-197">Aguarde alguns segundos para a lista de contêineres de Aplicativo Web ser atualizada. O contêiner do aplicativo Web recém-criado agora deve ser selecionado na lista.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-197">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="3ebcc-198">Agora você está pronto para concluir a implantação inicial de seu Aplicativo Web no Azure:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-198">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][11]
   
   <span data-ttu-id="3ebcc-200">Clique em **OK** para implantar o aplicativo Java no contêiner do Aplicativo Web selecionado.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-200">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="3ebcc-201">Por padrão, o aplicativo será implantado como um subdiretório do servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-201">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="3ebcc-202">Se desejar implantá-lo como o aplicativo raiz, marque a caixa de seleção **Implantar na raiz** antes de clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-202">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="3ebcc-203">Em seguida, você deverá ver o modo de exibição do **Log de Atividades do Azure** , que indicará o status da implantação de seu Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-203">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Log de Atividades do Azure][12]
   
   <span data-ttu-id="3ebcc-205">O processo de implantação de seu aplicativo Web no Azure deve demorar apenas alguns segundos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-205">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="3ebcc-206">Quando seu aplicativo estiver pronto, você verá um link chamado **Publicada** in the **Status** .</span><span class="sxs-lookup"><span data-stu-id="3ebcc-206">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="3ebcc-207">Ao clicar no link, você será levado à home page do Aplicativo Web implantado.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-207">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="3ebcc-208">Atualização de seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="3ebcc-208">Updating your web app</span></span>
<span data-ttu-id="3ebcc-209">A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-209">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="3ebcc-210">Você pode atualizar a implantação de um aplicativo Web Java existente.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-210">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="3ebcc-211">Você pode publicar um aplicativo Java adicional no mesmo contêiner de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-211">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="3ebcc-212">Em ambos os casos, o processo é idêntico e demora apenas alguns segundos:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-212">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="3ebcc-213">No explorador de projetos do Eclipse, clique com o botão direito do mouse no aplicativo Java que você deseja atualizar ou adicionar a um contêiner de aplicativos Web existente.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-213">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="3ebcc-214">Quando o menu de contexto for exibido, selecione **Azure** e, em seguida, **Publicar como Aplicativo Web do Azure...**</span><span class="sxs-lookup"><span data-stu-id="3ebcc-214">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="3ebcc-215">Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-215">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="3ebcc-216">Selecione aquele no qual deseja publicar ou publicar novamente o aplicativo Java e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-216">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="3ebcc-217">Após alguns segundos, o modo de exibição do **Log de Atividades do Azure** mostrará a implantação atualizada como **Publicada** e será possível verificar o aplicativo atualizado em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-217">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="3ebcc-218">Iniciar, parar ou reiniciar o aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="3ebcc-218">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="3ebcc-219">Para iniciar ou parar um contêiner do Aplicativo Web do Azure existente, (incluindo todos os aplicativos Java implantados nele), é possível usar o modo de exibição do **Azure Explorer** .</span><span class="sxs-lookup"><span data-stu-id="3ebcc-219">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="3ebcc-220">Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Janela** no Eclipse, clicando em **Mostrar Modo de Exibição**, em **Outros...**, em **Azure** e em **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-220">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="3ebcc-221">Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-221">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="3ebcc-222">Quando o modo de exibição do **Azure Explorer** for exibido, use estas etapas para iniciar ou parar o Aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="3ebcc-222">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="3ebcc-223">Expanda o nó **Azure** .</span><span class="sxs-lookup"><span data-stu-id="3ebcc-223">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="3ebcc-224">Expanda o nó **Aplicativos Web** .</span><span class="sxs-lookup"><span data-stu-id="3ebcc-224">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="3ebcc-225">Clique com botão direito do mouse no Aplicativo Web desejado.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-225">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="3ebcc-226">Quando o menu de contexto for exibido, clique em **Iniciar**, **Parar** ou **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-226">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="3ebcc-227">Observe que as opções de menu são sensíveis ao contexto, para que você só possa parar um aplicativo Web que esteja em execução ou iniciar um aplicativo Web que não esteja em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="3ebcc-227">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Interromper um aplicativo Web existente][13]

## <a name="next-steps"></a><span data-ttu-id="3ebcc-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ebcc-229">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="3ebcc-230">Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="3ebcc-230">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de Ferramentas do Azure para Eclipse]: azure-toolkit-for-eclipse.md
[Visão geral de Aplicativos Web]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
