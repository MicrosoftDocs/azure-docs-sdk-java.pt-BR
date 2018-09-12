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
ms.date: 07/30/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 336af51bbdf5d2f843c3868ebc2358e128daaeaa
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324322"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a><span data-ttu-id="abbe5-103">Implantar um aplicativo MicroProfile na nuvem com Docker e Azure</span><span class="sxs-lookup"><span data-stu-id="abbe5-103">Deploy a MicroProfile application to the cloud with Docker and Azure</span></span>

<span data-ttu-id="abbe5-104">Este artigo demonstra como empacotar um aplicativo [MicroProfile.io] em um contêiner do Docker e executá-lo nas Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="abbe5-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
>
> <span data-ttu-id="abbe5-105">Este procedimento funciona com qualquer implementação de MicroProfile.io, desde que a imagem de contêiner do Docker seja executada automaticamente (ou seja, inclui o tempo de execução).</span><span class="sxs-lookup"><span data-stu-id="abbe5-105">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abbe5-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="abbe5-106">Prerequisites</span></span>

<span data-ttu-id="abbe5-107">Para concluir as etapas neste tutorial, você precisará ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="abbe5-107">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="abbe5-108">Uma assinatura do Azure; se ainda não tiver uma, inscreva-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="abbe5-108">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="abbe5-109">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="abbe5-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="abbe5-110">Um [JDK (Java Development Kit)] versão 1.8 ou posterior atualizado.</span><span class="sxs-lookup"><span data-stu-id="abbe5-110">An up-to-date [Java Development Kit (JDK)], version 1.8 or later.</span></span>
* <span data-ttu-id="abbe5-111">A ferramenta de build do [Maven] do Apache (versão 3+).</span><span class="sxs-lookup"><span data-stu-id="abbe5-111">Apache's [Maven] build tool (version 3+).</span></span>
* <span data-ttu-id="abbe5-112">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="abbe5-112">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="abbe5-113">Exemplo do MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="abbe5-113">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="abbe5-114">Para este artigo, usaremos o exemplo [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure):</span><span class="sxs-lookup"><span data-stu-id="abbe5-114">For this article, we will use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample:</span></span>

### <a name="clone-build-and-run-locally"></a><span data-ttu-id="abbe5-115">Clonar, compilar e executar localmente</span><span class="sxs-lookup"><span data-stu-id="abbe5-115">Clone, build, and run locally</span></span>

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

<span data-ttu-id="abbe5-116">Você pode testar o aplicativo chamando `curl` ou visitando através de um [navegador](http://localhost:8080/api/hello):</span><span class="sxs-lookup"><span data-stu-id="abbe5-116">You can test the application by calling `curl` or visiting through a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a><span data-ttu-id="abbe5-117">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="abbe5-117">Deploy to Azure</span></span>

<span data-ttu-id="abbe5-118">Agora vamos colocar esse aplicativo na nuvem usando os serviços [Instâncias de Contêiner do Azure] e [Registro de Contêiner do Azure].</span><span class="sxs-lookup"><span data-stu-id="abbe5-118">Now let's bring this application to the cloud using [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="abbe5-119">Compilar uma imagem do docker</span><span class="sxs-lookup"><span data-stu-id="abbe5-119">Build a Docker image</span></span>

<span data-ttu-id="abbe5-120">O exemplo de projeto já fornece um Dockerfile que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="abbe5-120">The sample project already provides a Dockerfile you can use.</span></span> <span data-ttu-id="abbe5-121">No entanto, você não precisa do Docker instalado, já que usaremos o recurso de Build do Registro de Contêiner do Azure para compilar a imagem na nuvem.</span><span class="sxs-lookup"><span data-stu-id="abbe5-121">You don't need Docker installed though, as we will use Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="abbe5-122">Para compilar a imagem e se preparar para compilá-la no Azure, você terá que seguir estas etapas:</span><span class="sxs-lookup"><span data-stu-id="abbe5-122">To build the image and be ready to run on Azure, you will have to follow these steps:</span></span>

1. <span data-ttu-id="abbe5-123">Instalar e fazer logon com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="abbe5-123">Install and log in with Azure CLI</span></span>
1. <span data-ttu-id="abbe5-124">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="abbe5-124">Create an Azure Resource Group</span></span>
1. <span data-ttu-id="abbe5-125">Criar um Registro de Contêiner do Azure (ACR)</span><span class="sxs-lookup"><span data-stu-id="abbe5-125">Create an Azure Container Registry (ACR)</span></span>
1. <span data-ttu-id="abbe5-126">Criar a imagem de Docker</span><span class="sxs-lookup"><span data-stu-id="abbe5-126">Build the Docker image</span></span>
1. <span data-ttu-id="abbe5-127">Publicar a imagem do Docker no ACR criado anteriormente</span><span class="sxs-lookup"><span data-stu-id="abbe5-127">Publish the Docker image to the ACR created before</span></span>
1. <span data-ttu-id="abbe5-128">(Opcionalmente) Compilar e publicar no ACR com um comando</span><span class="sxs-lookup"><span data-stu-id="abbe5-128">(Optionally) Build and publish to ACR in one command</span></span>


#### <a name="set-up-azure-cli"></a><span data-ttu-id="abbe5-129">Configurar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="abbe5-129">Set up Azure CLI</span></span>

<span data-ttu-id="abbe5-130">Verifique se você tem uma assinatura do Azure, [CLI do Azure instalada](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), e que você está autenticado na sua conta:</span><span class="sxs-lookup"><span data-stu-id="abbe5-130">Make sure you have an Azure subscription, [Azure CLI installed](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you are authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="abbe5-131">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="abbe5-131">Create a Resource Group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="abbe5-132">Cria uma instância do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="abbe5-132">Create an Azure Container Registry instance</span></span>

<span data-ttu-id="abbe5-133">Esse comando criará um registro de contêiner globalmente exclusivo (se tudo der certo) usando um nome básico com um número aleatório.</span><span class="sxs-lookup"><span data-stu-id="abbe5-133">This command will create a globally unique (hopefully) container registry using a basic name with a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="abbe5-134">Criar a imagem de Docker</span><span class="sxs-lookup"><span data-stu-id="abbe5-134">Build the Docker image</span></span>

<span data-ttu-id="abbe5-135">Enquanto você pode facilmente criar a imagem do Docker localmente usando o próprio Docker, você talvez queira considerar criá-lo na Nuvem por alguns motivos:</span><span class="sxs-lookup"><span data-stu-id="abbe5-135">While you can easily build the Docker image locally using Docker itself, you may want to consider building it in the Cloud for few reasons:</span></span>

1. <span data-ttu-id="abbe5-136">Não há necessidade de instalar o Docker localmente</span><span class="sxs-lookup"><span data-stu-id="abbe5-136">No need to install Docker locally</span></span>
1. <span data-ttu-id="abbe5-137">Muito mais rápido, já que a compilação ocorrerá em outro lugar (com exceção de tempo de carregamento do contexto)</span><span class="sxs-lookup"><span data-stu-id="abbe5-137">Much faster since build will happen elsewhere (except for context upload time)</span></span>
1. <span data-ttu-id="abbe5-138">O processo na nuvem tem acesso à Internet mais rápida, portanto, os downloads são mais rápidos</span><span class="sxs-lookup"><span data-stu-id="abbe5-138">Process in the Cloud has access to faster Internet, therefore faster downloads</span></span>
1. <span data-ttu-id="abbe5-139">A imagem vai diretamente para o Registro de Contêiner</span><span class="sxs-lookup"><span data-stu-id="abbe5-139">Image goes directly into the Container Registry</span></span>

<span data-ttu-id="abbe5-140">Por esses motivos, vamos criar a imagem usando o recurso de [Build do Registro de Contêiner do Azure]:</span><span class="sxs-lookup"><span data-stu-id="abbe5-140">Because of these reasons, we will build the image using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a><span data-ttu-id="abbe5-141">Implantar a imagem do Docker do Registro de Contêiner do Azure (ACR) nas Instâncias de Contêiner (ACI)</span><span class="sxs-lookup"><span data-stu-id="abbe5-141">Deploy Docker Image from Azure Container Registry (ACR) into Container Instances (ACI)</span></span>

<span data-ttu-id="abbe5-142">Agora que a imagem está disponível em seu ACR, vamos enviar por push e instanciar uma instância de contêiner na ACI.</span><span class="sxs-lookup"><span data-stu-id="abbe5-142">Now that the image is available on your ACR, let's push and instanciate a container instance on ACI.</span></span> <span data-ttu-id="abbe5-143">Mas primeiro, é preciso certificar-se de que podemos autenticar para o ACR:</span><span class="sxs-lookup"><span data-stu-id="abbe5-143">But first, we need to make sure we can authenticate into the ACR:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="abbe5-144">Testar seu aplicativo MicroProfile implantado</span><span class="sxs-lookup"><span data-stu-id="abbe5-144">Test Your Deployed MicroProfile Application</span></span>

<span data-ttu-id="abbe5-145">Seu aplicativo agora deve estar em execução.</span><span class="sxs-lookup"><span data-stu-id="abbe5-145">Your application should now be up and running.</span></span> <span data-ttu-id="abbe5-146">Para testá-lo a partir da linha de comando, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="abbe5-146">To test it from the command-line, try the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="abbe5-147">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="abbe5-147">Congratulations!</span></span> <span data-ttu-id="abbe5-148">Você compilou e implantou um aplicativo MicroProfile como um contêiner do Docker no Microsoft Azure com êxito.</span><span class="sxs-lookup"><span data-stu-id="abbe5-148">You have successfuly built and deployed a MicroProfile application as a Docker container onto Microsoft Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abbe5-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abbe5-149">Next steps</span></span>

<span data-ttu-id="abbe5-150">Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="abbe5-150">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* [<span data-ttu-id="abbe5-151">Faça logon no Azure na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="abbe5-151">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Build do Registro de Contêiner do Azure]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[JDK (Java Development Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[Java Development Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[Instâncias de Contêiner do Azure]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Registro de Contêiner do Azure]:  https://docs.microsoft.com/azure/container-registry
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry