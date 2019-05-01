---
ms.openlocfilehash: 0a9b06932baa51c3cf003a4485a3a25261ffe91d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592494"
---
Criar um [arquivo de autenticação](../java-sdk-azure-authenticate.md#mgmt-file) e exportar uma variável de ambiente `AZURE_AUTH_LOCATION` na linha de comando com o caminho completo para o arquivo.

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

O arquivo de autenticação é usado para configurar o objeto `Azure` do ponto de entrada objeto usado pelas bibliotecas de gerenciamento para definir, criar e configurar os recursos do Azure.

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

[Saiba mais](../java-sdk-azure-authenticate.md#mgmt-auth) sobre as opções de autenticação ao usar as bibliotecas de gerenciamento do Azure para Java.