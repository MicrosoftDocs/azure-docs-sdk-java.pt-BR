---
title: Bibliotecas do Azure Active Directory para Java
description: Documentação de referência para as bibliotecas de gerenciamento e de cliente de Java para o Azure Active Directory
keywords: Azure, Java, SDK, API, SQL, autenticação, AAD, Active Directory, Graph, OAuth 2.0
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.openlocfilehash: 6147fc959727b53cd796534cefc927145b52d81d
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799832"
---
# <a name="azure-active-directory-libraries-for-java"></a><span data-ttu-id="71921-104">Bibliotecas do Azure Active Directory para Java</span><span class="sxs-lookup"><span data-stu-id="71921-104">Azure Active Directory libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="71921-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="71921-105">Overview</span></span>

<span data-ttu-id="71921-106">Conectar usuários e controlar o acesso a aplicativos e APIs com o [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span><span class="sxs-lookup"><span data-stu-id="71921-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

<span data-ttu-id="71921-107">Para começar a usar o Azure AD, consulte [Conectar-se e desconectar-se de aplicativo Web de Java com o Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span><span class="sxs-lookup"><span data-stu-id="71921-107">To get started with Azure AD, see [Java web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="71921-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="71921-108">Client library</span></span>

<span data-ttu-id="71921-109">Configurar a autenticação do OAuth2, OpenID Connect ou Active Directory Graph e conexão de acesso único [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) com a [biblioteca de autenticação do Azure Active Directory (ADAL) para Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span><span class="sxs-lookup"><span data-stu-id="71921-109">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span></span>

<span data-ttu-id="71921-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="71921-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="71921-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="71921-111">Example</span></span>

<span data-ttu-id="71921-112">Recuperar um Token Web JSON (JWT) para um usuário em um locatário do Active Directory usando a [API do Graph](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71921-112">Retrieve a JSON Web Token (JWT) for a user in your an Active Directory tenant using Azure Active Directory's [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api).</span></span> <span data-ttu-id="71921-113">Esse token, em seguida, pode ser usado para autenticar o usuário com um aplicativo ou com a API.</span><span class="sxs-lookup"><span data-stu-id="71921-113">This token can then be used to authenticate the user with an application or API.</span></span>

```java
ExecutorService service = Executors.newFixedThreadPool(1);
AuthenticationContext context = new AuthenticationContext(AUTHORITY, false, service);
Future<AuthenticationResult> future = context.acquireToken(
    "https://graph.windows.net", YOUR_TENANT_ID, username, password,
    null);
AuthenticationResult result = future.get();
System.out.println("Access Token - " + result.getAccessToken());
System.out.println("Refresh Token - " + result.getRefreshToken());
System.out.println("ID Token - " + result.getIdToken());
```

## <a name="management-api"></a><span data-ttu-id="71921-114">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="71921-114">Management API</span></span>

<span data-ttu-id="71921-115">Configurar [controle de acesso baseado em função](/azure/active-directory/role-based-access-control-what-is) e atribuir identidades (como usuários e [entidades de serviço](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) para essas funções com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="71921-115">Configure [role based access control](/azure/active-directory/role-based-access-control-what-is) and assign identities (such as users and [service principals](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) to those roles with the management API.</span></span> 

<span data-ttu-id="71921-116">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="71921-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="71921-117">Exemplo</span><span class="sxs-lookup"><span data-stu-id="71921-117">Example</span></span> 

<span data-ttu-id="71921-118">Criar uma nova entidade de serviço e atribuir a ela a função de Colaborador.</span><span class="sxs-lookup"><span data-stu-id="71921-118">Create a new service principal and assign it the Contributor role.</span></span>

```java
ServicePrincipal sp = Azure.servicePrincipals().define(spName)
    .withNewApplication("http://" + spName)
    .create();
RoleAssignment roleAssignment2 = authenticated.roleAssignments()
    .define("contribRoleAssignment")
    .forServicePrincipal(sp)
    .withBuiltInRole(BuiltInRole.CONTRIBUTOR)
    .withSubscriptionScope("862f67bc-d3ae-4243-bec7-3da6dca77717")
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="71921-119">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="71921-119">Explore the Management APIs</span></span>](/java/api/overview/azure/activedirectory/management)


## <a name="samples"></a><span data-ttu-id="71921-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="71921-120">Samples</span></span>

<span data-ttu-id="71921-121">[Gerenciar grupos, usuários e funções](https://github.com/Azure-Samples/aad-java-manage-users-groups-and-roles)  </span><span class="sxs-lookup"><span data-stu-id="71921-121">[Manage groups, users, and roles](https://github.com/Azure-Samples/aad-java-manage-users-groups-and-roles)  </span></span>  
<span data-ttu-id="71921-122">[Conectar e desconectar usuários em um aplicativo Web de Java](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span><span class="sxs-lookup"><span data-stu-id="71921-122">[Sign-in and sign-out users in a Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span></span>  
<span data-ttu-id="71921-123">[Acessar uma API com o Azure AD usando um aplicativo de linha de comando](https://github.com/Azure-Samples/active-directory-java-native-headless) </span><span class="sxs-lookup"><span data-stu-id="71921-123">[Access an API with Azure AD using a command line app](https://github.com/Azure-Samples/active-directory-java-native-headless) </span></span>  
[<span data-ttu-id="71921-124">Chamar a API do Graph do Active AD a partir do seu aplicativo Web de Java</span><span class="sxs-lookup"><span data-stu-id="71921-124">Call the Active AD Graph API from your Java web app</span></span>](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  

<span data-ttu-id="71921-125">Explorar mais [exemplos de código Java para o Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) que você pode usar nos seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="71921-125">Explore more [sample Java code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) you can use in your apps.</span></span>
