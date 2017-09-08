---
title: "Configurar implantações de aplicativo Web usando Java | Microsoft Docs"
description: "Exemplo de código de Java para configurar implantações de Git ou FTP do Serviço de Aplicativo do Azure usando o SDK do Azure para Java"
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
---
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a>Configurar fontes de implantação do Serviço de Aplicativo do Azure a partir dos seus aplicativos Java

[Este exemplo](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) implanta o código para quatro aplicativos em um único plano do [Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service/), cada um usando uma origem de implantação diferente.

## <a name="run-the-sample"></a>Execute o exemplo

Criar um [arquivo de autenticação](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) e definir uma variável de ambiente `AZURE_AUTH_LOCATION` com o caminho completo para o arquivo em seu computador. Em seguida, execute:

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

Exibição de [exemplo de código completo no GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).

## <a name="authenticate-with-azure"></a>Autenticar com o Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a>Criar um aplicativo do Serviço de Aplicativo executando Apache Tomcat

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

`withJavaVersion()` e `withWebContainer()` configuram o Serviço de Aplicativo para atender solicitações HTTP usando o Tomcat 8.

## <a name="deploy-a-java-application-using-ftp"></a>Implantar um aplicativo Java usando FTP
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

Esse código carrega um arquivo WAR no diretório `/site/wwwroot/webapps`. O Tomcat implanta arquivos WAR colocados neste diretório por padrão no Serviço de Aplicativo.

## <a name="deploy-a-java-application-from-a-local-git-repo"></a>Implantar um aplicativo Java a partir de um repositório Git local

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

Esse código usa as bibliotecas [JGit](https://eclipse.org/jgit/) para criar um novo repositório Git na pasta `src/main/resources/azure-samples-appservice-helloworld`. O exemplo de código, em seguida, adiciona todos os arquivos na pasta para uma confirmação inicial e envia a confirmação para o Azure usando as informações de implantação do Git do `PublishingProfile` do aplicativo Web. 

>[!NOTE]
> O layout dos arquivos no repositório deve corresponder exatamente ao modo como você deseja que os arquivos sejam implantados sob o diretório `/site/wwwroot/` no Serviço de Aplicativo do Azure.

## <a name="deploy-an-application-from-a-public-git-repo"></a>Implantar um aplicativo a partir de um repositório Git público

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

 O tempo de execução do Serviço de Aplicativo automaticamente cria e implanta o projeto do .NET usando o código mais recente na ramificação `master` do repositório.

## <a name="continuous-deployment-from-a-github-repo"></a>Implantação contínua de um repositório do GitHub

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

Os valores `username` e `reponame` são os usados no GitHub. [Criar um token de acesso pessoal do GitHub](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) com permissões de leitura do repositório e passá-lo para `withGitHubAccessToken`. 


## <a name="sample-explanation"></a>Explicação do exemplo

O exemplo cria o primeiro aplicativo usando Java 8 e o Tomcat 8 em execução em um plano de Serviço de Aplicativo [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) recém-criado. O código então envia por FTP um arquivo WAR usando as informações no objeto `PublishingProfile` e o Tomcat faz a implantação.

O segundo aplicativo usa o mesmo plano que o primeiro e também está configurado como um aplicativo de Java 8/Tomcat 8. As bibliotecas de JGit criam um novo repositório Git em uma pasta que contém um aplicativo de Web Java descompactado em uma estrutura de diretório que mapeia para o Serviço de Aplicativo. Uma nova confirmação adiciona os arquivos na pasta para o novo repositório Git e o Git envia a confirmação para o Azure com um nome de usuário/senha e URL remotos fornecidos pelo `PublishingProfile` do aplicativo Web.

O terceiro aplicativo não está configurado para Java e Tomcat. Em vez disso, um exemplo do .NET em um repositório GitHub público é implantado diretamente da fonte.

O quarto aplicativo implanta o código em sua ramificação mestre toda vez que você enviar por push as alterações ou mesclar uma solicitação pull na ramificação mestre do repositório GitHub.

| Classe usada no exemplo | Observações
|-------|-------|
| [WebApp](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | Criada a partir da cadeia fluente `azure.webApps().define()....create()`. Cria um aplicativo Web do Serviço de Aplicativo e todos os recursos necessários para o aplicativo. A maioria dos métodos de consulta o objeto para obter detalhes de configuração, mas métodos de verbo como `restart()` alteram o estado do aplicativo Web.
| [WebContainer](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | Classe com campos públicos estáticos usados como parâmetros para `withWebContainer()` ao definir um aplicativo Web executando um contêiner Web de Java. Existem opções para as versões Jetty e Tomcat.
| [PublishingProfile](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | Obtido por meio de um objeto de aplicativo Web usando o método `getPublishingProfile()`. Contém informações de implantação Git e FTP, incluindo o nome de usuário e senha de implantação (que são diferentes das credenciais da entidade de serviço ou da conta do Azure).
| [AppServicePlan](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | Retornado por `azure.appServices().appServicePlans().getByResourceGroup()`. Os métodos estão disponíveis para verificar a capacidade, a camada e o número de aplicativos Web em execução no plano.
| [AppServicePricingTier](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | Classe com campos estáticos públicos, que representa as camadas do Serviço de Aplicativo. Usada para definir uma camada de plano na linha durante a criação do aplicativo com `withPricingTier()` ou diretamente ao definir um plano por meio de `azure.appServices().appServicePlans().define()`
| [JavaVersion](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | Classe com campos estáticos públicos, que representa as versões Java compatíveis com o Serviço de Aplicativo. Usada com `withJavaVersion()` durante a cadeia `define()...create()` ao criar um novo aplicativo Web.

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [next-steps](includes/java-next-steps.md)]