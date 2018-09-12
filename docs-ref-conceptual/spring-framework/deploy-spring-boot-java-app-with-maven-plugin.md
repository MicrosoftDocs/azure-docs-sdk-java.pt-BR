---
title: Implantar um aplicativo Spring Boot para a nuvem com o Maven e o Azure
description: Saiba como implantar um aplicativo Spring Boot para a nuvem usando o plug-in Maven para Aplicativos Web do Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ca788354d26964bd9f1e21a0d3a8005ff65ce4bc
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324342"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a>Implantar um aplicativo Spring Boot na nuvem usando o Maven Plugin para o Serviço de Aplicativo do Azure

Este artigo demonstra como usar o plug-in do Maven para Aplicativos Web do Serviço de Aplicativo do Azure a fim de implantar um exemplo de aplicativo Spring Boot.

> [!NOTE]
> 
> O [plug-in do Maven para Aplicativos Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para [Apache Maven](http://maven.apache.org/) fornece uma integração perfeita do Serviço de Aplicativo do Azure em projetos Maven e simplifica o processo para os desenvolvedores implantarem aplicativos Web no Serviço de Aplicativo do Azure.

Antes de usar o plug-in do Maven, verifique na Central do Maven a versão mais recente do plugin disponível: [![Central do Maven](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22) 

## <a name="prerequisites"></a>Pré-requisitos

Para concluir as etapas neste tutorial, você precisará ter os seguintes pré-requisitos:

* Uma assinatura do Azure; se ainda não tiver uma, inscreva-se para uma [conta do Azure gratuita].
* A[CLI (interface de linha de comando) do Azure].
* Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.
* A ferramenta de compilação [Maven] do Apache (Versão 3).
* Um cliente [Git].

## <a name="clone-the-sample-spring-boot-web-app"></a>Clonar o aplicativo Web Spring Boot de exemplo

Nesta seção, você clonará um aplicativo Spring Boot concluído e o testará localmente.

1. Abra um prompt de comando ou janela de terminal e crie um diretório local para conter o aplicativo Spring Boot, e altere para esse diretório; por exemplo:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- ou --
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. Clone o projeto de exemplo [Introdução ao Spring Boot] para o diretório que você criou. Por exemplo:
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. Altere o diretório para o projeto concluído. Por exemplo:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Crie o arquivo JAR usando o Maven. Por exemplo:
   ```shell
   mvn clean package
   ```

1. Após a criação do aplicativo Web, inicie-o usando o Maven; por exemplo:
   ```shell
   mvn spring-boot:run
   ```

1. Teste o aplicativo Web navegando até ele localmente usando um navegador da Web. Por exemplo, use o comando a seguir, se você tiver o curl disponível:
   ```shell
   curl http://localhost:8080
   ```

1. Você verá a seguinte mensagem exibida: **Saudações do Spring Boot!**

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a>Ajustar o projeto para implantação com base em WAR no Serviço de Aplicativo do Azure

Nesta seção, ajustaremos rapidamente o projeto Spring Boot para implantá-lo como um arquivo WAR no Serviço de Aplicativo do Azure, que fornece o Tomcat como tempo de execução padrão. Para que isso funcione, dois arquivos precisam ser modificados:

- O arquivo `pom.xml` do Maven
- A classe `Application` de Java

Vamos começar com as configurações do Maven:

1. Abra `pom.xml`

1. Adicione `<packaging>war</packaging>` logo após a definição `<artifactId>` na parte superior:
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. Adicione a seguinte dependência:
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

Agora, abra a classe `Application`, após seu IDE já ter coletado as novas dependências, e continue com as seguintes modificações:

1. Torne a classe Application uma subclasse de `SpringBootServletInitializer`:
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. Adicione o seguinte método à classe Application:
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```
1. Organize suas importações para garantir que `SpringApplicationBuilder` e `SpringBootServletInitializer` são importados corretamente.

Agora, seu aplicativo está pronto para ser implantado no Tomcat e em qualquer outro tempo de execução do Servlet (por exemplo, Jetty).

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a>Adicionar o plug-in do Maven para Aplicativos Web do Serviço de Aplicativo do Azure

Nesta seção, adicionaremos um plug-in do Maven que automatizará toda a implantação desse aplicativo em Aplicativos Web do Serviço de Aplicativo do Azure.

1. Abra `pom.xml` mais uma vez.

1. Dentro de `<properties>`, defina um formato de carimbo de data/hora personalizada com a propriedade `maven.build.timestamp.format`. Como o Serviço de Aplicativo do Azure cria uma URL pública para o seu aplicativo, essa configuração será usada para gerar o nome da sua implantação e evitar conflitos com as implantações ativas de outros usuários.
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. No elemento `<plugins>`, adicione o seguinte:
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

Com essas configurações, seu projeto do Maven está pronto para a implantação ativa no Aplicativo Web do Serviço de Aplicativo do Azure.

## <a name="install-and-log-in-to-azure-cli"></a>Instalar e fazer logon na CLI do Azure

A maneira mais simples e fácil de obter o plug-in do Maven implantando seu aplicativo Spring Boot é usando a [CLI do Azure](https://docs.microsoft.com/cli/azure/). Verifique se ela está instalada.

1. Entre em sua conta do Azure usando a CLI do Azure:
   
   ```shell
   az login
   ```
   
   Siga as instruções na tela para concluir o processo de entrada.

## <a name="optionally-customize-pomxml-before-deploying"></a>Opcionalmente, personalize o pom.xml antes de implantar

Abra o arquivo `pom.xml` de seu aplicativo Spring Boot em um editor de texto e localize o elemento `<plugin>` para `azure-webapp-maven-plugin`. Esse elemento deverá se parecer com este exemplo:

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

Você pode modificar diversos valores do plug-in do Maven, e há uma descrição detalhada de cada um desses elementos disponível na documentação [Plug-in do Maven para aplicativos Web do Azure]. Dito isso, vale a pena destacar diversos valores neste artigo:

| Elemento | DESCRIÇÃO |
|---|---|
| `<version>` | Especifica a versão do [Plug-in do Maven para aplicativos Web do Azure]. Verifique a versão listada no [Repositório Central do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para garantir que esteja usando a versão mais recente. |
| `<resourceGroup>` | Especifica o grupo de recursos de destino, que é `maven-plugin` neste exemplo. Esse grupo de recursos é criado durante a implantação, caso ainda não exista. |
| `<appName>` | Especifica o nome de destino de seu aplicativo Web. Neste exemplo, o nome de destino é `maven-web-app-${maven.build.timestamp}`, no qual o sufixo `${maven.build.timestamp}` é acrescentado neste exemplo para evitar conflitos. (O carimbo de data/hora é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo). |
| `<region>` | Especifica a região de destino, que neste exemplo é `westus`. (Uma lista completa está disponível na documentação [Plug-in do Maven para aplicativos Web do Azure]). |
| `<javaVersion>` | Especifica a versão de tempo de execução Java para seu aplicativo Web. (Uma lista completa está disponível na documentação [Plug-in do Maven para aplicativos Web do Azure]). |
| `<deploymentType>` | Especifica o tipo de implantação para seu aplicativo Web. O padrão é `war`. |

## <a name="build-and-deploy-your-web-app-to-azure"></a>Criar e implantar seu aplicativo Web do Azure

Depois de definir todas as configurações nas seções anteriores deste artigo, você estará pronto para implantar seu aplicativo Web no Azure. Para fazer isso, execute as seguintes etapas:

1. Do prompt de comando ou janela de terminal que você estava usando antes, recompile o arquivo JAR usando o Maven, se você tiver feito alterações no arquivo *pom.xml*; por exemplo:
   ```shell
   mvn clean package
   ```

1. Implante seu aplicativo Web no Azure usando o Maven; por exemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

O Maven implantará seu aplicativo Web no Azure; se o aplicativo Web ainda não existir, ele será criado.

Após a implantação de sua Web, você poderá gerenciá-la usando o [portal do Azure].

* Seu aplicativo Web será listado nos **Serviços de Aplicativos**:

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* E a URL para seu aplicativo Web será listada na **Visão geral** de seu aplicativo Web:

   ![Como determinar a URL de seu aplicativo Web][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:

* [Plug-in do Maven para aplicativos Web do Azure]

* [Fazer logon no Azure desde a CLI do Azure](/azure/xplat-cli-connect)

* [Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Criar uma entidade de serviço do Azure com a CLI do Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referência de configurações do Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portal do Azure]: https://portal.azure.com/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in do Maven para aplicativos Web do Azure]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
