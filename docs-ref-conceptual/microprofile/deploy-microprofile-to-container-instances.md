---
title: Implantar um aplicativo MicroProfile na nuvem com Docker e Azure
description: Saiba como implantar um aplicativo MicroProfile na nuvem usando Instâncias de Contêiner do Azure e Docker.
services: container-instances;container-retistry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 22870b7ba32f115e7270c63d1bf42cbfc6531d7e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338780"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a><span data-ttu-id="aa8be-103">Implantar um aplicativo MicroProfile na nuvem com Docker e Azure</span><span class="sxs-lookup"><span data-stu-id="aa8be-103">Deploy a MicroProfile application to the cloud with Docker and Azure</span></span>

<span data-ttu-id="aa8be-104">Este artigo demonstra como empacotar um aplicativo [MicroProfile.io] em um contêiner do Docker e executá-lo nas Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa8be-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
>
> <span data-ttu-id="aa8be-105">Este procedimento funciona com qualquer implementação de MicroProfile.io, desde que a imagem de contêiner do Docker seja executada automaticamente (ou seja, inclui o tempo de execução).</span><span class="sxs-lookup"><span data-stu-id="aa8be-105">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa8be-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aa8be-106">Prerequisites</span></span>

<span data-ttu-id="aa8be-107">Para concluir as etapas neste tutorial, você precisará ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="aa8be-107">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="aa8be-108">Uma assinatura do Azure; se ainda não tiver uma, inscreva-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="aa8be-108">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="aa8be-109">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="aa8be-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="aa8be-110">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="aa8be-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="aa8be-111">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="aa8be-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="aa8be-112">A ferramenta de build do [Maven] do Apache (versão 3+).</span><span class="sxs-lookup"><span data-stu-id="aa8be-112">Apache's [Maven] build tool (version 3+).</span></span>
* <span data-ttu-id="aa8be-113">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="aa8be-113">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="aa8be-114">Exemplo do MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="aa8be-114">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="aa8be-115">Para este artigo, usaremos o exemplo [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure):</span><span class="sxs-lookup"><span data-stu-id="aa8be-115">For this article, we will use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample:</span></span>

### <a name="clone-build-and-run-locally"></a><span data-ttu-id="aa8be-116">Clonar, compilar e executar localmente</span><span class="sxs-lookup"><span data-stu-id="aa8be-116">Clone, build, and run locally</span></span>

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

<span data-ttu-id="aa8be-117">Você pode testar o aplicativo chamando `curl` ou visitando através de um [navegador](http://localhost:8080/api/hello):</span><span class="sxs-lookup"><span data-stu-id="aa8be-117">You can test the application by calling `curl` or visiting through a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a><span data-ttu-id="aa8be-118">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="aa8be-118">Deploy to Azure</span></span>

<span data-ttu-id="aa8be-119">Agora vamos colocar esse aplicativo na nuvem usando os serviços [Instâncias de Contêiner do Azure] e [Registro de Contêiner do Azure].</span><span class="sxs-lookup"><span data-stu-id="aa8be-119">Now let's bring this application to the cloud using [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="aa8be-120">Compilar uma imagem do docker</span><span class="sxs-lookup"><span data-stu-id="aa8be-120">Build a Docker image</span></span>

<span data-ttu-id="aa8be-121">O exemplo de projeto já fornece um Dockerfile que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="aa8be-121">The sample project already provides a Dockerfile you can use.</span></span> <span data-ttu-id="aa8be-122">No entanto, você não precisa do Docker instalado, já que usaremos o recurso de Build do Registro de Contêiner do Azure para compilar a imagem na nuvem.</span><span class="sxs-lookup"><span data-stu-id="aa8be-122">You don't need Docker installed though, as we will use Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="aa8be-123">Para compilar a imagem e se preparar para compilá-la no Azure, você terá que seguir estas etapas:</span><span class="sxs-lookup"><span data-stu-id="aa8be-123">To build the image and be ready to run on Azure, you will have to follow these steps:</span></span>

1. <span data-ttu-id="aa8be-124">Instalar e fazer logon com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aa8be-124">Install and log in with Azure CLI</span></span>
1. <span data-ttu-id="aa8be-125">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="aa8be-125">Create an Azure Resource Group</span></span>
1. <span data-ttu-id="aa8be-126">Criar um Registro de Contêiner do Azure (ACR)</span><span class="sxs-lookup"><span data-stu-id="aa8be-126">Create an Azure Container Registry (ACR)</span></span>
1. <span data-ttu-id="aa8be-127">Criar a imagem de Docker</span><span class="sxs-lookup"><span data-stu-id="aa8be-127">Build the Docker image</span></span>
1. <span data-ttu-id="aa8be-128">Publicar a imagem do Docker no ACR criado anteriormente</span><span class="sxs-lookup"><span data-stu-id="aa8be-128">Publish the Docker image to the ACR created before</span></span>
1. <span data-ttu-id="aa8be-129">(Opcionalmente) Compilar e publicar no ACR com um comando</span><span class="sxs-lookup"><span data-stu-id="aa8be-129">(Optionally) Build and publish to ACR in one command</span></span>


#### <a name="set-up-azure-cli"></a><span data-ttu-id="aa8be-130">Configurar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aa8be-130">Set up Azure CLI</span></span>

<span data-ttu-id="aa8be-131">Verifique se você tem uma assinatura do Azure, [CLI do Azure instalada](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), e que você está autenticado na sua conta:</span><span class="sxs-lookup"><span data-stu-id="aa8be-131">Make sure you have an Azure subscription, [Azure CLI installed](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you are authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="aa8be-132">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="aa8be-132">Create a Resource Group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="aa8be-133">Cria uma instância do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="aa8be-133">Create an Azure Container Registry instance</span></span>

<span data-ttu-id="aa8be-134">Esse comando criará um registro de contêiner globalmente exclusivo (se tudo der certo) usando um nome básico com um número aleatório.</span><span class="sxs-lookup"><span data-stu-id="aa8be-134">This command will create a globally unique (hopefully) container registry using a basic name with a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="aa8be-135">Criar a imagem de Docker</span><span class="sxs-lookup"><span data-stu-id="aa8be-135">Build the Docker image</span></span>

<span data-ttu-id="aa8be-136">Enquanto você pode facilmente criar a imagem do Docker localmente usando o próprio Docker, você talvez queira considerar criá-lo na Nuvem por alguns motivos:</span><span class="sxs-lookup"><span data-stu-id="aa8be-136">While you can easily build the Docker image locally using Docker itself, you may want to consider building it in the Cloud for few reasons:</span></span>

1. <span data-ttu-id="aa8be-137">Não há necessidade de instalar o Docker localmente</span><span class="sxs-lookup"><span data-stu-id="aa8be-137">No need to install Docker locally</span></span>
1. <span data-ttu-id="aa8be-138">Muito mais rápido, já que a compilação ocorrerá em outro lugar (com exceção de tempo de carregamento do contexto)</span><span class="sxs-lookup"><span data-stu-id="aa8be-138">Much faster since build will happen elsewhere (except for context upload time)</span></span>
1. <span data-ttu-id="aa8be-139">O processo na nuvem tem acesso à Internet mais rápida, portanto, os downloads são mais rápidos</span><span class="sxs-lookup"><span data-stu-id="aa8be-139">Process in the Cloud has access to faster Internet, therefore faster downloads</span></span>
1. <span data-ttu-id="aa8be-140">A imagem vai diretamente para o Registro de Contêiner</span><span class="sxs-lookup"><span data-stu-id="aa8be-140">Image goes directly into the Container Registry</span></span>

<span data-ttu-id="aa8be-141">Por esses motivos, vamos criar a imagem usando o recurso de [Build do Registro de Contêiner do Azure]:</span><span class="sxs-lookup"><span data-stu-id="aa8be-141">Because of these reasons, we will build the image using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a><span data-ttu-id="aa8be-142">Implantar a imagem do Docker do Registro de Contêiner do Azure (ACR) nas Instâncias de Contêiner (ACI)</span><span class="sxs-lookup"><span data-stu-id="aa8be-142">Deploy Docker Image from Azure Container Registry (ACR) into Container Instances (ACI)</span></span>

<span data-ttu-id="aa8be-143">Agora que a imagem está disponível em seu ACR, vamos enviar por push e instanciar uma instância de contêiner na ACI.</span><span class="sxs-lookup"><span data-stu-id="aa8be-143">Now that the image is available on your ACR, let's push and instanciate a container instance on ACI.</span></span> <span data-ttu-id="aa8be-144">Mas primeiro, é preciso certificar-se de que podemos autenticar para o ACR:</span><span class="sxs-lookup"><span data-stu-id="aa8be-144">But first, we need to make sure we can authenticate into the ACR:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="aa8be-145">Testar seu aplicativo MicroProfile implantado</span><span class="sxs-lookup"><span data-stu-id="aa8be-145">Test Your Deployed MicroProfile Application</span></span>

<span data-ttu-id="aa8be-146">Seu aplicativo agora deve estar em execução.</span><span class="sxs-lookup"><span data-stu-id="aa8be-146">Your application should now be up and running.</span></span> <span data-ttu-id="aa8be-147">Para testá-lo a partir da linha de comando, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="aa8be-147">To test it from the command-line, try the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="aa8be-148">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="aa8be-148">Congratulations!</span></span> <span data-ttu-id="aa8be-149">Você compilou e implantou um aplicativo MicroProfile como um contêiner do Docker no Microsoft Azure com êxito.</span><span class="sxs-lookup"><span data-stu-id="aa8be-149">You have successfuly built and deployed a MicroProfile application as a Docker container onto Microsoft Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa8be-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa8be-150">Next steps</span></span>

<span data-ttu-id="aa8be-151">Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa8be-151">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* [<span data-ttu-id="aa8be-152">Faça logon no Azure na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aa8be-152">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Build do Registro de Contêiner do Azure]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Instâncias de Contêiner do Azure]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Registro de Contêiner do Azure]:  https://docs.microsoft.com/azure/container-registry
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry