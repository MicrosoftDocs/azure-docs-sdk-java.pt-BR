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
ms.openlocfilehash: 818e37291fa47f99cb161c63a86062bddbf6248c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799932"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="b2dea-103">CI/CD para aplicativos MicroProfile usando o Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="b2dea-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="b2dea-104">Este tutorial mostra como os desenvolvedores Java EE podem configurar facilmente um ciclo de lançamento de CI/CD para implantar seus aplicativos [MicroProfile](http://microprofile.io) em um Aplicativo Web para Contêineres usando o Azure DevOps (antes conhecido como VSTS).</span><span class="sxs-lookup"><span data-stu-id="b2dea-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="b2dea-105">Neste exemplo, usaremos um aplicativo MicroProfile que usa um [Payara Micro](https://www.payara.fish/payara_micro) como uma imagem básica.</span><span class="sxs-lookup"><span data-stu-id="b2dea-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="b2dea-106">Vamos começar o processo de colocação em contêiner do Azure DevOps criando uma imagem do Docker e enviando a imagem de contêiner para um Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dea-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="b2dea-107">Em seguida, conclua com um pipeline de lançamento do Azure DevOps para implantar a imagem de contêiner em um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b2dea-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2dea-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b2dea-108">Prerequisites</span></span>
- <span data-ttu-id="b2dea-109">Copiar e salvar a URL Git do [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span><span class="sxs-lookup"><span data-stu-id="b2dea-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="b2dea-110">Registrar-se ou fazer logon em sua conta do [Azure DevOps](https://dev.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b2dea-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="b2dea-111">Criar um novo [projeto do Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) e usar a URL Git acima para **importar um repositório**</span><span class="sxs-lookup"><span data-stu-id="b2dea-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="b2dea-112">Criar um [Registro de Contêiner do Azure](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span><span class="sxs-lookup"><span data-stu-id="b2dea-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="b2dea-113">Criar um Aplicativo Web para Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="b2dea-113">Create an Azure Web App for Container</span></span>
  > [!NOTE]
  >
  > <span data-ttu-id="b2dea-114">Selecionar "Início Rápido" nas Configurações do Contêiner ao provisionar a instância do Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b2dea-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="b2dea-115">Criar a definição de build</span><span class="sxs-lookup"><span data-stu-id="b2dea-115">Create a Build definition</span></span>

<span data-ttu-id="b2dea-116">A definição de build no Azure DevOps executa automaticamente todas as tarefas no build sempre que há uma confirmação no aplicativo de origem do Java EE.</span><span class="sxs-lookup"><span data-stu-id="b2dea-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="b2dea-117">Neste exemplo, o Azure DevOps usará Maven para compilar o projeto MicroProfile em Java.</span><span class="sxs-lookup"><span data-stu-id="b2dea-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="b2dea-118">Clique na guia "Build e Versão" na parte superior da página do projeto Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="b2dea-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="b2dea-119">Em seguida, selecione o link **Builds**</span><span class="sxs-lookup"><span data-stu-id="b2dea-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="b2dea-120">Clique no botão **Novo Pipeline** e em **Continuar** para começar a definir as tarefas de build</span><span class="sxs-lookup"><span data-stu-id="b2dea-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="b2dea-121">Selecione "Maven" na lista de modelos e clique no botão **Aplicar** para compilar seu projeto Java</span><span class="sxs-lookup"><span data-stu-id="b2dea-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="b2dea-122">Use o menu suspenso no campo Pool de agentes para selecionar a opção **Versão prévia do Linux Hospedada**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
   > [!NOTE]
   >
   > <span data-ttu-id="b2dea-123">Isso informa ao Azure DevOps sobre qual servidor de build usar.</span><span class="sxs-lookup"><span data-stu-id="b2dea-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="b2dea-124">Você pode usar seu próprio servidor de build personalizado</span><span class="sxs-lookup"><span data-stu-id="b2dea-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="b2dea-125">Para configurar o build para a integração contínua, selecione a guia **Gatilhos** e marque a caixa de seleção **Habilitar integração contínua**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 

6. <span data-ttu-id="b2dea-126">Selecione a guia <strong>Tarefas</strong> para retornar à página do pipeline de build principal</span><span class="sxs-lookup"><span data-stu-id="b2dea-126">Select the <strong>Tasks</strong> tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="b2dea-127">Use o menu suspenso <strong>Salvar &amp; enfileirar</strong> para selecionar a opção <strong>Salvar</strong></span><span class="sxs-lookup"><span data-stu-id="b2dea-127">Use the <strong>Save &amp; queue</strong> drop-down menu to select the <strong>Save</strong> option</span></span>


## <a name="create-a-docker-build-image"></a><span data-ttu-id="b2dea-128">Criar uma Imagem de Build do Docker</span><span class="sxs-lookup"><span data-stu-id="b2dea-128">Create a Docker Build Image</span></span>

<span data-ttu-id="b2dea-129">Nessa tarefa, o Azure DevOps usa um Dockerfile com uma imagem básica do Payara Micro para criar uma imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="b2dea-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="b2dea-130">Selecione a guia **Tarefas** para retornar à página do pipeline de build principal</span><span class="sxs-lookup"><span data-stu-id="b2dea-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="b2dea-131">Clique no ícone **+** para adicionar uma nova tarefa à definição de build</span><span class="sxs-lookup"><span data-stu-id="b2dea-131">Click on the **+** icon to add new task to the build definition</span></span>

<img src="media/VSTS/Tasks-add4.png">

3. <span data-ttu-id="b2dea-132">Selecione &quot;Docker&quot; na lista de modelos e clique no botão <strong>Adicionar</strong></span><span class="sxs-lookup"><span data-stu-id="b2dea-132">Select &quot;Docker&quot; from the list of templates, then click on the <strong>Add</strong> button</span></span>
4. <span data-ttu-id="b2dea-133">Insira um nome descritivo no campo <strong>Nome de exibição</strong></span><span class="sxs-lookup"><span data-stu-id="b2dea-133">Enter a description name for the <strong>Display name</strong> field</span></span>
5. <span data-ttu-id="b2dea-134">Verifique se a opção <strong>Registro de Contêiner do Azure</strong> está selecionada no menu suspenso do <strong>Tipo do registro de contêiner</strong>.</span><span class="sxs-lookup"><span data-stu-id="b2dea-134">Verify that <strong>Azure Container Registry</strong> is selected in the drop-down menu for <strong>Container registry type</strong>.</span></span>
<span data-ttu-id="b2dea-135">&gt;</span><span class="sxs-lookup"><span data-stu-id="b2dea-135">&gt;</span></span> [!NOTE]
<span data-ttu-id="b2dea-136">&gt; &gt;  Se você estiver usando o Hub do Docker ou outro registro, selecione &quot;Registro de Contêiner&quot;.</span><span class="sxs-lookup"><span data-stu-id="b2dea-136">&gt; &gt;  If you are using Docker Hub or another registry, select &quot;Container Registry&quot; instead.</span></span>  <span data-ttu-id="b2dea-137">Em seguida, clique no botão &quot;+ Novo&quot; para fornecer as credenciais e as informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="b2dea-137">Then click on the &quot;+ New&quot; button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="b2dea-138">Vá para a seção Comandos para continuar.</span><span class="sxs-lookup"><span data-stu-id="b2dea-138">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="b2dea-139">Use o menu suspenso **Assinatura do Azure** para selecionar a ID de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dea-139">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="b2dea-140">Em seguida, clique no botão **Autorizar**</span><span class="sxs-lookup"><span data-stu-id="b2dea-140">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="b2dea-141">No menu suspenso **Registro de contêiner do Azure**, selecione o nome de registro criado no Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dea-141">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="b2dea-142">Verifique se a opção **build** está selecionada no menu suspenso **Comando**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-142">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="b2dea-143">Para o **Dockerfile**, clique no ícone de navegação do caminho ao lado da caixa de texto para selecionar o Dockerfile no projeto GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2dea-143">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="b2dea-144">Em seguida, clique no botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-144">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="b2dea-145">No **Nome da imagem**, marque a caixa de seleção **Incluir marca mais recente**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-145">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="b2dea-146">Use o menu suspenso **Salvar e enfileirar** para selecionar a opção **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-146">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="b2dea-147">Enviar por push a Imagem do Docker para o ACR</span><span class="sxs-lookup"><span data-stu-id="b2dea-147">Push Docker Image to ACR</span></span>

<span data-ttu-id="b2dea-148">Nessa tarefa, o Azure DevOps enviará por push a imagem do Docker para seu Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dea-148">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="b2dea-149">Isso será usado para executar o aplicativo de API MicroProfile como um aplicativo Web Java em contêineres.</span><span class="sxs-lookup"><span data-stu-id="b2dea-149">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="b2dea-150">Como estamos usando o Docker no Azure DevOps, crie um novo modelo de Docker repetindo as etapas 1 a 7 acima na seção **Criar uma Imagem de Build do Docker**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-150">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="b2dea-151">Selecione **push** no menu suspenso **Comando**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-151">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="b2dea-152">Clique na guia **Salvar e enfileirar** e selecione a opção **Salvar e enfileirar**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-152">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="b2dea-153">Verifique se a **Versão Prévia do Linux Hospedada** está selecionada para o Pool de agentes na janela pop-up.</span><span class="sxs-lookup"><span data-stu-id="b2dea-153">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="b2dea-154">Em seguida, clique no botão **Salvar e enfileirar**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-154">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="b2dea-155">Clique no número de build para verificar se o pipeline de build do projeto Java foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="b2dea-155">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">


## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="b2dea-156">Criar uma definição da versão para um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="b2dea-156">Create a release definition for a Java app</span></span>

<span data-ttu-id="b2dea-157">O pipeline de lançamento no Azure DevOps dispara automaticamente a implantação de artefatos de build em um ambiente de destino, como o Azure, assim que o processo de compilação é concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="b2dea-157">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="b2dea-158">O pipeline de lançamento pode ser criado para ambientes de desenvolvimento, teste, preparo ou produção.</span><span class="sxs-lookup"><span data-stu-id="b2dea-158">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="b2dea-159">Clique na guia "Build e versão" na parte superior da página do projeto Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="b2dea-159">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="b2dea-160">Em seguida, selecione o link **Versões**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-160">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">

2. <span data-ttu-id="b2dea-161">Clique no botão &quot;Novo pipeline\*\*</span><span class="sxs-lookup"><span data-stu-id="b2dea-161">Click on the &quot;New pipeline\*\* button</span></span>
3. <span data-ttu-id="b2dea-162">Selecione <strong>Implantar um aplicativo Java no Serviço de Aplicativo do Azure</strong> na lista de modelos e clique no botão <strong>Aplicar</strong>.</span><span class="sxs-lookup"><span data-stu-id="b2dea-162">Select the <strong>Deploy a Java app to Azure App Service</strong> in the list of templates, then click on the <strong>Apply</strong> button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">

4. <span data-ttu-id="b2dea-163">Defina um <strong>Nome do estágio</strong> (por exemplo, Desenvolvimento, Teste, Preparo ou Produção).</span><span class="sxs-lookup"><span data-stu-id="b2dea-163">Set a <strong>Stage name</strong> (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="b2dea-164">Em seguida, clique no botão <strong>X</strong> para fechar a janela pop-up</span><span class="sxs-lookup"><span data-stu-id="b2dea-164">Then click on the <strong>X</strong> button to close the pop-up window</span></span>
5. <span data-ttu-id="b2dea-165">Clique no botão <strong>+ Adicionar</strong> na seção Artefatos.</span><span class="sxs-lookup"><span data-stu-id="b2dea-165">Click on the <strong>+ Add</strong> button in the Artifacts section.</span></span>  <span data-ttu-id="b2dea-166">Isso vinculará os artefatos da definição de build a essa definição da versão.</span><span class="sxs-lookup"><span data-stu-id="b2dea-166">This will link artifacts from the build definition to this release definition.</span></span><br/><span data-ttu-id="b2dea-167">6. Use o menu suspenso da <strong>Fonte (pipeline de build)</strong> para selecionar sua definição de build.</span><span class="sxs-lookup"><span data-stu-id="b2dea-167">6. Use the drop-down menu for the <strong>Source (build pipeline)</strong> to select your build definition.</span></span> <span data-ttu-id="b2dea-168">Em seguida, clique no botão <strong>Adicionar</strong> para continuar.</span><span class="sxs-lookup"><span data-stu-id="b2dea-168">Then click the <strong>Add</strong> button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">

7. <span data-ttu-id="b2dea-169">Clique na guia <strong>Tarefas</strong> no pipeline.</span><span class="sxs-lookup"><span data-stu-id="b2dea-169">Click on the <strong>Tasks</strong> tab on the pipeline.</span></span>  <span data-ttu-id="b2dea-170">Depois, selecione o nome do estágio.</span><span class="sxs-lookup"><span data-stu-id="b2dea-170">Then, select your stage name.</span></span>

<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="b2dea-171">Use o menu suspenso **Assinatura do Azure** para selecionar a ID de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2dea-171">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="b2dea-172">Selecione **Aplicativo Linux** no menu suspenso **Tipo de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-172">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="b2dea-173">Selecione o nome da instância do Aplicativo Web para Contêiner criado acima, no menu suspenso **Nome do serviço de aplicativo**</span><span class="sxs-lookup"><span data-stu-id="b2dea-173">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="b2dea-174">Insira o nome do registro de contêiner do Azure no campo **Registro ou Namespaces**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-174">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="b2dea-175">Por exemplo, **myregistry.azure.io**</span><span class="sxs-lookup"><span data-stu-id="b2dea-175">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="b2dea-176">Insira o nome do registro no campo **Repositório**</span><span class="sxs-lookup"><span data-stu-id="b2dea-176">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="b2dea-177">Clique em **Implantar Serviço de Aplicativo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-177">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="b2dea-178">Insira a marca da imagem de contêiner na caixa de texto **Marca**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-178">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="b2dea-179">Clique em **Executar no agente**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-179">Click on **Run on agent**.</span></span>  <span data-ttu-id="b2dea-180">Selecione **Versão Prévia do Linux Hospedada** no menu suspenso Pool de agentes.</span><span class="sxs-lookup"><span data-stu-id="b2dea-180">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="b2dea-181">Configurar Variáveis de Ambiente</span><span class="sxs-lookup"><span data-stu-id="b2dea-181">Setup Environment Variables</span></span>

1. <span data-ttu-id="b2dea-182">Clique na guia **Variáveis**.  Em seguida, clique no botão **+ Adicionar** para definir as variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="b2dea-182">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="b2dea-183">Adicione o nome da variável e valores para a URL do registro de contêiner, nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="b2dea-183">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="b2dea-184">Para maior segurança, clique no ícone de cadeado para ocultar o valor da senha.</span><span class="sxs-lookup"><span data-stu-id="b2dea-184">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="b2dea-185">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="b2dea-185">For example:</span></span>
- <span data-ttu-id="b2dea-186">registry.password</span><span class="sxs-lookup"><span data-stu-id="b2dea-186">registry.password</span></span>
- <span data-ttu-id="b2dea-187">registry.url</span><span class="sxs-lookup"><span data-stu-id="b2dea-187">registry.url</span></span>
- <span data-ttu-id="b2dea-188">registry.username</span><span class="sxs-lookup"><span data-stu-id="b2dea-188">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="b2dea-189">Clique na guia **Tarefas** para retornar à página de definição do pipeline de lançamento principal.</span><span class="sxs-lookup"><span data-stu-id="b2dea-189">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="b2dea-190">Clique em **Implantar Serviço de Aplicativo do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b2dea-190">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="b2dea-191">Expanda a seção **Definições do Aplicativo e da Configuração** e clique no caminho de navegação do campo **Configurações do Aplicativo** para adicionar a variável de ambiente e conectar o registro de contêiner durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="b2dea-191">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="b2dea-192">Clique no botão \*\* + Adicionar\*\* para definir as configurações do aplicativo a seguir e atribuir as variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="b2dea-192">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
7. <span data-ttu-id="b2dea-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span><span class="sxs-lookup"><span data-stu-id="b2dea-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
8. <span data-ttu-id="b2dea-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="b2dea-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
9. <span data-ttu-id="b2dea-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span><span class="sxs-lookup"><span data-stu-id="b2dea-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">

7. <span data-ttu-id="b2dea-196">Clique no botão <strong>OK</strong> para continuar</span><span class="sxs-lookup"><span data-stu-id="b2dea-196">Click on the <strong>OK</strong> button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="b2dea-197">Configurar Implantação Contínua e Implantar Aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="b2dea-197">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="b2dea-198">Para habilitar a implantação contínua, clique na guia **Pipelines**</span><span class="sxs-lookup"><span data-stu-id="b2dea-198">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="b2dea-199">Na seção Artefatos, clique no ícone de raio.</span><span class="sxs-lookup"><span data-stu-id="b2dea-199">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="b2dea-200">Em seguida, defina o **Gatilho de implantação contínua** para Habilitado.</span><span class="sxs-lookup"><span data-stu-id="b2dea-200">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">

3. <span data-ttu-id="b2dea-201">Clique no botão <strong>Salvar</strong> e no botão <strong>OK</strong></span><span class="sxs-lookup"><span data-stu-id="b2dea-201">Click on the <strong>Save</strong> button, then the <strong>OK</strong> button</span></span> 
4. <span data-ttu-id="b2dea-202">Clique no menu suspenso <strong>+ Versão</strong> e selecione o link <strong>Criar uma versão</strong></span><span class="sxs-lookup"><span data-stu-id="b2dea-202">Click on the <strong>+ Release</strong> drop-down menu, then select <strong>Create a release</strong> link</span></span>
5. <span data-ttu-id="b2dea-203">Use o menu suspenso <strong>Estágios para alterar gatilho de automático para manual</strong> para marcar a caixa de seleção do nome do estágio</span><span class="sxs-lookup"><span data-stu-id="b2dea-203">Use the <strong>Stages for a trigger change from automated to manual</strong> drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="b2dea-204">Clique no botão <strong>Criar</strong> para continuar</span><span class="sxs-lookup"><span data-stu-id="b2dea-204">Click the <strong>Create</strong> button to continue</span></span>
7. <span data-ttu-id="b2dea-205">Clique no número da versão.</span><span class="sxs-lookup"><span data-stu-id="b2dea-205">Click on the release number.</span></span>  <span data-ttu-id="b2dea-206">Em seguida, passe o cursor do mouse sobre o nome do estágio e clique no botão <strong>Implantar</strong></span><span class="sxs-lookup"><span data-stu-id="b2dea-206">Then hover your mouse cursor over the stage name and click on the <strong>Deploy</strong> button</span></span>
8. <span data-ttu-id="b2dea-207">Clique no botão <strong>Implantar</strong> na janela pop-up para iniciar o processo de implantação no Azure</span><span class="sxs-lookup"><span data-stu-id="b2dea-207">The click on the <strong>Deploy</strong> button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="b2dea-208">Testar Aplicativo Web Java</span><span class="sxs-lookup"><span data-stu-id="b2dea-208">Test the Java Web Application</span></span>
1. <span data-ttu-id="b2dea-209">Execute a URL do aplicativo Web no navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="b2dea-209">Run the web app url in web browser:</span></span>  
   <span data-ttu-id="b2dea-210">https://{nome-do-serviço-de-aplicativo}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="b2dea-210">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>


<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="b2dea-211">A página da Web deverá mostrar **Olá Azure!**</span><span class="sxs-lookup"><span data-stu-id="b2dea-211">The web page should say **Hello Azure!**</span></span>

<img src="media/VSTS/web-api17.png">
