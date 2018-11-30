---
title: Como usar o Plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Registro de Contêiner do Azure ao Serviço de Aplicativo do Azure
description: Este tutorial percorrerá as etapas para implantar um aplicativo Spring Boot do Registro de Contêiner do Azure no Serviço de Aplicativo do Azure usando um plug-in do Maven.
services: container-registry
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: cc345987085e442978b59a45d6fc3e1b52160515
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338940"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a>Como usar o Plug-in do Maven para Aplicativos Web do Azure para implantar um aplicativo Spring Boot no Registro de Contêiner do Azure ao Serviço de Aplicativo do Azure

Este artigo demonstra como implantar um exemplo de aplicativo [Spring Boot] no Registro de Contêiner do Azure e, depois, usar o plug-in do Maven para Aplicativos Web do Azure a fim de implantar seu aplicativo nos Serviço de Aplicativo do Azure.

> [!NOTE]
> 
> O Plug-in do Maven para Aplicativos Web do Azure para [Apache Maven](http://maven.apache.org/) fornece uma integração perfeita do Serviço de Aplicativo do Azure em projetos Maven e simplifica o processo para os desenvolvedores implantarem aplicativos Web no Serviço de Aplicativo do Azure.
> 
> O plug-in do Maven para Aplicativos Web do Azure está disponível no momento como uma versão prévia. Por enquanto, há suporte somente para a publicação FTP, embora existam planos para recursos adicionais futuros.
> 

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
   git clone -b https://github.com/spring-guides/gs-spring-boot-docker
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

   ![Procurar aplicativo de exemplo localmente][SB01]

> [!NOTE]
>
> Quando você estiver usando o Docker localmente, verá um erro informando que não pode conectar o host local na porta 2375. Se isso acontecer, você precisará habilitar o uso do Docker localmente sem TLS. Para tanto, abra as configurações do Docker e marque a opção para **Expor o Daemon em TCP://localhost:2375 sem TLS**.
>
> ![Expor o daemon do Docker na porta TCP 2375 local][TL01]

## <a name="create-an-azure-service-principal"></a>Criar uma entidade de serviço do Azure

Nesta seção, você criará uma entidade de serviço do Azure que será usada pelo plug-in do Maven durante a implantação de seu contêiner no Azure.

1. Abra um prompt de comando.

2. Entre em sua conta do Azure usando a CLI do Azure:
   ```azurecli
   az login
   ```
   Siga as instruções na tela para concluir o processo de entrada.

3. Crie uma entidade de serviço do Azure:
   ```azurecli
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

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Criar um Registro de Contêiner do Azure usando a CLI do Azure

1. Abra um prompt de comando.

1. Faça logon na sua Conta do Azure:
   ```azurecli
   az login
   ```

1. Crie um grupo de recursos para os recursos do Azure usados neste artigo:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Substitua `wingtiptoysresources` neste exemplo por um nome exclusivo para o grupo de recursos.

1. Crie um registro de contêiner privado do Azure no grupo de recursos para seu aplicativo Spring Boot: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Substitua `wingtiptoysregistry` neste exemplo por um nome exclusivo para seu registro de contêiner.

1. Recupere a senha de seu registro de contêiner:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   O Azure responderá com sua senha; por exemplo:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a>Adicionar seu registro de contêiner do Azure e a entidade de serviço do Azure às suas configurações do Maven

1. Abra seu arquivo `settings.xml` do Maven em um editor de texto; esse arquivo pode estar em um caminho como os exemplos a seguir:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. Adicione as configurações de acesso do Registro de Contêiner do Azure da seção anterior deste artigo para a coleção `<servers>` no arquivo *settings.xml*; por exemplo:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Em que:

   |   Elemento    |                                 DESCRIÇÃO                                  |
   |--------------|------------------------------------------------------------------------------|
   |    `<id>`    |         Contém o nome de seu Registro de Contêiner privado do Azure.          |
   | `<username>` |         Contém o nome de seu Registro de Contêiner privado do Azure.          |
   | `<password>` | Contém a senha que você recuperou na seção anterior deste artigo. |


3. Adicione as configurações de sua entidade de serviço do Azure de uma seção anterior deste artigo à coleção `<servers>` no arquivo *settings.xml*; por exemplo:

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


4. Salve e feche o arquivo *settings.xml*.

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a>Compilar imagem de contêiner do Docker e enviá-la por push ao registro de contêiner do Azure

1. Navegue até o diretório de projeto completo para o seu aplicativo Spring Boot (por exemplo: "*C:\SpringBoot\gs-spring-boot-docker\complete*" ou "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") e abra o arquivo *pom.xml* com um editor de texto.

2. Atualize a coleção `<properties>` no arquivo *pom.xml* com o valor do servidor de logon para seu Registro de Contêiner do Azure da seção anterior deste tutorial. Por exemplo:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Em que:

   |           Elemento           |                                                                       DESCRIÇÃO                                                                       |
   |-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
   | `<azure.containerRegistry>` |                                              Especifica o nome de seu Registro de Contêiner privado do Azure.                                               |
   |   `<docker.image.prefix>`   | Especifica a URL de seu Registro de Contêiner privado do Azure, que é derivado acrescentando ".azurecr.io" ao nome de seu registro de contêiner privado. |


3. Verifique se `<plugin>` para o plug-in do Docker em seu arquivo *pom.xml* contém as propriedades corretas para o endereço do servidor de logon e nome do registro da etapa anterior neste tutorial. Por exemplo: 

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Em que:

   |     Elemento     |                                       DESCRIÇÃO                                       |
   |-----------------|-----------------------------------------------------------------------------------------|
   |  `<serverId>`   |  Especifica a propriedade que contém o nome de seu Registro de Contêiner privado do Azure.   |
   | `<registryUrl>` | Especifica a propriedade que contém a URL de seu Registro de Contêiner privado do Azure. |


4. Navegue até o diretório de projeto completo para o seu aplicativo Spring Boot e execute o seguinte comando para recompilar o aplicativo e fazer o push do contêiner ao registro de contêiner do Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

5. OPCIONAL: navegue até o [Portal do Azure] e verifique se há uma imagem de contêiner do Docker chamada **gs-spring-boot-docker** no registro do contêiner.

   ![Verificar o contêiner no Portal do Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a>Personalizar seu pom.xml e, depois, compilar e implantar o contêiner no Azure

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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
| `<resourceGroup>` | Especifica o grupo de recursos de destino, que é `wingtiptoysresources` neste exemplo. Esse grupo de recursos será criado durante a implantação, caso ainda não exista. |
| `<appName>` | Especifica o nome de destino de seu aplicativo Web. Neste exemplo, o nome de destino é `maven-linux-app-${maven.build.timestamp}`, no qual o sufixo `${maven.build.timestamp}` é acrescentado neste exemplo para evitar conflitos. (O carimbo de data/hora é opcional; você pode especificar qualquer cadeia de caracteres exclusiva para o nome do aplicativo). |
| `<region>` | Especifica a região de destino, que neste exemplo é `westus`. (Uma lista completa está disponível na documentação [Plug-in do Maven para aplicativos Web do Azure]). |
| `<containerSettings>` | Especifica as propriedades que contêm o nome e a URL de seu contêiner. |
| `<appSettings>` | Especifica quaisquer configurações exclusivas para o Maven usar ao implantar seu aplicativo Web no Azure. Neste exemplo, um elemento `<property>` contém um par de nome/valor de elementos filho que especifique a porta para o seu aplicativo. |

> [!NOTE]
>
> As configurações de alteração do número da porta neste exemplo só serão necessárias quando você estiver alterando a porta padrão.
>

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

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre as diversas tecnologias discutidas neste artigo, veja os artigos a seguir:

* [Plug-in do Maven para aplicativos Web do Azure]

* [Faça logon no Azure na CLI do Azure](/azure/xplat-cli-connect)

* [Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referência de configurações do Maven](https://maven.apache.org/settings.html)

* [Plug-in do Docker para o Maven]

<!-- URL List -->

[CLI (interface de linha de comando) do Azure]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portal do Azure]: https://portal.azure.com/
[Plug-in do Maven para aplicativos Web do Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Plug-in do Docker para o Maven]: https://github.com/spotify/docker-maven-plugin
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Introdução ao Spring Boot no Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
