---
title: Criar um aplicativo Web Olá, Mundo para o Azure usando o kit de ferramentas herdado do IntelliJ
description: Este tutorial mostra como usar a versão 3.0.6 (ou anterior) do Kit de Ferramentas do Azure para IntelliJ para criar um aplicativo Web Olá, Mundo para o Azure.
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
ms.openlocfilehash: efc1dffa248987772827bbe7bc0caa9f10a0b4ef
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090779"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a>Criar um aplicativo Web Olá, Mundo para o Azure usando o kit de ferramentas herdado do IntelliJ

Este tutorial mostra como criar e implantar um aplicativo Olá, Mundo básico para o Azure como um aplicativo Web usando a versão 3.0.6 (ou anterior) do [Kit de Ferramentas do Azure para IntelliJ].

> [!NOTE]
>
> Para obter uma versão deste artigo que usa o [Kit de Ferramentas do Azure para Eclipse], consulte [Criar um aplicativo Web Olá, Mundo para o Azure usando o Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> O Kit de Ferramentas do Azure para IntelliJ foi atualizado em agosto de 2017 com um fluxo de trabalho diferente. Este artigo mostra a criação de um aplicativo Web Olá, Mundo usando a versão 3.0.6 (ou anterior) do Kit de Ferramentas do Azure para IntelliJ. Se você estiver usando a versão 3.0.7 (ou posterior) do kit de ferramentas, precisará seguir as etapas em [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ][Updated Version].
>

Após a conclusão deste tutorial, seu aplicativo será semelhante à ilustração a seguir quando exibido em um navegador da Web:

![Visualização do aplicativo Hello World][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Criar um novo projeto do aplicativo Web

1. Inicie o IntelliJ e entre em sua conta do Azure usando as instruções no artigo [Instruções de entrada do Azure para o Kit de Ferramentas do Azure para IntelliJ][intelliJ-sign-in-instructions].

1. Clique menu **Arquivo**, clique em **Novo** e em **Projeto**.
   
   ![Arquivo Novo Projeto][02]

2. Na caixa de diálogo **Novo Projeto**, selecione **Java**, **Aplicativo Web** e clique em **Avançar** para adicionar um SDK do Projeto.
   
   ![Caixa de diálogo Novo Projeto][03a]
   
3. Na caixa de diálogo Selecionar o Diretório Base para o JDK, selecione a pasta onde o JDK está instalado e clique **OK**. Clique em **Avançar** na caixa de diálogo Novo Projeto para continuar.
   
   ![Especificar o diretório base do JDK][03b]

4. Para a finalidade deste tutorial, nomeie o projeto como **Java-Web-App-On-Azure** e clique em **Concluir**.
   
   ![Caixa de diálogo Novo Projeto][04]

5. Na exibição do Explorador de Projetos do IntelliJ, expanda **Java-Web-App-On-Azure**, expanda **Web** e clique duas vezes em **index.jsp**.
   
   ![Abrir Índice de Página][05c]

6. Quando o arquivo index.jsp for aberto no IntelliJ, adicione o texto para exibir dinamicamente **Hello World!** dentro do elemento existente `<body>`. Seu conteúdo do `<body>` atualizado deve ser parecido com o exemplo a seguir:
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. Salve o index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Implante seu aplicativo Web no Azure

Há várias maneiras pelas quais você pode implantar um aplicativo Web Java no Azure. Este tutorial descreve uma das mais simples: o aplicativo será implantado em um contêiner de aplicativos Web do Azure, e não há a necessidade de qualquer tipo de projeto especial nem de ferramentas adicionais. O JDK e o software do contêiner da Web serão fornecidos a você pelo Azure, portanto, não é necessário carregar seu próprio; tudo o que você precisa é de seu aplicativo Web Java. Como resultado, o processo de publicação de seu aplicativo demorará segundos, e não minutos.

Antes de publicar seu aplicativo, você precisa definir as configurações de módulo. Para fazer isso, execute as seguintes etapas:

1. No Explorador de Projetos do IntelliJ, clique com o botão direito do mouse no projeto **Java-Web-App-On-Azure** . Quando o menu de contexto for exibido, clique em **Abrir Configurações do Módulo**.

   ![Abrir configurações do módulo][05a]

2. Quando a caixa de diálogo Estrutura do Projeto aparece:

   a. Clique em **Artefatos** na lista de **Configurações do Projeto**.

   b. Altere o nome do artefato na caixa **Nome** de modo que ele não contenha caracteres especiais ou espaços em branco. Isso é necessário porque o nome será usado no URI (Uniform Resource Identifier).

   c. Altere o **Tipo** para **Aplicativo Web: arquivo**.

   d. Clique em **OK** para fechar a caixa de diálogo Estrutura de Projeto.

   ![Abrir configurações do módulo][05b]

Quando você tiver definido suas configurações de módulo, poderá publicar seu aplicativo no Azure usando as seguintes etapas:

1. No Explorador de Projetos do IntelliJ, clique com o botão direito do mouse no projeto **Java-Web-App-On-Azure** . Quando o menu de contexto for exibido, selecione **Azure** e clique em **Publicar como Aplicativo Web do Azure...**
   
   ![Menu de Contexto de Publicação do Azure][06]

2. Se você ainda não tiver entrado no Azure pelo IntelliJ, será solicitada a entrada em sua conta do Azure. (Se você tiver várias contas do Azure, alguns dos avisos mostrados durante o processo de entrada poderão ser exibidos mais de uma vez, mesmo se forem aparentemente os mesmos. Quando isso acontecer, continue seguindo as instruções de entrada.)
   
   ![Caixa de diálogo Login do Azure][07]

3. Após a conexão bem-sucedida em sua conta do Azure, a caixa de diálogo **Gerenciar Assinaturas** exibirá uma lista de assinaturas associadas às suas credenciais. (Se houver várias assinaturas listadas e você quiser trabalhar com apenas um subconjunto específico, será possível desmarcar as que não deseja usar.) Depois de selecionar suas assinaturas, clique em **Fechar**.
   
   ![Gerenciar Assinaturas][08]

4. Quando a caixa de diálogo **Implantar no Contêiner do Aplicativo Web do Azure** for mostrada, ela exibirá todos os contêineres do Aplicativo Web criados anteriormente por você; se você não tiver criado nenhum contêiner, a lista estará vazia.
   
   ![Contêineres de Aplicativo][09]

5. Se você nunca tiver criado um contêiner de aplicativos Web do Azure, ou se quiser publicar seu aplicativo em um novo contêiner, use as etapas a seguir. Caso contrário, selecione um Contêiner de Aplicativo Web existente e pule para a etapa 6 abaixo.
   
   a. Clique no sinal **+**.
      
      ![Adicionar Contêiner de Aplicativo][10]

   b. A caixa de diálogo **Novo Contêiner de Aplicativo Web** será exibida e será usada nas próximas etapas.
      
      ![Novo Contêiner de Aplicativo][11a]
   
   c. Insira um **Rótulo DNS** para seu Contêiner do Aplicativo Web; isso formará o rótulo DNS folha da URL do host de seu aplicativo Web no Azure. Observe que o nome deve estar disponível e de acordo com os requisitos de nomenclatura de aplicativo Web do Azure.

   d. No menu suspenso **Contêiner da Web** , selecione o software apropriado ao seu aplicativo.
      
      No momento, você pode escolher entre o Tomcat 8, Tomcat 7 ou Jetty 9. Uma distribuição recente do software selecionado será fornecida pelo Azure e ele será executado em uma distribuição recente do JDK 8 criado pela Oracle e fornecido pelo Azure.

   e. No menu suspenso **Assinatura** , selecione a assinatura que deseja usar para essa implantação.

   f. No menu suspenso **Grupo de Recursos** , selecione o Grupo de Recursos com o qual deseja associar seu Aplicativo Web. (Os Grupos de Recursos do Azure lhe permitem agrupar recursos relacionados para que, por exemplo, possam ser excluídos juntos.)
      
      Você pode selecionar um Grupo de Recursos existente (se houver) e ignorar a etapa g abaixo ou usar as seguintes etapas para criar um novo Grupo de Recursos:
      
      * Selecione **&lt;&lt; Criar novo grupo de recursos &gt;&gt;** no menu suspenso **Grupo de recursos**.
      * A caixa de diálogo **Novo Grupo de Recursos** será exibida:
        
         ![Novo grupo de recursos][12]

      * Na caixa de texto **Nome**, especifique um nome para o novo Grupo de Recursos.
      * No menu suspenso **Região**, selecione a localização do data center do Azure apropriada ao Grupo de Recursos.
      * Clique em **OK**.

   g. O menu suspenso **Plano do Serviço de Aplicativo** lista os planos do serviço de aplicativo associados ao Grupo de Recursos selecionado. (Um Plano do Serviço de Aplicativo especifica informações como o local de seu Aplicativo Web, o tipo de preço e o tamanho da instância de computação. Um único Plano do Serviço de Aplicativo pode ser usado para vários Aplicativos Web, por isso, ele é mantido separadamente de uma implantação de Aplicativo Web específica.)
      
      Você pode selecionar um Plano do Serviço de Aplicativo existente (se houver) e ignorar a etapa h abaixo ou usar as seguintes etapas para criar um novo Plano do Serviço de Aplicativo:
      
      * Selecione **&lt;&lt; Criar novo plano do Serviço de Aplicativo &gt;&gt;** no menu suspenso **Plano do Serviço de Aplicativo**.
      * A caixa de diálogo **Novo Plano do Serviço de Aplicativo** será exibida:
        
         ![Novo Plano do Serviço de Aplicativo][13]

      * Na caixa de texto **Nome**, especifique um nome para o novo Plano do Serviço de Aplicativo.
      * No menu suspenso **Localização**, selecione a localização do data center do Azure apropriada ao plano.
      * No menu suspenso **Tipo de Preço**, selecione o preço apropriado ao plano. Para fins de teste, é possível escolher **Gratuito**.
      * No menu suspenso **Tamanho da Instância**, selecione o tamanho de instância apropriado ao plano. Para fins de teste, é possível escolher **Pequeno**.
      * Clique em **OK**.

   h. (Opcional) Por padrão, uma distribuição recente de Java 8 será implantada automaticamente como sua JVM pelo Azure no contêiner do aplicativo Web. No entanto, você pode selecionar uma versão diferente e uma distribuição da JVM. Para fazer isso, execute as seguintes etapas:
      
   * Clique na guia **JDK** na caixa de diálogo **Novo Contêiner do Aplicativo Web**.
   * Você pode escolher entre uma das duas seguintes opções:
        
      * Implantar o JDK padrão, que é oferecido pelo Azure
      * Implantar um JDK de terceiros de uma lista suspensa de JDKs adicionais que estão disponíveis no Azure
      * Implantar um JDK personalizado, que deve ser empacotado como um arquivo ZIP e ser publicamente disponível ou em sua conta de armazenamento do Azure
        
     ![Guia Novo JDK de Contêiner de Aplicativo][11b]

   i. Depois de concluir todas as etapas acima, a caixa de diálogo New Web App Container (Novo Contêiner de Aplicativos Web) deve ser semelhante à ilustração a seguir:
      
      ![Novo Contêiner de Aplicativo][14]
   
   j. Clique em **OK** para concluir a criação do novo contêiner do Aplicativo Web.
       
      Aguarde alguns segundos para a lista de contêineres de Aplicativo Web ser atualizada. O contêiner do aplicativo Web recém-criado agora deve ser selecionado na lista.

6. Agora você está pronto para concluir a implantação inicial do seu aplicativo Web no Azure. Clique em **OK** para implantar seu aplicativo Java no contêiner do aplicativo Web selecionado. Por padrão, o aplicativo será implantado como um subdiretório do servidor de aplicativos. Se desejar implantá-lo como o aplicativo raiz, marque a caixa de seleção **Implantar na raiz** antes de clicar em **OK**.
   
   ![Implantar no Azure][15]

7. Em seguida, você deverá ver o modo de exibição do **Log de Atividades do Azure** , que indicará o status da implantação de seu Aplicativo Web.
   
   ![Indicador de Progresso][16]
   
   O processo de implantação de seu aplicativo Web no Azure deve demorar apenas alguns segundos para ser concluído. Quando seu aplicativo estiver pronto, você verá um link chamado **Publicado** na coluna **Status**. Quando você clicar no link, ele o levará à página inicial do seu aplicativo Web implantado, ou você pode usar as etapas da seção a seguir para navegar até o seu aplicativo Web.

## <a name="browsing-to-your-web-app-on-azure"></a>Navegando até seu aplicativo Web no Azure

Para navegar até o aplicativo Web no Azure, você poderá usar o modo de exibição do **Azure Explorer** .

Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Exibir** no IntelliJ, clicando em **Janelas de Ferramentas** e em **Service Explorer**. Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.

Quando o modo de exibição do **Azure Explorer** for exibido, use estas etapas para navegar pelo aplicativo Web: 

1. Expanda o nó **Azure** .
2. Expanda o nó **Aplicativos Web** . 
3. Clique com botão direito do mouse no Aplicativo Web desejado.
4. Quando o menu de contexto for exibido, clique em **Abrir no Navegador**.
   
   ![Procurar o Aplicativo Web][17]

## <a name="updating-your-web-app"></a>Atualizando seu aplicativo Web

A atualização de um aplicativo Web do Azure em execução é um processo rápido e fácil, e você tem duas opções de atualização:

* Você pode atualizar a implantação de um aplicativo Web Java existente.
* Você pode publicar um aplicativo Java adicional no mesmo contêiner de aplicativo Web.

Em ambos os casos, o processo é idêntico e demora apenas alguns segundos:

1. No explorador de projetos do IntelliJ, clique com o botão direito do mouse no aplicativo Java que você deseja atualizar ou adicionar a um contêiner de aplicativos Web existente.
2. Quando o menu de contexto for exibido, selecione **Azure** e, em seguida, **Publicar como Aplicativo Web do Azure...**
3. Como você já fez logon anteriormente, verá uma lista com seus contêineres de aplicativo Web existentes. Selecione aquele no qual deseja publicar ou publicar novamente o aplicativo Java e clique em **OK**.

Após alguns segundos, o modo de exibição do **Log de Atividades do Azure** mostrará a implantação atualizada como **Publicada** e será possível verificar o aplicativo atualizado em um navegador da Web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Iniciar, parar ou reiniciar o aplicativo Web existente

Para iniciar ou parar um contêiner do Aplicativo Web do Azure existente, (incluindo todos os aplicativos Java implantados nele), é possível usar o modo de exibição do **Azure Explorer** .

Se o modo de exibição do **Azure Explorer** ainda não estiver aberto, você poderá abri-lo clicando no menu **Exibir** no IntelliJ, clicando em **Janelas de Ferramentas** e em **Service Explorer**. Se você não tiver feito logon anteriormente, receberá uma solicitação para fazê-lo.

Quando o modo de exibição do **Azure Explorer** for exibido, siga estas etapas para iniciar ou parar o Aplicativo Web: 

1. Expanda o nó **Azure** .
2. Expanda o nó **Aplicativos Web** . 
3. Clique com botão direito do mouse no Aplicativo Web desejado.
4. Quando o menu de contexto for exibido, clique em **Iniciar**, **Parar** ou **Reiniciar**. Observe que as opções de menu são sensíveis ao contexto, para que você só possa parar um aplicativo Web que esteja em execução ou iniciar um aplicativo Web que não esteja em execução no momento.
   
   ![Parar Aplicativo Web][18]

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
[Updated Version]: azure-toolkit-for-intellij-create-hello-world-web-app.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/18-Stop-Web-App.png
