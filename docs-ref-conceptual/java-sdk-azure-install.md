---
title: Azure para desenvolvedores de Java Microsoft Docs
description: Java SDK e referência da API para Azure
keywords: Java do Azure, referência de API de Java do Azure, biblioteca de classes Java do Azure, SDK do Azure
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 5c8bb4b81080461285551573eefc0d76b47b2d3d
ms.sourcegitcommit: 61030d025614b084e897809e603b2ec79900ec8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
ms.locfileid: "30302544"
---
# <a name="azure-libraries-for-java"></a>Bibliotecas do Azure para Java

As bibliotecas do Azure o ajudam a consumir os serviços do Azure em seus aplicativos Java usando interfaces nativas. Cada biblioteca é independente e pode ser usada separadamente das outras.

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [Armazenamento do Azure](#azure-storage) | [Banco de Dados SQL](#sql-database)  | [Cache Redis](#redis-cache)   | [Azure Cosmos DB](#cosmos-db) |
| [Barramento de Serviço](#servicebus)  | [Azure Active Directory](#azuread) | [Key Vault](#keyvault)  | [Hub de Evento](#eventhub)
| [Serviço de IoT](#iotservice) | [Dispositivo IoT](#iotdevice) | [Data Lake](#datalake)  | [AppInsights](#appinsights) | 
| [Batch](#batch) | [Gerenciar recursos do Azure](#management) |

## <a name="install-with-maven"></a>Instalar com o Maven

Adicionar uma entrada de dependência em seu `pom.xml` para importar uma biblioteca para o seu projeto [Maven](https://maven.apache.org).

Por exemplo, para incluir a versão mais recente das [bibliotecas de gerenciamento do Azure para Java](#management):

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

Outras ferramentas de compilação de Java como Gradle têm suporte, mas as etapas de instalação não são fornecidas neste artigo. Leia a documentação para sua ferramenta de compilação para saber como consumir importações Maven.

## <a name="azure-service-libraries"></a>Bibliotecas de serviço do Azure

Integrar serviços do Azure para adicionar funcionalidade aos seus aplicativos usando essas bibliotecas. Saiba mais sobre como criar aplicativos com serviços do Azure na [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java).

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[Armazenamento do Azure](/azure/storage/storage-introduction)  

Armazenamento de dados e sistema de mensagens para seus aplicativos.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

[Exemplos](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Referência](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Notas de versão](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[Banco de Dados SQL](/azure/sql-database/sql-database-technical-overview)

Driver JDBC para o Banco de Dados SQL do Azure.

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

[Exemplos](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Referência](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Notas de versão](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[Cache Redis](https://azure.microsoft.com/services/cache/)

Repositório de chave-valor de baixa latência e de alto desempenho.

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

[Exemplos](/azure/redis-cache/cache-java-get-started) | [Referência](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Notas de versão](https://github.com/xetorthio/jedis/releases)  

<a name="cosmos-db"></a>

### <a name="azure-cosmos-dbazurecosmos-dbintroduction"></a>[Azure Cosmos DB](/azure/cosmos-db/introduction)

Banco de dados NoSQL escalonável com documentos JSON e uma sintaxe de consulta SQL ou JavaScript.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

[Exemplos](/azure/cosmos-db/sql-api-java-application) | [Referência](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Notas de versão](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[Barramento de Serviço](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 Barramento de Serviço é um serviço de plataforma de mensagens transacionais, de classe empresarial.
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 [Exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referência](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notas de versão](https://github.com/Azure/azure-service-bus-java)   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[Azure Active Directory](/azure/active-directory/active-directory-whatis)   

Gerenciamento de identidade e logon seguro em seus aplicativos.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
[Exemplos](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Referência](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Notas de versão](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[Key Vault](/azure/key-vault) 

Acessar com segurança as chaves e segredos de seus aplicativos. 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

[Exemplos](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Referência](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Notas de versão](https://github.com/Azure/azure-keyvault-java) 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[Hub de Evento](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
Eventos de alta taxa de transferência e tratamento de telemetria para seus cenários de IoT ou instrumentação.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

[Exemplos](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Referência](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Notas de versão](https://github.com/Azure/azure-event-hubs-java)

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[Serviço de IoT](/azure/iot-hub/)

Gerenciar identidades, enviar mensagens e obter feedback de dispositivos registrados com o hub IoT.

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
[Exemplos](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Referência](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notas de versão](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[Dispositivo IoT](/azure/iot-hub/iot-hub-devguide)

Enviar uma mensagem para um hub IoT do seu dispositivo.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

[Exemplos](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Referência](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notas de versão](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[Data Lake Store](/azure/data-lake-store/data-lake-store-overview)   
   
Capturar dados de qualquer tamanho e forma em um único local para executar a análise.    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

[Exemplos](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Referência](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Notas de versão](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[AppInsights](/azure/application-insights/app-insights-overview)

Controlar o uso, adicionar telemetria e monitorar seus aplicativos Web.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

[Exemplos](/azure/application-insights/app-insights-java-get-started) | [Referência](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Notas de versão](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)

<a name="batch"></a>

### <a name="batchazurebatch"></a>[Batch](/azure/batch)

Executar aplicativos paralelos em grande escala e aplicativos de computação de alto desempenho com eficiência na nuvem.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

[Exemplos](https://github.com/azure/azure-batch-samples) | [Referência](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Notas de versão](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)

<a name="management"></a> 

## <a name="manage-azure-resources"></a>Gerenciar recursos do Azure

Criar, atualizar e excluir recursos do Azure do seu código do aplicativo.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

[Exemplos](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Referência](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Notas de versão](java-sdk-azure-release-notes.md)

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[Barramento de Serviço](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
Barramento de Serviço é um serviço de plataforma de mensagens transacionais, de classe empresarial.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

[Exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Referência](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notas de versão](https://github.com/Azure/azure-service-bus-java)

