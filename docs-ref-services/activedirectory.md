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
ms.service: active-directory
ms.openlocfilehash: 28063a1a4299fd78ba76533d0ffdc0346434eea2
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823779"
---
# <a name="azure-active-directory-libraries-for-java"></a>Bibliotecas do Azure Active Directory para Java

## <a name="overview"></a>Visão geral

Conectar usuários e controlar o acesso a aplicativos e APIs com o [Azure Active Directory](/azure/active-directory/active-directory-whatis).

Para começar a usar o Azure AD, consulte [Conectar-se e desconectar-se de aplicativo Web de Java com o Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).

## <a name="client-library"></a>Biblioteca do cliente

Configurar a autenticação do OAuth2, OpenID Connect ou Active Directory Graph e conexão de acesso único [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) com a [biblioteca de autenticação do Azure Active Directory (ADAL) para Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Recuperar um Token Web JSON (JWT) para um usuário em um locatário do Active Directory usando a [API do Graph](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) do Azure Active Directory. Esse token, em seguida, pode ser usado para autenticar o usuário com um aplicativo ou com a API.

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

## <a name="management-api"></a>API de gerenciamento

Configurar [controle de acesso baseado em função](/azure/active-directory/role-based-access-control-what-is) e atribuir identidades (como usuários e [entidades de serviço](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)) para essas funções com a API de gerenciamento. 

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Exemplo 

Criar uma nova entidade de serviço e atribuir a ela a função de Colaborador.

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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/activedirectory/management)


## <a name="samples"></a>Exemplos

[Gerenciar grupos, usuários e funções](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)    
[Conectar e desconectar usuários em um aplicativo Web de Java](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)    
[Acessar uma API com o Azure AD usando um aplicativo de linha de comando](https://github.com/Azure-Samples/active-directory-java-native-headless)   
[Chamar a API do Graph do Active AD a partir do seu aplicativo Web de Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web/)  

Explorar mais [exemplos de código Java para o Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) que você pode usar nos seus aplicativos.
