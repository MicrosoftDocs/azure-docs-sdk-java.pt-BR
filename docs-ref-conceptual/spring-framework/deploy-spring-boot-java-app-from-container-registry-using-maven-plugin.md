---
title: "Como usar o Plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Registro de Contêiner do Azure ao Serviço de Aplicativo do Azure"
description: "Este tutorial percorrerá as etapas para implantar um aplicativo Spring Boot do Registro de Contêiner do Azure no Serviço de Aplicativo do Azure usando um plug-in do Maven."
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: multiple
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: b7c2735cdcdeb3dcbfe91fad6c57616e4e5c620c
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="a1233-104">Como usar o Plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Registro de Contêiner do Azure ao Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a1233-104">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="a1233-105">**[Spring Framework]** é um framework de software livre popular que ajuda os desenvolvedores de Java a criar aplicativos de API, Web e móveis.</span><span class="sxs-lookup"><span data-stu-id="a1233-105">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="a1233-106">Este tutorial usa um aplicativo de exemplo criado usando o [Spring Boot], uma abordagem controlada por convenção para o uso do Spring para começar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a1233-106">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="a1233-107">Este artigo demonstra como implantar um exemplo de aplicativo Spring Boot no Registro de Contêiner do Azure e, depois, usar o plug-in do Maven para Aplicativos Web do Azure a fim de implantar seu aplicativo nos Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-107">This article demonstrates how to deploy a sample Spring Boot application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a1233-108">O plug-in do Maven para Aplicativos Web do Azure está disponível no momento como uma versão prévia.</span><span class="sxs-lookup"><span data-stu-id="a1233-108">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="a1233-109">Por enquanto, há suporte somente para a publicação FTP, embora existam planos para recursos adicionais futuros.</span><span class="sxs-lookup"><span data-stu-id="a1233-109">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="a1233-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a1233-110">Prerequisites</span></span>

<span data-ttu-id="a1233-111">Para concluir as etapas deste tutorial, você precisa ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="a1233-111">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="a1233-112">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="a1233-112">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a1233-113">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="a1233-113">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="a1233-114">Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.</span><span class="sxs-lookup"><span data-stu-id="a1233-114">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="a1233-115">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="a1233-115">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="a1233-116">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="a1233-116">A [Git] client.</span></span>
* <span data-ttu-id="a1233-117">Um cliente do [Docker].</span><span class="sxs-lookup"><span data-stu-id="a1233-117">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a1233-118">Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.</span><span class="sxs-lookup"><span data-stu-id="a1233-118">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="a1233-119">Clonar o exemplo de Spring Boot no aplicativo Web do Docker</span><span class="sxs-lookup"><span data-stu-id="a1233-119">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="a1233-120">Nesta seção, você clonará um aplicativo Spring Boot em contêineres e o testará localmente.</span><span class="sxs-lookup"><span data-stu-id="a1233-120">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="a1233-121">Abra um prompt de comando ou janela de terminal e crie um diretório local para conter o aplicativo Spring Boot, e altere para esse diretório; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-121">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="a1233-122">-- ou --</span><span class="sxs-lookup"><span data-stu-id="a1233-122">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="a1233-123">Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório criado. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-123">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="a1233-124">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-124">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="a1233-125">Crie o arquivo JAR usando o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-125">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="a1233-126">Após a criação do aplicativo Web, inicie-o usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-126">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="a1233-127">Teste o aplicativo Web navegando até ele localmente usando um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="a1233-127">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="a1233-128">Por exemplo, use o comando a seguir, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="a1233-128">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="a1233-129">Você verá a seguinte mensagem exibida: **Olá, Mundo Docker**</span><span class="sxs-lookup"><span data-stu-id="a1233-129">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Procurar aplicativo de exemplo localmente][SB01]

> [!NOTE]
>
> <span data-ttu-id="a1233-131">Quando você estiver usando o Docker localmente, verá um erro informando que não pode conectar o host local na porta 2375.</span><span class="sxs-lookup"><span data-stu-id="a1233-131">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="a1233-132">Se isso acontecer, você precisará habilitar o uso do Docker localmente sem TLS.</span><span class="sxs-lookup"><span data-stu-id="a1233-132">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="a1233-133">Para tanto, abra as configurações do Docker e marque a opção para **Expor o Daemon do Docker em TCP://localhost:2375 sem TLS**.</span><span class="sxs-lookup"><span data-stu-id="a1233-133">To do so, open your Docker settings and check the option to **Expose Docker Daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![Expor o daemon do Docker na porta TCP 2375 local][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="a1233-135">Criar uma entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="a1233-135">Create an Azure service principal</span></span>

<span data-ttu-id="a1233-136">Nesta seção, você criará uma entidade de serviço do Azure que será usada pelo plug-in do Maven durante a implantação de seu contêiner no Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-136">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="a1233-137">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="a1233-137">Open a command prompt.</span></span>

1. <span data-ttu-id="a1233-138">Entre em sua conta do Azure usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="a1233-138">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="a1233-139">Siga as instruções na tela para concluir o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="a1233-139">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="a1233-140">Crie uma entidade de serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="a1233-140">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="a1233-141">Onde `uuuuuuuu` é o nome de usuário e `pppppppp` é a senha para a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="a1233-141">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="a1233-142">O Azure responde com um JSON parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1233-142">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="a1233-143">Você usará os valores dessa resposta em JSON ao configurar o plug-in do Maven para implantar seu contêiner no Azure, .</span><span class="sxs-lookup"><span data-stu-id="a1233-143">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="a1233-144">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` e `tttttttt` são valores de espaço reservado, usados neste exemplo para facilitar o mapeamento desses valores para seus respectivos elementos durante a configuração de seu arquivo `settings.xml` do Maven na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="a1233-144">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="a1233-145">Criar um Registro de Contêiner do Azure usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a1233-145">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="a1233-146">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="a1233-146">Open a command prompt.</span></span>

1. <span data-ttu-id="a1233-147">Faça logon na sua Conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="a1233-147">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="a1233-148">Crie um grupo de recursos para os recursos do Azure usados neste artigo:</span><span class="sxs-lookup"><span data-stu-id="a1233-148">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="a1233-149">Substitua `wingtiptoysresources` neste exemplo por um nome exclusivo para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1233-149">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="a1233-150">Crie um registro de contêiner privado do Azure no grupo de recursos para seu aplicativo Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="a1233-150">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="a1233-151">Substitua `wingtiptoysregistry` neste exemplo por um nome exclusivo para seu registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="a1233-151">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="a1233-152">Recupere a senha de seu registro de contêiner:</span><span class="sxs-lookup"><span data-stu-id="a1233-152">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="a1233-153">O Azure responderá com sua senha; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-153">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="a1233-154">Adicionar seu registro de contêiner do Azure e a entidade de serviço do Azure às suas configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="a1233-154">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="a1233-155">Abra seu arquivo `settings.xml` do Maven em um editor de texto; esse arquivo pode estar em um caminho como os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1233-155">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="a1233-156">Adicione as configurações de acesso do Registro de Contêiner do Azure da seção anterior deste artigo para a coleção `<servers>` no arquivo *settings.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-156">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="a1233-157">Em que:</span><span class="sxs-lookup"><span data-stu-id="a1233-157">Where:</span></span>
   <span data-ttu-id="a1233-158">Elemento</span><span class="sxs-lookup"><span data-stu-id="a1233-158">Element</span></span> | <span data-ttu-id="a1233-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="a1233-159">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="a1233-160">Contém o nome de seu Registro de Contêiner privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-160">Contains the name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="a1233-161">Contém o nome de seu Registro de Contêiner privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-161">Contains the name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="a1233-162">Contém a senha que você recuperou na seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a1233-162">Contains the password you retrieved in the previous section of this article.</span></span>

1. <span data-ttu-id="a1233-163">Adicione as configurações de sua entidade de serviço do Azure de uma seção anterior deste artigo à coleção `<servers>` no arquivo *settings.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-163">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="a1233-164">Em que:</span><span class="sxs-lookup"><span data-stu-id="a1233-164">Where:</span></span>
   <span data-ttu-id="a1233-165">Elemento</span><span class="sxs-lookup"><span data-stu-id="a1233-165">Element</span></span> | <span data-ttu-id="a1233-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="a1233-166">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="a1233-167">Especifica um nome exclusivo usado pelo Maven para analisar suas configurações de segurança durante a implantação de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-167">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="a1233-168">Contém o valor `appId` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="a1233-168">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="a1233-169">Contém o valor `tenant` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="a1233-169">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="a1233-170">Contém o valor `password` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="a1233-170">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="a1233-171">Define o ambiente de nuvem do Azure de destino, que é `AZURE` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="a1233-171">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="a1233-172">(Uma lista completa dos ambientes está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure])</span><span class="sxs-lookup"><span data-stu-id="a1233-172">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="a1233-173">Salve e feche o arquivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="a1233-173">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="a1233-174">Compilar imagem de contêiner do Docker e enviá-la por push ao registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="a1233-174">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="a1233-175">Navegue até o diretório de projeto completo para o seu aplicativo Spring Boot (por exemplo: "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra o arquivo *pom.xml* com um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="a1233-175">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="a1233-176">Atualize a coleção `<properties>` no arquivo *pom.xml* com o valor do servidor de logon para seu Registro de Contêiner do Azure da seção anterior deste tutorial. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-176">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="a1233-177">Em que:</span><span class="sxs-lookup"><span data-stu-id="a1233-177">Where:</span></span>
   <span data-ttu-id="a1233-178">Elemento</span><span class="sxs-lookup"><span data-stu-id="a1233-178">Element</span></span> | <span data-ttu-id="a1233-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="a1233-179">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="a1233-180">Especifica o nome de seu Registro de Contêiner privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-180">Specifies the name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="a1233-181">Especifica a URL de seu Registro de Contêiner privado do Azure, que é derivado acrescentando ".azurecr.io" ao nome de seu registro de contêiner privado.</span><span class="sxs-lookup"><span data-stu-id="a1233-181">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span>

1. <span data-ttu-id="a1233-182">Verifique se `<plugin>` para o plug-in do Docker em seu arquivo *pom.xml* contém as propriedades corretas para o endereço do servidor de logon e nome do registro da etapa anterior neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a1233-182">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="a1233-183">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-183">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="a1233-184">Em que:</span><span class="sxs-lookup"><span data-stu-id="a1233-184">Where:</span></span>
   <span data-ttu-id="a1233-185">Elemento</span><span class="sxs-lookup"><span data-stu-id="a1233-185">Element</span></span> | <span data-ttu-id="a1233-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="a1233-186">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="a1233-187">Especifica a propriedade que contém o nome de seu Registro de Contêiner privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-187">Specifies the property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="a1233-188">Especifica a propriedade que contém a URL de seu Registro de Contêiner privado do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-188">Specifies the property which contains the URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="a1233-189">Navegue até o diretório de projeto completo para o seu aplicativo Spring Boot e execute o seguinte comando para recompilar o aplicativo e fazer o push do contêiner ao registro de contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="a1233-189">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="a1233-190">OPCIONAL: navegue até o [Portal do Azure] e verifique se há uma imagem de contêiner do Docker chamada **gs-spring-boot-docker** no registro do contêiner.</span><span class="sxs-lookup"><span data-stu-id="a1233-190">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Verificar o contêiner no Portal do Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="a1233-192">Personalizar seu pom.xml e, depois, compilar e implantar o contêiner no Azure</span><span class="sxs-lookup"><span data-stu-id="a1233-192">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="a1233-193">Abra o arquivo `pom.xml` de seu aplicativo Spring Boot em um editor de texto e localize o elemento `<plugin>` para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="a1233-193">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="a1233-194">Esse elemento deverá se parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-194">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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

<span data-ttu-id="a1233-195">Você pode modificar diversos valores do plug-in do Maven, e há uma descrição detalhada de cada um desses elementos disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="a1233-195">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="a1233-196">Dito isso, vale a pena destacar diversos valores neste artigo:</span><span class="sxs-lookup"><span data-stu-id="a1233-196">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="a1233-197">Elemento</span><span class="sxs-lookup"><span data-stu-id="a1233-197">Element</span></span> | <span data-ttu-id="a1233-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="a1233-198">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="a1233-199">Especifica a versão do [Plug-in do Maven para Aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="a1233-199">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="a1233-200">Você deve verificar a versão listada no [Repositório Central do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para garantir que esteja usando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="a1233-200">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="a1233-201">Especifica as informações de autenticação do Azure, que, neste exemplo, contêm um elemento `<serverId>` contendo `azure-auth`; o Maven usa esse valor para procurar os valores de entidade de serviço do Azure em seu arquivo *settings.xml* do Maven, que você definiu em uma seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a1233-201">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="a1233-202">Especifica o grupo de recursos de destino, que é `wingtiptoysresources` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="a1233-202">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="a1233-203">Esse grupo de recursos será criado durante a implantação, caso ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="a1233-203">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="a1233-204">Especifica o nome de destino de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a1233-204">Specifies the target name for your web app.</span></span> <span data-ttu-id="a1233-205">Neste exemplo, o nome de destino é `maven-linux-app-${maven.build.timestamp}`, no qual o sufixo `${maven.build.timestamp}` é acrescentado neste exemplo para evitar conflitos.</span><span class="sxs-lookup"><span data-stu-id="a1233-205">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="a1233-206">(O carimbo de data/hora é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="a1233-206">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="a1233-207">Especifica a região de destino, que neste exemplo é `westus`.</span><span class="sxs-lookup"><span data-stu-id="a1233-207">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="a1233-208">(Uma lista completa está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure])</span><span class="sxs-lookup"><span data-stu-id="a1233-208">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="a1233-209">Especifica as propriedades que contêm o nome e a URL de seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="a1233-209">Specifies the properties which contain the name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="a1233-210">Especifica quaisquer configurações exclusivas para o Maven usar ao implantar seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="a1233-210">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="a1233-211">Neste exemplo, um elemento `<property>` contém um par de nome/valor de elementos filho que especifique a porta para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1233-211">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a1233-212">As configurações de alteração do número da porta neste exemplo só serão necessárias quando você estiver alterando a porta padrão.</span><span class="sxs-lookup"><span data-stu-id="a1233-212">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="a1233-213">Do prompt de comando ou janela de terminal que você estava usando antes, recompile o arquivo JAR usando o Maven, se você tiver feito alterações no arquivo *pom.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-213">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="a1233-214">Implante seu aplicativo Web no Azure usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a1233-214">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="a1233-215">O Maven implantará seu aplicativo Web no Azure; se o aplicativo web ainda não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="a1233-215">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a1233-216">Se a região que você especificou no elemento `<region>` de seu arquivo *pom.xml* não tiver servidores suficientes disponíveis no início de sua implantação, talvez você veja um erro semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1233-216">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="a1233-217">Se isso acontecer, especifique outra região e execute novamente o comando do Maven para implantar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1233-217">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="a1233-218">Após a implantação de sua Web, você poderá gerenciá-la usando o [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="a1233-218">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="a1233-219">Seu aplicativo Web será listado nos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="a1233-219">Your web app will be listed in **App Services**:</span></span>

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* <span data-ttu-id="a1233-221">E a URL para seu aplicativo Web será listada na **Visão geral** de seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="a1233-221">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Como determinar a URL de seu aplicativo Web][AP02]

## <a name="next-steps"></a><span data-ttu-id="a1233-223">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1233-223">Next steps</span></span>

<span data-ttu-id="a1233-224">Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1233-224">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="a1233-225">[Plug-in do Maven para Aplicativos Web do Azure]</span><span class="sxs-lookup"><span data-stu-id="a1233-225">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="a1233-226">Faça logon no Azure na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a1233-226">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="a1233-227">Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a1233-227">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="a1233-228">Referência de configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="a1233-228">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="a1233-229">[Plug-in do Docker para o Maven]</span><span class="sxs-lookup"><span data-stu-id="a1233-229">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Portal do Azure]: https://portal.azure.com/
[Plug-in do Maven para Aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Plug-in do Docker para o Maven]: https://github.com/spotify/docker-maven-plugin
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
