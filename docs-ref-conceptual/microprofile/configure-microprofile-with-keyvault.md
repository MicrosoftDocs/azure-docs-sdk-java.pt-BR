---
title: Configurar o MicroProfile usando o Azure Key Vault
description: Saiba como injetar segredos em um serviço Web do MicroProfile usando o Azure Key Vault
services: key-vault
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: c405711813176823f2ddee6b4002f75c2b25fdb5
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533619"
---
# <a name="configure-microprofile-by-using-azure-key-vault"></a><span data-ttu-id="d8af5-103">Configurar o MicroProfile usando o Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d8af5-103">Configure MicroProfile by using Azure Key Vault</span></span>

<span data-ttu-id="d8af5-104">Este artigo demonstra como configurar um aplicativo do [MicroProfile](http://microprofile.io) para recuperar segredos de um [cofre de chaves do Azure](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="d8af5-104">This article demonstrates how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from an [Azure key vault](https://azure.microsoft.com/services/key-vault/).</span></span> <span data-ttu-id="d8af5-105">Neste processo, você usará as [APIs de Configuração do MicroProfile](https://microprofile.io/project/eclipse/microprofile-config) para criar uma conexão direta com um cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8af5-105">In this process, you use the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to an Azure key vault.</span></span> <span data-ttu-id="d8af5-106">Como desenvolvedor, usando as APIs de Configuração do MicroProfile, você se beneficia de uma API padrão para recuperação e injeção de dados de configuração em seus microsserviços.</span><span class="sxs-lookup"><span data-stu-id="d8af5-106">As a developer, by using the MicroProfile Config APIs, you benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="d8af5-107">Antes de começar, dê uma olhada rápida no que uma combinação do Azure Key Vault e da API de Configuração do MicroProfile permite escrever no código.</span><span class="sxs-lookup"><span data-stu-id="d8af5-107">Before you start, take a quick look at what a combination of Azure Key Vault and the MicroProfile Config API enables you to write in your code.</span></span> <span data-ttu-id="d8af5-108">O snippet de código a seguir é de um campo em uma classe que é anotada com `@Inject` e `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="d8af5-108">The following code snippet is of a field in a class that's annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="d8af5-109">O *name* especificado na anotação é o nome da propriedade a ser pesquisado no cofre de chaves, e o *defaultValue* é o que será definido caso a chave não seja descoberta.</span><span class="sxs-lookup"><span data-stu-id="d8af5-109">The *name* that's specified in the annotation is the name of the property to look up in your key vault, and the *defaultValue* is what will be set if the key is not discovered.</span></span> <span data-ttu-id="d8af5-110">O resultado é que o valor armazenado no cofre de chaves, ou o valor padrão, é injetado automaticamente no campo em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="d8af5-110">The result is that the value that's stored in the key vault, or the default value, is injected automatically into the field at runtime.</span></span> <span data-ttu-id="d8af5-111">Essa ação pode simplificar sua vida, porque você não precisa mais passar valores em construtores e métodos setter.</span><span class="sxs-lookup"><span data-stu-id="d8af5-111">This action can simplify your life, because you no longer need to pass values around in constructors and setter methods.</span></span> <span data-ttu-id="d8af5-112">Em vez disso, o MicroProfile cuida dessa tarefa.</span><span class="sxs-lookup"><span data-stu-id="d8af5-112">Instead, MicroProfile handles this task.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="d8af5-113">Para solicitar segredos, conforme necessário, acesse também a configuração do MicroProfile diretamente.</span><span class="sxs-lookup"><span data-stu-id="d8af5-113">To request secrets, as necessary, you can also access the MicroProfile config directly.</span></span> <span data-ttu-id="d8af5-114">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d8af5-114">For example:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="d8af5-115">Esse código de exemplo usa o [Payara Micro](https://www.payara.fish/payara_micro) e o [MicroProfile](https://microprofile.io/) para criar um arquivo WAR (requisito de aplicativo Web) Java pequeno que pode ser executado localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="d8af5-115">This sample code uses [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java web application requirement (WAR) file that you can run locally on your machine.</span></span> <span data-ttu-id="d8af5-116">Ele não demonstra como converter o código para Docker nem enviá-lo por push ao Azure, mas a seção no final deste artigo contém links para outros tutoriais úteis que explicam como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="d8af5-116">It doesn't demonstrate how to Dockerize or push the code to Azure, but the section at the end of this article has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="d8af5-117">A amostra usa uma biblioteca de software livre gratuita que cria uma fonte de configuração (usando a API de Configuração do MicroProfile) no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="d8af5-117">The sample uses a free and open source library that creates a config source (using the MicroProfile Config API) in your key vault.</span></span> <span data-ttu-id="d8af5-118">Para saber mais sobre essa biblioteca e examinar o código, confira a [página do projeto no GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="d8af5-118">To learn more about this library and review the code, see the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="d8af5-119">Se você usar a biblioteca, o código deste tutorial poderá simplesmente se concentrar na configuração da biblioteca e, em seguida, injetar chaves no código.</span><span class="sxs-lookup"><span data-stu-id="d8af5-119">If you use the library, the code in this tutorial can simply focus on the configuration of the library and then inject keys into your code.</span></span> <span data-ttu-id="d8af5-120">Não é necessário escrever nenhum código específico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8af5-120">You don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="d8af5-121">Para executar esse código no computador local, começando com a criação de um recurso do cofre de chaves, siga as instruções das próximas seções.</span><span class="sxs-lookup"><span data-stu-id="d8af5-121">To run this code on your local machine, starting with creating a key vault resource, follow the instructions in the next sections.</span></span>

## <a name="create-a-key-vault-resource"></a><span data-ttu-id="d8af5-122">Criar um recurso do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="d8af5-122">Create a key vault resource</span></span>

<span data-ttu-id="d8af5-123">Nesta seção, você usará a CLI do Azure para criar um recurso do cofre de chaves e populá-lo com um segredo.</span><span class="sxs-lookup"><span data-stu-id="d8af5-123">In this section, you use the Azure CLI to create a key vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="d8af5-124">Crie uma entidade de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8af5-124">Create an Azure service principal.</span></span> <span data-ttu-id="d8af5-125">Essa etapa fornece a ID do cliente e a chave necessárias para acessar o cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="d8af5-125">This step gives you the client ID and key that you need to access your key vault:</span></span>

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    <span data-ttu-id="d8af5-126">Vamos usar *microprofile-keyvault-service-principal* para substituir *\<service_principal_name>* na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="d8af5-126">Let's use *microprofile-keyvault-service-principal* to replace *\<service_principal_name>* in the preceding step.</span></span> <span data-ttu-id="d8af5-127">A resposta do Azure será semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="d8af5-127">The response from Azure would be similar to the following:</span></span>

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    <span data-ttu-id="d8af5-128">Vale destacar aqui os valores de *appId* e *password*.</span><span class="sxs-lookup"><span data-stu-id="d8af5-128">Of particular note here are the *appId* and *password* values.</span></span> <span data-ttu-id="d8af5-129">Você os usará mais adiante neste artigo como a *ID do cliente* e a *chave*.</span><span class="sxs-lookup"><span data-stu-id="d8af5-129">You'll use them later in this article as *client ID* and *key*.</span></span>

1. <span data-ttu-id="d8af5-130">(Opcional) Agora que você criou uma entidade de serviço, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8af5-130">(Optional) Now that you've created a service principal, you can create a resource group.</span></span> <span data-ttu-id="d8af5-131">Caso já tenha um grupo de recursos que deseje usar, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="d8af5-131">If you already have a resource group that you want to use, you can skip this step.</span></span> <span data-ttu-id="d8af5-132">Para obter uma lista de localizações do grupo de recursos, chame `az account list-locations` e use o valor de *name* dessa lista para especificar a localização em que o grupo de recursos deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="d8af5-132">To get a list of resource group locations, you can call `az account list-locations` and use the *name* value from that list to specify where the resource group should be created.</span></span>

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. <span data-ttu-id="d8af5-133">Crie um recurso do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="d8af5-133">Create a key vault resource.</span></span> <span data-ttu-id="d8af5-134">Você usará o nome do cofre de chaves para referenciar o cofre de chaves mais tarde; portanto, escolha um nome fácil de ser lembrado.</span><span class="sxs-lookup"><span data-stu-id="d8af5-134">You'll use your key vault name to refer to the key vault later, so be sure to choose a memorable name.</span></span>

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. <span data-ttu-id="d8af5-135">Conceda as permissões apropriadas à entidade de serviço criada anteriormente, de modo que ela possa acessar os segredos do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="d8af5-135">Grant the appropriate permissions to the service principal that you created earlier, so that it can access the key vault secrets.</span></span> <span data-ttu-id="d8af5-136">O valor de appId no código a seguir é o valor de *appId* da etapa 1, em que você criou a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="d8af5-136">The appId value in the following code is the *appId* value from step 1, where you created the service principal.</span></span> <span data-ttu-id="d8af5-137">Ou seja, a *appId* na etapa 1 era *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, mas você deverá usar o valor de sua própria saída do terminal.</span><span class="sxs-lookup"><span data-stu-id="d8af5-137">That is, the *appId* in step 1 was *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, but you should use the value from your own terminal output.</span></span>

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. <span data-ttu-id="d8af5-138">Agora você pode enviar um segredo por push ao cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="d8af5-138">Now you can push a secret into your key vault.</span></span> <span data-ttu-id="d8af5-139">Use o nome da chave *demo-key* e defina o valor da chave como *demo-value*:</span><span class="sxs-lookup"><span data-stu-id="d8af5-139">Use the key name *demo-key*, and set the value of the key to *demo-value*:</span></span>

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

<span data-ttu-id="d8af5-140">É isso!</span><span class="sxs-lookup"><span data-stu-id="d8af5-140">That's it!</span></span> <span data-ttu-id="d8af5-141">Agora você tem um cofre de chaves em execução no Azure com um único segredo.</span><span class="sxs-lookup"><span data-stu-id="d8af5-141">You now have a key vault running in Azure with a single secret.</span></span> <span data-ttu-id="d8af5-142">Agora clone esse repositório e configure-o para usar esse recurso em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8af5-142">You can now clone this repo and configure it to use this resource in your app.</span></span>

## <a name="get-up-and-running-locally"></a><span data-ttu-id="d8af5-143">Colocá-lo em funcionamento localmente</span><span class="sxs-lookup"><span data-stu-id="d8af5-143">Get up and running locally</span></span>

<span data-ttu-id="d8af5-144">Este exemplo se baseia em um aplicativo de exemplo disponível no GitHub; portanto, você clonará esse aplicativo e, em seguida, executará o código em etapas.</span><span class="sxs-lookup"><span data-stu-id="d8af5-144">This example is based on a sample application that's available on GitHub, so you'll clone that application and then step through the code.</span></span> 

1. <span data-ttu-id="d8af5-145">Clone o código no computador inserindo os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d8af5-145">Clone the code onto your machine by entering the following commands:</span></span>

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="d8af5-146">Acesse *src/main/resources/META-INF/microprofile-config.properties* e, em seguida, altere as propriedades no arquivo *microprofile-config.properties* usando os valores das etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="d8af5-146">Go to *src/main/resources/META-INF/microprofile-config.properties*, and then change the properties in the *microprofile-config.properties* file by using the values from the previous steps.</span></span>

1. <span data-ttu-id="d8af5-147">Tente executar o servidor usando `mvn clean package payara-micro:start`.</span><span class="sxs-lookup"><span data-stu-id="d8af5-147">Try running the server by using `mvn clean package payara-micro:start`.</span></span>

1. <span data-ttu-id="d8af5-148">Tente acessar [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="d8af5-148">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser.</span></span> <span data-ttu-id="d8af5-149">Você deverá ver uma resposta simples que demonstra os valores que estão sendo lidos do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="d8af5-149">You should see a simple response that demonstrates values that are being read from your key vault.</span></span>

## <a name="summary"></a><span data-ttu-id="d8af5-150">Resumo</span><span class="sxs-lookup"><span data-stu-id="d8af5-150">Summary</span></span>

<span data-ttu-id="d8af5-151">Este aplicativo de exemplo combina a API de Configuração do MicroProfile, o Azure Key Vault e a biblioteca de software livre gratuita [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) para permitir a fácil injeção de dados de configuração e segredos em seus serviços Web do MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="d8af5-151">This sample application combines the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into your MicroProfile web services.</span></span>
