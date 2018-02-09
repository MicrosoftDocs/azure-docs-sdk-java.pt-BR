---
title: Como usar o iniciador do Spring Boot para o Azure Active Directory
description: Descubra como configurar um aplicativo inicializador do Spring Boot com o iniciador do Azure Active Directory.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: cf1cad0b87626058f7204a6565d09fb8901b7ce4
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a>Como usar o iniciador do Spring Boot para o Azure Active Directory

## <a name="overview"></a>Visão geral

Este artigo demonstra como criar um aplicativo com o **[Spring Initializr]**, que é o iniciador do Spring Boot do Azure Active Directory (Azure AD).

## <a name="prerequisites"></a>pré-requisitos

Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.
* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Criar um aplicativo personalizado usando o Spring Initializr

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

1. Preencha os campos **Nome da organização** e **Nome de domínio inicial** e clique em **Criar**.

   ![Especificar nomes do Azure Active Directory][directory-02]

1. Selecione o novo Azure Active Directory no menu suspenso na barra de ferramentas superior do portal do Azure.

   ![Escolher seu Azure Active Directory][directory-03]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Adicionar um registro de aplicativo para seu aplicativo do Spring Boot

1. Selecione **Azure Active Directory** no menu do portal, clique em **Visão geral**, depois, em **Registros de aplicativo**.

   ![Adicionar um novo registro de aplicativo][directory-04]

1. Clique em **Novo registro de aplicativo**, especifique o **Nome** do aplicativo, use http://localhost:8080 como a **URL de entrada** e depois clique em **Criar**.

   ![Criar novo registro de aplicativo][directory-05]

1. Clique em seu registro de aplicativo depois de ele ter sido criado.

   ![Selecione o registro de aplicativo][directory-06]

1. Quando estiver na página do registro do aplicativo, anote a **ID do aplicativo** para usar mais tarde e clique em **Chaves**.

   ![Criar chaves do registro de aplicativo][directory-07]

1. Adicione uma **Descrição**, especifique a **Duração** de uma nova chave e clique em **Salvar**. O valor da chave será preenchido automaticamente quando você clicar no ícone **Salvar**. Anote esse valor, ele será necessário posteriormente. (Você não conseguirá recuperar esse valor depois.)

   ![Especificar parâmetros da chave de registro do aplicativo][directory-08]

1. Na página principal do registro do aplicativo, clique em **Permissões necessárias**.

   ![Permissões necessárias para o registro do aplicativo][directory-09]

1. Clique em **Microsoft Azure Active Directory**.

   ![Selecione Microsoft Azure Active Directory][directory-10]

1. Marque as caixas **Acessar o diretório como o usuário conectado** e **Entrar e ler o perfil de usuário**, depois clique em **Salvar**.

   ![Habilitar permissões de acesso][directory-11]

1. Na página **Permissões necessárias**, clique em **Conceder Permissões** e em **Sim**, quando solicitado.

   ![Conceder permissões de acesso][directory-12]

## <a name="configure-and-compile-your-spring-boot-application"></a>Configurar e compilar seu aplicativo Spring Boot

1. Extraia em um diretório os arquivos do projeto baixado.

1. Navegue até a pasta pai no seu projeto e abra o arquivo *pom.xml* em um editor de texto.

1. Adicione a dependência da segurança do Spring OAuth2. Por exemplo:

   ```xml
   <dependency>
      <groupId>org.springframework.security.oauth</groupId>
      <artifactId>spring-security-oauth2</artifactId>
   </dependency>
   ```

1. Salve e feche o arquivo *pom.xml*.

1. Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* em um editor de texto.

1. Adicione a chave para sua conta de armazenamento usando os valores anteriores. Por exemplo:

   ```yaml
   # Specifies your Active Directory Application ID:
   azure.activedirectory.clientId=11111111-1111-1111-1111-1111111111111111

   # Specifies your secret key:
   azure.activedirectory.clientSecret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.activeDirectoryGroups=Users
   ```
   Em que:
   | Parâmetro | Descrição |
   |---|---|
   | `azure.activedirectory.clientId` | Contém a **ID do aplicativo**, que foi anotada anteriormente. |
   | `azure.activedirectory.clientSecret` | Contém o valor da chave do registro de aplicativo que você preencheu anteriormente. |
   | `azure.activedirectory.activeDirectoryGroups` | Contém uma lista dos grupos do Active Directory a serem usados para autenticação. |


1. Salve e feche o arquivo *application.properties*.

1. Crie uma pasta chamada *controller* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/controller*.

1. Crie um arquivo Java chamado *HelloController.java* na pasta *controller* e abra-o em um editor de texto.

1. Insira o código a seguir, depois salve e feche o arquivo:

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

1. Crie uma pasta chamada *security* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/security*.

1. Crie um novo arquivo Java chamado *WebSecurityConfig.java* na pasta *security* e abra-o em um editor de texto.

1. Insira o código a seguir, depois salve e feche o arquivo:

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

## <a name="build-and-test-your-app"></a>Crie e testar seu aplicativo

1. Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* do aplicativo está localizado.

1. Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:

   ```shell
   mvn clean package
   ```

   ![Crie seu aplicativo][build-application]

1. Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Depois que seu aplicativo for criado e iniciado pelo Maven, abra <http://localhost:8080> em um navegador da Web.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar o Azure Active Directory, veja estes artigos:

* [Documentação do Azure Active Directory].

Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:

* [Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].

O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos. Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>. Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.

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
