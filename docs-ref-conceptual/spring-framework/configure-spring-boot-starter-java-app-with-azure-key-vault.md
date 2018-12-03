---
title: Como usar o iniciador do Spring Boot para o Azure Key Vault
description: Descubra como configurar um aplicativo inicializador do Spring Boot com o iniciador do Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: fcb18de809f4465239f1f360a755624a5095e03a
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339150"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="19d2e-103">Como usar o iniciador do Spring Boot para o Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="19d2e-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="19d2e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="19d2e-104">Overview</span></span>

<span data-ttu-id="19d2e-105">Este artigo demonstra como criar um aplicativo com o **[Spring Initializr]**, o qual usa o iniciador do Spring Boot para o Azure Key Vault para recuperar uma cadeia de conexão armazenada como um segredo em um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="19d2e-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19d2e-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="19d2e-106">Prerequisites</span></span>

<span data-ttu-id="19d2e-107">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="19d2e-108">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [Benefícios do assinante do MSDN] ou inscrever-se para uma [conta do Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="19d2e-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="19d2e-109">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="19d2e-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="19d2e-110">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="19d2e-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="19d2e-111">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="19d2e-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="19d2e-112">Criar um aplicativo usando o Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="19d2e-112">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="19d2e-113">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="19d2e-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="19d2e-114">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="19d2e-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Especificar os nomes do grupo e do artefato][secrets-01]

1. <span data-ttu-id="19d2e-116">Role para baixo, até a seção **Azure** e marque a caixa do **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="19d2e-116">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Selecionar o iniciador do Azure Key Vault][secrets-02]

1. <span data-ttu-id="19d2e-118">Role até a parte inferior da página e clique no botão **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="19d2e-118">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Gerar projeto do Spring Boot][secrets-03]

1. <span data-ttu-id="19d2e-120">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="19d2e-120">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure"></a><span data-ttu-id="19d2e-121">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="19d2e-121">Sign into Azure</span></span>

1. <span data-ttu-id="19d2e-122">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="19d2e-122">Open a command prompt.</span></span>

1. <span data-ttu-id="19d2e-123">Entre em sua conta do Azure usando a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="19d2e-123">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="19d2e-124">Siga as instruções na tela para concluir o processo de entrada.</span><span class="sxs-lookup"><span data-stu-id="19d2e-124">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="19d2e-125">Liste suas assinaturas:</span><span class="sxs-lookup"><span data-stu-id="19d2e-125">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="19d2e-126">O Azure retornará uma lista de suas assinaturas, e será preciso copiar o GUID para a assinatura que deseja usar. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-126">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="19d2e-127">Especifique o GUID para a conta que quer usar no Azure; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-127">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-a-new-azure-key-vault"></a><span data-ttu-id="19d2e-128">Crie um novo Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="19d2e-128">Create a new Azure Key Vault</span></span>

1. <span data-ttu-id="19d2e-129">Crie um grupo de recursos para os recursos do Azure que serão usados no seu cofre de chaves. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-129">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="19d2e-130">Em que:</span><span class="sxs-lookup"><span data-stu-id="19d2e-130">Where:</span></span>

   | <span data-ttu-id="19d2e-131">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="19d2e-131">Parameter</span></span> | <span data-ttu-id="19d2e-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="19d2e-132">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="19d2e-133">Especifica um nome exclusivo para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="19d2e-133">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="19d2e-134">Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual seu grupo de recursos será hospedado.</span><span class="sxs-lookup"><span data-stu-id="19d2e-134">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="19d2e-135">A CLI do Azure exibirá os resultados da criação do grupo de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-135">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

2. <span data-ttu-id="19d2e-136">Crie uma entidade de serviço do Azure a partir do registro do seu aplicativo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-136">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="19d2e-137">Em que:</span><span class="sxs-lookup"><span data-stu-id="19d2e-137">Where:</span></span>

   | <span data-ttu-id="19d2e-138">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="19d2e-138">Parameter</span></span> | <span data-ttu-id="19d2e-139">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="19d2e-139">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="19d2e-140">Especifica o nome para a entidade de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="19d2e-140">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="19d2e-141">A CLI do Azure retornará uma mensagem de status do JSON que contém o *appId* e a *senha*, o que será usado posteriormente como a ID e senha do cliente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-141">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. <span data-ttu-id="19d2e-142">Crie um novo cofre de chaves no grupo de recursos. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-142">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="19d2e-143">Em que:</span><span class="sxs-lookup"><span data-stu-id="19d2e-143">Where:</span></span>

   | <span data-ttu-id="19d2e-144">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="19d2e-144">Parameter</span></span> | <span data-ttu-id="19d2e-145">Descrição</span><span class="sxs-lookup"><span data-stu-id="19d2e-145">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="19d2e-146">Especifica um nome exclusivo para o seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="19d2e-146">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="19d2e-147">Especifica a [região do Azure](https://azure.microsoft.com/regions/) na qual seu grupo de recursos será hospedado.</span><span class="sxs-lookup"><span data-stu-id="19d2e-147">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="19d2e-148">Especifica a [opção de implantação do cofre de chaves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="19d2e-148">Specifies the [key vault deployment option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="19d2e-149">Especifica a [opção de criptografia do cofre de chaves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="19d2e-149">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="19d2e-150">Especifica a [opção de criptografia do cofre de chaves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="19d2e-150">Specifies the [key vault encryption option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="19d2e-151">Especifica a [opção de SKU do cofre de chaves](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="19d2e-151">Specifies the [key vault SKU option](https://docs.microsoft.com/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="19d2e-152">Especifica um valor a ser recuperado da resposta, que é o URI do cofre de chaves que será necessário para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="19d2e-152">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="19d2e-153">A CLI do Azure exibirá o URI do cofre de chaves, que será usado posteriormente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-153">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. <span data-ttu-id="19d2e-154">Defina a política de acesso da entidade de serviço do Azure criada anteriormente. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-154">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="19d2e-155">Em que:</span><span class="sxs-lookup"><span data-stu-id="19d2e-155">Where:</span></span>

   | <span data-ttu-id="19d2e-156">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="19d2e-156">Parameter</span></span> | <span data-ttu-id="19d2e-157">Descrição</span><span class="sxs-lookup"><span data-stu-id="19d2e-157">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="19d2e-158">Especifica o nome do cofre de chaves de antes.</span><span class="sxs-lookup"><span data-stu-id="19d2e-158">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="19d2e-159">Especifica as [políticas de segurança](https://docs.microsoft.com/cli/azure/keyvault) do seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="19d2e-159">Specifies the [security policies](https://docs.microsoft.com/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="19d2e-160">Especifica o GUID do seu registro de aplicativo de antes.</span><span class="sxs-lookup"><span data-stu-id="19d2e-160">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="19d2e-161">A CLI do Azure exibirá os resultados da criação da política de segurança. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-161">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

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

5. <span data-ttu-id="19d2e-162">Armazenar um segredo no seu novo cofre de chaves. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-162">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="19d2e-163">Em que:</span><span class="sxs-lookup"><span data-stu-id="19d2e-163">Where:</span></span>

   | <span data-ttu-id="19d2e-164">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="19d2e-164">Parameter</span></span> | <span data-ttu-id="19d2e-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="19d2e-165">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="19d2e-166">Especifica o nome do cofre de chaves de antes.</span><span class="sxs-lookup"><span data-stu-id="19d2e-166">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="19d2e-167">Especifica o nome do seu segredo.</span><span class="sxs-lookup"><span data-stu-id="19d2e-167">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="19d2e-168">Especifica o valor do seu segredo.</span><span class="sxs-lookup"><span data-stu-id="19d2e-168">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="19d2e-169">A CLI do Azure exibirá os resultados da criação do segredo. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-169">The Azure CLI will display the results of your secret creation; for example:</span></span>  

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

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="19d2e-170">Configurar e compilar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="19d2e-170">Configure and compile your app</span></span>

1. <span data-ttu-id="19d2e-171">Extraia os arquivos do projeto Spring Boot que você baixou anteriormente em um diretório.</span><span class="sxs-lookup"><span data-stu-id="19d2e-171">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

2. <span data-ttu-id="19d2e-172">Navegue até a pasta *src/main/resources* no seu projeto e abra o arquivo *application.properties* no editor de texto.</span><span class="sxs-lookup"><span data-stu-id="19d2e-172">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

3. <span data-ttu-id="19d2e-173">Adicione os valores do cofre de chaves usando os valores obtidos nas etapas concluídas anteriormente neste tutorial. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-173">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="19d2e-174">Em que:</span><span class="sxs-lookup"><span data-stu-id="19d2e-174">Where:</span></span>

   |          <span data-ttu-id="19d2e-175">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="19d2e-175">Parameter</span></span>          |                                 <span data-ttu-id="19d2e-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="19d2e-176">Description</span></span>                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           <span data-ttu-id="19d2e-177">Especifica o URI de quando você criou seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="19d2e-177">Specifies the URI from when you created your key vault.</span></span>           |
   | `azure.keyvault.client-id`  |  <span data-ttu-id="19d2e-178">Especifica o GUID da *appId* de quando você criou a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="19d2e-178">Specifies the *appId* GUID from when you created your service principal.</span></span>   |
   | `azure.keyvault.client-key` | <span data-ttu-id="19d2e-179">Especifica o GUID da *senha* de quando você criou a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="19d2e-179">Specifies the *password* GUID from when you created your service principal.</span></span> |


4. <span data-ttu-id="19d2e-180">Navegue até o arquivo de código-fonte principal do projeto. Por exemplo: */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="19d2e-180">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

5. <span data-ttu-id="19d2e-181">Abra o arquivo Java principal do aplicativo em um editor de texto, por exemplo *SecretsApplication.java*, e adicione as seguintes linhas ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-181">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

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
   <span data-ttu-id="19d2e-182">Este exemplo de código recupera a cadeia de conexão do cofre de chaves e a exibe à linha de comando.</span><span class="sxs-lookup"><span data-stu-id="19d2e-182">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

6. <span data-ttu-id="19d2e-183">Salve e feche o arquivo Java.</span><span class="sxs-lookup"><span data-stu-id="19d2e-183">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="19d2e-184">Crie e testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="19d2e-184">Build and test your app</span></span>

1. <span data-ttu-id="19d2e-185">Navegue até o diretório no qual o arquivo *pom.xml* do seu aplicativo Spring Boot está localizado:</span><span class="sxs-lookup"><span data-stu-id="19d2e-185">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="19d2e-186">Crie seu aplicativo Spring Boot com o Maven. Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-186">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="19d2e-187">O Maven exibirá os resultados de seu build.</span><span class="sxs-lookup"><span data-stu-id="19d2e-187">Maven will display the results of your build.</span></span>

   ![Status do build do aplicativo Spring Boot][build-application-01]

1. <span data-ttu-id="19d2e-189">Execute o aplicativo Spring Boot com o Maven. O aplicativo exibirá a cadeia de conexão do seu cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="19d2e-189">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="19d2e-190">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="19d2e-190">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Mensagem do tempo de execução do Spring Boot][build-application-02]

## <a name="summary"></a><span data-ttu-id="19d2e-192">Resumo</span><span class="sxs-lookup"><span data-stu-id="19d2e-192">Summary</span></span>

<span data-ttu-id="19d2e-193">Neste tutorial, você criou um novo aplicativo Web Java usando o **[Spring Initializr]**, criou um Azure Key Vault para armazenar informações confidenciais e, por fim, configurou o aplicativo para recuperar informações do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="19d2e-193">In this tutorial, you created a new Java web application using the **[Spring Initializr]**, created ab Azure Key Vault to store sensitive information, and then configured your application to retrieve information from your key vault.</span></span>

<span data-ttu-id="19d2e-194">Para obter mais informações sobre como usar o Azure Key Vault, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="19d2e-194">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="19d2e-195">[Documentação do Key Vault].</span><span class="sxs-lookup"><span data-stu-id="19d2e-195">[Key Vault Documentation].</span></span>

* <span data-ttu-id="19d2e-196">[Introdução ao Cofre da Chave do Azure]</span><span class="sxs-lookup"><span data-stu-id="19d2e-196">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="19d2e-197">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="19d2e-197">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="19d2e-198">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="19d2e-198">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="19d2e-199">Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="19d2e-199">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="19d2e-200">Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="19d2e-200">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

## <a name="next-steps"></a><span data-ttu-id="19d2e-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19d2e-201">Next steps</span></span>

<span data-ttu-id="19d2e-202">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="19d2e-202">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="19d2e-203">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="19d2e-203">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Documentação do Key Vault]: /azure/key-vault/
[Key Vault Documentation]: /azure/key-vault/
[Introdução ao Cofre da Chave do Azure]: /azure/key-vault/key-vault-get-started
[Get started with Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[conta do Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Benefícios do assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
