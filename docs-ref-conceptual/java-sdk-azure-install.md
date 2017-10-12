---
title: Azure para desenvolvedores de Java Microsoft Docs
description: "Java SDK e referência da API para Azure"
keywords: "Java do Azure, referência de API de Java do Azure, biblioteca de classes Java do Azure, SDK do Azure"
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 28cefcfa6c86e233e15a780ec819e61bf91e0a72
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="fcfb9-104">Bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="fcfb9-104">Azure libraries for Java</span></span>

<span data-ttu-id="fcfb9-105">As bibliotecas do Azure o ajudam a consumir os serviços do Azure em seus aplicativos Java usando interfaces nativas.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-105">Azure libraries help you consume Azure services in your Java apps using native interfaces.</span></span> <span data-ttu-id="fcfb9-106">Cada biblioteca é independente e pode ser usada separadamente das outras.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-106">Each library is independent and can be used separately from the others another.</span></span>

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [<span data-ttu-id="fcfb9-107">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfb9-107">Azure Storage</span></span>](#azure-storage) | [<span data-ttu-id="fcfb9-108">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="fcfb9-108">SQL Database</span></span>](#sql-database)  | [<span data-ttu-id="fcfb9-109">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="fcfb9-109">Redis Cache</span></span>](#redis-cache)   | [<span data-ttu-id="fcfb9-110">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="fcfb9-110">DocumentDB</span></span>](#documentdb) |
| [<span data-ttu-id="fcfb9-111">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="fcfb9-111">Service Bus</span></span>](#servicebus)  | [<span data-ttu-id="fcfb9-112">Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfb9-112">Azure Active Directory</span></span>](#azuread) | [<span data-ttu-id="fcfb9-113">Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="fcfb9-113">Key Vault</span></span>](#keyvault)  | [<span data-ttu-id="fcfb9-114">Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="fcfb9-114">Event Hub</span></span>](#eventhub)
| [<span data-ttu-id="fcfb9-115">Serviço de IoT</span><span class="sxs-lookup"><span data-stu-id="fcfb9-115">IoT Service</span></span>](#iotservice) | [<span data-ttu-id="fcfb9-116">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="fcfb9-116">IoT Device</span></span>](#iotdevice) | [<span data-ttu-id="fcfb9-117">Data Lake</span><span class="sxs-lookup"><span data-stu-id="fcfb9-117">Data Lake</span></span>](#datalake)  | [<span data-ttu-id="fcfb9-118">AppInsights</span><span class="sxs-lookup"><span data-stu-id="fcfb9-118">AppInsights</span></span>](#appinsights) | 
| [<span data-ttu-id="fcfb9-119">Batch</span><span class="sxs-lookup"><span data-stu-id="fcfb9-119">Batch</span></span>](#batch) | [<span data-ttu-id="fcfb9-120">Gerenciar recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfb9-120">Manage Azure resources</span></span>](#management) |

## <a name="install-with-maven"></a><span data-ttu-id="fcfb9-121">Instalar com o Maven</span><span class="sxs-lookup"><span data-stu-id="fcfb9-121">Install with Maven</span></span>

<span data-ttu-id="fcfb9-122">Adicionar uma entrada de dependência em seu `pom.xml` para importar uma biblioteca para o seu projeto [Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="fcfb9-122">Add a dependency entry in your `pom.xml` to import a library into your [Maven](https://maven.apache.org) project.</span></span>

<span data-ttu-id="fcfb9-123">Por exemplo, para incluir a versão mais recente das [bibliotecas de gerenciamento do Azure para Java](#management):</span><span class="sxs-lookup"><span data-stu-id="fcfb9-123">For example, to include the latest version of the [Azure management libraries for Java](#management):</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="fcfb9-124">Outras ferramentas de compilação de Java como Gradle têm suporte, mas as etapas de instalação não são fornecidas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-124">Other Java build tools like Gradle are supported but the install steps are not provided in this article.</span></span> <span data-ttu-id="fcfb9-125">Leia a documentação para sua ferramenta de compilação para saber como consumir importações Maven.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-125">Review the documentation for your build tool on how to consume Maven imports.</span></span>

## <a name="azure-service-libraries"></a><span data-ttu-id="fcfb9-126">Bibliotecas de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfb9-126">Azure service libraries</span></span>

<span data-ttu-id="fcfb9-127">Integrar serviços do Azure para adicionar funcionalidade aos seus aplicativos usando essas bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-127">Integrate Azure services to add functionality to your apps using these libraries.</span></span> <span data-ttu-id="fcfb9-128">Saiba mais sobre como criar aplicativos com serviços do Azure na [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java).</span><span class="sxs-lookup"><span data-stu-id="fcfb9-128">Learn more about building apps with Azure services at the [Java developer center](https://azure.microsoft.com/develop/java).</span></span>

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[<span data-ttu-id="fcfb9-129">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfb9-129">Azure Storage</span></span>](/azure/storage/storage-introduction)  

<span data-ttu-id="fcfb9-130">Armazenamento de dados e sistema de mensagens para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-130">Data storage and messaging for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

<span data-ttu-id="fcfb9-131">[Exemplos](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Referência](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Notas de versão](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-131">[Samples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Reference](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Release Notes](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span></span>

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[<span data-ttu-id="fcfb9-132">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="fcfb9-132">SQL Database</span></span>](/azure/sql-database/sql-database-technical-overview)

<span data-ttu-id="fcfb9-133">Driver JDBC para o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-133">JDBC driver for Azure SQL Database.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="fcfb9-134">[Exemplos](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Referência](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Notas de versão](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-134">[Samples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Reference](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Release Notes](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span></span>

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[<span data-ttu-id="fcfb9-135">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="fcfb9-135">Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)

<span data-ttu-id="fcfb9-136">Repositório de chave-valor de baixa latência e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-136">Low-latency, high-performance key-value store.</span></span>

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

<span data-ttu-id="fcfb9-137">[Exemplos](/azure/redis-cache/cache-java-get-started) | [Referência](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Notas de versão](https://github.com/xetorthio/jedis/releases)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-137">[Samples](/azure/redis-cache/cache-java-get-started) | [Reference](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Release Notes](https://github.com/xetorthio/jedis/releases)</span></span>  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[<span data-ttu-id="fcfb9-138">Banco de Dados Cosmos</span><span class="sxs-lookup"><span data-stu-id="fcfb9-138">Cosmos DB</span></span>](/azure/documentdb/documentdb-introduction)

<span data-ttu-id="fcfb9-139">Banco de dados NoSQL escalonável com documentos JSON e uma sintaxe de consulta SQL ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-139">Scalable NoSQL database with JSON documents and a SQL or JavaScript query syntax.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

<span data-ttu-id="fcfb9-140">[Exemplos](/azure/documentdb/documentdb-java-application) | [Referência](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Notas de versão](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-140">[Samples](/azure/documentdb/documentdb-java-application) | [Reference](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Release Notes](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span></span>

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="fcfb9-141">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="fcfb9-141">ServiceBus</span></span>](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 <span data-ttu-id="fcfb9-142">Barramento de Serviço é um serviço de plataforma de mensagens transacionais, de classe empresarial.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-142">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 <span data-ttu-id="fcfb9-143">[Exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referência](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notas de versão](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-143">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[<span data-ttu-id="fcfb9-144">Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfb9-144">Azure Active Directory</span></span>](/azure/active-directory/active-directory-whatis)   

<span data-ttu-id="fcfb9-145">Gerenciamento de identidade e logon seguro em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-145">Identity management and secure sign-in for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
<span data-ttu-id="fcfb9-146">[Exemplos](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Referência](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Notas de versão](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-146">[Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Reference](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Release Notes](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span></span>
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[<span data-ttu-id="fcfb9-147">Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="fcfb9-147">Key Vault</span></span>](/azure/key-vault) 

<span data-ttu-id="fcfb9-148">Acessar com segurança as chaves e segredos de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-148">Safely access keys and secrets from your applications.</span></span> 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

<span data-ttu-id="fcfb9-149">[Exemplos](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Referência](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Notas de versão](https://github.com/Azure/azure-keyvault-java)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-149">[Samples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Reference](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Release Notes](https://github.com/Azure/azure-keyvault-java)</span></span> 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[<span data-ttu-id="fcfb9-150">Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="fcfb9-150">Event Hub</span></span>](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
<span data-ttu-id="fcfb9-151">Eventos de alta taxa de transferência e tratamento de telemetria para seus cenários de IoT ou instrumentação.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-151">High-throughput event and telemetry handling for your instrumentation or IoT scenarios.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

<span data-ttu-id="fcfb9-152">[Exemplos](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Referência](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Notas de versão](https://github.com/Azure/azure-event-hubs-java)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-152">[Samples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Reference](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Release Notes](https://github.com/Azure/azure-event-hubs-java)</span></span>

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[<span data-ttu-id="fcfb9-153">Serviço de IoT</span><span class="sxs-lookup"><span data-stu-id="fcfb9-153">IoT Service</span></span>](/azure/iot-hub/)

<span data-ttu-id="fcfb9-154">Gerenciar identidades, enviar mensagens e obter feedback de dispositivos registrados com o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-154">Manage identities, send messages, and get feedback from devices registered with your IoT hub.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
<span data-ttu-id="fcfb9-155">[Exemplos](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Referência](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notas de versão](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-155">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[<span data-ttu-id="fcfb9-156">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="fcfb9-156">IoT Device</span></span>](/azure/iot-hub/iot-hub-devguide)

<span data-ttu-id="fcfb9-157">Enviar uma mensagem para um hub IoT do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-157">Send a message to an IoT hub from your device.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

<span data-ttu-id="fcfb9-158">[Exemplos](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Referência](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notas de versão](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-158">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[<span data-ttu-id="fcfb9-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fcfb9-159">Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)   
   
<span data-ttu-id="fcfb9-160">Capturar dados de qualquer tamanho e forma em um único local para executar a análise.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-160">Capture data of any size and shape into a single location for performing analytics.</span></span>    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

<span data-ttu-id="fcfb9-161">[Exemplos](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Referência](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Notas de versão](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-161">[Samples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Reference](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Release Notes](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span></span>

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[<span data-ttu-id="fcfb9-162">AppInsights</span><span class="sxs-lookup"><span data-stu-id="fcfb9-162">AppInsights</span></span>](/azure/application-insights/app-insights-overview)

<span data-ttu-id="fcfb9-163">Controlar o uso, adicionar telemetria e monitorar seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-163">Track usage, add telemetry, and monitor your web apps.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

<span data-ttu-id="fcfb9-164">[Exemplos](/azure/application-insights/app-insights-java-get-started) | [Referência](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Notas de versão](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-164">[Samples](/azure/application-insights/app-insights-java-get-started) | [Reference](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Release Notes](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span></span>

<a name="batch"></a>

### <a name="batchazurebatch"></a>[<span data-ttu-id="fcfb9-165">Batch</span><span class="sxs-lookup"><span data-stu-id="fcfb9-165">Batch</span></span>](/azure/batch)

<span data-ttu-id="fcfb9-166">Executar aplicativos paralelos em grande escala e aplicativos de computação de alto desempenho com eficiência na nuvem.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-166">Run large-scale parallel and high-performance computing applications efficiently in the cloud.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

<span data-ttu-id="fcfb9-167">[Exemplos](https://github.com/azure/azure-batch-samples) | [Referência](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Notas de versão](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-167">[Samples](https://github.com/azure/azure-batch-samples) | [Reference](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Release Notes](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span></span>

<a name="management"></a> 

## <a name="manage-azure-resources"></a><span data-ttu-id="fcfb9-168">Gerenciar recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="fcfb9-168">Manage Azure resources</span></span>

<span data-ttu-id="fcfb9-169">Criar, atualizar e excluir recursos do Azure do seu código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-169">Create, update, and delete Azure resources from your application code.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="fcfb9-170">[Exemplos](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Referência](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Notas de versão](java-sdk-azure-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-170">[Samples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Reference](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Release Notes](java-sdk-azure-release-notes.md)</span></span>

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomen-usazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="fcfb9-171">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="fcfb9-171">ServiceBus</span></span>](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) 
   
<span data-ttu-id="fcfb9-172">Barramento de Serviço é um serviço de plataforma de mensagens transacionais, de classe empresarial.</span><span class="sxs-lookup"><span data-stu-id="fcfb9-172">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

<span data-ttu-id="fcfb9-173">[Exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referência](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notas de versão](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="fcfb9-173">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>

