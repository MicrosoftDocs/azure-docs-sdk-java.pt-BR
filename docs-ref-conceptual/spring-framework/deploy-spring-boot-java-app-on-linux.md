---
title: Implantar um Aplicativo Web Spring Boot no Linux no Serviço de Contêiner do Azure
description: Este tutorial orienta você pelas etapas de implantar um aplicativo Spring Boot como um aplicativo Web do Linux no Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 30be16aebb18e3c9e18f9a023ea9b82e5d614e94
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339140"
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="88dbd-103">Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="88dbd-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="88dbd-104">Este tutorial mostra como usar o [Docker] para desenvolver e implantar um aplicativo [Spring Boot] em um host do Linux no [Serviço de Contêiner do Azure (AKS)].</span><span class="sxs-lookup"><span data-stu-id="88dbd-104">This tutorial walks you through using [Docker] to develop and deploy a [Spring Boot] application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88dbd-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="88dbd-105">Prerequisites</span></span>

<span data-ttu-id="88dbd-106">Para concluir as etapas deste tutorial, você precisa ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="88dbd-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="88dbd-107">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="88dbd-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="88dbd-108">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="88dbd-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="88dbd-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="88dbd-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="88dbd-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="88dbd-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="88dbd-111">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="88dbd-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="88dbd-112">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="88dbd-112">A [Git] client.</span></span>
* <span data-ttu-id="88dbd-113">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="88dbd-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="88dbd-114">Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="88dbd-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="88dbd-115">Criar o aplicativo Web de Introdução ao Spring Boot no Docker</span><span class="sxs-lookup"><span data-stu-id="88dbd-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="88dbd-116">As etapas a seguir explicarão as etapas necessárias para criar um aplicativo Web Spring Boot simples e testá-lo localmente.</span><span class="sxs-lookup"><span data-stu-id="88dbd-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="88dbd-117">Abra um prompt de comando, crie um diretório local para conter o aplicativo e altere para o diretório. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="88dbd-118">-- ou --</span><span class="sxs-lookup"><span data-stu-id="88dbd-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="88dbd-119">Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório criado. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="88dbd-120">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="88dbd-121">Crie o arquivo JAR usando o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="88dbd-122">Quando o aplicativo Web tiver sido criado, altere o diretório para o diretório `target` em que o arquivo JAR está localizado e inicie o aplicativo Web. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="88dbd-123">Teste o aplicativo Web navegando até ele localmente usando um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="88dbd-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="88dbd-124">Por exemplo, se você tiver ondulação disponível e tiver configurado o servidor Tomcat para ser executado na porta 80:</span><span class="sxs-lookup"><span data-stu-id="88dbd-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="88dbd-125">Você verá a seguinte mensagem exibida: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="88dbd-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="88dbd-127">Criar um Registro de Contêiner do Azure para usar como um Registro do Docker Privado</span><span class="sxs-lookup"><span data-stu-id="88dbd-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="88dbd-128">As etapas a seguir orientam você no uso do portal do Azure para criar um Registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="88dbd-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="88dbd-129">Se você quiser usar a CLI do Azure, em vez do portal do Azure, siga as etapas em [Criar um registro de contêiner do Docker privado usando a CLI do Azure 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="88dbd-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="88dbd-130">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="88dbd-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="88dbd-131">Depois de entrar em sua conta no portal do Azure, você pode seguir as etapas no artigo [Criar um registro de contêiner privado do Docker usando o portal do Azure], que foram parafraseadas nas etapas a seguir para fins de conveniência.</span><span class="sxs-lookup"><span data-stu-id="88dbd-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="88dbd-132">Clique no ícone do menu para **+ Novo** e, em seguida, clique em **Contêineres** e em **Registro de Contêiner do Azure**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Criar um novo Registro de Contêiner do Azure][AR01]

1. <span data-ttu-id="88dbd-134">Quando a página de informações para o modelo de Registro de Contêiner do Azure for exibida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Criar um novo Registro de Contêiner do Azure][AR02]

1. <span data-ttu-id="88dbd-136">Quando a página **Criar registro de contêiner** for exibida, insira seu **Nome do registro** e **Grupo de recursos**, escolha **Habilitar** para o **Usuário administrador** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Definir configurações do registro de contêiner do Azure][AR03]

1. <span data-ttu-id="88dbd-138">Quando o registro de contêiner tiver sido criado, navegue até o registro de contêiner no portal do Azure e, em seguida, clique em **Chaves de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="88dbd-139">Anote o nome de usuário e a senha para as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="88dbd-139">Take note of the username and password for the next steps.</span></span>

   ![Chaves de acesso do Registro de Contêiner do Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="88dbd-141">Configurar o Maven para usar as chaves de acesso do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="88dbd-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="88dbd-142">Navegue até o diretório de configuração para sua instalação do Maven e abra o arquivo *settings.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="88dbd-142">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="88dbd-143">Adicione as configurações de acesso do Registro de Contêiner do Azure da seção anterior deste tutorial para a coleção `<servers>` no arquivo *settings.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-143">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="88dbd-144">Navegue até o diretório do projeto completo de seu aplicativo Spring Boot (por exemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra o arquivo *pom.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="88dbd-144">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="88dbd-145">Atualize a coleção `<properties>` no arquivo *pom.xml* com o valor do servidor de logon para seu Registro de Contêiner do Azure da seção anterior deste tutorial. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-145">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="88dbd-146">Atualize a coleção `<plugins>` no arquivo *pom.xml* para que o `<plugin>` contenha o endereço do servidor de logon e o nome de registro para seu Registro de Contêiner do Azure da seção anterior deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="88dbd-146">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="88dbd-147">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="88dbd-147">For example:</span></span>

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

1. <span data-ttu-id="88dbd-148">Navegue até o diretório de projeto completo para o seu aplicativo Spring Boot e execute o seguinte comando para recompilar o aplicativo e fazer o push do contêiner ao Registro de Contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="88dbd-148">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="88dbd-149">Quando você estiver enviando o contêiner do Docker ao Azure, você poderá receber uma mensagem de erro semelhante a uma das seguintes mesmo que seu contêiner do Docker tenha sido criado com êxito:</span><span class="sxs-lookup"><span data-stu-id="88dbd-149">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="88dbd-150">Se isso acontecer, você poderá entrar na sua conta do Azure usando a linha de comando do Docker. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-150">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="88dbd-151">Você pode fazer o push seu contêiner da linha de comando. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="88dbd-151">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="88dbd-152">Criar um aplicativo Web no Linux no Serviço de Aplicativo do Azure usando a imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="88dbd-152">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="88dbd-153">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="88dbd-153">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="88dbd-154">Clique no ícone do menu para **+ Novo** e, em seguida, clique em **Web + Móvel** e em **Aplicativo Web no Linux**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-154">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Criar um aplicativo Web no portal do Azure][LX01]

3. <span data-ttu-id="88dbd-156">Quando a página **Aplicativo Web no Linux** for exibida, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="88dbd-156">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="88dbd-157"> a.</span><span class="sxs-lookup"><span data-stu-id="88dbd-157">a.</span></span> <span data-ttu-id="88dbd-158">Insira um nome exclusivo para o **Nome do aplicativo**. Por exemplo: "*wingtiptoyslinux*".</span><span class="sxs-lookup"><span data-stu-id="88dbd-158">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="88dbd-159">b.</span><span class="sxs-lookup"><span data-stu-id="88dbd-159">b.</span></span> <span data-ttu-id="88dbd-160">Escolha uma **Assinatura** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="88dbd-160">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="88dbd-161">c.</span><span class="sxs-lookup"><span data-stu-id="88dbd-161">c.</span></span> <span data-ttu-id="88dbd-162">Escolha um **Grupo de Recursos** existente ou especifique um nome para criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="88dbd-162">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="88dbd-163">d.</span><span class="sxs-lookup"><span data-stu-id="88dbd-163">d.</span></span> <span data-ttu-id="88dbd-164">Clique em **Configurar contêiner** e insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="88dbd-164">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="88dbd-165">Escolha **Registro particular**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-165">Choose **Private registry**.</span></span>

   * <span data-ttu-id="88dbd-166">**Marca de imagem e opcional**: especifique o nome do contêiner de antes. Por exemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="88dbd-166">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

   * <span data-ttu-id="88dbd-167">**URL do servidor**: especifique a URL de registro de antes; por exemplo: "*<https://wingtiptoysregistry.azurecr.io>*"</span><span class="sxs-lookup"><span data-stu-id="88dbd-167">**Server URL**: Specify your registry URL from earlier; for example: "*<https://wingtiptoysregistry.azurecr.io>*"</span></span>

   * <span data-ttu-id="88dbd-168">**Nome de usuário de logon** e **Senha**: especifique suas credenciais de logon das **Chaves de Acesso** usadas nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="88dbd-168">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="88dbd-169">e.</span><span class="sxs-lookup"><span data-stu-id="88dbd-169">e.</span></span> <span data-ttu-id="88dbd-170">Depois de ter inserido todas as informações acima, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-170">Once you have entered all of the above information, click **OK**.</span></span>

   ![Definir configurações do aplicativo Web][LX02]

4. <span data-ttu-id="88dbd-172">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-172">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="88dbd-173">O Azure mapeará automaticamente as solicitações de Internet para o servidor Tomcat inserido que está em execução nas portas padrão 80 ou 8080.</span><span class="sxs-lookup"><span data-stu-id="88dbd-173">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="88dbd-174">No entanto, se você tiver configurado seu servidor Tomcat inserido para ser executado em uma porta personalizada, precisará adicionar uma variável de ambiente ao seu aplicativo Web que defina a porta do servidor Tomcat inserido.</span><span class="sxs-lookup"><span data-stu-id="88dbd-174">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="88dbd-175">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="88dbd-175">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="88dbd-176">Navegue até o [portal do Azure] e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="88dbd-176">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="88dbd-177">Clique no ícone **Serviços de Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-177">Click the icon for **App Services**.</span></span> <span data-ttu-id="88dbd-178">(Consulte o item 1 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="88dbd-178">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="88dbd-179">Selecione o aplicativo Web na lista.</span><span class="sxs-lookup"><span data-stu-id="88dbd-179">Select your web app from the list.</span></span> <span data-ttu-id="88dbd-180">(Item 2 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="88dbd-180">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="88dbd-181">Clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-181">Click **Application Settings**.</span></span> <span data-ttu-id="88dbd-182">(Item 3 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="88dbd-182">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="88dbd-183">Na seção **Configurações do aplicativo**, adicione uma nova variável de ambiente denominada **PORTA** e insira seu número da porta personalizada para o valor.</span><span class="sxs-lookup"><span data-stu-id="88dbd-183">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="88dbd-184">(Item 4 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="88dbd-184">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="88dbd-185">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="88dbd-185">Click **Save**.</span></span> <span data-ttu-id="88dbd-186">(Item 5 na imagem abaixo.)</span><span class="sxs-lookup"><span data-stu-id="88dbd-186">(Item #5 in the image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="88dbd-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88dbd-188">Next steps</span></span>

<span data-ttu-id="88dbd-189">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="88dbd-189">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="88dbd-190">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="88dbd-190">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="88dbd-191">Implantar um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="88dbd-191">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="88dbd-192">Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="88dbd-192">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="88dbd-193">Para obter mais detalhes sobre o Spring Boot no projeto de exemplo do Docker, consulte [Introdução ao Spring Boot no Docker].</span><span class="sxs-lookup"><span data-stu-id="88dbd-193">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="88dbd-194">Para obter ajuda na introdução a seus próprios aplicativos Spring Boot, confira **Spring Initializr** em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="88dbd-194">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="88dbd-195">Para obter mais informações de introdução sobre como criar um aplicativo Spring Boot simples, consulte o Spring Initializr em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="88dbd-195">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="88dbd-196">Para obter mais exemplos sobre como usar imagens personalizadas do Docker com o Azure, veja [Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux].</span><span class="sxs-lookup"><span data-stu-id="88dbd-196">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Serviço de Contêiner do Azure (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portal do Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Criar um registro de contêiner privado do Docker usando o portal do Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

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
