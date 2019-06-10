---
title: Implantar um Aplicativo Spring Boot no Kubernetes no Serviço de Kubernetes do Azure
description: Este tutorial orienta você pelas etapas de implantação de um aplicativo Spring Boot em um cluster Kubernetes no Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 9ab781d27e8968ab867efc65f3ac422ac6253a6a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270853"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a><span data-ttu-id="3b362-103">Implantar um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Kubernetes do Azure</span><span class="sxs-lookup"><span data-stu-id="3b362-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Kubernetes Service</span></span>

<span data-ttu-id="3b362-104">O **[Kubernetes]** e o **[Docker]** são soluções de software livre que ajudam os desenvolvedores a automatizar a implantação, o dimensionamento e o gerenciamento de seus aplicativos em execução em contêineres.</span><span class="sxs-lookup"><span data-stu-id="3b362-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications running in containers.</span></span>

<span data-ttu-id="3b362-105">Este tutorial fornece uma orientação sobre como combinar essas duas tecnologias populares de software livre para desenvolver e implantar um aplicativo Spring Boot no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3b362-105">This tutorial walks you through combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="3b362-106">Mais especificamente, você usa o *[Spring Boot]* para o desenvolvimento de aplicativos, o *[Kubernetes]* para a implantação de contêineres e o [AKS (Serviço de Kubernetes do Azure)] para hospedar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3b362-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Kubernetes Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3b362-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3b362-107">Prerequisites</span></span>

* <span data-ttu-id="3b362-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="3b362-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="3b362-109">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="3b362-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="3b362-110">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="3b362-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="3b362-111">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="3b362-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="3b362-112">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="3b362-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="3b362-113">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="3b362-113">A [Git] client.</span></span>
* <span data-ttu-id="3b362-114">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="3b362-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3b362-115">Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="3b362-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="3b362-116">Criar o aplicativo Web de Introdução ao Spring Boot no Docker</span><span class="sxs-lookup"><span data-stu-id="3b362-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="3b362-117">As etapas a seguir mostram como compilar um aplicativo Web Spring Boot e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="3b362-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="3b362-118">Abra um prompt de comando, crie um diretório local para conter o aplicativo e altere para o diretório. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b362-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="3b362-119">-- ou --</span><span class="sxs-lookup"><span data-stu-id="3b362-119">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="3b362-120">Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório.</span><span class="sxs-lookup"><span data-stu-id="3b362-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="3b362-121">Altere o diretório para o projeto concluído.</span><span class="sxs-lookup"><span data-stu-id="3b362-121">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="3b362-122">Use o Maven para compilar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3b362-122">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="3b362-123">Teste o aplicativo Web navegando até `http://localhost:8080` ou com o seguinte comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="3b362-123">Test the web app by browsing to `http://localhost:8080`, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="3b362-124">Você verá a seguinte mensagem exibida: **Olá, mundo do Docker**</span><span class="sxs-lookup"><span data-stu-id="3b362-124">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="3b362-126">Criar um Registro de Contêiner do Azure usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3b362-126">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="3b362-127">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="3b362-127">Open a command prompt.</span></span>

1. <span data-ttu-id="3b362-128">Faça logon na sua Conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="3b362-128">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="3b362-129">Escolha a sua Assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="3b362-129">Choose your Azure Subscription:</span></span>
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. <span data-ttu-id="3b362-130">Crie um grupo de recursos para os recursos do Azure usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3b362-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="3b362-131">Crie um registro de contêiner do Azure privado no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3b362-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="3b362-132">O tutorial envia o aplicativo de exemplo para esse registro como uma imagem de Docker em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="3b362-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="3b362-133">Substitua `wingtiptoysregistry` por um nome exclusivo para o registro.</span><span class="sxs-lookup"><span data-stu-id="3b362-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a><span data-ttu-id="3b362-134">Enviar por push seu aplicativo para o registro de contêiner via Jib</span><span class="sxs-lookup"><span data-stu-id="3b362-134">Push your app to the container registry via Jib</span></span>

1. <span data-ttu-id="3b362-135">Faça logon no Registro de Contêiner do Azure a partir da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b362-135">Log in to your Azure Container Registry from the Azure CLI.</span></span>
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. <span data-ttu-id="3b362-136">Navegue até o diretório do projeto completo de seu aplicativo Spring Boot (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou " */users/robert/SpringBoot/gs-spring-boot-docker/complete*"), e abra o arquivo *pom.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="3b362-136">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="3b362-137">Atualize a coleção `<properties>` no arquivo *pom.xml* com o nome de registro do Registro de Contêiner do Azure e a versão mais recente do [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="3b362-137">Update the `<properties>` collection in the *pom.xml* file with the registry name for your Azure Container Registry and the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="3b362-138">Atualize a coleção `<plugins>` no arquivo *pom.xml* para que `<plugin>` contenha o `jib-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="3b362-138">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the `jib-maven-plugin`.</span></span>

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="3b362-139">Navegue para o diretório do projeto completo de seu aplicativo Spring Boot, execute o seguinte comando para compilar a imagem e envie por push a imagem para o registro:</span><span class="sxs-lookup"><span data-stu-id="3b362-139">Navigate to the completed project directory for your Spring Boot application and run the following command to build the image and push the image to the registry:</span></span>

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> <span data-ttu-id="3b362-140">Devido à preocupação com a segurança da CLI do Azure e do Registro de Contêiner do Azure, a credencial criada pelo `az acr login` é válida por 1 hora; se você encontrar o erro *401 Não Autorizado*, poderá executar o comando `az acr login -n <your registry name>` novamente para autenticar-se outra vez.</span><span class="sxs-lookup"><span data-stu-id="3b362-140">Due to the security concern of Azure Cli and Azure Container Registry, the credential created by `az acr login` is valid for 1 hour, if you meet *401 Unauthorized* error, you can run the `az acr login -n <your registry name>` command again to reauthenticate.</span></span>
>

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="3b362-141">Criar um Cluster Kubernetes no AKS usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3b362-141">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="3b362-142">Criar um cluster Kubernetes no Serviço de Kubernetes do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b362-142">Create a Kubernetes cluster in Azure Kubernetes Service.</span></span> <span data-ttu-id="3b362-143">O comando a seguir cria um cluster *kubernetes* no grupo de recursos *wingtiptoys-kubernetes*, com *wingtiptoys-akscluster* como o nome do cluster e *wingtiptoys-kubernetes* como o prefixo DNS:</span><span class="sxs-lookup"><span data-stu-id="3b362-143">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-akscluster* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   <span data-ttu-id="3b362-144">Esse comando pode demorar algum tempo para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="3b362-144">This command may take a while to complete.</span></span>

1. <span data-ttu-id="3b362-145">Quando você estiver usando o Registro de Contêiner do Azure (ACR) com o Serviço de Kubernetes do Azure (AKS), precisará conceder acesso de pull do Serviço de Kubernetes do Azure ao Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b362-145">When you're using Azure Container Registry (ACR) with Azure Kubernetes Service (AKS), you need to grant Azure Kubernetes Service pull access to Azure Container Registry.</span></span> <span data-ttu-id="3b362-146">O Azure cria uma entidade de serviço padrão quando você cria um Serviço de Kubernetes do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b362-146">Azure creates a default service principal when you are creating Azure Kubernetes Service.</span></span> <span data-ttu-id="3b362-147">Execute os seguintes scripts em bash ou no Powershell para conceder acesso de AKS ao ACR; confira mais detalhes em [Autenticar com o Registro de Contêiner do Azure do Serviço de Kubernetes do Azure (AKS)].</span><span class="sxs-lookup"><span data-stu-id="3b362-147">Please run the following scripts in bash or Powershell to grant AKS access to ACR, see more details at [Authenticate with Azure Container Registry from Azure Kubernetes Service].</span></span>

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  <span data-ttu-id="3b362-148">-- ou --</span><span class="sxs-lookup"><span data-stu-id="3b362-148">-- or --</span></span>

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. <span data-ttu-id="3b362-149">Instalar `kubectl` usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b362-149">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="3b362-150">Os usuários de Linux podem ter que prefixar esse comando com `sudo`, já que ele implanta a CLI do Kubernetes em `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="3b362-150">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az aks install-cli
   ```

1. <span data-ttu-id="3b362-151">Baixe as informações de configuração do cluster para que possa gerenciá-lo na interface da Web do Kubernetes e `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="3b362-151">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="3b362-152">Implantar a imagem em seu cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3b362-152">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="3b362-153">Este tutorial implanta o aplicativo usando `kubectl` e depois permite que você explore a implantação por meio da interface da Web do Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="3b362-153">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-kubectl"></a><span data-ttu-id="3b362-154">Implantar com kubectl</span><span class="sxs-lookup"><span data-stu-id="3b362-154">Deploy with kubectl</span></span>

1. <span data-ttu-id="3b362-155">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="3b362-155">Open a command prompt.</span></span>

1. <span data-ttu-id="3b362-156">Execute seu contêiner no cluster Kubernetes usando o comando `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="3b362-156">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="3b362-157">Forneça um nome de serviço para seu aplicativo no Kubernetes e o nome de imagem completo.</span><span class="sxs-lookup"><span data-stu-id="3b362-157">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="3b362-158">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b362-158">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="3b362-159">Neste comando:</span><span class="sxs-lookup"><span data-stu-id="3b362-159">In this command:</span></span>

   * <span data-ttu-id="3b362-160">O nome do contêiner `gs-spring-boot-docker` é especificado imediatamente após o comando `run`</span><span class="sxs-lookup"><span data-stu-id="3b362-160">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="3b362-161">O parâmetro `--image` especifica a combinação de servidor de logon e nome da imagem como `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="3b362-161">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="3b362-162">Exponha seu cluster Kubernetes externamente usando o comando `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="3b362-162">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="3b362-163">Especifique o nome do serviço, a porta TCP voltada para o público usada para acessar o aplicativo e a porta de destino interna na qual seu aplicativo escuta.</span><span class="sxs-lookup"><span data-stu-id="3b362-163">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="3b362-164">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b362-164">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="3b362-165">Neste comando:</span><span class="sxs-lookup"><span data-stu-id="3b362-165">In this command:</span></span>

   * <span data-ttu-id="3b362-166">O nome do contêiner `gs-spring-boot-docker` é especificado imediatamente após o comando `expose deployment`</span><span class="sxs-lookup"><span data-stu-id="3b362-166">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="3b362-167">O parâmetro `--type` especifica que o cluster usa o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="3b362-167">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="3b362-168">O parâmetro `--port` especifica a porta TCP 80 voltada para o público.</span><span class="sxs-lookup"><span data-stu-id="3b362-168">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="3b362-169">Você acessa o aplicativo nessa porta.</span><span class="sxs-lookup"><span data-stu-id="3b362-169">You access the app on this port.</span></span>

   * <span data-ttu-id="3b362-170">O parâmetro `--target-port` especifica a porta TCP interna 8080.</span><span class="sxs-lookup"><span data-stu-id="3b362-170">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="3b362-171">O balanceador de carga encaminha solicitações ao seu aplicativo nesta porta.</span><span class="sxs-lookup"><span data-stu-id="3b362-171">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="3b362-172">Após a implantação do aplicativo no cluster, consulte o endereço IP externo e abra-o em seu navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="3b362-172">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Procurar aplicativo de exemplo no Azure][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="3b362-174">Implantar com a interface da Web do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3b362-174">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="3b362-175">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="3b362-175">Open a command prompt.</span></span>

1. <span data-ttu-id="3b362-176">Abra o site de configuração do cluster Kubernetes em seu navegador padrão:</span><span class="sxs-lookup"><span data-stu-id="3b362-176">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. <span data-ttu-id="3b362-177">Quando o site de configuração de Kubernetes abrir no navegador, clique no link para **implantar um aplicativo em contêiner**:</span><span class="sxs-lookup"><span data-stu-id="3b362-177">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Site de configuração do Kubernetes][KB01]

1. <span data-ttu-id="3b362-179">Quando a página **Criação de Recursos** for exibida, especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="3b362-179">When the **Resource Creation** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="3b362-180">a.</span><span class="sxs-lookup"><span data-stu-id="3b362-180">a.</span></span> <span data-ttu-id="3b362-181">Selecione **CRIAR UM APLICATIVO**.</span><span class="sxs-lookup"><span data-stu-id="3b362-181">Select **CREATE AN APP**.</span></span>

   <span data-ttu-id="3b362-182">b.</span><span class="sxs-lookup"><span data-stu-id="3b362-182">b.</span></span> <span data-ttu-id="3b362-183">Insira o nome do aplicativo Spring Boot para o **Nome do aplicativo**; por exemplo: "*gs-spring-boot-docker*".</span><span class="sxs-lookup"><span data-stu-id="3b362-183">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="3b362-184">c.</span><span class="sxs-lookup"><span data-stu-id="3b362-184">c.</span></span> <span data-ttu-id="3b362-185">Insira o servidor de logon e imagem do contêiner de antes na **Imagem do contêiner**; por exemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="3b362-185">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="3b362-186">d.</span><span class="sxs-lookup"><span data-stu-id="3b362-186">d.</span></span> <span data-ttu-id="3b362-187">Escolha **Externo** para o **Serviço**.</span><span class="sxs-lookup"><span data-stu-id="3b362-187">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="3b362-188">e.</span><span class="sxs-lookup"><span data-stu-id="3b362-188">e.</span></span> <span data-ttu-id="3b362-189">Especifique as portas internas e externas nas caixas de texto **Porta** e **Porta de destino**.</span><span class="sxs-lookup"><span data-stu-id="3b362-189">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Site de configuração do Kubernetes][KB02]


1. <span data-ttu-id="3b362-191">Clique em **Implantar** para implantar o contêiner.</span><span class="sxs-lookup"><span data-stu-id="3b362-191">Click **Deploy** to deploy the container.</span></span>

   ![Implantar Kubernetes][KB05]

1. <span data-ttu-id="3b362-193">Após a implantação de seu aplicativo, você verá o aplicativo Spring Boot listado em **Serviços**.</span><span class="sxs-lookup"><span data-stu-id="3b362-193">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Serviços Kubernetes][KB06]

1. <span data-ttu-id="3b362-195">Se você clicar no link para **Pontos de extremidade externos**, poderá ver o aplicativo Spring Boot em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="3b362-195">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Serviços Kubernetes][KB07]

   ![Procurar aplicativo de exemplo no Azure][SB02]

## <a name="next-steps"></a><span data-ttu-id="3b362-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b362-198">Next steps</span></span>

<span data-ttu-id="3b362-199">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b362-199">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b362-200">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="3b362-200">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="3b362-201">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3b362-201">Additional Resources</span></span>

<span data-ttu-id="3b362-202">Para obter mais informações sobre como usar o Spring Boot no Azure, confira o seguinte artigo:</span><span class="sxs-lookup"><span data-stu-id="3b362-202">For more information about using Spring Boot on Azure, see the following article:</span></span>

* [<span data-ttu-id="3b362-203">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="3b362-203">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

<span data-ttu-id="3b362-204">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Trabalhando com o Java e Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="3b362-204">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="3b362-205">Para saber mais sobre como implantar um aplicativo Java para Kubernetes com o Visual Studio Code, confira [Tutoriais de Java do Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="3b362-205">For more information about deploying a Java application to Kubernetes with Visual Studio Code, see [Visual Studio Code Java Tutorials].</span></span>

<span data-ttu-id="3b362-206">Para saber mais sobre o Spring Boot no projeto de exemplo do Docker, veja [Introdução ao Spring Boot no Docker].</span><span class="sxs-lookup"><span data-stu-id="3b362-206">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="3b362-207">Os links a seguir fornecem mais informações sobre como criar aplicativos Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="3b362-207">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="3b362-208">Para saber mais sobre como começar a criar um aplicativo Spring Boot simples, confira o Spring Initializr em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="3b362-208">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="3b362-209">Os links a seguir fornecem mais informações sobre como usar kubernetes com o Azure:</span><span class="sxs-lookup"><span data-stu-id="3b362-209">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="3b362-210">Comece com um cluster Kubernetes no Serviço de Kubernetes do Azure</span><span class="sxs-lookup"><span data-stu-id="3b362-210">Get started with a Kubernetes cluster in Azure Kubernetes Service</span></span>](/azure/aks/intro-kubernetes)

<span data-ttu-id="3b362-211">Saiba mais sobre como usar a interface de linha de comando Kubernetes no guia do usuário **kubectl** em <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="3b362-211">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="3b362-212">O site do Kubernetes tem vários artigos que abordam o uso de imagens em registros privados:</span><span class="sxs-lookup"><span data-stu-id="3b362-212">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="3b362-213">[Configurar contas de serviço para Pods]</span><span class="sxs-lookup"><span data-stu-id="3b362-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="3b362-214">[Namespaces]</span><span class="sxs-lookup"><span data-stu-id="3b362-214">[Namespaces]</span></span>
* <span data-ttu-id="3b362-215">[Extrair uma imagem de um registro privado]</span><span class="sxs-lookup"><span data-stu-id="3b362-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="3b362-216">Para obter mais exemplos sobre como usar imagens personalizadas do Docker com o Azure, veja [Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux].</span><span class="sxs-lookup"><span data-stu-id="3b362-216">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<span data-ttu-id="3b362-217">Para obter mais informações sobre como executar iterativamente e depurar os contêineres direto no Serviço de Kubernetes do Azure (AKS) com o Azure Dev Spaces, confira [Introdução ao Azure Dev Spaces com Java]</span><span class="sxs-lookup"><span data-stu-id="3b362-217">For more information about iteratively running and debugging containers directly in Azure Kubernetes Service (AKS) with Azure Dev Spaces, see [Get started on Azure Dev Spaces with Java]</span></span>

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[AKS (Serviço de Kubernetes do Azure)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure para desenvolvedores Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Trabalhando com o Java e Azure DevOps]: /azure/devops/java/
[Working with Azure DevOps and Java]: /azure/devops/java/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configurar contas de serviço para Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Extrair uma imagem de um registro privado]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[Autenticar com o Registro de Contêiner do Azure do Serviço de Kubernetes do Azure (AKS)]: /azure/container-registry/container-registry-auth-aks/
[Authenticate with Azure Container Registry from Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Tutoriais de Java do Visual Studio Code]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Visual Studio Code Java Tutorials]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Introdução ao Azure Dev Spaces com Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
[Get started on Azure Dev Spaces with Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
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
