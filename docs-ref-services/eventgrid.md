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
# <a name="azure-event-grid-libraries-for-java"></a>Bibliotecas da Grade de Eventos do Azure para Java

Crie aplicativos orientados para eventos que escutam e reagem a eventos de serviços do Azure e fontes personalizadas usando a manipulação de eventos simples com base em HTTP com a Grade de Eventos do Azure.

[Saiba mais](/azure/event-grid/overview) sobre a Grade de Eventos do Azure e começar a usar o [tutorial de eventos do armazenamento de Blobs do Azure](/azure/storage/blobs/storage-blob-event-quickstart). 

## <a name="client-sdk"></a>SDK do cliente

Crie eventos, autentique e publique tópicos usando o SDK do cliente da Grade de Eventos do Azure.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a>Publicar eventos

O código a seguir autentica com o Azure e publica uma `List` de eventos `EventGridEvent` de um tipo personalizado (neste exemplo, `Contoso.Items.ItemsReceived`) para um tópico. O tópico-chave e o endereço de ponto de extremidade usados no exemplo podem ser recuperados do CLI do Azure:

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
> [Explorar as APIs de cliente da Grade de Eventos](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>SDK de Gerenciamento

Criar, atualizar ou excluir instâncias da Grade de Eventos, tópicos e assinaturas com o SDK de gerenciamento da Grade de Eventos.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

O exemplo a seguir cria uma assinatura de Grade de Eventos, tirada das [amostras EventGrid Java](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)

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
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/eventgrid/management)