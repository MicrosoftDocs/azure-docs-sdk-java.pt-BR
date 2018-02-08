---
title: "Criar um aplicativo Web Olá, Mundo para o Azure usando o Eclipse"
description: Este tutorial mostra como usar o Kit de Ferramentas do Azure para Eclipse para criar um aplicativo Web Hello World para o Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: bec94e65951330c933e0173fd580c3578e759c18
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a>Criar um aplicativo Web Olá, Mundo para o Azure usando o Eclipse

Este tutorial mostra como criar e implantar um aplicativo Olá, Mundo básico para o Azure como um aplicativo Web usando o [Kit de Ferramentas do Azure para Eclipse].

> [!NOTE]
>
> Para obter uma versão deste artigo que usa o [Kit de Ferramentas do Azure para IntelliJ], consulte [Criar um aplicativo Web Olá, Mundo para o Azure usando o IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> O Kit de Ferramentas do Azure para Eclipse foi atualizado em agosto de 2017, com um fluxo de trabalho diferente. Este artigo mostra a criação de um aplicativo Web Olá, Mundo usando a versão 3.0.7 (ou posterior) do Kit de Ferramentas do Azure para Eclipse. Se você estiver usando a versão 3.0.6 (ou anterior) do kit de ferramentas, precisará seguir as etapas em [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse usando o kit de ferramentas herdado][Legacy Version].
> 

Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:

![Visualização do aplicativo Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Criar um novo projeto do aplicativo Web

1. Inicie o Eclipse e entre em sua conta do Azure usando as instruções no artigo [Instruções de entrada no Azure para o Kit de Ferramentas do Azure para Eclipse][eclipse-sign-in-instructions].

1. Clique em **Arquivo**, **Novo**, em seguida, clique em **Projeto Web Dinâmico**. (Se você não vir o **Projeto Web Dinâmico** listado como um projeto disponível depois de clicar em **Arquivo** e em **Novo**, faça o seguinte: clique em **Arquivo**, clique em **Novo**, clique em **Projeto...**, expanda **Web**, clique em **Projeto Web Dinâmico** e clique em **Avançar**.)

   ![Criando um novo projeto Web dinâmico][file-new-dynamic-web-project]

2. Para o objetivo deste tutorial, nomeie o projeto **MyWebApp**. Sua tela será semelhante à seguinte:
   
   ![Novas propriedades do Projeto Web Dinâmico][dynamic-web-project-properties]

3. Clique em **Concluir**.

4. No modo de exibição do Gerenciador de Projeto do Eclipse, expanda **MyWebApp**. Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.

   ![Criar um novo arquivo JSP][create-new-jsp-file]

5. Na caixa de diálogo **Novo Arquivo JSP**, nomeie o arquivo **index.jsp**, mantenha a pasta pai como **MyWebApp/WebContent** e clique em **Avançar**.

   ![Caixa de diálogo Novo Arquivo JSP][new-jsp-file-dialog]

6. Na caixa de diálogo **Selecionar Modelo JSP**, para a finalidade deste tutorial, escolha **Novo Arquivo JSP (html)** e clique em **Concluir**.

   ![Selecionar um modelo JSP][select-jsp-template]

7. Quando o arquivo index.jsp for aberto no Eclipse, adicione o texto para exibir dinamicamente **Hello World!** dentro do elemento existente `<body>`. Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Salve o index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Implante seu aplicativo Web no Azure

1. Na exibição Gerenciador de Projetos do Eclipse, clique no projeto com o botão direito, escolha **Azure**, em seguida, escolha **Publicar como Aplicativo Web**.
   
   ![Publicar como Aplicativo Web do Azure][publish-as-azure-web-app]

1. Quando a caixa de diálogo **Implantar Aplicativo Web**for exibida, você poderá escolher uma das seguintes opções:

   * Selecione um aplicativo Web existente se houver.

      ![Selecionar o serviço de aplicativo][select-app-service]

   * Clique em **Criar Novo Aplicativo Web**.

      ![Criar Serviço de Aplicativo][create-app-service]

      Especifique as informações necessárias para seu aplicativo Web na caixa de diálogo **Criar Serviço de Aplicativo** e clique em **Criar**.

      ![Criar a caixa de diálogo Serviço de Aplicativo][create-app-service-dialog]

1. Selecione seu aplicativo Web e clique em **Implantar**.

   ![Implantar serviço de aplicativo][deploy-app-service]

1. O kit de ferramentas exibirá um status **Publicado** no **Log de Atividades do Azure** quando o aplicativo Web for implantado com êxito, que é um hiperlink para a URL do aplicativo Web implantado.

   ![Status de publicação][publish-status]

1. Você pode navegar até seu aplicativo Web usando o link fornecido na mensagem de status.

   ![Procurar seu aplicativo Web][browse-web-app]

1. Depois de publicar a Web no Azure, você poderá gerenciar seu aplicativo ao clicar com o botão direito e selecionar uma das opções no menu de contexto. Por exemplo, você pode **Iniciar**, **Parar** ou **Excluir** seu aplicativo Web.

   ![Gerenciar o serviço de aplicativo][manage-app-service]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].

<!-- URL List -->

[Kit de Ferramentas do Azure para Eclipse]: azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Visão geral de Aplicativos Web]: /azure/app-service/app-service-web-overview
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
