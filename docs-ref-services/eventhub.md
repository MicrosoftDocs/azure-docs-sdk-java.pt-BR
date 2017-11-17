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
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="9ce36-104">Bibliotecas do Hub de Eventos do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="9ce36-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="9ce36-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9ce36-105">Overview</span></span>

<span data-ttu-id="9ce36-106">Coletar e gerenciar milhões de eventos por segundo de aplicativos e dispositivos IoT conectados com os [Hubs de Eventos do Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="9ce36-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="9ce36-107">Para começar a usar os Hubs de Eventos do Azure, consulte [Receber eventos de Hubs de Eventos do Azure usando o Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="9ce36-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="9ce36-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="9ce36-108">Client library</span></span>

<span data-ttu-id="9ce36-109">Enviar eventos para um Hub de Eventos do Azure e consumir e processar eventos de um Hub de Eventos usando a biblioteca de cliente de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="9ce36-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="9ce36-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="9ce36-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="9ce36-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9ce36-111">Example</span></span>

<span data-ttu-id="9ce36-112">Enviar um evento para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="9ce36-112">Send an event to an event hub.</span></span>

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ce36-113">Explorar as APIs de Cliente</span><span class="sxs-lookup"><span data-stu-id="9ce36-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhub/clientlibrary)


## <a name="samples"></a><span data-ttu-id="9ce36-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="9ce36-114">Samples</span></span>

<span data-ttu-id="9ce36-115">[Gravar no Hub de Eventos por meio do JMS e ler do Apache Storm][1]
[Leitura e gravação de Hubs de Eventos usando uma topologia de .NET/Java híbrida][2]</span><span class="sxs-lookup"><span data-stu-id="9ce36-115">[Write to Event Hub via JMS and read from Apache Storm][1]
[Read and write from EventHubs using a hybrid .NET/Java topology][2]</span></span> 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="9ce36-116">Explorar mais [exemplos de código Java para os Hubs de Eventos do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9ce36-116">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

