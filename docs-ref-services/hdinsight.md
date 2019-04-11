---
title: SDK do Java do Azure HDInsight
description: Referência para o SDK do Java do Azure HDInsight. O SDK Java do HDInsight oferece classes e métodos que permitem gerenciar os seus clusters do HDInsight.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 11/21/2018
ms.openlocfilehash: 0ae8d78a0618c4dbcc5e734fce311f7c2e5684bd
ms.sourcegitcommit: a108a82414bd35be896e3c4e7047f5eb7b1518cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58489644"
---
# <a name="hdinsight-java-management-sdk-preview"></a>SDK de Gerenciamento de Java do HDInsight (versão prévia)

## <a name="overview"></a>Visão geral

O SDK Java do HDInsight oferece classes e métodos que permitem gerenciar os seus clusters do HDInsight. Inclui operações para criar, excluir, atualizar, listar, redimensionar, executar ações de script, monitorar, obter propriedades dos clusters HDInsight e muito mais.

## <a name="prerequisites"></a>Pré-requisitos

* Uma conta do Azure. Se você não tiver uma, [obtenha uma avaliação gratuita](https://azure.microsoft.com/free/).
* Um JDK (Java Development Kit) com suporte. Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.
* [Maven](https://maven.apache.org/download.cgi)

## <a name="sdk-installation"></a>Instalação do SDK

O SDK de Java do HDInsight está disponível no Maven [aqui](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight). Adicione a seguinte dependência ao seu pom.xml:

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

Você também precisará adicionar as seguintes dependências ao pom.xml:

* [Biblioteca de autenticação de cliente do Azure:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
  </dependency>
  ```

* [Tempo de execução de cliente Java do Azure para ARM:](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
  </dependency>
  ```

## <a name="authentication"></a>Authentication

O SDK precisa primeiro ser autenticado com a assinatura do Azure.  Siga o exemplo abaixo para criar uma entidade de serviço e use-a para a autenticação. Após isso ser feito, você terá uma instância de um `HDInsightManagementClientImpl`, que contém muitos métodos (destacados nas seções abaixo) que podem ser usados para realizar operações de gerenciamento.

> [!NOTE]
> Existem outras formas de autenticar além do exemplo abaixo que talvez sejam mais adequadas às suas necessidades. Todos os métodos são descritos aqui: [Autenticar com as bibliotecas de gerenciamento do Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)

### <a name="authentication-example-using-a-service-principal"></a>Exemplo de autenticação usando uma entidade de serviço

Primeiro, faça logon no [Azure Cloud Shell](https://shell.azure.com/bash). Verifique se você está usando atualmente a assinatura na qual deseja a entidade de serviço criada. 

```azurecli-interactive
az account show
```

As informações da assinatura são exibidas como JSON.

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

Se você não estiver conectado à assinatura correta, selecione a correta executando: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Se você já não tiver registrado o Provedor de Recursos do HDInsight através de outro método (tais como criar um cluster do HDInsight através do portal do Azure), você precisa fazer isso uma vez antes de poder autenticar. Isso também pode ser feito no [Azure Cloud Shell](https://shell.azure.com/bash) executando o seguinte comando:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Em seguida, escolha um nome para a sua entidade de serviço e crie-a com o seguinte comando:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

As informações da entidade de serviço são exibidas como JSON.

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
Copie o trecho abaixo e preencha `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` e `SUBSCRIPTION_ID` com as cadeias de caracteres do JSON que foi retornado após a execução do comando para criar a entidade de serviço.

```java
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.*;
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.implementation.HDInsightManagementClientImpl;

public class Main {
    public static void main (String[] args) {

        // Tenant ID for your Azure Subscription
        String TENANT_ID = "";
        // Your Service Principal App Client ID
        String CLIENT_ID = "";
        // Your Service Principal Client Secret
        String CLIENT_SECRET = "";
        // Azure Subscription ID
        String SUBSCRIPTION_ID = "";

        ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(
                CLIENT_ID,
                TENANT_ID,
                CLIENT_SECRET,
                AzureEnvironment.AZURE);

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials)
                .withSubscriptionId(SUBSCRIPTION_ID);
```


## <a name="cluster-management"></a>Gerenciamento de clusters

> [!NOTE]
> Essa seção pressupõe que você já autenticou e criou uma `HDInsightManagementClientImpl` instância e a armazenou em uma variável chamada `client`. As instruções para autenticar e obter um `HDInsightManagementClientImpl` podem ser encontradas na seção Autenticação acima.

### <a name="create-a-cluster"></a>Criar um cluster

Um novo cluster pode ser criado chamando `client.clusters().create()`.

#### <a name="example"></a>Exemplo

Este exemplo demonstra como criar um cluster Spark com 2 nós principais e 1 nó de trabalho.

> [!NOTE]
> Primeiro você precisa criar um grupo de recursos e uma conta de armazenamento, conforme explicado abaixo. Se você já os tiver criado, ignore as próximas etapas.

##### <a name="creating-a-resource-group"></a>Criar um grupo de recursos

É possível criar um grupo de recursos usando o [Azure Cloud Shell](https://shell.azure.com/bash) executando:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Criar uma conta de armazenamento

É possível criar uma conta de armazenamento usando o [Azure Cloud Shell](https://shell.azure.com/bash) executando:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Agora execute o comando a seguir para obter a chave para a sua conta de armazenamento (você precisará dela para criar um cluster):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
O trecho em Java abaixo cria um cluster Spark com 2 nós de cabeçalho e 1 nó de trabalho. Preencha as variáveis em branco conforme explicado nos comentários e fique à vontade para alterar outros parâmetros conforme as suas necessidades.

```java
// The name for the cluster you are creating
String clusterName = "";
// The name of your existing Resource Group
String resourceGroupName = "";
// Choose a username
String username = "";
// Choose a password
String password = "";
// Replace <> with the name of your storage account
String storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
String storageAccountKey = "";
// Choose a region
String location = "";
String container = "default";

HashMap<String, HashMap<String, String>> configurations = new HashMap<String, HashMap<String, String>>();
        HashMap<String, String> gateway = new HashMap<String, String>();
        gateway.put("restAuthCredential.enabled_credential", "True");
        gateway.put("restAuthCredential.username", username);
        gateway.put("restAuthCredential.password", password);
        configurations.put("gateway", gateway);

        ClusterCreateParametersExtended parameters = new ClusterCreateParametersExtended()
            .withLocation(location)
            .withTags(Collections.EMPTY_MAP)
            .withProperties(
                new ClusterCreateProperties()
                    .withClusterVersion("3.6")
                    .withOsType(OSType.LINUX)
                    .withClusterDefinition(new ClusterDefinition()
                            .withKind("spark")
                            .withConfigurations(configurations)
                    )
                    .withTier(Tier.STANDARD)
                    .withComputeProfile(new ComputeProfile()
                        .withRoles(List.of(
                            new Role()
                                .withName("headnode")
                                .withTargetInstanceCount(2)
                                .withHardwareProfile(new HardwareProfile()
                                    .withVmSize("Large")
                                )
                                .withOsProfile(new OsProfile()
                                    .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                    )
                                ),
                            new Role()
                                    .withName("workernode")
                                    .withTargetInstanceCount(1)
                                    .withHardwareProfile(new HardwareProfile()
                                        .withVmSize("Large")
                                    )
                                    .withOsProfile(new OsProfile()
                                        .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                        )
                                    )
                        ))
                    )
                    .withStorageProfile(new StorageProfile()
                        .withStorageaccounts(List.of(
                                new StorageAccount()
                                    .withName(storageAccount)
                                    .withKey(storageAccountKey)
                                    .withContainer(container)
                                    .withIsDefault(true)
                        ))
                    )
            );
        client.clusters().create(resourceGroupName, clusterName, parameters);
```

### <a name="get-cluster-details"></a>Obter detalhes do cluster

Para obter propriedades para um determinado cluster:

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemplo

Você pode usar `get` para confirmar que criou com êxito o seu cluster.

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

A saída deve ser assim:

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a>Listar clusters

#### <a name="list-clusters-under-the-subscription"></a>Listar os clusters em uma assinatura

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a>Listar os clusters por grupo de recursos

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> Tanto `List()` quanto `ListByResourceGroup()` retornam um objeto `PagedList<ClusterInner>`. Chamar `loadNext()` retorna uma lista de clusters nessa página e avança o objeto `ClusterPaged` para a página seguinte. Isso pode ser repetido até que `hasNextPage()` retorne `false`, indicando que não existem mais páginas.

#### <a name="example"></a>Exemplo

O exemplo a seguir imprime as propriedades de todos os clusters da assinatura atual:

```java
PagedList<ClusterInner> clusterPages = client.clusters().list();
while (true) {
    for (ClusterInner cluster : clusterPages.currentPage().items()) {
        System.out.println(cluster.name());
    }
    if (clusterPages.hasNextPage()) {
        clusterPages.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="delete-a-cluster"></a>Excluir um cluster

Para excluir um cluster:

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>Atualizar marcas de cluster

É possível atualizar as marcas de um determinado cluster da seguinte forma:

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a>Redimensionar Cluster

É possível redimensionar o número de nós de trabalho de determinado cluster especificando um novo tamanho, assim:

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>Monitoramento do cluster

O SDK de gerenciamento do HDInsight também pode ser usado para gerenciar o monitoramento dos seus clusters através do Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Habilitar Monitoramento de OMS

> [!NOTE]
> Para habilitar o Monitoramento de OMS, você deve ter um espaço de trabalho do Log Analytics existente. Se você ainda não criou, aprenda como fazer isso aqui: [Criar um workspace do Log Analytics no Portal do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Para habilitar o Monitoramento de OMS no seu cluster:

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>Exibir o status do Monitoramento de OMS

Para obter o status do OMS no seu cluster:

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>Desabilitar Monitoramento de OMS

Para desabilitar o OMS no seu cluster:

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>Ações de script

O HDInsight fornece um método de configuração chamado ações de script que chama os scripts personalizados para personalizar o cluster.
> [!NOTE]
> Mais informações sobre como usar as ações de script podem ser encontradas aqui: [Customizar clusters HDInsight baseados em Linux usando as ações de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>Executar ações de script

É possível executar ações de script em um determinado cluster da seguinte forma:

```java
RuntimeScriptAction scriptAction1 = new RuntimeScriptAction()
    .withName("<Script Name>")
    .withUri("<URL To Script>")
    .withRoles(<List<String> of roles>);
client.clusters().executeScriptActions(
    resourceGroupName, 
    clusterName, 
    new ExecuteScriptActionParameters().withPersistOnSuccess(false).withScriptActions(new LinkedList<>(Arrays.asList(scriptAction1)))); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Excluir ação de script

Para excluir uma ação de script persistente específica em um determinado cluster:

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>Listar ações de script persistentes

> [!NOTE]
> Os dois `listByCluster()` retornam um objeto `PagedList<RuntimeScriptActionDetailInner>`. Chamar `currentPage().items()` retorna uma lista de `RuntimeScriptActionDetailInner`, e `loadNextPage()` avança para a página seguinte. Isso pode ser repetido até que `hasNextPage()` retorne `false`, indicando que não existem mais páginas.

Para listar todas as ações de script persistentes para o cluster especificado:
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemplo

```java
PagedList<RuntimeScriptActionDetailInner> scriptsPaged = client.scriptActions().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptsPaged.hasNextPage()) {
        scriptsPaged.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="list-all-scripts-execution-history"></a>Listar o histórico de execução de todos os scripts

Para listar o histórico de execução de todos os scripts para o cluster especificado:

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemplo

Este exemplo imprime todos os detalhes para todas as execuções de script anteriores.

```java
PagedList<RuntimeScriptActionDetailInner> scriptExecutionsPaged = client.scriptExecutionHistorys().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptExecutionsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptExecutionsPaged.hasNextPage()) {
        scriptExecutionsPaged.loadNextPage();
    } else {
        break;
    }
}
```
