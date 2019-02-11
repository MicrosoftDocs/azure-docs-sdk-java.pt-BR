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
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="300cb-103">Implantar um aplicativo Web Olá, Mundo em um contêiner do Linux na nuvem usando o Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="300cb-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="300cb-104">Contêineres do [Docker] são um método amplamente usado para implantar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="300cb-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="300cb-105">Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor.</span><span class="sxs-lookup"><span data-stu-id="300cb-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="300cb-106">O Azure Toolkit for Eclipse simplifica o processo para desenvolvedores de Java adicionando recursos para implantação de contêineres no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="300cb-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="300cb-107">Este artigo demonstra as etapas que são necessárias para criar um aplicativo Web Olá, Mundo básico e publicar seu aplicativo Web em um contêiner do Linux no Azure usando o Azure Toolkit for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="300cb-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]
* <span data-ttu-id="300cb-108">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="300cb-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="300cb-109">Para concluir as etapas neste tutorial, você precisa configurar o [Docker] para expor o daemon na porta 2375 sem TLS.</span><span class="sxs-lookup"><span data-stu-id="300cb-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="300cb-110">Você pode definir essa configuração ao instalar o Docker ou por meio do menu de configurações do Docker.</span><span class="sxs-lookup"><span data-stu-id="300cb-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Menu de configurações do Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="300cb-112">Criar um novo projeto do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="300cb-112">Create a new web app project</span></span>

1. <span data-ttu-id="300cb-113">Inicie o Eclipse e entre em sua conta do Azure usando as etapas no artigo [Instruções de entrada para o Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="300cb-113">Start Eclipse and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="300cb-114">Clique em **Arquivo**, **Novo** e clique em **Projeto Web dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="300cb-114">Click the **File** menu, then click **New**, and then click **Dynamic Web Project**.</span></span>
   
   ![Criar um novo projeto][file-new-project]

1. <span data-ttu-id="300cb-116">Na caixa de diálogo **Novo projeto Web dinâmico**, especifique um nome de projeto e local e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="300cb-116">In the **New Dynamic Web Project** dialog box, specify your project name and location, and then click **Finish**.</span></span>
   
   ![Especifique o nome do projeto][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="300cb-118">Criar um Registro de Contêiner do Azure para usar como um registro do Docker privado</span><span class="sxs-lookup"><span data-stu-id="300cb-118">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="300cb-119">As etapas a seguir orientam você no uso do portal do Azure para criar um Registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="300cb-119">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="300cb-120">Se você quiser usar a CLI do Azure, em vez do Portal do Azure, siga as etapas em [Criar um registro de contêiner do Docker privado usando a CLI do Azure 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="300cb-120">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="300cb-121">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="300cb-121">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="300cb-122">Depois de entrar em sua conta no portal do Azure, você pode seguir as etapas no artigo [Criar um registro de contêiner privado do Docker usando o portal do Azure], que foram parafraseadas nas etapas a seguir para fins de conveniência.</span><span class="sxs-lookup"><span data-stu-id="300cb-122">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="300cb-123">Clique no ícone do menu para **+ Criara um recurso** e, em seguida, clique em **Contêineres** e em **Registro de Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="300cb-123">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![Criar um novo Registro de Contêiner do Azure][create-container-registry-01]

1. <span data-ttu-id="300cb-125">Quando a página **Criar registro de contêiner** for exibida, insira seu **Nome do registro** e **Grupo de recursos**, escolha **Habilitar** para o **Usuário administrador** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="300cb-125">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Definir configurações do registro de contêiner do Azure][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="300cb-127">Implante seu aplicativo Web em um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="300cb-127">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="300cb-128">Clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Adicionar suporte do Docker**.</span><span class="sxs-lookup"><span data-stu-id="300cb-128">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="300cb-129">Isso criará automaticamente um arquivo do Docker com uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="300cb-129">This will automatically create a Docker file with a default configuration.</span></span>

   ![Adicionar suporte ao Docker][add-docker-support]

1. <span data-ttu-id="300cb-131">Após ter adicionado o suporte do Docker, clique com o botão direito do mouse no seu projeto no explorador de projeto, escolha **Azure** e, em seguida, clique em **Publicar no Aplicativo Web para Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="300cb-131">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Publish to Web App for Containers**.</span></span>

   ![Publicar no Aplicativo Web para Contêineres][run-on-web-app-for-containers]

1. <span data-ttu-id="300cb-133">Quando a caixa de diálogo **Executar no Aplicativo Web para Contêineres** for exibida, preencha as informações necessárias:</span><span class="sxs-lookup"><span data-stu-id="300cb-133">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="300cb-134">**Arquivo do Docker**: especifica o caminho para o arquivo do Docker que foi criado quando você adicionou o suporte do Docker ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="300cb-134">**Docker File**: This specifies the path to the Docker file that was created when you added Docker support to your project.</span></span> 

   * <span data-ttu-id="300cb-135">**Registro de Contêiner**: escolha o registro de contêiner no menu suspenso que você criou na seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="300cb-135">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="300cb-136">Os campos para **URL do servidor**, **Nome de usuário**, e **Senha** serão preenchidos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="300cb-136">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="300cb-137">**Imagem e marca**: especifica o nome da imagem de contêiner. Geralmente usará a sintaxe a seguir: “*registry*.azurecr.io/*appname*:latest”, em que:</span><span class="sxs-lookup"><span data-stu-id="300cb-137">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="300cb-138">*registry* é o registro de contêiner da seção anterior deste artigo</span><span class="sxs-lookup"><span data-stu-id="300cb-138">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="300cb-139">*appname* é o nome do seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="300cb-139">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="300cb-140">**Aplicativo Web para Contêineres**: escolha **Usar existente** ou **Criar novo** para especificar se você implantará o contêiner em um aplicativo Web existente ou criará um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="300cb-140">**Web App for Container**: Choose **Use Existing** or **Create New** to specify whether you will deploy your container to an existing web app or create a new web app.</span></span>  <span data-ttu-id="300cb-141">O **Nome do aplicativo** especificado criará a URL do aplicativo Web, por exemplo: *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="300cb-141">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="300cb-142">**Grupo de Recursos**: especifica se você criará um novo grupo de recursos ou usará um existente.</span><span class="sxs-lookup"><span data-stu-id="300cb-142">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="300cb-143">**Plano do Serviço de Aplicativo**: especifica se você criará um novo plano de serviço de aplicativo ou usará um existente.</span><span class="sxs-lookup"><span data-stu-id="300cb-143">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Executar no Aplicativo Web para Contêineres][run-on-web-app-linux]

1. <span data-ttu-id="300cb-145">Quando terminar de definir as configurações listadas acima, clique em **OK** para publicar seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="300cb-145">When you have finished configuring the settings listed above, click **OK** to publish your web app to Azure.</span></span>

1. <span data-ttu-id="300cb-146">Depois que seu aplicativo Web tiver sido publicado, você pode navegar até a URL especificada anteriormente para seu aplicativo Web; por exemplo: *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="300cb-146">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![Navegar até seu aplicativo Web][browsing-to-web-app]

## <a name="next-steps"></a><span data-ttu-id="300cb-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="300cb-148">Next steps</span></span>

<span data-ttu-id="300cb-149">Para obter recursos adicionais para o Docker, consulte o [site oficial do Docker][Docker].</span><span class="sxs-lookup"><span data-stu-id="300cb-149">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

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

[add-docker-support]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-eclipse-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/file-new-project.png
[project-name]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-linux.png
