---
title: Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Azure
description: Saiba como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 8e5ad501f5c00ee1265878a643793f6e9754bb68
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-to-azure"></a><span data-ttu-id="3ae40-103">Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Azure</span><span class="sxs-lookup"><span data-stu-id="3ae40-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure</span></span>

<span data-ttu-id="3ae40-104">Este artigo demonstra como usar o plug-in do Maven para Aplicativos Web do Azure a fim de implantar um exemplo de aplicativo Spring Boot para os Serviços de Aplicativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae40-104">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application to Azure App Services.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="3ae40-105">O [Plug-in do Maven para Aplicativos Web do Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Apache Maven](http://maven.apache.org/) fornece uma integração perfeita do Serviço de Aplicativo do Azure em projetos Maven, e simplifica o processo para os desenvolvedores implantarem aplicativos Web no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae40-105">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="3ae40-106">O plug-in do Maven para Aplicativos Web do Azure está disponível no momento como uma versão prévia.</span><span class="sxs-lookup"><span data-stu-id="3ae40-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="3ae40-107">Por enquanto, há suporte somente para a publicação FTP, embora existam planos para recursos adicionais futuros.</span><span class="sxs-lookup"><span data-stu-id="3ae40-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="3ae40-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3ae40-108">Prerequisites</span></span>

<span data-ttu-id="3ae40-109">Para concluir as etapas deste tutorial, você precisa ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="3ae40-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="3ae40-110">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="3ae40-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="3ae40-111">A[CLI (interface de linha de comando) do Azure].</span><span class="sxs-lookup"><span data-stu-id="3ae40-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="3ae40-112">Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.</span><span class="sxs-lookup"><span data-stu-id="3ae40-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="3ae40-113">A ferramenta de compilação [Maven] do Apache (Versão 3).</span><span class="sxs-lookup"><span data-stu-id="3ae40-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="3ae40-114">Um cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="3ae40-114">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="3ae40-115">Clonar o aplicativo Web Spring Boot de exemplo</span><span class="sxs-lookup"><span data-stu-id="3ae40-115">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="3ae40-116">Nesta seção, você clonará um aplicativo Spring Boot concluído e o testará localmente.</span><span class="sxs-lookup"><span data-stu-id="3ae40-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="3ae40-117">Abra um prompt de comando ou janela de terminal e crie um diretório local para conter o aplicativo Spring Boot, e altere para esse diretório; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-117">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="3ae40-118">-- ou --</span><span class="sxs-lookup"><span data-stu-id="3ae40-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="3ae40-119">Clone o projeto de exemplo [Introdução ao Spring Boot] para o diretório que você criou. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-119">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="3ae40-120">Altere o diretório para o projeto concluído. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-120">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="3ae40-121">Crie o arquivo JAR usando o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-121">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="3ae40-122">Após a criação do aplicativo Web, inicie-o usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-122">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="3ae40-123">Teste o aplicativo Web navegando até ele localmente usando um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="3ae40-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="3ae40-124">Por exemplo, use o comando a seguir, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="3ae40-124">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="3ae40-125">Você verá a seguinte mensagem exibida: **Saudações do Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="3ae40-125">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="3ae40-126">Criar uma entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="3ae40-126">Create an Azure service principal</span></span>

<span data-ttu-id="3ae40-127">Nesta seção, você criará uma entidade de serviço do Azure que será usada pelo plug-in do Maven durante a implantação de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae40-127">In this section, you create an Azure service principal that the Maven plugin uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="3ae40-128">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="3ae40-128">Open a command prompt.</span></span>

1. <span data-ttu-id="3ae40-129">Entre em sua conta do Azure usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="3ae40-129">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="3ae40-130">Siga as instruções na tela para concluir o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="3ae40-130">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="3ae40-131">Crie uma entidade de serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="3ae40-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="3ae40-132">Onde `uuuuuuuu` é o nome de usuário e `pppppppp` é a senha para a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3ae40-132">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="3ae40-133">O Azure responde com um JSON parecido com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ae40-133">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="3ae40-134">Você usará os valores dessa resposta em JSON ao configurar o plug-in do Maven para implantar seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae40-134">You will use the values from this JSON response when you configure the Maven plugin to deploy your web app to Azure.</span></span> <span data-ttu-id="3ae40-135">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` e `tttttttt` são valores de espaço reservado, usados neste exemplo para facilitar o mapeamento desses valores para seus respectivos elementos durante a configuração de seu arquivo `settings.xml` do Maven na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="3ae40-135">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="3ae40-136">Configurar o Maven para usar a entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="3ae40-136">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="3ae40-137">Nesta seção, você usará os valores de sua entidade de serviço do Azure para configurar a autenticação usada pelo Maven durante a implantação de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae40-137">In this section, you use the values from your Azure service principal to configure the authentication that Maven uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="3ae40-138">Abra seu arquivo `settings.xml` do Maven em um editor de texto; esse arquivo pode estar em um caminho como os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ae40-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="3ae40-139">Adicione as configurações de sua entidade de serviço do Azure da seção anterior deste tutorial à coleção `<servers>` no arquivo *settings.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-139">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="3ae40-140">Em que:</span><span class="sxs-lookup"><span data-stu-id="3ae40-140">Where:</span></span>
   <span data-ttu-id="3ae40-141">Elemento</span><span class="sxs-lookup"><span data-stu-id="3ae40-141">Element</span></span> | <span data-ttu-id="3ae40-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="3ae40-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="3ae40-143">Especifica um nome exclusivo usado pelo Maven para analisar suas configurações de segurança durante a implantação de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae40-143">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="3ae40-144">Contém o valor `appId` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3ae40-144">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="3ae40-145">Contém o valor `tenant` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3ae40-145">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="3ae40-146">Contém o valor `password` de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="3ae40-146">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="3ae40-147">Define o ambiente de nuvem do Azure de destino, que é `AZURE` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="3ae40-147">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="3ae40-148">(Uma lista completa dos ambientes está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure])</span><span class="sxs-lookup"><span data-stu-id="3ae40-148">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="3ae40-149">Salve e feche o arquivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="3ae40-149">Save and close the *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a><span data-ttu-id="3ae40-150">OPCIONAL: Personalizar seu pom.xml antes de implantar seu aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="3ae40-150">OPTIONAL: Customize your pom.xml before deploying your web app to Azure</span></span>

<span data-ttu-id="3ae40-151">Abra o arquivo `pom.xml` de seu aplicativo Spring Boot em um editor de texto e localize o elemento `<plugin>` para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="3ae40-151">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="3ae40-152">Esse elemento deverá se parecer com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-152">This element should resemble the following example:</span></span>

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="3ae40-153">Você pode modificar diversos valores do plug-in do Maven, e há uma descrição detalhada de cada um desses elementos disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="3ae40-153">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="3ae40-154">Dito isso, vale a pena destacar diversos valores neste artigo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="3ae40-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="3ae40-155">Element</span></span> | <span data-ttu-id="3ae40-156">Descrição</span><span class="sxs-lookup"><span data-stu-id="3ae40-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="3ae40-157">Especifica a versão do [Plug-in do Maven para Aplicativos Web do Azure].</span><span class="sxs-lookup"><span data-stu-id="3ae40-157">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="3ae40-158">Você deve verificar a versão listada no [Repositório Central do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para garantir que esteja usando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="3ae40-158">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="3ae40-159">Especifica as informações de autenticação do Azure, que, neste exemplo, contêm um elemento `<serverId>` contendo `azure-auth`; o Maven usa esse valor para procurar os valores de entidade de serviço do Azure em seu arquivo *settings.xml* do Maven, que você definiu em uma seção anterior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="3ae40-159">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="3ae40-160">Especifica o grupo de recursos de destino, que é `maven-plugin` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="3ae40-160">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="3ae40-161">Esse grupo de recursos é criado durante a implantação, caso ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="3ae40-161">The resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="3ae40-162">Especifica o nome de destino de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3ae40-162">Specifies the target name for your web app.</span></span> <span data-ttu-id="3ae40-163">Neste exemplo, o nome de destino é `maven-web-app-${maven.build.timestamp}`, no qual o sufixo `${maven.build.timestamp}` é acrescentado neste exemplo para evitar conflitos.</span><span class="sxs-lookup"><span data-stu-id="3ae40-163">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="3ae40-164">(O carimbo de data/hora é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="3ae40-164">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="3ae40-165">Especifica a região de destino, que neste exemplo é `westus`.</span><span class="sxs-lookup"><span data-stu-id="3ae40-165">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="3ae40-166">(Uma lista completa está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure]).</span><span class="sxs-lookup"><span data-stu-id="3ae40-166">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="3ae40-167">Especifica a versão de tempo de execução Java para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3ae40-167">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="3ae40-168">(Uma lista completa está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure]).</span><span class="sxs-lookup"><span data-stu-id="3ae40-168">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="3ae40-169">Especifica o tipo de implantação para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3ae40-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="3ae40-170">Por enquanto, somente o `ftp` tem suporte, embora o suporte para outros tipos de implantação esteja em desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="3ae40-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="3ae40-171">Especifica os recursos e os destinos que o Maven usa durante a implantação de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae40-171">Specifies resources and target destinations which Maven uses when deploying your web app to Azure.</span></span> <span data-ttu-id="3ae40-172">Neste exemplo, dois elementos `<resource>` especificam que o Maven implantará o arquivo JAR para seu aplicativo Web e o arquivo *Web.config* do projeto Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="3ae40-172">In this example, two `<resource>` elements specify that Maven will deploy the JAR file for your web app and the *web.config* file from the Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="3ae40-173">Criar e implantar seu aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="3ae40-173">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="3ae40-174">Depois de definir todas as configurações nas seções anteriores deste artigo, você estará pronto para implantar seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae40-174">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="3ae40-175">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3ae40-175">To do so, use the following steps:</span></span>

1. <span data-ttu-id="3ae40-176">Do prompt de comando ou janela de terminal que você estava usando antes, recompile o arquivo JAR usando o Maven, se você tiver feito alterações no arquivo *pom.xml*; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-176">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="3ae40-177">Implante seu aplicativo Web no Azure usando o Maven; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae40-177">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="3ae40-178">O Maven implantará seu aplicativo Web no Azure; se o aplicativo Web ainda não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="3ae40-178">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="3ae40-179">Após a implantação de sua Web, você poderá gerenciá-la usando o [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="3ae40-179">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="3ae40-180">Seu aplicativo Web será listado nos **Serviços de Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="3ae40-180">Your web app will be listed in **App Services**:</span></span>

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* <span data-ttu-id="3ae40-182">E a URL para seu aplicativo Web será listada na **Visão geral** de seu aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="3ae40-182">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3ae40-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ae40-184">Next steps</span></span>

<span data-ttu-id="3ae40-185">Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ae40-185">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="3ae40-186">[Plug-in do Maven para Aplicativos Web do Azure]</span><span class="sxs-lookup"><span data-stu-id="3ae40-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="3ae40-187">Fazer logon no Azure desde a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3ae40-187">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="3ae40-188">Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure</span><span class="sxs-lookup"><span data-stu-id="3ae40-188">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="3ae40-189">Criar uma entidade de serviço do Azure com a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3ae40-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="3ae40-190">Referência de configurações do Maven</span><span class="sxs-lookup"><span data-stu-id="3ae40-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[portal do Azure]: https://portal.azure.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in do Maven para Aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
