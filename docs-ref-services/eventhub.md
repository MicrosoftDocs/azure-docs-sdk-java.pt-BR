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
ms.openlocfilehash: 9e2ae18f98083cb35bb076a5f84726b669cbf81e
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593351"
---
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="b0052-104">Bibliotecas do Hub de Eventos do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="b0052-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="b0052-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b0052-105">Overview</span></span>

<span data-ttu-id="b0052-106">Coletar e gerenciar milhões de eventos por segundo de aplicativos e dispositivos IoT conectados com os [Hubs de Eventos do Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="b0052-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="b0052-107">Para começar a usar os Hubs de Eventos do Azure, consulte [Receber eventos de Hubs de Eventos do Azure usando o Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="b0052-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="b0052-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="b0052-108">Client library</span></span>

<span data-ttu-id="b0052-109">Enviar eventos para um Hub de Eventos do Azure e consumir e processar eventos de um Hub de Eventos usando a biblioteca de cliente de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="b0052-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="b0052-110">[Adicione uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a [biblioteca de clientes](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b0052-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the [client library](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) in your project.</span></span>
 

## <a name="example"></a><span data-ttu-id="b0052-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b0052-111">Example</span></span>

<span data-ttu-id="b0052-112">Enviar um evento para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="b0052-112">Send an event to an event hub.</span></span>

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
> [<span data-ttu-id="b0052-113">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="b0052-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a><span data-ttu-id="b0052-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b0052-114">Samples</span></span>

<span data-ttu-id="b0052-115">[Explorar a API do plano de dados do Hub de Eventos usando exemplos][1]</span><span class="sxs-lookup"><span data-stu-id="b0052-115">[Explore Event Hub data-plane API using samples][1]</span></span>

<span data-ttu-id="b0052-116">[Gravar no Hub de Eventos por meio do JMS ler a partir do Apache Storm][2]</span><span class="sxs-lookup"><span data-stu-id="b0052-116">[Write to Event Hub via JMS and read from Apache Storm][2]</span></span>

<span data-ttu-id="b0052-117">[Ler e gravar a partir dos Hubs de Eventos usando uma topologia .NET/Java híbrida][3]</span><span class="sxs-lookup"><span data-stu-id="b0052-117">[Read and write from EventHubs using a hybrid .NET/Java topology][3]</span></span> 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="b0052-118">Explorar mais [exemplos de código Java para os Hubs de Eventos do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b0052-118">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

