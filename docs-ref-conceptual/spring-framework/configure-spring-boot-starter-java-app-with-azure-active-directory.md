---
title: Como usar o iniciador do Spring Boot para o Azure Active Directory
description: Saiba como configurar um aplicativo inicializador do Spring Boot com o iniciador do Azure Active Directory.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm
ms.openlocfilehash: a999e33674ea01e776db10186e8af83ce157ef20
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="b82dd-103">Como usar o iniciador do Spring Boot para o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b82dd-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="b82dd-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b82dd-104">Overview</span></span>

<span data-ttu-id="b82dd-105">Este artigo demonstra como criar um aplicativo com o **[Spring Initializr]** do iniciador do Spring Boot do Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b82dd-105">This article demonstrates creating an app with the **[Spring Initializr]** which the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b82dd-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b82dd-106">Prerequisites</span></span>

<span data-ttu-id="b82dd-107">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="b82dd-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="b82dd-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="b82dd-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b82dd-109">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b82dd-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="b82dd-110">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b82dd-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="b82dd-111">Criar um aplicativo personalizado usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="b82dd-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="b82dd-112">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="b82dd-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="b82dd-113">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="b82dd-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar os nomes do grupo e do artefato][security-01]

1. <span data-ttu-id="b82dd-115">Role para baixo até a seção **Núcleo**, marque a caixa **Segurança** e, na seção **Web**, marque a caixa **Web**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Selecione os iniciadores de segurança e da Web][security-02]

1. <span data-ttu-id="b82dd-117">Role para baixo até a seção **Azure** e marque a caixa do **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Selecionar iniciador do Azure Active Directory][security-03]

1. <span data-ttu-id="b82dd-119">Role até a parte inferior da página e clique no botão **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Gerar projeto do Spring Boot][security-04]

1. <span data-ttu-id="b82dd-121">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="b82dd-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="b82dd-122">Criar e configurar uma nova instância do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b82dd-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="b82dd-123">Criar a instância do Active Directory</span><span class="sxs-lookup"><span data-stu-id="b82dd-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="b82dd-124">Faça logon em <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="b82dd-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="b82dd-125">Clique em **+Novo**, depois em **Segurança + Identidade** e em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Criar uma nova instância do Azure Active Directory][directory-01]

1. <span data-ttu-id="b82dd-127">Insira o **Nome da organização** e seu **Nome de domínio inicial** e depois clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Especificar nomes do Azure Active Directory][directory-02]

1. <span data-ttu-id="b82dd-129">Selecione o novo Azure Active Directory no menu suspenso na barra de ferramentas superior do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b82dd-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Escolher seu Azure Active Directory][directory-03]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="b82dd-131">Adicionar um registro de aplicativo para seu aplicativo Spring Boot</span><span class="sxs-lookup"><span data-stu-id="b82dd-131">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="b82dd-132">Selecione **Azure Active Directory** no menu do portal, clique em **Visão geral** e depois em **Registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-132">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Adicionar um novo registro de aplicativo][directory-04]

1. <span data-ttu-id="b82dd-134">Clique em **Novo registro de aplicativo**, especifique o **Nome** do aplicativo, use http://localhost:8080 como a **URL de entrada** e depois clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-134">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Criar novo registro de aplicativo][directory-05]

1. <span data-ttu-id="b82dd-136">Clique em seu registro de aplicativo depois de ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="b82dd-136">Click your application registration after it has been created.</span></span>

   ![Selecione o registro de aplicativo][directory-06]

1. <span data-ttu-id="b82dd-138">Quando estiver na página do registro de aplicativo, copie a **ID do aplicativo** para mais tarde, depois clique em **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-138">When the page for your app registration, copy your **Application ID** for later, then click **Keys**.</span></span>

   ![Criar chaves do registro de aplicativo][directory-07]

1. <span data-ttu-id="b82dd-140">Adicione uma **Descrição**, especifique a **Duração** de uma nova chave e clique em **Salvar**; o valor da chave será preenchido automaticamente ao clicar no ícone **Salvar**, e você precisa anotar o valor da chave para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="b82dd-140">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="b82dd-141">(Você não conseguirá recuperar esse valor depois.)</span><span class="sxs-lookup"><span data-stu-id="b82dd-141">(You will not be able to retrieve this value later.)</span></span>

   ![Especificar parâmetros da chave de registro do aplicativo][directory-08]

1. <span data-ttu-id="b82dd-143">Na página principal do registro do aplicativo, clique em **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-143">From the main page for your app registration, click **Required permissions**.</span></span>

   ![Permissões necessárias para o registro do aplicativo][directory-09]

1. <span data-ttu-id="b82dd-145">Clique em **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-145">Click **Windows Azure Active Directory**.</span></span>

   ![Selecione Microsoft Azure Active Directory][directory-10]

1. <span data-ttu-id="b82dd-147">Marque as caixas **Acessar o diretório como o usuário conectado** e **Entrar e ler o perfil de usuário**, depois clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b82dd-147">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Habilitar permissões de acesso][directory-11]

1. <span data-ttu-id="b82dd-149">Na página **Permissões necessárias**, clique em **Conceder Permissões** e em **Sim**, quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="b82dd-149">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Conceder permissões de acesso][directory-12]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="b82dd-151">Configurar e compilar seu aplicativo Spring Boot</span><span class="sxs-lookup"><span data-stu-id="b82dd-151">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="b82dd-152">Extraia os arquivos do arquivo de projeto baixado em um diretório.</span><span class="sxs-lookup"><span data-stu-id="b82dd-152">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="b82dd-153">Navegue até a pasta pai no seu projeto e abra o arquivo *pom.xml* em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b82dd-153">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

1. <span data-ttu-id="b82dd-154">Adicione a dependência da segurança do Spring OAuth2. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b82dd-154">Add the dependency for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security.oauth</groupId>
      <artifactId>spring-security-oauth2</artifactId>
   </dependency>
   ```

1. <span data-ttu-id="b82dd-155">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="b82dd-155">Save and close the  the *pom.xml* file.</span></span>

1. <span data-ttu-id="b82dd-156">Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* no editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b82dd-156">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="b82dd-157">Adicione a chave para sua conta de armazenamento usando os valores anteriores. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b82dd-157">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory Application ID:
   azure.activedirectory.clientId=11111111-1111-1111-1111-1111111111111111

   # Specifies your secret key:
   azure.activedirectory.clientSecret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.activeDirectoryGroups=Users
   ```
   <span data-ttu-id="b82dd-158">Em que:</span><span class="sxs-lookup"><span data-stu-id="b82dd-158">Where:</span></span>
   <span data-ttu-id="b82dd-159">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b82dd-159">Parameter</span></span> | <span data-ttu-id="b82dd-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="b82dd-160">Description</span></span>
   ---|---|---
   `azure.activedirectory.clientId` | <span data-ttu-id="b82dd-161">Contém a **ID do aplicativo** de momento anterior.</span><span class="sxs-lookup"><span data-stu-id="b82dd-161">Contains your **Application ID** from earlier.</span></span>
   `azure.activedirectory.clientSecret` | <span data-ttu-id="b82dd-162">Contém o valor da chave do registro de aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b82dd-162">Contains the key value from your app registration which you completed earlier.</span></span>
   `azure.activedirectory.activeDirectoryGroups` | <span data-ttu-id="b82dd-163">Contém uma lista de grupos do Active Directory para usar para autenticação.</span><span class="sxs-lookup"><span data-stu-id="b82dd-163">Contains a list of Active Directory groups to use for authentication.</span></span>


1. <span data-ttu-id="b82dd-164">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="b82dd-164">Save and close the  the *application.properties* file.</span></span>

1. <span data-ttu-id="b82dd-165">Crie uma pasta chamada *controller* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="b82dd-165">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="b82dd-166">Crie um novo arquivo Java chamado *HelloController.java* na pasta *controller* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b82dd-166">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="b82dd-167">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="b82dd-167">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;
   
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.web.authentication.preauth.PreAuthenticatedAuthenticationToken;
   
   @RestController
   public class HelloController {
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String hello() {
         return "Hello World!";
      }
   }
   ```

1. <span data-ttu-id="b82dd-168">Crie uma pasta chamada *security* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="b82dd-168">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="b82dd-169">Crie um novo arquivo Java chamado *WebSecurityConfig.java* na pasta *security* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b82dd-169">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="b82dd-170">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="b82dd-170">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import com.microsoft.azure.spring.autoconfigure.aad.AADAuthenticationFilter;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.autoconfigure.security.oauth2.client.EnableOAuth2Sso;
   import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
   import org.springframework.security.config.annotation.web.builders.HttpSecurity;
   import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
   import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
   import org.springframework.security.web.csrf.CookieCsrfTokenRepository;
   
   @EnableOAuth2Sso
   @EnableGlobalMethodSecurity(securedEnabled = true, prePostEnabled = true)
   
   public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
      @Autowired
      private AADAuthenticationFilter aadAuthFilter;
      @Override
      protected void configure(HttpSecurity http) throws Exception {
         http.authorizeRequests().anyRequest().permitAll();
         http.addFilterBefore(aadAuthFilter, UsernamePasswordAuthenticationFilter.class);
      }
   }
   ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="b82dd-171">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b82dd-171">Build and test your app</span></span>

1. <span data-ttu-id="b82dd-172">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* do aplicativo está localizado.</span><span class="sxs-lookup"><span data-stu-id="b82dd-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="b82dd-173">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b82dd-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   ```

   ![][build-application]

1. <span data-ttu-id="b82dd-174">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b82dd-174">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```



1. <span data-ttu-id="b82dd-175">Depois que seu aplicativo for criado e iniciado pelo Maven, abra <http://localhost:8080> em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="b82dd-175">After your application is built and started by Maven, open <http://localhost:8080> in a web browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b82dd-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b82dd-176">Next steps</span></span>

<span data-ttu-id="b82dd-177">Para obter mais informações sobre o Azure Active Directory, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b82dd-177">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="b82dd-178">[Documentação do Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="b82dd-178">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="b82dd-179">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b82dd-179">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="b82dd-180">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b82dd-180">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="b82dd-181">Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="b82dd-181">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="b82dd-182">Para saber mais sobre como usar o Azure com o Java, consulte [Azure para desenvolvedores Java] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b82dd-182">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="b82dd-183">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="b82dd-183">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="b82dd-184">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="b82dd-184">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="b82dd-185">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="b82dd-185">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="b82dd-186">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="b82dd-186">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentação do Azure Active Directory]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[security-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-01.png
[security-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-02.png
[security-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-03.png
[security-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-04.png

[directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-01.png
[directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-02.png
[directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-03.png
[directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-04.png
[directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-05.png
[directory-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-06.png
[directory-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-07.png
[directory-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-08.png
[directory-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-09.png
[directory-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-10.png
[directory-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-11.png
[directory-12]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-12.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
