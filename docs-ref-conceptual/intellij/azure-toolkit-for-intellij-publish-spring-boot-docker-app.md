---
title: "Publicar um aplicativo Spring Boot como um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ"
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
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 65fbdc32824c2b6312929f4888844d1673101ac8
ms.sourcegitcommit: 062e07cbd42cda74f02c82b933ce90da646a50a0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="56199-103">Publicar um aplicativo Spring Boot como um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="56199-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="56199-104">O [Spring Framework] é uma solução de software livre que ajuda os desenvolvedores do Java a criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="56199-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="56199-105">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="56199-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="56199-106">O [Docker] é uma solução de software livre que ajuda os desenvolvedores a automatizar a implantação, o dimensionamento e o gerenciamento de seus aplicativos executados em contêineres.</span><span class="sxs-lookup"><span data-stu-id="56199-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="56199-107">Este tutorial explica as etapas para implantação de um aplicativo Spring Boot como um contêiner do Docker no Microsoft Azure usando o Kit de Ferramentas do Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="56199-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="56199-108">Clonar o repositório padrão do Spring Boot Docker</span><span class="sxs-lookup"><span data-stu-id="56199-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="56199-109">As etapas a seguir explicam a clonagem do repositório do Spring Boot Docker usando o IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="56199-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="56199-110">Se desejar usar uma linha de comando, consulte [Implantar um aplicativo Spring Boot no Linux no Serviço de Contêiner do Azure][Deploy Spring Boot on Linux in AKS].</span><span class="sxs-lookup"><span data-stu-id="56199-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="56199-111">Abra o IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="56199-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="56199-112">Na tela de boas-vindas, selecione a opção **GitHub** na lista **Fazer Check-out do Controle de Versão**.</span><span class="sxs-lookup"><span data-stu-id="56199-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![Opção do GitHub para controle de versão][CL01]

1. <span data-ttu-id="56199-114">Se você for solicitado a fazer logon, insira suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="56199-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="56199-115">Se você estiver usando um nome de usuário e uma senha para fazer logon no GitHub:</span><span class="sxs-lookup"><span data-stu-id="56199-115">If you are using a username/password to log in to GitHub:</span></span> 

      ![Caixa de diálogo para inserir o nome de usuário e a senha do GitHub][CL02a]

   * <span data-ttu-id="56199-117">Se você estiver usando um token para fazer logon no GitHub:</span><span class="sxs-lookup"><span data-stu-id="56199-117">If you are using a token to log in to GitHub:</span></span> 

      ![Caixa de diálogo para inserção de um token do GitHub][CL02b]

1. <span data-ttu-id="56199-119">Insira **https://github.com/spring-guides/gs-spring-boot-docker.git** como a URL do repositório, especifique o caminho local e as informações de pasta e, em seguida, clique em **Clonar**.</span><span class="sxs-lookup"><span data-stu-id="56199-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Caixa de diálogo Clonar Repositório][CL03]

1. <span data-ttu-id="56199-121">Quando solicitado a criar um projeto do IntelliJ, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="56199-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![Recusar-se a criar um projeto do IntelliJ][CL04]

1. <span data-ttu-id="56199-123">Na página inicial, clique em **Importar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="56199-123">On the welcome page, click **Import Project**.</span></span>

   ![Seleção Importar Projeto][CL05]

1. <span data-ttu-id="56199-125">Localize o caminho em que você clonou o repositório do Spring Boot, selecione a pasta **complete** na raiz e, depois, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56199-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![Selecionar uma pasta para importação][CL06]

1. <span data-ttu-id="56199-127">Quando solicitado, selecione **Criar projeto com base nas fontes existentes**.</span><span class="sxs-lookup"><span data-stu-id="56199-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Opção para criar um projeto com base nas fontes existentes][CL07]

1. <span data-ttu-id="56199-129">Especifique o nome do projeto ou aceite o padrão, confirme o caminho correto para a pasta **complete** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56199-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![Especifique o nome do projeto][CL08]

1. <span data-ttu-id="56199-131">Personalize quaisquer diretórios para importação e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="56199-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Escolher diretórios][CL09]

1. <span data-ttu-id="56199-133">Examine as bibliotecas para importar e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="56199-133">Review the libraries to import, and then click **Next**.</span></span>

   ![Examine as bibliotecas do projeto][CL10]

1. <span data-ttu-id="56199-135">Examine a estrutura do módulo e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="56199-135">Review the module structure, and then click **Next**.</span></span>

   ![Examinar a estrutura do módulo][CL11]

1. <span data-ttu-id="56199-137">Especifique o seu JDK e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="56199-137">Specify your JDK, and then click **Next**.</span></span>

   ![Especificar um JDK][CL12]

1. <span data-ttu-id="56199-139">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="56199-139">Click **Finish**.</span></span>

   ![Botão Concluir][CL13]

<span data-ttu-id="56199-141">O IntelliJ importa o aplicativo Spring Boot como um projeto e exibe a estrutura após a conclusão da importação.</span><span class="sxs-lookup"><span data-stu-id="56199-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![Aplicativo Spring Boot no IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="56199-143">Criar seu aplicativo Spring Boot</span><span class="sxs-lookup"><span data-stu-id="56199-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="56199-144">Criar o aplicativo usando o POM do Maven</span><span class="sxs-lookup"><span data-stu-id="56199-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="56199-145">Abra a janela de ferramentas do Maven, caso ela ainda não esteja aberta.</span><span class="sxs-lookup"><span data-stu-id="56199-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="56199-146">Clique em **Exibir** > **Janelas de Ferramentas** > **Projetos do Maven**.</span><span class="sxs-lookup"><span data-stu-id="56199-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Comandos da Janela de Ferramentas e Projetos do Maven][BU01]

1. <span data-ttu-id="56199-148">Na janela de ferramentas do Maven, clique com o botão direito do mouse em **Pacote** e selecione **Executar Build do Maven**.</span><span class="sxs-lookup"><span data-stu-id="56199-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="56199-149">(Se o projeto do Maven não for mostrado automaticamente, clique no ícone **Reimportar** na barra de ferramentas do Maven.)</span><span class="sxs-lookup"><span data-stu-id="56199-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Executar o comando de Build do Maven][BU02]

1. <span data-ttu-id="56199-151">O IntelliJ deverá exibir uma mensagem **ÊXITO NO BUILD** quando o aplicativo Spring Boot for criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="56199-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Mensagem ÊXITO NO BUILD][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="56199-153">Criar um artefato pronto para implantação</span><span class="sxs-lookup"><span data-stu-id="56199-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="56199-154">Para publicar o aplicativo Spring Boot, você precisa criar um artefato pronto para implantação.</span><span class="sxs-lookup"><span data-stu-id="56199-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="56199-155">Use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="56199-155">Use the following steps:</span></span>

1. <span data-ttu-id="56199-156">Abra seu projeto de aplicativo Web no IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="56199-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="56199-157">Clique em **Arquivo** e depois em **Estrutura do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="56199-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Comando Estrutura do Projeto][ART01]

1. <span data-ttu-id="56199-159">Clique no símbolo de sinal de adição verde (**+**) para adicionar um artefato, clique em **JAR** e, em seguida, em **Vazio**.</span><span class="sxs-lookup"><span data-stu-id="56199-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Adicionar um artefato][ART02]

1. <span data-ttu-id="56199-161">Nomeie seu artefato sem adicionar a extensão ".jar" e, em seguida, especifique a pasta de destino para a saída do Maven.</span><span class="sxs-lookup"><span data-stu-id="56199-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![Especificar as propriedades do artefato][ART03]

1. <span data-ttu-id="56199-163">Crie um manifesto para o artefato (opcional):</span><span class="sxs-lookup"><span data-stu-id="56199-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="56199-164">a.</span><span class="sxs-lookup"><span data-stu-id="56199-164">a.</span></span> <span data-ttu-id="56199-165">Clique em **Criar Manifesto**.</span><span class="sxs-lookup"><span data-stu-id="56199-165">Click **Create Manifest**.</span></span>

      ![Clicar no botão Criar Manifesto][ART04a]

   <span data-ttu-id="56199-167">b.</span><span class="sxs-lookup"><span data-stu-id="56199-167">b.</span></span> <span data-ttu-id="56199-168">Escolha o caminho padrão para o artefato e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56199-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![Especificar o caminho do artefato][ART04b]

   <span data-ttu-id="56199-170">c.</span><span class="sxs-lookup"><span data-stu-id="56199-170">c.</span></span> <span data-ttu-id="56199-171">Clique nas reticências (**…**) para localizar a classe principal.</span><span class="sxs-lookup"><span data-stu-id="56199-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![Localizar a classe principal][ART04c]

   <span data-ttu-id="56199-173">d.</span><span class="sxs-lookup"><span data-stu-id="56199-173">d.</span></span> <span data-ttu-id="56199-174">Escolha sua classe principal e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56199-174">Choose your main class, and then click **OK**.</span></span>

      ![Especificar a classe principal][ART04d]

1. <span data-ttu-id="56199-176">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56199-176">Click **OK**.</span></span>

   ![Fechar a caixa de diálogo Estrutura do Projeto][ART05]

> [!NOTE]
> <span data-ttu-id="56199-178">Para obter mais informações sobre como criar artefatos no IntelliJ, consulte [Configurar Artefatos] no site da JetBrains.</span><span class="sxs-lookup"><span data-stu-id="56199-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="56199-179">Faça o build do artefato para implantação</span><span class="sxs-lookup"><span data-stu-id="56199-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="56199-180">Clique em **Criar** e, em seguida, clique em **Artefatos**.</span><span class="sxs-lookup"><span data-stu-id="56199-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Comando Criar Artefatos][BU04]

1. <span data-ttu-id="56199-182">Quando o menu de contexto **Criar Artefato** for exibido, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="56199-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Menu de contexto Criar Artefato][BU05]

<span data-ttu-id="56199-184">O IntelliJ deverá exibir o artefato concluído para o aplicativo Spring Boot na janela de ferramentas do projeto.</span><span class="sxs-lookup"><span data-stu-id="56199-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![Artefato criado][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="56199-186">Publicar seu aplicativo Web no Azure usando um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="56199-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="56199-187">Se você não entrou em sua conta do Azure, siga as etapas em [Instruções de conexão para o Kit de Ferramentas do Azure para IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="56199-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="56199-188">Na janela de ferramentas do Explorador de Projeto, clique com o botão direito do mouse no projeto e, em seguida, selecione **Azure** > **Publicar como Contêiner Docker**.</span><span class="sxs-lookup"><span data-stu-id="56199-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Comando Publicar como Contêiner do Docker][PU01]

1. <span data-ttu-id="56199-190">Quando a caixa de diálogo **Implantar Contêiner do Docker no Azure** for exibida, todos os hosts existentes do Docker serão exibidos.</span><span class="sxs-lookup"><span data-stu-id="56199-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="56199-191">Se você optar por implantar em um host existente, poderá pular para a etapa 4.</span><span class="sxs-lookup"><span data-stu-id="56199-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="56199-192">Caso contrário, use as seguintes etapas para criar um host:</span><span class="sxs-lookup"><span data-stu-id="56199-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="56199-193">a.</span><span class="sxs-lookup"><span data-stu-id="56199-193">a.</span></span> <span data-ttu-id="56199-194">Clique no símbolo de sinal de adição verde (**+**).</span><span class="sxs-lookup"><span data-stu-id="56199-194">Click the green plus (**+**) symbol.</span></span>

      ![Adicionar um novo host do Docker][PU02]

   <span data-ttu-id="56199-196">b.</span><span class="sxs-lookup"><span data-stu-id="56199-196">b.</span></span> <span data-ttu-id="56199-197">Quando a caixa de diálogo **Criar Host do Docker** for exibida, você poderá optar por aceitar os padrões ou especificar configurações personalizadas para o novo host do Docker.</span><span class="sxs-lookup"><span data-stu-id="56199-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="56199-198">(Para obter descrições detalhadas das várias configurações, consulte [Publicar um aplicativo Web como um contêiner do Docker usando o Kit de Ferramentas do Azure para IntelliJ][Publish Container with Azure Toolkit].) Clique em **Próximo** quando tiver especificado as configurações a serem usadas.</span><span class="sxs-lookup"><span data-stu-id="56199-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Especificar opções de host do Docker][PU03a]

   <span data-ttu-id="56199-200">c.</span><span class="sxs-lookup"><span data-stu-id="56199-200">c.</span></span> <span data-ttu-id="56199-201">Você pode optar por usar as credenciais de logon existentes de um Azure Key Vault ou inserir novas credenciais de logon do Docker.</span><span class="sxs-lookup"><span data-stu-id="56199-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="56199-202">Clique em **Concluir** quando tiver especificado suas opções.</span><span class="sxs-lookup"><span data-stu-id="56199-202">Click **Finish** when you have specified your options.</span></span>

      ![Especificar as credenciais de host do Docker][PU03b]

1. <span data-ttu-id="56199-204">Selecione o host do Docker e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56199-204">Select your Docker host, and then click **Next**.</span></span>

   ![Selecionar o host do Docker a ser usado][PU04]

1. <span data-ttu-id="56199-206">Na última página da caixa de diálogo **Implantar o Contêiner do Docker no Azure**, especifique as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="56199-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="56199-207">a.</span><span class="sxs-lookup"><span data-stu-id="56199-207">a.</span></span> <span data-ttu-id="56199-208">Você pode optar por especificar um nome personalizado para o contêiner que hospedará o contêiner do Docker ou aceitar o padrão.</span><span class="sxs-lookup"><span data-stu-id="56199-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="56199-209">b.</span><span class="sxs-lookup"><span data-stu-id="56199-209">b.</span></span> <span data-ttu-id="56199-210">Insira as portas TCP do host do Docker usando a seguinte sintaxe: *[external port]*:*[internal port]*.</span><span class="sxs-lookup"><span data-stu-id="56199-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="56199-211">Por exemplo, **80:8080** especifica uma porta externa 80 e a porta interna padrão 8080 do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="56199-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="56199-212">Se você tiver personalizado a porta interna (por exemplo, editando o arquivo application.yml), precisará especificar o número da porta para o roteamento correto ocorrer no Azure.</span><span class="sxs-lookup"><span data-stu-id="56199-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="56199-213">c.</span><span class="sxs-lookup"><span data-stu-id="56199-213">c.</span></span> <span data-ttu-id="56199-214">Depois de configurar essas opções, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="56199-214">After you have configured these options, click **Finish**.</span></span>

   ![Implantar um contêiner do Docker no Azure][PU05]

1. <span data-ttu-id="56199-216">Quando o Kit de Ferramentas do Azure concluir a publicação, o Log de Atividades do Azure exibirá **Publicado** como o status.</span><span class="sxs-lookup"><span data-stu-id="56199-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Host do Docker implantado com êxito][PU06]

## <a name="next-steps"></a><span data-ttu-id="56199-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="56199-218">Next steps</span></span>

<span data-ttu-id="56199-219">Para saber mais sobre outros métodos para criar aplicativos Spring Boot usando o IntelliJ, consulte [Criando projetos do Spring Boot](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) no site da JetBrains.</span><span class="sxs-lookup"><span data-stu-id="56199-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configurar Artefatos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
