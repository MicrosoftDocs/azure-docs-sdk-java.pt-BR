---
title: ''
description: Este tutorial mostra como usar a versão 3.0.6 (ou anterior) do Kit de Ferramentas do Azure para Eclipse para criar um aplicativo Web Olá, Mundo para o Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: b05dcd52f36524ab17652f83c6ced4006f874365
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338710"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a>Criar um aplicativo Web Olá, Mundo para o Azure usando o kit de ferramentas herdado do Eclipse

Este tutorial mostra como criar e implantar um aplicativo Olá, Mundo básico para o Azure como um aplicativo Web usando a versão 3.0.6 (ou anterior) do [Kit de Ferramentas do Azure para Eclipse].

> [!NOTE]
>
> Para obter uma versão deste artigo que usa o [Kit de Ferramentas do Azure para IntelliJ], consulte [Criar um aplicativo Web Olá, Mundo para o Azure usando o IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> O Kit de Ferramentas do Azure para Eclipse foi atualizado em agosto de 2017, com um fluxo de trabalho diferente. Este artigo mostra a criação de um aplicativo Web Olá, Mundo usando a versão 3.0.6 (ou anterior) do Kit de Ferramentas do Azure para Eclipse. Se você estiver usando a versão 3.0.7 (ou posterior) do kit de ferramentas, precisará seguir as etapas em [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse][Updated Version].
>

Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:

![Visualização do aplicativo Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Criar um novo projeto do aplicativo Web

1. Inicie o Eclipse e entre em sua conta do Azure usando as instruções no artigo [Instruções de entrada do Azure para o Kit de Ferramentas do Azure para Eclipse][eclipse-sign-in-instructions].

1. Clique em **Arquivo**, **Novo**, em seguida, clique em **Projeto Web Dinâmico**. (Se você não vir o **Projeto Web Dinâmico** listado como um projeto disponível depois de clicar em **Arquivo** e em **Novo**, faça o seguinte: clique em **Arquivo**, clique em **Novo**, clique em **Projeto...**, expanda **Web**, clique em **Projeto Web Dinâmico** e clique em **Avançar**.)

2. Para o objetivo deste tutorial, nomeie o projeto **MyWebApp**. Sua tela será semelhante à seguinte:
   
   ![Criando um novo projeto Web dinâmico][02]

3. Clique em **Concluir**.

4. Na exibição **Gerenciador de Projetos** do Eclipse, expanda **MyWebApp**. Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.

5. Na caixa de diálogo **Novo Arquivo JSP**, nomeie o arquivo **index.jsp**, mantenha a pasta pai como **MyWebApp/WebContent** e clique em **Avançar**.

6. Na caixa de diálogo **Selecionar Modelo JSP**, para a finalidade deste tutorial, escolha **Novo Arquivo JSP (html)** e clique em **Concluir**.

7. Quando o arquivo index.jsp for aberto no Eclipse, adicione o texto para exibir dinamicamente **Hello World!** dentro do elemento existente `<body>`. Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Salve o index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Implante seu aplicativo Web no Azure

Há várias maneiras pelas quais você pode implantar um aplicativo Web Java no Azure. Este tutorial descreve uma das mais simples: o aplicativo será implantado em um contêiner de aplicativos Web do Azure, e não há a necessidade de qualquer tipo de projeto especial nem de ferramentas adicionais. O JDK e o software do contêiner da Web serão fornecidos a você pelo Azure, portanto, não é necessário carregar seu próprio; tudo o que você precisa é de seu aplicativo Web Java. Como resultado, o processo de publicação de seu aplicativo demorará segundos, e não minutos.

1. No Gerenciador de Projetos do Eclipse, clique com o botão direito do mouse em **MyWebApp**.

2. No menu de contexto, selecione **Azure** e clique em **Publicar como Aplicativo Web do Azure...**
   
   ![Publicar como Aplicativo Web do Azure][03]
   
   Como alternativa, enquanto o projeto do aplicativo Web é selecionado no Explorador de Projeto, é possível clicar no botão suspenso **Publicar** na barra de ferramentas e selecionar **Publicar como Aplicativo Web do Azure** lá:
   
   ![Publicar como Aplicativo Web do Azure][14]

3. Se você ainda não entrou no Azure por meio do Eclipse, será solicitado que você entre em sua conta do Azure:
   
   ![Caixa de diálogo Entrar no Azure][04]
   
   Se você tiver várias contas do Azure, alguns dos avisos mostrados durante o processo de entrada poderão ser exibidos mais de uma vez, mesmo se forem aparentemente os mesmos. Quando isso acontecer, continue seguindo as instruções de entrada.

4. Após o logon bem-sucedido em sua conta do Azure, a caixa de diálogo **Gerenciar Assinaturas** exibirá uma lista de assinaturas associadas às suas credenciais. Se houver várias assinaturas listadas e se você quiser trabalhar com apenas um subconjunto específico delas, poderá, opcionalmente, desmarcar as que deseja usar. Depois de selecionar suas assinaturas, clique em **Fechar**.
   
   ![Caixa de diálogo Gerenciar Assinaturas][05]

5. Quando a caixa de diálogo **Implantar no Contêiner do Aplicativo Web do Azure** for mostrada, ela exibirá todos os contêineres do Aplicativo Web criados anteriormente por você; se você não tiver criado nenhum contêiner, a lista estará vazia.
   
   ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][06]

6. Se você nunca tiver criado um contêiner de aplicativos Web do Azure, ou se quiser publicar seu aplicativo em um novo contêiner, use as etapas a seguir. Caso contrário, selecione um Contêiner de Aplicativo Web existente e pule para a etapa 7 abaixo.
   
    a. Clique em **Novo...**
      
      ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][15]

   b. A caixa de diálogo **Novo Contêiner do Aplicativo Web** será exibida:
      
      ![Caixa de diálogo Novo contêiner do aplicativo Web][07a]

   c. Insira um **Rótulo DNS** para seu Contêiner do Aplicativo Web; isso formará o rótulo DNS folha da URL do host de seu aplicativo Web no Azure. (Observe que o nome deve estar disponível e de acordo com os requisitos de nomenclatura de aplicativo Web do Azure.)

   d. No menu suspenso **Contêiner da Web** , selecione o software apropriado ao seu aplicativo.
      
      No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9. Uma distribuição recente do software selecionado será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK fornecido pelo Azure.

   e. No menu suspenso **Assinatura** , selecione a assinatura que deseja usar para essa implantação.

   f. No menu suspenso **Grupo de Recursos** , selecione o Grupo de Recursos com o qual deseja associar seu Aplicativo Web. (Os Grupos de Recursos do Azure lhe permitem agrupar recursos relacionados para que, por exemplo, possam ser excluídos juntos.)
      
      Você pode selecionar um Grupo de Recursos existente (se houver) e ignorar a etapa g abaixo ou usar as seguintes etapas para criar um novo Grupo de Recursos:
      
   * Clique em **Novo...**
   * A caixa de diálogo **Novo Grupo de Recursos** será exibida:
        
       ![Caixa de diálogo Novo Grupo de Recursos][08]
   * Na caixa de texto **Nome** , especifique um nome para o novo Grupo de Recursos.
   * No menu suspenso **Região** , selecione a localização do data center do Azure apropriada ao Grupo de Recursos.
   * OPCIONAL: por padrão, uma distribuição recente de Java 8 será implantada pelo Azure automaticamente no contêiner de aplicativo Web como sua JVM. No entanto, você pode especificar uma versão e uma distribuição da JVM diferentes se for necessário para seu aplicativo Web. Para especificar o JDK do seu aplicativo Web, clique na guia **JDK** e selecione uma das seguintes opções:
     * **Implantar o JDK padrão oferecido pelo Serviço de Aplicativos Web do Azure**: essa opção implantará uma distribuição recente do Java.
     * **Implantar um JDK de terceiro disponível no Azure**: essa opção permite que você escolha na lista de JDKs que são fornecidos pelo Microsoft Azure.
     * **Meu próprio JDK deste local de download**: essa opção permite que você especifique sua própria distribuição de JDK, que deve ser empacotada como um arquivo ZIP e carregada em um local de download disponível publicamente ou em uma conta de armazenamento do Azure à qual você tenha acesso.
          
       ![Caixa de diálogo Novo contêiner do aplicativo Web][07b]

   g. Clique em **OK**.

   h. O menu suspenso **Plano do Serviço de Aplicativo** lista os planos do serviço de aplicativo associados ao Grupo de Recursos selecionado. (Os Planos do Serviço de Aplicativo especificam informações como o local de seu Aplicativo Web, o tipo de preço e o tamanho da instância de computação. Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * Clique em **Novo...**
      * A caixa de diálogo **Novo Plano do Serviço de Aplicativo** será exibida:
        
          ![Caixa de diálogo Novo Plano do Serviço de Aplicativo][09]
      * Na caixa de texto **Nome** , especifique um nome para o novo Plano do Serviço de Aplicativo.
      * No menu suspenso **Localização** , selecione a localização do data center do Azure apropriada ao plano.
      * No menu suspenso **Tipo de Preço** , selecione o preço apropriado ao plano. Para fins de teste, é possível escolher **Gratuito**.
      * No menu suspenso **Tamanho da Instância** , selecione o tamanho de instância apropriado ao plano. Para fins de teste, é possível escolher **Pequeno**.

   i. Depois de concluir todas as etapas acima, a caixa de diálogo New Web App Container (Novo Contêiner de Aplicativos Web) deve ser semelhante à ilustração a seguir:
      
      ![Caixa de diálogo Novo contêiner do aplicativo Web][10]

   j. Clique em **OK** para concluir a criação do novo contêiner do Aplicativo Web.
       
      Aguarde alguns segundos para a lista de contêineres de Aplicativo Web ser atualizada. O contêiner do aplicativo Web recém-criado agora deve ser selecionado na lista.

7. Agora você está pronto para concluir a implantação inicial de seu Aplicativo Web no Azure:
   
   ![Caixa de diálogo Implantar no contêiner do aplicativo Web do Azure][11]
   
   Clique em **OK** para implantar o aplicativo Java no contêiner do Aplicativo Web selecionado.
   
   Por padrão, o aplicativo será implantado como um subdiretório do servidor de aplicativos. Se desejar implantá-lo como o aplicativo raiz, marque a caixa de seleção **Implantar na raiz** antes de clicar em **OK**.

8. Em seguida, você deverá ver o modo de exibição do **Log de Atividades do Azure** , que indicará o status da implantação de seu Aplicativo Web.
   
   ![Log de Atividades do Azure][12]
   
   O processo de implantação de seu aplicativo Web no Azure deve demorar apenas alguns segundos para ser concluído. Quando seu aplicativo estiver pronto, você verá um link chamado **Publicada** in the **Status** . Ao clicar no link, você será levado à home page do Aplicativo Web implantado.

## <a name="updating-your-web-app"></a>Atualização de seu aplicativo Web

A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:

* Você pode atualizar a implantação de um aplicativo Web Java existente.
* Você pode publicar um aplicativo Java adicional no mesmo contêiner de aplicativo Web.

Em ambos os casos, o processo é idêntico e demora apenas alguns segundos:

1. No explorador de projetos do Eclipse, clique com o botão direito do mouse no aplicativo Java que você deseja atualizar ou adicionar a um contêiner de aplicativos Web existente.

2. Quando o menu de contexto for exibido, selecione **Azure** e, em seguida, **Publicar como Aplicativo Web do Azure...**

3. Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes. Selecione aquele no qual deseja publicar ou publicar novamente o aplicativo Java e clique em **OK**.

Após alguns segundos, o modo de exibição do **Log de Atividades do Azure** mostrará a implantação atualizada como **Publicada** e será possível verificar o aplicativo atualizado em um navegador da Web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Iniciar, parar ou reiniciar o aplicativo Web existente

Para iniciar ou parar um contêiner do Aplicativo Web do Azure existente, (incluindo todos os aplicativos Java implantados nele), é possível usar o modo de exibição do **Azure Explorer** .

Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Janela** no Eclipse, clicando em **Mostrar Modo de Exibição**, em **Outros...**, em **Azure** e em **Azure Explorer**. Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.

Quando o modo de exibição do **Azure Explorer** for exibido, use estas etapas para iniciar ou parar o Aplicativo Web: 

1. Expanda o nó **Azure** .

2. Expanda o nó **Aplicativos Web** . 

3. Clique com botão direito do mouse no Aplicativo Web desejado.

4. Quando o menu de contexto for exibido, clique em **Iniciar**, **Parar** ou **Reiniciar**. Observe que as opções de menu são sensíveis ao contexto, para que você só possa parar um aplicativo Web que esteja em execução ou iniciar um aplicativo Web que não esteja em execução no momento.
   
   ![Interromper um aplicativo Web existente][13]

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
