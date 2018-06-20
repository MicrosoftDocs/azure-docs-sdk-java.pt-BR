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
# <a name="get-started-with-cloud-development-using-the-azure-libraries-for-java"></a>Introdução ao desenvolvimento em nuvem usando as bibliotecas do Azure para Java

Este guia orienta em relação à configuração de um ambiente de desenvolvimento para o desenvolvimento do Azure em Java. Você vai criar alguns recursos do Azure e conectá-los para executar algumas tarefas básicas, como carregar um arquivo ou implantar um aplicativo Web. Quando terminar, você estará pronto para começar a usar os serviços do Azure em seus próprios aplicativos Java.

## <a name="prerequisites"></a>pré-requisitos

- Uma conta do Azure. Se você não tiver uma, [obtenha uma avaliação gratuita](https://azure.microsoft.com/free/)
- [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) ou [CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).
- [Java 8](https://www.azul.com/downloads/zulu/) (incluído no Azure Cloud Shell)
- [Maven 3](http://maven.apache.org/download.cgi) (incluído no Azure Cloud Shell)

## <a name="set-up-authentication"></a>Configurar a autenticação

Seu aplicativo Java precisa ler e criar permissões em sua assinatura do Azure para executar o exemplo de código neste tutorial. Criar uma entidade de serviço e configurar seu aplicativo para ser executado com suas credenciais. As entidades de serviço fornecem uma maneira de criar uma conta não interativa associada à sua identidade para a qual você concede apenas os privilégios que seu aplicativo precisa para ser executado.

[Criar uma entidade de serviço usando a CLI do Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) e capturar a saída. Forneça uma [senha segura](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) no argumento de senha, em vez de `MY_SECURE_PASSWORD`. A senha deve ter de 8 a 16 caracteres e satisfazer pelo menos 3 dos 4 critérios a seguir:

* Incluir caracteres minúsculos
* Incluir caracteres maiúsculos
* Incluir números
* Incluir um dos seguintes símbolos: @ # $ % ^ & * - _ ! + = [ ] { } | \ : ‘ , . ? / ` ~ “ ( ) ;


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

O que lhe dá uma resposta no seguinte formato:

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

Em seguida, copie o seguinte em um arquivo de texto no seu sistema:

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

Substitua os quatro valores principais pelo seguinte:

- assinatura: usar o valor *id* de `az account show` na CLI do Azure 2.0.
- cliente: usar o valor *appId* da saída obtida de uma entidade de serviço.
- chave: usar o valor da *senha* da saída da entidade de serviço.
- locatário: usar o valor do *locatário* da saída da entidade de serviço.

Salve esse arquivo em um local seguro no sistema onde o seu código possa lê-lo. Você pode usar esse arquivo para um código futuro, então é recomendável armazená-lo em algum lugar externo ao aplicativo neste artigo.

Defina uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo de autenticação no seu shell.   

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Se estiver trabalhando em um ambiente Windows, adicione a variável às propriedades do sistema. Abra uma janela do PowerShell com privilégios de administrador e, depois de substituir a segunda variável pelo caminho do seu arquivo, insira o seguinte comando:

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="create-a-new-maven-project"></a>Criar um novo projeto Maven

> [!NOTE]
> Este guia usa a ferramenta de compilação Maven para compilar e executar o exemplo de código, mas outras ferramentas de compilação como Gradle também funcionam com as bibliotecas do Azure para Java. 

Crie um projeto Maven a partir da linha de comando em um novo diretório no seu sistema:

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=AzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

Isso cria um projeto Maven básico na pasta `testAzureApp`. Adicione as seguintes entradas no projeto `pom.xml` para importar as bibliotecas usadas no exemplo de código neste tutorial.

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

Adicionar uma entrada `build` sob o elemento `project` de nível superior para usar o [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) para executar os exemplos:

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
   
## <a name="create-a-linux-virtual-machine"></a>Criar uma máquina virtual Linux

Crie um novo arquivo denominado `AzureApp.java` no diretório `src/main/java/com/fabirkam` do projeto e cole-o no seguinte bloco de código. Atualize as variáveis `userName` e `sshKey` com valores reais para a sua máquina. O código cria uma nova VM do Linux com o nome `testLinuxVM` em um grupo de recursos `sampleResourceGroup` em execução na região Leste dos EUA do Azure.

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

Execute o exemplo a partir da linha de comando:

```
mvn compile exec:java
```

Você verá algumas solicitações REST e respostas no console conforme o SDK faz as chamadas subjacentes para a API REST do Azure para configuração da máquina virtual e dos seus recursos. Quando o programa for concluído, verifique se a máquina virtual em sua assinatura com a CLI do Azure 2.0:

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

Depois de verificar se o código funcionou, use a CLI para excluir a VM e seus recursos.

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Implantar um aplicativo Web a partir de um repositório GitHub

Substitua o método principal em `AzureApp.java` pelo mostrado abaixo, atualizando a variável `appName` com um valor exclusivo antes de executar o código. Esse código implanta um aplicativo Web a partir da ramificação `master` em um repositório GitHub público em um novo [Aplicativo Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) em execução no tipo de preços gratuito.

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

Execute o código como antes usando Maven:

```
mvn clean compile exec:java
```

Abra um navegador apontado para o aplicativo usando a CLI:

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

Remova o aplicativo Web e o plano da sua assinatura depois de verificar a implantação.

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a>Conectar-se a um banco de dados SQL do Azure

Substitua o método principal atual em `AzureApp.java` pelo código abaixo, definindo um valor real para a variável `dbPassword`.
Esse código cria um novo banco de dados do SQL com uma regra de firewall permitindo o acesso remoto e, em seguida, se conecta a ele usando o driver JBDC do Banco de Dados SQL. 

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
Execute o exemplo a partir da linha de comando:

```
mvn clean compile exec:java
```

Depois limpe os recursos usando a CLI:

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a>Gravar um blob em uma nova conta de armazenamento

Substitua o método principal atual em `AzureApp.java` pelo código abaixo. Esse código cria uma [conta de armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-introduction) e, em seguida, usa as bibliotecas de Armazenamento do Azure para Java para criar um novo arquivo de texto na nuvem.

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

Execute o exemplo a partir da linha de comando:

```
mvn clean compile exec:java
```

Você pode procurar o arquivo `helloazure.txt` em sua conta de armazenamento por meio do portal do Azure ou com o [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).

Limpar a conta de armazenamento usando a CLI:

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a>Explorar mais exemplos

Para saber mais sobre como usar as bibliotecas de gerenciamento do Azure para Java para gerenciar recursos e automatizar tarefas, confira o nosso exemplo de código para [máquinas virtuais](java-sdk-azure-virtual-machine-samples.md), [aplicativos Web](java-sdk-azure-web-apps-samples.md) e [banco de dados SQL](java-sdk-azure-sql-database-samples.md) .

## <a name="reference-and-release-notes"></a>Referência e notas de versão

Uma [referência](http://docs.microsoft.com/java/api) está disponível para todos os pacotes.

## <a name="get-help-and-give-feedback"></a>Obter ajuda e fazer comentários

Poste perguntas para a comunidade no [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java). Relate bugs e problemas não resolvidos com as bibliotecas do Azure para Java no [projeto GitHub](https://github.com/Azure/azure-sdk-for-java).
