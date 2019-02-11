---
title: Implantar um aplicativo Web Olá, Mundo sendo executado em um contêiner do Linux na nuvem usando o Azure Toolkit for Eclipse
description: Executar um aplicativo Web Olá, Mundo em um contêiner do Linux e implantá-lo na nuvem usando o Azure Toolkit for Eclipse.
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
ms.openlocfilehash: 799f21a282956f9a88aa35743157fc1292197569
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55649242"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-eclipse"></a>Implantar um aplicativo Web Olá, Mundo em um contêiner do Linux na nuvem usando o Azure Toolkit for Eclipse

Contêineres do [Docker] são um método amplamente usado para implantar aplicativos Web. Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor. O Azure Toolkit for Eclipse simplifica o processo para desenvolvedores de Java adicionando recursos para implantação de contêineres no Microsoft Azure.

Este artigo demonstra as etapas que são necessárias para criar um aplicativo Web Olá, Mundo básico e publicar seu aplicativo Web em um contêiner do Linux no Azure usando o Azure Toolkit for Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]
* Um cliente do [Docker].

> [!NOTE]
>
> Para concluir as etapas neste tutorial, você precisa configurar o [Docker] para expor o daemon na porta 2375 sem TLS. Você pode definir essa configuração ao instalar o Docker ou por meio do menu de configurações do Docker.
>
> ![Menu de configurações do Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Criar um novo projeto do aplicativo Web

1. Inicie o Eclipse e entre em sua conta do Azure usando as etapas no artigo [Instruções de entrada para o Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).

1. Clique em **Arquivo**, **Novo** e clique em **Projeto Web dinâmico**.
   
   ![Criar um novo projeto][file-new-project]

1. Na caixa de diálogo **Novo projeto Web dinâmico**, especifique um nome de projeto e local e, em seguida, clique em **Concluir**.
   
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

1. Após ter adicionado o suporte do Docker, clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Publicar no Aplicativo Web para Contêineres**.

   ![Publicar no Aplicativo Web para Contêineres][run-on-web-app-for-containers]

1. Quando a caixa de diálogo **Executar no Aplicativo Web para Contêineres** for exibida, preencha as informações necessárias:

   * **Arquivo do Docker**: especifica o caminho para o arquivo do Docker que foi criado quando você adicionou o suporte do Docker ao seu projeto. 

   * **Registro de Contêiner**: escolha o registro de contêiner no menu suspenso que você criou na seção anterior deste artigo. Os campos para **URL do servidor**, **Nome de usuário**, e **Senha** serão preenchidos automaticamente.

   * **Imagem e marca**: especifica o nome da imagem de contêiner. Geralmente usará a sintaxe a seguir: “*registry*.azurecr.io/*appname*:latest”, em que: 
      * *registry* é o registro de contêiner da seção anterior deste artigo 
      * *appname* é o nome do seu aplicativo Web 

   * **Aplicativo Web para Contêineres**: escolha **Usar existente** ou **Criar novo** para especificar se você implantará o contêiner em um aplicativo Web existente ou criará um novo aplicativo Web.  O **Nome do aplicativo** especificado criará a URL do aplicativo Web, por exemplo: *wingtiptoys.azurewebsites.net*.

   * **Grupo de Recursos**: especifica se você criará um novo grupo de recursos ou usará um existente. 

   * **Plano do Serviço de Aplicativo**: especifica se você criará um novo plano de serviço de aplicativo ou usará um existente. 

   ![Executar no Aplicativo Web para Contêineres][run-on-web-app-linux]

1. Quando terminar de definir as configurações listadas acima, clique em **OK** para publicar seu aplicativo Web no Azure.

1. Depois que seu aplicativo Web tiver sido publicado, você pode navegar até a URL especificada anteriormente para seu aplicativo Web; por exemplo: *wingtiptoys.azurewebsites.net*.

   ![Navegar até seu aplicativo Web][browsing-to-web-app]

## <a name="next-steps"></a>Próximas etapas

Para obter recursos adicionais para o Docker, consulte o [site oficial do Docker][Docker].

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Portal do Azure]: https://portal.azure.com/
[Criar um registro de contêiner privado do Docker usando o portal do Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-eclipse-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/file-new-project.png
[project-name]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-linux.png
