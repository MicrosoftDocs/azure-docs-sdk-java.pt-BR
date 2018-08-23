---
title: Implantar um aplicativo Spring Boot para a nuvem com o Maven e o Azure
description: Saiba como implantar um aplicativo Spring Boot para a nuvem usando o plug-in Maven para Aplicativos Web do Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: d58cafe3456150069ec8572c101c62d1b2c29c5d
ms.sourcegitcommit: e1a5d9687e006e8bf12d11747d45cf130a2c82af
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2018
ms.locfileid: "42703361"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a><span data-ttu-id="7df77-103">Implantar um aplicativo Spring Boot na nuvem usando o Maven Plugin para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7df77-103">Deploy a Spring Boot app to the cloud using the Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="7df77-104">Este artigo demonstra como usar o plug-in do Maven para Aplicativos Web do Serviço de Aplicativo do Azure a fim de implantar um exemplo de aplicativo Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="7df77-104">This article demonstrates using the Maven Plugin for Azure App Service Web Apps to deploy a sample Spring Boot application.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="7df77-105">O [plug-in do Maven para Aplicativos Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para [Apache Maven](http://maven.apache.org/) fornece uma integração perfeita do Serviço de Aplicativo do Azure em projetos Maven e simplifica o processo para os desenvolvedores implantarem aplicativos Web no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="7df77-105">The [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="7df77-106">Antes de usar o plug-in do Maven, verifique na Central do Maven a versão mais recente do plugin disponível: [![Central do Maven](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span><span class="sxs-lookup"><span data-stu-id="7df77-106">Before using the Maven plugin, check on Maven Central for the latest available version of the plugin: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7df77-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7df77-107">Prerequisites</span></span>

<span data-ttu-id="7df77-108">Para concluir as etapas neste tutorial, você precisará ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="7df77-108">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="7df77-109">Uma assinatura do Azure; se ainda não tiver uma, inscreva-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="7df77-109">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="7df77-110">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="7df77-110">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="7df77-111">Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.</span><span class="sxs-lookup"><span data-stu-id="7df77-111">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="7df77-112">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="7df77-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="7df77-113">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="7df77-113">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="7df77-114">Clonar o aplicativo Web Spring Boot de exemplo</span><span class="sxs-lookup"><span data-stu-id="7df77-114">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="7df77-115">Nesta seção, você clonará um aplicativo Spring Boot concluído e o testará localmente.</span><span class="sxs-lookup"><span data-stu-id="7df77-115">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="7df77-116">Abra um prompt de comando ou janela de terminal e crie um diretório local para conter o aplicativo Spring Boot, e altere para esse diretório; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7df77-116">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="7df77-117">-- ou --</span><span class="sxs-lookup"><span data-stu-id="7df77-117">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="7df77-118">Clone o projeto de exemplo [Introdução ao Spring Boot] para o diretório que você criou. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7df77-118">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="7df77-119">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7df77-119">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="7df77-120">Crie o arquivo JAR usando o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7df77-120">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="7df77-121">Após a criação do aplicativo Web, inicie-o usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7df77-121">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="7df77-122">Teste o aplicativo Web navegando até ele localmente usando um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="7df77-122">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="7df77-123">Por exemplo, use o comando a seguir, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="7df77-123">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="7df77-124">Você verá a seguinte mensagem exibida: **Saudações do Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="7df77-124">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a><span data-ttu-id="7df77-125">Ajustar o projeto para implantação com base em WAR no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7df77-125">Adjust project for WAR-based deployment on Azure App Service</span></span>

<span data-ttu-id="7df77-126">Nesta seção, ajustaremos rapidamente o projeto Spring Boot para implantá-lo como um arquivo WAR no Serviço de Aplicativo do Azure, que fornece o Tomcat como tempo de execução padrão.</span><span class="sxs-lookup"><span data-stu-id="7df77-126">In this section we will quickly adjust the Spring Boot project to be deployed as a WAR file on Azure App Service, which provides Tomcat as the runtime by default.</span></span> <span data-ttu-id="7df77-127">Para que isso funcione, dois arquivos precisam ser modificados:</span><span class="sxs-lookup"><span data-stu-id="7df77-127">For this to work, there are two files to be modified:</span></span>

- <span data-ttu-id="7df77-128">O arquivo `pom.xml` do Maven</span><span class="sxs-lookup"><span data-stu-id="7df77-128">The Maven `pom.xml` file</span></span>
- <span data-ttu-id="7df77-129">A classe `Application` de Java</span><span class="sxs-lookup"><span data-stu-id="7df77-129">The `Application` Java class</span></span>

<span data-ttu-id="7df77-130">Vamos começar com as configurações do Maven:</span><span class="sxs-lookup"><span data-stu-id="7df77-130">Let's start with the Maven settings:</span></span>

1. <span data-ttu-id="7df77-131">Abra `pom.xml`</span><span class="sxs-lookup"><span data-stu-id="7df77-131">Open `pom.xml`</span></span>

1. <span data-ttu-id="7df77-132">Adicione `<packaging>war</packaging>` logo após a definição `<artifactId>` na parte superior:</span><span class="sxs-lookup"><span data-stu-id="7df77-132">Add `<packaging>war</packaging>` right after the `<artifactId>` definition at the top:</span></span>
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. <span data-ttu-id="7df77-133">Adicione a seguinte dependência:</span><span class="sxs-lookup"><span data-stu-id="7df77-133">Add the following dependency:</span></span>
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

<span data-ttu-id="7df77-134">Agora, abra a classe `Application`, após seu IDE já ter coletado as novas dependências, e continue com as seguintes modificações:</span><span class="sxs-lookup"><span data-stu-id="7df77-134">Now open the class `Application`, hopefully after your IDE has already picked up the new dependencies, and proceed with the following modifications:</span></span>

1. <span data-ttu-id="7df77-135">Torne a classe Application uma subclasse de `SpringBootServletInitializer`:</span><span class="sxs-lookup"><span data-stu-id="7df77-135">Make class Application a subclass of `SpringBootServletInitializer`:</span></span>
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. <span data-ttu-id="7df77-136">Adicione o seguinte método à classe Application:</span><span class="sxs-lookup"><span data-stu-id="7df77-136">Add the following method to the Application class:</span></span>
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```

<span data-ttu-id="7df77-137">Agora, seu aplicativo está pronto para ser implantado no Tomcat e em qualquer outro tempo de execução do Servlet (por exemplo, Jetty).</span><span class="sxs-lookup"><span data-stu-id="7df77-137">Your application is now ready to be deployed to Tomcat and any other Servlet runtime (e.g. Jetty).</span></span>

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a><span data-ttu-id="7df77-138">Adicionar o plug-in do Maven para Aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7df77-138">Add the Maven Plugin for Azure App Service Web Apps</span></span>

<span data-ttu-id="7df77-139">Nesta seção, adicionaremos um plug-in do Maven que automatizará toda a implantação desse aplicativo em Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="7df77-139">In this section, we will add a Maven plugin that will automate the entire deployment of this application into Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="7df77-140">Abra `pom.xml` mais uma vez.</span><span class="sxs-lookup"><span data-stu-id="7df77-140">Open `pom.xml` once again.</span></span>

1. <span data-ttu-id="7df77-141">Dentro de `<properties>`, defina um formato de carimbo de data/hora personalizada com a propriedade `maven.build.timestamp.format`.</span><span class="sxs-lookup"><span data-stu-id="7df77-141">Inside `<properties>`, set a custom timestamp format with the property `maven.build.timestamp.format`.</span></span> <span data-ttu-id="7df77-142">Como o Serviço de Aplicativo do Azure cria uma URL pública para o seu aplicativo, essa configuração será usada para gerar o nome da sua implantação e evitar conflitos com as implantações ativas de outros usuários.</span><span class="sxs-lookup"><span data-stu-id="7df77-142">Because Azure App Service creates a public URL for your application, this setting will be used to generate the name of your deployment, and avoid conflict with other users' live deployments.</span></span>
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. <span data-ttu-id="7df77-143">No elemento `<plugins>`, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7df77-143">In the `<plugins>` element, add the following:</span></span>
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

<span data-ttu-id="7df77-144">Com essas configurações, seu projeto do Maven está pronto para a implantação ativa no Aplicativo Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="7df77-144">With these settings, your Maven project is now ready for live deployment to Azure App Service Web App.</span></span>

## <a name="install-and-log-in-to-azure-cli"></a><span data-ttu-id="7df77-145">Instalar e fazer logon na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7df77-145">Install and log in to Azure CLI</span></span>

<span data-ttu-id="7df77-146">A maneira mais simples e fácil de obter o plug-in do Maven implantando seu aplicativo Spring Boot é usando a [CLI do Azure](https://docs.microsoft.com/cli/azure/).</span><span class="sxs-lookup"><span data-stu-id="7df77-146">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span> <span data-ttu-id="7df77-147">Verifique se ela está instalada.</span><span class="sxs-lookup"><span data-stu-id="7df77-147">Make sure you have it installed.</span></span>

1. <span data-ttu-id="7df77-148">Entre em sua conta do Azure usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="7df77-148">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
   <span data-ttu-id="7df77-149">Siga as instruções na tela para concluir o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="7df77-149">Follow the instructions to complete the sign-in process.</span></span>

## <a name="optionally-customize-pomxml-before-deploying"></a><span data-ttu-id="7df77-150">Opcionalmente, personalize o pom.xml antes de implantar</span><span class="sxs-lookup"><span data-stu-id="7df77-150">Optionally, customize pom.xml before deploying</span></span>

<span data-ttu-id="7df77-151">Abra o arquivo `pom.xml` de seu aplicativo Spring Boot em um editor de texto e localize o elemento `<plugin>` para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="7df77-151">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="7df77-152">Esse elemento deverá se parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="7df77-152">This element should resemble the following example:</span></span>

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

<span data-ttu-id="7df77-153">Você pode modificar diversos valores do plug-in do Maven, e há uma descrição detalhada de cada um desses elementos disponível na documentação [Plug-in do Maven para aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="7df77-153">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="7df77-154">Dito isso, vale a pena destacar diversos valores neste artigo:</span><span class="sxs-lookup"><span data-stu-id="7df77-154">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="7df77-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="7df77-155">Element</span></span> | <span data-ttu-id="7df77-156">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="7df77-156">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="7df77-157">Especifica a versão do [Plug-in do Maven para aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="7df77-157">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="7df77-158">Verifique a versão listada no [Repositório Central do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para garantir que esteja usando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="7df77-158">Verify the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="7df77-159">Especifica o grupo de recursos de destino, que é `maven-plugin` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="7df77-159">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="7df77-160">Esse grupo de recursos é criado durante a implantação, caso ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="7df77-160">The resource group is created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="7df77-161">Especifica o nome de destino de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="7df77-161">Specifies the target name for your web app.</span></span> <span data-ttu-id="7df77-162">Neste exemplo, o nome de destino é `maven-web-app-${maven.build.timestamp}`, no qual o sufixo `${maven.build.timestamp}` é acrescentado neste exemplo para evitar conflitos.</span><span class="sxs-lookup"><span data-stu-id="7df77-162">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="7df77-163">(O carimbo de data/hora é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="7df77-163">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="7df77-164">Especifica a região de destino, que neste exemplo é `westus`.</span><span class="sxs-lookup"><span data-stu-id="7df77-164">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="7df77-165">(Uma lista completa está disponível na documentação [Plug-in do Maven para aplicativos Web do Azure]).</span><span class="sxs-lookup"><span data-stu-id="7df77-165">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<javaVersion>` | <span data-ttu-id="7df77-166">Especifica a versão de tempo de execução Java para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="7df77-166">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="7df77-167">(Uma lista completa está disponível na documentação [Plug-in do Maven para aplicativos Web do Azure]).</span><span class="sxs-lookup"><span data-stu-id="7df77-167">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<deploymentType>` | <span data-ttu-id="7df77-168">Especifica o tipo de implantação para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="7df77-168">Specifies deployment type for your web app.</span></span> <span data-ttu-id="7df77-169">O padrão é `war`.</span><span class="sxs-lookup"><span data-stu-id="7df77-169">Default is `war`.</span></span> |

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="7df77-170">Criar e implantar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="7df77-170">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="7df77-171">Depois de definir todas as configurações nas seções anteriores deste artigo, você estará pronto para implantar seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="7df77-171">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="7df77-172">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7df77-172">To do so, use the following steps:</span></span>

1. <span data-ttu-id="7df77-173">Do prompt de comando ou janela de terminal que você estava usando antes, recompile o arquivo JAR usando o Maven, se você tiver feito alterações no arquivo *pom.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7df77-173">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="7df77-174">Implante seu aplicativo Web no Azure usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7df77-174">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="7df77-175">O Maven implantará seu aplicativo Web no Azure; se o aplicativo Web ainda não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="7df77-175">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="7df77-176">Após a implantação de sua Web, você poderá gerenciá-la usando o [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="7df77-176">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="7df77-177">Seu aplicativo Web será listado nos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="7df77-177">Your web app will be listed in **App Services**:</span></span>

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* <span data-ttu-id="7df77-179">E a URL para seu aplicativo Web será listada na **Visão geral** de seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="7df77-179">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7df77-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7df77-181">Next steps</span></span>

<span data-ttu-id="7df77-182">Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7df77-182">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="7df77-183">[Plug-in do Maven para aplicativos Web do Azure]</span><span class="sxs-lookup"><span data-stu-id="7df77-183">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="7df77-184">Fazer logon no Azure desde a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7df77-184">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="7df77-185">Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure</span><span class="sxs-lookup"><span data-stu-id="7df77-185">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="7df77-186">Criar uma entidade de serviço do Azure com a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7df77-186">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="7df77-187">Referência de configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="7df77-187">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portal do Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
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
