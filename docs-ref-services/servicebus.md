---
title: Bibliotecas de Barramento de Serviço para Java
description: Documentação de referência para as bibliotecas de gerenciamento e de cliente de Java para Barramento de Serviço
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
ms.openlocfilehash: ed830b4f7ffa104174205f75ea2923235029ea80
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33887756"
---
# <a name="service-bus-libraries-for-java"></a>Bibliotecas de Barramento de Serviço para Java

## <a name="overview"></a>Visão geral

Barramento de Serviço é um serviço de plataforma de sistema de mensagens transacionais, de classe empresarial que fornece tópicos de publicação/assinatura e filas altamente confiáveis com recursos de grande capacidade como entrega ordenada, sessões, particionamento, agendamento, assinaturas complexas, bem como o tratamento de fluxos de trabalho e transações.

Os recursos do Barramento de Serviço são comparáveis e geralmente excedem aqueles dos sofisticados agentes de mensagens herdados locais. Os recursos do Barramento de Serviço estão disponíveis por meio de protocolos baseados em padrões, como AMQP 1.0 e HTTPS e todos os gestos de protocolo são totalmente documentados, permitindo uma ampla interoperabilidade. 

Focado em um sistema de mensagens duráveis confiáveis e de alta disponibilidade, o tipo de Barramento de Serviço Premium oferece desempenho de taxa de transferência competitiva mesmo com implantações de datacenter local significativas, mas sem a seleção de hardware e processos de aquisição, execução e planejamento de implantação e sessões de otimização de desempenho que não acabam nunca. 

O Barramento de Serviço Premium é uma oferta totalmente gerenciada com capacidade dedicada reservada para cada locatário que gera um desempenho previsível com um modelo de preço simples e orientado à capacidade e a um custo geral muito menor do que os agentes comerciais locais. Para muitos clientes, o Barramento de Serviço Premium pode atualmente substituir clusters de sistemas de mensagens locais dedicados, mesmo se as cargas de trabalho anexadas não forem executadas na nuvem. 

Saiba mais sobre conceitos de Barramento de Serviço [na seção de documentação do sistema de mensagens](https://docs.microsoft.com/azure/service-bus-messaging/) 

Para desenvolvedores de Java, o Barramento de serviço fornece uma API nativa compatível com a Microsoft e o Barramento de Serviço também pode ser usado com bibliotecas compatíveis do AMQP 1.0 como o provedor JMS do Apache Qpid Proton.

## <a name="client-library"></a>Biblioteca do cliente

O cliente oficial do Barramento de Serviço está disponível no [formulário de código-fonte no GitHub](https://github.com/azure/azure-service-bus-java) e os binários e pacotes de códigos-fontes [estão disponíveis na Central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).

**O [repositório de código de exemplo](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contém amostras para:**
* Como usar o [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)
* Como usar o [TopicClient e SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)
* Como usar mensagens do [MessageSender e MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) a partir do barramento de serviço.

Adicionar uma dependência ao arquivo `pom.xml` do seu projeto Maven para usar a biblioteca em seu próprio projeto. Especifique a versão desejada.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

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
> [Explorar as APIs de cliente](/java/api/overview/azure/servicebus/client)
> [Encontre mais exemplos aqui (veja também acima para obter mais detalhes)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)

## <a name="management-api"></a>API de gerenciamento

Criar e gerenciar namespaces, tópicos, filas e assinaturas com a API de gerenciamento.

**Veja alguns exemplos aqui:**
* [Gerenciar filas do Barramento de Serviço](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
* [Criar e assinar tópicos do Barramento de Serviço](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)

**Use a API de gerenciamento em seu projeto:**
\
[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a API de gerenciamento em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/servicebus/management)

Explorar mais [exemplos de código Java para o Barramento de Serviço do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) que você pode usar em seus aplicativos.
