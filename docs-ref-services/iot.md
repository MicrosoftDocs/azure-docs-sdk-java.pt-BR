---
title: Bibliotecas do Hub IoT do Azure para Java
description: Documentação de referência para as bibliotecas do Hub IoT do Azure para Java
keywords: Azure, Java, SDK, API, evento, IoT, fluxos, dispositivos, hub iot
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: 497b2a72d851b8e43a48384c6f1a160e8a38cbe6
ms.sourcegitcommit: bb7286fad75a2bb43e6ce1a8f1b09e701147c9f9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047143"
---
# <a name="azure-iot-libraries-for-java"></a>Bibliotecas de IoT do Azure para Java

Conecte, monitore e controle ativos de Internet das Coisas com o [Hub IoT do Azure](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).

Para se familiarizar com o Hub IoT do Azure, consulte [Conectar seu dispositivo ao seu hub IoT usando Java](/azure/iot-hub/iot-hub-java-java-getstarted).

## <a name="iot-service-library"></a>Biblioteca de Serviço de IoT

Registrar dispositivos e enviar mensagens da nuvem para dispositivos registrados usando a biblioteca de Serviço IoT.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a>Biblioteca de Dispositivo Iot

Enviar mensagens para a nuvem e receber mensagens em dispositivos usando a biblioteca de Dispositivo IoT.

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorar as APIs de cliente](/java/api/overview/azure/iot/client)   

## <a name="example"></a>Exemplo

Enviar uma mensagem do Hub IoT do Azure para um dispositivo.

```java
Message messageToSend = new Message(messageText);
messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
messageToSend.setMessageId(java.util.UUID.randomUUID().toString());

// set message properties
Map<String, String> propertiesToSend = new HashMap<String, String>();
propertiesToSend.put(messagePropertyKey,messagePropertyKey);
messageToSend.setProperties(propertiesToSend);

CompletableFuture<Void> future = serviceClient.sendAsync(deviceId, messageToSend);
try {
    future.get();
}
catch (ExecutionException e) {
    System.out.println("Exception : " + e.getMessage());
}
```


## <a name="samples"></a>Exemplos

[Exemplos de Dispositivo IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)     
[Exemplos de Serviço IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

Explore mais [exemplos de código Java para o IoT do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) que você pode usar em seus aplicativos.
