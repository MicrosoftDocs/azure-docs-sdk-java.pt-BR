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
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="e5f03-103">Implantar um aplicativo Web Olá, Mundo em um contêiner do Linux na nuvem usando o Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="e5f03-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="e5f03-104">Contêineres do [Docker] são um método amplamente usado para implantar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="e5f03-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="e5f03-105">Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor.</span><span class="sxs-lookup"><span data-stu-id="e5f03-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="e5f03-106">O Kit de Ferramentas do Azure para IntelliJ simplifica o processo para desenvolvedores de Java adicionando recursos para implantação de contêineres no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e5f03-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="e5f03-107">Este artigo demonstra as etapas que são necessárias para criar um aplicativo Web Olá, Mundo básico e publicar seu aplicativo Web em um contêiner do Linux no Azure usando o Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e5f03-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="e5f03-108">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="e5f03-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e5f03-109">Para concluir as etapas neste tutorial, você precisa configurar o [Docker] para expor o daemon na porta 2375 sem TLS.</span><span class="sxs-lookup"><span data-stu-id="e5f03-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="e5f03-110">Você pode definir essa configuração ao instalar o Docker ou por meio do menu de configurações do Docker.</span><span class="sxs-lookup"><span data-stu-id="e5f03-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Menu de configurações do Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="e5f03-112">Criar um novo projeto do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e5f03-112">Create a new web app project</span></span>

1. <span data-ttu-id="e5f03-113">Inicie o IntelliJ e entre em sua conta do Azure usando as etapas no artigo [Instruções de entrada para o Kit de Ferramentas do Azure para IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="e5f03-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="e5f03-114">Clique menu **Arquivo**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Criar um novo projeto][file-new-project]

1. <span data-ttu-id="e5f03-116">Na caixa de diálogo **Novo Projeto**, selecione **Maven**, em seguida, **maven-archetype-webapp** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Escolha o aplicativo Web do modelo Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="e5f03-118">Especifique o **GroupId** e **ArtifactId** para seu aplicativo Web e depois clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Especifique GroupId e ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="e5f03-120">Personalize as configurações de Maven ou aceite os padrões e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Especifique as configurações de Maven][maven-options]

1. <span data-ttu-id="e5f03-122">Especifique um nome de projeto e local e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Especifique o nome do projeto][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="e5f03-124">Criar um Registro de Contêiner do Azure para usar como um registro do Docker privado</span><span class="sxs-lookup"><span data-stu-id="e5f03-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="e5f03-125">As etapas a seguir orientam você no uso do portal do Azure para criar um Registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5f03-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e5f03-126">Se você quiser usar a CLI do Azure, em vez do Portal do Azure, siga as etapas em [Criar um registro de contêiner do Docker privado usando a CLI do Azure 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="e5f03-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="e5f03-127">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="e5f03-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="e5f03-128">Depois de entrar em sua conta no portal do Azure, você pode seguir as etapas no artigo [Criar um registro de contêiner privado do Docker usando o portal do Azure], que foram parafraseadas nas etapas a seguir para fins de conveniência.</span><span class="sxs-lookup"><span data-stu-id="e5f03-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="e5f03-129">Clique no ícone do menu para **+ Criara um recurso** e, em seguida, clique em **Contêineres** e em **Registro de Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-129">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![Criar um novo Registro de Contêiner do Azure][create-container-registry-01]

1. <span data-ttu-id="e5f03-131">Quando a página **Criar registro de contêiner** for exibida, insira seu **Nome do registro** e **Grupo de recursos**, escolha **Habilitar** para o **Usuário administrador** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-131">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Definir configurações do registro de contêiner do Azure][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="e5f03-133">Implante seu aplicativo Web em um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="e5f03-133">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="e5f03-134">Clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Adicionar suporte do Docker**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-134">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="e5f03-135">Isso criará automaticamente um arquivo do Docker com uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="e5f03-135">This will automatically create a Docker file with a default configuration.</span></span>

   ![Adicionar suporte ao Docker][add-docker-support]

1. <span data-ttu-id="e5f03-137">Após ter adicionado o suporte do Docker, clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Executar no Aplicativo Web para Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-137">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App for Containers**.</span></span>

   ![Executar no Aplicativo Web para Contêineres][run-on-web-app-for-containers]

1. <span data-ttu-id="e5f03-139">Quando a caixa de diálogo **Executar no Aplicativo Web para Contêineres** for exibida, preencha as informações necessárias:</span><span class="sxs-lookup"><span data-stu-id="e5f03-139">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="e5f03-140">**Nome**: especifica o nome amigável que é exibido no Azure Toolkit.</span><span class="sxs-lookup"><span data-stu-id="e5f03-140">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="e5f03-141">**Registro de Contêiner**: escolha o registro de contêiner no menu suspenso que você criou na seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="e5f03-141">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="e5f03-142">Os campos para **URL do servidor**, **Nome de usuário**, e **Senha** serão preenchidos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e5f03-142">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="e5f03-143">**Imagem e marca**: especifica o nome da imagem de contêiner. Geralmente usará a sintaxe a seguir: “*registry*.azurecr.io/*appname*:latest”, em que:</span><span class="sxs-lookup"><span data-stu-id="e5f03-143">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="e5f03-144">*registry* é o registro de contêiner da seção anterior deste artigo</span><span class="sxs-lookup"><span data-stu-id="e5f03-144">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="e5f03-145">*appname* é o nome do seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e5f03-145">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="e5f03-146">**Usar o aplicativo Web existente** ou **Criar novo aplicativo Web**: especifica se você implantará o contêiner em um aplicativo Web existente ou criará um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e5f03-146">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> <span data-ttu-id="e5f03-147">O **Nome do aplicativo** especificado criará a URL do aplicativo Web, por exemplo: *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="e5f03-147">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="e5f03-148">**Grupo de Recursos**: especifica se você criará um novo grupo de recursos ou usará um existente.</span><span class="sxs-lookup"><span data-stu-id="e5f03-148">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="e5f03-149">**Plano do Serviço de Aplicativo**: especifica se você criará um novo plano de serviço de aplicativo ou usará um existente.</span><span class="sxs-lookup"><span data-stu-id="e5f03-149">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Executar no Aplicativo Web para Contêineres][run-on-web-app-linux]

1. <span data-ttu-id="e5f03-151">Quando terminar de definir as configurações listadas acima, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-151">When you have finished configuring the settings listed above, click **Run**.</span></span> <span data-ttu-id="e5f03-152">Quando seu aplicativo Web tiver sido implantado com êxito, o status será exibido na janela **Executar**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-152">When your web app has been successfully deployed, the status will be displayed in the **Run** window.</span></span>

   ![Aplicativo Web implantado com êxito][successfully-deployed]

1. <span data-ttu-id="e5f03-154">Depois que seu aplicativo Web tiver sido publicado, você pode navegar até a URL especificada anteriormente para seu aplicativo Web; por exemplo: *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="e5f03-154">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![Navegar até seu aplicativo Web][browsing-to-web-app]

## <a name="optional-modify-your-web-app-publish-settings"></a><span data-ttu-id="e5f03-156">Opcional: Modificar configurações de publicação do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e5f03-156">Optional: Modify your web app publish settings</span></span>

1. <span data-ttu-id="e5f03-157">Depois de publicar seu aplicativo Web, as configurações serão salvas como padrão e você poderá executar seu aplicativo no Azure clicando no ícone de seta verde na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="e5f03-157">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="e5f03-158">Você pode modificar essas configurações clicando no menu suspenso para seu aplicativo Web e clicando em **Editar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-158">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menu Editar configuração][edit-configuration-menu]

1. <span data-ttu-id="e5f03-160">Quando a caixa de diálogo **Configurações de execução/depuração** for exibida, você poderá modificar as configurações padrão e, em seguida, clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5f03-160">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Caixa de diálogo Editar configuração][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="e5f03-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5f03-162">Next steps</span></span>

<span data-ttu-id="e5f03-163">Para obter recursos adicionais para o Docker, consulte o [site oficial do Docker][Docker].</span><span class="sxs-lookup"><span data-stu-id="e5f03-163">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Portal do Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Criar um registro de contêiner privado do Docker usando o portal do Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
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
