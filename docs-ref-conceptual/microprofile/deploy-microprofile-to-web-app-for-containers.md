---
title: Implantar um serviço MicroProfile baseado em Java para o Aplicativo Web para Contêineres do Azure
description: Saiba como implantar um serviço MicroProfile usando o Docker e o Aplicativo Web para Contêineres do Azure
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533595"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a>Implantar um serviço MicroProfile baseado em Java para o Aplicativo Web para Contêineres do Azure

O MicroProfile é uma ótima maneira de compilar aplicativos Java extremamente pequenos que podem ser implantados com rapidez e facilidade em serviços, como o [Aplicativo Web para Contêineres do Azure](https://azure.microsoft.com/services/app-service/containers/). Neste tutorial, você criará um microsserviço simples baseado no MicroProfile que será colocado em um contêiner do Docker, implantado em uma [instância do Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry/) e, em seguida, hospedado usando o Aplicativo Web para Contêineres do Azure.

> [!NOTE]
> Este procedimento funciona com qualquer implementação do MicroProfile.io, desde que a imagem de contêiner do Docker seja autoexecutável (ou seja, a imagem inclui o tempo de execução).

Nesta amostra, você usará o [Payara Micro](https://www.payara.fish/payara_micro) e o [MicroProfile 1.3](https://microprofile.io/) para criar um arquivo WAR (requisito de aplicativo Web) Java pequeno (aproximadamente 5.000 bytes) e, em seguida, o empacotará em uma imagem do Docker de cerca de 174 MB (megabytes). A imagem do Docker contém tudo o que é necessário para uma implantação totalmente contida em contêiner do aplicativo Web.

Uma imagem inteira do Docker de 174 MB não precisa ser reimplantada sempre que o código-fonte do aplicativo é alterado, pois o Docker carrega apenas as diferenças (que são significativamente menores). Consequentemente, o processo de execução uma nova versão de um aplicativo do MicroProfile por meio de um pipeline de CI/CD é extremamente eficiente e rápido, reduzindo conflitos e possibilitando uma iteração rápida de desenvolvimento.

Você trabalhará neste tutorial primeiro criando e executando o código localmente e, em seguida, implantando-o como um aplicativo Web no Azure. Em ambas as fases, você poderá depender do Docker para simplificar e padronizar seus esforços. Antes de começar, você criará uma instância do Registro de Contêiner do Azure para armazenar seus contêineres do Docker.

## <a name="create-an-azure-container-registry-instance"></a>Criar uma instância do Registro de Contêiner do Azure

Você pode usar o [portal do Azure](http://portal.azure.com) para criar a instância do Registro de Contêiner do Azure, mas há outras opções também, como a CLI do Azure. Para criar uma instância do Registro de Contêiner do Azure, faça o seguinte:

1. Entre no [portal do Azure](http://portal.azure.com) e crie um recurso do Registro de Contêiner do Azure. Forneça um nome de registro (esse nome deve ser definido como a propriedade `docker.registry` no arquivo *pom.xml*). Altere os padrões, conforme desejado e, em seguida, selecione **Criar**.

1. Em aproximadamente 30 segundos, quando a instância do registro de contêiner estiver ativa, selecione a instância do registro de contêiner e, em seguida, no painel esquerdo, selecione o link **Chaves de acesso**. 

    Habilite a configuração *usuário administrador* para acessar essa instância do registro de contêiner nos computadores e enviar contêineres do Docker por push para ela. Essa ação também permite o acesso por meio da instância do Aplicativo Web para Contêineres do Azure que você configurará em breve.

1. No painel **Chaves de acesso**, copie os valores de **nome de usuário** e **senha** e cole-os no arquivo *settings.xml* global do Maven. Para obter mais informações sobre as configurações do Maven, acesse o site do [Projeto Apache Maven](https://maven.apache.org/settings.html). 

   Para referência, este é um exemplo do arquivo *${user.home}/.m2/settings.xml*:

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

Agora que você criou a instância do registro de contêiner, continue para criar e executar seu aplicativo do MicroProfile localmente.

## <a name="create-your-microprofile-application"></a>Criar seu aplicativo do MicroProfile

Este código de exemplo se baseia em um aplicativo de exemplo disponível no GitHub. Para clonar o código no computador, insira os seguintes comandos:

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

Esse diretório contém um arquivo *pom.xml* que você pode usar para especificar o projeto no formato que é usado pela ferramenta de build Maven. Edite o arquivo de acordo com suas necessidades. Em particular, as propriedades `docker.registry` e `docker.name` devem ser alteradas para as propriedades `docker.registry` e `docker.name` que foram criadas quando você configurou a instância do Registro de Contêiner do Azure.

Outro arquivo importante neste diretório é o Dockerfile, que é reproduzido abaixo:

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

O Dockerfile cria um contêiner do Docker com base no Contêiner do Docker do Payara Micro. Ele copia o arquivo WAR que foi criado como parte do processo de build. Também expõe a porta 8080 para que você possa acessar o serviço depois que ele estiver em funcionamento em um contêiner do Docker.

Ao abrir o diretório *src*, você acabará descobrindo a classe `Application` que é reproduzida aqui:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

A anotação *@ApplicationPath("/api")* especifica o ponto de extremidade base para esse microsserviço. Ou seja, para todos os pontos de extremidade, */api* precede o restante da URL necessária para acessar qualquer ponto de extremidade REST específico.

Dentro do pacote *api*, há uma classe chamada `API`, que contém o seguinte código:

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

Por meio do uso da anotação *@Path("/helloworld")* , você poderá ver que esse ponto de extremidade REST, quando combinado com a anotação */api* especificada na classe `Application`, será */api/helloworld*. Ao chamar esse ponto de extremidade usando uma solicitação HTTP GET, você verá que o método produzirá text/html e, na verdade, é simplesmente uma cadeia de caracteres embutida em código, "Olá, mundo!"

Até agora, este artigo abordou todo o código necessário para você criar um microsserviço usando o MicroProfile. Agora você pode usar o Maven para compilá-lo, colocá-lo em um contêiner do Docker e executá-lo localmente fazendo o seguinte:

1. Execute `mvn clean package` e aguarde até ele ser concluído.

1. Execute `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`. Por exemplo, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, em que *\<docker.registry>* é *jogilescr.azurecr.io* e *\<docker.name>* é *samples/docker-helloworld*.

1. Tente acessar [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) e [http://localhost:8080/health](http://localhost:8080/health) no navegador da Web. Se você vir a resposta esperada “Olá, mundo!” (e as informações relacionadas à integridade do ponto de extremidade [/health](http://localhost:8080/health)), isso indicará que você implantou com êxito o aplicativo do MicroProfile no computador local.

## <a name="push-the-container-to-the-azure-container-registry-instance"></a>Enviar o contêiner por push à instância do Registro de Contêiner do Azure

Agora que você compilou e executou com êxito seu aplicativo do MicroProfile no computador local, envie esse contêiner por push à instância do registro de contêiner. 

> [!NOTE]
> Embora este artigo use uma instância do Registro de Contêiner do Azure, qualquer instância do registro de contêiner deverá funcionar, desde que o arquivo *pom.xml* seja editado a fim de apontar para uma localização relevante.

1. Para limpar, compilar e criar uma imagem local do Docker, execute `mvn clean package`.
2. Para enviar o contêiner por push à instância do Registro de Contêiner do Azure, execute `mvn dockerfile:push`.

Agora você carregou sua imagem de contêiner do Docker na instância do Registro de Contêiner do Azure. No entanto, ela ainda não está em execução. Agora você precisa implantá-la em uma instância do Aplicativo Web para Contêineres do Azure. 

## <a name="create-an-azure-web-app-for-containers-instance"></a>Criar uma instância do Aplicativo Web para Contêineres do Azure

1. No [portal do Azure](http://portal.azure.com), no painel esquerdo, selecione **Web + Celular** e, em seguida, faça o seguinte:

   a. Especifique um nome. O nome se tornará a URL pública do aplicativo Web; portanto, é uma boa ideia escolher um nome que possa ser lembrado com facilidade. Você poderá adicionar um nome de domínio personalizado mais tarde, se desejar.

   b. Na seção **Configurar contêiner**, em **Origem da imagem**, selecione **Registro de Contêiner do Azure** e, em seguida, na lista suspensa, selecione a imagem correta.

   c. Não é necessário especificar nenhum valor no campo **Arquivo de Inicialização**.

1. Depois de criar a instância, selecione-a e, em seguida, selecione **Configurações de Aplicativo**. Em **Chave**, insira **WEBSITES_PORT** e, em **Valor**, insira **8080**. Essas configurações instruem o Azure sobre qual porta deverá ser exposta no contêiner e a mapeá-la para a porta 80 externamente.

1. (Opcional) Selecione o link **Contêiner do Docker** e, em seguida, habilite **Implantação Contínua**. Ao fazer isso, sempre que você atualizar a imagem da instância do registro de contêiner do Azure, ela será atualizada automaticamente na instância do Aplicativo Web para Contêineres do Azure.

1. Agora você deverá conseguir acessar as instâncias hospedadas no Azure em `http://<appname>.azurewebsites.net/microprofile/api/helloworld` e `http://<appname>.azurewebsites.net/health`.

## <a name="summary"></a>Resumo

Neste tutorial, você acompanhou o processo de criação de um microsserviço simples baseado no MicroProfile, colocou-o em um contêiner do Docker, executou-o localmente e publicou-o no Azure. Você pode estender seu microsserviço para fornecer funcionalidades adicionais úteis. Para obter mais informações, acesse [MicroProfile.io](https://microprofile.io/).
