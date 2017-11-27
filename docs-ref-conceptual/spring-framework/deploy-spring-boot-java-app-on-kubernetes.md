---
title: "Implantar um Aplicativo Spring Boot no Kubernetes no Serviço de Contêiner do Azure"
description: "Este tutorial orienta você pelas etapas de implantação de um aplicativo Spring Boot em um cluster Kubernetes no Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Kubernetes
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 7f72a0eaeb932b400cd12a3ccc43706e890aebf6
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="8f5b4-104">Implantar um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8f5b4-104">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="8f5b4-105">**[Spring Framework]** é um framework de software livre popular que ajuda os desenvolvedores de Java a criar aplicativos de API, Web e móveis.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-105">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="8f5b4-106">Este tutorial usa um aplicativo de exemplo criado usando o [Spring Boot], uma abordagem controlada por convenção para o uso do Spring para começar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-106">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="8f5b4-107">O **[Kubernetes]** e o **[Docker]** são soluções de software livre que ajudam os desenvolvedores a automatizar a implantação, o dimensionamento e o gerenciamento de seus aplicativos em execução em contêineres.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-107">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="8f5b4-108">Este tutorial fornece uma orientação sobre como combinar essas duas tecnologias populares de software livre para desenvolver e implantar um aplicativo Spring Boot no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-108">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="8f5b4-109">Mais especificamente, você usa o *[Spring Boot]* para o desenvolvimento de aplicativos, o *[Kubernetes]* para a implantação de contêineres e o [AKS (Serviço de Contêiner do Azure)] para hospedar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-109">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8f5b4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f5b4-110">Prerequisites</span></span>

* <span data-ttu-id="8f5b4-111">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="8f5b4-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8f5b4-112">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="8f5b4-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="8f5b4-113">Um [JDK (Java Developer Kit)] atualizado.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-113">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="8f5b4-114">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="8f5b4-115">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="8f5b4-115">A [Git] client.</span></span>
* <span data-ttu-id="8f5b4-116">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="8f5b4-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8f5b4-117">Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="8f5b4-118">Criar o aplicativo Web de Introdução ao Spring Boot no Docker</span><span class="sxs-lookup"><span data-stu-id="8f5b4-118">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="8f5b4-119">As etapas a seguir mostram como compilar um aplicativo Web Spring Boot e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-119">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="8f5b4-120">Abra um prompt de comando, crie um diretório local para conter o aplicativo e altere para o diretório. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-120">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="8f5b4-121">-- ou --</span><span class="sxs-lookup"><span data-stu-id="8f5b4-121">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="8f5b4-122">Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="8f5b4-123">Altere o diretório para o projeto concluído.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-123">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="8f5b4-124">Use o Maven para compilar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-124">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="8f5b4-125">Teste o aplicativo Web navegando até http://localhost:8080, ou com o seguinte comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-125">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="8f5b4-126">Você verá a seguinte mensagem exibida: **Olá, Mundo Docker**</span><span class="sxs-lookup"><span data-stu-id="8f5b4-126">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="8f5b4-128">Criar um Registro de Contêiner do Azure usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8f5b4-128">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="8f5b4-129">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-129">Open a command prompt.</span></span>

1. <span data-ttu-id="8f5b4-130">Faça logon na sua Conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-130">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="8f5b4-131">Crie um grupo de recursos para os recursos do Azure usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-131">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="8f5b4-132">Crie um registro de contêiner do Azure privado no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-132">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="8f5b4-133">O tutorial envia o aplicativo de exemplo para esse registro como uma imagem de Docker em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-133">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="8f5b4-134">Substitua `wingtiptoysregistry` por um nome exclusivo para o registro.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-134">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="8f5b4-135">Enviar seu aplicativo para o registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="8f5b4-135">Push your app to the container registry</span></span>

1. <span data-ttu-id="8f5b4-136">Navegue até o diretório de configuração de sua instalação do Maven (padrão ~/.m2/ ou C:\Usuários\nomedeusuário\.m2) e abra o arquivo *settings.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-136">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="8f5b4-137">Recupere a senha de seu registro de contêiner na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-137">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="8f5b4-138">Adicione a id do Registro de Contêiner do Azure e a senha a uma nova coleção do `<server>` no arquivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-138">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="8f5b4-139">`id` e `username` são os nomes do registro.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-139">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="8f5b4-140">Use o valor `password` do comando anterior (sem as aspas).</span><span class="sxs-lookup"><span data-stu-id="8f5b4-140">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="8f5b4-141">Navegue até o diretório do projeto completo de seu aplicativo Spring Boot (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), e abra o arquivo *pom.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-141">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="8f5b4-142">Atualize a coleção `<properties>` no arquivo *pom.xml* com o valor do servidor de logon para seu Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-142">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="8f5b4-143">Atualize a coleção `<plugins>` no arquivo *pom.xml* para que o `<plugin>` contenha o endereço do servidor de logon e o nome de registro para seu Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-143">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="8f5b4-144">Navegue até o diretório do projeto completo de seu aplicativo Spring Boot e execute o seguinte comando para compilar o contêiner do Docker e enviar a imagem ao Registro:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-144">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="8f5b4-145">Você receberá uma mensagem de erro semelhante a uma das seguintes quando o Maven enviar a imagem ao Azure:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-145">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="8f5b4-146">Se você receber esse erro, faça logon no Azure a partir da linha de comando do Docker.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-146">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="8f5b4-147">Em seguida, envie por push o seu contêiner:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-147">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="8f5b4-148">Criar um Cluster Kubernetes no AKS usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8f5b4-148">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="8f5b4-149">Crie um cluster Kubernetes no Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-149">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="8f5b4-150">O comando a seguir cria um cluster *kubernetes* no grupo de recursos *wingtiptoys-kubernetes*, com *wingtiptoys-containerservice* como o nome do cluster e *wingtiptoys-kubernetes* como o prefixo DNS:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-150">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="8f5b4-151">Esse comando pode demorar algum tempo para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-151">This command may take a while to complete.</span></span>

1. <span data-ttu-id="8f5b4-152">Instalar `kubectl` usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-152">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="8f5b4-153">Os usuários de Linux podem ter que prefixar esse comando com `sudo`, já que ele implanta a CLI do Kubernetes em `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-153">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="8f5b4-154">Baixe as informações de configuração do cluster para que possa gerenciá-lo na interface da Web do Kubernetes e `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-154">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="8f5b4-155">Implantar a imagem em seu cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f5b4-155">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="8f5b4-156">Este tutorial implanta o aplicativo usando `kubectl` e depois permite que você explore a implantação por meio da interface da Web do Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-156">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="8f5b4-157">Implantar com a interface da Web do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8f5b4-157">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="8f5b4-158">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-158">Open a command prompt.</span></span>

1. <span data-ttu-id="8f5b4-159">Abra o site de configuração do cluster Kubernetes em seu navegador padrão:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-159">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="8f5b4-160">Quando o site de configuração de Kubernetes abrir no navegador, clique no link para **implantar um aplicativo em contêiner**:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-160">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Site de configuração do Kubernetes][KB01]

1. <span data-ttu-id="8f5b4-162">Quando a página **Implantar um aplicativo em contêiner** for exibida, especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-162">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="8f5b4-163">a.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-163">a.</span></span> <span data-ttu-id="8f5b4-164">Selecione **Especificar detalhes do aplicativo abaixo**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-164">Select **Specify app details below**.</span></span>

   <span data-ttu-id="8f5b4-165">b.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-165">b.</span></span> <span data-ttu-id="8f5b4-166">Insira o nome do aplicativo Spring Boot para o **Nome do aplicativo**; por exemplo: "*gs-spring-boot-docker*".</span><span class="sxs-lookup"><span data-stu-id="8f5b4-166">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="8f5b4-167">c.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-167">c.</span></span> <span data-ttu-id="8f5b4-168">Insira o servidor de logon e imagem do contêiner de antes na **Imagem do contêiner**; por exemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="8f5b4-168">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="8f5b4-169">d.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-169">d.</span></span> <span data-ttu-id="8f5b4-170">Escolha **Externo** para o **Serviço**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-170">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="8f5b4-171">e.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-171">e.</span></span> <span data-ttu-id="8f5b4-172">Especifique as portas internas e externas nas caixas de texto **Porta** e **Porta de destino**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-172">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Site de configuração do Kubernetes][KB02]


1. <span data-ttu-id="8f5b4-174">Clique em **Implantar** para implantar o contêiner.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-174">Click **Deploy** to deploy the container.</span></span>

   ![Implantar o contêiner][KB05]

1. <span data-ttu-id="8f5b4-176">Após a implantação de seu aplicativo, você verá o aplicativo Spring Boot listado em **Serviços**.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-176">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Serviços Kubernetes][KB06]

1. <span data-ttu-id="8f5b4-178">Se você clicar no link para **Pontos de extremidade externos**, poderá ver o aplicativo Spring Boot em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-178">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Serviços Kubernetes][KB07]

   ![Procurar aplicativo de exemplo no Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="8f5b4-181">Implantar com kubectl</span><span class="sxs-lookup"><span data-stu-id="8f5b4-181">Deploy with kubectl</span></span>

1. <span data-ttu-id="8f5b4-182">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-182">Open a command prompt.</span></span>

1. <span data-ttu-id="8f5b4-183">Execute seu contêiner no cluster Kubernetes usando o comando `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-183">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="8f5b4-184">Forneça um nome de serviço para seu aplicativo no Kubernetes e o nome de imagem completo.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-184">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="8f5b4-185">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-185">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="8f5b4-186">Neste comando:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-186">In this command:</span></span>

   * <span data-ttu-id="8f5b4-187">O nome do contêiner `gs-spring-boot-docker` é especificado imediatamente após o comando `run`</span><span class="sxs-lookup"><span data-stu-id="8f5b4-187">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="8f5b4-188">O parâmetro `--image` especifica a combinação de servidor de logon e nome da imagem como `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="8f5b4-188">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="8f5b4-189">Exponha seu cluster Kubernetes externamente usando o comando `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-189">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="8f5b4-190">Especifique o nome do serviço, a porta TCP voltada para o público usada para acessar o aplicativo e a porta de destino interna na qual seu aplicativo escuta.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-190">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="8f5b4-191">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-191">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="8f5b4-192">Neste comando:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-192">In this command:</span></span>

   * <span data-ttu-id="8f5b4-193">O nome do contêiner `gs-spring-boot-docker` é especificado imediatamente após o comando `expose deployment`</span><span class="sxs-lookup"><span data-stu-id="8f5b4-193">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="8f5b4-194">O parâmetro `--type` especifica que o cluster usa o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="8f5b4-194">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="8f5b4-195">O parâmetro `--port` especifica a porta TCP 80 voltada para o público.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-195">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="8f5b4-196">Você acessa o aplicativo nessa porta.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-196">You access the app on this port.</span></span>

   * <span data-ttu-id="8f5b4-197">O parâmetro `--target-port` especifica a porta TCP interna 8080.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-197">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="8f5b4-198">O balanceador de carga encaminha solicitações ao seu aplicativo nesta porta.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-198">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="8f5b4-199">Após a implantação do aplicativo no cluster, consulte o endereço IP externo e abra-o em seu navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-199">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Procurar aplicativo de exemplo no Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="8f5b4-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f5b4-201">Next steps</span></span>

<span data-ttu-id="8f5b4-202">Para saber mais sobre como usar o Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-202">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="8f5b4-203">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="8f5b4-203">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="8f5b4-204">Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8f5b4-204">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

<span data-ttu-id="8f5b4-205">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="8f5b4-205">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="8f5b4-206">Para saber mais sobre o Spring Boot no projeto de exemplo do Docker, veja [Introdução ao Spring Boot no Docker].</span><span class="sxs-lookup"><span data-stu-id="8f5b4-206">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="8f5b4-207">Os links a seguir fornecem mais informações sobre como criar aplicativos Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-207">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="8f5b4-208">Para saber mais sobre como começar a criar um aplicativo Spring Boot simples, veja o Spring Initializr em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-208">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="8f5b4-209">Os links a seguir fornecem mais informações sobre como usar kubernetes com o Azure:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-209">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="8f5b4-210">Introdução ao cluster Kubernetes no Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="8f5b4-210">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="8f5b4-211">Usar a interface do usuário da Web Kubernetes com o Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8f5b4-211">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="8f5b4-212">Saiba mais sobre como usar a interface de linha de comando Kubernetes no guia do usuário **kubectl** em <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="8f5b4-212">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="8f5b4-213">O site do Kubernetes tem vários artigos que abordam o uso de imagens em registros privados:</span><span class="sxs-lookup"><span data-stu-id="8f5b4-213">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="8f5b4-214">[Configurar contas de serviço para Pods]</span><span class="sxs-lookup"><span data-stu-id="8f5b4-214">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="8f5b4-215">[Namespaces]</span><span class="sxs-lookup"><span data-stu-id="8f5b4-215">[Namespaces]</span></span>
* <span data-ttu-id="8f5b4-216">[Extrair uma imagem de um registro privado]</span><span class="sxs-lookup"><span data-stu-id="8f5b4-216">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="8f5b4-217">Para obter mais exemplos sobre como usar imagens personalizadas do Docker com o Azure, veja [Usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux].</span><span class="sxs-lookup"><span data-stu-id="8f5b4-217">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[AKS (Serviço de Contêiner do Azure)]: https://azure.microsoft.com/services/container-service/
[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configurar contas de serviço para Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Extrair uma imagem de um registro privado]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
