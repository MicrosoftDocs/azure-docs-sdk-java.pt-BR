---
title: Criar um aplicativo Web Olá, Mundo para o Serviço de Aplicativo do Azure usando o IntelliJ
description: Este tutorial mostra como usar o Kit de Ferramentas do Azure para IntelliJ para criar um aplicativo Web Hello World para o Azure.
services: app-service
keywords: java, intellij, aplicativo Web, serviço de aplicativo do azure, olá, mundo, início rápido
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ae0749ce1ddab971f1a83e2e5e58492fd8ccb287
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626112"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a><span data-ttu-id="46ae7-104">Criar um aplicativo Web Olá, Mundo para o Serviço de Aplicativo do Azure usando o IntelliJ</span><span class="sxs-lookup"><span data-stu-id="46ae7-104">Create a Hello World web app for Azure App Service using IntelliJ</span></span>

<span data-ttu-id="46ae7-105">Usando o plug-in [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) de software livre, criar e implantar um aplicativo Olá, Mundo básico para o Serviço de Aplicativo do Azure como um aplicativo Web pode ser feito em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="46ae7-105">Using open sourced [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="46ae7-106">Se você preferir usar o Eclipse, confira nosso [tutorial semelhante para o Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="46ae7-106">If you prefer using Eclipse, check out our [similar tutorial for Eclipse][eclipse-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="46ae7-107">Não se esqueça de limpar os recursos depois de concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="46ae7-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="46ae7-108">Nesse caso, executar este guia não excederá sua cota da conta gratuita.</span><span class="sxs-lookup"><span data-stu-id="46ae7-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="46ae7-109">Instalação e credenciais</span><span class="sxs-lookup"><span data-stu-id="46ae7-109">Installation and Sign-in</span></span>

1. <span data-ttu-id="46ae7-110">Na caixa de diálogo Configurações/Preferências do IntelliJ IDEA (Ctrl+Alt+S), selecione **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-110">In IntelliJ IDEA's Settings/Preferences dialog (Ctrl+Alt+S), select **Plugins**.</span></span> <span data-ttu-id="46ae7-111">Em seguida, localize o **Azure Toolkit for IntelliJ** no **Marketplace** e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-111">Then, find the **Azure Toolkit for IntelliJ** in the **Marketplace** and click **Install**.</span></span> <span data-ttu-id="46ae7-112">Depois de instalado, clique em **Reiniciar** para ativar o plug-in.</span><span class="sxs-lookup"><span data-stu-id="46ae7-112">After installed, click **Restart** to activate the plugin.</span></span> 

   ![Plug-in do Azure Toolkit for IntelliJ no Marketplace][marketplace]

2. <span data-ttu-id="46ae7-114">Para entrar sua conta do Azure, abra a barra lateral **Azure Explorer** e, em seguida, clique no ícone **Entrar no Azure** na barra na parte superior (ou no menu IDEA **Ferramentas/Azure/Entrada no Azure**).</span><span class="sxs-lookup"><span data-stu-id="46ae7-114">To sign in to your Azure account, open sidebar **Azure Explorer**, and then click the **Azure Sign In** icon in the bar on top (or from IDEA menu **Tools/Azure/Azure Sign in**).</span></span>

   ![O comando de Entrada do IntelliJ Azure][I01]

3. <span data-ttu-id="46ae7-116">Na janela **Entrar no Azure**, selecione **Logon do Dispositivo** e, em seguida, clique em **Entrar** ([outras opções de entrada](azure-toolkit-for-intellij-sign-in-instructions.md)).</span><span class="sxs-lookup"><span data-stu-id="46ae7-116">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign in options](azure-toolkit-for-intellij-sign-in-instructions.md)).</span></span>

   ![A janela Entrar no Azure com o logon no dispositivo selecionado][I02]

4. <span data-ttu-id="46ae7-118">Clique em **Copiar e Abrir** na caixa de diálogo **Logon no Dispositivo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-118">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![A janela da caixa de diálogo Logon no Azure][I03]

5. <span data-ttu-id="46ae7-120">No navegador, cole o código de dispositivo (que foi copiado quando você clicou em **Copiar e Abrir** na última etapa) e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-120">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![O navegador de logon do dispositivo][I04]

6. <span data-ttu-id="46ae7-122">Na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-122">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![A caixa de diálogo Selecionar Assinaturas][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="46ae7-124">Como criar um projeto de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="46ae7-124">Creating web app project</span></span>

1. <span data-ttu-id="46ae7-125">No IntelliJ, clique menu **Arquivo**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-125">In IntelliJ, click the **File** menu, then click **New**, and then click **Project**.</span></span>

   ![Criar um novo projeto][file-new-project]

2. <span data-ttu-id="46ae7-127">Na caixa de diálogo **Novo Projeto**, selecione **Maven**, em seguida, **maven-archetype-webapp** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-127">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>

   ![Escolha o Webapp do arquétipo Maven][maven-archetype-webapp]

3. <span data-ttu-id="46ae7-129">Especifique o **GroupId** e **ArtifactId** para seu aplicativo Web e depois clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-129">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>

   ![Especifique GroupId e ArtifactId][groupid-and-artifactid]

4. <span data-ttu-id="46ae7-131">Personalize as configurações de Maven ou aceite os padrões e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-131">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>

   ![Especifique as configurações de Maven][maven-options]

5. <span data-ttu-id="46ae7-133">Especifique um nome de projeto e local e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-133">Specify your project name and location, and then click **Finish**.</span></span>

   ![Especifique o nome do projeto][project-name]

6. <span data-ttu-id="46ae7-135">Na exibição do Explorador de Projeto, abra e edite o arquivo **src/main/webapp/index.jsp** da seguinte maneira e **salve as alterações**:</span><span class="sxs-lookup"><span data-stu-id="46ae7-135">Under Project Explorer view, open and edit the file **src/main/webapp/index.jsp** as following and **save the changes**:</span></span>

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Edite a página de índice][edit-index-page]

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="46ae7-137">Como implantar o aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="46ae7-137">Deploying web app to Azure</span></span>

1. <span data-ttu-id="46ae7-138">Na exibição do Explorador de Projeto, clique com o botão direito do mouse em seu projeto, expanda **Azure** e, em seguida, clique em **Implantar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-138">Under Project Explorer view, right-click your project, expand **Azure**, then click **Deploy to Azure**.</span></span>

   ![Menu Implantar no Azure][deploy-to-azure-menu]

1. <span data-ttu-id="46ae7-140">Na caixa de diálogo Implantar no Azure, você pode implantar diretamente o aplicativo em um webapp Tomcat existente se você já tiver um; caso contrário, deverá criar um primeiro.</span><span class="sxs-lookup"><span data-stu-id="46ae7-140">In the Deploy to Azure dialog box, you can directly deploy the application to an existing Tomcat webapp if you already have one, otherwise you should create a new one first.</span></span>
   1. <span data-ttu-id="46ae7-141">Clique no link **Nenhum webapp disponível, clique para criar um** para criar um aplicativo Web. Você poderia escolher **Criar WebApp** na lista suspensa do WebApp se houvesse webapps existentes em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="46ae7-141">Click the link **No Available webapp, click to create a new one** to crete a new web app, you could choose **Create New WebApp** from WebApp dropdown if there are existing webapps in your subscription.</span></span>

      ![Caixa de diálogo Implantar para o Azure][deploy-to-azure-dialog]

   1. <span data-ttu-id="46ae7-143">Na caixa de diálogo pop-up, escolha **TOMCAT 8.5-jre8** como o contêiner da Web, especifique outras informações necessárias e clique em **OK** para criar o webapp.</span><span class="sxs-lookup"><span data-stu-id="46ae7-143">In the pop-up dialog box, chose **TOMCAT 8.5-jre8** as Web Container and specify other required information, then click **OK** to create the webapp.</span></span>

      ![Criar novo aplicativo Web][create-new-web-app-dialog]

   1. <span data-ttu-id="46ae7-145">Escolha o aplicativo Web no menu suspenso WebApp e, em seguida, clique em **Executar**. (Você poderá começar aqui se desejar implantar em um webapp existente)</span><span class="sxs-lookup"><span data-stu-id="46ae7-145">Choose the web app from WebApp drop down, and then click **Run**.(You could start from here if you want deploy to an existing webapp)</span></span>

      ![Implantar no webapp existente][deploy-to-existing-webapp]

1. <span data-ttu-id="46ae7-147">O kit de ferramentas exibirá uma mensagem de status quando tiver implantado com êxito seu aplicativo Web, junto com a URL do aplicativo Web implantado, se bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="46ae7-147">The toolkit will display a status message when it has successfully deployed your web app, along with the URL of your deployed web app if succeed.</span></span>

   ![Implantação bem-sucedida][successfully-deployed]

1. <span data-ttu-id="46ae7-149">Você pode navegar até seu aplicativo Web usando o link fornecido na mensagem de status.</span><span class="sxs-lookup"><span data-stu-id="46ae7-149">You can browse to your web app using the link provided in the status message.</span></span>

   ![Procurar seu aplicativo Web][browse-web-app]

## <a name="managing-deploy-configurations"></a><span data-ttu-id="46ae7-151">Como gerenciar configurações de implantação</span><span class="sxs-lookup"><span data-stu-id="46ae7-151">Managing deploy configurations</span></span>

1. <span data-ttu-id="46ae7-152">Depois de publicar seu aplicativo Web, as configurações serão salvas como padrão e você poderá executar a implantação clicando no ícone de seta verde na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="46ae7-152">After you have published your web app, your settings will be saved as the default, and you can run the deployment by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="46ae7-153">Você pode modificar as configurações clicando no menu suspenso para seu aplicativo Web e clique em **Editar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-153">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menu Editar configuração][edit-configuration-menu]

1. <span data-ttu-id="46ae7-155">Quando a caixa de diálogo **Configurações de execução/depuração** for exibida, você poderá modificar as configurações padrão e, em seguida, clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="46ae7-155">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Caixa de diálogo Editar configuração][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a><span data-ttu-id="46ae7-157">Limpando recursos</span><span class="sxs-lookup"><span data-stu-id="46ae7-157">Cleaning up resources</span></span>

1. <span data-ttu-id="46ae7-158">Como excluir Aplicativos Web no Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="46ae7-158">Deleting Web Apps in Azure Explorer</span></span>

     ![Limpar recursos][clean-resources]

## <a name="next-steps"></a><span data-ttu-id="46ae7-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46ae7-160">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="46ae7-161">Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="46ae7-161">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Visão geral de Aplicativos Web]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->
[marketplace]:./media/azure-toolkit-for-intellij-create-hello-world-web-app/marketplace.png
[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[deploy-to-azure-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[deploy-to-azure-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[deploy-to-existing-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/deploy-to-existing-webapp.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
[clean-resources]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/clean-resource.png
[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-intellij-sign-in-instructions/I05.png
