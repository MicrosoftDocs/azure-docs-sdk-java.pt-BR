---
title: Introdução às bibliotecas do Azure para Java
description: Saiba como criar recursos de nuvem do Azure, conectá-los e usá-los em seus aplicativos Java.
keywords: Azure, Java, SDK, API, autenticar, introdução
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: b1e10b79-f75e-4605-aecd-eed64873e2d3
ms.openlocfilehash: f069183c96cdc42d590d2e58a5a6a500be5ab69a
ms.sourcegitcommit: 720c2eaf66532d277015610ec375c71e934d9ee6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
ms.locfileid: "29065523"
---
# <a name="get-started-with-cloud-development-using-the-azure-libraries-for-java"></a><span data-ttu-id="270c5-104">Introdução ao desenvolvimento em nuvem usando as bibliotecas do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="270c5-104">Get started with cloud development using the Azure libraries for Java</span></span>

<span data-ttu-id="270c5-105">Este guia orienta em relação à configuração de um ambiente de desenvolvimento para o desenvolvimento do Azure em Java.</span><span class="sxs-lookup"><span data-stu-id="270c5-105">This guide walks you through setting up a development environment for Azure development in Java.</span></span> <span data-ttu-id="270c5-106">Você vai criar alguns recursos do Azure e conectá-los para executar algumas tarefas básicas, como carregar um arquivo ou implantar um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="270c5-106">You'll then create some Azure resources and connect them to to perform some basic tasks, like uploading a file or deploying a web application.</span></span> <span data-ttu-id="270c5-107">Quando terminar, você estará pronto para começar a usar os serviços do Azure em seus próprios aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="270c5-107">When you're done, you'll be ready to start using Azure services in your own Java applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="270c5-108">pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="270c5-108">Prerequisites</span></span>

- <span data-ttu-id="270c5-109">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="270c5-109">An Azure account.</span></span> <span data-ttu-id="270c5-110">Se você não tiver uma, [obtenha uma avaliação gratuita](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="270c5-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="270c5-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) ou [CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="270c5-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="270c5-112">[Java 8](https://www.azul.com/downloads/zulu/) (incluído no Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="270c5-112">[Java 8](https://www.azul.com/downloads/zulu/) (included in Azure Cloud Shell)</span></span>
- <span data-ttu-id="270c5-113">[Maven 3](http://maven.apache.org/download.cgi) (incluído no Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="270c5-113">[Maven 3](http://maven.apache.org/download.cgi) (included in Azure Cloud Shell)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="270c5-114">Configurar a autenticação</span><span class="sxs-lookup"><span data-stu-id="270c5-114">Set up authentication</span></span>

<span data-ttu-id="270c5-115">Seu aplicativo Java precisa ler e criar permissões em sua assinatura do Azure para executar o exemplo de código neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="270c5-115">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="270c5-116">Criar uma entidade de serviço e configurar seu aplicativo para ser executado com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="270c5-116">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="270c5-117">As entidades de serviço fornecem uma maneira de criar uma conta não interativa associada à sua identidade para a qual você concede apenas os privilégios que seu aplicativo precisa para ser executado.</span><span class="sxs-lookup"><span data-stu-id="270c5-117">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="270c5-118">[Criar uma entidade de serviço usando a CLI do Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) e capturar a saída.</span><span class="sxs-lookup"><span data-stu-id="270c5-118">[Create a service principal using the Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) and capture the output.</span></span> <span data-ttu-id="270c5-119">Forneça uma [senha segura](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) no argumento de senha, em vez de `MY_SECURE_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="270c5-119">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="270c5-120">A senha deve ter de 8 a 16 caracteres e satisfazer pelo menos 3 dos 4 critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="270c5-120">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="270c5-121">Incluir caracteres minúsculos</span><span class="sxs-lookup"><span data-stu-id="270c5-121">Include lowercase characters</span></span>
* <span data-ttu-id="270c5-122">Incluir caracteres maiúsculos</span><span class="sxs-lookup"><span data-stu-id="270c5-122">Include uppercase characters</span></span>
* <span data-ttu-id="270c5-123">Incluir números</span><span class="sxs-lookup"><span data-stu-id="270c5-123">Include numbers</span></span>
* <span data-ttu-id="270c5-124">Incluir um dos seguintes símbolos: @ # $ % ^ & \* - _ !</span><span class="sxs-lookup"><span data-stu-id="270c5-124">Include one of the following symbols: @ # $ % ^ & \* - _ !</span></span> <span data-ttu-id="270c5-125">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="270c5-125">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="270c5-126">?</span><span class="sxs-lookup"><span data-stu-id="270c5-126">?</span></span> <span data-ttu-id="270c5-127">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="270c5-127">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="270c5-128">O que lhe dá uma resposta no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="270c5-128">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="270c5-129">Em seguida, copie o seguinte em um arquivo de texto no seu sistema:</span><span class="sxs-lookup"><span data-stu-id="270c5-129">Next, copy the following into a text file on your system:</span></span>

```text
# sample management library properties file
subscription=ssssssss-ssss-ssss-ssss-ssssssssssss
client=cccccccc-cccc-cccc-cccc-cccccccccccc
key=kkkkkkkkkkkkkkkk
tenant=tttttttt-tttt-tttt-tttt-tttttttttttt
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

<span data-ttu-id="270c5-130">Substitua os quatro valores principais pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="270c5-130">Replace the top four values with the following:</span></span>

- <span data-ttu-id="270c5-131">assinatura: usar o valor *id* de `az account show` na CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="270c5-131">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="270c5-132">cliente: usar o valor *appId* da saída obtida de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="270c5-132">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="270c5-133">chave: usar o valor da *senha* da saída da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="270c5-133">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="270c5-134">locatário: usar o valor do *locatário* da saída da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="270c5-134">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="270c5-135">Salve esse arquivo em um local seguro no sistema onde o seu código possa lê-lo.</span><span class="sxs-lookup"><span data-stu-id="270c5-135">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="270c5-136">Você pode usar esse arquivo para um código futuro, então é recomendável armazená-lo em algum lugar externo ao aplicativo neste artigo.</span><span class="sxs-lookup"><span data-stu-id="270c5-136">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span>

<span data-ttu-id="270c5-137">Defina uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo de autenticação no seu shell.</span><span class="sxs-lookup"><span data-stu-id="270c5-137">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>   

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="270c5-138">Se estiver trabalhando em um ambiente Windows, adicione a variável às propriedades do sistema.</span><span class="sxs-lookup"><span data-stu-id="270c5-138">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="270c5-139">Abra uma janela do PowerShell com privilégios de administrador e, depois de substituir a segunda variável pelo caminho do seu arquivo, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="270c5-139">Open a PowerShell window with administrator privledges and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="270c5-140">Criar um novo projeto Maven</span><span class="sxs-lookup"><span data-stu-id="270c5-140">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="270c5-141">Este guia usa a ferramenta de compilação Maven para compilar e executar o exemplo de código, mas outras ferramentas de compilação como Gradle também funcionam com as bibliotecas do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="270c5-141">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="270c5-142">Crie um projeto Maven a partir da linha de comando em um novo diretório no seu sistema:</span><span class="sxs-lookup"><span data-stu-id="270c5-142">Create a Maven project from the command line in a new directory on your system:</span></span>

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=AzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

<span data-ttu-id="270c5-143">Isso cria um projeto Maven básico na pasta `testAzureApp`.</span><span class="sxs-lookup"><span data-stu-id="270c5-143">This creates a basic Maven project under the `testAzureApp` folder.</span></span> <span data-ttu-id="270c5-144">Adicione as seguintes entradas no projeto `pom.xml` para importar as bibliotecas usadas no exemplo de código neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="270c5-144">Add the following entries into the project `pom.xml` to import the libraries used in the sample code in this tutorial.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="270c5-145">Adicionar uma entrada `build` sob o elemento `project` de nível superior para usar o [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) para executar os exemplos:</span><span class="sxs-lookup"><span data-stu-id="270c5-145">Add a `build` entry under the top-level `project` element to use the [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) to run the samples:</span></span>

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.AzureApp</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
 ```
   
## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="270c5-146">Criar uma máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="270c5-146">Create a Linux virtual machine</span></span>

<span data-ttu-id="270c5-147">Crie um novo arquivo denominado `AzureApp.java` no diretório `src/main/java/com/fabirkam` do projeto e cole-o no seguinte bloco de código.</span><span class="sxs-lookup"><span data-stu-id="270c5-147">Create a new file named `AzureApp.java` in the project's `src/main/java/com/fabirkam` directory and paste in the following block of code.</span></span> <span data-ttu-id="270c5-148">Atualize as variáveis `userName` e `sshKey` com valores reais para a sua máquina.</span><span class="sxs-lookup"><span data-stu-id="270c5-148">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="270c5-149">O código cria uma nova VM do Linux com o nome `testLinuxVM` em um grupo de recursos `sampleResourceGroup` em execução na região Leste dos EUA do Azure.</span><span class="sxs-lookup"><span data-stu-id="270c5-149">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

```java
package com.fabrikam;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.WebApp;
import com.microsoft.azure.management.storage.StorageAccount;
import com.microsoft.azure.management.storage.SkuName;
import com.microsoft.azure.management.storage.StorageAccountKey;
import com.microsoft.azure.management.sql.SqlDatabase;
import com.microsoft.azure.management.sql.SqlServer;
import com.microsoft.azure.management.resources.fluentcore.arm.Region;
import com.microsoft.azure.management.resources.fluentcore.utils.SdkContext;

import com.microsoft.rest.LogLevel;

import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

import java.io.File;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class AzureApp {

    public static void main(String[] args) {

        final String userName = "YOUR_VM_USERNAME";
        final String sshKey = "YOUR_PUBLIC_SSH_KEY";

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));    
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();
           
            // create a Ubuntu virtual machine in a new resource group 
            VirtualMachine linuxVM = azure.virtualMachines().define("testLinuxVM")
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup("sampleVmResourceGroup")
                    .withNewPrimaryNetwork("10.0.0.0/24")
                    .withPrimaryPrivateIPAddressDynamic()
                    .withoutPrimaryPublicIPAddress()
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withUnmanagedDisks()
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();   

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

<span data-ttu-id="270c5-150">Execute o exemplo a partir da linha de comando:</span><span class="sxs-lookup"><span data-stu-id="270c5-150">Run the sample from the command line:</span></span>

```
mvn compile exec:java
```

<span data-ttu-id="270c5-151">Você verá algumas solicitações REST e respostas no console conforme o SDK faz as chamadas subjacentes para a API REST do Azure para configuração da máquina virtual e dos seus recursos.</span><span class="sxs-lookup"><span data-stu-id="270c5-151">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="270c5-152">Quando o programa for concluído, verifique se a máquina virtual em sua assinatura com a CLI do Azure 2.0:</span><span class="sxs-lookup"><span data-stu-id="270c5-152">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="270c5-153">Depois de verificar se o código funcionou, use a CLI para excluir a VM e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="270c5-153">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="270c5-154">Implantar um aplicativo Web a partir de um repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="270c5-154">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="270c5-155">Substitua o método principal em `AzureApp.java` pelo mostrado abaixo, atualizando a variável `appName` com um valor exclusivo antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="270c5-155">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="270c5-156">Esse código implanta um aplicativo Web a partir da ramificação `master` em um repositório GitHub público em um novo [Aplicativo Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) em execução no tipo de preços gratuito.</span><span class="sxs-lookup"><span data-stu-id="270c5-156">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

```java
    public static void main(String[] args) {
        try {

            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            final String appName = "YOUR_APP_NAME";

            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            WebApp app = azure.webApps().define(appName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleWebResourceGroup")
                    .withNewWindowsPlan(PricingTier.FREE_F1)
                    .defineSourceControl()
                    .withPublicGitRepository(
                            "https://github.com/Azure-Samples/app-service-web-java-get-started")
                    .withBranch("master")
                    .attach()
                    .create();

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
```

<span data-ttu-id="270c5-157">Execute o código como antes usando Maven:</span><span class="sxs-lookup"><span data-stu-id="270c5-157">Run the code as before using Maven:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="270c5-158">Abra um navegador apontado para o aplicativo usando a CLI:</span><span class="sxs-lookup"><span data-stu-id="270c5-158">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="270c5-159">Remova o aplicativo Web e o plano da sua assinatura depois de verificar a implantação.</span><span class="sxs-lookup"><span data-stu-id="270c5-159">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="270c5-160">Conectar-se a um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="270c5-160">Connect to an Azure SQL database</span></span>

<span data-ttu-id="270c5-161">Substitua o método principal atual em `AzureApp.java` pelo código abaixo, definindo um valor real para a variável `dbPassword`.</span><span class="sxs-lookup"><span data-stu-id="270c5-161">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="270c5-162">Esse código cria um novo banco de dados do SQL com uma regra de firewall permitindo o acesso remoto e, em seguida, se conecta a ele usando o driver JBDC do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="270c5-162">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

```java

    public static void main(String args[])
    {
        // create the db using the management libraries
        try {
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            final String adminUser = SdkContext.randomResourceName("db",8);
            final String sqlServerName = SdkContext.randomResourceName("sql",10);
            final String sqlDbName = SdkContext.randomResourceName("dbname",8);
            final String dbPassword = "YOUR_PASSWORD_HERE";


            SqlServer sampleSQLServer = azure.sqlServers().define(sqlServerName)
                            .withRegion(Region.US_EAST)
                            .withNewResourceGroup("sampleSqlResourceGroup")
                            .withAdministratorLogin(adminUser)
                            .withAdministratorPassword(dbPassword)
                            .withNewFirewallRule("0.0.0.0","255.255.255.255")
                            .create();

            SqlDatabase sampleSQLDb = sampleSQLServer.databases().define(sqlDbName).create();

            // assemble the connection string to the database
            final String domain = sampleSQLServer.fullyQualifiedDomainName();
            String url = "jdbc:sqlserver://"+ domain + ":1433;" +
                    "database=" + sqlDbName +";" +
                    "user=" + adminUser+ "@" + sqlServerName + ";" +
                    "password=" + dbPassword + ";" +
                    "encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";

            // connect to the database, create a table and insert a entry into it
            Connection conn = DriverManager.getConnection(url);

            String createTable = "CREATE TABLE CLOUD ( name varchar(255), code int);";
            String insertValues = "INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);";
            String selectValues = "SELECT * FROM CLOUD";
            Statement createStatement = conn.createStatement();
            createStatement.execute(createTable);
            Statement insertStatement = conn.createStatement();
            insertStatement.execute(insertValues);
            Statement selectStatement = conn.createStatement();
            ResultSet rst = selectStatement.executeQuery(selectValues);

            while (rst.next()) {
                System.out.println(rst.getString(1) + " "
                        + rst.getString(2));
            }


        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println(e.getStackTrace().toString());
        }
    }
```
<span data-ttu-id="270c5-163">Execute o exemplo a partir da linha de comando:</span><span class="sxs-lookup"><span data-stu-id="270c5-163">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="270c5-164">Depois limpe os recursos usando a CLI:</span><span class="sxs-lookup"><span data-stu-id="270c5-164">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="270c5-165">Gravar um blob em uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="270c5-165">Write a blob into a new storage account</span></span>

<span data-ttu-id="270c5-166">Substitua o método principal atual em `AzureApp.java` pelo código abaixo.</span><span class="sxs-lookup"><span data-stu-id="270c5-166">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="270c5-167">Esse código cria uma [conta de armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-introduction) e, em seguida, usa as bibliotecas de Armazenamento do Azure para Java para criar um novo arquivo de texto na nuvem.</span><span class="sxs-lookup"><span data-stu-id="270c5-167">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

```java
public static void main(String[] args) {

    try {

        // use the properties file with the service principal information to authenticate
        // change the name of the environment variable if you used a different name in the previous step
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
                .withLogLevel(LogLevel.BASIC)
                .authenticate(credFile)
                .withDefaultSubscription();

        // create a new storage account
        String storageAccountName = SdkContext.randomResourceName("st",8);
        StorageAccount storage = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleStorageResourceGroup")
                    .create();

        // create a storage container to hold the file
        List<StorageAccountKey> keys = storage.getKeys();
        final String storageConnection = "DefaultEndpointsProtocol=https;"
                + "AccountName=" + storage.name()
                + ";AccountKey=" + keys.get(0).value()
                + ";EndpointSuffix=core.windows.net";

        CloudStorageAccount account = CloudStorageAccount.parse(storageConnection);
        CloudBlobClient serviceClient = account.createCloudBlobClient();

        // Container name must be lower case.
        CloudBlobContainer container = serviceClient.getContainerReference("helloazure");
        container.createIfNotExists();

        // Make the container public
        BlobContainerPermissions containerPermissions = new BlobContainerPermissions();
        containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
        container.uploadPermissions(containerPermissions);

        // write a blob to the container
        CloudBlockBlob blob = container.getBlockBlobReference("helloazure.txt");
        blob.uploadText("hello Azure");

    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }
    }
}
```

<span data-ttu-id="270c5-168">Execute o exemplo a partir da linha de comando:</span><span class="sxs-lookup"><span data-stu-id="270c5-168">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="270c5-169">Você pode procurar o arquivo `helloazure.txt` em sua conta de armazenamento por meio do portal do Azure ou com o [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span><span class="sxs-lookup"><span data-stu-id="270c5-169">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="270c5-170">Limpar a conta de armazenamento usando a CLI:</span><span class="sxs-lookup"><span data-stu-id="270c5-170">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="270c5-171">Explorar mais exemplos</span><span class="sxs-lookup"><span data-stu-id="270c5-171">Explore more samples</span></span>

<span data-ttu-id="270c5-172">Para saber mais sobre como usar as bibliotecas de gerenciamento do Azure para Java para gerenciar recursos e automatizar tarefas, confira o nosso exemplo de código para [máquinas virtuais](java-sdk-azure-virtual-machine-samples.md), [aplicativos Web](java-sdk-azure-web-apps-samples.md) e [banco de dados SQL](java-sdk-azure-sql-database-samples.md) .</span><span class="sxs-lookup"><span data-stu-id="270c5-172">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](java-sdk-azure-virtual-machine-samples.md), [web apps](java-sdk-azure-web-apps-samples.md) and [SQL database](java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="270c5-173">Referência e notas de versão</span><span class="sxs-lookup"><span data-stu-id="270c5-173">Reference and release notes</span></span>

<span data-ttu-id="270c5-174">Uma [referência](http://docs.microsoft.com/java/api) está disponível para todos os pacotes.</span><span class="sxs-lookup"><span data-stu-id="270c5-174">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="270c5-175">Obter ajuda e fazer comentários</span><span class="sxs-lookup"><span data-stu-id="270c5-175">Get help and give feedback</span></span>

<span data-ttu-id="270c5-176">Poste perguntas para a comunidade no [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span><span class="sxs-lookup"><span data-stu-id="270c5-176">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="270c5-177">Relate bugs e problemas não resolvidos com as bibliotecas do Azure para Java no [projeto GitHub](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="270c5-177">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
