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
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="56d9d-104">Bibliotecas do Hub de Eventos do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="56d9d-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="56d9d-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="56d9d-105">Overview</span></span>

<span data-ttu-id="56d9d-106">Coletar e gerenciar milhões de eventos por segundo de aplicativos e dispositivos IoT conectados com os [Hubs de Eventos do Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="56d9d-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="56d9d-107">Para começar a usar os Hubs de Eventos do Azure, consulte [Receber eventos de Hubs de Eventos do Azure usando o Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="56d9d-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="56d9d-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="56d9d-108">Client library</span></span>

<span data-ttu-id="56d9d-109">Enviar eventos para um Hub de Eventos do Azure e consumir e processar eventos de um Hub de Eventos usando a biblioteca de cliente de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="56d9d-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="56d9d-110">[Adicione uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a [biblioteca de clientes](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="56d9d-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the [client library](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) in your project.</span></span>
 

## <a name="example"></a><span data-ttu-id="56d9d-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="56d9d-111">Example</span></span>

<span data-ttu-id="56d9d-112">Enviar um evento para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="56d9d-112">Send an event to an event hub.</span></span>

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
> [<span data-ttu-id="56d9d-113">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="56d9d-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a><span data-ttu-id="56d9d-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="56d9d-114">Samples</span></span>

<span data-ttu-id="56d9d-115">[Explorar a API do plano de dados do Hub de Eventos usando exemplos][1]</span><span class="sxs-lookup"><span data-stu-id="56d9d-115">[Explore Event Hub data-plane API using samples][1]</span></span>

<span data-ttu-id="56d9d-116">[Gravar no Hub de Eventos por meio do JMS ler a partir do Apache Storm][2]</span><span class="sxs-lookup"><span data-stu-id="56d9d-116">[Write to Event Hub via JMS and read from Apache Storm][2]</span></span>

<span data-ttu-id="56d9d-117">[Ler e gravar a partir dos Hubs de Eventos usando uma topologia .NET/Java híbrida][3]</span><span class="sxs-lookup"><span data-stu-id="56d9d-117">[Read and write from EventHubs using a hybrid .NET/Java topology][3]</span></span> 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="56d9d-118">Explorar mais [exemplos de código Java para os Hubs de Eventos do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="56d9d-118">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

