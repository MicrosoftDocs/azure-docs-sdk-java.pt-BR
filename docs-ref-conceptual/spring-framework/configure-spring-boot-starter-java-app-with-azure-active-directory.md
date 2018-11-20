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
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="e1879-103">Tutorial: Proteger um aplicativo Web do Java usando o iniciador do Spring Boot para o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1879-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="e1879-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e1879-104">Overview</span></span>

<span data-ttu-id="e1879-105">Este artigo demonstra como criar um aplicativo com o **[Spring Initializr]**, que é o iniciador do Spring Boot do Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1879-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1879-106">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="e1879-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1879-107">Criar um aplicativo do Java usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="e1879-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="e1879-108">Configurar o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1879-108">Configure Azure Active Directory</span></span>
> * <span data-ttu-id="e1879-109">Proteger o aplicativo com classes e anotações do Spring Boot</span><span class="sxs-lookup"><span data-stu-id="e1879-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="e1879-110">Compilar e testar seu aplicativo do Java</span><span class="sxs-lookup"><span data-stu-id="e1879-110">Build and test your Java application</span></span>

<span data-ttu-id="e1879-111">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="e1879-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1879-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e1879-112">Prerequisites</span></span>

<span data-ttu-id="e1879-113">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="e1879-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="e1879-114">Um [Java Development Kit (JDK)](https://aka.ms/azure-jdks) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e1879-114">A [Java Development Kit (JDK)](https://aka.ms/azure-jdks), version 1.7 or later.</span></span>
* <span data-ttu-id="e1879-115">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e1879-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-application-using-the-spring-initializr"></a><span data-ttu-id="e1879-116">Criar um aplicativo usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="e1879-116">Create an application using the Spring Initializr</span></span>

1. <span data-ttu-id="e1879-117">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e1879-117">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e1879-118">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="e1879-118">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar os nomes do grupo e do artefato][security-01]

1. <span data-ttu-id="e1879-120">Role para baixo até a seção **Núcleo**, marque a caixa **Segurança** e, na seção **Web**, marque a caixa **Web**.</span><span class="sxs-lookup"><span data-stu-id="e1879-120">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Selecione os iniciadores de segurança e da Web][security-02]

1. <span data-ttu-id="e1879-122">Role para baixo até a seção **Azure** e marque a caixa do **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1879-122">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Selecionar iniciador do Azure Active Directory][security-03]

1. <span data-ttu-id="e1879-124">Role até a parte inferior da página e clique no botão **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="e1879-124">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Gerar projeto do Spring Boot][security-04]

1. <span data-ttu-id="e1879-126">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="e1879-126">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="e1879-127">Criar e configurar uma nova instância do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1879-127">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="e1879-128">Criar a instância do Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1879-128">Create the Active Directory instance</span></span>

1. <span data-ttu-id="e1879-129">Faça logon em <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="e1879-129">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="e1879-130">Clique em **+Novo**, depois em **Segurança + Identidade** e em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1879-130">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Criar uma nova instância do Azure Active Directory][directory-01]

1. <span data-ttu-id="e1879-132">Insira o **Nome da organização** e seu **Nome de domínio inicial**.</span><span class="sxs-lookup"><span data-stu-id="e1879-132">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="e1879-133">Copie a URL completa de seu diretório. Você usará isso para adicionar as contas de usuário mais tarde neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1879-133">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="e1879-134">(Por exemplo, `wingtiptoysdirectory.onmicrosoft.com`.) Ao terminar, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e1879-134">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Especificar nomes do Azure Active Directory][directory-02]

1. <span data-ttu-id="e1879-136">Selecione o novo Azure Active Directory no menu suspenso na barra de ferramentas superior do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1879-136">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Escolher seu Azure Active Directory][directory-03]

1. <span data-ttu-id="e1879-138">Selecione **Azure Active Directory** no menu do portal, clique em **Propriedades** e copie a **ID do Diretório**. Você usará esse valor para configurar o arquivo *application.properties* posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1879-138">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Copiar sua ID do Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="e1879-140">Adicionar um registro de aplicativo para seu aplicativo do Spring Boot</span><span class="sxs-lookup"><span data-stu-id="e1879-140">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="e1879-141">Selecione **Azure Active Directory** no menu do portal, clique em **Visão geral**, depois, em **Registros de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e1879-141">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Adicionar um novo registro de aplicativo][directory-04]

2. <span data-ttu-id="e1879-143">Clique em **Novo registro de aplicativo**, especifique o **Nome** do aplicativo, use http://localhost:8080 como a **URL de entrada** e depois clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e1879-143">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Criar novo registro de aplicativo][directory-05]

3. <span data-ttu-id="e1879-145">Clique em seu registro de aplicativo depois de ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="e1879-145">Click your application registration after it has been created.</span></span>

   ![Selecione o registro de aplicativo][directory-06]

4. <span data-ttu-id="e1879-147">Quando a página de registro do aplicativo aparecer, copie seu **ID do aplicativo**. Você usará esse valor para configurar o arquivo *application.properties* posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1879-147">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="e1879-148">Clique em **Configurações** e **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="e1879-148">Click **Settings**, and then click **Keys**.</span></span>

   ![Criar chaves do registro de aplicativo][directory-07]

5. <span data-ttu-id="e1879-150">Adicione uma **Descrição**, especifique a **Duração** de uma nova chave e clique em **Salvar**. O valor da chave será preenchido automaticamente quando clicar no ícone **Salvar** e você precisará copiar o valor da chave para configurar o arquivo *application.properties* posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1879-150">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="e1879-151">(Você não conseguirá recuperar esse valor depois.)</span><span class="sxs-lookup"><span data-stu-id="e1879-151">(You will not be able to retrieve this value later.)</span></span>

   ![Especificar parâmetros da chave de registro do aplicativo][directory-08]

6. <span data-ttu-id="e1879-153">Na página principal do registro do aplicativo, clique em **Configurações** e depois em **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="e1879-153">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Permissões necessárias para o registro do aplicativo][directory-09]

7. <span data-ttu-id="e1879-155">Clique em **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1879-155">Click **Windows Azure Active Directory**.</span></span>

   ![Selecione Microsoft Azure Active Directory][directory-10]

8. <span data-ttu-id="e1879-157">Marque as caixas **Acessar o diretório como o usuário conectado** e **Entrar e ler o perfil de usuário**, depois clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e1879-157">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Habilitar permissões de acesso][directory-11]

9. <span data-ttu-id="e1879-159">Na página **Permissões necessárias**, clique em **Conceder Permissões** e em **Sim**, quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="e1879-159">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Conceder permissões de acesso][directory-12]

10. <span data-ttu-id="e1879-161">Na página principal do registro do aplicativo, clique em **Configurações** e depois em **URLs de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="e1879-161">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![Editar URLs de Resposta][directory-14]

11. <span data-ttu-id="e1879-163">Insira "<http://localhost:8080/login/oauth2/code/azure>" como uma nova URL de resposta e depois clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e1879-163">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![Adicionar nova URL de Resposta][directory-15]

12. <span data-ttu-id="e1879-165">Na página principal de registro do aplicativo, clique em **Manifesto**, em seguida defina o valor do `oauth2AllowImplicitFlow` parâmetro para `true` e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e1879-165">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![Configurar manifesto do aplicativo][directory-16]

    > [!NOTE]
    > 
    > <span data-ttu-id="e1879-167">Para obter mais informações sobre o `oauth2AllowImplicitFlow` parâmetro e outras configurações do aplicativo, consulte [Manifesto do aplicativo do Azure Active Directory][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="e1879-167">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="e1879-168">Adicionar uma conta de usuário ao diretório e adicionar essa conta a um grupo</span><span class="sxs-lookup"><span data-stu-id="e1879-168">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="e1879-169">Na página **Visão geral** do Active Directory, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e1879-169">From the **Overview** page of your Active Directory, click **Users**.</span></span>

   ![Abrir painel de Usuários][directory-17]

1. <span data-ttu-id="e1879-171">Quando o painel **Usuários** for exibido, clique em **Novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="e1879-171">When the **Users** panel is displayed, click **New user**.</span></span>

   ![Adicionar uma nova conta de usuário][directory-18]

1. <span data-ttu-id="e1879-173">Quando o painel **Usuário** for exibido, insira o **Nome** e o **Nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="e1879-173">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Inserir informações da conta de usuário][directory-19]

   > [!NOTE]
   > 
   > <span data-ttu-id="e1879-175">Você precisa especificar a URL do diretório mostrada anteriormente neste tutorial quando inserir o nome de usuário. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e1879-175">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="e1879-176">Clique em **Grupos**, selecione os grupos que você usará para a autorização em seu aplicativo, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="e1879-176">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="e1879-177">(Para este tutorial, adicione a conta ao grupo _Usuários_.)</span><span class="sxs-lookup"><span data-stu-id="e1879-177">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Selecionar os grupos do usuário][directory-20]

1. <span data-ttu-id="e1879-179">Clique em **Mostrar senha**e copie a senha. Você usará isso quando entrar no aplicativo mais tarde neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1879-179">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span>

   ![Mostrar a senha][directory-21]

1. <span data-ttu-id="e1879-181">Clique em **Criar** para adicionar a nova conta de usuário ao seu diretório.</span><span class="sxs-lookup"><span data-stu-id="e1879-181">Click **Create** to add the new user account to your directory.</span></span>

   ![Criar a nova conta de usuário][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="e1879-183">Configurar e compilar seu aplicativo Spring Boot</span><span class="sxs-lookup"><span data-stu-id="e1879-183">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="e1879-184">Extraia os arquivos do arquivo de projeto criado e baixado antes neste tutorial para um diretório.</span><span class="sxs-lookup"><span data-stu-id="e1879-184">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="e1879-185">Navegue até a pasta-mãe no projeto e abra o `pom.xml`arquivo de projeto Maven em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e1879-185">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

1. <span data-ttu-id="e1879-186">Adicione as dependências de segurança do Spring OAuth2 a `pom.xml`:</span><span class="sxs-lookup"><span data-stu-id="e1879-186">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

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

1. <span data-ttu-id="e1879-187">Salve e feche o arquivo *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="e1879-187">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="e1879-188">Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e1879-188">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="e1879-189">Especifique as configurações de registro do aplicativo usando os valores criados anteriormente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e1879-189">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="e1879-190">Em que:</span><span class="sxs-lookup"><span data-stu-id="e1879-190">Where:</span></span>

   | <span data-ttu-id="e1879-191">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e1879-191">Parameter</span></span> | <span data-ttu-id="e1879-192">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="e1879-192">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="e1879-193">Contém a **ID de Diretório** anterior do seu Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1879-193">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="e1879-194">Contém a **ID de Aplicativo** do registro de aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e1879-194">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="e1879-195">Contém o **Valor** da chave do registro de aplicativo que você preencheu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e1879-195">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="e1879-196">Contém uma lista dos grupos do Active Directory a usar para autorização.</span><span class="sxs-lookup"><span data-stu-id="e1879-196">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="e1879-197">Para obter uma lista completa de valores que estão disponíveis em seu arquivo *application.properties*, consulte o [Exemplo de Spring Boot do Azure Active Directory][AAD Spring Boot Sample] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1879-197">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="e1879-198">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="e1879-198">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="e1879-199">Crie uma pasta chamada *controller* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="e1879-199">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="e1879-200">Crie um arquivo Java chamado *HelloController.java* na pasta *controller* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e1879-200">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="e1879-201">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="e1879-201">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="e1879-202">O nome do grupo que você especificar para o método `@PreAuthorize("hasRole('')")` deve conter um dos grupos que você especificou no campo `azure.activedirectory.active-directory-groups` de seu arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="e1879-202">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="e1879-203">Você pode especificar configurações de autorização diferentes para mapeamentos de solicitação diferentes; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e1879-203">You can specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="e1879-204">Crie uma pasta chamada *security* na pasta de origem do Java para o seu aplicativo. Por exemplo: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="e1879-204">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="e1879-205">Crie um novo arquivo Java chamado *WebSecurityConfig.java* na pasta *security* e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e1879-205">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="e1879-206">Insira o código a seguir, depois salve e feche o arquivo:</span><span class="sxs-lookup"><span data-stu-id="e1879-206">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="e1879-207">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e1879-207">Build and test your app</span></span>

1. <span data-ttu-id="e1879-208">Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* do aplicativo está localizado.</span><span class="sxs-lookup"><span data-stu-id="e1879-208">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="e1879-209">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e1879-209">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Crie seu aplicativo][build-application]

1. <span data-ttu-id="e1879-211">Após a criação e inicialização de seu aplicativo pelo Maven, abra <http://localhost:8080> em um navegador da Web; você deverá receber uma solicitação por um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="e1879-211">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Fazer logon em seu aplicativo][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="e1879-213">Você pode ser solicitado a alterar sua senha se for a primeira conexão para uma nova conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="e1879-213">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Alterando sua senha][update-password]
   > 

1. <span data-ttu-id="e1879-215">Após o logon bem-sucedido, você deverá ver o texto "Olá, Mundo" de exemplo no controlador.</span><span class="sxs-lookup"><span data-stu-id="e1879-215">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Logon bem-sucedido][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="e1879-217">Contas de usuário sem autorização receberão uma mensagem **HTTP 403 Não autorizado**.</span><span class="sxs-lookup"><span data-stu-id="e1879-217">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="e1879-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1879-218">Next steps</span></span>

<span data-ttu-id="e1879-219">Neste tutorial, você criou um novo aplicativo Web do Java usando o iniciador do Azure Active Directory, configurou um novo locatário do Azure AD e registrou um novo aplicativo, em seguida, configurou o aplicativo para usar as classes e as anotações do Spring para proteger o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e1879-219">In this tutorial, you created a new Java web application using the Azure Active Directory starter, configured a new Azure AD tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span> <span data-ttu-id="e1879-220">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1879-220">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1879-221">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="e1879-221">Spring on Azure</span></span>](/java/azure/spring-framework)

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
