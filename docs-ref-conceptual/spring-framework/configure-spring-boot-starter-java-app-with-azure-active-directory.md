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
ms.date: 12/19/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: b3d97917deffa75bfab5f0d9ded64affd90139e1
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991390"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="f6414-103">Tutorial: Proteger um aplicativo Web do Java usando o iniciador do Spring Boot para o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6414-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="f6414-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f6414-104">Overview</span></span>

<span data-ttu-id="f6414-105">Este artigo demonstra como criar um aplicativo Java com o **[Spring Initializr]**, que usa o Iniciador do Spring Boot para o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6414-105">This article demonstrates creating a Java app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6414-106">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="f6414-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f6414-107">Criar um aplicativo do Java usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="f6414-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="f6414-108">Configurar o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6414-108">Configure Azure Active Directory</span></span>
> * <span data-ttu-id="f6414-109">Proteger o aplicativo com classes e anotações do Spring Boot</span><span class="sxs-lookup"><span data-stu-id="f6414-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="f6414-110">Compilar e testar seu aplicativo do Java</span><span class="sxs-lookup"><span data-stu-id="f6414-110">Build and test your Java application</span></span>

<span data-ttu-id="f6414-111">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="f6414-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6414-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f6414-112">Prerequisites</span></span>

<span data-ttu-id="f6414-113">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="f6414-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="f6414-114">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="f6414-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="f6414-115">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="f6414-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="f6414-116">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f6414-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="f6414-117">Criar um aplicativo usando o Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="f6414-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="f6414-118">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="f6414-118">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="f6414-119">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="f6414-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar os nomes do grupo e do artefato][create-spring-app-01]

1. <span data-ttu-id="f6414-121">Role para baixo até a seção **Principal** e marque a caixa **Segurança**; na seção **Web**, marque a caixa **Web**; depois role para baixo até a seção **Azure** e marque a caixa **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6414-121">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**, then scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Selecionar os iniciadores de Segurança, da Web e do Azure Active Directory][create-spring-app-02]

1. <span data-ttu-id="f6414-123">Role até a parte superior ou inferior da página e clique no botão **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="f6414-123">Scroll to the top or bottom of the page and click the button to **Generate Project**.</span></span>

   ![Gerar projeto do Spring Boot][create-spring-app-03]

1. <span data-ttu-id="f6414-125">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="f6414-125">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="f6414-126">Criar uma instância do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6414-126">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="f6414-127">Criar a instância do Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6414-127">Create the Active Directory instance</span></span>

1. <span data-ttu-id="f6414-128">Faça logon em <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="f6414-128">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="f6414-129">Clique em **+Criar um recurso**, depois em **Identidade** e **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6414-129">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory**.</span></span>

   ![Criar uma nova instância do Azure Active Directory][create-directory-01]

1. <span data-ttu-id="f6414-131">Insira o **Nome da organização** e seu **Nome de domínio inicial**.</span><span class="sxs-lookup"><span data-stu-id="f6414-131">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="f6414-132">Copie a URL completa de seu diretório. Você usará isso para adicionar as contas de usuário mais tarde neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6414-132">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="f6414-133">(Por exemplo, `wingtiptoysdirectory.onmicrosoft.com`.) Ao terminar, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f6414-133">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Especificar nomes do Azure Active Directory][create-directory-02]

1. <span data-ttu-id="f6414-135">Selecione o nome de sua conta à direita superior da barra de ferramentas do portal do Azure, depois clique em **Trocar diretório**.</span><span class="sxs-lookup"><span data-stu-id="f6414-135">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Selecionar o nome da conta do Azure][create-directory-03]

1. <span data-ttu-id="f6414-137">Selecione o novo Azure Active Directory no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="f6414-137">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Escolher seu Azure Active Directory][create-directory-04]

1. <span data-ttu-id="f6414-139">Selecione **Azure Active Directory** no menu do portal, clique em **Propriedades** e copie a **ID do Diretório**. Você usará esse valor para configurar o arquivo *application.properties* posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6414-139">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Copiar sua ID do Azure Active Directory][create-directory-05]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="f6414-141">Adicionar um registro de aplicativo para seu aplicativo do Spring Boot</span><span class="sxs-lookup"><span data-stu-id="f6414-141">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="f6414-142">Selecione **Azure Active Directory** no menu do portal, clique em **Registros do aplicativo**, depois em **Novo registro do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="f6414-142">Select **Azure Active Directory** from the portal menu, click **App registrations**, and then click **New application registration**, .</span></span>

   ![Adicionar um novo registro de aplicativo][create-app-registration-01]

2. <span data-ttu-id="f6414-144">Especifique o **Nome** do aplicativo, use http://localhost:8080 para a **URL de entrada**, depois clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f6414-144">Specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Criar novo registro de aplicativo][create-app-registration-02]

4. <span data-ttu-id="f6414-146">Quando a página de registro do aplicativo aparecer, copie seu **ID do aplicativo**. Você usará esse valor para configurar o arquivo *application.properties* posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6414-146">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="f6414-147">Clique em **Configurações** e **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="f6414-147">Click **Settings**, and then click **Keys**.</span></span>

   ![Criar chaves do registro de aplicativo][create-app-registration-03]

5. <span data-ttu-id="f6414-149">Adicione uma **Descrição**, especifique a **Duração** de uma nova chave e clique em **Salvar**. O valor da chave será preenchido automaticamente quando clicar no ícone **Salvar** e você precisará copiar o valor da chave para configurar o arquivo *application.properties* posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6414-149">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="f6414-150">(Você não conseguirá recuperar esse valor depois.)</span><span class="sxs-lookup"><span data-stu-id="f6414-150">(You will not be able to retrieve this value later.)</span></span>

   ![Especificar parâmetros da chave de registro do aplicativo][create-app-registration-04]

6. <span data-ttu-id="f6414-152">Na página principal do registro do aplicativo, clique em **Configurações** e depois em **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="f6414-152">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Permissões necessárias para o registro do aplicativo][create-app-registration-05]

7. <span data-ttu-id="f6414-154">Clique em **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6414-154">Click **Windows Azure Active Directory**.</span></span>

   ![Selecione Microsoft Azure Active Directory][create-app-registration-06]

8. <span data-ttu-id="f6414-156">Marque as caixas **Acessar o diretório como o usuário conectado** e **Entrar e ler o perfil de usuário**, depois clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f6414-156">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Habilitar permissões de acesso][create-app-registration-07]

9. <span data-ttu-id="f6414-158">Na página **Permissões necessárias**, clique em **Conceder Permissões** e em **Sim**, quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="f6414-158">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Conceder permissões de acesso][create-app-registration-08]

10. <span data-ttu-id="f6414-160">Na página principal do registro do aplicativo, clique em **Configurações** e depois em **URLs de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="f6414-160">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![Editar URLs de Resposta][create-app-registration-09]

11. <span data-ttu-id="f6414-162">Insira "<http://localhost:8080/login/oauth2/code/azure>" como uma nova URL de resposta e depois clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f6414-162">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![Adicionar nova URL de Resposta][create-app-registration-10]

12. <span data-ttu-id="f6414-164">Na página principal de registro do aplicativo, clique em **Manifesto**, em seguida defina o valor do `oauth2AllowImplicitFlow` parâmetro para `true` e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f6414-164">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![Configurar manifesto do aplicativo][create-app-registration-11]

    > [!NOTE]
    > 
    > <span data-ttu-id="f6414-166">Para obter mais informações sobre o `oauth2AllowImplicitFlow` parâmetro e outras configurações do aplicativo, consulte [Manifesto do aplicativo do Azure Active Directory][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="f6414-166">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="f6414-167">Adicionar uma conta de usuário ao diretório e adicionar essa conta a um grupo</span><span class="sxs-lookup"><span data-stu-id="f6414-167">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="f6414-168">Na página **Visão geral** do Active Directory, clique em **Todos os Usuários**, depois clique em **Novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="f6414-168">From the **Overview** page of your Active Directory, click **All Users**, and then click **New user**.</span></span>

   ![Adicionar uma nova conta de usuário][create-user-01]

1. <span data-ttu-id="f6414-170">Quando o painel **Usuário** for exibido, insira o **Nome** e o **Nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="f6414-170">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Inserir informações da conta de usuário][create-user-02]

   > [!NOTE]
   > 
   > <span data-ttu-id="f6414-172">Você precisa especificar a URL do diretório mostrada anteriormente neste tutorial quando inserir o nome de usuário. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6414-172">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="f6414-173">Clique em **Grupos**, selecione os grupos que você usará para a autorização em seu aplicativo, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="f6414-173">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="f6414-174">(Para este tutorial, adicione a conta ao grupo _Usuários_.)</span><span class="sxs-lookup"><span data-stu-id="f6414-174">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Selecionar os grupos do usuário][create-user-03]

1. <span data-ttu-id="f6414-176">Clique em **Mostrar senha**e copie a senha. Você usará isso quando entrar no aplicativo mais tarde neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6414-176">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span> <span data-ttu-id="f6414-177">Depois de ter copiado a senha, clique em **Criar** para adicionar a nova conta do usuário ao diretório.</span><span class="sxs-lookup"><span data-stu-id="f6414-177">When you have copied the password, click **Create** to add the new user account to your directory.</span></span>

   ![Mostrar a senha][create-user-04]

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="f6414-179">Configurar e compilar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f6414-179">Configure and compile your app</span></span>

1. <span data-ttu-id="f6414-180">Extraia os arquivos do arquivo de projeto criado e baixado antes neste tutorial para um diretório.</span><span class="sxs-lookup"><span data-stu-id="f6414-180">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="f6414-181">Navegue até a pasta-mãe no projeto e abra o `pom.xml`arquivo de projeto Maven em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="f6414-181">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

1. <span data-ttu-id="f6414-182">Adicione as dependências de segurança do Spring OAuth2 a `pom.xml`:</span><span class="sxs-lookup"><span data-stu-id="f6414-182">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

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

1. <span data-ttu-id="f6414-183">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="f6414-183">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="f6414-184">Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="f6414-184">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="f6414-185">Especifique as configurações de registro do aplicativo usando os valores criados anteriormente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6414-185">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="f6414-186">Em que:</span><span class="sxs-lookup"><span data-stu-id="f6414-186">Where:</span></span>

   | <span data-ttu-id="f6414-187">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f6414-187">Parameter</span></span> | <span data-ttu-id="f6414-188">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="f6414-188">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="f6414-189">Contém a **ID de Diretório** anterior do seu Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6414-189">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="f6414-190">Contém a **ID de Aplicativo** do registro de aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f6414-190">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="f6414-191">Contém o **Valor** da chave do registro de aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f6414-191">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="f6414-192">Contém uma lista dos grupos do Active Directory a usar para autorização.</span><span class="sxs-lookup"><span data-stu-id="f6414-192">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="f6414-193">Para obter uma lista completa de valores que estão disponíveis em seu arquivo *application.properties*, consulte o [Exemplo de Spring Boot do Azure Active Directory][AAD Spring Boot Sample] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f6414-193">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="f6414-194">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="f6414-194">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="f6414-195">Crie uma pasta chamada *controller* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="f6414-195">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="f6414-196">Crie um arquivo Java chamado *HelloController.java* na pasta *controller* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="f6414-196">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="f6414-197">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="f6414-197">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="f6414-198">O nome do grupo que você especificar para o método `@PreAuthorize("hasRole('')")` deve conter um dos grupos que você especificou no campo `azure.activedirectory.active-directory-groups` de seu arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="f6414-198">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   > 
   > <span data-ttu-id="f6414-199">Também é possível especificar configurações de autorização diferentes para mapeamentos de solicitação diferentes; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6414-199">You can also specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="f6414-200">Crie uma pasta chamada *security* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="f6414-200">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="f6414-201">Crie um novo arquivo Java chamado *WebSecurityConfig.java* na pasta *security* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="f6414-201">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="f6414-202">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="f6414-202">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="f6414-203">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f6414-203">Build and test your app</span></span>

1. <span data-ttu-id="f6414-204">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* do aplicativo está localizado.</span><span class="sxs-lookup"><span data-stu-id="f6414-204">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="f6414-205">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6414-205">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Crie seu aplicativo][build-application]

1. <span data-ttu-id="f6414-207">Após a criação e inicialização de seu aplicativo pelo Maven, abra <http://localhost:8080> em um navegador da Web; você deverá receber uma solicitação por um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="f6414-207">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Fazer logon em seu aplicativo][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="f6414-209">Você pode ser solicitado a alterar sua senha se for a primeira conexão para uma nova conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="f6414-209">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Alterando sua senha][update-password]
   > 

1. <span data-ttu-id="f6414-211">Após o logon bem-sucedido, você deverá ver o texto "Olá, Mundo" de exemplo no controlador.</span><span class="sxs-lookup"><span data-stu-id="f6414-211">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Logon bem-sucedido][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="f6414-213">Contas de usuário sem autorização receberão uma mensagem **HTTP 403 Não autorizado**.</span><span class="sxs-lookup"><span data-stu-id="f6414-213">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="summary"></a><span data-ttu-id="f6414-214">Resumo</span><span class="sxs-lookup"><span data-stu-id="f6414-214">Summary</span></span>

<span data-ttu-id="f6414-215">Neste tutorial, você criou um novo aplicativo Web do Java usando o iniciador do Azure Active Directory, configurou um novo locatário do Azure AD e registrou um novo aplicativo, em seguida, configurou o aplicativo para usar as classes e as anotações do Spring para proteger o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f6414-215">In this tutorial, you created a new Java web application using the Azure Active Directory starter, configured a new Azure AD tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6414-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6414-216">Next steps</span></span>

<span data-ttu-id="f6414-217">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6414-217">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6414-218">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="f6414-218">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure for Java Developers]: /java/azure/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[create-spring-app-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-01.png
[create-spring-app-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-02.png
[create-spring-app-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-03.png

[create-directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-01.png
[create-directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-02.png
[create-directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-03.png
[create-directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-04.png
[create-directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-05.png

[create-app-registration-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-01.png
[create-app-registration-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-02.png
[create-app-registration-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-03.png
[create-app-registration-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-04.png
[create-app-registration-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-05.png
[create-app-registration-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-06.png
[create-app-registration-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-07.png
[create-app-registration-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-08.png
[create-app-registration-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-09.png
[create-app-registration-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-10.png
[create-app-registration-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-11.png

[create-user-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-01.png
[create-user-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-02.png
[create-user-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-03.png
[create-user-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-04.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
