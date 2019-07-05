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
# <a name="configure-microprofile-by-using-azure-key-vault"></a>Configurar o MicroProfile usando o Azure Key Vault

Este artigo demonstra como configurar um aplicativo do [MicroProfile](http://microprofile.io) para recuperar segredos de um [cofre de chaves do Azure](https://azure.microsoft.com/services/key-vault/). Neste processo, você usará as [APIs de Configuração do MicroProfile](https://microprofile.io/project/eclipse/microprofile-config) para criar uma conexão direta com um cofre de chaves do Azure. Como desenvolvedor, usando as APIs de Configuração do MicroProfile, você se beneficia de uma API padrão para recuperação e injeção de dados de configuração em seus microsserviços.

Antes de começar, dê uma olhada rápida no que uma combinação do Azure Key Vault e da API de Configuração do MicroProfile permite escrever no código. O snippet de código a seguir é de um campo em uma classe que é anotada com `@Inject` e `@ConfigProperty`. O *name* especificado na anotação é o nome da propriedade a ser pesquisado no cofre de chaves, e o *defaultValue* é o que será definido caso a chave não seja descoberta. O resultado é que o valor armazenado no cofre de chaves, ou o valor padrão, é injetado automaticamente no campo em tempo de execução. Essa ação pode simplificar sua vida, porque você não precisa mais passar valores em construtores e métodos setter. Em vez disso, o MicroProfile cuida dessa tarefa.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

Para solicitar segredos, conforme necessário, acesse também a configuração do MicroProfile diretamente. Por exemplo:

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

Esse código de exemplo usa o [Payara Micro](https://www.payara.fish/payara_micro) e o [MicroProfile](https://microprofile.io/) para criar um arquivo WAR (requisito de aplicativo Web) Java pequeno que pode ser executado localmente no computador. Ele não demonstra como converter o código para Docker nem enviá-lo por push ao Azure, mas a seção no final deste artigo contém links para outros tutoriais úteis que explicam como fazer isso.

A amostra usa uma biblioteca de software livre gratuita que cria uma fonte de configuração (usando a API de Configuração do MicroProfile) no cofre de chaves. Para saber mais sobre essa biblioteca e examinar o código, confira a [página do projeto no GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). Se você usar a biblioteca, o código deste tutorial poderá simplesmente se concentrar na configuração da biblioteca e, em seguida, injetar chaves no código. Não é necessário escrever nenhum código específico do Azure.

Para executar esse código no computador local, começando com a criação de um recurso do cofre de chaves, siga as instruções das próximas seções.

## <a name="create-a-key-vault-resource"></a>Criar um recurso do cofre de chaves

Nesta seção, você usará a CLI do Azure para criar um recurso do cofre de chaves e populá-lo com um segredo.

1. Crie uma entidade de serviço do Azure. Essa etapa fornece a ID do cliente e a chave necessárias para acessar o cofre de chaves:

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    Vamos usar *microprofile-keyvault-service-principal* para substituir *\<service_principal_name>* na etapa anterior. A resposta do Azure será semelhante à seguinte:

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    Vale destacar aqui os valores de *appId* e *password*. Você os usará mais adiante neste artigo como a *ID do cliente* e a *chave*.

1. (Opcional) Agora que você criou uma entidade de serviço, crie um grupo de recursos. Caso já tenha um grupo de recursos que deseje usar, ignore esta etapa. Para obter uma lista de localizações do grupo de recursos, chame `az account list-locations` e use o valor de *name* dessa lista para especificar a localização em que o grupo de recursos deve ser criado.

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. Crie um recurso do cofre de chaves. Você usará o nome do cofre de chaves para referenciar o cofre de chaves mais tarde; portanto, escolha um nome fácil de ser lembrado.

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. Conceda as permissões apropriadas à entidade de serviço criada anteriormente, de modo que ela possa acessar os segredos do cofre de chaves. O valor de appId no código a seguir é o valor de *appId* da etapa 1, em que você criou a entidade de serviço. Ou seja, a *appId* na etapa 1 era *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, mas você deverá usar o valor de sua própria saída do terminal.

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. Agora você pode enviar um segredo por push ao cofre de chaves. Use o nome da chave *demo-key* e defina o valor da chave como *demo-value*:

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

É isso! Agora você tem um cofre de chaves em execução no Azure com um único segredo. Agora clone esse repositório e configure-o para usar esse recurso em seu aplicativo.

## <a name="get-up-and-running-locally"></a>Colocá-lo em funcionamento localmente

Este exemplo se baseia em um aplicativo de exemplo disponível no GitHub; portanto, você clonará esse aplicativo e, em seguida, executará o código em etapas. 

1. Clone o código no computador inserindo os seguintes comandos:

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. Acesse *src/main/resources/META-INF/microprofile-config.properties* e, em seguida, altere as propriedades no arquivo *microprofile-config.properties* usando os valores das etapas anteriores.

1. Tente executar o servidor usando `mvn clean package payara-micro:start`.

1. Tente acessar [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) no navegador da Web. Você deverá ver uma resposta simples que demonstra os valores que estão sendo lidos do cofre de chaves.

## <a name="summary"></a>Resumo

Este aplicativo de exemplo combina a API de Configuração do MicroProfile, o Azure Key Vault e a biblioteca de software livre gratuita [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) para permitir a fácil injeção de dados de configuração e segredos em seus serviços Web do MicroProfile.
