---
title: Como usar o iniciador do Spring Boot para o Azure Active Directory B2C
description: Descubra como configurar um aplicativo inicializador do Spring Boot com o iniciador do Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: java
author: panli
manager: kevinzha
editor: panli
ms.assetid: ''
ms.author: panli
ms.date: 02/28/2019
ms.devlang: java
ms.service: active-directory-b2c
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 21aa6c812a519d686356851a57f00688d9a24fa4
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625715"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a><span data-ttu-id="46a3f-103">Tutorial: Proteger um aplicativo Web do Java usando o iniciador do Spring Boot para o Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="46a3f-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory B2C.</span></span>

## <a name="overview"></a><span data-ttu-id="46a3f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="46a3f-104">Overview</span></span>

<span data-ttu-id="46a3f-105">Este artigo demonstra como criar um aplicativo Java com o [Spring Initializr](https://start.spring.io/) que usa o Iniciador do Spring Boot para o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46a3f-105">This article demonstrates creating a Java app with the [Spring Initializr](https://start.spring.io/) that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46a3f-106">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="46a3f-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46a3f-107">Criar um aplicativo do Java usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="46a3f-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="46a3f-108">Configurar o Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="46a3f-108">Configure Azure Active Directory B2C</span></span>
> * <span data-ttu-id="46a3f-109">Proteger o aplicativo com classes e anotações do Spring Boot</span><span class="sxs-lookup"><span data-stu-id="46a3f-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="46a3f-110">Compilar e testar seu aplicativo do Java</span><span class="sxs-lookup"><span data-stu-id="46a3f-110">Build and test your Java application</span></span>

<span data-ttu-id="46a3f-111">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="46a3f-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46a3f-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="46a3f-112">Prerequisites</span></span>

<span data-ttu-id="46a3f-113">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="46a3f-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="46a3f-114">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="46a3f-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="46a3f-115">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="46a3f-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="46a3f-116">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="46a3f-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="46a3f-117">Criar um aplicativo usando o Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="46a3f-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="46a3f-118">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="46a3f-118">Browse to <https://start.spring.io/>.</span></span>

2. <span data-ttu-id="46a3f-119">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, selecione o módulo **Web** e **Segurança** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="46a3f-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select the **Web** and **Security** module of the Spring Initializr.</span></span>

   ![Especificar os nomes do grupo e do artefato](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. <span data-ttu-id="46a3f-121">Clique em `Generate Project` e baixe o projeto para um caminho no computador local quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="46a3f-121">Click `Generate Project`, download the project to a path on your local computer when prompted.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="46a3f-122">Criar uma instância do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46a3f-122">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="46a3f-123">Criar a instância do Active Directory</span><span class="sxs-lookup"><span data-stu-id="46a3f-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="46a3f-124">Faça logon em <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="46a3f-124">Log into <https://portal.azure.com>.</span></span>

2. <span data-ttu-id="46a3f-125">Clique em **+Criar um recurso**, depois em **Identidade** e **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="46a3f-125">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory B2C**.</span></span>

   ![Criar uma nova instância do Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. <span data-ttu-id="46a3f-127">Insira o **Nome da organização** e seu **Nome de domínio inicial**, registre o **nome de domínio** como seu `${your-tenant-name}` e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="46a3f-127">Enter your **Organization name** and your **Initial domain name**, record the **domain name** as your `${your-tenant-name}` and click **Create**.</span></span>

   ![Obter o nome do locatário B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. <span data-ttu-id="46a3f-129">Selecione o nome de sua conta à direita superior da barra de ferramentas do portal do Azure, depois clique em **Trocar diretório**.</span><span class="sxs-lookup"><span data-stu-id="46a3f-129">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Escolher seu Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. <span data-ttu-id="46a3f-131">Selecione o novo Azure Active Directory no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="46a3f-131">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Escolher seu Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. <span data-ttu-id="46a3f-133">Pesquise `b2c` e clique no serviço do `Azure AD B2C`.</span><span class="sxs-lookup"><span data-stu-id="46a3f-133">Search `b2c` and click `Azure AD B2C` service.</span></span>

   ![Localize a instância do Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="46a3f-135">Adicionar um registro de aplicativo para seu aplicativo do Spring Boot</span><span class="sxs-lookup"><span data-stu-id="46a3f-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="46a3f-136">Selecione **Azure AD B2C** no menu do portal, clique em **Aplicativos** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="46a3f-136">Select **Azure AD B2C** from the portal menu, click **Applications**, and then click **Add**.</span></span>

   ![Adicionar um novo registro de aplicativo](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. <span data-ttu-id="46a3f-138">Especifique o **Nome** do seu aplicativo, adicione `http://localhost:8080/home` para a **URL de Resposta**, registre a **ID do Aplicativo** como seu `${your-client-id}` e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="46a3f-138">Specify your application **Name**, add `http://localhost:8080/home` for the **Reply URL**, record the **Application ID** as your `${your-client-id}` and then click **Save**.</span></span>

   ![Adicionar URL de Resposta do Aplicativo](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. <span data-ttu-id="46a3f-140">Selecione **Chaves** do seu aplicativo, clique em **Gerar chave** para gerar `${your-client-secret}` e, em seguida, **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="46a3f-140">Select **Keys** from your application, click **Generate key** to generate `${your-client-secret}` and then **Save**.</span></span>

4. <span data-ttu-id="46a3f-141">Selecione **Fluxos dos usuários** à esquerda e então **Clique em** **Novo fluxo de usuário**.</span><span class="sxs-lookup"><span data-stu-id="46a3f-141">Select **User flows** on your left, and then **Click** \*\*New user flow \*\*.</span></span>

   ![Criar fluxo de usuário](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. <span data-ttu-id="46a3f-143">Escolher **Inscrever-se ou entrar**, **Edição de perfil** e **Redefinição de senha** para criar fluxos dos usuários, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="46a3f-143">Choose **Sign up or in**, **Profile editing** and **Password reset** to create user flows respectively.</span></span> <span data-ttu-id="46a3f-144">Especifique o **Nome** e os **Atributos e declarações do usuário** de seu fluxo de usuário e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="46a3f-144">Specify your user flow **Name** and **User attributes and claims**, click **Create**.</span></span>

   ![Configurar fluxo de usuário](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="46a3f-146">Configurar e compilar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="46a3f-146">Configure and compile your app</span></span>

1. <span data-ttu-id="46a3f-147">Extraia os arquivos do arquivo de projeto criado e baixado antes neste tutorial para um diretório.</span><span class="sxs-lookup"><span data-stu-id="46a3f-147">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

2. <span data-ttu-id="46a3f-148">Navegue até a pasta-mãe no projeto e abra o `pom.xml`arquivo de projeto Maven em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="46a3f-148">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

3. <span data-ttu-id="46a3f-149">Adicione as dependências de segurança do Spring OAuth2 a `pom.xml`:</span><span class="sxs-lookup"><span data-stu-id="46a3f-149">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-active-directory-b2c-spring-boot-starter</artifactId>
       <version>2.1.6.M2</version>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-thymeleaf</artifactId>
   </dependency>
   <dependency>
       <groupId>org.thymeleaf.extras</groupId>
       <artifactId>thymeleaf-extras-springsecurity5</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="46a3f-150">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="46a3f-150">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="46a3f-151">Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.yml* em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="46a3f-151">Navigate to the *src/main/resources* folder in your project and open the *application.yml* file in a text editor.</span></span>

6. <span data-ttu-id="46a3f-152">Especifique as configurações de registro do aplicativo usando os valores criados anteriormente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="46a3f-152">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

   ```yaml
   azure:
     activedirectory:
       b2c:
         tenant: ${your-tenant-name}
         client-id: ${your-client-id}
         client-secret: ${your-client-secret}
         reply-url: ${your-reply-url-from-aad} # should be absolute url.
         logout-success-url: ${you-logout-success-url}
         user-flows:
           sign-up-or-sign-in: ${your-sign-up-or-in-user-flow}
           profile-edit: ${your-profile-edit-user-flow}     # optional
           password-reset: ${your-password-reset-user-flow} # optional
   ```
   <span data-ttu-id="46a3f-153">Em que:</span><span class="sxs-lookup"><span data-stu-id="46a3f-153">Where:</span></span>

   | <span data-ttu-id="46a3f-154">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="46a3f-154">Parameter</span></span> | <span data-ttu-id="46a3f-155">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="46a3f-155">Description</span></span> |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | <span data-ttu-id="46a3f-156">Contém `${your-tenant-name` do AD B2C de antes.</span><span class="sxs-lookup"><span data-stu-id="46a3f-156">Contains your AD B2C's `${your-tenant-name` from earlier.</span></span> |
   | `azure.activedirectory.b2c.client-id` | <span data-ttu-id="46a3f-157">Contém o `${your-client-id}` de seu aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46a3f-157">Contains the `${your-client-id}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.client-secret` | <span data-ttu-id="46a3f-158">Contém o `${your-client-secret}` de seu aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46a3f-158">Contains the `${your-client-secret}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.reply-url` | <span data-ttu-id="46a3f-159">Contém uma das **URL de resposta** do seu aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46a3f-159">Contains one of the **Reply URL** from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.logout-success-url` | <span data-ttu-id="46a3f-160">Especifique a URL ao fazer logoff do aplicativo com êxito.</span><span class="sxs-lookup"><span data-stu-id="46a3f-160">Specify the URL when your application logout successfully.</span></span> |
   | `azure.activedirectory.b2c.user-flows` | <span data-ttu-id="46a3f-161">Contém o nome dos fluxos dos usuários que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46a3f-161">Contains the name of the user flows that you completed earlier.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="46a3f-162">Para obter uma lista completa de valores disponíveis em seu arquivo *application.yml*, confira o [Exemplo de Spring Boot do Azure Active Directory B2C][Exemplo de Spring Boot do AAD B2C] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="46a3f-162">For a full list of values that are available in your *application.yml* file, see the [Azure Active Directory B2C Spring Boot Sample][AAD B2C Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="46a3f-163">Salve e feche o arquivo *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="46a3f-163">Save and close the *application.yml* file.</span></span>

8. <span data-ttu-id="46a3f-164">Crie uma pasta chamada *controlador* na pasta de origem do Java para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46a3f-164">Create a folder named *controller* in the Java source folder for your application.</span></span>

9. <span data-ttu-id="46a3f-165">Crie um arquivo Java chamado *HelloController.java* na pasta *controller* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="46a3f-165">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="46a3f-166">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="46a3f-166">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.controller;
    
    import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
    import org.springframework.security.oauth2.core.user.OAuth2User;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class WebController {
    
        private void initializeModel(Model model, OAuth2AuthenticationToken token) {
            if (token != null) {
                final OAuth2User user = token.getPrincipal();
    
                model.addAttribute("grant_type", user.getAuthorities());
                model.addAllAttributes(user.getAttributes());
            }
        }
    
        @GetMapping(value = "/")
        public String index(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    
        @GetMapping(value = "/greeting")
        public String greeting(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "greeting";
        }
    
        @GetMapping(value = "/home")
        public String home(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    }
    ```

11. <span data-ttu-id="46a3f-167">Crie uma pasta chamada *segurança* na pasta de origem do Java para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46a3f-167">Create a folder named *security* in the Java source folder for your application.</span></span>

12. <span data-ttu-id="46a3f-168">Crie um novo arquivo Java chamado *WebSecurityConfig.java* na pasta *security* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="46a3f-168">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="46a3f-169">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="46a3f-169">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.security;
    
    import com.microsoft.azure.spring.autoconfigure.b2c.AADB2COidcLoginConfigurer;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    
    @EnableWebSecurity
    public class WebSecurityConfiguration extends WebSecurityConfigurerAdapter {
    
        private final AADB2COidcLoginConfigurer configurer;
    
        public WebSecurityConfiguration(AADB2COidcLoginConfigurer configurer) {
            this.configurer = configurer;
        }
    
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                    .authorizeRequests()
                    .anyRequest()
                    .authenticated()
                    .and()
                    .apply(configurer)
            ;
        }
    }
    ```
14. <span data-ttu-id="46a3f-170">Copie o `greeting.html` e o `home.html` do [Exemplo de Spring Boot do Azure AD B2C](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates) e substitua `${your-profile-edit-user-flow}` e `${your-password-reset-user-flow}` pelo nome do fluxo de usuário, respectivamente, concluídos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46a3f-170">Copy the `greeting.html` and `home.html` from [Azure AD B2C Spring Boot Sample](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), and replace the `${your-profile-edit-user-flow}` and `${your-password-reset-user-flow}` with your user flow name respectively that completed earlier.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="46a3f-171">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="46a3f-171">Build and test your app</span></span>

1. <span data-ttu-id="46a3f-172">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* do aplicativo está localizado.</span><span class="sxs-lookup"><span data-stu-id="46a3f-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

2. <span data-ttu-id="46a3f-173">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="46a3f-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. <span data-ttu-id="46a3f-174">Após a criação e inicialização de seu aplicativo pelo Maven, abra <http://localhost:8080/> em um navegador da Web; você deverá ser redirecionado para a página de logon.</span><span class="sxs-lookup"><span data-stu-id="46a3f-174">After your application is built and started by Maven, open <http://localhost:8080/> in a web browser; you should be redirected to login page.</span></span>

   ![Página de logon](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. <span data-ttu-id="46a3f-176">Clique no link com o nome do fluxo de usuário `${your-sign-up-or-in}`; você deve ser redirecionado do Azure AD B2C para iniciar o processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="46a3f-176">Click linke with name of `${your-sign-up-or-in}` user flow, you should be rediected Azure AD B2C to start the authentication process.</span></span>

   ![Logon do Azure AD B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. <span data-ttu-id="46a3f-178">Depois de entrar com êxito, você deverá ver o `home page` de exemplo do navegador.</span><span class="sxs-lookup"><span data-stu-id="46a3f-178">After you have logged in successfully, you should see the sample `home page` from the browser,</span></span>

   ![Logon bem-sucedido](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a><span data-ttu-id="46a3f-180">Resumo</span><span class="sxs-lookup"><span data-stu-id="46a3f-180">Summary</span></span>

<span data-ttu-id="46a3f-181">Neste tutorial, você criou um novo aplicativo Web do Java usando o iniciador do Azure Active Directory B2C, configurou um novo locatário do Azure AD B2C e registrou um novo aplicativo, em seguida, configurou o aplicativo para usar as classes e as anotações do Spring para proteger o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="46a3f-181">In this tutorial, you created a new Java web application using the Azure Active Directory B2C starter, configured a new Azure AD B2C tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46a3f-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46a3f-182">Next steps</span></span>

<span data-ttu-id="46a3f-183">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="46a3f-183">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46a3f-184">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="46a3f-184">Spring on Azure</span></span>](/java/azure/spring-framework)
