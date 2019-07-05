---
title: Implantar um serviço MicroProfile baseado em Java para o Aplicativo Web para Contêineres do Azure
description: Saiba como implantar um serviço MicroProfile usando o Docker e o Aplicativo Web para Contêineres do Azure
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533595"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="7a412-103">Implantar um serviço MicroProfile baseado em Java para o Aplicativo Web para Contêineres do Azure</span><span class="sxs-lookup"><span data-stu-id="7a412-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="7a412-104">O MicroProfile é uma ótima maneira de compilar aplicativos Java extremamente pequenos que podem ser implantados com rapidez e facilidade em serviços, como o [Aplicativo Web para Contêineres do Azure](https://azure.microsoft.com/services/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="7a412-104">MicroProfile is a great way to build exceedingly small Java applications that you can quickly and easily deploy to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="7a412-105">Neste tutorial, você criará um microsserviço simples baseado no MicroProfile que será colocado em um contêiner do Docker, implantado em uma [instância do Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry/) e, em seguida, hospedado usando o Aplicativo Web para Contêineres do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-105">In this tutorial, you create a simple, MicroProfile-based microservice that you containerize into a Docker container, deploy to an [Azure container registry instance](https://azure.microsoft.com/services/container-registry/), and then host by using Azure Web App for Containers.</span></span>

> [!NOTE]
> <span data-ttu-id="7a412-106">Este procedimento funciona com qualquer implementação do MicroProfile.io, desde que a imagem de contêiner do Docker seja autoexecutável (ou seja, a imagem inclui o tempo de execução).</span><span class="sxs-lookup"><span data-stu-id="7a412-106">This procedure works with any implementation of MicroProfile.io, as long the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

<span data-ttu-id="7a412-107">Nesta amostra, você usará o [Payara Micro](https://www.payara.fish/payara_micro) e o [MicroProfile 1.3](https://microprofile.io/) para criar um arquivo WAR (requisito de aplicativo Web) Java pequeno (aproximadamente 5.000 bytes) e, em seguida, o empacotará em uma imagem do Docker de cerca de 174 MB (megabytes).</span><span class="sxs-lookup"><span data-stu-id="7a412-107">In this sample, you use [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a small (approximately 5,000 bytes) Java web application requirement (WAR) file, and then package it into a Docker image of approximately 174 megabytes (MB).</span></span> <span data-ttu-id="7a412-108">A imagem do Docker contém tudo o que é necessário para uma implantação totalmente contida em contêiner do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="7a412-108">The Docker image contains everything necessary for a fully containerized deployment of the web app.</span></span>

<span data-ttu-id="7a412-109">Uma imagem inteira do Docker de 174 MB não precisa ser reimplantada sempre que o código-fonte do aplicativo é alterado, pois o Docker carrega apenas as diferenças (que são significativamente menores).</span><span class="sxs-lookup"><span data-stu-id="7a412-109">An entire 174 MB Docker image doesn't need to be redeployed whenever the application source code is changed, because Docker uploads only the differences (which are significantly smaller).</span></span> <span data-ttu-id="7a412-110">Consequentemente, o processo de execução uma nova versão de um aplicativo do MicroProfile por meio de um pipeline de CI/CD é extremamente eficiente e rápido, reduzindo conflitos e possibilitando uma iteração rápida de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7a412-110">Consequently, the process of executing a new release of a MicroProfile application via a CI/CD pipeline is extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="7a412-111">Você trabalhará neste tutorial primeiro criando e executando o código localmente e, em seguida, implantando-o como um aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-111">You'll work through this tutorial by first creating and running the code locally and then deploying it as a web app on Azure.</span></span> <span data-ttu-id="7a412-112">Em ambas as fases, você poderá depender do Docker para simplificar e padronizar seus esforços.</span><span class="sxs-lookup"><span data-stu-id="7a412-112">In both phases, you can depend on Docker to simplify and standardize your efforts.</span></span> <span data-ttu-id="7a412-113">Antes de começar, você criará uma instância do Registro de Contêiner do Azure para armazenar seus contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="7a412-113">Before you begin, you'll create an Azure container registry instance for storing your Docker containers.</span></span>

## <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="7a412-114">Criar uma instância do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="7a412-114">Create an Azure container registry instance</span></span>

<span data-ttu-id="7a412-115">Você pode usar o [portal do Azure](http://portal.azure.com) para criar a instância do Registro de Contêiner do Azure, mas há outras opções também, como a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-115">You can use the [Azure portal](http://portal.azure.com) to create the Azure container registry instance, but there are other choices also, such as the Azure CLI.</span></span> <span data-ttu-id="7a412-116">Para criar uma instância do Registro de Contêiner do Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a412-116">To create a new Azure container registry instance, do the following:</span></span>

1. <span data-ttu-id="7a412-117">Entre no [portal do Azure](http://portal.azure.com) e crie um recurso do Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-117">Sign in to the [Azure portal](http://portal.azure.com) and create a new Azure container registry resource.</span></span> <span data-ttu-id="7a412-118">Forneça um nome de registro (esse nome deve ser definido como a propriedade `docker.registry` no arquivo *pom.xml*).</span><span class="sxs-lookup"><span data-stu-id="7a412-118">Provide a registry name (this name should be set as the `docker.registry` property in the *pom.xml* file).</span></span> <span data-ttu-id="7a412-119">Altere os padrões, conforme desejado e, em seguida, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7a412-119">Change the defaults as you want, and then select **Create**.</span></span>

1. <span data-ttu-id="7a412-120">Em aproximadamente 30 segundos, quando a instância do registro de contêiner estiver ativa, selecione a instância do registro de contêiner e, em seguida, no painel esquerdo, selecione o link **Chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="7a412-120">In about 30 seconds, when the container registry instance is live, select the container registry instance and then, in the left pane, select the **Access keys** link.</span></span> 

    <span data-ttu-id="7a412-121">Habilite a configuração *usuário administrador* para acessar essa instância do registro de contêiner nos computadores e enviar contêineres do Docker por push para ela.</span><span class="sxs-lookup"><span data-stu-id="7a412-121">Be sure to enable the *admin user* setting, so that you can access this container registry instance from your machines and push Docker containers into it.</span></span> <span data-ttu-id="7a412-122">Essa ação também permite o acesso por meio da instância do Aplicativo Web para Contêineres do Azure que você configurará em breve.</span><span class="sxs-lookup"><span data-stu-id="7a412-122">Doing so also enables access from the Azure Web App for Containers instance that you'll set up soon.</span></span>

1. <span data-ttu-id="7a412-123">No painel **Chaves de acesso**, copie os valores de **nome de usuário** e **senha** e cole-os no arquivo *settings.xml* global do Maven.</span><span class="sxs-lookup"><span data-stu-id="7a412-123">In the **Access keys** pane, copy the **username** and **password** values and paste them into your global Maven *settings.xml* file.</span></span> <span data-ttu-id="7a412-124">Para obter mais informações sobre as configurações do Maven, acesse o site do [Projeto Apache Maven](https://maven.apache.org/settings.html).</span><span class="sxs-lookup"><span data-stu-id="7a412-124">For more information about Maven settings, go to the [Apache Maven Project](https://maven.apache.org/settings.html) website.</span></span> 

   <span data-ttu-id="7a412-125">Para referência, este é um exemplo do arquivo *${user.home}/.m2/settings.xml*:</span><span class="sxs-lookup"><span data-stu-id="7a412-125">For your reference, here's an example of the *${user.home}/.m2/settings.xml* file:</span></span>

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

<span data-ttu-id="7a412-126">Agora que você criou a instância do registro de contêiner, continue para criar e executar seu aplicativo do MicroProfile localmente.</span><span class="sxs-lookup"><span data-stu-id="7a412-126">Now that you've created your container registry instance, you can move on to building and running your MicroProfile application locally.</span></span>

## <a name="create-your-microprofile-application"></a><span data-ttu-id="7a412-127">Criar seu aplicativo do MicroProfile</span><span class="sxs-lookup"><span data-stu-id="7a412-127">Create your MicroProfile application</span></span>

<span data-ttu-id="7a412-128">Este código de exemplo se baseia em um aplicativo de exemplo disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a412-128">This example code is based on a sample application that's available on GitHub.</span></span> <span data-ttu-id="7a412-129">Para clonar o código no computador, insira os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7a412-129">To clone the code onto your machine, enter the following commands:</span></span>

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

<span data-ttu-id="7a412-130">Esse diretório contém um arquivo *pom.xml* que você pode usar para especificar o projeto no formato que é usado pela ferramenta de build Maven.</span><span class="sxs-lookup"><span data-stu-id="7a412-130">This directory contains a *pom.xml* file that you use to specify the project in the format that's used by the Maven build tool.</span></span> <span data-ttu-id="7a412-131">Edite o arquivo de acordo com suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="7a412-131">You can edit the file to suit your own needs.</span></span> <span data-ttu-id="7a412-132">Em particular, as propriedades `docker.registry` e `docker.name` devem ser alteradas para as propriedades `docker.registry` e `docker.name` que foram criadas quando você configurou a instância do Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-132">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` properties that were created when you set up the Azure container registry instance.</span></span>

<span data-ttu-id="7a412-133">Outro arquivo importante neste diretório é o Dockerfile, que é reproduzido abaixo:</span><span class="sxs-lookup"><span data-stu-id="7a412-133">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="7a412-134">O Dockerfile cria um contêiner do Docker com base no Contêiner do Docker do Payara Micro.</span><span class="sxs-lookup"><span data-stu-id="7a412-134">The Dockerfile creates a new Docker container that's based on the Payara Micro Docker Container.</span></span> <span data-ttu-id="7a412-135">Ele copia o arquivo WAR que foi criado como parte do processo de build.</span><span class="sxs-lookup"><span data-stu-id="7a412-135">It copies in the WAR file that was created as part of your build process.</span></span> <span data-ttu-id="7a412-136">Também expõe a porta 8080 para que você possa acessar o serviço depois que ele estiver em funcionamento em um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="7a412-136">It also exposes port 8080 so that you can access the service after it's up and running within a Docker container.</span></span>

<span data-ttu-id="7a412-137">Ao abrir o diretório *src*, você acabará descobrindo a classe `Application` que é reproduzida aqui:</span><span class="sxs-lookup"><span data-stu-id="7a412-137">When you open the *src* directory, you'll eventually discover the `Application` class that's reproduced here:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="7a412-138">A anotação *@ApplicationPath("/api")* especifica o ponto de extremidade base para esse microsserviço.</span><span class="sxs-lookup"><span data-stu-id="7a412-138">The *@ApplicationPath("/api")* annotation specifies the base endpoint for this microservice.</span></span> <span data-ttu-id="7a412-139">Ou seja, para todos os pontos de extremidade, */api* precede o restante da URL necessária para acessar qualquer ponto de extremidade REST específico.</span><span class="sxs-lookup"><span data-stu-id="7a412-139">That is, for all endpoints, */api* precedes the rest of the URL that's required to access any specific REST endpoint.</span></span>

<span data-ttu-id="7a412-140">Dentro do pacote *api*, há uma classe chamada `API`, que contém o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="7a412-140">Inside the *api* package is a class named `API`, which contains the following code:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

<span data-ttu-id="7a412-141">Por meio do uso da anotação *@Path("/helloworld")* , você poderá ver que esse ponto de extremidade REST, quando combinado com a anotação */api* especificada na classe `Application`, será */api/helloworld*.</span><span class="sxs-lookup"><span data-stu-id="7a412-141">Through the use of the *@Path("/helloworld")* annotation, you can see that this REST endpoint, when it's combined with the */api* that's specified in the `Application` class, will be */api/helloworld*.</span></span> <span data-ttu-id="7a412-142">Ao chamar esse ponto de extremidade usando uma solicitação HTTP GET, você verá que o método produzirá text/html e, na verdade, é simplesmente uma cadeia de caracteres embutida em código, "Olá, mundo!"</span><span class="sxs-lookup"><span data-stu-id="7a412-142">When you call this endpoint by using an HTTP GET request, you can see that the method produces text/html and, in fact, it's simply a hard-coded string, "Hello, world!"</span></span>

<span data-ttu-id="7a412-143">Até agora, este artigo abordou todo o código necessário para você criar um microsserviço usando o MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="7a412-143">So far, this article has covered all the code that's required for you to create a microservice by using MicroProfile.</span></span> <span data-ttu-id="7a412-144">Agora você pode usar o Maven para compilá-lo, colocá-lo em um contêiner do Docker e executá-lo localmente fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a412-144">You can now use Maven to build it, containerize it into a Docker container, and run it locally by doing the following:</span></span>

1. <span data-ttu-id="7a412-145">Execute `mvn clean package` e aguarde até ele ser concluído.</span><span class="sxs-lookup"><span data-stu-id="7a412-145">Run `mvn clean package`, and wait until it is complete.</span></span>

1. <span data-ttu-id="7a412-146">Execute `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span><span class="sxs-lookup"><span data-stu-id="7a412-146">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span></span> <span data-ttu-id="7a412-147">Por exemplo, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, em que *\<docker.registry>* é *jogilescr.azurecr.io* e *\<docker.name>* é *samples/docker-helloworld*.</span><span class="sxs-lookup"><span data-stu-id="7a412-147">For example, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, where *\<docker.registry>* is *jogilescr.azurecr.io* and *\<docker.name>* is *samples/docker-helloworld*.</span></span>

1. <span data-ttu-id="7a412-148">Tente acessar [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) e [http://localhost:8080/health](http://localhost:8080/health) no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="7a412-148">Try to access [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="7a412-149">Se você vir a resposta esperada “Olá, mundo!”</span><span class="sxs-lookup"><span data-stu-id="7a412-149">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="7a412-150">(e as informações relacionadas à integridade do ponto de extremidade [/health](http://localhost:8080/health)), isso indicará que você implantou com êxito o aplicativo do MicroProfile no computador local.</span><span class="sxs-lookup"><span data-stu-id="7a412-150">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you've successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="push-the-container-to-the-azure-container-registry-instance"></a><span data-ttu-id="7a412-151">Enviar o contêiner por push à instância do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="7a412-151">Push the container to the Azure container registry instance</span></span>

<span data-ttu-id="7a412-152">Agora que você compilou e executou com êxito seu aplicativo do MicroProfile no computador local, envie esse contêiner por push à instância do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="7a412-152">Now that you've successfully built and run your MicroProfile application on your local machine, push this container to your container registry instance.</span></span> 

> [!NOTE]
> <span data-ttu-id="7a412-153">Embora este artigo use uma instância do Registro de Contêiner do Azure, qualquer instância do registro de contêiner deverá funcionar, desde que o arquivo *pom.xml* seja editado a fim de apontar para uma localização relevante.</span><span class="sxs-lookup"><span data-stu-id="7a412-153">Although this article uses an Azure container registry instance, any container registry instance should work, as long as the *pom.xml* file is edited to point to the relevant location.</span></span>

1. <span data-ttu-id="7a412-154">Para limpar, compilar e criar uma imagem local do Docker, execute `mvn clean package`.</span><span class="sxs-lookup"><span data-stu-id="7a412-154">To clean, compile, and create a local Docker image, run `mvn clean package`.</span></span>
2. <span data-ttu-id="7a412-155">Para enviar o contêiner por push à instância do Registro de Contêiner do Azure, execute `mvn dockerfile:push`.</span><span class="sxs-lookup"><span data-stu-id="7a412-155">To push the container to the Azure container registry instance, run `mvn dockerfile:push`.</span></span>

<span data-ttu-id="7a412-156">Agora você carregou sua imagem de contêiner do Docker na instância do Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-156">You now have your Docker container image uploaded to the Azure container registry instance.</span></span> <span data-ttu-id="7a412-157">No entanto, ela ainda não está em execução.</span><span class="sxs-lookup"><span data-stu-id="7a412-157">However, it's not yet running.</span></span> <span data-ttu-id="7a412-158">Agora você precisa implantá-la em uma instância do Aplicativo Web para Contêineres do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-158">You now have to deploy it to an Azure Web App for Containers instance.</span></span> 

## <a name="create-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="7a412-159">Criar uma instância do Aplicativo Web para Contêineres do Azure</span><span class="sxs-lookup"><span data-stu-id="7a412-159">Create an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="7a412-160">No [portal do Azure](http://portal.azure.com), no painel esquerdo, selecione **Web + Celular** e, em seguida, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a412-160">In the [Azure portal](http://portal.azure.com), in the left pane, select **Web + Mobile**, and then do the following:</span></span>

   <span data-ttu-id="7a412-161">a.</span><span class="sxs-lookup"><span data-stu-id="7a412-161">a.</span></span> <span data-ttu-id="7a412-162">Especifique um nome.</span><span class="sxs-lookup"><span data-stu-id="7a412-162">Specify a name.</span></span> <span data-ttu-id="7a412-163">O nome se tornará a URL pública do aplicativo Web; portanto, é uma boa ideia escolher um nome que possa ser lembrado com facilidade.</span><span class="sxs-lookup"><span data-stu-id="7a412-163">The name will become the public URL of the web app, so it's a good idea to pick a name that you can easily remember.</span></span> <span data-ttu-id="7a412-164">Você poderá adicionar um nome de domínio personalizado mais tarde, se desejar.</span><span class="sxs-lookup"><span data-stu-id="7a412-164">You can add a custom domain name later, if you want.</span></span>

   <span data-ttu-id="7a412-165">b.</span><span class="sxs-lookup"><span data-stu-id="7a412-165">b.</span></span> <span data-ttu-id="7a412-166">Na seção **Configurar contêiner**, em **Origem da imagem**, selecione **Registro de Contêiner do Azure** e, em seguida, na lista suspensa, selecione a imagem correta.</span><span class="sxs-lookup"><span data-stu-id="7a412-166">In the **Configure container** section, under **Image source**, select **Azure Container Registry** and then, in the drop-down list, select the correct image.</span></span>

   <span data-ttu-id="7a412-167">c.</span><span class="sxs-lookup"><span data-stu-id="7a412-167">c.</span></span> <span data-ttu-id="7a412-168">Não é necessário especificar nenhum valor no campo **Arquivo de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="7a412-168">You don't need to specify a value in the **Startup File** field.</span></span>

1. <span data-ttu-id="7a412-169">Depois de criar a instância, selecione-a e, em seguida, selecione **Configurações de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="7a412-169">After you've created the instance, select it, and then select **Application Settings**.</span></span> <span data-ttu-id="7a412-170">Em **Chave**, insira **WEBSITES_PORT** e, em **Valor**, insira **8080**.</span><span class="sxs-lookup"><span data-stu-id="7a412-170">For **Key**, enter **WEBSITES_PORT**, and for **Value**, enter **8080**.</span></span> <span data-ttu-id="7a412-171">Essas configurações instruem o Azure sobre qual porta deverá ser exposta no contêiner e a mapeá-la para a porta 80 externamente.</span><span class="sxs-lookup"><span data-stu-id="7a412-171">These settings tell Azure which port to expose in the container and to map it to port 80 externally.</span></span>

1. <span data-ttu-id="7a412-172">(Opcional) Selecione o link **Contêiner do Docker** e, em seguida, habilite **Implantação Contínua**.</span><span class="sxs-lookup"><span data-stu-id="7a412-172">(Optional) Select the **Docker Container** link, and then enable **Continuous Deployment**.</span></span> <span data-ttu-id="7a412-173">Ao fazer isso, sempre que você atualizar a imagem da instância do registro de contêiner do Azure, ela será atualizada automaticamente na instância do Aplicativo Web para Contêineres do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-173">By doing so, whenever you update the Azure container registry instance image, it's automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="7a412-174">Agora você deverá conseguir acessar as instâncias hospedadas no Azure em `http://<appname>.azurewebsites.net/microprofile/api/helloworld` e `http://<appname>.azurewebsites.net/health`.</span><span class="sxs-lookup"><span data-stu-id="7a412-174">You should now be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="7a412-175">Resumo</span><span class="sxs-lookup"><span data-stu-id="7a412-175">Summary</span></span>

<span data-ttu-id="7a412-176">Neste tutorial, você acompanhou o processo de criação de um microsserviço simples baseado no MicroProfile, colocou-o em um contêiner do Docker, executou-o localmente e publicou-o no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a412-176">In this tutorial, you've stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, run it locally, and published it to Azure.</span></span> <span data-ttu-id="7a412-177">Você pode estender seu microsserviço para fornecer funcionalidades adicionais úteis.</span><span class="sxs-lookup"><span data-stu-id="7a412-177">You can extend your microservice to provide additional useful functionality.</span></span> <span data-ttu-id="7a412-178">Para obter mais informações, acesse [MicroProfile.io](https://microprofile.io/).</span><span class="sxs-lookup"><span data-stu-id="7a412-178">For more information, go to [MicroProfile.io](https://microprofile.io/).</span></span>
