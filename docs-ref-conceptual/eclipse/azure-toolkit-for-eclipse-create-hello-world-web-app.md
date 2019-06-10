---
title: Criar um aplicativo Web Olá, Mundo para o Serviço de Aplicativo do Azure usando o Eclipse
description: Este tutorial mostra como usar o Kit de Ferramentas do Azure para Eclipse para criar um aplicativo Web Hello World para o Azure.
services: app-service
keywords: java, eclipse, aplicativo Web, serviço de aplicativo do azure, olá, mundo, início rápido
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 7e88298afaf0b4601d85d6063b7096c79e677421
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625846"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-eclipse"></a><span data-ttu-id="948c7-104">Criar um aplicativo Web Olá, Mundo para o Serviço de Aplicativo do Azure usando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="948c7-104">Create a Hello World web app for Azure App Service using Eclipse</span></span>

<span data-ttu-id="948c7-105">Usando o plug-in [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) de software livre, criar e implantar um aplicativo Olá, Mundo básico para o Serviço de Aplicativo do Azure como um aplicativo Web pode ser feito em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="948c7-105">Using open sourced [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="948c7-106">Se você preferir usar o IntelliJ IDEA, confira nosso [tutorial semelhante para IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="948c7-106">If you prefer using IntelliJ IDEA, check out our [similar tutorial for IntelliJ][intellij-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="948c7-107">Não se esqueça de limpar os recursos depois de concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="948c7-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="948c7-108">Nesse caso, executar este guia não excederá sua cota da conta gratuita.</span><span class="sxs-lookup"><span data-stu-id="948c7-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="948c7-109">Instalação e credenciais</span><span class="sxs-lookup"><span data-stu-id="948c7-109">Installation and sign-in</span></span>

1. <span data-ttu-id="948c7-110">Arraste o botão a seguir para seu workspace do Eclipse em execução para instalar o plug-in do Azure Toolkit for Eclipse ([outras opções de instalação](azure-toolkit-for-eclipse-installation.md)).</span><span class="sxs-lookup"><span data-stu-id="948c7-110">Drag the following button to your running Eclipse workspace to install the Azure Toolkit for Eclipse plugin ([other installation options](azure-toolkit-for-eclipse-installation.md)).</span></span>

    <span data-ttu-id="948c7-111">[![Arraste para seu workspace do Eclipse* em execução. *Requer o Cliente do Eclipse Marketplace](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Arraste para seu workspace do Eclipse* em execução. *Requer o Cliente do Eclipse Marketplace")</span><span class="sxs-lookup"><span data-stu-id="948c7-111">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

1. <span data-ttu-id="948c7-112">Para entrar em sua conta do Azure, clique em **Ferramentas**, então em **Azure** e em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="948c7-112">To sign in to your Azure account, click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="948c7-113">![Menu do Eclipse para Entrada no Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="948c7-113">![Eclipse Menu for Azure Sign In][I01]</span></span>

1. <span data-ttu-id="948c7-114">Na janela **Entrar no Azure**, selecione **Logon do Dispositivo** e, em seguida, clique em **Entrar** ([outras opções de entrada](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span><span class="sxs-lookup"><span data-stu-id="948c7-114">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign-in options](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span></span>

   ![A janela Entrar no Azure com o logon no dispositivo selecionado][I02]

1. <span data-ttu-id="948c7-116">Clique em **Copiar e Abrir** na caixa de diálogo **Logon no Dispositivo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="948c7-116">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![A janela da caixa de diálogo Logon no Azure][I03]

1. <span data-ttu-id="948c7-118">No navegador, cole o código de dispositivo (que foi copiado quando você clicou em **Copiar e Abrir** na última etapa) e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="948c7-118">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![O navegador de logon do dispositivo][I04]

1. <span data-ttu-id="948c7-120">Por fim, na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="948c7-120">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![A caixa de diálogo Selecionar Assinaturas][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="948c7-122">Como criar um projeto de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="948c7-122">Creating web app project</span></span>

1. <span data-ttu-id="948c7-123">Clique em **Arquivo**, **Novo**, em seguida, clique em **Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="948c7-123">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="948c7-124">(Se você não vir o **Projeto Web Dinâmico** listado como um projeto disponível depois de clicar em **Arquivo** e em **Novo**, faça o seguinte: clique em **Arquivo**, clique em **Novo**, clique em **Projeto...** , expanda **Web**, clique em **Projeto Web Dinâmico** e clique em **Avançar**.)</span><span class="sxs-lookup"><span data-stu-id="948c7-124">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Criando um novo projeto Web dinâmico][file-new-dynamic-web-project]

2. <span data-ttu-id="948c7-126">Para o objetivo deste tutorial, nomeie o projeto **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="948c7-126">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="948c7-127">Sua tela será semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="948c7-127">Your screen will appear similar to the following:</span></span>
   
   ![Novas propriedades do Projeto Web Dinâmico][dynamic-web-project-properties]

3. <span data-ttu-id="948c7-129">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="948c7-129">Click **Finish**.</span></span>

4. <span data-ttu-id="948c7-130">No modo de exibição do Gerenciador de Projeto do Eclipse, expanda **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="948c7-130">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="948c7-131">Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="948c7-131">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Criar um novo arquivo JSP][create-new-jsp-file]

5. <span data-ttu-id="948c7-133">Na caixa de diálogo **Novo Arquivo JSP**, nomeie o arquivo **index.jsp**, mantenha a pasta pai como **MyWebApp/WebContent** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="948c7-133">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Caixa de diálogo Novo Arquivo JSP][new-jsp-file-dialog]

6. <span data-ttu-id="948c7-135">Na caixa de diálogo **Selecionar Modelo JSP**, para a finalidade deste tutorial, escolha **Novo Arquivo JSP (html)** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="948c7-135">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Selecionar um modelo JSP][select-jsp-template]

7. <span data-ttu-id="948c7-137">Quando o arquivo index.jsp for aberto no Eclipse, adicione o texto para exibir dinamicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="948c7-137">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="948c7-138">dentro do elemento existente `<body>`.</span><span class="sxs-lookup"><span data-stu-id="948c7-138">within the existing `<body>` element.</span></span> <span data-ttu-id="948c7-139">Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="948c7-139">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="948c7-140">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="948c7-140">Save index.jsp.</span></span>

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="948c7-141">Como implantar o aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="948c7-141">Deploying web app to Azure</span></span>

1. <span data-ttu-id="948c7-142">Na exibição Gerenciador de Projetos do Eclipse, clique no projeto com o botão direito, escolha **Azure**, em seguida, escolha **Publicar como Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="948c7-142">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Publicar como Aplicativo Web do Azure][publish-as-azure-web-app]

1. <span data-ttu-id="948c7-144">Quando a caixa de diálogo **Implantar Aplicativo Web**for exibida, você poderá escolher uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="948c7-144">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="948c7-145">Selecione um aplicativo Web existente se houver.</span><span class="sxs-lookup"><span data-stu-id="948c7-145">Select an existing web app if one exists.</span></span>

      ![Selecionar o serviço de aplicativo][select-app-service]

   * <span data-ttu-id="948c7-147">Clique em **Criar Novo Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="948c7-147">Click **Create New Web App**.</span></span>

      ![Criar Serviço de Aplicativo][create-app-service]

      <span data-ttu-id="948c7-149">Especifique as informações necessárias para seu aplicativo Web na caixa de diálogo **Criar Serviço de Aplicativo** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="948c7-149">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      <span data-ttu-id="948c7-150">Aqui você pode configurar o ambiente de tempo de execução, as configurações do aplicativo, o grupo de recursos e o plano de serviço.</span><span class="sxs-lookup"><span data-stu-id="948c7-150">Here you can configure the runtime environment, app settings, service plan and resource group.</span></span>

      ![Criar a caixa de diálogo Serviço de Aplicativo][create-app-service-dialog]

1. <span data-ttu-id="948c7-152">Selecione seu aplicativo Web e clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="948c7-152">Select your web app and then click **Deploy**.</span></span>

   ![Implantar serviço de aplicativo][deploy-app-service]

1. <span data-ttu-id="948c7-154">O kit de ferramentas exibirá um status **Publicado** na guia do **Log de Atividades do Azure** quando o aplicativo Web for implantado com êxito, que é um hiperlink para a URL do aplicativo Web implantado.</span><span class="sxs-lookup"><span data-stu-id="948c7-154">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![Status de publicação][publish-status]

1. <span data-ttu-id="948c7-156">Você pode navegar até seu aplicativo Web usando o link fornecido na mensagem de status.</span><span class="sxs-lookup"><span data-stu-id="948c7-156">You can browse to your web app using the link provided in the status message.</span></span>

   ![Procurar seu aplicativo Web][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="cleaning-up-resources"></a><span data-ttu-id="948c7-158">Limpando recursos</span><span class="sxs-lookup"><span data-stu-id="948c7-158">Cleaning up resources</span></span>

1. <span data-ttu-id="948c7-159">Depois de publicar o aplicativo Web no Azure, você poderá gerenciá-lo clicando com o botão direito do mouse no Azure Explorer e selecionando uma das opções no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="948c7-159">After you have published your web app to Azure, you can manage it by right-clicking in Azure Explorer and selecting one of the options in the context menu.</span></span> <span data-ttu-id="948c7-160">Por exemplo, você pode **Excluir** seu aplicativo Web aqui para limpar o recurso para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="948c7-160">For example, you can **Delete** your web app here to clean up the resource for this tutorial.</span></span>

   ![Gerenciar o serviço de aplicativo][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="948c7-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="948c7-162">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="948c7-163">Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="948c7-163">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Visão geral de Aplicativos Web]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->
[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
