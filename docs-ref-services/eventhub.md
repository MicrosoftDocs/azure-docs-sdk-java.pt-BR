---
title: Bibliotecas do Hub de Eventos do Azure para Java
description: "Documentação de referência para as bibliotecas do Hub de Eventos para Java"
keywords: Azure, Java, SDK, API, hub de eventos, IoT, processamento de fluxo
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: event-hub
ms.openlocfilehash: 8e5b032624862ffbef18c718abf4fa29359b3e67
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-event-hub-libraries-for-java"></a>Bibliotecas do Hub de Eventos do Azure para Java

## <a name="overview"></a>Visão geral

Coletar e gerenciar milhões de eventos por segundo de aplicativos e dispositivos IoT conectados com os [Hubs de Eventos do Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).

Para começar a usar os Hubs de Eventos do Azure, consulte [Receber eventos de Hubs de Eventos do Azure usando o Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Biblioteca do cliente

Enviar eventos para um Hub de Eventos do Azure e consumir e processar eventos de um Hub de Eventos usando a biblioteca de cliente de Hubs de Eventos.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a>Exemplo

Enviar um evento para um hub de eventos.

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [Explorar as APIs de Cliente](/java/api/overview/azure/eventhub/clientlibrary)


## <a name="samples"></a>Exemplos

[Gravar no Hub de Eventos por meio do JMS e ler do Apache Storm][1]
[Leitura e gravação de Hubs de Eventos usando uma topologia de .NET/Java híbrida][2] 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Explorar mais [exemplos de código Java para os Hubs de Eventos do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que você pode usar em seus aplicativos.

