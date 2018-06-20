---
title: Criar um aplicativo Web Olá, Mundo para o Azure usando o IntelliJ
description: Este tutorial mostra como usar o Kit de Ferramentas do Azure para IntelliJ para criar um aplicativo Web Hello World para o Azure.
services: app-service
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
ms.openlocfilehash: cc68e16a6940a1f0f2b08f0b63c90c58ec6dbc4e
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954187"
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a><span data-ttu-id="3bbf5-103">Criar um aplicativo Web Olá, Mundo para o Azure usando o IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3bbf5-103">Create a Hello World web app for Azure using IntelliJ</span></span>

<span data-ttu-id="3bbf5-104">Este tutorial mostra como criar e implantar um aplicativo Olá, Mundo básico para o Azure como um aplicativo Web usando o [Kit de Ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="3bbf5-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="3bbf5-105">Para obter uma versão deste artigo que usa o [Kit de Ferramentas do Azure para Eclipse], consulte [Criar um aplicativo Web Olá, Mundo para o Azure usando o Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="3bbf5-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="3bbf5-106">O Kit de Ferramentas do Azure para IntelliJ foi atualizado em agosto de 2017 com um fluxo de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="3bbf5-107">Este artigo mostra a criação de um aplicativo Web Olá, Mundo usando a versão 3.0.7 (ou posterior) do Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="3bbf5-108">Se você estiver usando a versão 3.0.6 (ou anterior) do kit de ferramentas, precisará seguir as etapas em [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ usando o kit de ferramentas herdado][Legacy Version].</span><span class="sxs-lookup"><span data-stu-id="3bbf5-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="3bbf5-109">Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="3bbf5-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Visualização do aplicativo Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="3bbf5-111">Criar um novo projeto do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="3bbf5-111">Create a new web app project</span></span>

1. <span data-ttu-id="3bbf5-112">Inicie o IntelliJ e entre em sua conta do Azure usando as instruções no artigo [Instruções de entrada do Azure para o Kit de Ferramentas do Azure para IntelliJ][intelliJ-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="3bbf5-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="3bbf5-113">Clique menu **Arquivo**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Criar um novo projeto][file-new-project]

1. <span data-ttu-id="3bbf5-115">Na caixa de diálogo **Novo Projeto**, selecione **Maven**, em seguida, **maven-archetype-webapp** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-115">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Escolha o aplicativo Web do modelo Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="3bbf5-117">Especifique o **GroupId** e **ArtifactId** para seu aplicativo Web e depois clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-117">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Especifique GroupId e ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="3bbf5-119">Personalize as configurações de Maven ou aceite os padrões e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-119">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Especifique as configurações de Maven][maven-options]

1. <span data-ttu-id="3bbf5-121">Especifique um nome de projeto e local e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-121">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Especifique o nome do projeto][project-name]

1. <span data-ttu-id="3bbf5-123">Na exibição do Explorador de Projetos do IntelliJ, expanda **src**, **principal**, **aplicativos Web** e clique duas vezes em **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-123">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![Abra a página de índice][open-index-page]

1. <span data-ttu-id="3bbf5-125">Quando o arquivo index.jsp for aberto no IntelliJ, adicione o texto para exibir dinamicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="3bbf5-125">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="3bbf5-126">dentro do elemento existente `<body>`.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-126">within the existing `<body>` element.</span></span> <span data-ttu-id="3bbf5-127">Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3bbf5-127">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Edite a página de índice][edit-index-page]

1. <span data-ttu-id="3bbf5-129">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-129">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="3bbf5-130">Implante seu aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="3bbf5-130">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="3bbf5-131">Na exibição do Explorador de Projetos do IntelliJ, clique no seu projeto com o botão direito do mouse, escolha **Azure**e, em seguida, escolha **Executar no aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-131">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![Menu Executar no aplicativo Web][run-on-web-app-menu]

1. <span data-ttu-id="3bbf5-133">Na caixa de diálogo Executar no aplicativo Web, você pode escolher uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="3bbf5-133">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="3bbf5-134">Escolha um aplicativo Web existente (se houver) e clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-134">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![Caixa de diálogo Executar no aplicativo Web][run-on-web-app-dialog]

   * <span data-ttu-id="3bbf5-136">Clique em **Criar Novo Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-136">Click **Create New Web App**.</span></span> <span data-ttu-id="3bbf5-137">Se você optar por criar um novo aplicativo Web, especifique as informações necessárias para seu aplicativo Web e, em seguida, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-137">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![Criar novo aplicativo Web][create-new-web-app-dialog]

1. <span data-ttu-id="3bbf5-139">O kit de ferramentas exibirá uma mensagem de status quando tiver implantado com êxito seu aplicativo Web, que também exibe a URL do aplicativo Web implantado.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-139">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![Implantação bem-sucedida][successfully-deployed]

1. <span data-ttu-id="3bbf5-141">Você pode navegar até seu aplicativo Web usando o link fornecido na mensagem de status.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-141">You can browse to your web app using the link provided in the status message.</span></span>

   ![Procurar seu aplicativo Web][browse-web-app]

1. <span data-ttu-id="3bbf5-143">Depois de publicar seu aplicativo Web, as configurações serão salvas como padrão e você poderá executar seu aplicativo no Azure clicando no ícone de seta verde na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-143">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="3bbf5-144">Você pode modificar as configurações clicando no menu suspenso para seu aplicativo Web e clique em **Editar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-144">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menu Editar configuração][edit-configuration-menu]

1. <span data-ttu-id="3bbf5-146">Quando a caixa de diálogo **Configurações de execução/depuração** for exibida, você poderá modificar as configurações padrão e, em seguida, clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3bbf5-146">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Caixa de diálogo Editar configuração][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="3bbf5-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3bbf5-148">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="3bbf5-149">Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="3bbf5-149">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

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
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
