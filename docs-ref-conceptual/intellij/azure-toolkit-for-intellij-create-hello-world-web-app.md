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
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a>Criar um aplicativo Web Olá, Mundo para o Azure usando o IntelliJ

Este tutorial mostra como criar e implantar um aplicativo Olá, Mundo básico para o Azure como um aplicativo Web usando o [Kit de Ferramentas do Azure para IntelliJ].

> [!NOTE]
>
> Para obter uma versão deste artigo que usa o [Kit de Ferramentas do Azure para Eclipse], consulte [Criar um aplicativo Web Olá, Mundo para o Azure usando o Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> O Kit de Ferramentas do Azure para IntelliJ foi atualizado em agosto de 2017 com um fluxo de trabalho diferente. Este artigo mostra a criação de um aplicativo Web Olá, Mundo usando a versão 3.0.7 (ou posterior) do Kit de Ferramentas do Azure para IntelliJ. Se você estiver usando a versão 3.0.6 (ou anterior) do kit de ferramentas, precisará seguir as etapas em [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ usando o kit de ferramentas herdado][Legacy Version].
> 

Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:

![Visualização do aplicativo Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Criar um novo projeto do aplicativo Web

1. Inicie o IntelliJ e entre em sua conta do Azure usando as instruções no artigo [Instruções de entrada do Azure para o Kit de Ferramentas do Azure para IntelliJ][intelliJ-sign-in-instructions].

1. Clique menu **Arquivo**, clique em **Novo** e em **Projeto**.
   
   ![Criar um novo projeto][file-new-project]

1. Na caixa de diálogo **Novo Projeto**, selecione **Maven**, em seguida, **maven-archetype-webapp** e, em seguida, clique em **Avançar**.
   
   ![Escolha o aplicativo Web do modelo Maven][maven-archetype-webapp]
   
1. Especifique o **GroupId** e **ArtifactId** para seu aplicativo Web e depois clique em **Avançar**.
   
   ![Especifique GroupId e ArtifactId][groupid-and-artifactid]

1. Personalize as configurações de Maven ou aceite os padrões e, em seguida, clique em **Avançar**.
   
   ![Especifique as configurações de Maven][maven-options]

1. Especifique um nome de projeto e local e, em seguida, clique em **Concluir**.
   
   ![Especifique o nome do projeto][project-name]

1. Na exibição do Explorador de Projetos do IntelliJ, expanda **src**, **principal**, **aplicativos Web** e clique duas vezes em **index.jsp**.
   
   ![Abra a página de índice][open-index-page]

1. Quando o arquivo index.jsp for aberto no IntelliJ, adicione o texto para exibir dinamicamente **Hello World!** dentro do elemento existente `<body>`. Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Edite a página de índice][edit-index-page]

1. Salve o index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Implante seu aplicativo Web no Azure

1. Na exibição do Explorador de Projetos do IntelliJ, clique no seu projeto com o botão direito do mouse, escolha **Azure**e, em seguida, escolha **Executar no aplicativo Web**.
   
   ![Menu Executar no aplicativo Web][run-on-web-app-menu]

1. Na caixa de diálogo Executar no aplicativo Web, você pode escolher uma das seguintes opções:

   * Escolha um aplicativo Web existente (se houver) e clique em **Executar**.

      ![Caixa de diálogo Executar no aplicativo Web][run-on-web-app-dialog]

   * Clique em **Criar Novo Aplicativo Web**. Se você optar por criar um novo aplicativo Web, especifique as informações necessárias para seu aplicativo Web e, em seguida, clique em **Executar**.

      ![Criar novo aplicativo Web][create-new-web-app-dialog]

1. O kit de ferramentas exibirá uma mensagem de status quando tiver implantado com êxito seu aplicativo Web, que também exibe a URL do aplicativo Web implantado.

   ![Implantação bem-sucedida][successfully-deployed]

1. Você pode navegar até seu aplicativo Web usando o link fornecido na mensagem de status.

   ![Procurar seu aplicativo Web][browse-web-app]

1. Depois de publicar seu aplicativo Web, as configurações serão salvas como padrão e você poderá executar seu aplicativo no Azure clicando no ícone de seta verde na barra de ferramentas. Você pode modificar as configurações clicando no menu suspenso para seu aplicativo Web e clique em **Editar Configurações**.

   ![Menu Editar configuração][edit-configuration-menu]

1. Quando a caixa de diálogo **Configurações de execução/depuração** for exibida, você poderá modificar as configurações padrão e, em seguida, clicar em **OK**.

   ![Caixa de diálogo Editar configuração][edit-configuration-dialog]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].

<!-- URL List -->

[Kit de Ferramentas do Azure para IntelliJ]: azure-toolkit-for-intellij.md
[Kit de Ferramentas do Azure para Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Visão geral de Aplicativos Web]: /azure/app-service/app-service-web-overview
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
