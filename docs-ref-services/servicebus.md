---
title: "Bibliotecas de Barramento de Serviço para Java"
description: "Documentação de referência para as bibliotecas de gerenciamento e de cliente de Java para Barramento de Serviço"
keywords: Azure, Java, SDK, API, sistema de mensagens, amqp, qpid, JMS, pubsub, pub-sub, agente de mensagens
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: service-bus
ms.openlocfilehash: f7c2b1fd35fbb9dbdc782577c3464b7a38977254
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2017
---
# <a name="service-bus-libraries-for-java"></a><span data-ttu-id="7074a-104">Bibliotecas de Barramento de Serviço para Java</span><span class="sxs-lookup"><span data-stu-id="7074a-104">Service Bus libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="7074a-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7074a-105">Overview</span></span>

<span data-ttu-id="7074a-106">Barramento de Serviço é um serviço de plataforma de sistema de mensagens transacionais, de classe empresarial que fornece tópicos de publicação/assinatura e filas altamente confiáveis com recursos de grande capacidade como entrega ordenada, sessões, particionamento, agendamento, assinaturas complexas, bem como o tratamento de fluxos de trabalho e transações.</span><span class="sxs-lookup"><span data-stu-id="7074a-106">Service Bus is an enterprise-class, transactional messaging platform service that provides highly reliable queues and publish/subscribe topics with deep feature capabilities such as ordered delivery, sessions, partitioning, scheduling, complex subscriptions, as well as workflow and transaction handling.</span></span>

<span data-ttu-id="7074a-107">Os recursos do Barramento de Serviço são comparáveis e geralmente excedem aqueles dos sofisticados agentes de mensagens herdados locais.</span><span class="sxs-lookup"><span data-stu-id="7074a-107">The Service Bus feature capabilities are comparable and often exceed those of high-end, on-premises legacy message brokers.</span></span> <span data-ttu-id="7074a-108">Os recursos do Barramento de Serviço estão disponíveis por meio de protocolos baseados em padrões, como AMQP 1.0 e HTTPS e todos os gestos de protocolo são totalmente documentados, permitindo uma ampla interoperabilidade.</span><span class="sxs-lookup"><span data-stu-id="7074a-108">The Service Bus features are available via standards-based protocols like AMQP 1.0 and HTTPS and all protocol gestures are fully documented, allowing for broad interoperability.</span></span> 

<span data-ttu-id="7074a-109">Focado em um sistema de mensagens duráveis confiáveis e de alta disponibilidade, o tipo de Barramento de Serviço Premium oferece desempenho de taxa de transferência competitiva mesmo com implantações de datacenter local significativas, mas sem a seleção de hardware e processos de aquisição, execução e planejamento de implantação e sessões de otimização de desempenho que não acabam nunca.</span><span class="sxs-lookup"><span data-stu-id="7074a-109">Focusing on highly available and reliable durable messaging, the Service Bus Premium provides competitive throughput performance even with substantial local datacenter deployments, but without hardware selection and acquisition processes, deployment planning and execution, and endless performance optimization sessions.</span></span> 

<span data-ttu-id="7074a-110">O Barramento de Serviço Premium é uma oferta totalmente gerenciada com capacidade dedicada reservada para cada locatário que gera um desempenho previsível com um modelo de preço simples e orientado à capacidade e a um custo geral muito menor do que os agentes comerciais locais.</span><span class="sxs-lookup"><span data-stu-id="7074a-110">Service Bus Premium is a fully managed offering with dedicated capacity reserved for each tenant that yields predictable performance with a simple, capacity-oriented pricing model and at extremely lower overall cost than commercial on-premises brokers.</span></span> <span data-ttu-id="7074a-111">Para muitos clientes, o Barramento de Serviço Premium pode atualmente substituir clusters de sistemas de mensagens locais dedicados, mesmo se as cargas de trabalho anexadas não forem executadas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="7074a-111">For many customers, Service Bus Premium can replace dedicated on-premises messaging clusters today, even if the attached workloads do not run in the cloud.</span></span> 

<span data-ttu-id="7074a-112">Saiba mais sobre conceitos de Barramento de Serviço [na seção de documentação do sistema de mensagens](https://docs.microsoft.com/en-us/azure/service-bus-messaging/)</span><span class="sxs-lookup"><span data-stu-id="7074a-112">Learn more about Service Bus concepts [in the messaging documentation section](https://docs.microsoft.com/en-us/azure/service-bus-messaging/)</span></span> 

<span data-ttu-id="7074a-113">Para desenvolvedores de Java, o Barramento de serviço fornece uma API nativa compatível com a Microsoft e o Barramento de Serviço também pode ser usado com bibliotecas compatíveis do AMQP 1.0 como o provedor JMS do Apache Qpid Proton.</span><span class="sxs-lookup"><span data-stu-id="7074a-113">For Java developers, Service Bus provides a Microsoft supported native API and Service Bus can also be used with AMQP 1.0 compliant libraries such as Apache Qpid Proton's JMS provider.</span></span>

<span data-ttu-id="7074a-114">O cliente oficial do Barramento de Serviço está disponível no [formulário de código-fonte no GitHub](https://github.com/azure/azure-service-bus-java) e os binários e pacotes de códigos-fontes [estão disponíveis na Central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span><span class="sxs-lookup"><span data-stu-id="7074a-114">The official Service Bus client is available in [source code form on GitHub](https://github.com/azure/azure-service-bus-java) and binaries and packaged sources [are available on Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span></span> 


## <a name="client-library"></a><span data-ttu-id="7074a-115">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="7074a-115">Client library</span></span>


<span data-ttu-id="7074a-116">Adicionar uma dependência ao arquivo `pom.xml` do seu projeto Maven para usar a biblioteca em seu próprio projeto.</span><span class="sxs-lookup"><span data-stu-id="7074a-116">Add a dependency to your Maven project's `pom.xml` file to use the library in your own project.</span></span> <span data-ttu-id="7074a-117">Especifique a versão desejada.</span><span class="sxs-lookup"><span data-stu-id="7074a-117">Specify the version as desired.</span></span>

<span data-ttu-id="7074a-118">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="7074a-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="examples"></a><span data-ttu-id="7074a-119">Exemplos</span><span class="sxs-lookup"><span data-stu-id="7074a-119">Examples</span></span>

<span data-ttu-id="7074a-120">O [repositório de exemplos de código](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contém exemplos de [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java) e [TopicClient e SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java) e [MessageSender e MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) de mensagens do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="7074a-120">The [sample code repository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contains samples for how to [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java) and [TopicClient and SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java) and [MessageSender and MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) messages from Service Bus.</span></span>


```java
public class BasicSendReceiveWithQueueClient {
    // Connection String for the namespace can be obtained from the Azure portal under the
    // 'Shared Access policies' section.
    private static final String connectionString = "{connection string}";
    private static final String queueName = "{queue name}";
    private static IQueueClient queueClient;
    private static int totalSend = 100;
    private static int totalReceived = 0;

    public static void main(String[] args) throws Exception {

        Log.log("Starting BasicSendReceiveWithQueueClient sample");

        // create client
        Log.log("Create queue client.");
        queueClient = new QueueClient(new ConnectionStringBuilder(connectionString, queueName), ReceiveMode.PeekLock);

        // send and receive
        queueClient.registerMessageHandler(new MessageHandler(queueClient), new MessageHandlerOptions(1, false, Duration.ofMinutes(1)));
        for (int i = 0; i < totalSend; i++) {
            int j = i;
            Log.log("Sending message #%d.", j);
            queueClient.sendAsync(new Message("" + i)).thenRunAsync(() -> { Log.log("Sent message #%d.", j);});
        }

        while(totalReceived != totalSend) {
            Thread.sleep(1000);
        }

        Log.log("Received all messages, exiting the sample.");
        Log.log("Closing queue client.");
        queueClient.close();
    }

    static class MessageHandler implements IMessageHandler {
        private IQueueClient client;

        public MessageHandler(IQueueClient client) {
            this.client = client;
        }

        @Override
        public CompletableFuture<Void> onMessageAsync(IMessage iMessage) {
            Log.log("Received message with sq#: %d and lock token: %s.", iMessage.getSequenceNumber(), iMessage.getLockToken());
            return this.client.completeAsync(iMessage.getLockToken()).thenRunAsync(() -> {
                Log.log("Completed message sq#: %d and locktoken: %s", iMessage.getSequenceNumber(), iMessage.getLockToken());
                totalReceived++;
            });
        }

        @Override
        public void notifyException(Throwable throwable, ExceptionPhase exceptionPhase) {
            Log.log(exceptionPhase + "-" + throwable.getMessage());
        }
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7074a-121">Explorar as APIs de Cliente</span><span class="sxs-lookup"><span data-stu-id="7074a-121">Explore the Client APIs</span></span>](/java/api/overview/azure/servicebus/clientlibrary)

## <a name="management-api"></a><span data-ttu-id="7074a-122">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="7074a-122">Management API</span></span>

<span data-ttu-id="7074a-123">Criar e gerenciar namespaces, tópicos, filas e assinaturas com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="7074a-123">Create and manage namespaces, topics, queues, and subscriptions with the management API.</span></span>

<span data-ttu-id="7074a-124">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="7074a-124">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7074a-125">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="7074a-125">Explore the Management APIs</span></span>](/java/api/overview/azure/servicebus/managementapi)


## <a name="examples"></a><span data-ttu-id="7074a-126">Exemplos</span><span class="sxs-lookup"><span data-stu-id="7074a-126">Examples</span></span>

<span data-ttu-id="7074a-127">[Gerenciar filas do Barramento de Serviço](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Criar e assinar tópicos do Barramento de Serviço](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span><span class="sxs-lookup"><span data-stu-id="7074a-127">[Manage Service Bus queues](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Create and subscribe to Service Bus topics](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span></span>

<span data-ttu-id="7074a-128">Explorar mais [exemplos de código Java para o Barramento de Serviço do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7074a-128">Explore more [sample Java code for Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) you can use in your apps.</span></span>