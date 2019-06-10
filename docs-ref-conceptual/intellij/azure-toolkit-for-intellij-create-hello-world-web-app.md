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
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a>Criar um aplicativo Web Olá, Mundo para o Serviço de Aplicativo do Azure usando o IntelliJ

Usando o plug-in [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) de software livre, criar e implantar um aplicativo Olá, Mundo básico para o Serviço de Aplicativo do Azure como um aplicativo Web pode ser feito em poucos minutos.

> [!NOTE]
>
> Se você preferir usar o Eclipse, confira nosso [tutorial semelhante para o Eclipse][eclipse-hello-world].
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> Não se esqueça de limpar os recursos depois de concluir este tutorial. Nesse caso, executar este guia não excederá sua cota da conta gratuita.
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a>Instalação e credenciais

1. Na caixa de diálogo Configurações/Preferências do IntelliJ IDEA (Ctrl+Alt+S), selecione **Plug-ins**. Em seguida, localize o **Azure Toolkit for IntelliJ** no **Marketplace** e clique em **Instalar**. Depois de instalado, clique em **Reiniciar** para ativar o plug-in. 

   ![Plug-in do Azure Toolkit for IntelliJ no Marketplace][marketplace]

2. Para entrar sua conta do Azure, abra a barra lateral **Azure Explorer** e, em seguida, clique no ícone **Entrar no Azure** na barra na parte superior (ou no menu IDEA **Ferramentas/Azure/Entrada no Azure**).

   ![O comando de Entrada do IntelliJ Azure][I01]

3. Na janela **Entrar no Azure**, selecione **Logon do Dispositivo** e, em seguida, clique em **Entrar** ([outras opções de entrada](azure-toolkit-for-intellij-sign-in-instructions.md)).

   ![A janela Entrar no Azure com o logon no dispositivo selecionado][I02]

4. Clique em **Copiar e Abrir** na caixa de diálogo **Logon no Dispositivo do Azure**.

   ![A janela da caixa de diálogo Logon no Azure][I03]

5. No navegador, cole o código de dispositivo (que foi copiado quando você clicou em **Copiar e Abrir** na última etapa) e, em seguida, clique em **Avançar**.

   ![O navegador de logon do dispositivo][I04]

6. Na caixa de diálogo **Selecionar Assinaturas**, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.

   ![A caixa de diálogo Selecionar Assinaturas][I05]

## <a name="creating-web-app-project"></a>Como criar um projeto de aplicativo Web

1. No IntelliJ, clique menu **Arquivo**, clique em **Novo** e em **Projeto**.

   ![Criar um novo projeto][file-new-project]

2. Na caixa de diálogo **Novo Projeto**, selecione **Maven**, em seguida, **maven-archetype-webapp** e, em seguida, clique em **Avançar**.

   ![Escolha o Webapp do arquétipo Maven][maven-archetype-webapp]

3. Especifique o **GroupId** e **ArtifactId** para seu aplicativo Web e depois clique em **Avançar**.

   ![Especifique GroupId e ArtifactId][groupid-and-artifactid]

4. Personalize as configurações de Maven ou aceite os padrões e, em seguida, clique em **Avançar**.

   ![Especifique as configurações de Maven][maven-options]

5. Especifique um nome de projeto e local e, em seguida, clique em **Concluir**.

   ![Especifique o nome do projeto][project-name]

6. Na exibição do Explorador de Projeto, abra e edite o arquivo **src/main/webapp/index.jsp** da seguinte maneira e **salve as alterações**:

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Edite a página de índice][edit-index-page]

## <a name="deploying-web-app-to-azure"></a>Como implantar o aplicativo Web no Azure

1. Na exibição do Explorador de Projeto, clique com o botão direito do mouse em seu projeto, expanda **Azure** e, em seguida, clique em **Implantar no Azure**.

   ![Menu Implantar no Azure][deploy-to-azure-menu]

1. Na caixa de diálogo Implantar no Azure, você pode implantar diretamente o aplicativo em um webapp Tomcat existente se você já tiver um; caso contrário, deverá criar um primeiro.
   1. Clique no link **Nenhum webapp disponível, clique para criar um** para criar um aplicativo Web. Você poderia escolher **Criar WebApp** na lista suspensa do WebApp se houvesse webapps existentes em sua assinatura.

      ![Caixa de diálogo Implantar para o Azure][deploy-to-azure-dialog]

   1. Na caixa de diálogo pop-up, escolha **TOMCAT 8.5-jre8** como o contêiner da Web, especifique outras informações necessárias e clique em **OK** para criar o webapp.

      ![Criar novo aplicativo Web][create-new-web-app-dialog]

   1. Escolha o aplicativo Web no menu suspenso WebApp e, em seguida, clique em **Executar**. (Você poderá começar aqui se desejar implantar em um webapp existente)

      ![Implantar no webapp existente][deploy-to-existing-webapp]

1. O kit de ferramentas exibirá uma mensagem de status quando tiver implantado com êxito seu aplicativo Web, junto com a URL do aplicativo Web implantado, se bem-sucedido.

   ![Implantação bem-sucedida][successfully-deployed]

1. Você pode navegar até seu aplicativo Web usando o link fornecido na mensagem de status.

   ![Procurar seu aplicativo Web][browse-web-app]

## <a name="managing-deploy-configurations"></a>Como gerenciar configurações de implantação

1. Depois de publicar seu aplicativo Web, as configurações serão salvas como padrão e você poderá executar a implantação clicando no ícone de seta verde na barra de ferramentas. Você pode modificar as configurações clicando no menu suspenso para seu aplicativo Web e clique em **Editar Configurações**.

   ![Menu Editar configuração][edit-configuration-menu]

1. Quando a caixa de diálogo **Configurações de execução/depuração** for exibida, você poderá modificar as configurações padrão e, em seguida, clicar em **OK**.

   ![Caixa de diálogo Editar configuração][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a>Limpando recursos

1. Como excluir Aplicativos Web no Azure Explorer

     ![Limpar recursos][clean-resources]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Para obter mais informações sobre como criar aplicativos Web do Azure, confira a [Visão geral de Aplicativos Web].

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Visão geral de Aplicativos Web]: /azure/app-service/app-service-web-overview
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
