---
title: Configurar implantações de aplicativo Web usando Java | Microsoft Docs
description: Exemplo de código de Java para configurar implantações de Git ou FTP do Serviço de Aplicativo do Azure usando o SDK do Azure para Java
author: rloutlaw
manager: douge
ms.assetid: 833e9c78-1e50-4c23-a611-f73a2f0c2983
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 910d1e43c9942d6402aeccb8757ba819b7453dab
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931182"
---
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a><span data-ttu-id="26071-103">Configurar fontes de implantação do Serviço de Aplicativo do Azure a partir dos seus aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="26071-103">Configure Azure App Service deployment sources from your Java applications</span></span>

<span data-ttu-id="26071-104">[Este exemplo](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) implanta o código para quatro aplicativos em um único plano do [Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service/), cada um usando uma origem de implantação diferente.</span><span class="sxs-lookup"><span data-stu-id="26071-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) deploys code to four applications in a single [Azure App Service](https://docs.microsoft.com/azure/app-service/) plan, each using a different deployment source.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="26071-105">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="26071-105">Run the sample</span></span>

<span data-ttu-id="26071-106">Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="26071-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="26071-107">Em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="26071-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

<span data-ttu-id="26071-108">Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span><span class="sxs-lookup"><span data-stu-id="26071-108">View the [complete sample code on GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="26071-109">Autenticar com o Azure</span><span class="sxs-lookup"><span data-stu-id="26071-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a><span data-ttu-id="26071-110">Criar um aplicativo do Serviço de Aplicativo executando Apache Tomcat</span><span class="sxs-lookup"><span data-stu-id="26071-110">Create a App Service app running Apache Tomcat</span></span>

```java
// create a new Standard app service plan and create a single Java 8/Tomcat 8 app in it
WebApp app1 = azure.webApps().define(app1Name)
             .withNewResourceGroup(rgName)
             .withNewAppServicePlan(planName)
             .withRegion(Region.US_WEST)
             .withPricingTier(AppServicePricingTier.STANDARD_S1)
             .withJavaVersion(JavaVersion.JAVA_8_NEWEST)
             .withWebContainer(WebContainer.TOMCAT_8_0_NEWEST)
             .create();
```

<span data-ttu-id="26071-111">`withJavaVersion()` e `withWebContainer()` configuram o Serviço de Aplicativo para atender solicitações HTTP usando o Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="26071-111">`withJavaVersion()` and `withWebContainer()` configure App Service to serve HTTP requests using Tomcat 8.</span></span>

## <a name="deploy-a-java-application-using-ftp"></a><span data-ttu-id="26071-112">Implantar um aplicativo Java usando FTP</span><span class="sxs-lookup"><span data-stu-id="26071-112">Deploy a Java application using FTP</span></span>
```java
// pass the PublishingProfile that contains FTP information to a helper method 
uploadFileToFtp(app1.getPublishingProfile(), "helloworld.war", 
      ManageWebAppSourceControl.class.getResourceAsStream("/helloworld.war"));

// Use the FTP classes in the Apache Commons library to connect to Azure using 
// the information from the PublishingProfile
private static void uploadFileToFtp(PublishingProfile profile, String fileName, InputStream file) throws Exception {
        FTPClient ftpClient = new FTPClient();
        String[] ftpUrlSegments = profile.ftpUrl().split("/", 2);
        String server = ftpUrlSegments[0];
        // Tomcat will deploy WAR files uploaded to this directory.
        String path = "./site/wwwroot/webapps"; 

        // FTP the build WAR to Azure
        ftpClient.connect(server);
        ftpClient.login(profile.ftpUsername(), profile.ftpPassword());
        ftpClient.setFileType(FTP.BINARY_FILE_TYPE);
        ftpClient.changeWorkingDirectory(path);
        ftpClient.storeFile(fileName, file);
        ftpClient.disconnect();
}
```

<span data-ttu-id="26071-113">Esse código carrega um arquivo WAR no diretório `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="26071-113">This code uploads a WAR file to the `/site/wwwroot/webapps` directory.</span></span> <span data-ttu-id="26071-114">O Tomcat implanta arquivos WAR colocados neste diretório por padrão no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26071-114">Tomcat deploys WAR files placed in this directory by default in App Service.</span></span>

## <a name="deploy-a-java-application-from-a-local-git-repo"></a><span data-ttu-id="26071-115">Implantar um aplicativo Java a partir de um repositório Git local</span><span class="sxs-lookup"><span data-stu-id="26071-115">Deploy a Java application from a local Git repo</span></span>

```java
// get the publishing profile from the App Service webapp
PublishingProfile profile = app2.getPublishingProfile();

// create a new Git repo in the sample directory under src/main/resources 
Git git = Git
    .init()
    .setDirectory(new File(ManageWebAppSourceControl.class.getResource("/azure-samples-appservice-helloworld/").getPath()))
    .call();
git.add().addFilepattern(".").call();
// add the files in the sample app to an initial commit
git.commit().setMessage("Initial commit").call(); 

// push the commit using the Azure Git remote URL and credentials in the publishing profile
PushCommand command = git.push();
command.setRemote(profile.gitUrl()); 
command.setCredentialsProvider(new UsernamePasswordCredentialsProvider(profile.gitUsername(), profile.gitPassword()));
command.setRefSpecs(new RefSpec("master:master")); 
command.setForce(true);
command.call();
```      

<span data-ttu-id="26071-116">Esse código usa as bibliotecas [JGit](https://eclipse.org/jgit/) para criar um novo repositório Git na pasta `src/main/resources/azure-samples-appservice-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="26071-116">This code uses the [JGit](https://eclipse.org/jgit/) libraries to create a new Git repo in the `src/main/resources/azure-samples-appservice-helloworld` folder.</span></span> <span data-ttu-id="26071-117">O exemplo de código, em seguida, adiciona todos os arquivos na pasta para uma confirmação inicial e envia a confirmação para o Azure usando as informações de implantação do Git do `PublishingProfile` do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="26071-117">The sample then adds all files in the folder to an initial commit and pushes the commit to Azure using Git deployment information from the webapp's `PublishingProfile`.</span></span> 

>[!NOTE]
> <span data-ttu-id="26071-118">O layout dos arquivos no repositório deve corresponder exatamente ao modo como você deseja que os arquivos sejam implantados sob o diretório `/site/wwwroot/` no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="26071-118">The layout of the files in the repo must match exactly how you want the files deployed under the `/site/wwwroot/` directory in Azure App Service.</span></span>

## <a name="deploy-an-application-from-a-public-git-repo"></a><span data-ttu-id="26071-119">Implantar um aplicativo a partir de um repositório Git público</span><span class="sxs-lookup"><span data-stu-id="26071-119">Deploy an application from a public Git repo</span></span>

```java
// deploy a .NET sample app from a public GitHub repo into a new webapp
WebApp app3 = azure.webApps().define(app3Name)
                .withNewResourceGroup(rgName)
                .withExistingAppServicePlan(plan)
                .defineSourceControl()
                .withPublicGitRepository(
                   "https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
                .withBranch("master")
                .attach()
                .create();
 ```

 <span data-ttu-id="26071-120">O tempo de execução do Serviço de Aplicativo automaticamente cria e implanta o projeto do .NET usando o código mais recente na ramificação `master` do repositório.</span><span class="sxs-lookup"><span data-stu-id="26071-120">The App Service runtime automatically builds and deploys the .NET project using the latest code on the `master` branch of the repo.</span></span>

## <a name="continuous-deployment-from-a-github-repo"></a><span data-ttu-id="26071-121">Implantação contínua de um repositório do GitHub</span><span class="sxs-lookup"><span data-stu-id="26071-121">Continuous deployment from a GitHub repo</span></span>

```java
// deploy the application whenever you push a new commit or merge a pull request into your master branch
WebApp app4 = azure.webApps()
                    .define(app4Name)
                    .withExistingResourceGroup(rgName)
                    .withExistingAppServicePlan(plan)
                    // Uncomment the following lines to turn on continuous deployment scenario
                    //.defineSourceControl()
                    //    .withContinuouslyIntegratedGitHubRepository("username", "reponame")
                    //    .withBranch("master")
                    //    .withGitHubAccessToken("YOUR GITHUB PERSONAL TOKEN")
                    //    .attach()
                    .create();
```  

<span data-ttu-id="26071-122">Os valores `username` e `reponame` são os usados no GitHub.</span><span class="sxs-lookup"><span data-stu-id="26071-122">The `username` and `reponame` values are the ones used in GitHub.</span></span> <span data-ttu-id="26071-123">[Criar um token de acesso pessoal do GitHub](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) com permissões de leitura do repositório e passá-lo para `withGitHubAccessToken`.</span><span class="sxs-lookup"><span data-stu-id="26071-123">[Create a GitHub personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) with repo read permissions and pass it to `withGitHubAccessToken`.</span></span> 


## <a name="sample-explanation"></a><span data-ttu-id="26071-124">Explicação do exemplo</span><span class="sxs-lookup"><span data-stu-id="26071-124">Sample explanation</span></span>

<span data-ttu-id="26071-125">O exemplo cria o primeiro aplicativo usando Java 8 e o Tomcat 8 em execução em um plano de Serviço de Aplicativo [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) recém-criado.</span><span class="sxs-lookup"><span data-stu-id="26071-125">The sample creates the first application using Java 8 and Tomcat 8 running in a newly created [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service plan.</span></span> <span data-ttu-id="26071-126">O código então envia por FTP um arquivo WAR usando as informações no objeto `PublishingProfile` e o Tomcat faz a implantação.</span><span class="sxs-lookup"><span data-stu-id="26071-126">The code then FTPs a WAR file using the information in the `PublishingProfile` object and Tomcat deploys it.</span></span>

<span data-ttu-id="26071-127">O segundo aplicativo usa o mesmo plano que o primeiro e também está configurado como um aplicativo de Java 8/Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="26071-127">The second application uses in the same plan as the first and is also configured as a Java 8/Tomcat 8 application.</span></span> <span data-ttu-id="26071-128">As bibliotecas de JGit criam um novo repositório Git em uma pasta que contém um aplicativo de Web Java descompactado em uma estrutura de diretório que mapeia para o Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26071-128">The JGit libraries create a new Git repository in a folder that contains an unpacked Java web application in a directory structure that maps to App Service.</span></span> <span data-ttu-id="26071-129">Uma nova confirmação adiciona os arquivos na pasta para o novo repositório Git e o Git envia a confirmação para o Azure com um nome de usuário/senha e URL remotos fornecidos pelo `PublishingProfile` do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="26071-129">A new commit adds the files in the folder to the new Git repo, and Git pushes the commit to Azure with a remote URL and username/password provided by the webapp's `PublishingProfile`.</span></span>

<span data-ttu-id="26071-130">O terceiro aplicativo não está configurado para Java e Tomcat.</span><span class="sxs-lookup"><span data-stu-id="26071-130">The third application is not configured for Java and Tomcat.</span></span> <span data-ttu-id="26071-131">Em vez disso, um exemplo do .NET em um repositório GitHub público é implantado diretamente da fonte.</span><span class="sxs-lookup"><span data-stu-id="26071-131">Instead, a .NET sample in a public GitHub repo is deployed directly from source.</span></span>

<span data-ttu-id="26071-132">O quarto aplicativo implanta o código em sua ramificação mestre toda vez que você enviar por push as alterações ou mesclar uma solicitação pull na ramificação mestre do repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="26071-132">The fourth application deploys the code in your master branch every time you push changes or merge a pull request into the GitHub repo's master branch.</span></span>

| <span data-ttu-id="26071-133">Classe usada no exemplo</span><span class="sxs-lookup"><span data-stu-id="26071-133">Class used in sample</span></span> | <span data-ttu-id="26071-134">Observações</span><span class="sxs-lookup"><span data-stu-id="26071-134">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="26071-135">WebApp</span><span class="sxs-lookup"><span data-stu-id="26071-135">WebApp</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | <span data-ttu-id="26071-136">Criada a partir da cadeia fluente `azure.webApps().define()....create()`.</span><span class="sxs-lookup"><span data-stu-id="26071-136">Created from the `azure.webApps().define()....create()` fluent chain.</span></span> <span data-ttu-id="26071-137">Cria um aplicativo Web do Serviço de Aplicativo e todos os recursos necessários para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26071-137">Creates a App Service web app and any resources needed for the app.</span></span> <span data-ttu-id="26071-138">A maioria dos métodos de consulta o objeto para obter detalhes de configuração, mas métodos de verbo como `restart()` alteram o estado do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="26071-138">Most methods query the object for configuration details, but verb methods like `restart()` change the state of the webapp.</span></span>
| [<span data-ttu-id="26071-139">WebContainer</span><span class="sxs-lookup"><span data-stu-id="26071-139">WebContainer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | <span data-ttu-id="26071-140">Classe com campos públicos estáticos usados como parâmetros para `withWebContainer()` ao definir um aplicativo Web executando um contêiner Web de Java.</span><span class="sxs-lookup"><span data-stu-id="26071-140">Class with static public fields used as paramters to `withWebContainer()` when defining a WebApp running a Java webcontainer.</span></span> <span data-ttu-id="26071-141">Existem opções para as versões Jetty e Tomcat.</span><span class="sxs-lookup"><span data-stu-id="26071-141">Has choices for both Jetty and Tomcat versions.</span></span>
| [<span data-ttu-id="26071-142">PublishingProfile</span><span class="sxs-lookup"><span data-stu-id="26071-142">PublishingProfile</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | <span data-ttu-id="26071-143">Obtido por meio de um objeto de aplicativo Web usando o método `getPublishingProfile()`.</span><span class="sxs-lookup"><span data-stu-id="26071-143">Obtained through a WebApp object using the `getPublishingProfile()` method.</span></span> <span data-ttu-id="26071-144">Contém informações de implantação Git e FTP, incluindo o nome de usuário e senha de implantação (que são diferentes das credenciais da entidade de serviço ou da conta do Azure).</span><span class="sxs-lookup"><span data-stu-id="26071-144">Contains FTP and Git deployment information, including deployment username and password (which is separate from Azure account or service principal credentials).</span></span>
| [<span data-ttu-id="26071-145">AppServicePlan</span><span class="sxs-lookup"><span data-stu-id="26071-145">AppServicePlan</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | <span data-ttu-id="26071-146">Retornado por `azure.appServices().appServicePlans().getByResourceGroup()`.</span><span class="sxs-lookup"><span data-stu-id="26071-146">Returned by `azure.appServices().appServicePlans().getByResourceGroup()`.</span></span> <span data-ttu-id="26071-147">Os métodos estão disponíveis para verificar a capacidade, a camada e o número de aplicativos Web em execução no plano.</span><span class="sxs-lookup"><span data-stu-id="26071-147">Methods are availble to check the capacity, tier, and number of web apps running in the plan.</span></span>
| [<span data-ttu-id="26071-148">AppServicePricingTier</span><span class="sxs-lookup"><span data-stu-id="26071-148">AppServicePricingTier</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | <span data-ttu-id="26071-149">Classe com campos estáticos públicos, que representa as camadas do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26071-149">Class with static public fields representing App Service tiers.</span></span> <span data-ttu-id="26071-150">Usada para definir uma camada de plano na linha durante a criação do aplicativo com `withPricingTier()` ou diretamente ao definir um plano por meio de `azure.appServices().appServicePlans().define()`</span><span class="sxs-lookup"><span data-stu-id="26071-150">Used to define a plan tier in-line during app creation with `withPricingTier()` or directly when defining a plan via `azure.appServices().appServicePlans().define()`</span></span>
| [<span data-ttu-id="26071-151">JavaVersion</span><span class="sxs-lookup"><span data-stu-id="26071-151">JavaVersion</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | <span data-ttu-id="26071-152">Classe com campos estáticos públicos, que representa as versões Java compatíveis com o Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26071-152">Class with static public fields representing Java versions supported by App Service.</span></span> <span data-ttu-id="26071-153">Usada com `withJavaVersion()` durante a cadeia `define()...create()` ao criar um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="26071-153">Used with `withJavaVersion()` during the `define()...create()` chain when creating a new webapp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26071-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26071-154">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]