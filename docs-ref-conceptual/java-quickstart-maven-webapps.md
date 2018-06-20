---
title: Implantar um aplicativo Web Java no Azure em cinco minutos com Maven | Microsoft Docs
description: Criar e implantar um aplicativo Java compilado com o Maven para o Azure
services: app-service\web
documentationcenter: ''
author: rloutlaw
manager: douge
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: routlaw
ms.openlocfilehash: 1adc0a104ba22bcd353664e68323165890e46c64
ms.sourcegitcommit: 30d502b3150fa14bcc1251f5f88c7c0dd83e531e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/12/2017
ms.locfileid: "22033628"
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a>Criar e implantar um aplicativo Java no Azure com Maven

Este guia de início rápido ajuda a criar e implantar um aplicativo Web Java simples para o [Serviço de Aplicativo do Azure](/azure/app-service/app-service-value-prop-what-is) em apenas alguns minutos usando o [Apache Maven](http://maven.apache.org) e a CLI do Azure.

## <a name="before-you-begin"></a>Antes de começar

Antes de começar, instale o seguinte:

- [Git](https://git-scm.com/)
- [Java 8](https://www.azul.com/downloads/zulu/)
- [Maven 3](http://maven.apache.org/download.cgi)
- [CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/install-az-cli2)

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="get-the-sample-code"></a>Obter o código de amostra

Clone o repositório de aplicativos de exemplo em seu computador local. O exemplo é um aplicativo JSP simples com uma configuração adicional Maven no projeto `pom.xml` para testar o aplicativo localmente e ajudar a implantar o exemplo para o Serviço de Aplicativo do Azure.

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a>Executar o aplicativo localmente

Abra um prompt de comando e use Maven para compilar o aplicativo e executá-lo em um contêiner Web [Tomcat](https://tomcat.apache.org) local. 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

Abra um navegador da Web e navegue até http://localhost:8080 para exibir o aplicativo:

  ![Saída de Hello World do aplicativo de exemplo de Java](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a>Fazer logon no Azure

Faça logon na CLI do Azure com `az login`. Este guia de início rápido usa a CLI para consultar e criar os recursos do Azure necessários para hospedar o aplicativo.
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos   

Crie um grupo de recursos com [az group create](/cli/azure/group#create). Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.

```azurecli
az group create --location "East US" --name myResourceGroup
```

Para ver os possíveis valores que podem ser usados para `---location`, use [az appservice list-locations](/cli/azure/appservice#list-locations)

## <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

Crie um **plano do Serviço de Aplicativo** [GRATUITO](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) usando [az appservice plan create](/cli/azure/appservice/plan#create). Os planos de Serviço de Aplicativo alocam recursos compartilhados em todos os aplicativos Web em execução no plano.


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

Quando o Plano do Serviço de Aplicativo estiver pronto, a CLI do Azure mostra informações semelhantes ao exemplo a seguir:

```json
{
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "location": "East US",
    "sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "tier": "Standard"
    },
    "status": "Ready",
    "type": "Microsoft.Web/serverfarms"
}
```


## <a name="create-a-web-app"></a>Criar um aplicativo Web

Criar um aplicativo Web que usa recursos do plano usando o comando [az webapp criar](/cli/azure/appservice/web#create) da CLI do Azure. A definição do aplicativo Web fornece um espaço para implantar o código e uma URL para acessar o aplicativo quando ele estiver em execução.

No comando abaixo, substitua o espaço reservado <appname> por seu próprio nome exclusivo de aplicativo. O <appname> é usado no site no nome do host padrão para o aplicativo Web. Se <appname> for não exclusivo, você receberá a mensagem de erro amigável "O site com o nome fornecido já existe".

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

Quando o aplicativo Web tiver sido criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir.1

```json
{
    "clientAffinityEnabled": true,
    "defaultHostName": "<appname>.azurewebsites.net",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<appname>",
    "isDefaultContainer": null,
    "kind": "app",
    "location": "East US",
    "name": "<app_name>",
    "repositorySiteName": "<app_name>",
    "reserved": true,
    "resourceGroup": "myResourceGroup",
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "state": "Running",
    "type": "Microsoft.Web/sites",
}
```

## <a name="configure-java-and-tomcat"></a>Configurar Java e Tomcat

Configurar o aplicativo Web para usar Java e Tomcat usando o comando [az webapp config](/cli/azure/appservice/web#config) da CLI do Azure. O exemplo a seguir configura o Serviço de Aplicativo para executar Java 8 e [Apache Tomcat 8.5](http://tomcat.apache.org/) para executar o aplicativo.

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a>Configurar Maven 

O `pom.xml` Maven de exemplo inclui a configuração para enviar o exemplo por FTP para o Azure, mas você precisará personalizá-lo para implantar seu próprio aplicativo Web. Recuperar as credenciais do seu Serviço de Aplicativo com [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):

```azurecli
az webapp deployment list-publishing-profiles  \
--name appname \ 
--resource-group myResourceGroup  \
--query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" 
```

```json
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "appname\\$appname"
  }
]
```

Substitua os espaços reservados no arquivo `az-settings.xml` pela senha, pelo nome de usuário e pelo nome de host do FTP da saída. Certifique-se de usar apenas um caractere `\` no nome de usuário em vez do valor de escape da saída da CLI.
   
```XML
...
    <server>
      <id>azure-hello-world</id>
      <username>appname\$appname</username>
      <password>aBcDeFgHiJkLmNoPqRsTuVwXyZ</password>
    </server>
...
   <configuration>
     <fromFile>${basedir}/target/AzureAppDemo-0.0.1-SNAPSHOT.war</fromFile>
     <url>ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot</url>
     <toFile>webapps/ROOT.war</toFile>
     <serverId>azure-hello-world</serverId>
   </configuration>
...
```

## <a name="deploy-the-sample-application"></a>Implantar o aplicativo de exemplo

Implantar com exemplo no Azure, usando o parâmetro `-s` Maven para usar a configuração no arquivo `az-settings.xml`.

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a>Navegar até o aplicativo Web

Exiba o exemplo em execução no Azure:

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a>Atualizar o aplicativo

Usando um editor de texto, abra `src/main/webapp/index.jsp` e substitua o JSP existente pelo abaixo.

```html
<%--
  Copyright (c) Microsoft Corporation. All rights reserved.
  Licensed under the MIT License. See License.txt in the project root for
  license information.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"  import="java.util.Date" %>
<html>
<head>
  <title>Azure Samples Hello World</title>
</head>
<body>
  <H1>Hello Azure!</H1>
   Current time is: <%= new Date() %>
</body>
</html>
```

Implantar a atualização com Maven:

```
mvn clean package
mvn install -s az-settings.xml
```

Atualize o navegador após a reimplantação do aplicativo para visualizar as alterações.

## <a name="manage-your-new-azure-app"></a>Gerenciar seu novo aplicativo do Azure

Vá para o portal do Azure para examinar o aplicativo Web que você acabou de criar.

Para fazer isso, entre em [https://portal.azure.com](https://portal.azure.com).

No menu à esquerda, clique em **Serviço de Aplicativo**, em seguida, clique no nome do seu aplicativo Web do Azure.

 ![Selecione o aplicativo na lista de aplicativos Web no portal](media/azure-app-service-portal.png)

Testar o monitoramento executando `curl` no aplicativo para enviar tráfego.

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

Você verá a atividade de solicitação no monitoramento depois de alguns minutos.

 ![Monitoramento no portal do Azure](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a>Limpar recursos

Para remover todos os recursos criados neste guia, execute o seguinte comando:

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a>Próximas etapas

Pesquise a lista completa de [exemplos de Java do Azure](https://azure.microsoft.com/resources/samples/?term=java).