---
title: Configure um aplicativo Inicializador do Spring Boot para usar o SpringBoot Starter do Azure Application Insights
description: Configure um aplicativo do Spring Boot criado com o Spring Initializr para usar o Application Insights SpringBoot Starter.
services: Application-Insights
documentationcenter: java
author: dhaval24
manager: alexklim
editor: ''
ms.assetid: ''
ms.author: dhdoshi
ms.date: 12/19/2018
ms.devlang: java
ms.service: Azure Monitor
ms.tgt_pltfrm: application-insights
ms.topic: article
ms.workload: na
ms.openlocfilehash: bf4f7e51f3108d684503465050d69461240f17e3
ms.sourcegitcommit: 9df42bd342ef2d25d56a6045f1ab1baf6f2c250e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2019
ms.locfileid: "54237287"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a><span data-ttu-id="5c19c-103">Configure um aplicativo Inicializador do Spring Boot para usar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="5c19c-103">Configure a Spring Boot Initializer app to use Application Insights</span></span>

<span data-ttu-id="5c19c-104">Este artigo explica como criar um aplicativo Spring Boot usando **[Spring Initializr]**, que usa o Spring Boot Starter do Azure Application Insights para monitoramento de ponta a ponta de aplicativos Java em nuvem.</span><span class="sxs-lookup"><span data-stu-id="5c19c-104">This article walks you through creating a Spring Boot application using **[Spring Initializr]**, that uses Azure Application Insights Spring Boot Starter for end-to-end monitoring of Java applications on cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c19c-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c19c-105">Prerequisites</span></span>

<span data-ttu-id="5c19c-106">Os seguintes pré-requisitos são obrigatórios para você concluir as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="5c19c-106">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="5c19c-107">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="5c19c-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="5c19c-108">Um JDK (Java Development Kit) com suporte.</span><span class="sxs-lookup"><span data-stu-id="5c19c-108">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="5c19c-109">Para obter mais informações sobre os JDKs disponíveis para usar durante o desenvolvimento no Azure, confira <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="5c19c-109">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="5c19c-110">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5c19c-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="5c19c-111">As APIs do Flux Web e do Netty **atualmente não têm suporte** com o iniciador do Spring Boot do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5c19c-111">Web Flux and Netty APIs are **not currently supported** with the Application Insights Spring Boot starter.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="5c19c-112">Criar um aplicativo personalizado usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="5c19c-112">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="5c19c-113">Navegue até [https://start.spring.io/](https://start.spring.io/).</span><span class="sxs-lookup"><span data-stu-id="5c19c-113">Browse to [https://start.spring.io/](https://start.spring.io/).</span></span>

1. <span data-ttu-id="5c19c-114">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, selecione a dependência Web na seção de dependências.</span><span class="sxs-lookup"><span data-stu-id="5c19c-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select web dependency in the dependenies section.</span></span>

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="5c19c-116">O Spring Initializr usará os nomes de **Grupo** e **Artefato** para criar o nome do pacote; por exemplo: *com.example.demo*.</span><span class="sxs-lookup"><span data-stu-id="5c19c-116">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.example.demo*.</span></span>
   >

1. <span data-ttu-id="5c19c-117">Clique no botão para **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="5c19c-117">Click the button to **Generate Project**.</span></span>

1. <span data-ttu-id="5c19c-118">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="5c19c-118">When prompted, download the project to a path on your local computer.</span></span>

1. <span data-ttu-id="5c19c-119">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot personalizado estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="5c19c-119">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Arquivos de projeto Spring Boot personalizados][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a><span data-ttu-id="5c19c-121">Criar um recurso do Application Insights no Azure</span><span class="sxs-lookup"><span data-stu-id="5c19c-121">Create an Application Insights Resource on Azure</span></span>

1. <span data-ttu-id="5c19c-122">Navegue até o Portal do Azure em <https://portal.azure.com/> e clique em **+Novo**.</span><span class="sxs-lookup"><span data-stu-id="5c19c-122">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Portal do Azure][AZ01]

1. <span data-ttu-id="5c19c-124">Clique em **Ferramentas de Gerenciamento** e, em seguida, clique em **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="5c19c-124">Click **Management Tools**, and then click **Application Insights**.</span></span>

   ![Portal do Azure][AZ02]

1. <span data-ttu-id="5c19c-126">Na página **Novo Recurso do Application Insights**, especifique as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="5c19c-126">On the **New Application Insights Resource** page, specify the following information:</span></span>

   * <span data-ttu-id="5c19c-127">Insira o **Nome** do seu recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5c19c-127">Enter the **Name** for your Application Insights resource.</span></span>
   * <span data-ttu-id="5c19c-128">Escolha o **Tipo de Aplicativo** para Aplicativo Web Java.</span><span class="sxs-lookup"><span data-stu-id="5c19c-128">Choose the **Application Type** to Java Web Application.</span></span>
   * <span data-ttu-id="5c19c-129">Especifique sua **Assinatura**, **Grupo de recursos** e **Local**.</span><span class="sxs-lookup"><span data-stu-id="5c19c-129">Specify your **Subscription**, **Resource group** and **Location**.</span></span>
   * <span data-ttu-id="5c19c-130">Selecione a opção Fixar no painel, se você quiser fixar o recurso no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c19c-130">Select Pin to dashboard option, if you would like to pin the resource on your Azure portal.</span></span>

   <span data-ttu-id="5c19c-131">Após especificar essas opções, clique em **Criar** para criar o recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5c19c-131">When you have specified these options, click **Create** to create your Application Insights resource.</span></span>

   ![Portal do Azure][AZ03]

1. <span data-ttu-id="5c19c-133">Após a criação do recurso, você o verá listado no **Painel** do Azure, bem como nas páginas **Todos os Recursos**.</span><span class="sxs-lookup"><span data-stu-id="5c19c-133">Once your resource has been created, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources** pages.</span></span> <span data-ttu-id="5c19c-134">Clique em seu recurso em qualquer um desses locais para abrir a página de visão geral do recurso Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5c19c-134">You can click on your resource on any of those locations to open the overview page of the Application Insights resource.</span></span> <span data-ttu-id="5c19c-135">Nessa página de visão geral, copie a **chave de instrumentação**.</span><span class="sxs-lookup"><span data-stu-id="5c19c-135">From this overview page please copy the **instrumentation key**.</span></span>

   ![Portal do Azure][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a><span data-ttu-id="5c19c-137">Configurar seu aplicativo baixado do Spring Boot para usar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="5c19c-137">Configure your downloaded Spring Boot Application to use Application Insights</span></span>

1. <span data-ttu-id="5c19c-138">Localize o arquivo *POM.xml* no diretório raiz do seu aplicativo e adicione a seguinte dependência em sua seção de dependências.</span><span class="sxs-lookup"><span data-stu-id="5c19c-138">Locate the *POM.xml* file in the root directory of your app, and add the following dependency in its dependencies section.</span></span> 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.1.1</version>
</dependency>
```

1. <span data-ttu-id="5c19c-139">Localize o arquivo *application.properties* no diretório *recursos* do seu aplicativo, ou crie o arquivo se ele ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="5c19c-139">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Localize o arquivo application.properties][RE01]

1. <span data-ttu-id="5c19c-141">Abra o arquivo *application.properties* em um editor de texto e adicione as seguintes linhas ao arquivo. Depois, substitua os valores de exemplo pelas propriedades adequadas com as credenciais certas:</span><span class="sxs-lookup"><span data-stu-id="5c19c-141">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties with appropriate credentials:</span></span>

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   <span data-ttu-id="5c19c-142">Para conferir outras maneiras de ajustar o Application Insights, consulte o [Leiame do inicializador Springboot do Application Insights](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="5c19c-142">For more ways to fine tune Application Insights please refer to [Application Insights Springboot starter readme](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="5c19c-143">Você pode usar chaves de instrumentação diferentes do Application Insights (ou seja,</span><span class="sxs-lookup"><span data-stu-id="5c19c-143">You can use different Application Insights instrumentation keys (i.e</span></span> <span data-ttu-id="5c19c-144">recursos diferentes) para perfis diferentes, como PROD, DEV etc. Consulte as [Propriedades específicas de perfil do Spring Boot] para saber mais.</span><span class="sxs-lookup"><span data-stu-id="5c19c-144">different resources) for different profiles like PROD, DEV etc. Please refer to [Spring Boot Profile Specific Properties] for additional information.</span></span> 

1. <span data-ttu-id="5c19c-145">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="5c19c-145">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="5c19c-146">Crie uma pasta chamada *controlador* sob a pasta de origem para o seu pacote; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c19c-146">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   <span data-ttu-id="5c19c-147">-ou-</span><span class="sxs-lookup"><span data-stu-id="5c19c-147">-or-</span></span>

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. <span data-ttu-id="5c19c-148">Crie um novo arquivo chamado *TestController.java* na pasta *controlador*.</span><span class="sxs-lookup"><span data-stu-id="5c19c-148">Create a new file named *TestController.java* in the *controller* folder.</span></span> <span data-ttu-id="5c19c-149">Abra o arquivo em um editor de texto e adicione o seguinte código a ele:</span><span class="sxs-lookup"><span data-stu-id="5c19c-149">Open the file in a text editor and add the following code to it:</span></span>

   ```java
    package com.example.demo;

    import com.microsoft.applicationinsights.TelemetryClient;
    import java.io.IOException;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    import com.microsoft.applicationinsights.telemetry.Duration;

    @RestController
    @RequestMapping("/sample")
    public class TestController {

        @Autowired
        TelemetryClient telemetryClient;

        @GetMapping("/hello")
        public String hello() {

            //track a custom event  
            telemetryClient.trackEvent("Sending a custom event...");

            //trace a custom trace
            telemetryClient.trackTrace("Sending a custom trace....");

            //track a custom metric
            telemetryClient.trackMetric("custom metric", 1.0);

            //track a custom dependency
            telemetryClient.trackDependency("SQL", "Insert", new Duration(0, 0, 1, 1, 1), true);

            return "hello";
        }
    }
   ```

   <span data-ttu-id="5c19c-150">Onde você precisará substituir `com.example.demo` pelo nome do pacote para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="5c19c-150">Where you will need to replace `com.example.demo` with the package name for your project.</span></span>

1. <span data-ttu-id="5c19c-151">Salve e feche o arquivo *TestController.java*.</span><span class="sxs-lookup"><span data-stu-id="5c19c-151">Save and close the *TestController.java* file.</span></span>

1. <span data-ttu-id="5c19c-152">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5c19c-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="5c19c-153">Teste o aplicativo Web navegando até http://localhost:8080/sample/hello com um navegador da Web ou use a sintaxe semelhante ao seguinte exemplo, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="5c19c-153">Test the web app by browsing to http://localhost:8080/sample/hello using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   <span data-ttu-id="5c19c-154">Você deve ver a mensagem "olá!"</span><span class="sxs-lookup"><span data-stu-id="5c19c-154">You should see the "hello!"</span></span> <span data-ttu-id="5c19c-155">no controlador de exemplo exibido.</span><span class="sxs-lookup"><span data-stu-id="5c19c-155">message from your sample controller displayed.</span></span> <span data-ttu-id="5c19c-156">O Application Insights coletará automaticamente essa solicitação e a enviará como um item de telemetria com seu evento personalizado, métrica personalizada, dependência personalizada e rastreamento personalizado associados, conforme especificado na lógica do controlador.</span><span class="sxs-lookup"><span data-stu-id="5c19c-156">Application Insights will automatically collect this request and send it as a telemetry item with it's associated custom event, custom metric, custom dependency and custom trace as specified in the controller logic.</span></span> 

   <span data-ttu-id="5c19c-157">Após alguns segundos, você deverá ver os dados no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c19c-157">After a few seconds you should see the data on Azure portal.</span></span> 

   ![Portal do Azure][AZ05]

   <span data-ttu-id="5c19c-159">Clique no bloco Mapa do Aplicativo para exibir os componentes de nível superior e a interação entre eles.</span><span class="sxs-lookup"><span data-stu-id="5c19c-159">You can click on Application Map tile to view high level components and their interaction with each other.</span></span> <span data-ttu-id="5c19c-160">Isso é recomendado para obter uma visão geral de alto nível de todo o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c19c-160">This is a recommended place to get a high level overview of entire application.</span></span> <span data-ttu-id="5c19c-161">Cada Microsserviço do Spring Boot é reconhecido pelo nome do aplicativo spring.</span><span class="sxs-lookup"><span data-stu-id="5c19c-161">Each Spring Boot Microservice is recognized by the spring application name.</span></span> <span data-ttu-id="5c19c-162">Lembre-se de defini-lo.</span><span class="sxs-lookup"><span data-stu-id="5c19c-162">Please remember to set it.</span></span>

   ![Portal do Azure][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a><span data-ttu-id="5c19c-164">Configurar aplicativo Springboot para enviar logs log4j ao Application Insights</span><span class="sxs-lookup"><span data-stu-id="5c19c-164">Configure Springboot Application to send log4j logs to Application Insights</span></span>

1. <span data-ttu-id="5c19c-165">Modifique o arquivo POM.xml do projeto e adicione/modifique a seção de dependências com o seguinte.</span><span class="sxs-lookup"><span data-stu-id="5c19c-165">Modify the POM.xml file of the project and add/modify the dependencies section with following.</span></span> 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-spring-boot-starter</artifactId>
        <version>1.1.1</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. <span data-ttu-id="5c19c-166">Salve e feche o arquivo *POM.xml*.</span><span class="sxs-lookup"><span data-stu-id="5c19c-166">Save and close the *POM.xml* file.</span></span>

3. <span data-ttu-id="5c19c-167">Na pasta \src\main\resources, crie um novo arquivo *log4j2.xml* e configure-o.</span><span class="sxs-lookup"><span data-stu-id="5c19c-167">In \src\main\resources folder, create a new file *log4j2.xml* and configure it.</span></span> <span data-ttu-id="5c19c-168">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="5c19c-168">For example:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Configuration packages="com.microsoft.applicationinsights.log4j.v2">
  <Properties>
    <Property name="LOG_PATTERN">
      %d{yyyy-MM-dd HH:mm:ss.SSS} %5p ${hostName} --- [%15.15t] %-40.40c{1.} : %m%n%ex
    </Property>
  </Properties>
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
    <ApplicationInsightsAppender name="aiAppender">
    </ApplicationInsightsAppender>
  </Appenders>
  <Loggers>
    <Root level="trace">
      <AppenderRef ref="Console"  />
      <AppenderRef ref="aiAppender"  />
    </Root>
  </Loggers>
</Configuration>
```
4. <span data-ttu-id="5c19c-169">Compile e execute novamente o aplicativo Spring Boot, como mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="5c19c-169">Build and run the Spring Boot application again as shown above.</span></span> 

<span data-ttu-id="5c19c-170">Dentro de alguns segundos, você verá todos os logs de spring disponíveis no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c19c-170">Within few seconds, you should see all the spring logs being available on Azure Portal.</span></span> 

![Portal do Azure][AZ06]

<span data-ttu-id="5c19c-172">É possível até mesmo examinar as mensagens de log detalhadas e fazer a análise no Portal do Analytics.</span><span class="sxs-lookup"><span data-stu-id="5c19c-172">You can even look at the detailed log messages and do analysis on Analytics Portal.</span></span> 

![Portal do Azure][AZ07]

## <a name="next-steps"></a><span data-ttu-id="5c19c-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c19c-174">Next steps</span></span>

<span data-ttu-id="5c19c-175">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c19c-175">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5c19c-176">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="5c19c-176">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="5c19c-177">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5c19c-177">Additional Resources</span></span>

<span data-ttu-id="5c19c-178">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="5c19c-178">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="5c19c-179">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="5c19c-179">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="5c19c-180">Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="5c19c-180">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="5c19c-181">O Application Insights oferece suporte à coleta automática de dependências externas e a correlação com as solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="5c19c-181">Application Insights supports automatic collection of external dependencies and its correlation with incoming requests.</span></span> <span data-ttu-id="5c19c-182">Atualmente, damos suporte à coleta automática da Oracle, MsSQL, MySQL e Redis.</span><span class="sxs-lookup"><span data-stu-id="5c19c-182">Currently we support autocollection of Oracle, MsSQL, MySQL and Redis.</span></span> <span data-ttu-id="5c19c-183">Para obter mais detalhes sobre como habilitar a coleta automática, confira o artigo [como usar o agente Java do Application Insights](/azure/application-insights/app-insights-java-agent).</span><span class="sxs-lookup"><span data-stu-id="5c19c-183">For more details on enabling autocollection please follow the article [how to use Application Insights Java agent](/azure/application-insights/app-insights-java-agent).</span></span>

<span data-ttu-id="5c19c-184">Para saber mais sobre o Azure Application Insights e seus recursos de monitoramento, confira a home page **[Application Insights]**.</span><span class="sxs-lookup"><span data-stu-id="5c19c-184">For more information about Azure Application Insights, and it's monitoring capabilities, see the **[Application Insights]** home page.</span></span>

<span data-ttu-id="5c19c-185">Para saber mais sobre detalhes de configuração adicionais do Inicializador do Spring Boot do Application Insights, consulte este [link](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="5c19c-185">For more information about additional configuration details of Application Insights Spring Boot Starter, please refer to this [link](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

<span data-ttu-id="5c19c-186">Para solicitações de recursos e possíveis bugs, registre os problemas em nosso repositório do [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues).</span><span class="sxs-lookup"><span data-stu-id="5c19c-186">For feature requests and potential bugs, please open issues on our [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues) repository.</span></span>

<span data-ttu-id="5c19c-187">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Como trabalhar com o Java e o Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="5c19c-187">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="5c19c-188">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="5c19c-188">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="5c19c-189">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="5c19c-189">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="5c19c-190">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em [https://github.com/spring-guides/](https://github.com/spring-guides/).</span><span class="sxs-lookup"><span data-stu-id="5c19c-190">To help developers get started with Spring Boot, several sample Spring Boot packages are available at [https://github.com/spring-guides/](https://github.com/spring-guides/).</span></span> <span data-ttu-id="5c19c-191">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="5c19c-191">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure para desenvolvedores Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Como trabalhar com o Java e o Azure DevOps]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Propriedades específicas de perfil do Spring Boot]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Boot Profile Specific Properties]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: /azure/application-insights/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_2.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_3.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Get_IKey.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/OverviewBladeResults.png
[AZ06]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Search_and_traces.png
[AZ07]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/traces_details.png
[AZ08]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/AppMap.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/spring_start.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/After_extract.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationproperties_loc.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationinsightsproperties.png
