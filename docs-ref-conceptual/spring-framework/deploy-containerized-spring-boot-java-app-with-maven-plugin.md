---
title: Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure
description: Saiba como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: d9f2cf5c15bb8f990c8e82fddd6455ecbf8cc02c
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090759"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="3c6c9-103">Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure</span><span class="sxs-lookup"><span data-stu-id="3c6c9-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="3c6c9-104">Este artigo demonstra como usar o [plug-in do Maven para Aplicativos Web do Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) a fim de implantar um exemplo de aplicativo Spring Boot em um contêiner do Docker para os Serviços de Aplicativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-104">This article demonstrates using the [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="3c6c9-105">O Plug-in do Maven para Aplicativos Web do Azure para [Apache Maven](http://maven.apache.org/) fornece uma integração perfeita do Serviço de Aplicativo do Azure em projetos Maven e simplifica o processo para os desenvolvedores implantarem aplicativos Web no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="3c6c9-106">O plug-in do Maven para Aplicativos Web do Azure está disponível no momento como uma versão prévia.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="3c6c9-107">Por enquanto, há suporte somente para a publicação FTP, embora existam planos para recursos adicionais futuros.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="3c6c9-108">pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3c6c9-108">Prerequisites</span></span>

<span data-ttu-id="3c6c9-109">Para concluir as etapas deste tutorial, você precisa ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="3c6c9-110">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="3c6c9-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="3c6c9-111">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="3c6c9-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="3c6c9-112">Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="3c6c9-113">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="3c6c9-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="3c6c9-114">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="3c6c9-114">A [Git] client.</span></span>
* <span data-ttu-id="3c6c9-115">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="3c6c9-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3c6c9-116">Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="3c6c9-117">Clonar o exemplo de Spring Boot no aplicativo Web do Docker</span><span class="sxs-lookup"><span data-stu-id="3c6c9-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="3c6c9-118">Nesta seção, você clonará um aplicativo Spring Boot em contêineres e o testará localmente.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="3c6c9-119">Abra um prompt de comando ou janela de terminal e crie um diretório local para conter o aplicativo Spring Boot, e altere para esse diretório; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="3c6c9-120">-- ou --</span><span class="sxs-lookup"><span data-stu-id="3c6c9-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="3c6c9-121">Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório criado. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. <span data-ttu-id="3c6c9-122">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="3c6c9-123">Crie o arquivo JAR usando o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="3c6c9-124">Após a criação do aplicativo Web, inicie-o usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="3c6c9-125">Teste o aplicativo Web navegando até ele localmente usando um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="3c6c9-126">Por exemplo, use o comando a seguir, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="3c6c9-127">Você verá a seguinte mensagem exibida: **Olá, Mundo Docker**</span><span class="sxs-lookup"><span data-stu-id="3c6c9-127">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="3c6c9-128">Criar uma entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="3c6c9-128">Create an Azure service principal</span></span>

<span data-ttu-id="3c6c9-129">Nesta seção, você criará uma entidade de serviço do Azure que será usada pelo plug-in do Maven durante a implantação de seu contêiner no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-129">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="3c6c9-130">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-130">Open a command prompt.</span></span>

2. <span data-ttu-id="3c6c9-131">Entre em sua conta do Azure usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-131">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="3c6c9-132">Siga as instruções na tela para concluir o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-132">Follow the instructions to complete the sign-in process.</span></span>

3. <span data-ttu-id="3c6c9-133">Crie uma entidade de serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="3c6c9-134">Em que:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-134">Where:</span></span>

   | <span data-ttu-id="3c6c9-135">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3c6c9-135">Parameter</span></span>  |                    <span data-ttu-id="3c6c9-136">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="3c6c9-136">Description</span></span>                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | <span data-ttu-id="3c6c9-137">Especifica o nome de usuário para a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-137">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="3c6c9-138">Especifica a senha para a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-138">Specifies the password for the service principal.</span></span>  |


4. <span data-ttu-id="3c6c9-139">O Azure responde com um JSON parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-139">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="3c6c9-140">Você usará os valores dessa resposta em JSON ao configurar o plug-in do Maven para implantar seu contêiner no Azure, .</span><span class="sxs-lookup"><span data-stu-id="3c6c9-140">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="3c6c9-141">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` e `tttttttt` são valores de espaço reservado, usados neste exemplo para facilitar o mapeamento desses valores para seus respectivos elementos durante a configuração de seu arquivo `settings.xml` do Maven na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-141">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="3c6c9-142">Configurar o Maven para usar a entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="3c6c9-142">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="3c6c9-143">Nesta seção, você usará os valores de sua entidade de serviço do Azure para configurar a autenticação usada pelo Maven durante a implantação de seu contêiner no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-143">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="3c6c9-144">Abra seu arquivo `settings.xml` do Maven em um editor de texto; esse arquivo pode estar em um caminho como os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-144">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. <span data-ttu-id="3c6c9-145">Adicione as configurações de sua entidade de serviço do Azure da seção anterior deste tutorial à coleção `<servers>` no arquivo *settings.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-145">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="3c6c9-146">Em que:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-146">Where:</span></span>

   |     <span data-ttu-id="3c6c9-147">Elemento</span><span class="sxs-lookup"><span data-stu-id="3c6c9-147">Element</span></span>     |                                                                                   <span data-ttu-id="3c6c9-148">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="3c6c9-148">Description</span></span>                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                <span data-ttu-id="3c6c9-149">Especifica um nome exclusivo usado pelo Maven para analisar suas configurações de segurança durante a implantação de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-149">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>                                |
   |   `<client>`    |                                                             <span data-ttu-id="3c6c9-150">Contém o valor `appId` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-150">Contains the `appId` value from your service principal.</span></span>                                                             |
   |   `<tenant>`    |                                                            <span data-ttu-id="3c6c9-151">Contém o valor `tenant` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-151">Contains the `tenant` value from your service principal.</span></span>                                                             |
   |     `<key>`     |                                                           <span data-ttu-id="3c6c9-152">Contém o valor `password` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-152">Contains the `password` value from your service principal.</span></span>                                                            |
   | `<environment>` | <span data-ttu-id="3c6c9-153">Define o ambiente de nuvem do Azure de destino, que é `AZURE` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-153">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="3c6c9-154">(Uma lista completa dos ambientes está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure])</span><span class="sxs-lookup"><span data-stu-id="3c6c9-154">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |


3. <span data-ttu-id="3c6c9-155">Salve e feche o arquivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-155">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="3c6c9-156">OPCIONAL: Implantar o arquivo local do Docker no Hub do Docker</span><span class="sxs-lookup"><span data-stu-id="3c6c9-156">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="3c6c9-157">Se você tiver uma conta do Docker, poderá compilar sua imagem de contêiner do Docker localmente e enviá-la por push ao Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-157">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="3c6c9-158">Para fazer isso, use as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-158">To do so, use the following steps.</span></span>

1. <span data-ttu-id="3c6c9-159">Abra o arquivo `pom.xml` de seu aplicativo Spring Boot em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-159">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="3c6c9-160">Localize o elemento filho `<imageName>` do elemento `<containerSettings>`.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-160">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="3c6c9-161">Atualize o valor `${docker.image.prefix}` com o nome de sua conta do Docker:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-161">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="3c6c9-162">Escolha um dos seguintes métodos de implantação:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-162">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="3c6c9-163">Compile sua imagem de contêiner localmente com o Maven, e use o Docker para enviar seu contêiner por push para o Hub do Docker:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-163">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```

   * <span data-ttu-id="3c6c9-164">Se o [Plug-in do Docker para o Maven] estiver instalado, você poderá compilar automaticamente a imagem de seu contêiner no Hub do Docker usando o parâmetro `-DpushImage`:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-164">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="3c6c9-165">OPCIONAL: Personalizar seu pom.xml antes de implantar seu contêiner no Azure</span><span class="sxs-lookup"><span data-stu-id="3c6c9-165">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="3c6c9-166">Abra o arquivo `pom.xml` de seu aplicativo Spring Boot em um editor de texto e localize o elemento `<plugin>` para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-166">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="3c6c9-167">Esse elemento deverá se parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-167">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="3c6c9-168">Você pode modificar diversos valores do plug-in do Maven, e há uma descrição detalhada de cada um desses elementos disponível na documentação [Plug-in do Maven para aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="3c6c9-168">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="3c6c9-169">Dito isso, vale a pena destacar diversos valores neste artigo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-169">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="3c6c9-170">Elemento</span><span class="sxs-lookup"><span data-stu-id="3c6c9-170">Element</span></span> | <span data-ttu-id="3c6c9-171">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="3c6c9-171">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="3c6c9-172">Especifica a versão do [Plug-in do Maven para aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="3c6c9-172">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="3c6c9-173">Você deve verificar a versão listada no [Repositório Central do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para garantir que esteja usando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-173">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="3c6c9-174">Especifica as informações de autenticação do Azure, que, neste exemplo, contêm um elemento `<serverId>` contendo `azure-auth`; o Maven usa esse valor para procurar os valores de entidade de serviço do Azure em seu arquivo *settings.xml* do Maven, que você definiu em uma seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-174">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="3c6c9-175">Especifica o grupo de recursos de destino, que é `maven-plugin` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-175">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="3c6c9-176">Esse grupo de recursos será criado durante a implantação, caso ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-176">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="3c6c9-177">Especifica o nome de destino de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-177">Specifies the target name for your web app.</span></span> <span data-ttu-id="3c6c9-178">Neste exemplo, o nome de destino é `maven-linux-app-${maven.build.timestamp}`, no qual o sufixo `${maven.build.timestamp}` é acrescentado neste exemplo para evitar conflitos.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-178">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="3c6c9-179">(O carimbo de data/hora é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="3c6c9-179">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="3c6c9-180">Especifica a região de destino, que neste exemplo é `westus`.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-180">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="3c6c9-181">(Uma lista completa está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure])</span><span class="sxs-lookup"><span data-stu-id="3c6c9-181">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<appSettings>` | <span data-ttu-id="3c6c9-182">Especifica quaisquer configurações exclusivas para o Maven usar ao implantar seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-182">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="3c6c9-183">Neste exemplo, um elemento `<property>` contém um par de nome/valor de elementos filho que especifique a porta para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-183">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="3c6c9-184">As configurações de alteração do número da porta neste exemplo só serão necessárias quando você estiver alterando a porta padrão.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-184">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="3c6c9-185">Compilar e implantar o contêiner no Azure</span><span class="sxs-lookup"><span data-stu-id="3c6c9-185">Build and deploy your container to Azure</span></span>

<span data-ttu-id="3c6c9-186">Depois de definir todas as configurações nas seções anteriores deste artigo, você estará pronto para implantar seu contêiner no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-186">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="3c6c9-187">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-187">To do so, use the following steps:</span></span>

1. <span data-ttu-id="3c6c9-188">Do prompt de comando ou janela de terminal que você estava usando antes, recompile o arquivo JAR usando o Maven, se você tiver feito alterações no arquivo *pom.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-188">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="3c6c9-189">Implante seu aplicativo Web no Azure usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-189">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="3c6c9-190">O Maven implantará seu aplicativo Web no Azure; se o aplicativo web ainda não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-190">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3c6c9-191">Se a região que você especificou no elemento `<region>` de seu arquivo *pom.xml* não tiver servidores suficientes disponíveis no início de sua implantação, talvez você veja um erro semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-191">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="3c6c9-192">Se isso acontecer, especifique outra região e execute novamente o comando do Maven para implantar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c6c9-192">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="3c6c9-193">Após a implantação de sua Web, você poderá gerenciá-la usando o [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="3c6c9-193">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="3c6c9-194">Seu aplicativo Web será listado nos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-194">Your web app will be listed in **App Services**:</span></span>

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* <span data-ttu-id="3c6c9-196">E a URL para seu aplicativo Web será listada na **Visão geral** de seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-196">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Como determinar a URL de seu aplicativo Web][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="3c6c9-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c6c9-198">Next steps</span></span>

<span data-ttu-id="3c6c9-199">Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c6c9-199">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="3c6c9-200">[Plug-in do Maven para aplicativos Web do Azure]</span><span class="sxs-lookup"><span data-stu-id="3c6c9-200">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="3c6c9-201">Faça logon no Azure na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3c6c9-201">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="3c6c9-202">Como usar o Plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="3c6c9-202">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service </span></span>](deploy-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="3c6c9-203">Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="3c6c9-203">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="3c6c9-204">Referência de configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="3c6c9-204">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="3c6c9-205">[Plug-in do Docker para o Maven]</span><span class="sxs-lookup"><span data-stu-id="3c6c9-205">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portal do Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Plug-in do Docker para o Maven]: https://github.com/spotify/docker-maven-plugin
[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Benefícios do assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Plug-in do Maven para aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP02.png
