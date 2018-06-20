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
# <a name="authenticate-with-the-azure-libraries-for-java"></a><span data-ttu-id="c2b52-104">Autenticar com as bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="c2b52-104">Authenticate with the Azure libraries for Java</span></span> 

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="c2b52-105">Conectar-se aos serviços com cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="c2b52-105">Connect to services with connection strings</span></span>

<span data-ttu-id="c2b52-106">A maioria das bibliotecas de serviço do Azure usa uma cadeia de conexão ou a chave segura para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c2b52-106">Most Azure service libraries use a connection string or secure key for authentication.</span></span> <span data-ttu-id="c2b52-107">Por exemplo, o banco de dados SQL inclui informações de nome de usuário e senha na cadeia de conexão JDBC:</span><span class="sxs-lookup"><span data-stu-id="c2b52-107">For example, SQL Database includes username and password information in the JDBC connection string:</span></span>

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

<span data-ttu-id="c2b52-108">O Armazenamento do Azure usa uma chave de armazenamento para autorizar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c2b52-108">Azure Storage uses a storage key to authorize the application:</span></span>

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

<span data-ttu-id="c2b52-109">As cadeias de conexão de serviço são usadas para autenticar outros serviços do Azure como [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Cache Redis](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) e [Barramento de Serviço](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span><span class="sxs-lookup"><span data-stu-id="c2b52-109">Service connection strings are used to authenticate to other Azure services like [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started), and [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span></span> <span data-ttu-id="c2b52-110">Você pode obter as cadeias de conexão usando a CLI ou o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2b52-110">You can get the connection strings using the Azure portal or the CLI.</span></span>  <span data-ttu-id="c2b52-111">Você também pode usar as bibliotecas de gerenciamento do Azure para Java para consultar recursos para criar cadeias de conexão no seu código.</span><span class="sxs-lookup"><span data-stu-id="c2b52-111">You can also use the Azure management libraries for Java to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="c2b52-112">Por exemplo, esse código usa as bibliotecas de gerenciamento para criar uma cadeia de conexão da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="c2b52-112">For example, this code uses the management libraries to create a storage account connection string:</span></span>

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

<span data-ttu-id="c2b52-113">Outras bibliotecas exigem que o aplicativo seja executado com um [entidade de serviço](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) que autoriza o aplicativo a ser executado com as credenciais concedidas.</span><span class="sxs-lookup"><span data-stu-id="c2b52-113">Other libraries require your application to run with a [service prinicpal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="c2b52-114">Essa configuração é semelhante às etapas de autenticação baseada em objeto para a biblioteca de gerenciamento listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="c2b52-114">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a><span data-ttu-id="c2b52-115">Autenticar com as bibliotecas de gerenciamento do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="c2b52-115">Authenticate with the Azure management libraries for Java</span></span>

<span data-ttu-id="c2b52-116">Duas opções estão disponíveis para autenticar seu aplicativo com o Azure ao usar as bibliotecas de gerenciamento do Java para criar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="c2b52-116">Two options are available to authenticate your application with Azure when using the Java management libraries to create and manage resources.</span></span>

### <a name="authenticate-with-an-applicationtokencredentials-object"></a><span data-ttu-id="c2b52-117">Autenticar com um objeto ApplicationTokenCredentials</span><span class="sxs-lookup"><span data-stu-id="c2b52-117">Authenticate with an ApplicationTokenCredentials object</span></span>

<span data-ttu-id="c2b52-118">Crie uma instância de `ApplicationTokenCredentials` para fornecer as credenciais da entidade de serviço para o objeto `Azure` de nível superior de dentro do seu código.</span><span class="sxs-lookup"><span data-stu-id="c2b52-118">Create an instance of `ApplicationTokenCredentials` to supply the service principal credentials to the top-level `Azure` object from inside your code.</span></span>

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

<span data-ttu-id="c2b52-119">Os valores `client`, `tenant` e `key` são os mesmos valores de entidade de serviço usados na [autenticação baseada em arquivo](#mgmt-file).</span><span class="sxs-lookup"><span data-stu-id="c2b52-119">The `client`, `tenant` and `key` are the same service principal values used with [file-based authentication](#mgmt-file).</span></span> <span data-ttu-id="c2b52-120">O valor `AzureEnvironment.AZURE` cria as credenciais na nuvem pública do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2b52-120">The `AzureEnvironment.AZURE` value creates credentials against the Azure public cloud.</span></span> <span data-ttu-id="c2b52-121">Altere para um valor diferente se você precisar acessar outra nuvem (por exemplo, `AzureEnvironment.AZURE_GERMANY`).</span><span class="sxs-lookup"><span data-stu-id="c2b52-121">Change this to a different value if you need to access another cloud (for example, `AzureEnvironment.AZURE_GERMANY`).</span></span>  

 <span data-ttu-id="c2b52-122">Leia os valores da entidade de serviço de variáveis de ambiente ou de um repositório de gerenciamento de segredo como o [Cofre de Chaves](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="c2b52-122">Read the service principal values from environment variables or a secret management store like [Key Vault](/azure/key-vault/key-vault-whatis).</span></span> <span data-ttu-id="c2b52-123">Evite definir esses valores como cadeias de caracteres de texto não criptografado em seu código para evitar expor acidentalmente credenciais no seu histórico de controle de versão.</span><span class="sxs-lookup"><span data-stu-id="c2b52-123">Avoid setting these values as cleartext strings in your code to prevent accidentally exposing credentials in your version control history.</span></span>   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a><span data-ttu-id="c2b52-124">Autenticação baseada em arquivo (Visualização)</span><span class="sxs-lookup"><span data-stu-id="c2b52-124">File based authentication (Preview)</span></span>

<span data-ttu-id="c2b52-125">A maneira mais simples de autenticar é criar um arquivo de propriedades que contém as credenciais para uma [entidade de serviço do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) usando o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="c2b52-125">The simplest way to authenticate is to create a properties file that contains credentials for an [Azure service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) using the following format:</span></span>

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

- <span data-ttu-id="c2b52-126">assinatura: usar o valor *id* de `az account show` na CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="c2b52-126">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="c2b52-127">cliente: usar o valor *appId* da saída obtida de uma entidade de serviço criada para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2b52-127">client: use the *appId* value from the output taken from a service principal created to run the application.</span></span> <span data-ttu-id="c2b52-128">Se você não tiver uma entidade de serviço para o seu aplicativo, [crie uma com a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c2b52-128">If you don't have a service principal for your app, [create one with the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>
- <span data-ttu-id="c2b52-129">chave: usar o valor da *senha* da saída da CLI de criação da entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="c2b52-129">key: use the *password* value from the service principal create CLI output</span></span> 
- <span data-ttu-id="c2b52-130">locatário: usar o valor de *locatário* da saída da CLI de criação da entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="c2b52-130">tenant: use the *tenant* value from the service principal create CLI output</span></span>

<span data-ttu-id="c2b52-131">Salve esse arquivo em um local seguro no sistema onde o seu código possa lê-lo.</span><span class="sxs-lookup"><span data-stu-id="c2b52-131">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="c2b52-132">Defina uma variável de ambiente com o caminho completo para o arquivo no shell:</span><span class="sxs-lookup"><span data-stu-id="c2b52-132">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="c2b52-133">Crie o objeto `Azure` do ponto de entrada para começar a trabalhar com as bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="c2b52-133">Create the entry point `Azure` object to start working with the libraries.</span></span> <span data-ttu-id="c2b52-134">Leia o local do arquivo de propriedades por meio da variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="c2b52-134">Read the location of the properties file through the environment variable.</span></span>

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



