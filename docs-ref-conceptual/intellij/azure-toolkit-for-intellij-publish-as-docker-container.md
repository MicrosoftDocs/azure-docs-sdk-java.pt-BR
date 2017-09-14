---
title: "Publicar um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ"
description: "Saiba como publicar um aplicativo Web para o Microsoft Azure como um contêiner do Docker usando o Kit de ferramentas do Azure para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 2d94dfa4467bc79d6155321a9966358b79e9e960
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="0c16a-103">Publicar um aplicativo Web como um contêiner do Docker usando o Kit de ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0c16a-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="0c16a-104">Contêineres do Docker são um método amplamente usado para implantar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="0c16a-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="0c16a-105">Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor.</span><span class="sxs-lookup"><span data-stu-id="0c16a-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="0c16a-106">O Kit de Ferramentas do Azure para IntelliJ simplifica o processo para desenvolvedores de Java adicionando recursos de *Publicar como Contêiner do Docker* para implantação no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0c16a-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="0c16a-107">Este artigo explica as etapas necessárias para publicar seus aplicativos no Azure como contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="0c16a-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0c16a-108">Saiba mais sobre o Docker no [site do Docker].</span><span class="sxs-lookup"><span data-stu-id="0c16a-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="0c16a-109">Publicar seu aplicativo Web no Azure usando um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="0c16a-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="0c16a-110">Para publicar seu aplicativo Web, é necessário criar um artefato pronto para implantação.</span><span class="sxs-lookup"><span data-stu-id="0c16a-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="0c16a-111">Para saber mais, confira a seção [Informações adicionais sobre a criação de artefatos](#artifacts).</span><span class="sxs-lookup"><span data-stu-id="0c16a-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="0c16a-112">Depois de concluir o assistente de implantação pelo menos uma vez, a maioria de suas configurações é usada como padrão na próxima execução do assistente.</span><span class="sxs-lookup"><span data-stu-id="0c16a-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="0c16a-113">Abra seu projeto de aplicativo Web no IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0c16a-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="0c16a-114">Para iniciar o assistente **Publicar como Contêiner do Docker**, execute um dos seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="0c16a-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="0c16a-115">Na janela de ferramentas **Projeto**, clique com o botão direito em seu projeto, clique em **Azure** e clique em **Publicar como Contêiner do Docker**:</span><span class="sxs-lookup"><span data-stu-id="0c16a-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![O comando Publicar como Contêiner do Docker][PUB01]

   * <span data-ttu-id="0c16a-117">Na barra de ferramentas do IntelliJ, clique no botão **Publicar Grupo** e clique em **Publicar como Contêiner do Docker**:</span><span class="sxs-lookup"><span data-stu-id="0c16a-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="0c16a-118">![O comando Publicar como Contêiner do Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="0c16a-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="0c16a-119">O assistente para **Implantar Contêiner do Docker no Azure** é aberto.</span><span class="sxs-lookup"><span data-stu-id="0c16a-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![O assistente para Implantar o Contêiner do Docker no Azure][PUB03]

3. <span data-ttu-id="0c16a-121">Na janela **Digite um nome de imagem, selecione o caminho do artefato e marque um host do Docker a ser usado**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0c16a-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="0c16a-122">a.</span><span class="sxs-lookup"><span data-stu-id="0c16a-122">a.</span></span> <span data-ttu-id="0c16a-123">Na caixa **Nome da imagem do Docker**, insira um nome exclusivo para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="0c16a-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="0c16a-124">(O assistente cria automaticamente um nome, mas você pode modificá-lo.)</span><span class="sxs-lookup"><span data-stu-id="0c16a-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="0c16a-125">b.</span><span class="sxs-lookup"><span data-stu-id="0c16a-125">b.</span></span> <span data-ttu-id="0c16a-126">A área **Hosts** exibe quaisquer hosts do Docker que você já criou.</span><span class="sxs-lookup"><span data-stu-id="0c16a-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="0c16a-127">Faça uma das opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c16a-127">Do either of the following:</span></span> 
      * <span data-ttu-id="0c16a-128">Se você tiver um host do Docker existente, poderá implantar seu aplicativo Web nele.</span><span class="sxs-lookup"><span data-stu-id="0c16a-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="0c16a-129">Para criar um host do Docker, clique no sinal de adição verde (**+**).</span><span class="sxs-lookup"><span data-stu-id="0c16a-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="0c16a-130">A caixa de diálogo **Criar Host do Docker** é aberta.</span><span class="sxs-lookup"><span data-stu-id="0c16a-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Assistente para Implantar o Contêiner do Docker no Azure][PUB04a]

4. <span data-ttu-id="0c16a-132">Na janela **Configurar a nova máquina virtual**, forneça as seguintes informações sobre o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="0c16a-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="0c16a-133">(O assistente gera automaticamente a maioria das informações para você, mas você pode modificar qualquer uma delas.)</span><span class="sxs-lookup"><span data-stu-id="0c16a-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="0c16a-134">a.</span><span class="sxs-lookup"><span data-stu-id="0c16a-134">a.</span></span> <span data-ttu-id="0c16a-135">Na caixa **Nome**, insira um nome exclusivo para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="0c16a-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="0c16a-136">(Não é o mesmo que o nome da imagem do Docker que você especificou anteriormente.)</span><span class="sxs-lookup"><span data-stu-id="0c16a-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="0c16a-137">b.</span><span class="sxs-lookup"><span data-stu-id="0c16a-137">b.</span></span> <span data-ttu-id="0c16a-138">Na caixa **Assinatura**, insira a assinatura do Azure que você usa para o host.</span><span class="sxs-lookup"><span data-stu-id="0c16a-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="0c16a-139">c.</span><span class="sxs-lookup"><span data-stu-id="0c16a-139">c.</span></span> <span data-ttu-id="0c16a-140">Na caixa **Região**, insira a região geográfica na qual o host está localizado.</span><span class="sxs-lookup"><span data-stu-id="0c16a-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="0c16a-141">d.</span><span class="sxs-lookup"><span data-stu-id="0c16a-141">d.</span></span> <span data-ttu-id="0c16a-142">Na guia **Sistema Operacional e Tamanho**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0c16a-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="0c16a-143">**Sistema Operacional de Host**: insira o sistema operacional da máquina virtual que contém seu host.</span><span class="sxs-lookup"><span data-stu-id="0c16a-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="0c16a-144">**Tamanho**: insira o tamanho da máquina virtual de seu host.</span><span class="sxs-lookup"><span data-stu-id="0c16a-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="0c16a-145">e.</span><span class="sxs-lookup"><span data-stu-id="0c16a-145">e.</span></span> <span data-ttu-id="0c16a-146">Na guia **Grupo de Recursos**, selecione uma das opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c16a-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="0c16a-147">**Novo grupo de recursos**: crie um grupo de recursos para o host.</span><span class="sxs-lookup"><span data-stu-id="0c16a-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="0c16a-148">**Grupo de recursos existente**: especifique um grupo de recursos existente de sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c16a-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="0c16a-149">f.</span><span class="sxs-lookup"><span data-stu-id="0c16a-149">f.</span></span> <span data-ttu-id="0c16a-150">Na guia **Rede**, selecione uma das opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c16a-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="0c16a-151">**Nova rede virtual**: crie uma rede virtual para o host.</span><span class="sxs-lookup"><span data-stu-id="0c16a-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="0c16a-152">**Rede virtual existente**: especifique uma rede virtual existente de sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c16a-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="0c16a-153">g.</span><span class="sxs-lookup"><span data-stu-id="0c16a-153">g.</span></span> <span data-ttu-id="0c16a-154">Na guia **Armazenamento**, selecione uma das opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c16a-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="0c16a-155">**Nova conta de armazenamento**: crie uma conta de armazenamento para o host.</span><span class="sxs-lookup"><span data-stu-id="0c16a-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="0c16a-156">**Conta de armazenamento existente**: especifique uma conta de armazenamento existente da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c16a-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="0c16a-157">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0c16a-157">Click **Next**.</span></span>  
     <span data-ttu-id="0c16a-158">A janela **Configurar credenciais de logon e configurações de porta** é aberta.</span><span class="sxs-lookup"><span data-stu-id="0c16a-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![A janela Configurar credenciais de logon e configurações de porta][PUB05]

6. <span data-ttu-id="0c16a-160">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="0c16a-160">Select one of the following options:</span></span>

      * <span data-ttu-id="0c16a-161">**Importar credenciais do Azure Key Vault**: especifique um conjunto de credenciais que são armazenadas em sua assinatura do Azure salva anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0c16a-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="0c16a-162">Um Azure Key Vault que é criado com uma conta ou entidade de serviço específica não poderá ser acessado automaticamente por outra conta ou entidade de serviço que compartilhe a assinatura.</span><span class="sxs-lookup"><span data-stu-id="0c16a-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="0c16a-163">Para permitir que outra conta ou entidade de serviço use o Key Vault, você deve usar o Portal do Azure para adicionar a conta ou a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0c16a-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="0c16a-164">**Novas credenciais de logon**: crie um novo conjunto de credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="0c16a-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="0c16a-165">Se você selecionar essa opção, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0c16a-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="0c16a-166">a.</span><span class="sxs-lookup"><span data-stu-id="0c16a-166">a.</span></span> <span data-ttu-id="0c16a-167">Na guia **Credenciais de VM** forneça as seguintes informações para as credenciais de logon da máquina virtual de seu host do Docker: * **Nome de usuário**: insira o nome de usuário para as credenciais de logon da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0c16a-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: * **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="0c16a-168">* **Senha** e **Confirmar**: especifica a senha para as credenciais de logon da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0c16a-168">* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="0c16a-169">* **SSH**: insira as configurações de SSH (Secure Shell) para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="0c16a-169">* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="0c16a-170">Você pode selecionar uma das seguintes opções: * **Nenhum** : especifica que a sua máquina virtual não permite conexões SSH.</span><span class="sxs-lookup"><span data-stu-id="0c16a-170">You can select one of the following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="0c16a-171">* **Gerar automaticamente**: cria automaticamente as configurações necessárias para conectar-se via SSH.</span><span class="sxs-lookup"><span data-stu-id="0c16a-171">* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="0c16a-172">* **Importar do diretório**: permite que você especifique um diretório que contém um conjunto de configurações de SSH salvas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0c16a-172">* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="0c16a-173">O diretório deve conter os dois arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c16a-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="0c16a-174">b.</span><span class="sxs-lookup"><span data-stu-id="0c16a-174">b.</span></span> <span data-ttu-id="0c16a-175">Na guia **Acesso ao Daemon do Docker** forneça as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="0c16a-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

          ![Criar host do Docker][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="0c16a-177">Depois de inserir as informações necessárias, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="0c16a-177">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="0c16a-178">O assistente para **Implantar Contêiner do Docker no Azure** é aberto novamente.</span><span class="sxs-lookup"><span data-stu-id="0c16a-178">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Assistente para Implantar o Contêiner do Docker no Azure][PUB07]

8. <span data-ttu-id="0c16a-180">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0c16a-180">Click **Next**.</span></span>  
    <span data-ttu-id="0c16a-181">A janela **Configurar o contêiner do Docker a ser criado** é aberta.</span><span class="sxs-lookup"><span data-stu-id="0c16a-181">The **Configure the Docker container to be created** window opens.</span></span>

   ![A janela Configurar o contêiner do Docker a ser criado][PUB08]

9. <span data-ttu-id="0c16a-183">Na janela **Configurar o contêiner do Docker a ser criado**, forneça as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="0c16a-183">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="0c16a-184">a.</span><span class="sxs-lookup"><span data-stu-id="0c16a-184">a.</span></span> <span data-ttu-id="0c16a-185">Na caixa **Nome do contêiner do Docker**, insira um nome exclusivo do contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="0c16a-185">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="0c16a-186">b.</span><span class="sxs-lookup"><span data-stu-id="0c16a-186">b.</span></span> <span data-ttu-id="0c16a-187">Escolha uma das seguintes imagens do Docker:</span><span class="sxs-lookup"><span data-stu-id="0c16a-187">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="0c16a-188">**Imagem do Docker predefinida**: especifique uma imagem já existente do Docker do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c16a-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="0c16a-189">A lista de imagens do Docker nessa caixa é composta por várias imagens às quais o Kit de Ferramentas do Azure foi configurado para aplicar patches, de modo que o artefato seja implantado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0c16a-189">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="0c16a-190">**Dockerfile personalizado**: especifique um Dockerfile salvo anteriormente do computador local.</span><span class="sxs-lookup"><span data-stu-id="0c16a-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="0c16a-191">Essa é uma funcionalidade mais avançada para desenvolvedores que desejam implantar um Dockerfile próprio.</span><span class="sxs-lookup"><span data-stu-id="0c16a-191">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="0c16a-192">No entanto, cabe aos desenvolvedores que usam essa opção garantir que o Dockerfile seja compilado corretamente.</span><span class="sxs-lookup"><span data-stu-id="0c16a-192">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="0c16a-193">Como o Kit de Ferramentas do Azure não valida o conteúdo em um Dockerfile personalizado, a implantação pode falhar se o Dockerfile tiver problemas.</span><span class="sxs-lookup"><span data-stu-id="0c16a-193">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="0c16a-194">Além disso, como o Kit de Ferramentas do Azure espera que o Dockerfile personalizado contenha um artefato de aplicativo Web, ele tenta abrir uma conexão HTTP.</span><span class="sxs-lookup"><span data-stu-id="0c16a-194">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="0c16a-195">Se os desenvolvedores publicarem um tipo diferente de artefato, eles poderão receber erros inócuos após a implantação.</span><span class="sxs-lookup"><span data-stu-id="0c16a-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="0c16a-196">c.</span><span class="sxs-lookup"><span data-stu-id="0c16a-196">c.</span></span> <span data-ttu-id="0c16a-197">Na caixa **Configurações de porta**, insira a associação de porta TCP exclusiva para seu contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="0c16a-197">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="0c16a-198">Depois de concluir as etapas anteriores, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="0c16a-198">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="0c16a-199">O Kit de ferramentas do Azure começa a implantar seu aplicativo Web no Azure em um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="0c16a-199">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="0c16a-200">A menos que você tenha configurado o IntelliJ para ser implantado em segundo plano, uma barra de progresso **Implantação no Azure** é exibida.</span><span class="sxs-lookup"><span data-stu-id="0c16a-200">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![A barra de progresso da implantação][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="0c16a-202">Informações adicionais sobre a criação de artefatos</span><span class="sxs-lookup"><span data-stu-id="0c16a-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="0c16a-203">Para criar um artefato pronto para implantação, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0c16a-203">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="0c16a-204">Abra seu projeto de aplicativo Web no IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0c16a-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="0c16a-205">Clique em **Arquivo** e depois em **Estrutura do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="0c16a-205">Click **File**, and then click **Project Structure**.</span></span>

   ![O comando Estrutura do Projeto][ART01]

3. <span data-ttu-id="0c16a-207">Para adicionar um artefato, clique no sinal de adição verde (**+**) e clique em **Aplicativo Web: Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="0c16a-207">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![O comando "Aplicativo Web: Arquivo"][ART02]

4. <span data-ttu-id="0c16a-209">Na caixa **Nome**, insira um nome para o artefato (não inclui a extensão *.war*) e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c16a-209">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![A caixa Nome do artefato][ART03]

<span data-ttu-id="0c16a-211">Para saber mais sobre como criar artefatos no IntelliJ, consulte [Configurar artefatos] no site da JetBrains.</span><span class="sxs-lookup"><span data-stu-id="0c16a-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c16a-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c16a-212">Next steps</span></span>

<span data-ttu-id="0c16a-213">Para obter recursos adicionais para o Docker, consulte o [site do Docker] oficial.</span><span class="sxs-lookup"><span data-stu-id="0c16a-213">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Site do Docker]: https://www.docker.com/
[Configurar artefatos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
