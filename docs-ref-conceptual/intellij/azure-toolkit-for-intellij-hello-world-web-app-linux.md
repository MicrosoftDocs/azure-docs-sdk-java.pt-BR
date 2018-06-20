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
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: d281f37b027d4011ea2e3106990c5e45b69ebc88
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33887089"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="097aa-103">Implantar um aplicativo Web Olá, Mundo em um contêiner do Linux na nuvem usando o Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="097aa-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="097aa-104">Contêineres do [Docker] são um método amplamente usado para implantar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="097aa-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="097aa-105">Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor.</span><span class="sxs-lookup"><span data-stu-id="097aa-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="097aa-106">O Kit de Ferramentas do Azure para IntelliJ simplifica o processo para desenvolvedores de Java adicionando recursos para implantação de contêineres no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="097aa-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="097aa-107">Este artigo demonstra as etapas que são necessárias para criar um aplicativo Web Olá, Mundo básico e publicar seu aplicativo Web em um contêiner do Linux no Azure usando o Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="097aa-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="097aa-108">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="097aa-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="097aa-109">Para concluir as etapas neste tutorial, você precisa configurar o [Docker] para expor o daemon na porta 2375 sem TLS.</span><span class="sxs-lookup"><span data-stu-id="097aa-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="097aa-110">Você pode definir essa configuração ao instalar o Docker ou por meio do menu de configurações do Docker.</span><span class="sxs-lookup"><span data-stu-id="097aa-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Menu de configurações do Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="097aa-112">Criar um novo projeto do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="097aa-112">Create a new web app project</span></span>

1. <span data-ttu-id="097aa-113">Inicie o IntelliJ e entre em sua conta do Azure usando as etapas no artigo [Instruções de entrada para o Kit de Ferramentas do Azure para IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="097aa-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="097aa-114">Clique menu **Arquivo**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="097aa-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Criar um novo projeto][file-new-project]

1. <span data-ttu-id="097aa-116">Na caixa de diálogo **Novo Projeto**, selecione **Maven**, em seguida, **maven-archetype-webapp** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="097aa-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Escolha o aplicativo Web do modelo Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="097aa-118">Especifique o **GroupId** e **ArtifactId** para seu aplicativo Web e depois clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="097aa-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Especifique GroupId e ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="097aa-120">Personalize as configurações de Maven ou aceite os padrões e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="097aa-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Especifique as configurações de Maven][maven-options]

1. <span data-ttu-id="097aa-122">Especifique um nome de projeto e local e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="097aa-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Especifique o nome do projeto][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="097aa-124">Criar um Registro de Contêiner do Azure para usar como um registro do Docker privado</span><span class="sxs-lookup"><span data-stu-id="097aa-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="097aa-125">As etapas a seguir orientam você no uso do portal do Azure para criar um Registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="097aa-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="097aa-126">Se você quiser usar a CLI do Azure, em vez do Portal do Azure, siga as etapas em [Criar um registro de contêiner do Docker privado usando a CLI do Azure 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="097aa-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="097aa-127">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="097aa-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="097aa-128">Depois de entrar em sua conta no portal do Azure, você pode seguir as etapas no artigo [Criar um registro de contêiner privado do Docker usando o portal do Azure], que foram parafraseadas nas etapas a seguir para fins de conveniência.</span><span class="sxs-lookup"><span data-stu-id="097aa-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="097aa-129">Clique no ícone do menu para **+ Novo** e, em seguida, clique em **Contêineres** e em **Registro de Contêiner do Azure**.</span><span class="sxs-lookup"><span data-stu-id="097aa-129">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Criar um novo Registro de Contêiner do Azure][AR01]

1. <span data-ttu-id="097aa-131">Quando a página de informações para o modelo de Registro de Contêiner do Azure for exibida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="097aa-131">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Criar um novo Registro de Contêiner do Azure][AR02]

1. <span data-ttu-id="097aa-133">Quando a página **Criar registro de contêiner** for exibida, insira seu **Nome do registro** e **Grupo de recursos**, escolha **Habilitar** para o **Usuário administrador** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="097aa-133">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Definir configurações do registro de contêiner do Azure][AR03]

1. <span data-ttu-id="097aa-135">Quando o registro de contêiner tiver sido criado, navegue até o registro de contêiner no portal do Azure e, em seguida, clique em **Chaves de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="097aa-135">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="097aa-136">Anote o nome de usuário e a senha para as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="097aa-136">Take note of the username and password for the next steps.</span></span>

   ![Chaves de acesso do Registro de Contêiner do Azure][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="097aa-138">Implante seu aplicativo Web em um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="097aa-138">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="097aa-139">Clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Adicionar suporte do Docker**.</span><span class="sxs-lookup"><span data-stu-id="097aa-139">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="097aa-140">Isso criará automaticamente um arquivo do Docker com uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="097aa-140">This will automatically create a Docker file with a default configuration.</span></span>

   ![Adicionar suporte ao Docker][add-docker-support]

1. <span data-ttu-id="097aa-142">Após ter adicionado o suporte do Docker, clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Executar no aplicativo Web (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="097aa-142">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App (Linux)**.</span></span>

   ![Executar no aplicativo Web (Linux)][run-on-web-app-linux]

1. <span data-ttu-id="097aa-144">Quando a caixa de diálogo **Executar no aplicativo Web (Linux)** for exibida, preencha as informações necessárias:</span><span class="sxs-lookup"><span data-stu-id="097aa-144">When the **Run on Web App (Linux)** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="097aa-145">**Nome**: especifica o nome amigável que é exibido no Kit de Ferramentas do Azure.</span><span class="sxs-lookup"><span data-stu-id="097aa-145">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="097aa-146">**URL do servidor**: especifica a URL para o registro de contêiner da seção anterior deste artigo. Geralmente usará a sintaxe a seguir: "*registry*.azurecr.io".</span><span class="sxs-lookup"><span data-stu-id="097aa-146">**Server URL**: This specifies the URL for your container registry from the previous section of this article; typically this will use the following syntax: "*registry*.azurecr.io".</span></span> 

   * <span data-ttu-id="097aa-147">**Nome de usuário** e **senha**: especifica as chaves de acesso para o registro de contêiner da seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="097aa-147">**Username** and **Password**: Specifies the access keys for your container registry from the previous section of this article.</span></span> 

   * <span data-ttu-id="097aa-148">**Imagem e marca**: especifica o nome da imagem de contêiner. Geralmente usará a sintaxe a seguir: "*registry*.azurecr.io/*appname*:latest", em que:</span><span class="sxs-lookup"><span data-stu-id="097aa-148">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="097aa-149">*registry* é o registro de contêiner da seção anterior deste artigo</span><span class="sxs-lookup"><span data-stu-id="097aa-149">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="097aa-150">*appname* é o nome do seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="097aa-150">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="097aa-151">**Usar aplicativo Web existente** ou **Criar novo aplicativo Web**: especifica se você implantará o contêiner em um aplicativo Web existente ou criará um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="097aa-151">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> 

   * <span data-ttu-id="097aa-152">**Grupo de recursos**: especifica se você criará um novo grupo de recursos ou usará um existente.</span><span class="sxs-lookup"><span data-stu-id="097aa-152">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="097aa-153">**Plano do Serviço de Aplicativo**: especifica se você criará um novo plano de serviço de aplicativo ou usará um existente.</span><span class="sxs-lookup"><span data-stu-id="097aa-153">**App Service Plan**: Specifies whether you willuse an existing or create a new app service plan.</span></span> 

1. <span data-ttu-id="097aa-154">Quando terminar de definir as configurações listadas acima, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="097aa-154">When you have finished configuring the settings listed above, click **Run**.</span></span>

   ![Criar um aplicativo Web][create-web-app]

1. <span data-ttu-id="097aa-156">Depois de publicar seu aplicativo Web, as configurações serão salvas como padrão e você poderá executar seu aplicativo no Azure clicando no ícone de seta verde na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="097aa-156">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="097aa-157">Você pode modificar essas configurações clicando no menu suspenso para seu aplicativo Web e clicando em **Editar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="097aa-157">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menu Editar configuração][edit-configuration-menu]

1. <span data-ttu-id="097aa-159">Quando a caixa de diálogo **Configurações de execução/depuração** for exibida, você poderá modificar as configurações padrão e, em seguida, clicar em **OK**.</span><span class="sxs-lookup"><span data-stu-id="097aa-159">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Caixa de diálogo Editar configuração][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="097aa-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="097aa-161">Next steps</span></span>

<span data-ttu-id="097aa-162">Para obter recursos adicionais para o Docker, consulte o [site oficial do Docker][Docker].</span><span class="sxs-lookup"><span data-stu-id="097aa-162">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[portal do Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Criar um registro de contêiner privado do Docker usando o portal do Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
