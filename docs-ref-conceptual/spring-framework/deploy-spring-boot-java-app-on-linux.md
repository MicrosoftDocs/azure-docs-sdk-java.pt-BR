---
title: Implantar um Aplicativo Web do Spring Boot no Serviço de Aplicativo do Azure para o Contêiner
description: Este tutorial orienta você pelas etapas de implantar um aplicativo Spring Boot como um aplicativo Web do Linux no Microsoft Azure.
services: azure app service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: azure app service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 407b852e24ef88d2fb075bd064f1acf2b107ddc1
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270864"
---
# <a name="deploy-a-spring-boot-application-on-azure-app-service-for-container"></a>Implantar um aplicativo do Spring Boot no Serviço de Aplicativo do Azure para o Contêiner

Este tutorial mostra como usar o [Docker] para colocar em contêiner um aplicativo [Spring Boot] e implantar sua própria imagem do docker em um host Linux no [Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).

## <a name="prerequisites"></a>Pré-requisitos

Para concluir as etapas deste tutorial, você precisa ter os seguintes pré-requisitos:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* A[CLI (interface de linha de comando) do Azure].
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.
* A ferramenta de compilação [Maven] do Apache (Versão 3).
* Um cliente [Git].
* Um cliente do [Docker].

> [!NOTE]
>
> Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Criar o aplicativo Web de Introdução ao Spring Boot no Docker

As etapas a seguir explicarão as etapas necessárias para criar um aplicativo Web Spring Boot simples e testá-lo localmente.

1. Abra um prompt de comando, crie um diretório local para conter o aplicativo e altere para o diretório. Por exemplo:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- ou --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório criado. Por exemplo:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Altere o diretório para o projeto concluído. Por exemplo:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Crie o arquivo JAR usando o Maven. Por exemplo:
   ```
   mvn package
   ```

1. Quando o aplicativo Web tiver sido criado, altere o diretório para o diretório `target` em que o arquivo JAR está localizado e inicie o aplicativo Web. Por exemplo:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Teste o aplicativo Web navegando até ele localmente usando um navegador da Web. Por exemplo, se você tiver ondulação disponível e tiver configurado o servidor Tomcat para ser executado na porta 80:
   ```
   curl http://localhost
   ```

1. Você verá a seguinte mensagem exibida: **Olá, mundo do Docker!**

   ![Procurar aplicativo de exemplo localmente][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Criar um Registro de Contêiner do Azure para usar como um Registro do Docker Privado

As etapas a seguir orientam você no uso do portal do Azure para criar um Registro de contêiner do Azure.

> [!NOTE]
>
> Se você quiser usar a CLI do Azure, em vez do portal do Azure, siga as etapas em [Criar um registro de contêiner do Docker privado usando a CLI do Azure 2.0](/azure/container-registry/container-registry-get-started-azure-cli).
>

1. Navegue até o [portal do Azure] e conecte-se.

   Depois de entrar em sua conta no portal do Azure, você pode seguir as etapas no artigo [Criar um registro de contêiner privado do Docker usando o portal do Azure], que foram parafraseadas nas etapas a seguir para fins de conveniência.

1. Clique no ícone do menu para **+ Novo** e, em seguida, clique em **Contêineres** e em **Registro de Contêiner do Azure**.
   
   ![Criar um novo Registro de Contêiner do Azure][AR01]

1. Quando a página de informações para o modelo de Registro de Contêiner do Azure for exibida, clique em **Criar**. 

   ![Criar um novo Registro de Contêiner do Azure][AR02]

1. Quando a página **Criar registro de contêiner** for exibida, insira seu **Nome do registro** e **Grupo de recursos**, escolha **Habilitar** para o **Usuário administrador** e clique em **Criar**.

   ![Definir configurações do registro de contêiner do Azure][AR03]

1. Quando o registro de contêiner tiver sido criado, navegue até o registro de contêiner no portal do Azure e, em seguida, clique em **Chaves de Acesso**. Anote o nome de usuário e a senha para as próximas etapas.

   ![Chaves de acesso do Registro de Contêiner do Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a>Configurar o Maven para usar as chaves de acesso do Registro de Contêiner do Azure

1. Navegue até o diretório de projeto concluído para o seu aplicativo Spring Boot (por exemplo: "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou " */users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra o arquivo *pom.xml* com um editor de texto.

1. Atualize a coleção `<properties>` no arquivo *pom.xml* com a versão mais recente do [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) e o valor do servidor de logon e acesse as configurações para seu Registro de Contêiner do Azure da seção anterior deste tutorial. Por exemplo:

   ```xml
   <properties>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <username>wingtiptoysregistry</username>
      <password>{put your Azure Container Registry access key here}</password>
   </properties>
   ```

1. Adicione [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) à coleção `<plugins>` no arquivo *pom.xml*, especifique a imagem base em `<from>/<image>` e o nome da imagem final `<to>/<image>`, especifique o nome de usuário e a senha na seção anterior em `<to>/<auth>`. Por exemplo:

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
            <auth>
               <username>${username}</username>
               <password>${password}</password>
            </auth>
        </to>
     </configuration>
   </plugin>
   ```

1. Navegue até o diretório de projeto completo para o seu aplicativo Spring Boot e execute o seguinte comando para recompilar o aplicativo e fazer o push do contêiner ao Registro de Contêiner do Azure:

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> Quando você estiver usando o Jib para enviar por push sua imagem no Registro de Contêiner do Azure, a imagem não cumprirá o *Dockerfile*. Confira [este](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) documento para obter detalhes.
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Criar um aplicativo Web no Linux no Serviço de Aplicativo do Azure usando a imagem de contêiner

1. Navegue até o [portal do Azure] e conecte-se.

2. Clique no ícone do menu para **+ Criar um recurso** e, em seguida, clique em **Web** e em **Aplicativo Web para Contêineres**.
   
   ![Criar um aplicativo Web no portal do Azure][LX01]

3. Quando a página **Aplicativo Web no Linux** for exibida, insira as seguintes informações:

   a. Insira um nome exclusivo para o **Nome do aplicativo**, por exemplo: "*wingtiptoyslinux*"

   b. Escolha uma **Assinatura** na lista suspensa.

   c. Escolha um **Grupo de Recursos** existente ou especifique um nome para criar um novo grupo de recursos.

   d. Escolha *Linux* como o **SO**.

   e. Clique em **Plano do Serviço de Aplicativo/Local** e escolha um plano de serviço de aplicativo existente ou clique em **Criar** para criar um plano do serviço de aplicativo.

   f. Clique em **Configurar contêiner** e insira as seguintes informações:

   * Escolha **Contêiner Único** e **Registro de Contêiner do Azure**.

   * **Registro**: escolha o nome do contêiner criado anteriormente, por exemplo: "*wingtiptoysregistry*"

   * **Imagem**: escolha o nome da imagem, por exemplo: "*gs-spring-boot-docker*"
   
   * **Tag**: escolha a marca para a imagem, por exemplo: "*mais recente*"
   
   * **Arquivo de Inicialização**: deixe em branco, pois a imagem já tem o comando de inicialização
   
   e. Depois de ter inserido todas as informações acima, clique em **Aplicar**.

   ![Definir configurações do aplicativo Web][LX02]

4. Clique em **Criar**.

> [!NOTE]
>
> O Azure mapeará automaticamente as solicitações de Internet para o servidor Tomcat inserido que está em execução nas portas padrão 80 ou 8080. No entanto, se você tiver configurado seu servidor Tomcat inserido para ser executado em uma porta personalizada, precisará adicionar uma variável de ambiente ao seu aplicativo Web que defina a porta do servidor Tomcat inserido. Para fazer isso, execute as seguintes etapas:
>
> 1. Navegue até o [portal do Azure] e conecte-se.
> 
> 2. Clique no ícone dos **Serviços de Aplicativos** e selecione seu aplicativo Web na lista.
>
> 4. Clique em **Configuração**. (Item 1 na imagem abaixo.)
>
> 5. Na seção **Configurações do aplicativo**, adicione uma nova configuração chamada **PORTA** e insira seu número da porta personalizada para o valor. (Itens 2, 3, 4 na imagem abaixo.)
>
> 6. Clique em **Save** (Salvar). (Item 5 na imagem abaixo.)
>
> ![Como salvar um número da porta personalizado no portal do Azure][LX03]
>

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

Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.

> [!div class="nextstepaction"]
> [Spring no Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Recursos adicionais

Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:

* [Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure](deploy-spring-boot-java-web-app-on-azure.md)
* [Implantar um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Trabalhando com o Java e Azure DevOps].

Para obter mais detalhes sobre o Spring Boot no projeto de exemplo do Docker, consulte [Introdução ao Spring Boot no Docker].

Para obter ajuda na introdução a seus próprios aplicativos Spring Boot, confira **Spring Initializr** em https://start.spring.io/.

Para obter mais informações de introdução sobre como criar um aplicativo Spring Boot simples, consulte o Spring Initializr em https://start.spring.io/.

Para obter mais exemplos sobre como usar imagens personalizadas do Docker com o Azure, veja [Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux].

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure para desenvolvedores Java]: /java/azure/
[Portal do Azure]: https://portal.azure.com/
[Criar um registro de contêiner privado do Docker usando o portal do Azure]: /azure/container-registry/container-registry-get-started-portal
[Usando uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Trabalhando com o Java e Azure DevOps]: /azure/devops/java/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
