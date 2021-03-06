---
title: Biblioteca do Azure Resource Manager para Java
description: Documentação de referência para as bibliotecas do Gerenciador de Recursos de Java
keywords: Azure, Java, SDK, API, grupos de recursos, arm, gerenciador de recursos
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 7316c05e39bc88c50670dcb0f6331ce8440fd711
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799802"
---
# <a name="azure-resource-manager-libraries-for-java"></a>Biblioteca do Azure Resource Manager para Java

## <a name="overview"></a>Visão geral

Implantar, monitorar e gerenciar recursos em grupos com o [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API de gerenciamento

Use a API de gerenciamento para criar grupos de recursos e implantar recursos de modelos.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Exemplo

Criar um novo grupo de recursos na região Leste dos EUA do Azure.

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/resources/management)

## <a name="samples"></a>Exemplos

[Gerenciar Grupos de Recursos do Azure com Java][1] 
[Implantar recursos usando um modelo do ARM][2]

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

Exibir a [lista completa](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) de amostras do Azure Resource Manager.
