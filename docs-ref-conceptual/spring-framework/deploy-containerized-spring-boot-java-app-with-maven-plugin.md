---
title: Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure
description: Saiba como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: d9f2cf5c15bb8f990c8e82fddd6455ecbf8cc02c
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090759"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a>Como usar o plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot em contêineres no Azure

Este artigo demonstra como usar o [plug-in do Maven para Aplicativos Web do Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) a fim de implantar um exemplo de aplicativo Spring Boot em um contêiner do Docker para os Serviços de Aplicativos do Azure.

> [!NOTE]
> 
> O Plug-in do Maven para Aplicativos Web do Azure para [Apache Maven](http://maven.apache.org/) fornece uma integração perfeita do Serviço de Aplicativo do Azure em projetos Maven e simplifica o processo para os desenvolvedores implantarem aplicativos Web no Serviço de Aplicativo do Azure.
> 
> O plug-in do Maven para Aplicativos Web do Azure está disponível no momento como uma versão prévia. Por enquanto, há suporte somente para a publicação FTP, embora existam planos para recursos adicionais futuros.
> 

## <a name="prerequisites"></a>pré-requisitos

Para concluir as etapas deste tutorial, você precisa ter os seguintes pré-requisitos:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].
* A[CLI (interface de linha de comando) do Azure].
* Um JDK (Java Development Kit) versão 1.7 ou posterior atualizado.
* A ferramenta de compilação [Maven] do Apache (Versão 3).
* Um cliente [Git].
* Um cliente do [Docker].

> [!NOTE]
>
> Devido aos requisitos de virtualização deste tutorial, você não pode seguir as etapas neste artigo em uma máquina virtual. Você deve usar um computador físico com recursos de virtualização habilitados.
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a>Clonar o exemplo de Spring Boot no aplicativo Web do Docker

Nesta seção, você clonará um aplicativo Spring Boot em contêineres e o testará localmente.

1. Abra um prompt de comando ou janela de terminal e crie um diretório local para conter o aplicativo Spring Boot, e altere para esse diretório; por exemplo:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- ou --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clone o exemplo de projeto [Introdução ao Spring Boot no Docker] para o diretório criado. Por exemplo:
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. Altere o diretório para o projeto concluído. Por exemplo:
   ```shell
   cd gs-spring-boot-docker/complete
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

1. Você verá a seguinte mensagem exibida: **Olá, Mundo Docker**

## <a name="create-an-azure-service-principal"></a>Criar uma entidade de serviço do Azure

Nesta seção, você criará uma entidade de serviço do Azure que será usada pelo plug-in do Maven durante a implantação de seu contêiner no Azure.

1. Abra um prompt de comando.

2. Entre em sua conta do Azure usando a CLI do Azure:
   ```shell
   az login
   ```
   Siga as instruções na tela para concluir o processo de entrada.

3. Crie uma entidade de serviço do Azure:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Em que:

   | Parâmetro  |                    DESCRIÇÃO                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | Especifica o nome de usuário para a entidade de serviço. |
   | `pppppppp` | Especifica a senha para a entidade de serviço.  |


4. O Azure responde com um JSON parecido com o exemplo a seguir:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Você usará os valores dessa resposta em JSON ao configurar o plug-in do Maven para implantar seu contêiner no Azure, . `aaaaaaaa`, `uuuuuuuu`, `pppppppp` e `tttttttt` são valores de espaço reservado, usados neste exemplo para facilitar o mapeamento desses valores para seus respectivos elementos durante a configuração de seu arquivo `settings.xml` do Maven na próxima seção.
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a>Configurar o Maven para usar a entidade de serviço do Azure

Nesta seção, você usará os valores de sua entidade de serviço do Azure para configurar a autenticação usada pelo Maven durante a implantação de seu contêiner no Azure.

1. Abra seu arquivo `settings.xml` do Maven em um editor de texto; esse arquivo pode estar em um caminho como os exemplos a seguir:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. Adicione as configurações de sua entidade de serviço do Azure da seção anterior deste tutorial à coleção `<servers>` no arquivo *settings.xml*; por exemplo:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Em que:

   |     Elemento     |                                                                                   DESCRIÇÃO                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                Especifica um nome exclusivo usado pelo Maven para analisar suas configurações de segurança durante a implantação de seu aplicativo Web no Azure.                                |
   |   `<client>`    |                                                             Contém o valor `appId` de sua entidade de serviço.                                                             |
   |   `<tenant>`    |                                                            Contém o valor `tenant` de sua entidade de serviço.                                                             |
   |     `<key>`     |                                                           Contém o valor `password` de sua entidade de serviço.                                                            |
   | `<environment>` | Define o ambiente de nuvem do Azure de destino, que é `AZURE` neste exemplo. (Uma lista completa dos ambientes está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure]) |


3. Salve e feche o arquivo *settings.xml*.

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a>OPCIONAL: Implantar o arquivo local do Docker no Hub do Docker

Se você tiver uma conta do Docker, poderá compilar sua imagem de contêiner do Docker localmente e enviá-la por push ao Hub do Docker. Para fazer isso, use as seguintes etapas.

1. Abra o arquivo `pom.xml` de seu aplicativo Spring Boot em um editor de texto.

1. Localize o elemento filho `<imageName>` do elemento `<containerSettings>`.

1. Atualize o valor `${docker.image.prefix}` com o nome de sua conta do Docker:
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. Escolha um dos seguintes métodos de implantação:

   * Compile sua imagem de contêiner localmente com o Maven, e use o Docker para enviar seu contêiner por push para o Hub do Docker:
      ```shell
      mvn clean package docker:build
      docker push
      ```

   * Se o [Plug-in do Docker para o Maven] estiver instalado, você poderá compilar automaticamente a imagem de seu contêiner no Hub do Docker usando o parâmetro `-DpushImage`:
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a>OPCIONAL: Personalizar seu pom.xml antes de implantar seu contêiner no Azure

Abra o arquivo `pom.xml` de seu aplicativo Spring Boot em um editor de texto e localize o elemento `<plugin>` para `azure-webapp-maven-plugin`. Esse elemento deverá se parecer com este exemplo:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Você pode modificar diversos valores do plug-in do Maven, e há uma descrição detalhada de cada um desses elementos disponível na documentação [Plug-in do Maven para aplicativos Web do Azure]. Dito isso, vale a pena destacar diversos valores neste artigo:

| Elemento | DESCRIÇÃO |
|---|---|
| `<version>` | Especifica a versão do [Plug-in do Maven para aplicativos Web do Azure]. Você deve verificar a versão listada no [Repositório Central do Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) para garantir que esteja usando a versão mais recente. |
| `<authentication>` | Especifica as informações de autenticação do Azure, que, neste exemplo, contêm um elemento `<serverId>` contendo `azure-auth`; o Maven usa esse valor para procurar os valores de entidade de serviço do Azure em seu arquivo *settings.xml* do Maven, que você definiu em uma seção anterior deste artigo. |
| `<resourceGroup>` | Especifica o grupo de recursos de destino, que é `maven-plugin` neste exemplo. Esse grupo de recursos será criado durante a implantação, caso ainda não exista. |
| `<appName>` | Especifica o nome de destino de seu aplicativo Web. Neste exemplo, o nome de destino é `maven-linux-app-${maven.build.timestamp}`, no qual o sufixo `${maven.build.timestamp}` é acrescentado neste exemplo para evitar conflitos. (O carimbo de data/hora é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo). |
| `<region>` | Especifica a região de destino, que neste exemplo é `westus`. (Uma lista completa está disponível na documentação [Plug-in do Maven para Aplicativos Web do Azure]) |
| `<appSettings>` | Especifica quaisquer configurações exclusivas para o Maven usar ao implantar seu aplicativo Web no Azure. Neste exemplo, um elemento `<property>` contém um par de nome/valor de elementos filho que especifique a porta para o seu aplicativo. |

> [!NOTE]
>
> As configurações de alteração do número da porta neste exemplo só serão necessárias quando você estiver alterando a porta padrão.
>

## <a name="build-and-deploy-your-container-to-azure"></a>Compilar e implantar o contêiner no Azure

Depois de definir todas as configurações nas seções anteriores deste artigo, você estará pronto para implantar seu contêiner no Azure. Para fazer isso, execute as seguintes etapas:

1. Do prompt de comando ou janela de terminal que você estava usando antes, recompile o arquivo JAR usando o Maven, se você tiver feito alterações no arquivo *pom.xml*; por exemplo:
   ```shell
   mvn clean package
   ```

1. Implante seu aplicativo Web no Azure usando o Maven; por exemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

O Maven implantará seu aplicativo Web no Azure; se o aplicativo web ainda não existir, ele será criado.

> [!NOTE]
>
> Se a região que você especificou no elemento `<region>` de seu arquivo *pom.xml* não tiver servidores suficientes disponíveis no início de sua implantação, talvez você veja um erro semelhante ao exemplo a seguir:
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> Se isso acontecer, especifique outra região e execute novamente o comando do Maven para implantar seu aplicativo.
>
>

Após a implantação de sua Web, você poderá gerenciá-la usando o [Portal do Azure].

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

* [Faça logon no Azure na CLI do Azure](/azure/xplat-cli-connect)

* [Como usar o Plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure](deploy-spring-boot-java-app-with-maven-plugin.md)

* [Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referência de configurações do Maven](https://maven.apache.org/settings.html)

* [Plug-in do Docker para o Maven]

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portal do Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Plug-in do Docker para o Maven]: https://github.com/spotify/docker-maven-plugin
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Benefícios do assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Plug-in do Maven para aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP02.png
