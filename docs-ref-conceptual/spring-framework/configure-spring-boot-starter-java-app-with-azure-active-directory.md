---
title: Como usar o iniciador do Spring Boot para o Azure Active Directory
description: Descubra como configurar um aplicativo inicializador do Spring Boot com o iniciador do Azure Active Directory.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 06/20/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: adcbc78cc129daf589bf070741308e4024432e5d
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090829"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="2b344-103">Como usar o iniciador do Spring Boot para o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b344-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="2b344-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2b344-104">Overview</span></span>

<span data-ttu-id="2b344-105">Este artigo demonstra como criar um aplicativo com o **[Spring Initializr]**, que é o iniciador do Spring Boot do Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b344-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b344-106">pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2b344-106">Prerequisites</span></span>

<span data-ttu-id="2b344-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="2b344-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="2b344-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="2b344-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="2b344-109">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2b344-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="2b344-110">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2b344-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="2b344-111">Criar um aplicativo personalizado usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="2b344-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="2b344-112">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="2b344-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="2b344-113">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="2b344-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar os nomes do grupo e do artefato][security-01]

1. <span data-ttu-id="2b344-115">Role para baixo até a seção **Núcleo**, marque a caixa **Segurança** e, na seção **Web**, marque a caixa **Web**.</span><span class="sxs-lookup"><span data-stu-id="2b344-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Selecione os iniciadores de segurança e da Web][security-02]

1. <span data-ttu-id="2b344-117">Role para baixo até a seção **Azure** e marque a caixa do **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b344-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Selecionar iniciador do Azure Active Directory][security-03]

1. <span data-ttu-id="2b344-119">Role até a parte inferior da página e clique no botão **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="2b344-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Gerar projeto do Spring Boot][security-04]

1. <span data-ttu-id="2b344-121">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="2b344-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="2b344-122">Criar e configurar uma nova instância do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b344-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="2b344-123">Criar a instância do Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b344-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="2b344-124">Faça logon em <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="2b344-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="2b344-125">Clique em **+Novo**, depois em **Segurança + Identidade** e em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b344-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Criar uma nova instância do Azure Active Directory][directory-01]

1. <span data-ttu-id="2b344-127">Preencha os campos **Nome da organização** e **Nome de domínio inicial** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2b344-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Especificar nomes do Azure Active Directory][directory-02]

1. <span data-ttu-id="2b344-129">Selecione o novo Azure Active Directory no menu suspenso na barra de ferramentas superior do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b344-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Escolher seu Azure Active Directory][directory-03]

1. <span data-ttu-id="2b344-131">Selecione **Azure Active Directory** no menu do portal, clique em **Propriedades** e copie a **ID de Diretório**. Você a usará mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2b344-131">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID** - you will use that later in this article.</span></span>

   ![Copiar sua ID do Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="2b344-133">Adicionar um registro de aplicativo para seu aplicativo do Spring Boot</span><span class="sxs-lookup"><span data-stu-id="2b344-133">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="2b344-134">Selecione **Azure Active Directory** no menu do portal, clique em **Visão geral**, depois, em **Registros de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="2b344-134">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Adicionar um novo registro de aplicativo][directory-04]

1. <span data-ttu-id="2b344-136">Clique em **Novo registro de aplicativo**, especifique o **Nome** do aplicativo, use http://localhost:8080 como a **URL de entrada** e depois clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2b344-136">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Criar novo registro de aplicativo][directory-05]

1. <span data-ttu-id="2b344-138">Clique em seu registro de aplicativo depois de ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="2b344-138">Click your application registration after it has been created.</span></span>

   ![Selecione o registro de aplicativo][directory-06]

1. <span data-ttu-id="2b344-140">Quando estiver na página do registro do aplicativo, anote a **ID do aplicativo** para usar mais tarde e clique em **Configurações** e depois em **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="2b344-140">When the page for your app registration, copy your **Application ID** for later use, then click **Settings**, and then click **Keys**.</span></span>

   ![Criar chaves do registro de aplicativo][directory-07]

1. <span data-ttu-id="2b344-142">Adicione uma **Descrição**, especifique a **Duração** de uma nova chave e clique em **Salvar**. O valor da chave será preenchido automaticamente quando você clicar no ícone **Salvar**. Anote esse valor, ele será necessário posteriormente.</span><span class="sxs-lookup"><span data-stu-id="2b344-142">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="2b344-143">(Você não conseguirá recuperar esse valor depois.)</span><span class="sxs-lookup"><span data-stu-id="2b344-143">(You will not be able to retrieve this value later.)</span></span>

   ![Especificar parâmetros da chave de registro do aplicativo][directory-08]

1. <span data-ttu-id="2b344-145">Na página principal do registro do aplicativo, clique em **Configurações** e depois em **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="2b344-145">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Permissões necessárias para o registro do aplicativo][directory-09]

1. <span data-ttu-id="2b344-147">Clique em **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b344-147">Click **Windows Azure Active Directory**.</span></span>

   ![Selecione Microsoft Azure Active Directory][directory-10]

1. <span data-ttu-id="2b344-149">Marque as caixas **Acessar o diretório como o usuário conectado** e **Entrar e ler o perfil de usuário**, depois clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2b344-149">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Habilitar permissões de acesso][directory-11]

1. <span data-ttu-id="2b344-151">Na página **Permissões necessárias**, clique em **Conceder Permissões** e em **Sim**, quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="2b344-151">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Conceder permissões de acesso][directory-12]

1. <span data-ttu-id="2b344-153">Na página principal do registro do aplicativo, clique em **Configurações** e depois em **URLs de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="2b344-153">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

   ![Editar URLs de Resposta][directory-14]

1. <span data-ttu-id="2b344-155">Insira "http://localhost:8080/login/oauth2/code/azure" como uma nova URL de resposta e depois clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2b344-155">Enter "http://localhost:8080/login/oauth2/code/azure" as a new reply URL, and then click **Save**.</span></span>

   ![Adicionar nova URL de Resposta][directory-15]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="2b344-157">Configurar e compilar seu aplicativo Spring Boot</span><span class="sxs-lookup"><span data-stu-id="2b344-157">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="2b344-158">Extraia em um diretório os arquivos do projeto baixado.</span><span class="sxs-lookup"><span data-stu-id="2b344-158">Extract the files from the downloaded project archive into a directory.</span></span>

2. <span data-ttu-id="2b344-159">Navegue até a pasta pai no seu projeto e abra o arquivo *pom.xml* em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="2b344-159">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

3. <span data-ttu-id="2b344-160">Adicione as dependências da segurança do Spring OAuth2. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2b344-160">Add the dependencies for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-client</artifactId>
   </dependency>
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-jose</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="2b344-161">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="2b344-161">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="2b344-162">Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="2b344-162">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

6. <span data-ttu-id="2b344-163">Adicione a chave para sua conta de armazenamento usando os valores anteriores. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2b344-163">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.active-directory-groups=Users
   ```
   <span data-ttu-id="2b344-164">Em que:</span><span class="sxs-lookup"><span data-stu-id="2b344-164">Where:</span></span>

   | <span data-ttu-id="2b344-165">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="2b344-165">Parameter</span></span> | <span data-ttu-id="2b344-166">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="2b344-166">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="2b344-167">Contém a **ID de Diretório** anterior do seu Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b344-167">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="2b344-168">Contém a **ID de Aplicativo** do registro de aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2b344-168">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="2b344-169">Contém o **Valor** da chave do registro de aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2b344-169">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="2b344-170">Contém uma lista dos grupos do Active Directory a serem usados para autenticação.</span><span class="sxs-lookup"><span data-stu-id="2b344-170">Contains a list of Active Directory groups to use for authentication.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="2b344-171">Para obter uma lista completa de valores que estão disponíveis em seu arquivo *application.properties*, consulte o [Exemplo de Spring Boot do Azure Active Directory][AAD Spring Boot Sample] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="2b344-171">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="2b344-172">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="2b344-172">Save and close the *application.properties* file.</span></span>

8. <span data-ttu-id="2b344-173">Crie uma pasta chamada *controller* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="2b344-173">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

9. <span data-ttu-id="2b344-174">Crie um arquivo Java chamado *HelloController.java* na pasta *controller* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="2b344-174">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="2b344-175">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="2b344-175">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.oauth2.client.OAuth2AuthorizedClient;
   import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
   import org.springframework.ui.Model;

   @RestController
   public class HelloController {
      @Autowired
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String helloWorld() {
         return "Hello World!";
      }
   }
   ```
   > [!NOTE]
   > 
   > <span data-ttu-id="2b344-176">O nome do grupo que você especificar para o método `@PreAuthorize("hasRole('')")` deve conter um dos grupos que você especificou no campo `azure.activedirectory.active-directory-groups` de seu arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="2b344-176">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="2b344-177">Você pode especificar configurações de autorização diferentes para mapeamentos de solicitação diferentes; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2b344-177">You can specify different authorization settings for different request mappings; for example:</span></span>
   >
   > ``` java
   > public class HelloController {
   >    @Autowired
   >    @PreAuthorize("hasRole('Users')")
   >    @RequestMapping("/")
   >    public String helloWorld() {
   >       return "Hello Users!";
   >    }
   >    @PreAuthorize("hasRole('Group1')")
   >    @RequestMapping("/Group1")
   >    public String groupOne() {
   >       return "Hello Group 1 Users!";
   >    }
   >    @PreAuthorize("hasRole('Group2')")
   >    @RequestMapping("/Group2")
   >    public String groupTwo() {
   >       return "Hello Group 2 Users!";
   >    }
   > }
   > ```
   >    

11. <span data-ttu-id="2b344-178">Crie uma pasta chamada *security* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="2b344-178">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

12. <span data-ttu-id="2b344-179">Crie um novo arquivo Java chamado *WebSecurityConfig.java* na pasta *security* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="2b344-179">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="2b344-180">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="2b344-180">Enter the following code, then save and close the file:</span></span>

    ```java
    package com.wingtiptoys.security;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    import org.springframework.security.oauth2.client.oidc.userinfo.OidcUserRequest;
    import org.springframework.security.oauth2.client.userinfo.OAuth2UserService;
    import org.springframework.security.oauth2.core.oidc.user.OidcUser;

    @EnableWebSecurity
    @EnableGlobalMethodSecurity(prePostEnabled = true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
        @Autowired
        private OAuth2UserService<OidcUserRequest, OidcUser> oidcUserService;

        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                .authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .oauth2Login()
                .userInfoEndpoint()
                .oidcUserService(oidcUserService);
        }
    }
    ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="2b344-181">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="2b344-181">Build and test your app</span></span>

1. <span data-ttu-id="2b344-182">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* do aplicativo está localizado.</span><span class="sxs-lookup"><span data-stu-id="2b344-182">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="2b344-183">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2b344-183">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Crie seu aplicativo][build-application]

1. <span data-ttu-id="2b344-185">Após a criação e inicialização de seu aplicativo pelo Maven, abra <http://localhost:8080> em um navegador da Web; você deverá receber uma solicitação por um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="2b344-185">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Fazer logon em seu aplicativo][application-login]

1. <span data-ttu-id="2b344-187">Após o logon bem-sucedido, você deverá ver o texto "Olá, Mundo" de exemplo no controlador.</span><span class="sxs-lookup"><span data-stu-id="2b344-187">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Logon bem-sucedido][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="2b344-189">Contas de usuário sem autorização receberão uma mensagem **HTTP 403 Não autorizado**.</span><span class="sxs-lookup"><span data-stu-id="2b344-189">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="2b344-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b344-190">Next steps</span></span>

<span data-ttu-id="2b344-191">Para obter mais informações sobre como usar o Azure Active Directory, veja estes artigos:</span><span class="sxs-lookup"><span data-stu-id="2b344-191">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="2b344-192">[Documentação do Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="2b344-192">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="2b344-193">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="2b344-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="2b344-194">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2b344-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="2b344-195">Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="2b344-195">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="2b344-196">Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="2b344-196">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="2b344-197">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="2b344-197">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="2b344-198">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="2b344-198">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="2b344-199">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="2b344-199">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="2b344-200">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="2b344-200">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="2b344-201">Para obter um exemplo mais detalhado, consulte o [Exemplo do Spring Boot do Azure Active Directory][AAD Spring Boot Sample] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="2b344-201">For a more-detailed sample, see the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>

<!-- URL List -->

[Documentação do Azure Active Directory]: /azure/active-directory/
[Azure Active Directory Documentation]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Benefícios do assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

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
[directory-13]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-13.png
[directory-14]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-14.png
[directory-15]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-15.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
