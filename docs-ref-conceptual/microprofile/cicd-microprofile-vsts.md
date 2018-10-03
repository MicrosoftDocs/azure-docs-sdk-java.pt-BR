---
title: CI/CD para aplicativos MicroProfile usando o Azure DevOps
description: Saiba como configurar um ciclo de lançamento de CI/CD para implantar um aplicativo MicroProfile em uma instância do Aplicativo Web para Contêineres do Azure usando o Azure DevOps
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: c2b6bf3370982d26d8d23fede370e0105a70b734
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506259"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="771ef-103">CI/CD para aplicativos MicroProfile usando o Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="771ef-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="771ef-104">Este tutorial mostra como os desenvolvedores Java EE podem configurar facilmente um ciclo de lançamento de CI/CD para implantar seus aplicativos [MicroProfile](http://microprofile.io) em um Aplicativo Web para Contêineres usando o Azure DevOps (antes conhecido como VSTS).</span><span class="sxs-lookup"><span data-stu-id="771ef-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="771ef-105">Neste exemplo, usaremos um aplicativo MicroProfile que usa um [Payara Micro](https://www.payara.fish/payara_micro) como uma imagem básica.</span><span class="sxs-lookup"><span data-stu-id="771ef-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="771ef-106">Vamos começar o processo de colocação em contêiner do Azure DevOps criando uma imagem do Docker e enviando a imagem de contêiner para um Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="771ef-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="771ef-107">Em seguida, conclua com um pipeline de lançamento do Azure DevOps para implantar a imagem de contêiner em um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="771ef-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="771ef-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="771ef-108">Prerequisites</span></span>
- <span data-ttu-id="771ef-109">Copiar e salvar a URL Git do [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span><span class="sxs-lookup"><span data-stu-id="771ef-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="771ef-110">Registrar-se ou fazer logon em sua conta do [Azure DevOps](https://dev.azure.com)</span><span class="sxs-lookup"><span data-stu-id="771ef-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="771ef-111">Criar um novo [projeto do Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) e usar a URL Git acima para **importar um repositório**</span><span class="sxs-lookup"><span data-stu-id="771ef-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="771ef-112">Criar um [Registro de Contêiner do Azure](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span><span class="sxs-lookup"><span data-stu-id="771ef-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="771ef-113">Criar um Aplicativo Web para Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="771ef-113">Create an Azure Web App for Container</span></span>
> [!NOTE]
>
> <span data-ttu-id="771ef-114">Selecionar "Início Rápido" nas Configurações do Contêiner ao provisionar a instância do Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="771ef-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="771ef-115">Criar a definição de build</span><span class="sxs-lookup"><span data-stu-id="771ef-115">Create a Build definition</span></span>

<span data-ttu-id="771ef-116">A definição de build no Azure DevOps executa automaticamente todas as tarefas no build sempre que há uma confirmação no aplicativo de origem do Java EE.</span><span class="sxs-lookup"><span data-stu-id="771ef-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="771ef-117">Neste exemplo, o Azure DevOps usará Maven para compilar o projeto MicroProfile em Java.</span><span class="sxs-lookup"><span data-stu-id="771ef-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="771ef-118">Clique na guia "Build e Versão" na parte superior da página do projeto Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="771ef-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="771ef-119">Em seguida, selecione o link **Builds**</span><span class="sxs-lookup"><span data-stu-id="771ef-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="771ef-120">Clique no botão **Novo Pipeline** e em **Continuar** para começar a definir as tarefas de build</span><span class="sxs-lookup"><span data-stu-id="771ef-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="771ef-121">Selecione "Maven" na lista de modelos e clique no botão **Aplicar** para compilar seu projeto Java</span><span class="sxs-lookup"><span data-stu-id="771ef-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="771ef-122">Use o menu suspenso no campo Pool de agentes para selecionar a opção **Versão prévia do Linux Hospedada**.</span><span class="sxs-lookup"><span data-stu-id="771ef-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
> [!NOTE]
>
> <span data-ttu-id="771ef-123">Isso informa ao Azure DevOps sobre qual servidor de build usar.</span><span class="sxs-lookup"><span data-stu-id="771ef-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="771ef-124">Você pode usar seu próprio servidor de build personalizado</span><span class="sxs-lookup"><span data-stu-id="771ef-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="771ef-125">Para configurar o build para a integração contínua, selecione a guia **Gatilhos** e marque a caixa de seleção **Habilitar integração contínua**.</span><span class="sxs-lookup"><span data-stu-id="771ef-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 
 
6. <span data-ttu-id="771ef-126">Selecione a guia **Tarefas** para retornar à página do pipeline de build principal</span><span class="sxs-lookup"><span data-stu-id="771ef-126">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="771ef-127">Use o menu suspenso **Salvar e enfileirar** para selecionar a opção **Salvar**</span><span class="sxs-lookup"><span data-stu-id="771ef-127">Use the **Save & queue** drop-down menu to select the **Save** option</span></span>
 

## <a name="create-a-docker-build-image"></a><span data-ttu-id="771ef-128">Criar uma Imagem de Build do Docker</span><span class="sxs-lookup"><span data-stu-id="771ef-128">Create a Docker Build Image</span></span>

<span data-ttu-id="771ef-129">Nessa tarefa, o Azure DevOps usa um Dockerfile com uma imagem básica do Payara Micro para criar uma imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="771ef-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="771ef-130">Selecione a guia **Tarefas** para retornar à página do pipeline de build principal</span><span class="sxs-lookup"><span data-stu-id="771ef-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="771ef-131">Clique no ícone **+** para adicionar uma nova tarefa à definição de build</span><span class="sxs-lookup"><span data-stu-id="771ef-131">Click on the **+** icon to add new task to the build definition</span></span>
 
<img src="media/VSTS/Tasks-add4.png">
 
3. <span data-ttu-id="771ef-132">Selecione "Docker" na lista de modelos e clique no botão **Adicionar**</span><span class="sxs-lookup"><span data-stu-id="771ef-132">Select "Docker" from the list of templates, then click on the **Add** button</span></span>
4. <span data-ttu-id="771ef-133">Insira um nome descritivo no campo **Nome de exibição**</span><span class="sxs-lookup"><span data-stu-id="771ef-133">Enter a description name for the **Display name** field</span></span>
5. <span data-ttu-id="771ef-134">Verifique se a opção **Registro de Contêiner do Azure** está selecionada no menu suspenso do **Tipo do registro de contêiner**.</span><span class="sxs-lookup"><span data-stu-id="771ef-134">Verify that **Azure Container Registry** is selected in the drop-down menu for **Container registry type**.</span></span>
> [!NOTE]
>
>  <span data-ttu-id="771ef-135">Se você estiver usando o Hub do Docker ou outro registro, selecione "Registro de Contêiner".</span><span class="sxs-lookup"><span data-stu-id="771ef-135">If you are using Docker Hub or another registry, select "Container Registry" instead.</span></span>  <span data-ttu-id="771ef-136">Em seguida, clique no botão "+ Novo" para fornecer as credenciais e as informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="771ef-136">Then click on the "+ New" button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="771ef-137">Vá para a seção Comandos para continuar.</span><span class="sxs-lookup"><span data-stu-id="771ef-137">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="771ef-138">Use o menu suspenso **Assinatura do Azure** para selecionar a ID de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="771ef-138">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="771ef-139">Em seguida, clique no botão **Autorizar**</span><span class="sxs-lookup"><span data-stu-id="771ef-139">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="771ef-140">No menu suspenso **Registro de contêiner do Azure**, selecione o nome de registro criado no Azure.</span><span class="sxs-lookup"><span data-stu-id="771ef-140">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="771ef-141">Verifique se a opção **build** está selecionada no menu suspenso **Comando**.</span><span class="sxs-lookup"><span data-stu-id="771ef-141">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="771ef-142">Para o **Dockerfile**, clique no ícone de navegação do caminho ao lado da caixa de texto para selecionar o Dockerfile no projeto GitHub.</span><span class="sxs-lookup"><span data-stu-id="771ef-142">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="771ef-143">Em seguida, clique no botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="771ef-143">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="771ef-144">No **Nome da imagem**, marque a caixa de seleção **Incluir marca mais recente**.</span><span class="sxs-lookup"><span data-stu-id="771ef-144">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="771ef-145">Use o menu suspenso **Salvar e enfileirar** para selecionar a opção **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="771ef-145">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="771ef-146">Enviar por push a Imagem do Docker para o ACR</span><span class="sxs-lookup"><span data-stu-id="771ef-146">Push Docker Image to ACR</span></span>

<span data-ttu-id="771ef-147">Nessa tarefa, o Azure DevOps enviará por push a imagem do Docker para seu Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="771ef-147">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="771ef-148">Isso será usado para executar o aplicativo de API MicroProfile como um aplicativo Web Java em contêineres.</span><span class="sxs-lookup"><span data-stu-id="771ef-148">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="771ef-149">Como estamos usando o Docker no Azure DevOps, crie um novo modelo de Docker repetindo as etapas 1 a 7 acima na seção **Criar uma Imagem de Build do Docker**.</span><span class="sxs-lookup"><span data-stu-id="771ef-149">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="771ef-150">Selecione **push** no menu suspenso **Comando**.</span><span class="sxs-lookup"><span data-stu-id="771ef-150">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="771ef-151">Clique na guia **Salvar e enfileirar** e selecione a opção **Salvar e enfileirar**.</span><span class="sxs-lookup"><span data-stu-id="771ef-151">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="771ef-152">Verifique se a **Versão Prévia do Linux Hospedada** está selecionada para o Pool de agentes na janela pop-up.</span><span class="sxs-lookup"><span data-stu-id="771ef-152">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="771ef-153">Em seguida, clique no botão **Salvar e enfileirar**.</span><span class="sxs-lookup"><span data-stu-id="771ef-153">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="771ef-154">Clique no número de build para verificar se o pipeline de build do projeto Java foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="771ef-154">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">
 

## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="771ef-155">Criar uma definição da versão para um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="771ef-155">Create a release definition for a Java app</span></span>

<span data-ttu-id="771ef-156">O pipeline de lançamento no Azure DevOps dispara automaticamente a implantação de artefatos de build em um ambiente de destino, como o Azure, assim que o processo de compilação é concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="771ef-156">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="771ef-157">O pipeline de lançamento pode ser criado para ambientes de desenvolvimento, teste, preparo ou produção.</span><span class="sxs-lookup"><span data-stu-id="771ef-157">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="771ef-158">Clique na guia "Build e versão" na parte superior da página do projeto Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="771ef-158">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="771ef-159">Em seguida, selecione o link **Versões**.</span><span class="sxs-lookup"><span data-stu-id="771ef-159">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">
 
2. <span data-ttu-id="771ef-160">Clique no botão “Novo pipeline”</span><span class="sxs-lookup"><span data-stu-id="771ef-160">Click on the "New pipeline\*\* button</span></span>
3. <span data-ttu-id="771ef-161">Selecione **Implantar um aplicativo Java no Serviço de Aplicativo do Azure** na lista de modelos e clique no botão **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="771ef-161">Select the **Deploy a Java app to Azure App Service** in the list of templates, then click on the **Apply** button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">
 
4. <span data-ttu-id="771ef-162">Defina um **Nome do estágio** (por exemplo, Desenvolvimento, Teste, Preparo ou Produção).</span><span class="sxs-lookup"><span data-stu-id="771ef-162">Set a **Stage name** (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="771ef-163">Em seguida, clique no botão **X** para fechar a janela pop-up</span><span class="sxs-lookup"><span data-stu-id="771ef-163">Then click on the **X** button to close the pop-up window</span></span>
5. <span data-ttu-id="771ef-164">Clique no botão **+ Adicionar** na seção Artefatos.</span><span class="sxs-lookup"><span data-stu-id="771ef-164">Click on the **+ Add** button in the Artifacts section.</span></span>  <span data-ttu-id="771ef-165">Isso vinculará os artefatos da definição de build a essa definição da versão.</span><span class="sxs-lookup"><span data-stu-id="771ef-165">This will link artifacts from the build definition to this release definition.</span></span>  
6. <span data-ttu-id="771ef-166">Use o menu suspenso da **Fonte (pipeline de build)** para selecionar sua definição de build.</span><span class="sxs-lookup"><span data-stu-id="771ef-166">Use the drop-down menu for the **Source (build pipeline)** to select your build definition.</span></span> <span data-ttu-id="771ef-167">Em seguida, clique no botão **Adicionar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="771ef-167">Then click the **Add** button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">
 
7. <span data-ttu-id="771ef-168">Clique na guia **Tarefas** no pipeline.</span><span class="sxs-lookup"><span data-stu-id="771ef-168">Click on the **Tasks** tab on the pipeline.</span></span>  <span data-ttu-id="771ef-169">Depois, selecione o nome do estágio.</span><span class="sxs-lookup"><span data-stu-id="771ef-169">Then, select your stage name.</span></span>
 
<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="771ef-170">Use o menu suspenso **Assinatura do Azure** para selecionar a ID de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="771ef-170">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="771ef-171">Selecione **Aplicativo Linux** no menu suspenso **Tipo de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="771ef-171">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="771ef-172">Selecione o nome da instância do Aplicativo Web para Contêiner criado acima, no menu suspenso **Nome do serviço de aplicativo**</span><span class="sxs-lookup"><span data-stu-id="771ef-172">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="771ef-173">Insira o nome do registro de contêiner do Azure no campo **Registro ou Namespaces**.</span><span class="sxs-lookup"><span data-stu-id="771ef-173">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="771ef-174">Por exemplo, **myregistry.azure.io**</span><span class="sxs-lookup"><span data-stu-id="771ef-174">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="771ef-175">Insira o nome do registro no campo **Repositório**</span><span class="sxs-lookup"><span data-stu-id="771ef-175">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="771ef-176">Clique em **Implantar Serviço de Aplicativo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="771ef-176">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="771ef-177">Insira a marca da imagem de contêiner na caixa de texto **Marca**.</span><span class="sxs-lookup"><span data-stu-id="771ef-177">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="771ef-178">Clique em **Executar no agente**.</span><span class="sxs-lookup"><span data-stu-id="771ef-178">Click on **Run on agent**.</span></span>  <span data-ttu-id="771ef-179">Selecione **Versão Prévia do Linux Hospedada** no menu suspenso Pool de agentes.</span><span class="sxs-lookup"><span data-stu-id="771ef-179">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="771ef-180">Configurar Variáveis de Ambiente</span><span class="sxs-lookup"><span data-stu-id="771ef-180">Setup Environment Variables</span></span>

1. <span data-ttu-id="771ef-181">Clique na guia **Variáveis**.  Em seguida, clique no botão **+ Adicionar** para definir as variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="771ef-181">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="771ef-182">Adicione o nome da variável e valores para a URL do registro de contêiner, nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="771ef-182">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="771ef-183">Para maior segurança, clique no ícone de cadeado para ocultar o valor da senha.</span><span class="sxs-lookup"><span data-stu-id="771ef-183">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="771ef-184">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="771ef-184">For example:</span></span>
- <span data-ttu-id="771ef-185">registry.password</span><span class="sxs-lookup"><span data-stu-id="771ef-185">registry.password</span></span>
- <span data-ttu-id="771ef-186">registry.url</span><span class="sxs-lookup"><span data-stu-id="771ef-186">registry.url</span></span>
- <span data-ttu-id="771ef-187">registry.username</span><span class="sxs-lookup"><span data-stu-id="771ef-187">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="771ef-188">Clique na guia **Tarefas** para retornar à página de definição do pipeline de lançamento principal.</span><span class="sxs-lookup"><span data-stu-id="771ef-188">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="771ef-189">Clique em **Implantar Serviço de Aplicativo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="771ef-189">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="771ef-190">Expanda a seção **Definições do Aplicativo e da Configuração** e clique no caminho de navegação do campo **Configurações do Aplicativo** para adicionar a variável de ambiente e conectar o registro de contêiner durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="771ef-190">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="771ef-191">Clique no botão \*\* + Adicionar\*\* para definir as configurações do aplicativo a seguir e atribuir as variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="771ef-191">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
- <span data-ttu-id="771ef-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span><span class="sxs-lookup"><span data-stu-id="771ef-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
- <span data-ttu-id="771ef-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="771ef-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
- <span data-ttu-id="771ef-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span><span class="sxs-lookup"><span data-stu-id="771ef-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">
 
7. <span data-ttu-id="771ef-195">Clique no botão **OK** para continuar</span><span class="sxs-lookup"><span data-stu-id="771ef-195">Click on the **OK** button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="771ef-196">Configurar Implantação Contínua e Implantar Aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="771ef-196">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="771ef-197">Para habilitar a implantação contínua, clique na guia **Pipelines**</span><span class="sxs-lookup"><span data-stu-id="771ef-197">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="771ef-198">Na seção Artefatos, clique no ícone de raio.</span><span class="sxs-lookup"><span data-stu-id="771ef-198">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="771ef-199">Em seguida, defina o **Gatilho de implantação contínua** para Habilitado.</span><span class="sxs-lookup"><span data-stu-id="771ef-199">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">
 
3. <span data-ttu-id="771ef-200">Clique no botão **Salvar** e no botão **OK**</span><span class="sxs-lookup"><span data-stu-id="771ef-200">Click on the **Save** button, then the **OK** button</span></span> 
4. <span data-ttu-id="771ef-201">Clique no menu suspenso **+ Versão** e selecione o link **Criar uma versão**</span><span class="sxs-lookup"><span data-stu-id="771ef-201">Click on the **+ Release** drop-down menu, then select **Create a release** link</span></span>
5. <span data-ttu-id="771ef-202">Use o menu suspenso **Estágios para alterar gatilho de automático para manual** para marcar a caixa de seleção do nome do estágio</span><span class="sxs-lookup"><span data-stu-id="771ef-202">Use the **Stages for a trigger change from automated to manual** drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="771ef-203">Clique no botão **Criar** para continuar</span><span class="sxs-lookup"><span data-stu-id="771ef-203">Click the **Create** button to continue</span></span>
7. <span data-ttu-id="771ef-204">Clique no número da versão.</span><span class="sxs-lookup"><span data-stu-id="771ef-204">Click on the release number.</span></span>  <span data-ttu-id="771ef-205">Em seguida, passe o cursor do mouse sobre o nome do estágio e clique no botão **Implantar**</span><span class="sxs-lookup"><span data-stu-id="771ef-205">Then hover your mouse cursor over the stage name and click on the **Deploy** button</span></span>
8. <span data-ttu-id="771ef-206">Clique no botão **Implantar** na janela pop-up para iniciar o processo de implantação no Azure</span><span class="sxs-lookup"><span data-stu-id="771ef-206">The click on the **Deploy** button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="771ef-207">Testar Aplicativo Web Java</span><span class="sxs-lookup"><span data-stu-id="771ef-207">Test the Java Web Application</span></span>
1. <span data-ttu-id="771ef-208">Execute a URL do aplicativo Web no navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="771ef-208">Run the web app url in web browser:</span></span>  
<span data-ttu-id="771ef-209">https://{nome-do-serviço-de-aplicativo}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="771ef-209">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>

 
<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="771ef-210">A página da Web deverá mostrar **Olá Azure!**</span><span class="sxs-lookup"><span data-stu-id="771ef-210">The web page should say **Hello Azure!**</span></span>
 
<img src="media/VSTS/web-api17.png">
