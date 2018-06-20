---
title: Como usar o iniciador do Spring Boot para o Azure Key Vault
description: Descubra como configurar um aplicativo inicializador do Spring Boot com o iniciador do Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 1dda697cac80a6cad3ebbbbf8a5a4f18b515dfd8
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33883679"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a>Como usar o iniciador do Spring Boot para o Azure Key Vault

## <a name="overview"></a>Visão geral

Este artigo demonstra como criar um aplicativo com o **[Spring Initializr]**, o qual usa o iniciador do Spring Boot para o Azure Key Vault para recuperar uma cadeia de conexão armazenada como um segredo em um cofre de chaves.

## <a name="prerequisites"></a>pré-requisitos

Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:

* Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].
* Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.
* [Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.

## <a name="create-an-app-using-the-spring-initialzr"></a>Criar um aplicativo usando o Spring Initialzr

1. Navegue até <https://start.spring.io/>.

1. Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.

   ![Especificar os nomes do grupo e do artefato][secrets-01]

1. Role para baixo, até a seção **Azure** e marque a caixa do **Azure Key Vault**.

   ![Selecionar o iniciador do Azure Key Vault][secrets-02]

1. Role até a parte inferior da página e clique no botão **Gerar Projeto**.

   ![Gerar projeto do Spring Boot][secrets-03]

1. Quando solicitado, baixe o projeto para um caminho no computador local.

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a>Entre no Azure e selecione a assinatura a ser usada

1. Abra um prompt de comando.

1. Entre em sua conta do Azure usando a CLI do Azure:

   ```azurecli
   az login
   ```
   Siga as instruções na tela para concluir o processo de entrada.

1. Liste suas assinaturas:

   ```azurecli
   az account list
   ```
   O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. Especifique o GUID para a conta que quer usar no Azure; por exemplo:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a>Criar e configurar um novo Azure Key Vault usando a CLI do Azure

1. Crie um grupo de recursos para os recursos do Azure que serão usados no seu cofre de chaves. Por exemplo:
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   Em que:
   | Parâmetro | Descrição |
   |---|---|
   | `name` | Especifica um nome exclusivo para o grupo de recursos. |
   | `location` | Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual seu grupo de recursos será hospedado. |

   A CLI do Azure exibirá os resultados da criação do grupo de recursos, por exemplo:  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

1. Crie uma entidade de serviço do Azure a partir do registro do seu aplicativo. Por exemplo:
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   Em que:
   | Parâmetro | DESCRIÇÃO |
   |---|---|
   | `name` | Especifica o nome para a entidade de serviço do Azure. |

   A CLI do Azure retornará uma mensagem de status do JSON que contém o *appId* e a *senha*, o que será usado posteriormente como a ID e senha do cliente. Por exemplo:

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

1. Crie um novo cofre de chaves no grupo de recursos. Por exemplo:
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   Em que:
   | Parâmetro | Descrição |
   |---|---|
   | `name` | Especifica um nome exclusivo para o seu cofre de chaves. |
   | `location` | Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual seu grupo de recursos será hospedado. |
   | `enabled-for-deployment` | Especifica a [opção de implantação do cofre de chaves](https://docs.microsoft.com/en-us/cli/azure/keyvault). |
   | `enabled-for-disk-encryption` | Especifica a [opção de criptografia do cofre de chaves](https://docs.microsoft.com/en-us/cli/azure/keyvault). |
   | `enabled-for-template-deployment` | Especifica a [opção de criptografia do cofre de chaves](https://docs.microsoft.com/en-us/cli/azure/keyvault). |
   | `sku` | Especifica a [opção de SKU do cofre de chaves](https://docs.microsoft.com/en-us/cli/azure/keyvault). |
   | `query` | Especifica um valor a ser recuperado da resposta, que é o URI do cofre de chaves que será necessário para concluir este tutorial. |

   A CLI do Azure exibirá o URI do cofre de chaves, que será usado posteriormente. Por exemplo:  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

1. Defina a política de acesso da entidade de serviço do Azure criada anteriormente. Por exemplo:
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   Em que:
   | Parâmetro | Descrição |
   |---|---|
   | `name` | Especifica o nome do cofre de chaves de antes. |
   | `secret-permission` | Especifica as [políticas de segurança](https://docs.microsoft.com/en-us/cli/azure/keyvault) do seu cofre de chaves. |
   | `spn` | Especifica o GUID do seu registro de aplicativo de antes. |

   A CLI do Azure exibirá os resultados da criação da política de segurança. Por exemplo:  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "location": "westus",
     "name": "wingtiptoyskeyvault",
     "properties": {
       ...
       ... (A long list of values will be displayed here.)
       ...
     },
     "resourceGroup": "wingtiptoysresources",
     "tags": {},
     "type": "Microsoft.KeyVault/vaults"
   }
   ```

1. Armazenar um segredo no seu novo cofre de chaves. Por exemplo:
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   Em que:
   | Parâmetro | Descrição |
   |---|---|
   | `vault-name` | Especifica o nome do cofre de chaves de antes. |
   | `name` | Especifica o nome do seu segredo. |
   | `value` | Especifica o valor do seu segredo. |

   A CLI do Azure exibirá os resultados da criação do segredo. Por exemplo:  

   ```json
   {
     "attributes": {
       "created": "2017-12-01T09:00:16+00:00",
       "enabled": true,
       "expires": null,
       "notBefore": null,
       "recoveryLevel": "Purgeable",
       "updated": "2017-12-01T09:00:16+00:00"
     },
     "contentType": null,
     "id": "https://wingtiptoyskeyvault.vault.azure.net/secrets/connectionString/123456789abcdef123456789abcdef",
     "kid": null,
     "managed": null,
     "tags": {
       "file-encoding": "utf-8"
     },
     "value": "jdbc:sqlserver://wingtiptoys.database.windows.net:1433;database=DATABASE;"
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a>Configurar e compilar seu aplicativo Spring Boot

1. Extraia os arquivos do projeto Spring Boot que você baixou anteriormente em um diretório.

1. Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* no editor de texto.

1. Adicione os valores do cofre de chaves usando os valores obtidos nas etapas concluídas anteriormente neste tutorial. Por exemplo:
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   Em que:
   | Parâmetro | Descrição |
   |---|---|
   | `azure.keyvault.uri` | Especifica o URI de quando você criou seu cofre de chaves. |
   | `azure.keyvault.client-id` | Especifica o GUID da *appId* de quando você criou a entidade de serviço. |
   | `azure.keyvault.client-key` | Especifica o GUID da *senha* de quando você criou a entidade de serviço. |

1. Navegue até o arquivo de código-fonte principal do projeto. Por exemplo: */src/main/java/com/wingtiptoys/secrets*.

1. Abra o arquivo Java principal do aplicativo em um editor de texto, por exemplo *SecretsApplication.java*, e adicione as seguintes linhas ao arquivo:

   ```java
   package com.wingtiptoys.secrets;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class SecretsApplication implements CommandLineRunner {

      @Value("${connectionString}")
      private String connectionString;

      public static void main(String[] args) {
         SpringApplication.run(SecretsApplication.class, args);
      }

      public void run(String... varl) throws Exception {
         System.out.println(String.format("\nConnection String stored in Azure Key Vault:\n%s\n",connectionString));
      }
   }
   ```
   Este exemplo de código recupera a cadeia de conexão do cofre de chaves e a exibe à linha de comando.

1. Salve e feche o arquivo Java.

## <a name="build-and-test-your-app"></a>Crie e testar seu aplicativo

1. Navegue até o diretório no qual o arquivo *pom.xml* do seu aplicativo Spring Boot está localizado:

1. Crie seu aplicativo Spring Boot com o Maven. Por exemplo:

   ```bash
   mvn clean package
   ```

   O Maven exibirá os resultados de seu build.

   ![Status do build do aplicativo Spring Boot][build-application-01]

1. Execute o aplicativo Spring Boot com o Maven. O aplicativo exibirá a cadeia de conexão do seu cofre de chaves. Por exemplo:

   ```bash
   mvn spring-boot:run
   ```

   ![Mensagem do tempo de execução do Spring Boot][build-application-02]

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar o Azure Key Vault, consulte os seguintes artigos:

* [Documentação do Key Vault].

* [Introdução ao Cofre da Chave do Azure]

Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:

* [Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].

<!-- URL List -->

[Documentação do Key Vault]: /azure/key-vault/
[Introdução ao Cofre da Chave do Azure]: /azure/key-vault/key-vault-get-started
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
