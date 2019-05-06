---
title: Publicar um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse
description: Saiba como publicar um aplicativo Web para o Microsoft Azure como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4eb159bef52b384de32ada18937b0b9a47a93afc
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61590721"
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="2c775-103">Publicar um aplicativo Web como um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="2c775-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="2c775-104">Contêineres do Docker são um método amplamente usado para implantar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="2c775-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="2c775-105">Com os contêineres do Docker, os desenvolvedores podem consolidar todos os arquivos de projeto e dependências em um único pacote para implantação em um servidor.</span><span class="sxs-lookup"><span data-stu-id="2c775-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="2c775-106">O Kit de Ferramentas do Azure para Eclipse simplifica o processo para desenvolvedores de Java adicionando recursos de *Publicar como Contêiner do Docker* para implantação no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2c775-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="2c775-107">Este artigo explica as etapas necessárias para publicar seus aplicativos no Azure como contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="2c775-108">Saiba mais sobre o Docker no [site do Docker].</span><span class="sxs-lookup"><span data-stu-id="2c775-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="2c775-109">Publicar seu aplicativo Web no Azure usando um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="2c775-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="2c775-110">Abra seu projeto de aplicativo Web no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2c775-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="2c775-111">Para iniciar o assistente **Publicar como Contêiner do Docker**, execute um dos seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="2c775-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="2c775-112">Na exibição **Navegador**, clique com o botão direito do mouse em seu projeto, clique em **Azure** e clique em **Publicar como Contêiner do Docker**.</span><span class="sxs-lookup"><span data-stu-id="2c775-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Comando Publicar como Contêiner do Docker da exibição Navegador][PUB01]

   * <span data-ttu-id="2c775-114">Na barra de ferramentas do Eclipse, clique no botão **Publicar** e clique em **Publicar como Contêiner do Docker**.</span><span class="sxs-lookup"><span data-stu-id="2c775-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Comando Publicar como Contêiner do Docker da barra de ferramentas do Eclipse][PUB02]
      
   <span data-ttu-id="2c775-116">O assistente para **Implantar Contêiner do Docker no Azure** é aberto.</span><span class="sxs-lookup"><span data-stu-id="2c775-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![O assistente para Implantar o Contêiner do Docker no Azure][PUB03]

3. <span data-ttu-id="2c775-118">Na janela **Digite um nome de imagem, selecione o caminho do artefato e marque um host do Docker a ser usado**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2c775-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

   <span data-ttu-id="2c775-119"> a.</span><span class="sxs-lookup"><span data-stu-id="2c775-119">a.</span></span> <span data-ttu-id="2c775-120">Na caixa **Nome da imagem do Docker**, insira um nome exclusivo para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="2c775-121">(O assistente cria automaticamente um nome, mas você pode modificá-lo.)</span><span class="sxs-lookup"><span data-stu-id="2c775-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

   <span data-ttu-id="2c775-122">b.</span><span class="sxs-lookup"><span data-stu-id="2c775-122">b.</span></span> <span data-ttu-id="2c775-123">A área **Hosts** exibe quaisquer hosts do Docker que você já criou.</span><span class="sxs-lookup"><span data-stu-id="2c775-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="2c775-124">Faça uma das opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c775-124">Do either of the following:</span></span>

   * <span data-ttu-id="2c775-125">Se você tiver um host do Docker existente, poderá implantar seu aplicativo Web nele.</span><span class="sxs-lookup"><span data-stu-id="2c775-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
   * <span data-ttu-id="2c775-126">Para criar um novo host do Docker, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2c775-126">To create a new Docker host, click **Add**.</span></span>  
      
      <span data-ttu-id="2c775-127">A caixa de diálogo **Criar Host do Docker** é aberta.</span><span class="sxs-lookup"><span data-stu-id="2c775-127">The **Create Docker Host** dialog box opens.</span></span>

   ![Assistente para Implantar o Contêiner do Docker no Azure][PUB04a]

4. <span data-ttu-id="2c775-129">Na janela **Configurar a nova máquina virtual**, especifique as seguintes opções para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="2c775-130">(O assistente gera automaticamente a maioria das opções para você, mas você pode modificar qualquer uma delas.)</span><span class="sxs-lookup"><span data-stu-id="2c775-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="2c775-131"> a.</span><span class="sxs-lookup"><span data-stu-id="2c775-131">a.</span></span> <span data-ttu-id="2c775-132">**Nome**: inserir um nome exclusivo para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="2c775-133">(Não é o mesmo que o nome da imagem do Docker que você especificou anteriormente.)</span><span class="sxs-lookup"><span data-stu-id="2c775-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="2c775-134">b.</span><span class="sxs-lookup"><span data-stu-id="2c775-134">b.</span></span> <span data-ttu-id="2c775-135">**Assinatura**: inserir a assinatura do Azure que você usa para o host.</span><span class="sxs-lookup"><span data-stu-id="2c775-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="2c775-136">c.</span><span class="sxs-lookup"><span data-stu-id="2c775-136">c.</span></span> <span data-ttu-id="2c775-137">**Região**: inserir a região geográfica na qual o host está localizado.</span><span class="sxs-lookup"><span data-stu-id="2c775-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="2c775-138">d.</span><span class="sxs-lookup"><span data-stu-id="2c775-138">d.</span></span> <span data-ttu-id="2c775-139">Na guia **Sistema Operacional de Host e Tamanho**:</span><span class="sxs-lookup"><span data-stu-id="2c775-139">On the **Host OS and Size** tab:</span></span> 
   * <span data-ttu-id="2c775-140">**SO do host**: inserir o sistema operacional da máquina virtual que contém seu host.</span><span class="sxs-lookup"><span data-stu-id="2c775-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
   * <span data-ttu-id="2c775-141">**Tamanho**: inserir o tamanho da máquina virtual de seu host.</span><span class="sxs-lookup"><span data-stu-id="2c775-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="2c775-142">e.</span><span class="sxs-lookup"><span data-stu-id="2c775-142">e.</span></span> <span data-ttu-id="2c775-143">Na guia **Grupo de Recursos**:</span><span class="sxs-lookup"><span data-stu-id="2c775-143">On the **Resource Group** tab:</span></span> 
   * <span data-ttu-id="2c775-144">**Novo grupo de recursos**: Criar um novo grupo de recursos para seu host.</span><span class="sxs-lookup"><span data-stu-id="2c775-144">**New resource group**: Create a new resource group for your host.</span></span>
   * <span data-ttu-id="2c775-145">**Grupo de recursos existente**: inserir um grupo de recursos de sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c775-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="2c775-146">f.</span><span class="sxs-lookup"><span data-stu-id="2c775-146">f.</span></span> <span data-ttu-id="2c775-147">Na guia **Rede**:</span><span class="sxs-lookup"><span data-stu-id="2c775-147">On the **Network** tab:</span></span> 
   * <span data-ttu-id="2c775-148">**Nova rede virtual**: criar uma nova rede virtual para o host.</span><span class="sxs-lookup"><span data-stu-id="2c775-148">**New virtual network**: Create a new virtual network for your host.</span></span>
   * <span data-ttu-id="2c775-149">**Rede virtual existente:** inserir uma rede virtual existente de sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c775-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="2c775-150">g.</span><span class="sxs-lookup"><span data-stu-id="2c775-150">g.</span></span> <span data-ttu-id="2c775-151">Sobre na guia **Armazenamento**:</span><span class="sxs-lookup"><span data-stu-id="2c775-151">On the **Storage** tab:</span></span> 
   * <span data-ttu-id="2c775-152">**Nova conta de armazenamento**: Criar uma nova conta de armazenamento para seu host.</span><span class="sxs-lookup"><span data-stu-id="2c775-152">**New storage account**: Create a new storage account for your host.</span></span>
   * <span data-ttu-id="2c775-153">**Conta de armazenamento existente**: inserir uma conta de armazenamento existente da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c775-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="2c775-154">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="2c775-154">Click **Next**.</span></span>

6. <span data-ttu-id="2c775-155">Na janela **Configurar credenciais de logon e configurações de porta**, selecione uma das opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c775-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

   * <span data-ttu-id="2c775-156">**Importar credenciais do Azure Key Vault**: especifica um conjunto de credenciais salvo anteriormente que está armazenado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c775-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span> 

   >[!NOTE]
   ><span data-ttu-id="2c775-157">Um Azure Key Vault que é criado com uma conta ou entidade de serviço específica não poderá ser acessado automaticamente por outra conta ou entidade de serviço que compartilhe a assinatura.</span><span class="sxs-lookup"><span data-stu-id="2c775-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="2c775-158">Para permitir que outra conta ou entidade de serviço use o Key Vault, você deve usar o Portal do Azure para adicionar a conta ou a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="2c775-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>
   >

   * <span data-ttu-id="2c775-159">**Novas credenciais de logon**: cria um novo conjunto de credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="2c775-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="2c775-160">Se você selecionar essa opção, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2c775-160">If you select this option, do the following:</span></span> 
    
     * <span data-ttu-id="2c775-161">Na guia **Credenciais de VM**, escolha uma das opções a seguir para as credenciais de logon de máquina virtual do host do Docker:</span><span class="sxs-lookup"><span data-stu-id="2c775-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span> 

       * <span data-ttu-id="2c775-162">**Nome de usuário**: inserir o nome de usuário de suas credenciais de logon de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2c775-162">**Username**: Enter the username for your virtual machine login credentials.</span></span> 
       * <span data-ttu-id="2c775-163">**Senha** e **Confirmar**: inserir a senha de suas credenciais de logon de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2c775-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span> 
       * <span data-ttu-id="2c775-164">**SSH**: inserir as configurações de SSH (Secure Shell) para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="2c775-165">É possível escolher um das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="2c775-165">You can choose from the following options:</span></span> 
          * <span data-ttu-id="2c775-166">**Nenhum**: especifica que a sua máquina virtual não permitirá conexões SSH.</span><span class="sxs-lookup"><span data-stu-id="2c775-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span> 
          * <span data-ttu-id="2c775-167">**Gerar automaticamente**: cria automaticamente as configurações necessárias para conectar-se via SSH.</span><span class="sxs-lookup"><span data-stu-id="2c775-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span> 
          * <span data-ttu-id="2c775-168">**Importar do diretório**: especifica um diretório que contém um conjunto de configurações de SSH salvas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2c775-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="2c775-169">O diretório deve conter os dois arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c775-169">The directory must contain the following two files:</span></span> 
             * <span data-ttu-id="2c775-170">*id_rsa*: contém a identificação da RSA de um usuário.</span><span class="sxs-lookup"><span data-stu-id="2c775-170">*id_rsa*: Contains the RSA identification for a user.</span></span> 
             * <span data-ttu-id="2c775-171">*id_rsa.pub*: contém a chave pública RSA que é usada na autenticação.</span><span class="sxs-lookup"><span data-stu-id="2c775-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span> 
        
         ![Criar host do Docker][PUB05]

     * <span data-ttu-id="2c775-173">Na guia **Credenciais de Daemon do Docker**, especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="2c775-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span> 

       * <span data-ttu-id="2c775-174">**Porta de Daemon do Docker**: inserir a porta TCP exclusiva para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span> 
       * <span data-ttu-id="2c775-175">**Segurança TLS**: inserir as configurações de protocolo TLS para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="2c775-176">É possível escolher um das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="2c775-176">You can choose from the following options:</span></span> 
          * <span data-ttu-id="2c775-177">**Nenhum**: especifica que sua máquina virtual não permitirá conexões TLS.</span><span class="sxs-lookup"><span data-stu-id="2c775-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span> 
          * <span data-ttu-id="2c775-178">**Gerar automaticamente**: cria automaticamente as configurações necessárias para conectar-se via TLS.</span><span class="sxs-lookup"><span data-stu-id="2c775-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span> 
          * <span data-ttu-id="2c775-179">**Importar do diretório**: especifica um diretório que contém um conjunto de configurações de TLS salvas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2c775-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="2c775-180">Mais especificamente, o diretório deve conter os seis arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c775-180">More specifically, the directory must contain the following six files:</span></span> 
             * <span data-ttu-id="2c775-181">*ca.pem* e *ca-key.pem*: contêm o certificado e a chave pública da Autoridade de Certificação TLS.</span><span class="sxs-lookup"><span data-stu-id="2c775-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span> 
             * <span data-ttu-id="2c775-182">*cert.pem* e *key.pem*: contêm o certificado do cliente e a chave pública que é usada na autenticação TLS.</span><span class="sxs-lookup"><span data-stu-id="2c775-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span> 
             * <span data-ttu-id="2c775-183">*server.pem* e *server-key.pem*: contêm o certificado do servidor e a chave pública do host.</span><span class="sxs-lookup"><span data-stu-id="2c775-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span> 

         ![Criar host do Docker][PUB06]

7. <span data-ttu-id="2c775-185">Depois de inserir todas as informações anteriores, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="2c775-185">After you have entered all of the preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="2c775-186">No assistente **Implantar Contêiner do Docker no Azure**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="2c775-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![O assistente para Implantar o Contêiner do Docker no Azure][PUB07]

9. <span data-ttu-id="2c775-188">Na janela **Configurar o contêiner do Docker a ser criado**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2c775-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="2c775-189"> a.</span><span class="sxs-lookup"><span data-stu-id="2c775-189">a.</span></span> <span data-ttu-id="2c775-190">Na caixa **Nome do contêiner do Docker**, insira um nome exclusivo do contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="2c775-191">b.</span><span class="sxs-lookup"><span data-stu-id="2c775-191">b.</span></span> <span data-ttu-id="2c775-192">Escolha uma das seguintes imagens do Docker:</span><span class="sxs-lookup"><span data-stu-id="2c775-192">Choose one of the following Docker images:</span></span> 

   * <span data-ttu-id="2c775-193">**Imagem do Docker predefinida**: especifica uma imagem do Docker já existente no Azure.</span><span class="sxs-lookup"><span data-stu-id="2c775-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span> 

     >[!NOTE]
     ><span data-ttu-id="2c775-194">A lista de imagens do Docker nessa caixa é composta por várias imagens às quais o Kit de Ferramentas do Azure foi configurado para aplicar patches, de modo que o artefato seja implantado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2c775-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>
     >

   * <span data-ttu-id="2c775-195">**Dockerfile personalizado**: especifica um Dockerfile salvo anteriormente do computador local.</span><span class="sxs-lookup"><span data-stu-id="2c775-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

     >[!NOTE]
     ><span data-ttu-id="2c775-196">Essa é uma funcionalidade mais avançada para desenvolvedores que desejam implantar um Dockerfile próprio.</span><span class="sxs-lookup"><span data-stu-id="2c775-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="2c775-197">No entanto, cabe aos desenvolvedores que usam essa opção garantir que o Dockerfile seja compilado corretamente.</span><span class="sxs-lookup"><span data-stu-id="2c775-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="2c775-198">O Kit de ferramentas do Azure não valida o conteúdo em um Dockerfile personalizado, portanto, a implantação poderá falhar se o Dockerfile tiver problemas.</span><span class="sxs-lookup"><span data-stu-id="2c775-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="2c775-199">Além disso, o Kit de Ferramentas do Azure espera que o Dockerfile personalizado contenha um artefato de aplicativo Web e ele tentará abrir uma conexão HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c775-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="2c775-200">Se os desenvolvedores publicarem um tipo diferente de artefato, eles poderão receber erros inócuos após a implantação.</span><span class="sxs-lookup"><span data-stu-id="2c775-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>
     >

   <span data-ttu-id="2c775-201">c.</span><span class="sxs-lookup"><span data-stu-id="2c775-201">c.</span></span> <span data-ttu-id="2c775-202">**Configurações de porta**: inserir a associação de porta TCP exclusiva do contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

      ![A janela Configurar o contêiner do Docker a ser criado][PUB08]

10. <span data-ttu-id="2c775-204">Depois de concluir todas as etapas anteriores, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="2c775-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="2c775-205">O Kit de ferramentas do Azure começa a implantar seu aplicativo Web no Azure em um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="2c775-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2c775-206">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c775-206">Next steps</span></span>

<span data-ttu-id="2c775-207">Para obter recursos adicionais para o Docker, consulte o [site do Docker] oficial.</span><span class="sxs-lookup"><span data-stu-id="2c775-207">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Site do Docker]: https://www.docker.com/
[Docker website]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png