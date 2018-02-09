---
title: Como usar o iniciador do Spring Boot para o Azure Key Vault
description: Descubra como configurar um aplicativo inicializador do Spring Boot com o iniciador do Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 52e7dc3f84ea96f22d8e478a597452c76ed8bf22
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="05a10-103">Como usar o iniciador do Spring Boot para o Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="05a10-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="05a10-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="05a10-104">Overview</span></span>

<span data-ttu-id="05a10-105">Este artigo demonstra como criar um aplicativo com o **[Spring Initializr]**, o qual usa o iniciador do Spring Boot para o Azure Key Vault para recuperar uma cadeia de conexão armazenada como um segredo em um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="05a10-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05a10-106">pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="05a10-106">Prerequisites</span></span>

<span data-ttu-id="05a10-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="05a10-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="05a10-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="05a10-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="05a10-109">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="05a10-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="05a10-110">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="05a10-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-the-spring-initialzr"></a><span data-ttu-id="05a10-111">Criar um aplicativo usando o Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="05a10-111">Create an app using the Spring Initialzr</span></span>

1. <span data-ttu-id="05a10-112">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="05a10-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="05a10-113">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="05a10-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar os nomes do grupo e do artefato][secrets-01]

1. <span data-ttu-id="05a10-115">Role para baixo, até a seção **Azure** e marque a caixa do **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="05a10-115">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Selecionar o iniciador do Azure Key Vault][secrets-02]

1. <span data-ttu-id="05a10-117">Role até a parte inferior da página e clique no botão **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="05a10-117">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Gerar projeto do Spring Boot][secrets-03]

1. <span data-ttu-id="05a10-119">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="05a10-119">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="05a10-120">Entre no Azure e selecione a assinatura a ser usada</span><span class="sxs-lookup"><span data-stu-id="05a10-120">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="05a10-121">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="05a10-121">Open a command prompt.</span></span>

1. <span data-ttu-id="05a10-122">Entre em sua conta do Azure usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="05a10-122">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="05a10-123">Siga as instruções na tela para concluir o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="05a10-123">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="05a10-124">Liste suas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="05a10-124">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="05a10-125">O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-125">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. Specify the GUID for the account you want to use with Azure; for example:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a><span data-ttu-id="05a10-126">Criar e configurar um novo Azure Key Vault usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="05a10-126">Create and configure a new Azure Key Vault using the Azure CLI</span></span>

1. <span data-ttu-id="05a10-127">Crie um grupo de recursos para os recursos do Azure que serão usados no seu cofre de chaves. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-127">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="05a10-128">Em que:</span><span class="sxs-lookup"><span data-stu-id="05a10-128">Where:</span></span>
   | <span data-ttu-id="05a10-129">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="05a10-129">Parameter</span></span> | <span data-ttu-id="05a10-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="05a10-130">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="05a10-131">Especifica um nome exclusivo para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="05a10-131">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="05a10-132">Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual seu grupo de recursos será hospedado.</span><span class="sxs-lookup"><span data-stu-id="05a10-132">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="05a10-133">A CLI do Azure exibirá os resultados da criação do grupo de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-133">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

1. <span data-ttu-id="05a10-134">Crie uma entidade de serviço do Azure a partir do registro do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-134">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="05a10-135">Em que:</span><span class="sxs-lookup"><span data-stu-id="05a10-135">Where:</span></span>
   | <span data-ttu-id="05a10-136">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="05a10-136">Parameter</span></span> | <span data-ttu-id="05a10-137">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="05a10-137">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="05a10-138">Especifica o nome para a entidade de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="05a10-138">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="05a10-139">A CLI do Azure retornará uma mensagem de status do JSON que contém o *appId* e a *senha*, o que será usado posteriormente como a ID e senha do cliente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-139">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

1. <span data-ttu-id="05a10-140">Crie um novo cofre de chaves no grupo de recursos. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-140">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="05a10-141">Em que:</span><span class="sxs-lookup"><span data-stu-id="05a10-141">Where:</span></span>
   | <span data-ttu-id="05a10-142">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="05a10-142">Parameter</span></span> | <span data-ttu-id="05a10-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="05a10-143">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="05a10-144">Especifica um nome exclusivo para o seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="05a10-144">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="05a10-145">Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual seu grupo de recursos será hospedado.</span><span class="sxs-lookup"><span data-stu-id="05a10-145">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="05a10-146">Especifica a [opção de implantação do cofre de chaves](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="05a10-146">Specifies the [key vault deployment option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="05a10-147">Especifica a [opção de criptografia do cofre de chaves](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="05a10-147">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="05a10-148">Especifica a [opção de criptografia do cofre de chaves](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="05a10-148">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="05a10-149">Especifica a [opção de SKU do cofre de chaves](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="05a10-149">Specifies the [key vault SKU option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="05a10-150">Especifica um valor a ser recuperado da resposta, que é o URI do cofre de chaves que será necessário para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="05a10-150">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="05a10-151">A CLI do Azure exibirá o URI do cofre de chaves, que será usado posteriormente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-151">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

1. <span data-ttu-id="05a10-152">Defina a política de acesso da entidade de serviço do Azure criada anteriormente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-152">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="05a10-153">Em que:</span><span class="sxs-lookup"><span data-stu-id="05a10-153">Where:</span></span>
   | <span data-ttu-id="05a10-154">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="05a10-154">Parameter</span></span> | <span data-ttu-id="05a10-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="05a10-155">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="05a10-156">Especifica o nome do cofre de chaves de antes.</span><span class="sxs-lookup"><span data-stu-id="05a10-156">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="05a10-157">Especifica as [políticas de segurança](https://docs.microsoft.com/en-us/cli/azure/keyvault) do seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="05a10-157">Specifies the [security policies](https://docs.microsoft.com/en-us/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="05a10-158">Especifica o GUID do seu registro de aplicativo de antes.</span><span class="sxs-lookup"><span data-stu-id="05a10-158">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="05a10-159">A CLI do Azure exibirá os resultados da criação da política de segurança. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-159">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

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

1. <span data-ttu-id="05a10-160">Armazenar um segredo no seu novo cofre de chaves. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-160">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="05a10-161">Em que:</span><span class="sxs-lookup"><span data-stu-id="05a10-161">Where:</span></span>
   | <span data-ttu-id="05a10-162">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="05a10-162">Parameter</span></span> | <span data-ttu-id="05a10-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="05a10-163">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="05a10-164">Especifica o nome do cofre de chaves de antes.</span><span class="sxs-lookup"><span data-stu-id="05a10-164">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="05a10-165">Especifica o nome do seu segredo.</span><span class="sxs-lookup"><span data-stu-id="05a10-165">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="05a10-166">Especifica o valor do seu segredo.</span><span class="sxs-lookup"><span data-stu-id="05a10-166">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="05a10-167">A CLI do Azure exibirá os resultados da criação do segredo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-167">The Azure CLI will display the results of your secret creation; for example:</span></span>  

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

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="05a10-168">Configurar e compilar seu aplicativo Spring Boot</span><span class="sxs-lookup"><span data-stu-id="05a10-168">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="05a10-169">Extraia os arquivos do projeto Spring Boot que você baixou anteriormente em um diretório.</span><span class="sxs-lookup"><span data-stu-id="05a10-169">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

1. <span data-ttu-id="05a10-170">Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* no editor de texto.</span><span class="sxs-lookup"><span data-stu-id="05a10-170">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="05a10-171">Adicione os valores do cofre de chaves usando os valores obtidos nas etapas concluídas anteriormente neste tutorial. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-171">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="05a10-172">Em que:</span><span class="sxs-lookup"><span data-stu-id="05a10-172">Where:</span></span>
   | <span data-ttu-id="05a10-173">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="05a10-173">Parameter</span></span> | <span data-ttu-id="05a10-174">Descrição</span><span class="sxs-lookup"><span data-stu-id="05a10-174">Description</span></span> |
   |---|---|
   | `azure.keyvault.uri` | <span data-ttu-id="05a10-175">Especifica o URI de quando você criou seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="05a10-175">Specifies the URI from when you created your key vault.</span></span> |
   | `azure.keyvault.client-id` | <span data-ttu-id="05a10-176">Especifica o GUID da *appId* de quando você criou a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="05a10-176">Specifies the *appId* GUID from when you created your service principal.</span></span> |
   | `azure.keyvault.client-key` | <span data-ttu-id="05a10-177">Especifica o GUID da *senha* de quando você criou a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="05a10-177">Specifies the *password* GUID from when you created your service principal.</span></span> |

1. <span data-ttu-id="05a10-178">Navegue até o arquivo de código-fonte principal do projeto. Por exemplo: */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="05a10-178">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

1. <span data-ttu-id="05a10-179">Abra o arquivo Java principal do aplicativo em um editor de texto, por exemplo *SecretsApplication.java*, e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="05a10-179">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

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
   <span data-ttu-id="05a10-180">Este exemplo de código recupera a cadeia de conexão do cofre de chaves e a exibe à linha de comando.</span><span class="sxs-lookup"><span data-stu-id="05a10-180">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

1. <span data-ttu-id="05a10-181">Salve e feche o arquivo Java.</span><span class="sxs-lookup"><span data-stu-id="05a10-181">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="05a10-182">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="05a10-182">Build and test your app</span></span>

1. <span data-ttu-id="05a10-183">Navegue até o diretório no qual o arquivo *pom.xml* do seu aplicativo Spring Boot está localizado:</span><span class="sxs-lookup"><span data-stu-id="05a10-183">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="05a10-184">Crie seu aplicativo Spring Boot com o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-184">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="05a10-185">O Maven exibirá os resultados de seu build.</span><span class="sxs-lookup"><span data-stu-id="05a10-185">Maven will display the results of your build.</span></span>

   ![Status do build do aplicativo Spring Boot][build-application-01]

1. <span data-ttu-id="05a10-187">Execute o aplicativo Spring Boot com o Maven. O aplicativo exibirá a cadeia de conexão do seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="05a10-187">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="05a10-188">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="05a10-188">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Mensagem do tempo de execução do Spring Boot][build-application-02]

## <a name="next-steps"></a><span data-ttu-id="05a10-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05a10-190">Next steps</span></span>

<span data-ttu-id="05a10-191">Para obter mais informações sobre como usar o Azure Key Vault, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="05a10-191">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="05a10-192">[Documentação do Key Vault].</span><span class="sxs-lookup"><span data-stu-id="05a10-192">[Key Vault Documentation].</span></span>

* <span data-ttu-id="05a10-193">[Introdução ao Cofre da Chave do Azure]</span><span class="sxs-lookup"><span data-stu-id="05a10-193">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="05a10-194">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="05a10-194">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="05a10-195">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="05a10-195">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="05a10-196">Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="05a10-196">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="05a10-197">Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="05a10-197">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

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
