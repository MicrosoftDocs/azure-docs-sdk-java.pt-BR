---
title: Implantar um aplicativo do MicroProfile na nuvem usando o Docker e o Azure
description: Saiba como implantar um aplicativo do MicroProfile na nuvem usando o Docker e as Instâncias de Contêiner do Azure.
services: container-instances;container-registry
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
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533609"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a><span data-ttu-id="653e1-103">Implantar um aplicativo do MicroProfile na nuvem usando o Docker e o Azure</span><span class="sxs-lookup"><span data-stu-id="653e1-103">Deploy a MicroProfile app to the cloud by using Docker and Azure</span></span>

<span data-ttu-id="653e1-104">Este artigo demonstra como empacotar um aplicativo [MicroProfile.io] em um contêiner do Docker e executá-lo nas Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="653e1-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
> <span data-ttu-id="653e1-105">Este procedimento funciona com qualquer implementação do MicroProfile.io, desde que a imagem de contêiner do Docker seja autoexecutável (ou seja, a imagem inclui o tempo de execução).</span><span class="sxs-lookup"><span data-stu-id="653e1-105">This procedure works with any implementation of MicroProfile.io, as long as the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="653e1-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="653e1-106">Prerequisites</span></span>

<span data-ttu-id="653e1-107">Para concluir este tutorial, você precisará dos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="653e1-107">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="653e1-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="653e1-108">An Azure subscription.</span></span> <span data-ttu-id="653e1-109">Caso ainda não tenha uma assinatura do Azure, inscreva-se em uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="653e1-109">If you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="653e1-110">A [CLI do Azure] instalada.</span><span class="sxs-lookup"><span data-stu-id="653e1-110">The [Azure CLI], installed.</span></span>
* <span data-ttu-id="653e1-111">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="653e1-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="653e1-112">Para obter mais informações sobre os JDKs disponíveis para uso durante o desenvolvimento no Azure, confira [Suporte de longo prazo do Java para o Azure e o Azure Stack](https://aka.ms/azure-jdks).</span><span class="sxs-lookup"><span data-stu-id="653e1-112">For more information about the JDKs that are available to use when you develop on Azure, see [Java long-term support for Azure and Azure Stack](https://aka.ms/azure-jdks).</span></span>
* <span data-ttu-id="653e1-113">A ferramenta de build [Apache Maven] (versão 3 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="653e1-113">The [Apache Maven] build tool (version 3 or later).</span></span>
* <span data-ttu-id="653e1-114">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="653e1-114">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="653e1-115">Exemplo do MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="653e1-115">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="653e1-116">Neste artigo, você usará a amostra [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="653e1-116">In this article, you use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample.</span></span> <span data-ttu-id="653e1-117">Clone, compile e execute-a localmente usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="653e1-117">Clone, build, and run it locally by using the following commands:</span></span>

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

<span data-ttu-id="653e1-118">Teste o aplicativo chamando `curl` ou usando um [navegador](http://localhost:8080/api/hello):</span><span class="sxs-lookup"><span data-stu-id="653e1-118">You can test the application by calling `curl` or by using a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="653e1-119">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="653e1-119">Deploy the app to Azure</span></span>

<span data-ttu-id="653e1-120">Agora leve esse aplicativo ao Azure usando os serviços [Instâncias de Contêiner do Azure] e [Registro de Contêiner do Azure].</span><span class="sxs-lookup"><span data-stu-id="653e1-120">Now bring this application to Azure by using the [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="653e1-121">Compilar uma imagem do docker</span><span class="sxs-lookup"><span data-stu-id="653e1-121">Build a Docker image</span></span>

<span data-ttu-id="653e1-122">O projeto de exemplo fornece um Dockerfile que você poderá usar.</span><span class="sxs-lookup"><span data-stu-id="653e1-122">The sample project provides a Dockerfile that you can use.</span></span> <span data-ttu-id="653e1-123">No entanto, você não precisa ter o Docker instalado, pois usará o recurso Build do Registro de Contêiner do Azure para compilar a imagem na nuvem.</span><span class="sxs-lookup"><span data-stu-id="653e1-123">You don't need to have Docker installed, though, because you'll use the Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="653e1-124">Para compilar a imagem e se preparar para executá-la no Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="653e1-124">To build the image and prepare to run it on Azure, do the following:</span></span>

1. <span data-ttu-id="653e1-125">Instale a CLI do Azure e entre nela.</span><span class="sxs-lookup"><span data-stu-id="653e1-125">Install and sign in to the Azure CLI.</span></span>
1. <span data-ttu-id="653e1-126">Crie um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="653e1-126">Create an Azure resource group.</span></span>
1. <span data-ttu-id="653e1-127">Crie uma instância do Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="653e1-127">Create an Azure container registry instance.</span></span>
1. <span data-ttu-id="653e1-128">Compile uma imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="653e1-128">Build a Docker image.</span></span>
1. <span data-ttu-id="653e1-129">Publique a imagem do Docker na instância do registro de contêiner criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="653e1-129">Publish the Docker image to the previously created container registry instance.</span></span>
1. <span data-ttu-id="653e1-130">(Opcional) Compile e publique a imagem na instância do registro de contêiner em um comando.</span><span class="sxs-lookup"><span data-stu-id="653e1-130">(Optional) Build and publish the image to the container registry instance in one command.</span></span>


#### <a name="set-up-the-azure-cli"></a><span data-ttu-id="653e1-131">Configurar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="653e1-131">Set up the Azure CLI</span></span>

<span data-ttu-id="653e1-132">Verifique se você tem uma assinatura do Azure, se instalou [a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) e se está autenticado em sua conta:</span><span class="sxs-lookup"><span data-stu-id="653e1-132">Make sure that you have an Azure subscription, that you've installed [the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you're authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="653e1-133">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="653e1-133">Create a resource group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a><span data-ttu-id="653e1-134">Criar uma instância do registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="653e1-134">Create a container registry instance</span></span>

<span data-ttu-id="653e1-135">Este comando deverá criar uma instância do registro de contêiner global exclusiva globalmente com um nome básico e um número aleatório.</span><span class="sxs-lookup"><span data-stu-id="653e1-135">This command should create a globally unique container registry instance with a basic name and a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="653e1-136">Criar a imagem de Docker</span><span class="sxs-lookup"><span data-stu-id="653e1-136">Build the Docker image</span></span>

<span data-ttu-id="653e1-137">Embora você possa compilar a imagem do Docker localmente com facilidade usando o próprio Docker, talvez queira considerar compilá-la na nuvem por alguns motivos:</span><span class="sxs-lookup"><span data-stu-id="653e1-137">Although you can easily build the Docker image locally by using Docker itself, you might consider building it in the cloud for few reasons:</span></span>

* <span data-ttu-id="653e1-138">Não é necessário instalar o Docker localmente.</span><span class="sxs-lookup"><span data-stu-id="653e1-138">You don't have to install Docker locally.</span></span>
* <span data-ttu-id="653e1-139">Isso é muito mais rápido, porque o build ocorre em outro lugar (com exceção do tempo de upload do contexto).</span><span class="sxs-lookup"><span data-stu-id="653e1-139">It's much faster, because the build happens elsewhere (except for context upload time).</span></span>
* <span data-ttu-id="653e1-140">O processo na nuvem tem um acesso mais rápido à Internet e, portanto, downloads mais rápidos.</span><span class="sxs-lookup"><span data-stu-id="653e1-140">The process in the cloud has faster access to the internet and, therefore, faster downloads.</span></span>
* <span data-ttu-id="653e1-141">A imagem vai diretamente para a instância do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="653e1-141">The image goes directly into the container registry instance.</span></span>

<span data-ttu-id="653e1-142">Por esses motivos, você compilará a imagem usando o recurso [Build do Registro de Contêiner do Azure]:</span><span class="sxs-lookup"><span data-stu-id="653e1-142">For these reasons, you build the image by using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a><span data-ttu-id="653e1-143">Implantar a imagem do Docker por meio da instância do Registro de Contêiner do Azure nas Instâncias de Contêiner</span><span class="sxs-lookup"><span data-stu-id="653e1-143">Deploy the Docker image from the Azure container registry instance to Container Instances</span></span>

<span data-ttu-id="653e1-144">Agora que a imagem está disponível na instância do registro de contêiner, envie uma instância de contêiner por push e crie uma instância dela nas Instâncias de Contêiner.</span><span class="sxs-lookup"><span data-stu-id="653e1-144">Now that the image is available on your container registry instance, push and instantiate a container instance on Container Instances.</span></span> <span data-ttu-id="653e1-145">Mas primeiro, verifique se você consegue se autenticar na instância do registro de contêiner:</span><span class="sxs-lookup"><span data-stu-id="653e1-145">But first, make sure that you can authenticate into the container registry instance:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="653e1-146">Testar o aplicativo do MicroProfile implantado</span><span class="sxs-lookup"><span data-stu-id="653e1-146">Test your deployed MicroProfile application</span></span>

<span data-ttu-id="653e1-147">Seu aplicativo agora deve estar em execução.</span><span class="sxs-lookup"><span data-stu-id="653e1-147">Your application should now be up and running.</span></span> <span data-ttu-id="653e1-148">Para testá-lo na interface de linha de comando, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="653e1-148">To test it from the command-line interface, use the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="653e1-149">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="653e1-149">Congratulations!</span></span> <span data-ttu-id="653e1-150">Você criou um aplicativo do MicroProfile como um contêiner do Docker e o implantou no Azure com êxito.</span><span class="sxs-lookup"><span data-stu-id="653e1-150">You've successfully built a MicroProfile application as a Docker container and deployed it to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="653e1-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="653e1-151">Next steps</span></span>

<span data-ttu-id="653e1-152">Para obter mais informações sobre as várias tecnologias abordadas neste artigo, confira:</span><span class="sxs-lookup"><span data-stu-id="653e1-152">For more information about the various technologies discussed in this article, see:</span></span>

* [<span data-ttu-id="653e1-153">Entrar no Azure por meio da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="653e1-153">Sign in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Build do Registro de Contêiner do Azure]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[CLI do Azure]: /cli/azure/overview
[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Instâncias de Contêiner do Azure]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Registro de Contêiner do Azure]:  https://docs.microsoft.com/azure/container-registry
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
