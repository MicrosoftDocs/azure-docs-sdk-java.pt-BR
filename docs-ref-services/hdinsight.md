---
title: SDK do Java do Azure HDInsight
description: Referência para o SDK do Java do Azure HDInsight
keywords: Azure, Java, SDK, API, HDInsight
author: tylerfox
ms.author: tyfox
manager: arindamc
ms.date: 9/20/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: hdinsight
ms.openlocfilehash: 4723613924d1a0c0b75cc8e4de28e3f59612ab19
ms.sourcegitcommit: 7c6a15f574fb85ee22f6ccdb7864627b73a6c1f7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/27/2018
ms.locfileid: "47398178"
---
# <a name="hdinsight-java-management-sdk-preview"></a><span data-ttu-id="cde4b-104">Visualização do SDK de Gerenciamento de Java do HDInsight</span><span class="sxs-lookup"><span data-stu-id="cde4b-104">HDInsight Java Management SDK Preview</span></span>

## <a name="overview"></a><span data-ttu-id="cde4b-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cde4b-105">Overview</span></span>

<span data-ttu-id="cde4b-106">O SDK Java do HDInsight oferece classes e métodos que permitem gerenciar os seus clusters do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cde4b-106">The HDInsight Java SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="cde4b-107">Ele inclui operações para criar, excluir, atualizar, listar, dimensionar, executar ações de script, monitorar, obter propriedades de clusters HDInsight e muito mais.</span><span class="sxs-lookup"><span data-stu-id="cde4b-107">It includes operations to create, delete, update, list, scale, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cde4b-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cde4b-108">Prerequisites</span></span>

* <span data-ttu-id="cde4b-109">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cde4b-109">An Azure account.</span></span> <span data-ttu-id="cde4b-110">Se você não tiver uma, [obtenha uma avaliação gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="cde4b-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="cde4b-111">Java JDK</span><span class="sxs-lookup"><span data-stu-id="cde4b-111">Java JDK</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [<span data-ttu-id="cde4b-112">Maven</span><span class="sxs-lookup"><span data-stu-id="cde4b-112">Maven</span></span>](https://maven.apache.org/install.html)

## <a name="sdk-installation"></a><span data-ttu-id="cde4b-113">Instalação do SDK</span><span class="sxs-lookup"><span data-stu-id="cde4b-113">SDK Installation</span></span>

<span data-ttu-id="cde4b-114">O SDK de Java do HDInsight está disponível no Maven [aqui](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="cde4b-114">The HDInsight Java SDK is available through Maven [here](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span></span> <span data-ttu-id="cde4b-115">Adicione a seguinte dependência ao seu pom.xml:</span><span class="sxs-lookup"><span data-stu-id="cde4b-115">Add the following dependency to your pom.xml:</span></span>

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

<span data-ttu-id="cde4b-116">Você também precisará adicionar as seguintes dependências ao pom.xml:</span><span class="sxs-lookup"><span data-stu-id="cde4b-116">You will also need to add the following dependencies to your pom.xml:</span></span>

* [<span data-ttu-id="cde4b-117">Biblioteca de autenticação de cliente do Azure:</span><span class="sxs-lookup"><span data-stu-id="cde4b-117">Azure Client Authentication Library:</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
    <scope>test</scope>
</dependency>
```

* [<span data-ttu-id="cde4b-118">Tempo de execução de cliente Java do Azure para ARM:</span><span class="sxs-lookup"><span data-stu-id="cde4b-118">Azure Java Client Runtime For ARM:</span></span>](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
</dependency>
```

## <a name="authentication"></a><span data-ttu-id="cde4b-119">Autenticação</span><span class="sxs-lookup"><span data-stu-id="cde4b-119">Authentication</span></span>

<span data-ttu-id="cde4b-120">O SDK precisa primeiro ser autenticado com a assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cde4b-120">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="cde4b-121">Siga o exemplo abaixo para criar uma entidade de serviço e use-a para a autenticação.</span><span class="sxs-lookup"><span data-stu-id="cde4b-121">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="cde4b-122">Após isso ser feito, você terá uma instância de um `HDInsightManagementClientImpl`, que contém muitos métodos (destacados nas seções abaixo) que podem ser usados para realizar operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="cde4b-122">After this is done, you will have an instance of an `HDInsightManagementClientImpl`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="cde4b-123">Existem outras formas de autenticar além do exemplo abaixo que talvez sejam mais adequadas às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="cde4b-123">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="cde4b-124">Todos os métodos são descritos aqui: [Autenticar com as bibliotecas de gerenciamento para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span><span class="sxs-lookup"><span data-stu-id="cde4b-124">All methods are outlined here: [Authenticate with the Azure management libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="cde4b-125">Exemplo de autenticação usando uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="cde4b-125">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="cde4b-126">Primeiro, faça logon no [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="cde4b-126">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="cde4b-127">Verifique se você está usando atualmente a assinatura na qual deseja a entidade de serviço criada.</span><span class="sxs-lookup"><span data-stu-id="cde4b-127">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="cde4b-128">As informações da assinatura são exibidas como JSON.</span><span class="sxs-lookup"><span data-stu-id="cde4b-128">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="cde4b-129">Se você não estiver conectado à assinatura correta, selecione a correta executando:</span><span class="sxs-lookup"><span data-stu-id="cde4b-129">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="cde4b-130">Se você já não tiver registrado o Provedor de Recursos do HDInsight através de outro método (tais como criar um cluster do HDInsight através do portal do Azure), você precisa fazer isso uma vez antes de poder autenticar.</span><span class="sxs-lookup"><span data-stu-id="cde4b-130">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="cde4b-131">Isso também pode ser feito no [Azure Cloud Shell](https://shell.azure.com/bash) executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cde4b-131">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="cde4b-132">Em seguida, escolha um nome para a sua entidade de serviço e crie-a com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cde4b-132">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="cde4b-133">As informações da entidade de serviço são exibidas como JSON.</span><span class="sxs-lookup"><span data-stu-id="cde4b-133">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="cde4b-134">Copie o trecho abaixo e preencha `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` e `SUBSCRIPTION_ID` com as cadeias de caracteres do JSON que foi retornado após a execução do comando para criar a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="cde4b-134">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials);
```


## <a name="cluster-management"></a><span data-ttu-id="cde4b-135">Gerenciamento de clusters</span><span class="sxs-lookup"><span data-stu-id="cde4b-135">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="cde4b-136">Essa seção pressupõe que você já autenticou e criou uma `HDInsightManagementClientImpl` instância e a armazenou em uma variável chamada `client`.</span><span class="sxs-lookup"><span data-stu-id="cde4b-136">This section assumes you have already authenticated and constructed an `HDInsightManagementClientImpl` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="cde4b-137">As instruções para autenticar e obter um `HDInsightManagementClientImpl` podem ser encontradas na seção Autenticação acima.</span><span class="sxs-lookup"><span data-stu-id="cde4b-137">Instructions for authenticating and obtaining an `HDInsightManagementClientImpl` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="cde4b-138">Criar um cluster</span><span class="sxs-lookup"><span data-stu-id="cde4b-138">Create a Cluster</span></span>

<span data-ttu-id="cde4b-139">Um novo cluster pode ser criado chamando `client.clusters().create()`.</span><span class="sxs-lookup"><span data-stu-id="cde4b-139">A new cluster can be created by calling `client.clusters().create()`.</span></span>

#### <a name="example"></a><span data-ttu-id="cde4b-140">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cde4b-140">Example</span></span>

<span data-ttu-id="cde4b-141">Este exemplo demonstra como criar um cluster Spark com 2 nós principais e 1 nó de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cde4b-141">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="cde4b-142">Primeiro você precisa criar um grupo de recursos e uma conta de armazenamento, conforme explicado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cde4b-142">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="cde4b-143">Se você já os tiver criado, ignore as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="cde4b-143">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="cde4b-144">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cde4b-144">Creating a Resource Group</span></span>

<span data-ttu-id="cde4b-145">É possível criar um grupo de recursos usando o [Azure Cloud Shell](https://shell.azure.com/bash) executando:</span><span class="sxs-lookup"><span data-stu-id="cde4b-145">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="cde4b-146">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="cde4b-146">Creating a Storage Account</span></span>

<span data-ttu-id="cde4b-147">É possível criar uma conta de armazenamento usando o [Azure Cloud Shell](https://shell.azure.com/bash) executando:</span><span class="sxs-lookup"><span data-stu-id="cde4b-147">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="cde4b-148">Agora execute o comando a seguir para obter a chave para a sua conta de armazenamento (você precisará dela para criar um cluster):</span><span class="sxs-lookup"><span data-stu-id="cde4b-148">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="cde4b-149">O trecho em Java abaixo cria um cluster Spark com 2 nós de cabeçalho e 1 nó de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cde4b-149">The below Java snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="cde4b-150">Preencha as variáveis em branco conforme explicado nos comentários e fique à vontade para alterar outros parâmetros conforme as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="cde4b-150">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="cde4b-151">Obter detalhes do cluster</span><span class="sxs-lookup"><span data-stu-id="cde4b-151">Get Cluster Details</span></span>

<span data-ttu-id="cde4b-152">Para obter propriedades para um determinado cluster:</span><span class="sxs-lookup"><span data-stu-id="cde4b-152">To get properties for a given cluster:</span></span>

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="cde4b-153">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cde4b-153">Example</span></span>

<span data-ttu-id="cde4b-154">Você pode usar `get` para confirmar que criou com êxito o seu cluster.</span><span class="sxs-lookup"><span data-stu-id="cde4b-154">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

<span data-ttu-id="cde4b-155">A saída deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="cde4b-155">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a><span data-ttu-id="cde4b-156">Listar clusters</span><span class="sxs-lookup"><span data-stu-id="cde4b-156">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="cde4b-157">Listar os clusters em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="cde4b-157">List Clusters Under The Subscription</span></span>

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="cde4b-158">Listar os clusters por grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cde4b-158">List Clusters By Resource Group</span></span>

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="cde4b-159">Tanto `List()` quanto `ListByResourceGroup()` retornam um objeto `PagedList<ClusterInner>`.</span><span class="sxs-lookup"><span data-stu-id="cde4b-159">Both `List()` and `ListByResourceGroup()` return a `PagedList<ClusterInner>` object.</span></span> <span data-ttu-id="cde4b-160">Chamar `loadNext()` retorna uma lista de clusters nessa página e avança o objeto `ClusterPaged` para a página seguinte.</span><span class="sxs-lookup"><span data-stu-id="cde4b-160">Calling `loadNext()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="cde4b-161">Isso pode ser repetido até que `hasNextPage()` retorne `false`, indicando que não existem mais páginas.</span><span class="sxs-lookup"><span data-stu-id="cde4b-161">This can be repeated until `hasNextPage()` return `false`, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="cde4b-162">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cde4b-162">Example</span></span>

<span data-ttu-id="cde4b-163">O exemplo a seguir imprime as propriedades de todos os clusters da assinatura atual:</span><span class="sxs-lookup"><span data-stu-id="cde4b-163">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="cde4b-164">Excluir um cluster</span><span class="sxs-lookup"><span data-stu-id="cde4b-164">Delete a Cluster</span></span>

<span data-ttu-id="cde4b-165">Para excluir um cluster:</span><span class="sxs-lookup"><span data-stu-id="cde4b-165">To delete a cluster:</span></span>

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="cde4b-166">Atualizar marcas de cluster</span><span class="sxs-lookup"><span data-stu-id="cde4b-166">Update Cluster Tags</span></span>

<span data-ttu-id="cde4b-167">É possível atualizar as marcas de um determinado cluster da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="cde4b-167">You can update the tags of a given cluster like so:</span></span>

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="scale-cluster"></a><span data-ttu-id="cde4b-168">Dimensionar cluster</span><span class="sxs-lookup"><span data-stu-id="cde4b-168">Scale Cluster</span></span>

<span data-ttu-id="cde4b-169">É possível dimensionar um determinado número de nós de trabalho do cluster especificando um novo tamanho da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="cde4b-169">You can scale a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="cde4b-170">Monitoramento do cluster</span><span class="sxs-lookup"><span data-stu-id="cde4b-170">Cluster Monitoring</span></span>

<span data-ttu-id="cde4b-171">O SDK de gerenciamento do HDInsight também pode ser usado para gerenciar o monitoramento dos seus clusters através do Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="cde4b-171">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="cde4b-172">Habilitar Monitoramento de OMS</span><span class="sxs-lookup"><span data-stu-id="cde4b-172">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="cde4b-173">Para habilitar o Monitoramento de OMS, você deve ter um espaço de trabalho existente do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="cde4b-173">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="cde4b-174">Se você já não tiver criado um, você pode aprender como fazer isso aqui: [Criar um espaço de trabalho do Log Analytics no portal do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="cde4b-174">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="cde4b-175">Para habilitar o Monitoramento de OMS no seu cluster:</span><span class="sxs-lookup"><span data-stu-id="cde4b-175">To enable OMS Monitoring on your cluster:</span></span>

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="cde4b-176">Exibir o status do Monitoramento de OMS</span><span class="sxs-lookup"><span data-stu-id="cde4b-176">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="cde4b-177">Para obter o status do OMS no seu cluster:</span><span class="sxs-lookup"><span data-stu-id="cde4b-177">To get the status of OMS on your cluster:</span></span>

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="cde4b-178">Desabilitar Monitoramento de OMS</span><span class="sxs-lookup"><span data-stu-id="cde4b-178">Disable OMS Monitoring</span></span>

<span data-ttu-id="cde4b-179">Para desabilitar o OMS no seu cluster:</span><span class="sxs-lookup"><span data-stu-id="cde4b-179">To disable OMS on your cluster:</span></span>

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="cde4b-180">Ações de script</span><span class="sxs-lookup"><span data-stu-id="cde4b-180">Script Actions</span></span>

<span data-ttu-id="cde4b-181">O HDInsight fornece um método de configuração chamado ações de script que chama os scripts personalizados para personalizar o cluster.</span><span class="sxs-lookup"><span data-stu-id="cde4b-181">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="cde4b-182">Mais informações sobre como usar as ações de script podem ser encontradas aqui: [Personalizar clusters HDInsight com base em Linux usando ações de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="cde4b-182">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="cde4b-183">Executar ações de script</span><span class="sxs-lookup"><span data-stu-id="cde4b-183">Execute Script Actions</span></span>

<span data-ttu-id="cde4b-184">É possível executar ações de script em um determinado cluster da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="cde4b-184">You can execute script actions on a given cluster like so:</span></span>

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

### <a name="delete-script-action"></a><span data-ttu-id="cde4b-185">Excluir ação de script</span><span class="sxs-lookup"><span data-stu-id="cde4b-185">Delete Script Action</span></span>

<span data-ttu-id="cde4b-186">Para excluir uma ação de script persistente específica em um determinado cluster:</span><span class="sxs-lookup"><span data-stu-id="cde4b-186">To delete a specified persisted script action on a given cluster:</span></span>

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="cde4b-187">Listar ações de script persistentes</span><span class="sxs-lookup"><span data-stu-id="cde4b-187">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="cde4b-188">Os dois `listByCluster()` retornam um objeto `PagedList<RuntimeScriptActionDetailInner>`.</span><span class="sxs-lookup"><span data-stu-id="cde4b-188">Both `listByCluster()` returns a `PagedList<RuntimeScriptActionDetailInner>` object.</span></span> <span data-ttu-id="cde4b-189">Chamar `currentPage().items()` retorna uma lista de `RuntimeScriptActionDetailInner`, e `loadNextPage()` avança para a página seguinte.</span><span class="sxs-lookup"><span data-stu-id="cde4b-189">Calling `currentPage().items()` returns a list of `RuntimeScriptActionDetailInner`, and `loadNextPage()` advances to the next page.</span></span> <span data-ttu-id="cde4b-190">Isso pode ser repetido até que `hasNextPage()` retorne `false`, indicando que não existem mais páginas.</span><span class="sxs-lookup"><span data-stu-id="cde4b-190">This can be repeated until `hasNextPage()` returns `false`, indicating that there are no more pages.</span></span>

<span data-ttu-id="cde4b-191">Para listar todas as ações de script persistentes para o cluster especificado:</span><span class="sxs-lookup"><span data-stu-id="cde4b-191">To list all persisted script actions for the specified cluster:</span></span>
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="cde4b-192">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cde4b-192">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="cde4b-193">Listar o histórico de execução de todos os scripts</span><span class="sxs-lookup"><span data-stu-id="cde4b-193">List All Scripts' Execution History</span></span>

<span data-ttu-id="cde4b-194">Para listar o histórico de execução de todos os scripts para o cluster especificado:</span><span class="sxs-lookup"><span data-stu-id="cde4b-194">To list all scripts' execution history for the specified cluster:</span></span>

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="cde4b-195">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cde4b-195">Example</span></span>

<span data-ttu-id="cde4b-196">Este exemplo imprime todos os detalhes para todas as execuções de script anteriores.</span><span class="sxs-lookup"><span data-stu-id="cde4b-196">This example prints all the details for all past script executions.</span></span>

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