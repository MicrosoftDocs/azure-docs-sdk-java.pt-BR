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
# <a name="configure-microprofile-with-azure-key-vault"></a>Configurar MicroProfile com o Azure Key Vault

Este tutorial demonstra como configurar um aplicativo [MicroProfile](http://microprofile.io) para recuperar segredos do [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) usando as [APIS de configuração do MicroProfile](https://microprofile.io/project/eclipse/microprofile-config) para criar uma conexão direta ao Azure Key Vault. Usando as APIs de configuração do MicroProfile, os desenvolvedores se beneficiam de uma API padrão para recuperação e injeção de dados de configuração em seus microsserviços.

Antes de nos aprofundarmos, vamos dar uma olhada no que uma combinação entre o Azure Key Vault e a API de configuração do MicroProfile nos permite escrever em nosso código. Aqui está um trecho de código de um campo em uma classe que foi anotada com `@Inject` e `@ConfigProperty`. A `name` especificada na anotação é o nome da propriedade para pesquisar no Azure Key Vault e `defaultValue` é o que será definido se a chave não for descoberta. O resultado final é que o valor armazenado no Azure Key Vault ou o valor padrão, será injetado automaticamente no campo em tempo de execução, simplificando a vida dos desenvolvedores, pois eles não precisam mais passar valores em torno de métodos constuctors e um setter, deixando isso para o MicroProfile manipular.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

Também é possível acessar a configuração de MicroProfile diretamente, para solicitar segredos conforme necessário, por exemplo:

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

Este exemplo utiliza [Payara Micro](https://www.payara.fish/payara_micro) e [MicroProfile](https://microprofile.io/) para criar um arquivo war Java pequeno que pode ser executado localmente em seu computador. Ele não demonstra como dockerizar ou enviar por push o código para o Azure, mas a seção de links no final deste tutorial tem links para outros tutoriais úteis que explicam isso.

Este exemplo usa uma biblioteca de software livre gratuita que cria uma fonte de configuração (usando a API de configuração do MicroProfile) para o Azure Key Vault. Você pode saber mais sobre essa biblioteca e examine o código na [página do projeto GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). Ao usar essa biblioteca, o código neste tutorial pode se focar simplesmente na configuração da biblioteca, seguido pela injeção de chaves no seu código e não precisamos escrever nenhum código específico do Azure.

Aqui estão as etapas necessárias para executar esse código em seu computador local, começando com a criação de um recurso do Azure Key Vault.

## <a name="creating-an-azure-key-vault-resource"></a>Criar um recurso do Azure Key Vault

Nós usaremos a CLI do Azure para criar o recurso do Azure Key Vault e preenchê-lo com um segredo.

1. Primeiro, vamos criar uma entidade de serviço do Azure. Isso fornecerá a ID do cliente e a chave necessária para acessar o Key Vault:

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

Vamos dizer que usamos `microprofile-keyvault-service-principal` para o nome da entidade de serviço na etapa anterior. A resposta do Azure para isso estará no formulário a seguir, um pouco censurado:

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

O que deve ser observado aqui são os valores `appID` e `password` - esses são os valores que usaremos mais tarde como `client ID` e `key`, respectivamente.

Agora que criamos uma entidade de serviço, podemos, opcionalmente, criar um grupo de recursos (se você já tiver um que deseja usar, você pode ignorar esta etapa). Observe que, para obter uma lista de locais de grupo de recursos, você pode chamar `az account list-locations` e usar o valor `name` nessa lista para especificar onde o grupo de recursos deve ser criado.

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

Agora criamos um recurso do Azure Key Vault. Observe que o nome do Key Vault é o que você usará para referenciar o cofre de chaves mais tarde, então escolha algo fácil de lembrar.

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

Também é necessário conceder as permissões apropriadas para a entidade de serviço criada anteriormente, para que ela possa acessar os segredos do Key Vault. Observe que o valor de appID é o valor `appId` mencionado acima onde criamos a entidade de serviço (ou seja, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79` - mas use o valor da sua saída do terminal).

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

Agora estamos no ponto onde podemos enviar por push um segredo para o Key Vault. Vamos usar o nome da chave `demo-key` e defina o valor da chave para `demo-value`:

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

É isso! Agora temos o Key Vault em execução no Azure com um segredo único. Agora podemos clonar esse repositório e configurá-lo para usar esse recurso em nosso aplicativo.

## <a name="getting-up-and-running-locally"></a>Colocar em execução localmente

Este exemplo é baseado em um aplicativo de exemplo disponível no GitHub, para que possamos clonar e, em seguida, percorrer o código. Siga as etapas abaixo para obter o código clonado em seu computador:

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. Navegue até `src/main/resources/META-INF/microprofile-config.properties` e altere as propriedades no arquivo microprofile-config.properties com os detalhes acima.

1. Tente executar o servidor usando `mvn clean package payara-micro:start`

1. Tente acessar [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) no seu navegador da Web - você deve ver uma resposta simples que demonstra os valores que estão sendo lidos do Azure Key Vault.

## <a name="summary"></a>Resumo

Este aplicativo de exemplo junta a API de configuração do MicroProfile, o Azure Key Vault e a biblioteca gratuita e de software livre [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) para permitir a fácil injeção de dados de configuração e segredos em nossos serviços Web do MicroProfile.
