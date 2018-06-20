---
title: Bibliotecas do Azure Key Vault para Java
description: Visão geral das bibliotecas do Azure Key Vault para Java
keywords: Azure, Java, SDK, API, keyvault, seguro, chaves, segredos, cofre
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: 396d02b8bba5878ffb24f5f8994ae29aef36cfdc
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823819"
---
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="cb970-104">Bibliotecas do Azure Key Vault para Java</span><span class="sxs-lookup"><span data-stu-id="cb970-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="cb970-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cb970-105">Overview</span></span>

<span data-ttu-id="cb970-106">Proteger e gerenciar as chaves de criptografia e os segredos usados por aplicativos e serviços de nuvem com o [Azure Key Vault](/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="cb970-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="cb970-107">Para saber mais sobre como configurar o Azure Key Vault, consulte [Introdução ao Azure Key Vault](/azure/key-vault/key-vault-get-started).</span><span class="sxs-lookup"><span data-stu-id="cb970-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="cb970-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="cb970-108">Client library</span></span>

<span data-ttu-id="cb970-109">Criar, atualizar e excluir chaves e segredos no Azure Key Vault com as bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="cb970-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="cb970-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cb970-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="cb970-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cb970-111">Example</span></span>

<span data-ttu-id="cb970-112">Recuperar uma [chave da Web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) de um Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="cb970-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb970-113">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="cb970-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a><span data-ttu-id="cb970-114">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="cb970-114">Management API</span></span>

<span data-ttu-id="cb970-115">Use as bibliotecas de gerenciamento do Azure Key Vault para criar cofres de chaves, autorizar aplicativos e gerenciar permissões.</span><span class="sxs-lookup"><span data-stu-id="cb970-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="cb970-116">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cb970-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="cb970-117">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cb970-117">Example</span></span>

<span data-ttu-id="cb970-118">Autorizar um aplicativo em execução com a [entidade de serviço](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` para listar e recuperar segredos de um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="cb970-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

```java
vault1 = vault1.update()
            .defineAccessPolicy()
                .forServicePrincipal(clientId)
                .allowKeyAllPermissions()
                .allowSecretPermissions(SecretPermissions.GET)
                .allowSecretPermissions(SecretPermissions.LIST)
                .attach()
            .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb970-119">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="cb970-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a><span data-ttu-id="cb970-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="cb970-120">Samples</span></span>

<span data-ttu-id="cb970-121">[Gerenciar Cofres de Chaves][1]</span><span class="sxs-lookup"><span data-stu-id="cb970-121">[Manage Key Vaults][1]</span></span>   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

<span data-ttu-id="cb970-122">Explorar mais [exemplos de código Java para o Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="cb970-122">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>
