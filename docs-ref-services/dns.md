---
title: Bibliotecas de DNS do Azure para Java
description: Documentação de referência para as bibliotecas de gerenciamento de Java de DNS do Azure
keywords: Azure, Java, SDK, API, domínios, DNS, nome, service, serviço de nome de domínio
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: 2cd8fe7ee4d6a87da32a349fe8f1d2815d3fd36d
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892897"
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Bibliotecas do Gerenciador de Tráfego do Azure para Java

## <a name="overview"></a>Visão geral

Fornecer resolução de nome de domínio e gerenciar seus registros DNS usando as mesmas credenciais, APIs, ferramentas e cobrança que seus outros serviços do Azure com o [DNS do Azure](/azure/dns/dns-overview).

Para começar a usar o DNS do Azure, consulte [Introdução ao DNS do Azure usando a CLI do Azure 2.0](/azure/dns/dns-getstarted-cli).

## <a name="management-api"></a>API de gerenciamento

Criar zonas de DNS e adicionar registros às zonas com a API de gerenciamento.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Exemplo

Criar uma zona de DNS de raiz e adicionar um registro CNAME `www` em um grupo de recursos existentes.

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/dns/management)

## <a name="samples"></a>Exemplos

[Hospedar e gerenciar seus domínios com DNS do Azure](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

Explorar mais [exemplos de código Java para o DNS do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) que você pode usar em seus aplicativos.

<!---Loc Comment: Please, refer to conversation section to check the issue. Thanks.--->
