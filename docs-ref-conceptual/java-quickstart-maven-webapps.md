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
ms.openlocfilehash: 70b508118c50b75693e2d746dc1e2919c827cb29
ms.sourcegitcommit: 0f38ef9ad64cffdb7b2e9e966224dfd0af251b0f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703539"
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a><span data-ttu-id="8d6d8-103">Criar e implantar um aplicativo Java no Azure com Maven</span><span class="sxs-lookup"><span data-stu-id="8d6d8-103">Create and deploy a Java app to Azure with Maven</span></span>

<span data-ttu-id="8d6d8-104">Este guia de início rápido ajuda a criar e implantar um aplicativo Web Java simples para o [Serviço de Aplicativo do Azure](/azure/app-service/app-service-value-prop-what-is) em apenas alguns minutos usando o [Apache Maven](http://maven.apache.org) e a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-104">This quickstart helps you create and deploy a simple Java web app to [Azure App Service](/azure/app-service/app-service-value-prop-what-is) in just a few minutes using [Apache Maven](http://maven.apache.org) and the Azure CLI.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8d6d8-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8d6d8-105">Before you begin</span></span>

<span data-ttu-id="8d6d8-106">Antes de começar, instale o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8d6d8-106">Before you start, set up the following:</span></span>

- [<span data-ttu-id="8d6d8-107">Git</span><span class="sxs-lookup"><span data-stu-id="8d6d8-107">Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="8d6d8-108">Java 8</span><span class="sxs-lookup"><span data-stu-id="8d6d8-108">Java 8</span></span>](https://www.azul.com/downloads/zulu/)
- [<span data-ttu-id="8d6d8-109">Maven 3</span><span class="sxs-lookup"><span data-stu-id="8d6d8-109">Maven 3</span></span>](http://maven.apache.org/download.cgi)
- [<span data-ttu-id="8d6d8-110">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d8-110">Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-az-cli2)

<span data-ttu-id="8d6d8-111">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="8d6d8-112">Obter o código de amostra</span><span class="sxs-lookup"><span data-stu-id="8d6d8-112">Get the sample code</span></span>

<span data-ttu-id="8d6d8-113">Clone o repositório de aplicativos de exemplo em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-113">Clone the sample app repository to your local machine.</span></span> <span data-ttu-id="8d6d8-114">O exemplo é um aplicativo JSP simples com uma configuração adicional Maven no projeto `pom.xml` para testar o aplicativo localmente e ajudar a implantar o exemplo para o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-114">The sample is a simple JSP application with additional Maven configuration in the project `pom.xml` to test the app locally and help deploy the sample to Azure App Service.</span></span>

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a><span data-ttu-id="8d6d8-115">Executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="8d6d8-115">Run the app locally</span></span>

<span data-ttu-id="8d6d8-116">Abra um prompt de comando e use Maven para compilar o aplicativo e executá-lo em um contêiner Web [Tomcat](https://tomcat.apache.org) local.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-116">Open a command prompt and use Maven to build the app and run it in a local [Tomcat](https://tomcat.apache.org) web container.</span></span> 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

<span data-ttu-id="8d6d8-117">Abra um navegador da Web e navegue até http://localhost:8080 para visualizar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8d6d8-117">Open a web browser and navigate to http://localhost:8080 to preview the app:</span></span>

  ![Saída de Hello World do aplicativo de exemplo de Java](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="8d6d8-119">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d8-119">Log in to Azure</span></span>

<span data-ttu-id="8d6d8-120">Faça logon na CLI do Azure com `az login`.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-120">Log in to the Azure CLI with `az login`.</span></span> <span data-ttu-id="8d6d8-121">Este guia de início rápido usa a CLI para consultar e criar os recursos do Azure necessários para hospedar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-121">This quickstart uses the CLI to query and create the Azure resources needed to host the app.</span></span>
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="8d6d8-122">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8d6d8-122">Create a resource group</span></span>   

<span data-ttu-id="8d6d8-123">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8d6d8-123">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8d6d8-124">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-124">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

```azurecli
az group create --location "East US" --name myResourceGroup
```

<span data-ttu-id="8d6d8-125">Para ver os possíveis valores que podem ser usados para `---location`, use [az appservice list-locations](/cli/azure/appservice#list-locations)</span><span class="sxs-lookup"><span data-stu-id="8d6d8-125">To see other possible values you can use for `---location`, use [az appservice list-locations](/cli/azure/appservice#list-locations)</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="8d6d8-126">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8d6d8-126">Create an App Service plan</span></span>

<span data-ttu-id="8d6d8-127">Crie um **plano do Serviço de Aplicativo** [GRATUITO](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) usando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="8d6d8-127">Create a **FREE** [App Service plan](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) using [az appservice plan create](/cli/azure/appservice/plan#create).</span></span> <span data-ttu-id="8d6d8-128">Os planos de Serviço de Aplicativo alocam recursos compartilhados em todos os aplicativos Web em execução no plano.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-128">App Service plans allocate resources shared across all web apps running in the plan.</span></span>


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="8d6d8-129">Quando o Plano do Serviço de Aplicativo estiver pronto, a CLI do Azure mostra informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d6d8-129">When the App Service Plan is ready, the Azure CLI shows information similar to the following example:</span></span>

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


## <a name="create-a-web-app"></a><span data-ttu-id="8d6d8-130">Criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="8d6d8-130">Create a web app</span></span>

<span data-ttu-id="8d6d8-131">Criar um aplicativo Web que usa recursos do plano usando o comando [az webapp criar](/cli/azure/appservice/web#create) da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-131">Create a web app that uses the plan's resources using the Azure CLI [az webapp create](/cli/azure/appservice/web#create) command.</span></span> <span data-ttu-id="8d6d8-132">A definição do aplicativo Web fornece um espaço para implantar o código e uma URL para acessar o aplicativo quando ele estiver em execução.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-132">The web app definition provides a space to deploy the code to and a URL to access the app once it's running.</span></span>

<span data-ttu-id="8d6d8-133">No comando abaixo, substitua o espaço reservado <appname> por seu próprio nome exclusivo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-133">In the command below substitute your own unique app name where you see the <appname> placeholder.</span></span> <span data-ttu-id="8d6d8-134">O <appname> é usado no site no nome do host padrão para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-134">The <appname> is used in the default hostname for the web app.</span></span> <span data-ttu-id="8d6d8-135">Se <appname> for não exclusivo, você receberá a mensagem de erro amigável "O site com o nome fornecido já existe".</span><span class="sxs-lookup"><span data-stu-id="8d6d8-135">If <appname> is not unique, you get the friendly error message "Website with given name already exists."</span></span>

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

<span data-ttu-id="8d6d8-136">Quando o aplicativo Web tiver sido criado, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir.1</span><span class="sxs-lookup"><span data-stu-id="8d6d8-136">When the Web App has been created, the Azure CLI shows information similar to the following example.1</span></span>

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

## <a name="configure-java-and-tomcat"></a><span data-ttu-id="8d6d8-137">Configurar Java e Tomcat</span><span class="sxs-lookup"><span data-stu-id="8d6d8-137">Configure Java and Tomcat</span></span>

<span data-ttu-id="8d6d8-138">Configurar o aplicativo Web para usar Java e Tomcat usando o comando [az webapp config](/cli/azure/appservice/web#config) da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-138">Configure the web app to use Java and Tomcat using the Azure CLI's [az webapp config](/cli/azure/appservice/web#config) command.</span></span> <span data-ttu-id="8d6d8-139">O exemplo a seguir configura o Serviço de Aplicativo para executar Java 8 e [Apache Tomcat 8.5](http://tomcat.apache.org/) para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-139">The example below configures App Service to run Java 8 and [Apache Tomcat 8.5](http://tomcat.apache.org/) to run the app.</span></span>

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a><span data-ttu-id="8d6d8-140">Configurar Maven</span><span class="sxs-lookup"><span data-stu-id="8d6d8-140">Configure Maven</span></span> 

<span data-ttu-id="8d6d8-141">O `pom.xml` Maven de exemplo inclui a configuração para enviar o exemplo por FTP para o Azure, mas você precisará personalizá-lo para implantar seu próprio aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-141">The sample's Maven `pom.xml` includes configuration to FTP the sample into Azure, but you'll need to customize it to deploy to your own web app.</span></span> <span data-ttu-id="8d6d8-142">Recupere as credenciais do seu Serviço de Aplicativo com [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span><span class="sxs-lookup"><span data-stu-id="8d6d8-142">Retreive your App Service credentials with [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span></span>

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

<span data-ttu-id="8d6d8-143">Substitua os espaços reservados no arquivo `az-settings.xml` pela senha, pelo nome de usuário e pelo nome de host do FTP da saída.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-143">Replace the placeholders in the `az-settings.xml` file with password, username, and FTP hostname from the output.</span></span> <span data-ttu-id="8d6d8-144">Certifique-se de usar apenas um caractere `\` no nome de usuário em vez do valor de escape da saída da CLI.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-144">Make sure to only use one `\` character in the username instead of the escaped value from the CLI output.</span></span>
   
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

## <a name="deploy-the-sample-application"></a><span data-ttu-id="8d6d8-145">Implantar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="8d6d8-145">Deploy the sample application</span></span>

<span data-ttu-id="8d6d8-146">Implantar com exemplo no Azure, usando o parâmetro `-s` Maven para usar a configuração no arquivo `az-settings.xml`.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-146">Deploy with sample to Azure, using Maven's `-s` parameter to use the configuration in the `az-settings.xml` file.</span></span>

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a><span data-ttu-id="8d6d8-147">Navegar até o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="8d6d8-147">Browse to web app</span></span>

<span data-ttu-id="8d6d8-148">Exiba o exemplo em execução no Azure:</span><span class="sxs-lookup"><span data-stu-id="8d6d8-148">View the sample running in Azure:</span></span>

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a><span data-ttu-id="8d6d8-149">Atualizar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="8d6d8-149">Update the app</span></span>

<span data-ttu-id="8d6d8-150">Usando um editor de texto, abra `src/main/webapp/index.jsp` e substitua o JSP existente pelo abaixo.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-150">Using a text editor, open `src/main/webapp/index.jsp`, and replace the existing JSP with the one below.</span></span>

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

<span data-ttu-id="8d6d8-151">Implantar a atualização com Maven:</span><span class="sxs-lookup"><span data-stu-id="8d6d8-151">Deploy the update with Maven:</span></span>

```
mvn clean package
mvn install -s az-settings.xml
```

<span data-ttu-id="8d6d8-152">Atualize o navegador após a reimplantação do aplicativo para visualizar as alterações.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-152">Refresh your browser after the app redeploys to view your changes.</span></span>

## <a name="manage-your-new-azure-app"></a><span data-ttu-id="8d6d8-153">Gerenciar seu novo aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="8d6d8-153">Manage your new Azure app</span></span>

<span data-ttu-id="8d6d8-154">Vá para o portal do Azure para examinar o aplicativo Web que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-154">Go to the Azure portal to take a look at the web app you just created.</span></span>

<span data-ttu-id="8d6d8-155">Para fazer isso, conecte [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8d6d8-155">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="8d6d8-156">No menu à esquerda, clique em **Serviço de Aplicativo**, em seguida, clique no nome do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-156">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

 ![Selecione o aplicativo na lista de aplicativos Web no portal](media/azure-app-service-portal.png)

<span data-ttu-id="8d6d8-158">Testar o monitoramento executando `curl` no aplicativo para enviar tráfego.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-158">Test the monitoring by running `curl` against the app to send some traffic.</span></span>

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

<span data-ttu-id="8d6d8-159">Você verá a atividade de solicitação no monitoramento depois de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="8d6d8-159">You'll see the request activity in the monitoring after a couple of minutes.</span></span>

 ![Monitoramento no portal do Azure](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a><span data-ttu-id="8d6d8-161">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="8d6d8-161">Clean up resources</span></span>

<span data-ttu-id="8d6d8-162">Para remover todos os recursos criados neste guia, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8d6d8-162">To remove all the resources created in this guide, run the following command:</span></span>

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8d6d8-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8d6d8-163">Next steps</span></span>

<span data-ttu-id="8d6d8-164">Pesquise a lista completa de [exemplos de Java do Azure](https://azure.microsoft.com/resources/samples/?term=java).</span><span class="sxs-lookup"><span data-stu-id="8d6d8-164">Browse the full list of [Azure Java samples](https://azure.microsoft.com/resources/samples/?term=java).</span></span>
