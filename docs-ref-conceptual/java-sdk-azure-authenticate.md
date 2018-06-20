---
title: Autenticar com as bibliotecas de gerenciamento do Azure para Java
description: Autenticar com uma entidade de serviço para as bibliotecas de gerenciamento do Azure para Java
keywords: Azure, Java, SDK, API, Maven, Gradle, autenticação, active directory, entidade de serviço
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 10f457e3-578b-4655-8cd1-51339226ee7d
ms.openlocfilehash: 1d556955fcc5b73f1ba099a0b846b571ba64ccff
ms.sourcegitcommit: 107c3c5ed8c6991c751f95bcaf3757220940df9e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34050723"
---
# <a name="authenticate-with-the-azure-libraries-for-java"></a>Autenticar com as bibliotecas do Azure para Java 

## <a name="connect-to-services-with-connection-strings"></a>Conectar-se aos serviços com cadeias de conexão

A maioria das bibliotecas de serviço do Azure usa uma cadeia de conexão ou a chave segura para autenticação. Por exemplo, o banco de dados SQL inclui informações de nome de usuário e senha na cadeia de conexão JDBC:

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

O Armazenamento do Azure usa uma chave de armazenamento para autorizar o aplicativo:

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

As cadeias de conexão de serviço são usadas para autenticar outros serviços do Azure como [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Cache Redis](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) e [Barramento de Serviço](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues). Você pode obter as cadeias de conexão usando a CLI ou o portal do Azure.  Você também pode usar as bibliotecas de gerenciamento do Azure para Java para consultar recursos para criar cadeias de conexão no seu código. 

Por exemplo, esse código usa as bibliotecas de gerenciamento para criar uma cadeia de conexão da conta de armazenamento:

```java
// create a new storage account
StorageAccount storage = azure.storageAccounts().getByResourceGroup("myResourceGroup","myStorageAccount");

// create a storage container to hold the file
List<StorageAccountKey> keys = storage.getKeys();
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.name()
        + ";AccountKey=" + keys.get(0).value()
        + ";EndpointSuffix=core.windows.net";
```

Outras bibliotecas exigem que o aplicativo seja executado com um [entidade de serviço](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) que autoriza o aplicativo a ser executado com as credenciais concedidas. Essa configuração é semelhante às etapas de autenticação baseada em objeto para a biblioteca de gerenciamento listadas abaixo.

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a>Autenticar com as bibliotecas de gerenciamento do Azure para Java

Duas opções estão disponíveis para autenticar seu aplicativo com o Azure ao usar as bibliotecas de gerenciamento do Java para criar e gerenciar recursos.

### <a name="authenticate-with-an-applicationtokencredentials-object"></a>Autenticar com um objeto ApplicationTokenCredentials

Crie uma instância de `ApplicationTokenCredentials` para fornecer as credenciais da entidade de serviço para o objeto `Azure` de nível superior de dentro do seu código.

```java
import com.microsoft.azure.credentials.ApplicationTokenCredentials;
import com.microsoft.azure.AzureEnvironment;

// ...

ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(client, 
        tenant,
        key, 
        AzureEnvironment.AZURE);
        
Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credentials)
        .withDefaultSubscription();
```

Os valores `client`, `tenant` e `key` são os mesmos valores de entidade de serviço usados na [autenticação baseada em arquivo](#mgmt-file). O valor `AzureEnvironment.AZURE` cria as credenciais na nuvem pública do Azure. Altere para um valor diferente se você precisar acessar outra nuvem (por exemplo, `AzureEnvironment.AZURE_GERMANY`).  

 Leia os valores da entidade de serviço de variáveis de ambiente ou de um repositório de gerenciamento de segredo como o [Cofre de Chaves](/azure/key-vault/key-vault-whatis). Evite definir esses valores como cadeias de caracteres de texto não criptografado em seu código para evitar expor acidentalmente credenciais no seu histórico de controle de versão.   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a>Autenticação baseada em arquivo (Visualização)

A maneira mais simples de autenticar é criar um arquivo de propriedades que contém as credenciais para uma [entidade de serviço do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) usando o seguinte formato:

```text
# sample management library properties file
subscription=########-####-####-####-############
client=########-####-####-####-############
key=XXXXXXXXXXXXXXXX
tenant=########-####-####-####-############
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

- assinatura: usar o valor *id* de `az account show` na CLI do Azure 2.0.
- cliente: usar o valor *appId* da saída obtida de uma entidade de serviço criada para executar o aplicativo. Se você não tiver uma entidade de serviço para o seu aplicativo, [crie uma com a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).
- chave: usar o valor da *senha* da saída da CLI de criação da entidade de serviço 
- locatário: usar o valor de *locatário* da saída da CLI de criação da entidade de serviço

Salve esse arquivo em um local seguro no sistema onde o seu código possa lê-lo. Defina uma variável de ambiente com o caminho completo para o arquivo no shell:

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Crie o objeto `Azure` do ponto de entrada para começar a trabalhar com as bibliotecas. Leia o local do arquivo de propriedades por meio da variável de ambiente.

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



