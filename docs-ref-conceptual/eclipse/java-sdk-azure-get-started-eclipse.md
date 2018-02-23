---
title: "Introdução ao Azure para Java usando o Eclipse"
description: "Introdução ao uso básico das bibliotecas do Azure para Java com sua própria assinatura do Azure."
keywords: "Azure, Java, SDK, API, autenticar, introdução"
services: 
documentationcenter: java
author: roygara
manager: timlt
editor: 
ms.author: v-rogara
ms.date: 02/01/2018
ms.devlang: java
ms.prod: azure
ms.technology: azure
ms.topic: get-started-article
ms.service: multiple
ms.openlocfilehash: 740679197981f49d99b8d8251e257963d3030fb1
ms.sourcegitcommit: 720c2eaf66532d277015610ec375c71e934d9ee6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="get-started-with-the-azure-libraries-using-eclipse"></a><span data-ttu-id="38f9a-104">Introdução às bibliotecas do Azure usando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="38f9a-104">Get started with the Azure libraries using Eclipse</span></span>

<span data-ttu-id="38f9a-105">Este guia orienta em relação à configuração de um ambiente de desenvolvimento e ao uso de bibliotecas do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="38f9a-105">This guide walks you through setting up a development environment and using the Azure libraries for Java.</span></span> <span data-ttu-id="38f9a-106">Você vai criar uma entidade de serviço para autenticar com o Azure e executar um código de exemplo que cria e usa recursos do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="38f9a-106">You'll create a service principal to authenticate with Azure and run some sample code that creates and uses Azure resources in your subscription.</span></span> <span data-ttu-id="38f9a-107">Usar o Eclipse é opcional para desenvolvimento Java com o Azure.</span><span class="sxs-lookup"><span data-stu-id="38f9a-107">Using Eclipse is optional for Java development with Azure.</span></span> <span data-ttu-id="38f9a-108">Qualquer IDE que tenha integração com o Maven funciona.</span><span class="sxs-lookup"><span data-stu-id="38f9a-108">Any IDE that has Maven integration works.</span></span> <span data-ttu-id="38f9a-109">Como alternativa, você pode executar o código a partir da linha de comando usando Maven, caso prefira não usar nenhum IDE.</span><span class="sxs-lookup"><span data-stu-id="38f9a-109">Alternatively, you can run your code from the commandline using Maven if you prefer not to use any IDE.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38f9a-110">pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="38f9a-110">Prerequisites</span></span>

- <span data-ttu-id="38f9a-111">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="38f9a-111">An Azure account.</span></span> <span data-ttu-id="38f9a-112">Se você não tiver uma, [obtenha uma avaliação gratuita](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="38f9a-112">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="38f9a-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) ou [CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="38f9a-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="38f9a-114">A última versão estável do [Eclipse](http://www.eclipse.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="38f9a-114">The latest stable version of [Eclipse](http://www.eclipse.org/downloads/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="38f9a-115">Configurar a autenticação</span><span class="sxs-lookup"><span data-stu-id="38f9a-115">Set up authentication</span></span>

<span data-ttu-id="38f9a-116">Seu aplicativo Java precisa ler e criar permissões em sua assinatura do Azure para executar o exemplo de código neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="38f9a-116">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="38f9a-117">Criar uma entidade de serviço e configurar seu aplicativo para ser executado com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="38f9a-117">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="38f9a-118">As entidades de serviço fornecem uma maneira de criar uma conta não interativa associada à sua identidade para a qual você concede apenas os privilégios de que seu aplicativo precisa para ser executado.</span><span class="sxs-lookup"><span data-stu-id="38f9a-118">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="38f9a-119">[Criar uma entidade de serviço](/cli/azure/create-an-azure-service-principal-azure-cli) para conceder ao seu código permissão para criar e atualizar recursos em sua assinatura sem usar diretamente as credenciais de conta.</span><span class="sxs-lookup"><span data-stu-id="38f9a-119">[Create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli) to grant your code permission to create and update resources in your subscription without using your account credentials directly.</span></span> <span data-ttu-id="38f9a-120">Verifique se capturou a saída.</span><span class="sxs-lookup"><span data-stu-id="38f9a-120">Make sure to capture the output.</span></span> <span data-ttu-id="38f9a-121">Forneça uma [senha segura](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) no argumento de senha, em vez de `MY_SECURE_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="38f9a-121">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="38f9a-122">A senha deve ter de 8 a 16 caracteres e satisfazer pelo menos 3 dos 4 critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="38f9a-122">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="38f9a-123">Incluir caracteres minúsculos</span><span class="sxs-lookup"><span data-stu-id="38f9a-123">Include lowercase characters</span></span>
* <span data-ttu-id="38f9a-124">Incluir caracteres maiúsculos</span><span class="sxs-lookup"><span data-stu-id="38f9a-124">Include uppercase characters</span></span>
* <span data-ttu-id="38f9a-125">Incluir números</span><span class="sxs-lookup"><span data-stu-id="38f9a-125">Include numbers</span></span>
* <span data-ttu-id="38f9a-126">Incluir um dos seguintes símbolos: @ # $ % ^ & \* - _ !</span><span class="sxs-lookup"><span data-stu-id="38f9a-126">Include one of the following symbols: @ # $ % ^ & \* - _ !</span></span> <span data-ttu-id="38f9a-127">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="38f9a-127">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="38f9a-128">?</span><span class="sxs-lookup"><span data-stu-id="38f9a-128">?</span></span> <span data-ttu-id="38f9a-129">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="38f9a-129">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="38f9a-130">O que lhe dá uma resposta no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="38f9a-130">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="38f9a-131">Em seguida, copie o seguinte em um arquivo de texto no seu sistema:</span><span class="sxs-lookup"><span data-stu-id="38f9a-131">Next, copy the following into a text file on your system:</span></span>

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

<span data-ttu-id="38f9a-132">Substitua os quatro valores principais pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="38f9a-132">Replace the top four values with the following:</span></span>

- <span data-ttu-id="38f9a-133">assinatura: usar o valor *id* de `az account show` na CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="38f9a-133">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="38f9a-134">cliente: usar o valor *appId* da saída obtida de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="38f9a-134">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="38f9a-135">chave: usar o valor da *senha* da saída da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="38f9a-135">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="38f9a-136">locatário: usar o valor do *locatário* da saída da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="38f9a-136">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="38f9a-137">Salve esse arquivo em um local seguro no sistema onde o seu código possa lê-lo.</span><span class="sxs-lookup"><span data-stu-id="38f9a-137">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="38f9a-138">Você pode usar esse arquivo para um código futuro, então é recomendável armazená-lo em algum lugar externo ao aplicativo neste artigo.</span><span class="sxs-lookup"><span data-stu-id="38f9a-138">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span>

<span data-ttu-id="38f9a-139">Defina uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo de autenticação no seu shell.</span><span class="sxs-lookup"><span data-stu-id="38f9a-139">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="38f9a-140">Se estiver trabalhando em um ambiente Windows, adicione a variável às propriedades do sistema.</span><span class="sxs-lookup"><span data-stu-id="38f9a-140">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="38f9a-141">Abra uma janela do PowerShell com privilégios de administrador e, depois de substituir a segunda variável pelo caminho do seu arquivo, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="38f9a-141">Open a PowerShell window with administrator privledges and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="38f9a-142">Criar um novo projeto Maven</span><span class="sxs-lookup"><span data-stu-id="38f9a-142">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="38f9a-143">Este guia usa a ferramenta de compilação Maven para compilar e executar o exemplo de código, mas outras ferramentas de compilação como Gradle também funcionam com as bibliotecas do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="38f9a-143">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="38f9a-144">Abra o Eclipse e selecione **Arquivo** -> **Novo**.</span><span class="sxs-lookup"><span data-stu-id="38f9a-144">Open Eclipse, select **File** -> **New**.</span></span> <span data-ttu-id="38f9a-145">Na nova janela exibida, abra a pasta do Maven e selecione projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="38f9a-145">In the new window that appears open the Maven folder then select Maven Project.</span></span> 

<span data-ttu-id="38f9a-146">Mantenha as seleções na próxima tela no padrão e selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="38f9a-146">Leave the selections on the next screen defaults, and select **Next**.</span></span> <span data-ttu-id="38f9a-147">Faça o mesmo nessa tela quanto aos arquétipos.</span><span class="sxs-lookup"><span data-stu-id="38f9a-147">Do the same for this screen regarding archetypes.</span></span>

<span data-ttu-id="38f9a-148">Ao chegar à tela solicitando groupID, ArtifactID, etc. Insira "com.fabrikam" para a groupID e "AzureApp" para a artifactID.</span><span class="sxs-lookup"><span data-stu-id="38f9a-148">When you come to the screen asking for groupID, ArtifactID, etc. Enter "com.fabrikam" for the groupID and enter "AzureApp" for the artifactID.</span></span>

<span data-ttu-id="38f9a-149">Agora abra o arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="38f9a-149">Now, open the pom.xml file.</span></span> <span data-ttu-id="38f9a-150">Dentro da marca `dependencies`, adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="38f9a-150">Inside the `dependencies` tag add the following code:</span></span>

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

<span data-ttu-id="38f9a-151">Agora salve o arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="38f9a-151">Now, save the pom.xml.</span></span> <span data-ttu-id="38f9a-152">Isso faz uma solicitação ao Eclipse para baixar as dependências especificadas.</span><span class="sxs-lookup"><span data-stu-id="38f9a-152">This prompts Eclipse to download all the specified dependencies.</span></span> <span data-ttu-id="38f9a-153">Isso pode demorar um pouco.</span><span class="sxs-lookup"><span data-stu-id="38f9a-153">This may take a moment.</span></span>
   
## <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="38f9a-154">Instalar o kit de ferramentas do Azure para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="38f9a-154">Install the azure toolkit for Eclipse</span></span>

<span data-ttu-id="38f9a-155">O [Kit de ferramentas do Azure](azure-toolkit-for-eclipse.md) é necessário caso você vá implantar aplicativos Web ou APIs de forma programática, mas não está sendo usado para outros tipos de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="38f9a-155">The [Azure toolkit](azure-toolkit-for-eclipse.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="38f9a-156">A seguir há um resumo dos processos de instalação.</span><span class="sxs-lookup"><span data-stu-id="38f9a-156">The following is a summary of the installation process.</span></span> <span data-ttu-id="38f9a-157">Para obter etapas detalhadas, visite [Instalação do Kit de ferramentas do Azure para o Eclipse](azure-toolkit-for-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="38f9a-157">For detailed stpes, visit [Installing the Azure Toolkit for Eclipse](azure-toolkit-for-eclipse.md).</span></span>

<span data-ttu-id="38f9a-158">Selecione o menu **Ajuda** e depois **Instalar novo software**.</span><span class="sxs-lookup"><span data-stu-id="38f9a-158">Select the **Help** menu and then select **Install New software**.</span></span>

<span data-ttu-id="38f9a-159">No campo **Trabalhar com:**, insira `http://dl.microsoft.com/eclipse` e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="38f9a-159">In the **Work with:** field enter `http://dl.microsoft.com/eclipse` and press enter.</span></span>

<span data-ttu-id="38f9a-160">Depois marque a caixa de seleção próxima a **Kit de ferramentas do Azure para Java** e desmarque a caixa de seleção para **Contatar todos os sites de atualização durante a instalação para encontrar o software requerido**.</span><span class="sxs-lookup"><span data-stu-id="38f9a-160">Then, select the checkbox next to **Azure toolkit for Java** and uncheck the checkbox for **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="38f9a-161">Depois selecione Avançar.</span><span class="sxs-lookup"><span data-stu-id="38f9a-161">Then select next.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="38f9a-162">Criar uma máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="38f9a-162">Create a Linux virtual machine</span></span>

<span data-ttu-id="38f9a-163">Crie um novo arquivo denominado `AzureApp.java` no diretório `src/main/java` do projeto e cole-o no seguinte bloco de código.</span><span class="sxs-lookup"><span data-stu-id="38f9a-163">Create a new file named `AzureApp.java` in the project's `src/main/java` directory and paste in the following block of code.</span></span> <span data-ttu-id="38f9a-164">Atualize as variáveis `userName` e `sshKey` com valores reais para a sua máquina.</span><span class="sxs-lookup"><span data-stu-id="38f9a-164">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="38f9a-165">O código cria uma nova VM do Linux com o nome `testLinuxVM` em um grupo de recursos `sampleResourceGroup` em execução na região Leste dos EUA do Azure.</span><span class="sxs-lookup"><span data-stu-id="38f9a-165">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

<span data-ttu-id="38f9a-166">Para criar um `sshkey`, abra o Azure Cloud Shell e insira `ssh-keygen -t rsa -b 2048`.</span><span class="sxs-lookup"><span data-stu-id="38f9a-166">In order to create an `sshkey`, open the azure cloud shell and enter `ssh-keygen -t rsa -b 2048`.</span></span> <span data-ttu-id="38f9a-167">Nomeie o arquivo, depois acesse o arquivo .public para obter a chave, a qual é usada no código a seguir, e copie e cole em toda a sua variável `sshKey`.</span><span class="sxs-lookup"><span data-stu-id="38f9a-167">Name the file and then access the .public file to get the key, which you use in the following code, copy and paste it all into your variable `sshKey`.</span></span>

```java
package com.fabrikam.AzureApp;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.PricingTier;
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
import java.util.List;

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


<span data-ttu-id="38f9a-168">Você verá algumas solicitações REST e respostas no console conforme o SDK faz as chamadas subjacentes para a API REST do Azure para configurar a máquina virtual e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="38f9a-168">You see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="38f9a-169">Quando o programa for concluído, verifique se a máquina virtual em sua assinatura com a CLI do Azure 2.0:</span><span class="sxs-lookup"><span data-stu-id="38f9a-169">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="38f9a-170">Depois de verificar se o código funcionou, use a CLI para excluir a VM e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="38f9a-170">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="38f9a-171">Implantar um aplicativo Web a partir de um repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="38f9a-171">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="38f9a-172">Substitua o método principal em `AzureApp.java` pelo mostrado abaixo, atualizando a variável `appName` com um valor exclusivo antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="38f9a-172">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="38f9a-173">Esse código implanta um aplicativo Web a partir da ramificação `master` em um repositório GitHub público em um novo [Aplicativo Web do Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) em execução no tipo de preços gratuito.</span><span class="sxs-lookup"><span data-stu-id="38f9a-173">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

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

<span data-ttu-id="38f9a-174">Execute o código como antes usando Maven:</span><span class="sxs-lookup"><span data-stu-id="38f9a-174">Run the code as before using Maven:</span></span>

<span data-ttu-id="38f9a-175">Abra um navegador apontado para o aplicativo usando a CLI:</span><span class="sxs-lookup"><span data-stu-id="38f9a-175">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
<span data-ttu-id="38f9a-176">Remova o aplicativo Web e o plano da sua assinatura depois de verificar a implantação.</span><span class="sxs-lookup"><span data-stu-id="38f9a-176">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="38f9a-177">Conectar-se a um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="38f9a-177">Connect to an Azure SQL database</span></span>

<span data-ttu-id="38f9a-178">Substitua o método principal atual em `AzureApp.java` pelo código abaixo, definindo um valor real para a variável `dbPassword`.</span><span class="sxs-lookup"><span data-stu-id="38f9a-178">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="38f9a-179">Esse código cria um novo banco de dados do SQL com uma regra de firewall permitindo o acesso remoto e, em seguida, se conecta a ele usando o driver JBDC do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="38f9a-179">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

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
<span data-ttu-id="38f9a-180">Execute o exemplo a partir da linha de comando:</span><span class="sxs-lookup"><span data-stu-id="38f9a-180">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="38f9a-181">Depois limpe os recursos usando a CLI:</span><span class="sxs-lookup"><span data-stu-id="38f9a-181">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="38f9a-182">Gravar um blob em uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="38f9a-182">Write a blob into a new storage account</span></span>

<span data-ttu-id="38f9a-183">Substitua o método principal atual em `AzureApp.java` pelo código abaixo.</span><span class="sxs-lookup"><span data-stu-id="38f9a-183">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="38f9a-184">Esse código cria uma [conta de armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-introduction) e, em seguida, usa as bibliotecas de Armazenamento do Azure para Java para criar um novo arquivo de texto na nuvem.</span><span class="sxs-lookup"><span data-stu-id="38f9a-184">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

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

            // create a storage container to hold the files
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

<span data-ttu-id="38f9a-185">Execute o exemplo a partir da linha de comando:</span><span class="sxs-lookup"><span data-stu-id="38f9a-185">Run the sample from the command line:</span></span>

<span data-ttu-id="38f9a-186">Você pode procurar o arquivo `helloazure.txt` em sua conta de armazenamento por meio do portal do Azure ou com o [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span><span class="sxs-lookup"><span data-stu-id="38f9a-186">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="38f9a-187">Limpar a conta de armazenamento usando a CLI:</span><span class="sxs-lookup"><span data-stu-id="38f9a-187">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="38f9a-188">Explorar mais exemplos</span><span class="sxs-lookup"><span data-stu-id="38f9a-188">Explore more samples</span></span>

<span data-ttu-id="38f9a-189">Para saber mais sobre como usar as bibliotecas de gerenciamento do Azure para Java para gerenciar recursos e automatizar tarefas, confira o nosso exemplo de código para [máquinas virtuais](../java-sdk-azure-virtual-machine-samples.md), [aplicativos Web](../java-sdk-azure-web-apps-samples.md) e [banco de dados SQL](../java-sdk-azure-sql-database-samples.md) .</span><span class="sxs-lookup"><span data-stu-id="38f9a-189">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](../java-sdk-azure-virtual-machine-samples.md), [web apps](../java-sdk-azure-web-apps-samples.md) and [SQL database](../java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="38f9a-190">Referência e notas de versão</span><span class="sxs-lookup"><span data-stu-id="38f9a-190">Reference and release notes</span></span>

<span data-ttu-id="38f9a-191">Uma [referência](http://docs.microsoft.com/java/api) está disponível para todos os pacotes.</span><span class="sxs-lookup"><span data-stu-id="38f9a-191">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="38f9a-192">Obter ajuda e fazer comentários</span><span class="sxs-lookup"><span data-stu-id="38f9a-192">Get help and give feedback</span></span>

<span data-ttu-id="38f9a-193">Poste perguntas para a comunidade no [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span><span class="sxs-lookup"><span data-stu-id="38f9a-193">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="38f9a-194">Relate bugs e problemas não resolvidos com as bibliotecas do Azure para Java no [projeto GitHub](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="38f9a-194">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
