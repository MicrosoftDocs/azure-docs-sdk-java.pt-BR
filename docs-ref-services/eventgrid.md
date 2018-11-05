---
title: Bibliotecas da Grade de Eventos do Azure para Java
description: Documentação de referência para as bibliotecas da Grade de Eventos do Azure para Java
keywords: Azure, Java, SDK, API, grade de eventos, mensagens, controlado por evento
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 07/11/2017
ms.topic: managed-reference
ms.devlang: java
ms.service: event-grid
ms.openlocfilehash: 35acbdeede2fbc541128029ad43f149209a057c4
ms.sourcegitcommit: db36eeb667a0bfe6d113953bb0583240db61b0f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50134621"
---
# <a name="azure-event-grid-libraries-for-java"></a><span data-ttu-id="0d02c-104">Bibliotecas da Grade de Eventos do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="0d02c-104">Azure Event Grid libraries for Java</span></span>

<span data-ttu-id="0d02c-105">Crie aplicativos orientados para eventos que escutam e reagem a eventos de serviços do Azure e fontes personalizadas usando a manipulação de eventos simples com base em HTTP com a Grade de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d02c-105">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="0d02c-106">[Saiba mais](/azure/event-grid/overview) sobre a Grade de Eventos do Azure e começar a usar o [tutorial de eventos do armazenamento de Blobs do Azure](/azure/storage/blobs/storage-blob-event-quickstart).</span><span class="sxs-lookup"><span data-stu-id="0d02c-106">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="0d02c-107">SDK do cliente</span><span class="sxs-lookup"><span data-stu-id="0d02c-107">Client SDK</span></span>

<span data-ttu-id="0d02c-108">Crie eventos, autentique e publique tópicos usando o SDK do cliente da Grade de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d02c-108">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="0d02c-109">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="0d02c-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a><span data-ttu-id="0d02c-110">Publicar eventos</span><span class="sxs-lookup"><span data-stu-id="0d02c-110">Publish events</span></span>

<span data-ttu-id="0d02c-111">O código a seguir autentica com o Azure e publica uma `List` de eventos `EventGridEvent` de um tipo personalizado (neste exemplo, `Contoso.Items.ItemsReceived`) para um tópico.</span><span class="sxs-lookup"><span data-stu-id="0d02c-111">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceived` ) to a topic.</span></span> <span data-ttu-id="0d02c-112">O tópico-chave e o endereço de ponto de extremidade usados no exemplo podem ser recuperados do CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="0d02c-112">The topic key and endpoint address used in the sample can be retrieved from the Azure CLI:</span></span>

```azurecli-interactive
az eventgrid topic show -g gridResourceGroup -n topicName
az eventgrid topic key list -g gridResourceGroup -n topicName
```

```java
// Create an event grid client.
TopicCredentials topicCredentials = new TopicCredentials(System.getenv("EVENTGRID_TOPIC_KEY"));
EventGridClient client = new EventGridClientImpl(topicCredentials);

// Publish custom events to the EventGrid.
System.out.println("Publish custom events to the EventGrid");
List<EventGridEvent> eventsList = new ArrayList<>();
for (int i = 0; i < 5; i++) {
    eventsList.add(new EventGridEvent(
        UUID.randomUUID().toString(),
        String.format("Door%d", i),
        new ContosoItemReceivedEventData("Contoso Item SKU #1"),
        "Contoso.Items.ItemReceived",
        DateTime.now(),
        "2.0"
    ));
}

String eventGridEndpoint = String.format("https://%s/", new URI(System.getenv("EVENTGRID_TOPIC_ENDPOINT")).getHost());

client.publishEvents(eventGridEndpoint, eventsList);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d02c-113">Explorar as APIs de cliente da Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="0d02c-113">Explore the Event Grid Client APIs</span></span>](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="0d02c-114">SDK de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0d02c-114">Management SDK</span></span>

<span data-ttu-id="0d02c-115">Criar, atualizar ou excluir instâncias da Grade de Eventos, tópicos e assinaturas com o SDK de gerenciamento da Grade de Eventos.</span><span class="sxs-lookup"><span data-stu-id="0d02c-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the Event Grid management SDK.</span></span>

<span data-ttu-id="0d02c-116">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="0d02c-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

<span data-ttu-id="0d02c-117">O exemplo a seguir cria uma assinatura de Grade de Eventos, tirada das [amostras EventGrid Java](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span><span class="sxs-lookup"><span data-stu-id="0d02c-117">The following example creates an Event Grid subscription, taken from the [EventGrid Java samples](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span></span>

```java
// Create an event grid subscription.
//
System.out.println("Creating an Azure EventGrid Subscription");

EventSubscription eventSubscription = eventGridManager.eventSubscriptions().define(eventSubscriptionName)
    .withScope(eventGridTopic.id())
    .withDestination(new EventHubEventSubscriptionDestination()
        .withResourceId(eventHub.id()))
    .withFilter(new EventSubscriptionFilter()
        .withIsSubjectCaseSensitive(false)
        .withSubjectBeginsWith("")
        .withSubjectEndsWith(""))
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d02c-118">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0d02c-118">Explore the management APIs</span></span>](/java/api/overview/azure/eventgrid/management)