---
title: Implantar um aplicativo de arquivo JAR do Spring Boot na nuvem com o Maven e o Azure
description: Saiba como implantar um aplicativo Spring Boot na nuvem usando o plug-in Maven do Aplicativo Web do Azure para Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.author: robmcm;kevinzha;brborges
ms.date: 10/04/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 36afcc764c1cb984779518ddec004ecbfa1b7c57
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48876390"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="bf7a3-103">Implantar um aplicativo Web do arquivo JAR do Spring Boot no Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="bf7a3-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="bf7a3-104">Este artigo demonstra como usar o [plug-in do Maven para os Aplicativos Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para implantar um aplicativo Spring Boot empacotado como um Java SE JAR no [Serviço de Aplicativo do Azure no Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="bf7a3-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/).</span></span> <span data-ttu-id="bf7a3-105">Escolha a implantação Java SE em vez dos [arquivos Tomcat e WAR](/azure/app-service/containers/quickstart-java) quando quiser consolidar as dependências, execução e configuração do aplicativo em um único artefato de implantação.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's depedencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="bf7a3-106">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf7a3-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bf7a3-107">Prerequisites</span></span>

<span data-ttu-id="bf7a3-108">Para concluir as etapas deste tutorial, você precisa ter o seguinte instalado e configurado:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="bf7a3-109">A [CLI do Azure](/cli/azure/), localmente ou por meio do [Azure Cloud Shell](https://shell.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf7a3-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="bf7a3-110">O [Java Development Kit (JDK)](https://www.azul.com/downloads/azure-only/zulu/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-110">[Java Development Kit (JDK)](https://www.azul.com/downloads/azure-only/zulu/), version 1.7 or later.</span></span>
* <span data-ttu-id="bf7a3-111">O [Maven](https://maven.apache.org/) do Apache, versão 3.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-111">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="bf7a3-112">Um cliente [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="bf7a3-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="bf7a3-113">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7a3-113">Clone the sample app</span></span>

<span data-ttu-id="bf7a3-114">Nesta seção, você clonará um aplicativo Spring Boot concluído e o testará localmente.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-114">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="bf7a3-115">Abra um prompt de comando ou janela de terminal e crie um diretório local para conter o aplicativo Spring Boot, e altere para esse diretório; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-115">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="bf7a3-116">-- ou --</span><span class="sxs-lookup"><span data-stu-id="bf7a3-116">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="bf7a3-117">Clone o projeto de exemplo [Introdução ao Spring Boot] para o diretório que você criou. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-117">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="bf7a3-118">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-118">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="bf7a3-119">Crie o arquivo JAR usando o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-119">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="bf7a3-120">Após a criação do aplicativo Web, inicie-o usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-120">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="bf7a3-121">Teste o aplicativo Web navegando até ele localmente usando um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-121">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="bf7a3-122">Por exemplo, use o comando a seguir, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-122">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="bf7a3-123">Você verá a seguinte mensagem exibida: **Saudações do Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="bf7a3-123">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="bf7a3-124">Configurar o plug-in do Maven para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="bf7a3-124">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="bf7a3-125">Nesta seção, será configurado o projeto Spring Boot `pom.xml` para que o Maven possa implantar o aplicativo no Serviço de Aplicativo do Azure no Linux.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-125">In this section, you will configure the the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="bf7a3-126">Abra `pom.xml` em um editor de código.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-126">Open `pom.xml` in a code editor.</span></span>

1. <span data-ttu-id="bf7a3-127">Na seção `<build>` do pom.xml, adicione a seguinte entrada `<plugin>` dentro da marca `<plugins>`.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-127">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
  <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
  </plugin>
  ```

1. <span data-ttu-id="bf7a3-128">Atualize os seguintes espaços reservados na configuração do plug-in:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-128">Update the following placeholders in the plugin configuration:</span></span>

| <span data-ttu-id="bf7a3-129">Placeholder</span><span class="sxs-lookup"><span data-stu-id="bf7a3-129">Placeholder</span></span> | <span data-ttu-id="bf7a3-130">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="bf7a3-130">Description</span></span> |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | <span data-ttu-id="bf7a3-131">Nome do novo grupo de recursos no qual criar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-131">Name for the new resource group in which to create your web app.</span></span> <span data-ttu-id="bf7a3-132">Ao colocar todos os recursos para um aplicativo em um grupo, você pode gerenciá-los juntos.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-132">By putting all the resources for an app in a group, you can manage them together.</span></span> <span data-ttu-id="bf7a3-133">Por exemplo, excluir o grupo de recursos excluiria todos os recursos associados ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-133">For example, deleting the resource group would delete all resources associated with the app.</span></span> <span data-ttu-id="bf7a3-134">Atualize esse valor com um novo nome de grupo de recursos exclusivo, por exemplo, *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-134">Update this value with a unique new resource group name, for example, *TestResources*.</span></span> <span data-ttu-id="bf7a3-135">Você usará esse nome de grupo de recursos para limpar todos os recursos do Azure em uma seção posterior.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-135">You will use this resource group name to clean up all Azure resources in a later section.</span></span> |
| `WEBAPP_NAME` | <span data-ttu-id="bf7a3-136">O nome do aplicativo será parte do nome do host do aplicativo Web quando implantado no Azure (NOME_APLICATIVO_WEB.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="bf7a3-136">The app name will be part the host name for the web app when deployed to Azure (WEBAPP_NAME.azurewebsites.net).</span></span> <span data-ttu-id="bf7a3-137">Atualize esse valor com um nome exclusivo para o novo aplicativo Web do Azure que irá hospedar seu aplicativo Java, por exemplo, *contoso*.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-137">Update this value with a unique name for the new Azure web app, which will host your Java app, for example *contoso*.</span></span> |
| `REGION` | <span data-ttu-id="bf7a3-138">Uma região do Azure onde o aplicativo Web está hospedado, por exemplo, `westus2`.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-138">An Azure region where the web app is hosted, for example `westus2`.</span></span> <span data-ttu-id="bf7a3-139">Você pode obter uma lista de regiões do Cloud Shell ou da CLI usando o comando `az account list-locations`.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-139">You can get a list of regions from the Cloud Shell or CLI using the `az account list-locations` command.</span></span> |

<span data-ttu-id="bf7a3-140">Há uma lista completa das opções de configuração na [referência de plug-in do Maven no GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="bf7a3-140">A full list of configuration options can be found in the [Maven plugin reference on GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span></span>

## <a name="install-and-log-in-to-azure-cli"></a><span data-ttu-id="bf7a3-141">Instalar e fazer logon na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bf7a3-141">Install and log in to Azure CLI</span></span>

<span data-ttu-id="bf7a3-142">A maneira mais simples e fácil de obter o plug-in do Maven implantando seu aplicativo Spring Boot é usando a [CLI do Azure](https://docs.microsoft.com/cli/azure/).</span><span class="sxs-lookup"><span data-stu-id="bf7a3-142">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span>

1. <span data-ttu-id="bf7a3-143">Entre em sua conta do Azure usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-143">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
   <span data-ttu-id="bf7a3-144">Siga as instruções na tela para concluir o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-144">Follow the instructions to complete the sign-in process.</span></span>

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="bf7a3-145">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="bf7a3-145">Deploy the app to Azure</span></span>

<span data-ttu-id="bf7a3-146">Depois de definir todas as configurações nas seções anteriores deste artigo, você estará pronto para implantar seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-146">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="bf7a3-147">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-147">To do so, use the following steps:</span></span>

1. <span data-ttu-id="bf7a3-148">Do prompt de comando ou janela de terminal que você estava usando antes, recompile o arquivo JAR usando o Maven, se você tiver feito alterações no arquivo *pom.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-148">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="bf7a3-149">Implante seu aplicativo Web no Azure usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-149">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="bf7a3-150">O Maven implantará seu aplicativo Web no Azure. Se o aplicativo Web ou o plano dele ainda não existirem, eles serão criados.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-150">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="bf7a3-151">Depois que a Web tiver sido implantada, você conseguirá gerenciá-la por meio do [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="bf7a3-151">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="bf7a3-152">Seu aplicativo Web será listado nos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-152">Your web app will be listed in **App Services**:</span></span>

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* <span data-ttu-id="bf7a3-154">E a URL para seu aplicativo Web será listada na **Visão geral** de seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-154">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Como determinar a URL de seu aplicativo Web][AP02]

<span data-ttu-id="bf7a3-156">Verifique se a implantação foi bem-sucedida usando o mesmo comando cURL de antes e com a URL do aplicativo Web do Portal em vez de `localhost`.</span><span class="sxs-lookup"><span data-stu-id="bf7a3-156">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="bf7a3-157">Você verá a seguinte mensagem exibida: **Saudações do Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="bf7a3-157">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bf7a3-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf7a3-158">Next steps</span></span>

<span data-ttu-id="bf7a3-159">Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf7a3-159">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="bf7a3-160">[Plug-in do Maven para aplicativos Web do Azure]</span><span class="sxs-lookup"><span data-stu-id="bf7a3-160">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="bf7a3-161">Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure</span><span class="sxs-lookup"><span data-stu-id="bf7a3-161">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="bf7a3-162">Criar uma entidade de serviço do Azure com a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bf7a3-162">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="bf7a3-163">Referência de configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="bf7a3-163">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portal do Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in do Maven para aplicativos Web do Azure]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
