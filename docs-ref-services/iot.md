---
title: Bibliotecas do Hub IoT do Azure para Java
description: "Documentação de referência para as bibliotecas do Hub IoT do Azure para Java"
keywords: Azure, Java, SDK, API, evento, IoT, fluxos, dispositivos, hub iot
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: b386612741e222fcaeb7b6c38753d0cb7d616239
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-iot-libraries-for-java"></a><span data-ttu-id="91569-104">Bibliotecas de IoT do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="91569-104">Azure IoT libraries for Java</span></span>

<span data-ttu-id="91569-105">Conecte, monitore e controle ativos de Internet das Coisas com o [Hub IoT do Azure](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-what-is-iot-hub).</span><span class="sxs-lookup"><span data-stu-id="91569-105">Connect, monitor, and control Internet of Things assets with [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-what-is-iot-hub).</span></span>

<span data-ttu-id="91569-106">Para se familiarizar com o Hub IoT do Azure, consulte [Conectar seu dispositivo ao seu hub IoT usando Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span><span class="sxs-lookup"><span data-stu-id="91569-106">To get started with Azure IoT Hub, see [Connect your device to your IoT hub using Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span></span>

## <a name="iot-service-library"></a><span data-ttu-id="91569-107">Biblioteca de Serviço de IoT</span><span class="sxs-lookup"><span data-stu-id="91569-107">IoT Service library</span></span>

<span data-ttu-id="91569-108">Registrar dispositivos e enviar mensagens da nuvem para dispositivos registrados usando a biblioteca de Serviço IoT.</span><span class="sxs-lookup"><span data-stu-id="91569-108">Register devices and send messages from the cloud to registered devices using the IoT Service library.</span></span>

<span data-ttu-id="91569-109">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="91569-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a><span data-ttu-id="91569-110">Biblioteca de Dispositivo Iot</span><span class="sxs-lookup"><span data-stu-id="91569-110">Iot Device library</span></span>

<span data-ttu-id="91569-111">Enviar mensagens para a nuvem e receber mensagens em dispositivos usando a biblioteca de Dispositivo IoT.</span><span class="sxs-lookup"><span data-stu-id="91569-111">Send messages to the cloud and receive messages on devices using the IoT Device library.</span></span>

<span data-ttu-id="91569-112">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="91569-112">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="91569-113">Explorar as APIs de Cliente</span><span class="sxs-lookup"><span data-stu-id="91569-113">Explore the Client APIs</span></span>](/java/api/overview/azure/iot/clientlibrary)   

## <a name="example"></a><span data-ttu-id="91569-114">Exemplo</span><span class="sxs-lookup"><span data-stu-id="91569-114">Example</span></span>

<span data-ttu-id="91569-115">Enviar uma mensagem do Hub IoT do Azure para um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91569-115">Send a message from Azure IoT Hub to a device.</span></span>

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


## <a name="samples"></a><span data-ttu-id="91569-116">Exemplos</span><span class="sxs-lookup"><span data-stu-id="91569-116">Samples</span></span>

<span data-ttu-id="91569-117">[Exemplos de Dispositivo IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span><span class="sxs-lookup"><span data-stu-id="91569-117">[IoT Device samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span></span>  
[<span data-ttu-id="91569-118">Exemplos de Serviço IoT</span><span class="sxs-lookup"><span data-stu-id="91569-118">IoT Service samples</span></span>](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

<span data-ttu-id="91569-119">Explore mais [exemplos de código Java para o IoT do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="91569-119">Explore more [sample Java code for Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) you can use in your apps.</span></span>
