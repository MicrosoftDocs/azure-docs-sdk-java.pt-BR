---
title: Bibliotecas do Hub de Eventos do Azure para Java
description: Documentação de referência para as bibliotecas do Hub de Eventos para Java
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
ms.openlocfilehash: 076906ff3cafcb4eba97b0a022e5214d7834517c
ms.sourcegitcommit: 02b70b9f5d34415c337601f0b818f7e0985fd884
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
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
> [Explorar as APIs de cliente](/java/api/overview/azure/eventhub/client)


## <a name="samples"></a>Exemplos

[Gravar no Hub de Eventos por meio do JMS e ler do Apache Storm][1]
[Leitura e gravação de Hubs de Eventos usando uma topologia de .NET/Java híbrida][2] 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Explorar mais [exemplos de código Java para os Hubs de Eventos do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que você pode usar em seus aplicativos.

