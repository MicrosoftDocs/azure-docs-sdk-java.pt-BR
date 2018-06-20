---
title: Criar um aplicativo Web Olá, Mundo para o Azure usando o Eclipse
description: Este tutorial mostra como usar o Kit de Ferramentas do Azure para Eclipse para criar um aplicativo Web Hello World para o Azure.
services: app-service
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
ms.openlocfilehash: 5e025c90c2619ec72ffddf5815fd49c3ac59c00f
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33883643"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a><span data-ttu-id="59435-103">Criar um aplicativo Web Olá, Mundo para o Azure usando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="59435-103">Create a Hello World web app for Azure using Eclipse</span></span>

<span data-ttu-id="59435-104">Este tutorial mostra como criar e implantar um aplicativo Olá, Mundo básico para o Azure como um aplicativo Web usando o [Kit de Ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="59435-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="59435-105">Para obter uma versão deste artigo que usa o [Kit de Ferramentas do Azure para IntelliJ], consulte [Criar um aplicativo Web Olá, Mundo para o Azure usando o IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="59435-105">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="59435-106">O Kit de Ferramentas do Azure para Eclipse foi atualizado em agosto de 2017, com um fluxo de trabalho diferente.</span><span class="sxs-lookup"><span data-stu-id="59435-106">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="59435-107">Este artigo mostra a criação de um aplicativo Web Olá, Mundo usando a versão 3.0.7 (ou posterior) do Kit de Ferramentas do Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="59435-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="59435-108">Se você estiver usando a versão 3.0.6 (ou anterior) do kit de ferramentas, precisará seguir as etapas em [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse usando o kit de ferramentas herdado][Legacy Version].</span><span class="sxs-lookup"><span data-stu-id="59435-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="59435-109">Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="59435-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Visualização do aplicativo Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="59435-111">Criar um novo projeto do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="59435-111">Create a new web app project</span></span>

1. <span data-ttu-id="59435-112">Inicie o Eclipse e entre em sua conta do Azure usando as instruções no artigo [Instruções de entrada no Azure para o Kit de Ferramentas do Azure para Eclipse][eclipse-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="59435-112">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="59435-113">Clique em **Arquivo**, **Novo**, em seguida, clique em **Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="59435-113">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="59435-114">(Se você não vir o **Projeto Web Dinâmico** listado como um projeto disponível depois de clicar em **Arquivo** e em **Novo**, faça o seguinte: clique em **Arquivo**, clique em **Novo**, clique em **Projeto...**, expanda **Web**, clique em **Projeto Web Dinâmico** e clique em **Avançar**.)</span><span class="sxs-lookup"><span data-stu-id="59435-114">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Criando um novo projeto Web dinâmico][file-new-dynamic-web-project]

2. <span data-ttu-id="59435-116">Para o objetivo deste tutorial, nomeie o projeto **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="59435-116">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="59435-117">Sua tela será semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="59435-117">Your screen will appear similar to the following:</span></span>
   
   ![Novas propriedades do Projeto Web Dinâmico][dynamic-web-project-properties]

3. <span data-ttu-id="59435-119">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="59435-119">Click **Finish**.</span></span>

4. <span data-ttu-id="59435-120">No modo de exibição do Gerenciador de Projeto do Eclipse, expanda **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="59435-120">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="59435-121">Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="59435-121">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Criar um novo arquivo JSP][create-new-jsp-file]

5. <span data-ttu-id="59435-123">Na caixa de diálogo **Novo Arquivo JSP**, nomeie o arquivo **index.jsp**, mantenha a pasta pai como **MyWebApp/WebContent** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="59435-123">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Caixa de diálogo Novo Arquivo JSP][new-jsp-file-dialog]

6. <span data-ttu-id="59435-125">Na caixa de diálogo **Selecionar Modelo JSP**, para a finalidade deste tutorial, escolha **Novo Arquivo JSP (html)** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="59435-125">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Selecionar um modelo JSP][select-jsp-template]

7. <span data-ttu-id="59435-127">Quando o arquivo index.jsp for aberto no Eclipse, adicione o texto para exibir dinamicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="59435-127">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="59435-128">dentro do elemento existente `<body>`.</span><span class="sxs-lookup"><span data-stu-id="59435-128">within the existing `<body>` element.</span></span> <span data-ttu-id="59435-129">Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="59435-129">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="59435-130">Salve o index.jsp.</span><span class="sxs-lookup"><span data-stu-id="59435-130">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="59435-131">Implante seu aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="59435-131">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="59435-132">Na exibição Gerenciador de Projetos do Eclipse, clique no projeto com o botão direito, escolha **Azure**, em seguida, escolha **Publicar como Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="59435-132">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Publicar como Aplicativo Web do Azure][publish-as-azure-web-app]

1. <span data-ttu-id="59435-134">Quando a caixa de diálogo **Implantar Aplicativo Web**for exibida, você poderá escolher uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="59435-134">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="59435-135">Selecione um aplicativo Web existente se houver.</span><span class="sxs-lookup"><span data-stu-id="59435-135">Select an existing web app if one exists.</span></span>

      ![Selecionar o serviço de aplicativo][select-app-service]

   * <span data-ttu-id="59435-137">Clique em **Criar Novo Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="59435-137">Click **Create New Web App**.</span></span>

      ![Criar Serviço de Aplicativo][create-app-service]

      <span data-ttu-id="59435-139">Especifique as informações necessárias para seu aplicativo Web na caixa de diálogo **Criar Serviço de Aplicativo** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="59435-139">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      ![Criar a caixa de diálogo Serviço de Aplicativo][create-app-service-dialog]

1. <span data-ttu-id="59435-141">Selecione seu aplicativo Web e clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="59435-141">Select your web app and then click **Deploy**.</span></span>

   ![Implantar serviço de aplicativo][deploy-app-service]

1. <span data-ttu-id="59435-143">O kit de ferramentas exibirá um status **Publicado** na guia do **Log de Atividades do Azure** quando o aplicativo Web for implantado com êxito, que é um hiperlink para a URL do aplicativo Web implantado.</span><span class="sxs-lookup"><span data-stu-id="59435-143">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![Status de publicação][publish-status]

1. <span data-ttu-id="59435-145">Você pode navegar até seu aplicativo Web usando o link fornecido na mensagem de status.</span><span class="sxs-lookup"><span data-stu-id="59435-145">You can browse to your web app using the link provided in the status message.</span></span>

   ![Procurar seu aplicativo Web][browse-web-app]

1. <span data-ttu-id="59435-147">Depois de publicar a Web no Azure, você poderá gerenciar seu aplicativo ao clicar com o botão direito e selecionar uma das opções no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="59435-147">After you have published your web to Azure, you can manage your app by right-clicking on it and selecting one of the options on the context menu.</span></span> <span data-ttu-id="59435-148">Por exemplo, você pode **Iniciar**, **Parar** ou **Excluir** seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="59435-148">For example, you can **Start**, **Stop**, or **Delete** your web app.</span></span>

   ![Gerenciar o serviço de aplicativo][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="59435-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59435-150">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="59435-151">Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].</span><span class="sxs-lookup"><span data-stu-id="59435-151">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

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
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

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
