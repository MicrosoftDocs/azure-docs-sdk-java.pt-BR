---
title: Implantar um aplicativo Spring Boot usando o plug-in Fabric8 Maven
description: Este tutorial orienta você pelas etapas para implantar um aplicativo Spring Boot no Microsoft Azure usando o plug-in Fabric8 para Apache Maven.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: yuwzho;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: f05dca50f84b27f157892d63cda02286c6755795
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090809"
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a><span data-ttu-id="151dd-103">Implantar um aplicativo Spring Boot usando o plug-in Fabric8 Maven</span><span class="sxs-lookup"><span data-stu-id="151dd-103">Deploy a Spring Boot app using the Fabric8 Maven Plugin</span></span>

<span data-ttu-id="151dd-104">O **[Fabric8]** é uma solução de software livre baseada em **[Kubernetes]**, que ajuda os desenvolvedores a criar aplicativos em contêineres do Linux.</span><span class="sxs-lookup"><span data-stu-id="151dd-104">**[Fabric8]** is an open-source solution that is built on **[Kubernetes]**, which helps developers create applications in Linux containers.</span></span>

<span data-ttu-id="151dd-105">Este tutorial mostra como usar o plug-in Fabric8 do Maven para desenvolver e implantar um aplicativo em um host do Linux no [Serviço de Contêiner do Azure (AKS)].</span><span class="sxs-lookup"><span data-stu-id="151dd-105">This tutorial walks you through using the Fabric8 plugin for Maven to develop to deploy an application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="151dd-106">pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="151dd-106">Prerequisites</span></span>

<span data-ttu-id="151dd-107">Para concluir as etapas deste tutorial, você precisa ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="151dd-107">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="151dd-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="151dd-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="151dd-109">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="151dd-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="151dd-110">Um [JDK (Java Developer Kit)] atualizado.</span><span class="sxs-lookup"><span data-stu-id="151dd-110">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="151dd-111">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="151dd-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="151dd-112">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="151dd-112">A [Git] client.</span></span>
* <span data-ttu-id="151dd-113">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="151dd-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="151dd-114">Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="151dd-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="151dd-115">Criar o aplicativo Web de Introdução ao Spring Boot no Docker</span><span class="sxs-lookup"><span data-stu-id="151dd-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="151dd-116">As etapas a seguir mostram como compilar um aplicativo Web Spring Boot e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="151dd-116">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="151dd-117">Abra um prompt de comando, crie um diretório local para conter o aplicativo e altere para o diretório. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   <span data-ttu-id="151dd-118">-- ou --</span><span class="sxs-lookup"><span data-stu-id="151dd-118">-- or --</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. <span data-ttu-id="151dd-119">Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório.</span><span class="sxs-lookup"><span data-stu-id="151dd-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="151dd-120">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-120">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   <span data-ttu-id="151dd-121">-- ou --</span><span class="sxs-lookup"><span data-stu-id="151dd-121">-- or --</span></span>
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. <span data-ttu-id="151dd-122">Use o Maven para compilar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="151dd-122">Use Maven to build and run the sample app.</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

1. <span data-ttu-id="151dd-123">Teste o aplicativo Web navegando até http://localhost:8080 ou com o seguinte comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="151dd-123">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="151dd-124">Você verá a mensagem **Hello Docker World** exibida.</span><span class="sxs-lookup"><span data-stu-id="151dd-124">You should see a **Hello Docker World** message displayed.</span></span>

   ![Procurar o aplicativo de exemplo localmente][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a><span data-ttu-id="151dd-126">Instalar a interface de linha de comando Kubernetes e criar um grupo de recursos do Azure usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="151dd-126">Install the Kubernetes command-line interface and create an Azure resource group using the Azure CLI</span></span>

1. <span data-ttu-id="151dd-127">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="151dd-127">Open a command prompt.</span></span>

1. <span data-ttu-id="151dd-128">Digite o seguinte comando para fazer logon na conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="151dd-128">Type the following command to log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="151dd-129">Siga as instruções para concluir o processo de logon</span><span class="sxs-lookup"><span data-stu-id="151dd-129">Follow the instructions to complete the login process</span></span>

   <span data-ttu-id="151dd-130">A CLI do Azure exibirá uma lista de suas contas, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-130">The Azure CLI will display a list of your accounts; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="151dd-131">Se você ainda não tiver a interface de linha de comando Kubernetes (`kubectl`) instalada, poderá instalar usando a CLI do Azure, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-131">If you do not already have the Kubernetes command-line interface (`kubectl`) installed, you can install using the Azure CLI; for example:</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="151dd-132">Os usuários de Linux podem ter que prefixar esse comando com `sudo`, já que ele implanta a CLI do Kubernetes em `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="151dd-132">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   >
   > <span data-ttu-id="151dd-133">Se você já tiver o `kubectl` instalado e sua versão do `kubectl` for muito antiga, poderá ver uma mensagem de erro semelhante ao exemplo a seguir quando tentar concluir as etapas listadas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="151dd-133">If you already have `kubectl`) installed and your version of `kubectl` is too old, you may see an error message similar to the following example when you attempt to complete the steps listed later in this article:</span></span>
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > <span data-ttu-id="151dd-134">Se isso acontecer, você precisará reinstalar `kubectl` para atualizar sua versão.</span><span class="sxs-lookup"><span data-stu-id="151dd-134">If this happens, you will need to reinstall `kubectl` to update your version.</span></span>
   >

1. <span data-ttu-id="151dd-135">Crie um grupo de recursos para os recursos do Azure que serão usados neste tutorial, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-135">Create a resource group for the Azure resources that you will use in this tutorial; for example:</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   <span data-ttu-id="151dd-136">Em que:</span><span class="sxs-lookup"><span data-stu-id="151dd-136">Where:</span></span>  
      * <span data-ttu-id="151dd-137">*wingtiptoys-kubernetes* é um nome exclusivo para o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="151dd-137">*wingtiptoys-kubernetes* is a unique name for your resource group</span></span>  
      * <span data-ttu-id="151dd-138">*westeurope* é uma localização geográfica apropriada para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="151dd-138">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="151dd-139">A CLI do Azure exibirá os resultados da criação do grupo de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-139">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a><span data-ttu-id="151dd-140">Criar um cluster Kubernetes usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="151dd-140">Create a Kubernetes cluster using the Azure CLI</span></span>

1. <span data-ttu-id="151dd-141">Crie um cluster Kubernetes no novo grupo de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-141">Create a Kubernetes cluster in your new resource group; for example:</span></span>  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   <span data-ttu-id="151dd-142">Em que:</span><span class="sxs-lookup"><span data-stu-id="151dd-142">Where:</span></span>  
      * <span data-ttu-id="151dd-143">*wingtiptoys kubernetes* é o nome do seu grupo de recursos de antes neste artigo</span><span class="sxs-lookup"><span data-stu-id="151dd-143">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="151dd-144">*wingtiptoys-cluster* é um nome exclusivo para o cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="151dd-144">*wingtiptoys-cluster* is a unique name for your Kubernetes cluster</span></span>
      * <span data-ttu-id="151dd-145">*wingtiptoys* é um nome DNS exclusivo para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="151dd-145">*wingtiptoys* is a unique name DNS name for your application</span></span>

   <span data-ttu-id="151dd-146">A CLI do Azure exibirá os resultados da criação do cluster, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-146">The Azure CLI will display the results of your cluster creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. <span data-ttu-id="151dd-147">Baixe suas credenciais para o novo cluster Kubernetes, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-147">Download your credentials for your new Kubernetes cluster; for example:</span></span>  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. <span data-ttu-id="151dd-148">Verifique sua conexão com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="151dd-148">Verify your connection with the following command:</span></span>
   ```shell 
   kubectl get nodes
   ```

   <span data-ttu-id="151dd-149">Você verá uma lista de nós e status semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="151dd-149">You should see a list of nodes and statuses like the following example:</span></span>

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="151dd-150">Criar um Registro de Contêiner do Azure privado usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="151dd-150">Create a private Azure container registry using the Azure CLI</span></span>

1. <span data-ttu-id="151dd-151">Crie um Registro de Contêiner do Azure privado no grupo de recursos para hospedar a imagem de Docker, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-151">Create a private Azure container registry in your resource group to host your Docker image; for example:</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="151dd-152">Em que:</span><span class="sxs-lookup"><span data-stu-id="151dd-152">Where:</span></span>

   | <span data-ttu-id="151dd-153">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="151dd-153">Parameter</span></span> | <span data-ttu-id="151dd-154">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="151dd-154">Description</span></span> |
   |---|---|
   | `wingtiptoys-kubernetes` | <span data-ttu-id="151dd-155">Especifica o nome do seu grupo de recursos referido anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="151dd-155">Specifies the name of your resource group from earlier in this article.</span></span> |
   | `wingtiptoysregistry` | <span data-ttu-id="151dd-156">Especifica um nome exclusivo para o seu registro privado.</span><span class="sxs-lookup"><span data-stu-id="151dd-156">Specifies a unique name for your private registry.</span></span> |
   | `westeurope` | <span data-ttu-id="151dd-157">Especifica uma localização geográfica apropriada para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="151dd-157">Specifies an appropriate geographic location for your application.</span></span> |

   <span data-ttu-id="151dd-158">A CLI do Azure exibirá os resultados da criação do Registro, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-158">The Azure CLI will display the results of your registry creation; for example:</span></span>  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

2. <span data-ttu-id="151dd-159">Recupere a senha de seu registro de contêiner na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="151dd-159">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   <span data-ttu-id="151dd-160">A CLI do Azure exibirá a senha do Registro, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-160">The Azure CLI will display the password for your registry; for example:</span></span>  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

3. <span data-ttu-id="151dd-161">Navegue até o diretório de configuração de sua instalação do Maven (padrão ~/.m2/ ou C:\Usuários\nomedeusuário\.m2) e abra o arquivo *settings.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="151dd-161">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

4. <span data-ttu-id="151dd-162">Adicione o nome de usuário, a senha e a URL do Registro de Contêiner do Azure a uma nova coleção `<server>` no arquivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="151dd-162">Add your Azure Container Registry URL, username and password to a new `<server>` collection in the *settings.xml* file.</span></span>
   <span data-ttu-id="151dd-163">`id` e `username` são os nomes do registro.</span><span class="sxs-lookup"><span data-stu-id="151dd-163">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="151dd-164">Use o valor `password` do comando anterior (sem as aspas).</span><span class="sxs-lookup"><span data-stu-id="151dd-164">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

5. <span data-ttu-id="151dd-165">Navegue até o diretório do projeto completo de seu aplicativo Spring Boot (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") e abra o arquivo *pom.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="151dd-165">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

6. <span data-ttu-id="151dd-166">Atualize a coleção `<properties>` no arquivo *pom.xml* com o valor do servidor de logon para seu Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="151dd-166">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

7. <span data-ttu-id="151dd-167">Atualize a coleção `<plugins>` no arquivo *pom.xml* para que o `<plugin>` contenha o endereço do servidor de logon e o nome de registro para seu Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="151dd-167">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
     <groupId>com.spotify</groupId>
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

8. <span data-ttu-id="151dd-168">Navegue até o diretório do projeto completo de seu aplicativo Spring Boot e execute o seguinte comando do Maven para compilar o contêiner do Docker e enviar por push a imagem ao Registro:</span><span class="sxs-lookup"><span data-stu-id="151dd-168">Navigate to the completed project directory for your Spring Boot application, and run the following Maven command to build the Docker container and push the image to your registry:</span></span>

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   <span data-ttu-id="151dd-169">O Maven exibirá os resultados de seu build, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-169">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a><span data-ttu-id="151dd-170">Configurar seu aplicativo Spring Boot para usar o plug-in Fabric8 Maven</span><span class="sxs-lookup"><span data-stu-id="151dd-170">Configure your Spring Boot app to use the Fabric8 Maven plugin</span></span>

1. <span data-ttu-id="151dd-171">Navegue até o diretório do projeto completo de seu aplicativo Spring Boot (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") e abra o arquivo *pom.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="151dd-171">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="151dd-172">Atualize a coleção `<plugins>` no arquivo *pom.xml* para adicionar o plug-in Fabric8 Maven:</span><span class="sxs-lookup"><span data-stu-id="151dd-172">Update the `<plugins>` collection in the *pom.xml* file to add the Fabric8 Maven plugin:</span></span>

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="151dd-173">Navegue até o diretório de origem principal do aplicativo Spring Boot (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" ou "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*") e crie uma nova pasta chamada "*fabric8*".</span><span class="sxs-lookup"><span data-stu-id="151dd-173">Navigate to the main source directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*"), and create a new folder named "*fabric8*".</span></span>

1. <span data-ttu-id="151dd-174">Crie três arquivos de fragmento YAML na nova pasta *fabric8*:</span><span class="sxs-lookup"><span data-stu-id="151dd-174">Create three YAML fragment files in the new *fabric8* folder:</span></span>

   <span data-ttu-id="151dd-175">a.</span><span class="sxs-lookup"><span data-stu-id="151dd-175">a.</span></span> <span data-ttu-id="151dd-176">Crie um arquivo chamado **deployment.yml** com o conteúdo abaixo:</span><span class="sxs-lookup"><span data-stu-id="151dd-176">Create a file named **deployment.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   <span data-ttu-id="151dd-177">b.</span><span class="sxs-lookup"><span data-stu-id="151dd-177">b.</span></span> <span data-ttu-id="151dd-178">Crie um arquivo chamado **secrets.yml** com o conteúdo abaixo:</span><span class="sxs-lookup"><span data-stu-id="151dd-178">Create a file named **secrets.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   <span data-ttu-id="151dd-179">c.</span><span class="sxs-lookup"><span data-stu-id="151dd-179">c.</span></span> <span data-ttu-id="151dd-180">Crie um arquivo chamado **service.yml** com o conteúdo abaixo:</span><span class="sxs-lookup"><span data-stu-id="151dd-180">Create a file named **service.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. <span data-ttu-id="151dd-181">Execute o seguinte comando Maven para criar o arquivo de lista de recursos do Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="151dd-181">Run the following Maven command to build the Kubernetes resource list file:</span></span>

   ```shell
   mvn fabric8:resource
   ```

   <span data-ttu-id="151dd-182">Este comando mescla todos os arquivos yaml de recursos do Kubernetes na pasta *src/main/fabric8* para um arquivo YAML que contém a lista de recursos do Kubernetes, que pode ser aplicado ao diretório de cluster do Kubernetes ou exportado para um gráfico Helm.</span><span class="sxs-lookup"><span data-stu-id="151dd-182">This command merges all Kubernetes resource yaml files under the *src/main/fabric8* folder to a YAML file that contains a Kubernetes resource list, which can be applied to Kubernetes cluster directly or export to a helm chart.</span></span>

   <span data-ttu-id="151dd-183">O Maven exibirá os resultados de seu build, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-183">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="151dd-184">Execute o comando Maven a seguir para aplicar o arquivo da lista de recursos ao cluster Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="151dd-184">Run the following Maven command to apply the resource list file to your Kubernetes cluster:</span></span>

   ```shell
   mvn fabric8:apply
   ```

   <span data-ttu-id="151dd-185">O Maven exibirá os resultados de seu build, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-185">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="151dd-186">Após a implantação do aplicativo no cluster, consulte o endereço IP externo usando o aplicativo `kubectl`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-186">Once the app is deployed to the cluster, query the external IP address using the `kubectl` application; for example:</span></span>
   ```shell
   kubectl get svc -w
   ```

   <span data-ttu-id="151dd-187">`kubectl` exibirá os endereços IP internos e externos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-187">`kubectl` will display your internal and external IP addresses; for example:</span></span>

   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```

   <span data-ttu-id="151dd-188">Você pode usar o endereço IP externo para abrir o aplicativo em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="151dd-188">You can use the external IP address to open your application in a web browser.</span></span>

   ![Procurar o aplicativo de exemplo externamente][SB02]

## <a name="delete-your-kubernetes-cluster"></a><span data-ttu-id="151dd-190">Excluir o cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="151dd-190">Delete your Kubernetes cluster</span></span>

<span data-ttu-id="151dd-191">Quando o cluster Kubernetes não for mais necessário, você poderá usar o comando `az group delete` para remover o grupo de recursos, o que removerá todos os seus recursos relacionados, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="151dd-191">When your Kubernetes cluster is no longer needed, you can use the `az group delete` command to remove the resource group, which will remove all of its related resources; for example:</span></span>

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a><span data-ttu-id="151dd-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="151dd-192">Next steps</span></span>

<span data-ttu-id="151dd-193">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="151dd-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="151dd-194">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="151dd-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="151dd-195">Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="151dd-195">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)
* [<span data-ttu-id="151dd-196">Implantar um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="151dd-196">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="151dd-197">Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="151dd-197">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="151dd-198">Para obter mais detalhes sobre o Spring Boot no projeto de exemplo do Docker, consulte [Introdução ao Spring Boot no Docker].</span><span class="sxs-lookup"><span data-stu-id="151dd-198">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="151dd-199">Para obter ajuda na introdução a seus próprios aplicativos Spring Boot, confira **Spring Initializr** em <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="151dd-199">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at <https://start.spring.io/>.</span></span>

<span data-ttu-id="151dd-200">Para obter mais informações de introdução sobre como criar um aplicativo Spring Boot simples, consulte o Spring Initializr em <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="151dd-200">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at <https://start.spring.io/>.</span></span>

<span data-ttu-id="151dd-201">Para obter mais exemplos sobre como usar imagens personalizadas do Docker com o Azure, veja [Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux].</span><span class="sxs-lookup"><span data-stu-id="151dd-201">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Serviço de Contêiner do Azure (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[Benefícios do assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
