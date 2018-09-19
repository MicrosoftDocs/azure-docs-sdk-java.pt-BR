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
ms.openlocfilehash: 1eb0e7d7a718a1c106adebbf89011f6e3fa1504e
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040244"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="a4392-103">Implantar um serviço MicroProfile baseado em Java para o Aplicativo Web para Contêineres do Azure</span><span class="sxs-lookup"><span data-stu-id="a4392-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="a4392-104">MicroProfile é uma ótima maneira para compilar aplicativos Java extremamente pequenos que podem ser rápida e facilmente implantados nos serviços, como [Aplicativo Web para Contêineres do Azure](https://azure.microsoft.com/services/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="a4392-104">MicroProfile is a great way to build exceedingly tiny Java applications that can be quickly and easily deployed to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="a4392-105">Neste tutorial, criaremos um microsserviço baseado em MicroProfile simples que é colocado no contêiner do Docker, implantado em um [Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry/) e, em seguida, hospedado usando o Aplicativo Web para Contêineres do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4392-105">In this tutorial we will create a simple MicroProfile-based microservice that is then containerized into a Docker container, deployed into an [Azure Container Registry](https://azure.microsoft.com/services/container-registry/), and then hosted using Azure Web App for Containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a4392-106">Este procedimento funciona com qualquer implementação de MicroProfile.io, desde que a imagem de contêiner do Docker seja executada automaticamente (ou seja, inclui o tempo de execução).</span><span class="sxs-lookup"><span data-stu-id="a4392-106">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

<span data-ttu-id="a4392-107">Mais concretamente, este exemplo usa [Payara Micro](https://www.payara.fish/payara_micro) e [MicroProfile 1.3](https://microprofile.io/) para criar um arquivo war de Java pequeno (5.085 bytes na máquina de criadores) e, em seguida, empacotá-lo em uma imagem do Docker (que é de aproximadamente 174 megabytes).</span><span class="sxs-lookup"><span data-stu-id="a4392-107">More concretely, this sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a tiny Java war file (5,085 bytes on the authors machine), and then packages it up into a Docker image (which is approximately 174 megabytes).</span></span> <span data-ttu-id="a4392-108">Essa imagem do Docker contém todo o necessário para uma implantação totalmente contida em contêiner deste aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a4392-108">This Docker image contains everything necessary for a fully-containerised deployment of this webapp.</span></span>

<span data-ttu-id="a4392-109">Devido à maneira como o Docker funciona, é comum que a imagem do Docker de 174 megabytes não precise ser reimplantada em sua totalidade sempre que o código-fonte do aplicativo é alterado, já que o Docker carregará somente as diferenças (que é significativamente menor).</span><span class="sxs-lookup"><span data-stu-id="a4392-109">Because of the way Docker works, it is often the case that the entire 174 megabyte Docker image does not need to be redeployed whenever the application source code is changed, as Docker will only upload the differences (which is significantly smaller).</span></span> <span data-ttu-id="a4392-110">Isso torna o processo de executar uma nova versão de um aplicativo MicroProfile por meio de um pipeline de CI/CD extremamente eficiente e rápido, reduzindo o atrito e habilitando a iteração de desenvolvimento rápido.</span><span class="sxs-lookup"><span data-stu-id="a4392-110">This makes the process of executing a new release of a MicroProfile application via a CI/CD pipeline extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="a4392-111">Vamos trabalhar neste tutorial em primeiro lugar, criando e executando o código localmente e, em seguida, implantaremos este código como um aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="a4392-111">We will work through this tutorial firstly by creating and running the code locally, and then we will deploy this as a web app on Azure.</span></span> <span data-ttu-id="a4392-112">Em ambos os casos, dependemos do Docker para simplificar e padronizar nossos esforços.</span><span class="sxs-lookup"><span data-stu-id="a4392-112">In both cases we will depend on Docker to simplify and standardize our efforts.</span></span> <span data-ttu-id="a4392-113">Antes de começar, vamos criar um Registro de Contêiner do Azure para armazenar nossos contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="a4392-113">Before we begin, we will create an Azure Container Registry to store our Docker containers in.</span></span>

## <a name="creating-an-azure-container-registry"></a><span data-ttu-id="a4392-114">Criar um Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="a4392-114">Creating an Azure Container Registry</span></span>

<span data-ttu-id="a4392-115">Nós usaremos o [Portal do Azure](http://portal.azure.com) para criar o Registro de Contêiner do Azure, mas observe que há opções alternativas, como a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4392-115">We will use the [Azure Portal](http://portal.azure.com) for creating the Azure Container Registry, but note that there are alternate choices such as the Azure CLI.</span></span> <span data-ttu-id="a4392-116">Siga as etapas abaixo para criar um novo Registro de Contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="a4392-116">Follow the steps below to create a new Azure Container Registry:</span></span>

1. <span data-ttu-id="a4392-117">Faça logon no [Portal do Azure](http://portal.azure.com) e crie um novo recurso de Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4392-117">Log in to the [Azure Portal](http://portal.azure.com) and create a new Azure Container Registry resource.</span></span> <span data-ttu-id="a4392-118">Forneça um nome de registro (Observe que esse é o nome que deve ser definido como a propriedade `docker.registry` em `pom.xml`).</span><span class="sxs-lookup"><span data-stu-id="a4392-118">Provide a registry name (note that this is the name that should be set as the `docker.registry` property in `pom.xml`).</span></span> <span data-ttu-id="a4392-119">Altere os padrões conforme desejar e, em seguida, clique em “criar”.</span><span class="sxs-lookup"><span data-stu-id="a4392-119">Change the defaults as you wish, and then click 'create'.</span></span>

1. <span data-ttu-id="a4392-120">Depois que o registro de contêiner estiver ativo (que demora aproximadamente 30 segundos depois de clicar em “criar”), clique no registro de contêiner e clique no link “Acessar chaves” na área do menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="a4392-120">Once the container registry is live (which is about 30 seconds after clicking 'create'), click on the container registry, and click on the 'Access keys' link in the left-menu area.</span></span> <span data-ttu-id="a4392-121">Aqui, você precisa habilitar a configuração de “usuário administrador”, para que o registro de contêiner possa ser acessado de nossos computadores (para enviar por push os contêineres do Docker), e também para habilitar a instância de Aplicativos Web para Contêineres do Azure que configuraremos em breve.</span><span class="sxs-lookup"><span data-stu-id="a4392-121">In here, you need to enable the 'admin user' setting, so that this container registry can be accessed from our machines (to push docker containers into), and also to enable access from the Azure Web Apps for Containers instance we will setup soon.</span></span>

1. <span data-ttu-id="a4392-122">Enquanto você estiver na área de “Chaves de Acesso”, anote os valores `username` e `password`.</span><span class="sxs-lookup"><span data-stu-id="a4392-122">Whilst you are in the 'Access keys' area, note the `username` and `password` values.</span></span> <span data-ttu-id="a4392-123">Esses valores serão copiados / colados no nosso arquivo `settings.xml` Maven global (para obter mais informações sobre configurações do Maven, consulte o site [Projeto do Apache Maven](https://maven.apache.org/settings.html)).</span><span class="sxs-lookup"><span data-stu-id="a4392-123">We will copy / paste these into our global Maven `settings.xml` file  (for more information on Maven settings, refer to the [Apache Maven Project](https://maven.apache.org/settings.html) website).</span></span> <span data-ttu-id="a4392-124">Para referência, aqui está uma versão oculta do arquivo `${user.home}/.m2/settings.xml` no sistema de criadores:</span><span class="sxs-lookup"><span data-stu-id="a4392-124">For reference, here is an obfuscated version of the `${user.home}/.m2/settings.xml` file on the authors system:</span></span>

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

<span data-ttu-id="a4392-125">Agora que isso foi concluído, podemos continuar com a criação e execução de nosso aplicativo MicroProfile localmente.</span><span class="sxs-lookup"><span data-stu-id="a4392-125">Now that this is complete, we can move on with building and running our MicroProfile application locally.</span></span>

## <a name="creating-our-microprofile-application"></a><span data-ttu-id="a4392-126">Criar nosso aplicativo MicroProfile</span><span class="sxs-lookup"><span data-stu-id="a4392-126">Creating our MicroProfile application</span></span>

<span data-ttu-id="a4392-127">Este exemplo é baseado em um aplicativo de exemplo disponível no GitHub, para que possamos clonar e, em seguida, percorrer o código.</span><span class="sxs-lookup"><span data-stu-id="a4392-127">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="a4392-128">Siga as etapas abaixo para obter o código clonado em seu computador:</span><span class="sxs-lookup"><span data-stu-id="a4392-128">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

<span data-ttu-id="a4392-129">Nesse diretório, há um arquivo `pom.xml` que é usado para especificar o projeto no formato usado pela ferramenta de build do Maven.</span><span class="sxs-lookup"><span data-stu-id="a4392-129">In this directory there is a `pom.xml` file that is used to specify the project in the format used by the Maven build tool.</span></span> <span data-ttu-id="a4392-130">Esse arquivo pode ser editado para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="a4392-130">This file can be edited to suit your own needs.</span></span> <span data-ttu-id="a4392-131">Em particular, as propriedades `docker.registry` e `docker.name` devem ser alteradas para `docker.registry` e `docker.name` criadas quando o Registro de Contêiner do Azure foi configurado.</span><span class="sxs-lookup"><span data-stu-id="a4392-131">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` created when the Azure Container Registry was setup.</span></span>

<span data-ttu-id="a4392-132">Outro arquivo importante neste diretório é o Dockerfile, que é reproduzido abaixo:</span><span class="sxs-lookup"><span data-stu-id="a4392-132">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="a4392-133">Este Dockerfile simplesmente cria um novo contêiner do Docker com base no contêiner do Docker Payara Micro e copia o arquivo .war que é criado como parte do nosso processo de criação.</span><span class="sxs-lookup"><span data-stu-id="a4392-133">This Dockerfile simply creates a new Docker container based on the Payara Micro Docker Container, and copies in the .war file that is created as part of our build process.</span></span> <span data-ttu-id="a4392-134">Ele também expõe a porta 8080 para que possamos acessar o serviço depois que ele está em execução dentro de um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="a4392-134">It also exposes port 8080 so that we may access the service once it is up and running within a Docker container.</span></span>

<span data-ttu-id="a4392-135">Ao nos aprofundarmos no diretório `src`, eventualmente, descobriremos a classe `Application` reproduzida abaixo:</span><span class="sxs-lookup"><span data-stu-id="a4392-135">Diving into the `src` directory, we will eventually discover the `Application` class reproduced below:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="a4392-136">A anotação `@ApplicationPath("/api")` especifica o ponto de extremidade de base para este microsserviço - ou seja, que todos os pontos de extremidade terão `/api` antes do restante da URL necessária para acessar qualquer ponto de extremidade REST específico.</span><span class="sxs-lookup"><span data-stu-id="a4392-136">The `@ApplicationPath("/api")` annotation specifies the base endpoint for this microservice - that is, that all endpoints will have `/api` preceed the rest of the URL required to access any specific REST endpoint.</span></span>

<span data-ttu-id="a4392-137">Dentro do pacote `api` está uma classe chamada `API`, que contém o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4392-137">Inside the `api` package is a class named `API`, which contains the following code:</span></span>

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

<span data-ttu-id="a4392-138">Com o uso da anotação `@Path("/helloworld")`, podemos ver que esse ponto de extremidade REST, quando combinado com o `/api` especificado na classe `Application`, será `/api/helloworld`.</span><span class="sxs-lookup"><span data-stu-id="a4392-138">Through the use of the `@Path("/helloworld")` annotation, we can see that this REST endpoint, when combined with the `/api` specified in the `Application` class, will be `/api/helloworld`.</span></span> <span data-ttu-id="a4392-139">Quando esse ponto de extremidade é chamado usando uma solicitação HTTP GET, podemos ver que o método produzirá texto/html e, na verdade, é simplesmente uma cadeia de caracteres embutidos em código “Olá, mundo!”.</span><span class="sxs-lookup"><span data-stu-id="a4392-139">When this endpoint is called using an HTTP GET request, we can see that the method will produce text/html, and in fact it is simply a hard-coded string "Hello, world!".</span></span>

<span data-ttu-id="a4392-140">Agora, abordamos todo o código necessário para criar um microsserviço usando MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="a4392-140">We have now covered all the code required to create a microservice using MicroProfile.</span></span> <span data-ttu-id="a4392-141">Agora podemos usar Maven para compilá-lo, colocar no contêiner do Docker e executá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="a4392-141">We can now use Maven to build it, containerize it into a Docker container, and run it locally.</span></span> <span data-ttu-id="a4392-142">Você pode fazer isso através das seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a4392-142">We can do that with the following steps:</span></span>

1. <span data-ttu-id="a4392-143">Executar `mvn clean package` e aguardar até que ele seja concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="a4392-143">Run `mvn clean package` and wait until it successfully completes.</span></span>

1. <span data-ttu-id="a4392-144">Executar `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, por exemplo, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, se seu `docker.registry` é `jogilescr.azurecr.io` e `docker.name` é `samples/docker-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="a4392-144">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, for example, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, if your `docker.registry` is `jogilescr.azurecr.io` and `docker.name` is `samples/docker-helloworld`.</span></span>

1. <span data-ttu-id="a4392-145">Tentar acessar [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) e [http://localhost:8080/health](http://localhost:8080/health) no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="a4392-145">Try accessing [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="a4392-146">Se você vir a resposta esperada “Olá, mundo!”</span><span class="sxs-lookup"><span data-stu-id="a4392-146">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="a4392-147">(e as informações relacionadas à integridade para o ponto de extremidade [/integridade](http://localhost:8080/health)), você implantou com êxito o aplicativo MicroProfile em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="a4392-147">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you have successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="pushing-to-the-azure-container-registry"></a><span data-ttu-id="a4392-148">Enviar por push o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="a4392-148">Pushing to the Azure Container Registry</span></span>

<span data-ttu-id="a4392-149">Agora que criamos e executamos com êxito o aplicativo MicroProfile em nosso computador local, a próxima etapa é enviar por push esse contêiner para o registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="a4392-149">Now that we have successfully built and run our MicroProfile application on our local machine, the next step is to push this container into our container registry.</span></span> <span data-ttu-id="a4392-150">Neste tutorial estamos usando o Registro de Contêiner do Azure, mas qualquer registro de contêiner funcionará (desde que o arquivo `pom.xml` seja editado para apontar para o local relevante).</span><span class="sxs-lookup"><span data-stu-id="a4392-150">In this tutorial we are using the Azure Container Registry, but any container registry will work (as long as the `pom.xml` file is edited to point to the relevant location).</span></span>

1. <span data-ttu-id="a4392-151">Execute `mvn clean package` para limpar, compilar e criar uma imagem do Docker local.</span><span class="sxs-lookup"><span data-stu-id="a4392-151">Run `mvn clean package` to clean, compile, and create a local docker image.</span></span>
2. <span data-ttu-id="a4392-152">Execute `mvn dockerfile:push` para enviar por push ao Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4392-152">Run `mvn dockerfile:push` to push to the Azure Container Registry.</span></span>

<span data-ttu-id="a4392-153">Neste estágio você tem sua imagem de contêiner do Docker carregada no Registro de Contêiner do Azure, mas ele ainda não está em execução, pois agora temos que implantá-lo em uma instância do Aplicativo Web para Contêineres do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4392-153">At this stage you now have your docker container image uploaded to the Azure Container Registry, but it is not yet running as we now have to deploy it into an Azure Web App for Containers instance.</span></span> <span data-ttu-id="a4392-154">Agora faremos isso.</span><span class="sxs-lookup"><span data-stu-id="a4392-154">We will now do that.</span></span>

## <a name="creating-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="a4392-155">Criar uma instância de Aplicativo Web para Contêineres do Azure</span><span class="sxs-lookup"><span data-stu-id="a4392-155">Creating an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="a4392-156">Volte para o [Portal do Azure](http://portal.azure.com) e crie uma nova instância do Aplicativo Web para Contêineres (localizado no título “Web + Móvel” no menu).</span><span class="sxs-lookup"><span data-stu-id="a4392-156">Return to the [Azure Portal](http://portal.azure.com) and create a new Web App for Containers instance (located under the 'Web + Mobile' heading in the menu).</span></span> <span data-ttu-id="a4392-157">Algumas dicas:</span><span class="sxs-lookup"><span data-stu-id="a4392-157">A few pointers:</span></span>

   1. <span data-ttu-id="a4392-158">O nome que você especificar aqui será a URL pública do aplicativo Web (embora um domínio personalizado possa ser adicionado mais tarde, se desejado). Portanto, é uma boa ideia escolher um nome que você possa se lembrar com facilidade.</span><span class="sxs-lookup"><span data-stu-id="a4392-158">The name you specify here will be the public URL of the web app (although a custom domain can be added later if desired), so it is a good idea to pick a name that you can easily remember.</span></span>

   1. <span data-ttu-id="a4392-159">Quando chegar à seção “Configurar contêiner”, você pode selecionar “Registro de Contêiner do Azure” para a “Origem da imagem” e, em seguida, selecionar a imagem correta das listas suspensas.</span><span class="sxs-lookup"><span data-stu-id="a4392-159">When you get to the 'Configure container' section, you can select 'Azure Container Registry' for the 'Image source', and then select the correct image from the drop-down lists.</span></span>

   1. <span data-ttu-id="a4392-160">Não é necessário especificar nenhum valor no campo “Arquivo de inicialização”.</span><span class="sxs-lookup"><span data-stu-id="a4392-160">You do not need to specify any value in the 'Startup File' field.</span></span>

1. <span data-ttu-id="a4392-161">Depois que a instância for criada (novamente, isso é muito rápido), clique nela e, em seguida, clique no item de menu de “Configurações do aplicativo”.</span><span class="sxs-lookup"><span data-stu-id="a4392-161">Once the instance is created (again, it is very quick), click on it and then click on the 'Application Settings' menu item.</span></span> <span data-ttu-id="a4392-162">Aqui você precisa adicionar uma nova configuração de aplicativo, onde a chave é `WEBSITES_PORT` e o valor é `8080`.</span><span class="sxs-lookup"><span data-stu-id="a4392-162">In here you need to add a new application setting, where the key is `WEBSITES_PORT` and the value is `8080`.</span></span> <span data-ttu-id="a4392-163">Isso informa ao Azure a porta que você deseja expor no contêiner e será mapeada para a porta 80 externamente.</span><span class="sxs-lookup"><span data-stu-id="a4392-163">This tells Azure which port you want to expose in the container, and it will be mapped to port 80 externally.</span></span>

1. <span data-ttu-id="a4392-164">Opcionalmente, clique no link “Contêiner do Docker” e habilite a “Implantação contínua”, de modo que sempre que você atualizar a imagem do Registro de Contêiner do Azure ela é atualizada automaticamente na instância do Aplicativo Web para Contêineres do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4392-164">Optionally, click on the 'Docker Container' link, and enable 'Continuous Deployment', so that whenever you update the Azure Container Registry image it is automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="a4392-165">Você deve ser capaz de acessar as instâncias hospedadas no Azure em `http://<appname>.azurewebsites.net/microprofile/api/helloworld` e `http://<appname>.azurewebsites.net/health`.</span><span class="sxs-lookup"><span data-stu-id="a4392-165">You should be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="a4392-166">Resumo</span><span class="sxs-lookup"><span data-stu-id="a4392-166">Summary</span></span>

<span data-ttu-id="a4392-167">Neste tutorial percorremos o processo de criação de um microsserviço baseado em MicroProfile simples, em um contêiner Docker, e o executamos localmente e publicamos no Azure.</span><span class="sxs-lookup"><span data-stu-id="a4392-167">Through this tutorial we have stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, and we have run it locally and published it to Azure.</span></span> <span data-ttu-id="a4392-168">Estender o nosso microsserviço para fornecer funcionalidades mais úteis está fora do escopo deste tutorial, mas há uma grande quantidade de tutoriais e conselhos sobre MicroProfile na Internet e os leitores são incentivados a analisar [MicroProfile.io](https://microprofile.io/) para obter mais conteúdo.</span><span class="sxs-lookup"><span data-stu-id="a4392-168">Extending our microservice to provide more useful functionality is outside the scope of this tutorial, but there is a wealth of tutorials and advice on MicroProfile on the internet, and readers are encouraged to review [MicroProfile.io](https://microprofile.io/) for more content.</span></span>
