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
ms.date: 07/02/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: da44a40b7b52e75bb0a946b46ddfc033bfef54e9
ms.sourcegitcommit: 473c3aec55f3e9b131dc87c62e2eac218ce9564e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51571713"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a>Tutorial: Proteger um aplicativo Web do Java usando o iniciador do Spring Boot para o Azure Active Directory

## <a name="overview"></a>Visão geral

Este artigo demonstra como criar um aplicativo com o **[Spring Initializr]**, que é o iniciador do Spring Boot do Azure Active Directory (Azure AD).

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar um aplicativo do Java usando o Spring Initializr
> * Configurar o Azure Active Directory
> * Proteger o aplicativo com classes e anotações do Spring Boot
> * Compilar e testar seu aplicativo do Java

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:

* Um [Java Development Kit (JDK)](https://aka.ms/azure-jdks) versão 1.7 ou posterior.
* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.

## <a name="create-an-application-using-the-spring-initializr"></a>Criar um aplicativo usando o Spring Initializr

1. Navegue até <https://start.spring.io/>.

1. Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.

   ![Especificar os nomes do grupo e do artefato][security-01]

1. Role para baixo até a seção **Núcleo**, marque a caixa **Segurança** e, na seção **Web**, marque a caixa **Web**.

   ![Selecione os iniciadores de segurança e da Web][security-02]

1. Role para baixo até a seção **Azure** e marque a caixa do **Azure Active Directory**.

   ![Selecionar iniciador do Azure Active Directory][security-03]

1. Role até a parte inferior da página e clique no botão **Gerar Projeto**.

   ![Gerar projeto do Spring Boot][security-04]

1. Quando solicitado, baixe o projeto para um caminho no computador local.

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a>Criar e configurar uma nova instância do Azure Active Directory

### <a name="create-the-active-directory-instance"></a>Criar a instância do Active Directory

1. Faça logon em <https://portal.azure.com>.

1. Clique em **+Novo**, depois em **Segurança + Identidade** e em **Azure Active Directory**.

   ![Criar uma nova instância do Azure Active Directory][directory-01]

1. Insira o **Nome da organização** e seu **Nome de domínio inicial**. Copie a URL completa de seu diretório. Você usará isso para adicionar as contas de usuário mais tarde neste tutorial. (Por exemplo, `wingtiptoysdirectory.onmicrosoft.com`.) Ao terminar, clique em **Criar**.

   ![Especificar nomes do Azure Active Directory][directory-02]

1. Selecione o novo Azure Active Directory no menu suspenso na barra de ferramentas superior do portal do Azure.

   ![Escolher seu Azure Active Directory][directory-03]

1. Selecione **Azure Active Directory** no menu do portal, clique em **Propriedades** e copie a **ID do Diretório**. Você usará esse valor para configurar o arquivo *application.properties* posteriormente neste tutorial.

   ![Copiar sua ID do Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Adicionar um registro de aplicativo para seu aplicativo do Spring Boot

1. Selecione **Azure Active Directory** no menu do portal, clique em **Visão geral**, depois, em **Registros de aplicativo**.

   ![Adicionar um novo registro de aplicativo][directory-04]

2. Clique em **Novo registro de aplicativo**, especifique o **Nome** do aplicativo, use http://localhost:8080 como a **URL de entrada** e depois clique em **Criar**.

   ![Criar novo registro de aplicativo][directory-05]

3. Clique em seu registro de aplicativo depois de ele ter sido criado.

   ![Selecione o registro de aplicativo][directory-06]

4. Quando a página de registro do aplicativo aparecer, copie seu **ID do aplicativo**. Você usará esse valor para configurar o arquivo *application.properties* posteriormente no tutorial. Clique em **Configurações** e **Chaves**.

   ![Criar chaves do registro de aplicativo][directory-07]

5. Adicione uma **Descrição**, especifique a **Duração** de uma nova chave e clique em **Salvar**. O valor da chave será preenchido automaticamente quando clicar no ícone **Salvar** e você precisará copiar o valor da chave para configurar o arquivo *application.properties* posteriormente neste tutorial. (Você não conseguirá recuperar esse valor depois.)

   ![Especificar parâmetros da chave de registro do aplicativo][directory-08]

6. Na página principal do registro do aplicativo, clique em **Configurações** e depois em **Permissões necessárias**.

   ![Permissões necessárias para o registro do aplicativo][directory-09]

7. Clique em **Microsoft Azure Active Directory**.

   ![Selecione Microsoft Azure Active Directory][directory-10]

8. Marque as caixas **Acessar o diretório como o usuário conectado** e **Entrar e ler o perfil de usuário**, depois clique em **Salvar**.

   ![Habilitar permissões de acesso][directory-11]

9. Na página **Permissões necessárias**, clique em **Conceder Permissões** e em **Sim**, quando solicitado.

   ![Conceder permissões de acesso][directory-12]

10. Na página principal do registro do aplicativo, clique em **Configurações** e depois em **URLs de Resposta**.

    ![Editar URLs de Resposta][directory-14]

11. Insira "<http://localhost:8080/login/oauth2/code/azure>" como uma nova URL de resposta e depois clique em **Salvar**.

    ![Adicionar nova URL de Resposta][directory-15]

12. Na página principal de registro do aplicativo, clique em **Manifesto**, em seguida defina o valor do `oauth2AllowImplicitFlow` parâmetro para `true` e clique em **Salvar**.

    ![Configurar manifesto do aplicativo][directory-16]

    > [!NOTE]
    > 
    > Para obter mais informações sobre o `oauth2AllowImplicitFlow` parâmetro e outras configurações do aplicativo, consulte [Manifesto do aplicativo do Azure Active Directory][AAD app manifest]. 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a>Adicionar uma conta de usuário ao diretório e adicionar essa conta a um grupo

1. Na página **Visão geral** do Active Directory, clique em **Usuários**.

   ![Abrir painel de Usuários][directory-17]

1. Quando o painel **Usuários** for exibido, clique em **Novo usuário**.

   ![Adicionar uma nova conta de usuário][directory-18]

1. Quando o painel **Usuário** for exibido, insira o **Nome** e o **Nome de usuário**.

   ![Inserir informações da conta de usuário][directory-19]

   > [!NOTE]
   > 
   > Você precisa especificar a URL do diretório mostrada anteriormente neste tutorial quando inserir o nome de usuário. Por exemplo:
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. Clique em **Grupos**, selecione os grupos que você usará para a autorização em seu aplicativo, em seguida, clique em **Selecionar**. (Para este tutorial, adicione a conta ao grupo _Usuários_.)

   ![Selecionar os grupos do usuário][directory-20]

1. Clique em **Mostrar senha**e copie a senha. Você usará isso quando entrar no aplicativo mais tarde neste tutorial.

   ![Mostrar a senha][directory-21]

1. Clique em **Criar** para adicionar a nova conta de usuário ao seu diretório.

   ![Criar a nova conta de usuário][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a>Configurar e compilar seu aplicativo Spring Boot

1. Extraia os arquivos do arquivo de projeto criado e baixado antes neste tutorial para um diretório.

1. Navegue até a pasta-mãe no projeto e abra o `pom.xml`arquivo de projeto Maven em um editor de texto.

1. Adicione as dependências de segurança do Spring OAuth2 a `pom.xml`:

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

1. Salve e feche o arquivo *pom.xml*.

1. Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* em um editor de texto.

1. Especifique as configurações de registro do aplicativo usando os valores criados anteriormente. Por exemplo:

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authorization:
   azure.activedirectory.active-directory-groups=Users
   ```
   Em que:

   | Parâmetro | DESCRIÇÃO |
   |---|---|
   | `azure.activedirectory.tenant-id` | Contém a **ID de Diretório** anterior do seu Active Directory. |
   | `spring.security.oauth2.client.registration.azure.client-id` | Contém a **ID de Aplicativo** do registro de aplicativo que você preencheu anteriormente. |
   | `spring.security.oauth2.client.registration.azure.client-secret` | Contém o **Valor** da chave do registro de aplicativo que você preencheu anteriormente. |
   | `azure.activedirectory.active-directory-groups` | Contém uma lista dos grupos do Active Directory a usar para autorização. |

   > [!NOTE]
   > 
   > Para obter uma lista completa de valores que estão disponíveis em seu arquivo *application.properties*, consulte o [Exemplo de Spring Boot do Azure Active Directory][AAD Spring Boot Sample] no GitHub.
   >

1. Salve e feche o arquivo *application.properties*.

1. Crie uma pasta chamada *controller* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/controller*.

1. Crie um arquivo Java chamado *HelloController.java* na pasta *controller* e abra-o em um editor de texto.

1. Insira o código a seguir, depois salve e feche o arquivo:

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
   > O nome do grupo que você especificar para o método `@PreAuthorize("hasRole('')")` deve conter um dos grupos que você especificou no campo `azure.activedirectory.active-directory-groups` de seu arquivo *application.properties*.
   >

   > [!NOTE]
   > 
   > Você pode especificar configurações de autorização diferentes para mapeamentos de solicitação diferentes; por exemplo:
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

1. Crie uma pasta chamada *security* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/security*.

1. Crie um novo arquivo Java chamado *WebSecurityConfig.java* na pasta *security* e abra-o em um editor de texto.

1. Insira o código a seguir, depois salve e feche o arquivo:

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

## <a name="build-and-test-your-app"></a>Crie e testar seu aplicativo

1. Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* do aplicativo está localizado.

1. Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Crie seu aplicativo][build-application]

1. Após a criação e inicialização de seu aplicativo pelo Maven, abra <http://localhost:8080> em um navegador da Web; você deverá receber uma solicitação por um nome de usuário e senha.

   ![Fazer logon em seu aplicativo][application-login]

   > [!NOTE]
   > 
   > Você pode ser solicitado a alterar sua senha se for a primeira conexão para uma nova conta de usuário.
   > 
   > ![Alterando sua senha][update-password]
   > 

1. Após o logon bem-sucedido, você deverá ver o texto "Olá, Mundo" de exemplo no controlador.

   ![Logon bem-sucedido][hello-world]

   > [!NOTE]
   > 
   > Contas de usuário sem autorização receberão uma mensagem **HTTP 403 Não autorizado**.
   >

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um novo aplicativo Web do Java usando o iniciador do Azure Active Directory, configurou um novo locatário do Azure AD e registrou um novo aplicativo, em seguida, configurou o aplicativo para usar as classes e as anotações do Spring para proteger o aplicativo Web. Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.

> [!div class="nextstepaction"]
> [Spring no Azure](/java/azure/spring-framework)

<!-- URL List -->

[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure for Java Developers]: /java/azure/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
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
[directory-16]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-16.png
[directory-17]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-17.png
[directory-18]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-18.png
[directory-19]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-19.png
[directory-20]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-20.png
[directory-21]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-21.png
[directory-22]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-22.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
