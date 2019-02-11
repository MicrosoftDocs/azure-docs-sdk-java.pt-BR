---
title: Implantar um aplicativo Web Olá, Mundo sendo executado em um contêiner do Linux na nuvem usando o Kit de Ferramentas do Azure para IntelliJ
description: Executar um aplicativo Web Olá, Mundo em um contêiner do Linux e implantá-lo na nuvem usando o Kit de Ferramentas do Azure para IntelliJ.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: fdff8dc2bd7a29473314d5c0bc99b7bcda369156
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55648720"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a>Implantar um aplicativo Web Olá, Mundo em um contêiner do Linux na nuvem usando o Kit de Ferramentas do Azure para IntelliJ

Contêineres do [Docker] são um método amplamente usado para implantar aplicativos Web. Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor. O Kit de Ferramentas do Azure para IntelliJ simplifica o processo para desenvolvedores de Java adicionando recursos para implantação de contêineres no Microsoft Azure.

Este artigo demonstra as etapas que são necessárias para criar um aplicativo Web Olá, Mundo básico e publicar seu aplicativo Web em um contêiner do Linux no Azure usando o Kit de Ferramentas do Azure para IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* Um cliente do [Docker].

> [!NOTE]
>
> Para concluir as etapas neste tutorial, você precisa configurar o [Docker] para expor o daemon na porta 2375 sem TLS. Você pode definir essa configuração ao instalar o Docker ou por meio do menu de configurações do Docker.
>
> ![Menu de configurações do Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Criar um novo projeto do aplicativo Web

1. Inicie o IntelliJ e entre em sua conta do Azure usando as etapas no artigo [Instruções de entrada para o Kit de Ferramentas do Azure para IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions).

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

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Criar um Registro de Contêiner do Azure para usar como um registro do Docker privado

As etapas a seguir orientam você no uso do portal do Azure para criar um Registro de contêiner do Azure.

> [!NOTE]
>
> Se você quiser usar a CLI do Azure, em vez do Portal do Azure, siga as etapas em [Criar um registro de contêiner do Docker privado usando a CLI do Azure 2.0][Create Docker Registry using Azure CLI].
>

1. Navegue até o [portal do Azure] e conecte-se.

   Depois de entrar em sua conta no portal do Azure, você pode seguir as etapas no artigo [Criar um registro de contêiner privado do Docker usando o portal do Azure], que foram parafraseadas nas etapas a seguir para fins de conveniência.

1. Clique no ícone do menu para **+ Criara um recurso** e, em seguida, clique em **Contêineres** e em **Registro de Contêiner**.
   
   ![Criar um novo Registro de Contêiner do Azure][create-container-registry-01]

1. Quando a página **Criar registro de contêiner** for exibida, insira seu **Nome do registro** e **Grupo de recursos**, escolha **Habilitar** para o **Usuário administrador** e clique em **Criar**.

   ![Definir configurações do registro de contêiner do Azure][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Implante seu aplicativo Web em um contêiner do Docker

1. Clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Adicionar suporte do Docker**.

   Isso criará automaticamente um arquivo do Docker com uma configuração padrão.

   ![Adicionar suporte ao Docker][add-docker-support]

1. Após ter adicionado o suporte do Docker, clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Executar no Aplicativo Web para Contêineres**.

   ![Executar no Aplicativo Web para Contêineres][run-on-web-app-for-containers]

1. Quando a caixa de diálogo **Executar no Aplicativo Web para Contêineres** for exibida, preencha as informações necessárias:

   * **Nome**: especifica o nome amigável que é exibido no Azure Toolkit. 

   * **Registro de Contêiner**: escolha o registro de contêiner no menu suspenso que você criou na seção anterior deste artigo. Os campos para **URL do servidor**, **Nome de usuário**, e **Senha** serão preenchidos automaticamente.

   * **Imagem e marca**: especifica o nome da imagem de contêiner. Geralmente usará a sintaxe a seguir: “*registry*.azurecr.io/*appname*:latest”, em que: 
      * *registry* é o registro de contêiner da seção anterior deste artigo 
      * *appname* é o nome do seu aplicativo Web 

   * **Usar o aplicativo Web existente** ou **Criar novo aplicativo Web**: especifica se você implantará o contêiner em um aplicativo Web existente ou criará um novo aplicativo Web. O **Nome do aplicativo** especificado criará a URL do aplicativo Web, por exemplo: *wingtiptoys.azurewebsites.net*.

   * **Grupo de Recursos**: especifica se você criará um novo grupo de recursos ou usará um existente. 

   * **Plano do Serviço de Aplicativo**: especifica se você criará um novo plano de serviço de aplicativo ou usará um existente. 

   ![Executar no Aplicativo Web para Contêineres][run-on-web-app-linux]

1. Quando terminar de definir as configurações listadas acima, clique em **Executar**. Quando seu aplicativo Web tiver sido implantado com êxito, o status será exibido na janela **Executar**.

   ![Aplicativo Web implantado com êxito][successfully-deployed]

1. Depois que seu aplicativo Web tiver sido publicado, você pode navegar até a URL especificada anteriormente para seu aplicativo Web; por exemplo: *wingtiptoys.azurewebsites.net*.

   ![Navegar até seu aplicativo Web][browsing-to-web-app]

## <a name="optional-modify-your-web-app-publish-settings"></a>Opcional: Modificar configurações de publicação do aplicativo Web

1. Depois de publicar seu aplicativo Web, as configurações serão salvas como padrão e você poderá executar seu aplicativo no Azure clicando no ícone de seta verde na barra de ferramentas. Você pode modificar essas configurações clicando no menu suspenso para seu aplicativo Web e clicando em **Editar Configurações**.

   ![Menu Editar configuração][edit-configuration-menu]

1. Quando a caixa de diálogo **Configurações de execução/depuração** for exibida, você poderá modificar as configurações padrão e, em seguida, clicar em **OK**.

   ![Caixa de diálogo Editar configuração][edit-configuration-dialog]

## <a name="next-steps"></a>Próximas etapas

Para obter recursos adicionais para o Docker, consulte o [site oficial do Docker][Docker].

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Portal do Azure]: https://portal.azure.com/
[Criar um registro de contêiner privado do Docker usando o portal do Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-intellij-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
