---
title: Implantar um aplicativo de arquivo JAR do Spring Boot na nuvem com o Maven e o Azure
description: Saiba como implantar um aplicativo Spring Boot na nuvem usando o plug-in Maven do Aplicativo Web do Azure para Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: b133290d1f14429cbf36d6ed5a67d27e1a637593
ms.sourcegitcommit: 599405a9ce892d75073ef0776befa2fa22407b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67237603"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a>Implantar um aplicativo Web do arquivo JAR do Spring Boot no Serviço de Aplicativo do Azure no Linux

Este artigo demonstra como usar o [plug-in do Maven para os Aplicativos Web do Serviço de Aplicativo do Azure](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) para implantar um aplicativo Spring Boot empacotado como um Java SE JAR no [Serviço de Aplicativo do Azure no Linux](/azure/app-service/containers/). Escolha a implantação Java SE em vez dos [arquivos Tomcat e WAR](/azure/app-service/containers/quickstart-java) quando quiser consolidar as dependências, execução e configuração do aplicativo em um único artefato de implantação.


Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir as etapas deste tutorial, você precisa ter o seguinte instalado e configurado:

* A [CLI do Azure](/cli/azure/), localmente ou por meio do [Azure Cloud Shell](https://shell.azure.com).
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.
* O [Maven](https://maven.apache.org/) do Apache, versão 3.
* Um cliente [Git](https://git-scm.com/downloads).

## <a name="install-and-sign-in-to-azure-cli"></a>Instalar e entrar na CLI do Azure

A maneira mais simples e fácil de obter o plug-in do Maven implantando seu aplicativo Spring Boot é usando a [CLI do Azure](/cli/azure/).

Entre em sua conta do Azure usando a CLI do Azure:
   
   ```shell
   az login
   ```
   
Siga as instruções na tela para concluir o processo de entrada.

## <a name="clone-the-sample-app"></a>Clonar o aplicativo de exemplo

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

## <a name="configure-maven-plugin-for-azure-app-service"></a>Configurar o plug-in do Maven para o Serviço de Aplicativo do Azure

Nesta seção, será configurado o projeto Spring Boot `pom.xml` para que o Maven possa implantar o aplicativo no Serviço de Aplicativo do Azure no Linux.

1. Abra `pom.xml` em um editor de código.

2. Na seção `<build>` do pom.xml, adicione a seguinte entrada `<plugin>` dentro da marca `<plugins>`.

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.6.0</version>
   </plugin>
   ```

3. Em seguida, você pode configurar a implantação, executar o comando maven `mvn azure-webapp:config` no prompt de comando e usar o **número** para escolher essas opções no prompt:
    * **SO**: linux  
    * **javaVersion**: jre8
    * **runtimeStack**: jre8

Quando for exibida a solicitação **Confirmar (S/N)** , pressione **'s'** e a configuração estará concluída.

```cmd
~@Azure:~/gs-spring-boot/complete$ mvn azure-webapp:config
[INFO] Scanning for projects...
[INFO]
[INFO] -----------------< org.springframework:gs-spring-boot >-----------------
[INFO] Building gs-spring-boot 0.1.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- azure-webapp-maven-plugin:1.6.0:config (default-cli) @ gs-spring-boot ---
[WARNING] The plugin may not work if you change the os of an existing webapp.
Define value for OS(Default: Linux):
1. linux [*]
2. windows
3. docker
Enter index to use:
Define value for javaVersion(Default: jre8):
1. jre8 [*]
2. java11
Enter index to use:
Define value for runtimeStack(Default: TOMCAT 8.5):
1. TOMCAT 9.0
2. jre8
3. TOMCAT 8.5 [*]
4. WILDFLY 14
Enter index to use: 2
Please confirm webapp properties
AppName : gs-spring-boot-1559091271202
ResourceGroup : gs-spring-boot-1559091271202-rg
Region : westeurope
PricingTier : Premium_P1V2
OS : Linux
RuntimeStack : JAVA 8-jre8
Deploy to slot : false
Confirm (Y/N)? : Y
```

4. Adicione a seção `<appSettings>` à seção `<configuration>` do `<azure-webapp-maven-plugin>` para escutar na porta *80*.

    ```xml
   <plugin>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-webapp-maven-plugin</artifactId>
       <version>1.6.0</version>
       <configuration>
          <schemaVersion>V2</schemaVersion>
          <resourceGroup>gs-spring-boot-1559091271202-rg</resourceGroup>
          <appName>gs-spring-boot-1559091271202</appName>
          <region>westeurope</region>
          <pricingTier>P1V2</pricingTier>

          <!-- Begin of App Settings  -->
          <appSettings>
             <property>
                   <name>JAVA_OPTS</name>
                   <value>-Dserver.port=80</value>
             </property>
          </appSettings>
          <!-- End of App Settings  -->
          ...
         </configuration>
   </plugin>
   ```

## <a name="deploy-the-app-to-azure"></a>Implantar o aplicativo no Azure

Depois de definir todas as configurações nas seções anteriores deste artigo, você estará pronto para implantar seu aplicativo Web no Azure. Para fazer isso, execute as seguintes etapas:

1. Do prompt de comando ou janela de terminal que você estava usando antes, recompile o arquivo JAR usando o Maven, se você tiver feito alterações no arquivo *pom.xml*; por exemplo:
   ```shell
   mvn clean package
   ```

1. Implante seu aplicativo Web no Azure usando o Maven; por exemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

O Maven implantará seu aplicativo Web no Azure. Se o aplicativo Web ou o plano dele ainda não existirem, eles serão criados.

Depois que a Web tiver sido implantada, você conseguirá gerenciá-la por meio do [portal do Azure].

* Seu aplicativo Web será listado nos **Serviços de Aplicativos**:

   ![Aplicativo Web listado nos Serviços de Aplicativos do portal do Azure][AP01]

* E a URL para seu aplicativo Web será listada na **Visão geral** de seu aplicativo Web:

   ![Como determinar a URL de seu aplicativo Web][AP02]

Verifique se a implantação foi bem-sucedida usando o mesmo comando cURL de antes e com a URL do aplicativo Web do Portal em vez de `localhost`. Você verá a seguinte mensagem exibida: **Saudações do Spring Boot!** 

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.

> [!div class="nextstepaction"]
> [Spring no Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionais

Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:

* [Plug-in do Maven para aplicativos Web do Azure]

* [Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Criar uma entidade de serviço do Azure com a CLI do Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referência de configurações do Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[Portal do Azure]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in do Maven para aplicativos Web do Azure]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
