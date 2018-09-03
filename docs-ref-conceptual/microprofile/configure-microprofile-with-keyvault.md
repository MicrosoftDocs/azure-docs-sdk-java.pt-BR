---
title: Configurar MicroProfile com o Azure Key Vault
description: Saiba como inserir segredos em um serviço da web de MicroProfile com o Azure Key Vault
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
ms.openlocfilehash: fa93788f9b600d963f35ea599a58d309d3a3ee52
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240819"
---
# <a name="configure-microprofile-with-azure-key-vault"></a><span data-ttu-id="0072d-103">Configurar MicroProfile com o Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="0072d-103">Configure MicroProfile with Azure Key Vault</span></span>

<span data-ttu-id="0072d-104">Este tutorial demonstra como configurar um aplicativo [MicroProfile](http://microprofile.io) para recuperar segredos do [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) usando as [APIS de configuração do MicroProfile](https://microprofile.io/project/eclipse/microprofile-config) para criar uma conexão direta ao Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0072d-104">This tutorial will demonstrate how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) using the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to Azure Key Vault.</span></span> <span data-ttu-id="0072d-105">Usando as APIs de configuração do MicroProfile, os desenvolvedores se beneficiam de uma API padrão para recuperação e injeção de dados de configuração em seus microsserviços.</span><span class="sxs-lookup"><span data-stu-id="0072d-105">By using the MicroProfile Config APIs, developers benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="0072d-106">Antes de nos aprofundarmos, vamos dar uma olhada no que uma combinação entre o Azure Key Vault e a API de configuração do MicroProfile nos permite escrever em nosso código.</span><span class="sxs-lookup"><span data-stu-id="0072d-106">Before we dive in, lets quickly take a look at what a combination of Azure Key Vault and the MicroProfile Config API enables us to write in our code.</span></span> <span data-ttu-id="0072d-107">Aqui está um trecho de código de um campo em uma classe que foi anotada com `@Inject` e `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="0072d-107">Here's a code snippet of a field in a class that has been annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="0072d-108">A `name` especificada na anotação é o nome da propriedade para pesquisar no Azure Key Vault e `defaultValue` é o que será definido se a chave não for descoberta.</span><span class="sxs-lookup"><span data-stu-id="0072d-108">The `name` specified in the annotation is the name of the property to look up in Azure Key Vault, and the `defaultValue` is what will be set if the key is not discovered.</span></span> <span data-ttu-id="0072d-109">O resultado final é que o valor armazenado no Azure Key Vault ou o valor padrão, será injetado automaticamente no campo em tempo de execução, simplificando a vida dos desenvolvedores, pois eles não precisam mais passar valores em torno de métodos constuctors e um setter, deixando isso para o MicroProfile manipular.</span><span class="sxs-lookup"><span data-stu-id="0072d-109">The end result is that the value stored in Azure Key Vault, or the default value, will be injected automatically into the field at runtime, simplifying the life of developers as they no longer need to pass values around in constuctors and setter methods, instead leaving it to MicroProfile to handle.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="0072d-110">Também é possível acessar a configuração de MicroProfile diretamente, para solicitar segredos conforme necessário, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0072d-110">It is also possible to access the MicroProfile config directly, to request secrets as necessary, e.g.:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="0072d-111">Este exemplo utiliza [Payara Micro](https://www.payara.fish/payara_micro) e [MicroProfile](https://microprofile.io/) para criar um arquivo war Java pequeno que pode ser executado localmente em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0072d-111">This sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java war file that can be run locally on your machine.</span></span> <span data-ttu-id="0072d-112">Ele não demonstra como dockerizar ou enviar por push o código para o Azure, mas a seção de links no final deste tutorial tem links para outros tutoriais úteis que explicam isso.</span><span class="sxs-lookup"><span data-stu-id="0072d-112">It does not demonstrate how to dockerise or push the code to Azure, but the links section at the end of this tutorial has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="0072d-113">Este exemplo usa uma biblioteca de software livre gratuita que cria uma fonte de configuração (usando a API de configuração do MicroProfile) para o Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0072d-113">This sample makes use of a free and open source library that creats a config source (using the MicroProfile Config API) for Azure Key Vault.</span></span> <span data-ttu-id="0072d-114">Você pode saber mais sobre essa biblioteca e examine o código na [página do projeto GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="0072d-114">You can learn more about this library, and review the code, on the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="0072d-115">Ao usar essa biblioteca, o código neste tutorial pode se focar simplesmente na configuração da biblioteca, seguido pela injeção de chaves no seu código e não precisamos escrever nenhum código específico do Azure.</span><span class="sxs-lookup"><span data-stu-id="0072d-115">By using this library, the code in this tutorial can simply focus on configuration of the library, followed by injecting keys into your code, and we don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="0072d-116">Aqui estão as etapas necessárias para executar esse código em seu computador local, começando com a criação de um recurso do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0072d-116">Here are the steps required to run this code on your local machine, starting with creating an Azure Key Vault resource.</span></span>

## <a name="creating-an-azure-key-vault-resource"></a><span data-ttu-id="0072d-117">Criar um recurso do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="0072d-117">Creating an Azure Key Vault resource</span></span>

<span data-ttu-id="0072d-118">Nós usaremos a CLI do Azure para criar o recurso do Azure Key Vault e preenchê-lo com um segredo.</span><span class="sxs-lookup"><span data-stu-id="0072d-118">We will use the Azure CLI to create the Azure Key Vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="0072d-119">Primeiro, vamos criar uma entidade de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="0072d-119">Firstly, lets create an Azure service principal.</span></span> <span data-ttu-id="0072d-120">Isso fornecerá a ID do cliente e a chave necessária para acessar o Key Vault:</span><span class="sxs-lookup"><span data-stu-id="0072d-120">This will provide us with the client ID and key we need to access Key Vault:</span></span>

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

<span data-ttu-id="0072d-121">Vamos dizer que usamos `microprofile-keyvault-service-principal` para o nome da entidade de serviço na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="0072d-121">Lets say we use `microprofile-keyvault-service-principal` for the service principal name in the previous step.</span></span> <span data-ttu-id="0072d-122">A resposta do Azure para isso estará no formulário a seguir, um pouco censurado:</span><span class="sxs-lookup"><span data-stu-id="0072d-122">The response from Azure for doing this will be in the following, slightly censored, form:</span></span>

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

<span data-ttu-id="0072d-123">O que deve ser observado aqui são os valores `appID` e `password` - esses são os valores que usaremos mais tarde como `client ID` e `key`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0072d-123">Of particular note here is the `appID` and `password` values - these are what we will use later on as `client ID` and `key`, respectively.</span></span>

<span data-ttu-id="0072d-124">Agora que criamos uma entidade de serviço, podemos, opcionalmente, criar um grupo de recursos (se você já tiver um que deseja usar, você pode ignorar esta etapa).</span><span class="sxs-lookup"><span data-stu-id="0072d-124">Now that we have created a service principal, we can optionally create a resource group (if you already have one you want to use, you can skip this step).</span></span> <span data-ttu-id="0072d-125">Observe que, para obter uma lista de locais de grupo de recursos, você pode chamar `az account list-locations` e usar o valor `name` nessa lista para especificar onde o grupo de recursos deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="0072d-125">Note that to get a list of resource group locations, you can call `az account list-locations` and use the `name` value from that list to specify where the resource group should be created.</span></span>

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

<span data-ttu-id="0072d-126">Agora criamos um recurso do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0072d-126">We now create an Azure Key Vault resource.</span></span> <span data-ttu-id="0072d-127">Observe que o nome do Key Vault é o que você usará para referenciar o cofre de chaves mais tarde, então escolha algo fácil de lembrar.</span><span class="sxs-lookup"><span data-stu-id="0072d-127">Note that the Key Vault name is what you will use to reference the key vault later, so choose something memorable.</span></span>

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

<span data-ttu-id="0072d-128">Também é necessário conceder as permissões apropriadas para a entidade de serviço criada anteriormente, para que ela possa acessar os segredos do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0072d-128">We also need to grant the appropriate permissions to the service principal we created earlier, so that it may access the Key Vault secrets.</span></span> <span data-ttu-id="0072d-129">Observe que o valor de appID é o valor `appId` mencionado acima onde criamos a entidade de serviço (ou seja, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79` - mas use o valor da sua saída do terminal).</span><span class="sxs-lookup"><span data-stu-id="0072d-129">Note that the appID value is the `appId` value from above where we created the service principal (that is, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79` - but use the value from your terminal output).</span></span>

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

<span data-ttu-id="0072d-130">Agora estamos no ponto onde podemos enviar por push um segredo para o Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0072d-130">We are now at the point where we can push a secret into Key Vault.</span></span> <span data-ttu-id="0072d-131">Vamos usar o nome da chave `demo-key` e defina o valor da chave para `demo-value`:</span><span class="sxs-lookup"><span data-stu-id="0072d-131">Lets use the key name `demo-key`, and set the value of the key to be `demo-value`:</span></span>

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

<span data-ttu-id="0072d-132">É isso!</span><span class="sxs-lookup"><span data-stu-id="0072d-132">That's it!</span></span> <span data-ttu-id="0072d-133">Agora temos o Key Vault em execução no Azure com um segredo único.</span><span class="sxs-lookup"><span data-stu-id="0072d-133">We now have Key Vault running in Azure with a single secret.</span></span> <span data-ttu-id="0072d-134">Agora podemos clonar esse repositório e configurá-lo para usar esse recurso em nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0072d-134">We can now clone this repo and configure it to use this resource in our app.</span></span>

## <a name="getting-up-and-running-locally"></a><span data-ttu-id="0072d-135">Colocar em execução localmente</span><span class="sxs-lookup"><span data-stu-id="0072d-135">Getting up and running locally</span></span>

<span data-ttu-id="0072d-136">Este exemplo é baseado em um aplicativo de exemplo disponível no GitHub, para que possamos clonar e, em seguida, percorrer o código.</span><span class="sxs-lookup"><span data-stu-id="0072d-136">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="0072d-137">Siga as etapas abaixo para obter o código clonado em seu computador:</span><span class="sxs-lookup"><span data-stu-id="0072d-137">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="0072d-138">Navegue até `src/main/resources/META-INF/microprofile-config.properties` e altere as propriedades no arquivo microprofile-config.properties com os detalhes acima.</span><span class="sxs-lookup"><span data-stu-id="0072d-138">Navigate to `src/main/resources/META-INF/microprofile-config.properties` and change the properties in microprofile-config.properties file with details from above.</span></span>

1. <span data-ttu-id="0072d-139">Tente executar o servidor usando `mvn clean package payara-micro:start`</span><span class="sxs-lookup"><span data-stu-id="0072d-139">Try running the server using `mvn clean package payara-micro:start`</span></span>

1. <span data-ttu-id="0072d-140">Tente acessar [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) no seu navegador da Web - você deve ver uma resposta simples que demonstra os valores que estão sendo lidos do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0072d-140">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser - you should see a simple response that demonstrates values being read from Azure Key Vault.</span></span>

## <a name="summary"></a><span data-ttu-id="0072d-141">Resumo</span><span class="sxs-lookup"><span data-stu-id="0072d-141">Summary</span></span>

<span data-ttu-id="0072d-142">Este aplicativo de exemplo junta a API de configuração do MicroProfile, o Azure Key Vault e a biblioteca gratuita e de software livre [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) para permitir a fácil injeção de dados de configuração e segredos em nossos serviços Web do MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="0072d-142">This sample application bakes together the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into our MicroProfile web services.</span></span>
