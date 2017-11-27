---
title: "Implantar um Aplicativo Web Spring Boot no Linux no Serviço de Contêiner do Azure"
description: "Este tutorial orienta você pelas etapas de implantar um aplicativo Spring Boot como um aplicativo Web do Linux no Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework
ms.assetid: 
ms.service: container-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 8f7b2cbf66c9ceda6f723a9c9d423d94586fc777
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="b7e77-104">Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="b7e77-104">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="b7e77-105">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="b7e77-105">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="b7e77-106">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="b7e77-106">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="b7e77-107">O **[Docker]** é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação, o dimensionamento e o gerenciamento de seus aplicativos executados em contêineres.</span><span class="sxs-lookup"><span data-stu-id="b7e77-107">**[Docker]** is open-source solutions that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="b7e77-108">Este tutorial mostra como usar o Docker para desenvolver e implantar um aplicativo Spring Boot em um host do Linux no [AKS (Serviço de Contêiner do Azure)].</span><span class="sxs-lookup"><span data-stu-id="b7e77-108">This tutorial walks you through using Docker to develop and deploy a Spring Boot application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7e77-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b7e77-109">Prerequisites</span></span>

<span data-ttu-id="b7e77-110">Para concluir as etapas deste tutorial, você precisa ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="b7e77-110">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="b7e77-111">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="b7e77-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b7e77-112">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="b7e77-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="b7e77-113">Um [JDK (Java Developer Kit)] atualizado.</span><span class="sxs-lookup"><span data-stu-id="b7e77-113">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="b7e77-114">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="b7e77-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="b7e77-115">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="b7e77-115">A [Git] client.</span></span>
* <span data-ttu-id="b7e77-116">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="b7e77-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b7e77-117">Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="b7e77-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="b7e77-118">Criar o aplicativo Web de Introdução ao Spring Boot no Docker</span><span class="sxs-lookup"><span data-stu-id="b7e77-118">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="b7e77-119">As etapas a seguir explicarão as etapas necessárias para criar um aplicativo Web Spring Boot simples e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="b7e77-119">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="b7e77-120">Abra um prompt de comando, crie um diretório local para conter o aplicativo e altere para o diretório. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-120">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="b7e77-121">-- ou --</span><span class="sxs-lookup"><span data-stu-id="b7e77-121">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="b7e77-122">Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório criado. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="b7e77-123">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-123">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="b7e77-124">Crie o arquivo JAR usando o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-124">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="b7e77-125">Quando o aplicativo Web tiver sido criado, altere o diretório para o diretório `target` em que o arquivo JAR está localizado e inicie o aplicativo Web. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-125">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="b7e77-126">Teste o aplicativo Web navegando até ele localmente usando um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="b7e77-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="b7e77-127">Por exemplo, se você tiver ondulação disponível e tiver configurado o servidor Tomcat para ser executado na porta 80:</span><span class="sxs-lookup"><span data-stu-id="b7e77-127">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="b7e77-128">Você verá a seguinte mensagem exibida: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="b7e77-128">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="b7e77-130">Criar um Registro de Contêiner do Azure para usar como um Registro do Docker Privado</span><span class="sxs-lookup"><span data-stu-id="b7e77-130">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="b7e77-131">As etapas a seguir orientam você no uso do portal do Azure para criar um Registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7e77-131">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b7e77-132">Se você quiser usar a CLI do Azure, em vez do portal do Azure, siga as etapas em [Criar um registro de contêiner do Docker privado usando a CLI do Azure 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b7e77-132">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="b7e77-133">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="b7e77-133">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="b7e77-134">Depois de entrar em sua conta no portal do Azure, você pode seguir as etapas no artigo [Criar um registro de contêiner privado do Docker usando o portal do Azure], que foram parafraseadas nas etapas a seguir para fins de conveniência.</span><span class="sxs-lookup"><span data-stu-id="b7e77-134">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="b7e77-135">Clique no ícone do menu para **+ Novo** e, em seguida, clique em **Contêineres** e em **Registro de Contêiner do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-135">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Criar um novo Registro de Contêiner do Azure][AR01]

1. <span data-ttu-id="b7e77-137">Quando a página de informações para o modelo de Registro de Contêiner do Azure for exibida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-137">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Criar um novo Registro de Contêiner do Azure][AR02]

1. <span data-ttu-id="b7e77-139">Quando a página **Criar registro de contêiner** for exibida, insira seu **Nome do registro** e **Grupo de recursos**, escolha **Habilitar** para o **Usuário administrador** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-139">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Definir configurações do registro de contêiner do Azure][AR03]

1. <span data-ttu-id="b7e77-141">Quando o registro de contêiner tiver sido criado, navegue até o registro de contêiner no portal do Azure e, em seguida, clique em **Chaves de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-141">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="b7e77-142">Anote o nome de usuário e a senha para as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="b7e77-142">Take note of the username and password for the next steps.</span></span>

   ![Chaves de acesso do Registro de Contêiner do Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="b7e77-144">Configurar o Maven para usar as chaves de acesso do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="b7e77-144">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="b7e77-145">Navegue até o diretório de configuração para sua instalação do Maven e abra o arquivo *settings.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b7e77-145">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="b7e77-146">Adicione as configurações de acesso do Registro de Contêiner do Azure da seção anterior deste tutorial para a coleção `<servers>` no arquivo *settings.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-146">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="b7e77-147">Navegue até o diretório do projeto completo de seu aplicativo Spring Boot (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra o arquivo *pom.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b7e77-147">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="b7e77-148">Atualize a coleção `<properties>` no arquivo *pom.xml* com o valor do servidor de logon para seu Registro de Contêiner do Azure da seção anterior deste tutorial. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-148">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="b7e77-149">Atualize a coleção `<plugins>` no arquivo *pom.xml* para que o `<plugin>` contenha o endereço do servidor de logon e o nome de registro para seu Registro de Contêiner do Azure da seção anterior deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b7e77-149">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="b7e77-150">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-150">For example:</span></span>

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

1. <span data-ttu-id="b7e77-151">Navegue até o diretório de projeto completo para o seu aplicativo Spring Boot e execute o seguinte comando para recompilar o aplicativo e fazer o push do contêiner ao Registro de Contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="b7e77-151">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="b7e77-152">Quando você estiver enviando o contêiner do Docker ao Azure, você poderá receber uma mensagem de erro semelhante a uma das seguintes mesmo que seu contêiner do Docker tenha sido criado com êxito:</span><span class="sxs-lookup"><span data-stu-id="b7e77-152">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="b7e77-153">Se isso acontecer, você poderá entrar na sua conta do Azure usando a linha de comando do Docker. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-153">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="b7e77-154">Você pode fazer o push seu contêiner da linha de comando. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b7e77-154">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="b7e77-155">Criar um aplicativo Web no Linux no Serviço de Aplicativo do Azure usando a imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="b7e77-155">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="b7e77-156">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="b7e77-156">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="b7e77-157">Clique no ícone do menu para **+ Novo** e, em seguida, clique em **Web + Móvel** e em **Aplicativo Web no Linux**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-157">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Criar um aplicativo Web no portal do Azure][LX01]

1. <span data-ttu-id="b7e77-159">Quando a página **Aplicativo Web no Linux** for exibida, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="b7e77-159">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="b7e77-160">a.</span><span class="sxs-lookup"><span data-stu-id="b7e77-160">a.</span></span> <span data-ttu-id="b7e77-161">Insira um nome exclusivo para o **Nome do aplicativo**. Por exemplo: "*wingtiptoyslinux*".</span><span class="sxs-lookup"><span data-stu-id="b7e77-161">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="b7e77-162">b.</span><span class="sxs-lookup"><span data-stu-id="b7e77-162">b.</span></span> <span data-ttu-id="b7e77-163">Escolha uma **Assinatura** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="b7e77-163">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="b7e77-164">c.</span><span class="sxs-lookup"><span data-stu-id="b7e77-164">c.</span></span> <span data-ttu-id="b7e77-165">Escolha um **Grupo de Recursos** existente ou especifique um nome para criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b7e77-165">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="b7e77-166">d.</span><span class="sxs-lookup"><span data-stu-id="b7e77-166">d.</span></span> <span data-ttu-id="b7e77-167">Clique em **Configurar contêiner** e insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="b7e77-167">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="b7e77-168">Escolha **Registro particular**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-168">Choose **Private registry**.</span></span>

      * <span data-ttu-id="b7e77-169">**Marca de imagem e opcional**: especifique o nome do contêiner de antes. Por exemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="b7e77-169">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="b7e77-170">**URL do servidor**: especifique a URL de registro de antes; por exemplo: "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="b7e77-170">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="b7e77-171">**Nome de usuário de logon** e **Senha**: especifique suas credenciais de logon das **Chaves de Acesso** usadas nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="b7e77-171">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="b7e77-172">e.</span><span class="sxs-lookup"><span data-stu-id="b7e77-172">e.</span></span> <span data-ttu-id="b7e77-173">Depois de ter inserido todas as informações acima, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-173">Once you have entered all of the above information, click **OK**.</span></span>

   ![Definir configurações do aplicativo Web][LX02]

1. <span data-ttu-id="b7e77-175">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-175">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b7e77-176">O Azure mapeará automaticamente as solicitações de Internet para o servidor Tomcat inserido que está em execução nas portas padrão 80 ou 8080.</span><span class="sxs-lookup"><span data-stu-id="b7e77-176">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="b7e77-177">No entanto, se você tiver configurado seu servidor Tomcat inserido para ser executado em uma porta personalizada, precisará adicionar uma variável de ambiente ao seu aplicativo Web que defina a porta do servidor Tomcat inserido.</span><span class="sxs-lookup"><span data-stu-id="b7e77-177">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="b7e77-178">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b7e77-178">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="b7e77-179">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="b7e77-179">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="b7e77-180">Clique no ícone **Serviços de Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-180">Click the icon for **App Services**.</span></span> <span data-ttu-id="b7e77-181">(Consulte o item 1 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="b7e77-181">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="b7e77-182">Selecione o aplicativo Web na lista.</span><span class="sxs-lookup"><span data-stu-id="b7e77-182">Select your web app from the list.</span></span> <span data-ttu-id="b7e77-183">(Item 2 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="b7e77-183">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="b7e77-184">Clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-184">Click **Application Settings**.</span></span> <span data-ttu-id="b7e77-185">(Item 3 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="b7e77-185">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="b7e77-186">Na seção **Configurações do aplicativo**, adicione uma nova variável de ambiente denominada **PORTA** e insira seu número da porta personalizada para o valor.</span><span class="sxs-lookup"><span data-stu-id="b7e77-186">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="b7e77-187">(Item 4 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="b7e77-187">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="b7e77-188">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b7e77-188">Click **Save**.</span></span> <span data-ttu-id="b7e77-189">(Item 5 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="b7e77-189">(Item #5 in the image below.)</span></span>
>
> ![Como salvar um número da porta personalizado no portal do Azure][LX03]
>

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

## <a name="next-steps"></a><span data-ttu-id="b7e77-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7e77-191">Next steps</span></span>

<span data-ttu-id="b7e77-192">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b7e77-192">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="b7e77-193">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b7e77-193">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="b7e77-194">Implantar um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="b7e77-194">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="b7e77-195">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b7e77-195">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="b7e77-196">Para obter mais detalhes sobre o Spring Boot no projeto de exemplo do Docker, consulte [Introdução ao Spring Boot no Docker].</span><span class="sxs-lookup"><span data-stu-id="b7e77-196">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="b7e77-197">Para obter ajuda na introdução a seus próprios aplicativos Spring Boot, confira **Spring Initializr** em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="b7e77-197">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="b7e77-198">Para obter mais informações sobre como começar a criar um aplicativo Spring Boot simples, consulte o Spring Initializr em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="b7e77-198">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="b7e77-199">Para obter exemplos adicionais sobre como usar imagens personalizadas do Docker com o Azure, consulte [Usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux].</span><span class="sxs-lookup"><span data-stu-id="b7e77-199">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[AKS (Serviço de Contêiner do Azure)]: https://azure.microsoft.com/services/container-service/
[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[portal do Azure]: https://portal.azure.com/
[Criar um registro de contêiner privado do Docker usando o portal do Azure]: /azure/container-registry/container-registry-get-started-portal
[Usando uma imagem personalizada do Docker para o aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
