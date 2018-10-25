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
ms.openlocfilehash: 84ea77a19c326409f453f62359cf46c90398daeb
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799922"
---
# <a name="azure-key-vault-libraries-for-java"></a>Bibliotecas do Azure Key Vault para Java

## <a name="overview"></a>Visão geral

Proteger e gerenciar as chaves de criptografia e os segredos usados por aplicativos e serviços de nuvem com o [Azure Key Vault](/azure/key-vault/).

Para saber mais sobre como configurar o Azure Key Vault, consulte [Introdução ao Azure Key Vault](/azure/key-vault/key-vault-get-started).

## <a name="client-library"></a>Biblioteca do cliente

Criar, atualizar e excluir chaves e segredos no Azure Key Vault com as bibliotecas de cliente.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.1.0</version>
</dependency>
```   

## <a name="example"></a>Exemplo

Recuperar uma [chave da Web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) de um Cofre de Chaves.

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [Explorar as APIs de cliente](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a>API de gerenciamento

Use as bibliotecas de gerenciamento do Azure Key Vault para criar cofres de chaves, autorizar aplicativos e gerenciar permissões. 

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.15.0</version>
</dependency>
```

## <a name="example"></a>Exemplo

Autorizar um aplicativo em execução com a [entidade de serviço](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` para listar e recuperar segredos de um cofre de chaves. 

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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a>Exemplos

Explorar mais [exemplos de código Java para o Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) que você pode usar em seus aplicativos.
