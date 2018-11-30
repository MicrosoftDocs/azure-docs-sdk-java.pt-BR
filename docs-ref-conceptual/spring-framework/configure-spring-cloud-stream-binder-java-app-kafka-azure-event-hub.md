---
title: Como usar o Inicializador do Spring Boot para Apache Kafka com os Hubs de Eventos do Azure
description: Saiba como configurar um aplicativo criado com o Spring Boot Initializr para usar o Apache Kafka com os Hubs de Eventos do Azure.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: ab465b56c05c7d480109fc97a4f1c74beaf53856
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339110"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a>Como usar o Inicializador do Spring Boot para Apache Kafka com os Hubs de Eventos do Azure

## <a name="overview"></a>Visão geral

Este artigo demonstra como configurar um Spring Cloud Stream Binder baseado em Java criado com o Spring Boot Initializer para usar o [Apache Kafka] com os Hubs de Eventos do Azure.

## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.

> [!IMPORTANT]
>
> É necessário o Spring Boot versão 2.0 ou posterior para concluir as etapas neste artigo.
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a>Criar um Hub de Eventos do Azure usando o portal do Azure

### <a name="create-an-azure-event-hub-namespace"></a>Criar um Namespace do Hub de Eventos do Azure

1. Navegue até o portal do Azure em <https://portal.azure.com/> e entre.

1. Clique em **+Criar um recurso**, **Internet das Coisas** e em **Hubs de Eventos**.

   ![Criar Namespace do Hub de Eventos do Azure][IMG01]

1. Na página **Criar Namespace**, insira as seguintes informações:

   * Insira um **Nome** exclusivo, que se tornará parte da URI do namespace do hub de eventos. Por exemplo: se você inseriu **wingtiptoys** como o **Nome**, a URI será *wingtiptoys.servicebus.windows.net*.
   * Escolha um **Tipo de preço** para o namespace do hub de eventos.
   * Especifique **Habilitar Kafka** como o namespace.
   * Escolha a **Assinatura** que você deseja usar para o banco de dados.
   * Especifique se deseja criar um novo **Grupo de recursos** para o namespace ou escolher um grupo de recursos existente.
   * Especifique o **Local** do namespace do hub de eventos.

   ![Especificar opções de Namespace do Hub de Eventos do Azure][IMG02]

1. Quando você tiver especificado as opções listadas acima, clique em **Criar** para criar o namespace.

### <a name="create-an-azure-event-hub-in-your-namespace"></a>Criar um Hub de Eventos do Azure no namespace

1. Navegue até o portal do Azure em <https://portal.azure.com/>.

1. Clique em **Todos os recursos** e no namespace criado.

   ![Selecionar Namespace do Hub de Eventos do Azure][IMG03]

1. Clique em **Hubs de Eventos** e **+Hub de Eventos**.

   ![Adicionar novo Hub de Eventos do Azure][IMG04]

1. Na página **Criar Hub de Eventos**, insira um **Nome** exclusivo para o Hub de Eventos e clique **Criar**.

   ![Criar Hub de Eventos do Azure][IMG05]

1. Quando o Hub de Eventos tiver sido criado, ele será listado na página **Hubs de Eventos**.

   ![Criar Hub de Eventos do Azure][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Criar um aplicativo Spring Boot simples com o Spring Initializr

1. Navegue até <https://start.spring.io/>.

1. Especifique as seguintes opções:

   * Gere um projeto **Maven** com **Java**.
   * Especifique uma versão **Spring Boot** igual ou maior que 2.0.
   * Especifique os nomes de **Grupo** e **Artefato** do aplicativo.
   * Adicione a dependência da **Web**.

      ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote, por exemplo, *com.wintiptoys.kafka*.
   >

1. Quando você tiver especificado as opções listadas acima, clique em **Gerar Projeto**.

1. Quando solicitado, baixe o projeto para um caminho no computador local.

   ![Baixar projeto do Spring][SI02]

1. Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot simple estará pronto para edição.

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a>Configurar o aplicativo Spring Boot para usar os iniciadores do Spring Cloud Kafka Stream e iniciadores do Hub de Eventos do Azure

1. Localize o arquivo *pom.xml* no diretório-raiz do aplicativo, por exemplo:

   `C:\SpringBoot\kafka\pom.xml`

   -ou-

   `/users/example/home/kafka/pom.xml`

1. Abra o arquivo *pom.xml* em um editor de texto e adicione o iniciador do Spring Cloud Kafka Stream e os iniciadores do Hub de Eventos do Azure à lista de `<dependencies>`:

   ```xml
   <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-stream-kafka</artifactId>
      <version>2.0.1.RELEASE</version>
   </dependency>
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-starter-eventhub</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Editar o arquivo pom.xml][SI03]

1. Salve e feche o arquivo *pom.xml*.

## <a name="create-an-azure-credential-file"></a>Criar um arquivo de credencial do Azure

1. Abra um prompt de comando.

1. Navegue até o diretório de *recursos* do aplicativo Spring Boot, por exemplo:

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   -ou-

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. Entre na sua conta do Azure:

   ```azurecli
   az login
   ```

1. Liste suas assinaturas:

   ```azurecli
   az account list
   ```
   O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```
   
1. Especifique o GUID para a assinatura que quer usar no Azure; por exemplo:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. Crie seu arquivo de credencial do Azure:

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   Esse comando criará um arquivo *my.azureauth* no diretório *recursos* com conteúdo semelhante ao seguinte exemplo:

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a>Configurar aplicativo Spring Boot para usar seu Hub de Eventos do Azure

1. Localize *application.properties* no diretório *recursos* do aplicativo, por exemplo:

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   -ou-

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. Abra o arquivo *application.properties* em um editor de texto, adicione as seguintes linhas e substitua os valores de exemplo pelas propriedades adequadas de seu hub de eventos:

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   Em que:

   |                       Campo                       |                                                                                   DESCRIÇÃO                                                                                    |
   |---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `spring.cloud.azure.credential-file-path`     |                                                    Especifica o arquivo de credencial do Azure que você criou anteriormente neste tutorial.                                                    |
   |        `spring.cloud.azure.resource-group`        |                                                      Especifica o Grupo de Recursos do Azure que contém seu Hub de Eventos do Azure.                                                      |
   |            `spring.cloud.azure.region`            |                                           Especifica a região geográfica definida quando você criou o Hub de Eventos do Azure.                                            |
   |      `spring.cloud.azure.eventhub.namespace`      |                                          Especifica o nome exclusivo definido quando você criou o namespace do Hub de Eventos do Azure.                                           |
   | `spring.cloud.stream.bindings.input.destination`  |                            Especifica o destino de entrada do Hub de Eventos do Azure, que é o hub criado anteriormente neste tutorial.                            |
   |    `spring.cloud.stream.bindings.input.group `    | Especifica um Grupo de Consumidores do Hub de Eventos do Azure, que pode ser definido para “$Default” para usar o grupo de consumidores básico gerado quando você criou seu Hub de Eventos do Azure. |
   | `spring.cloud.stream.bindings.output.destination` |                               Especifica o destino de saída do Hub de Eventos do Azure que, para este tutorial, será igual ao destino de entrada.                               |


3. Salve e feche o arquivo *application.properties*.

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a>Adicionar código de exemplo para implementar a funcionalidade básica do hub de eventos

Nesta seção, você criará as classes Java necessárias para enviar eventos ao hub de eventos.

### <a name="modify-the-main-application-class"></a>Modificar a classe principal do aplicativo

1. Localize o arquivo Java do aplicativo principal no diretório do pacote do seu aplicativo. Por exemplo:

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   -ou-

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. Abra o arquivo Java do aplicativo principal em um editor de texto e adicione as seguintes linhas ao arquivo:

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class KafkaApplication {
      public static void main(String[] args) {
         SpringApplication.run(KafkaApplication.class, args);
      }
   }
   ```

1. Salve e feche o arquivo Java do aplicativo principal.


### <a name="create-a-new-class-for-the-source-connector"></a>Criar uma nova classe para o conector de origem

1. Crie um novo arquivo Java chamado *KafkaSource.java* no diretório do pacote de seu aplicativo; abra o arquivo em um editor de texto e adicione as seguintes linhas:

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class KafkaSource {
      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String sendMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```

1. Salve e feche o arquivo *KafkaSource.java*.

### <a name="create-a-new-class-for-the-sink-connector"></a>Criar uma nova classe para o conector do coletor

1. Crie um novo arquivo Java chamado *KafkaSink.java* no diretório do pacote de seu aplicativo; abra o arquivo em um editor de texto e adicione as seguintes linhas:

   ```java
   package com.wingtiptoys.kafka;

   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;

   @EnableBinding(Sink.class)
   public class KafkaSink {
      private static final Logger LOGGER = LoggerFactory.getLogger(KafkaSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message) {
         LOGGER.info("New message received: " + message);
      }
   }
   ```

1. Salve e feche o arquivo *KafkaSink.java*.

## <a name="build-and-test-your-application"></a>Criar e testar o aplicativo

1. Abra um prompt de comando e altere o diretório para a pasta em que seu arquivo *pom.xml* está localizado, por exemplo:

   `cd C:\SpringBoot\kafka`

   -ou-

   `cd /users/example/home/kafka`

1. Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Quando seu aplicativo estiver em execução, você poderá usar *curl* para testá-lo, por exemplo:

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   Você deverá ver "olá" publicado nos logs do aplicativo. Por exemplo: 

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> Para fins de teste, você poderia modificar o *KafkaSource.java* para que contivesse um formulário HTML simples, como no exemplo abaixo:
> 
> ```java
> package com.wingtiptoys.kafka;
>    
> import org.springframework.beans.factory.annotation.Autowired;
> import org.springframework.cloud.stream.annotation.EnableBinding;
> import org.springframework.cloud.stream.messaging.Source;
> import org.springframework.messaging.support.GenericMessage;
> import org.springframework.web.bind.annotation.GetMapping;
> import org.springframework.web.bind.annotation.PostMapping;
> import org.springframework.web.bind.annotation.RequestBody;
> import org.springframework.web.bind.annotation.RequestParam;
> import org.springframework.web.bind.annotation.RestController;
> 
> @EnableBinding(Source.class)
> @RestController
> public class KafkaSource {
>   @Autowired
>   private Source source;
> 
>   @GetMapping("/")
>   public String sendForm() {
>     return "<html><body>" +
>       "<form action=\"/messages\" method=\"post\">" +
>       "<input type=\"text\" name=\"text\">" +
>       "<input type=\"submit\">" +
>       "</form></body><html>";
>     }
> 
>   @PostMapping("/messages")
>   public String sendMessage(@RequestBody String message) {
>     this.source.output().send(new GenericMessage<>(message));
>     return message;
>   }
> }
> ```
> 
> Isso permitiria o uso de um navegador da Web para testar seu aplicativo:
> 
> ![Testando o aplicativo em um navegador da Web][TB01]
> 
> Quando você envia o formulário, o aplicativo exibe os resultados:
> 
> ![Resposta do aplicativo em um navegador da Web][TB02]
> 

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o suporte do Azure para o Event Hub Stream Binder e para o Apache Kafka, confira os seguintes artigos:

* [O que é Hub de Eventos do Azure?](/azure/event-hubs/event-hubs-about)

* [Hubs de Eventos do Azure para Apache Kafka](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [Criar um namespace dos Hubs de Eventos e um hub de eventos usando o portal do Azure](/azure/event-hubs/event-hubs-create)

* [Criar hubs de eventos habilitados para Apache Kafka](/azure/event-hubs/event-hubs-create-kafka-enabled)

Para obter mais informações sobre como usar o Azure com Java, veja [Azure para Desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].

O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial. Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos. Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>. Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-03.png

[TB01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-01.png
[TB02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-02.png
