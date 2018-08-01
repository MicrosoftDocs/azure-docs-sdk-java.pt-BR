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
ms.openlocfilehash: b6646ef27edace4247090e749c9a52cd6a33a82c
ms.sourcegitcommit: 3d3460289ab6b9165c2cf6a3dd56eafd0692501e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34283020"
---
# <a name="azure-event-hub-libraries-for-java"></a>Bibliotecas do Hub de Eventos do Azure para Java

## <a name="overview"></a>Visão geral

Coletar e gerenciar milhões de eventos por segundo de aplicativos e dispositivos IoT conectados com os [Hubs de Eventos do Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).

Para começar a usar os Hubs de Eventos do Azure, consulte [Receber eventos de Hubs de Eventos do Azure usando o Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Biblioteca do cliente

Enviar eventos para um Hub de Eventos do Azure e consumir e processar eventos de um Hub de Eventos usando a biblioteca de cliente de Hubs de Eventos.

[Adicione uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a [biblioteca de clientes](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) em seu projeto.
 

## <a name="example"></a>Exemplo

Enviar um evento para um hub de eventos.

```java
final ConnectionStringBuilder connStr = new ConnectionStringBuilder()
                                            .setNamespaceName(namespaceName)
                                            .setEventHubName(eventHubName)
                                            .setSasKeyName(sasKeyName)
                                            .setSasKey(sasKey);
final EventHubClient ehClient = EventHubClient.createSync(connStr.toString());

final byte[] payloadBytes = "Test AMQP message".getBytes("UTF-8");
final EventData sendEvent = new EventData(payloadBytes);

ehClient.sendSync(sendEvent);
```


> [!div class="nextstepaction"]
> [Explorar as APIs de cliente](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a>Exemplos

[Explorar a API do plano de dados do Hub de Eventos usando exemplos][1]

[Gravar no Hub de Eventos por meio do JMS ler a partir do Apache Storm][2]

[Ler e gravar a partir dos Hubs de Eventos usando uma topologia .NET/Java híbrida][3] 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Explorar mais [exemplos de código Java para os Hubs de Eventos do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que você pode usar em seus aplicativos.

