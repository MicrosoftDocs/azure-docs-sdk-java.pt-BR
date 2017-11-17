---
title: Como configurar o aplicativo Inicializador do Spring Boot para usar o Cache Redis
description: Saiba como configurar um aplicativo do Spring Boot criado com o Inicializador do Spring para usar o Cache Redis do Microsoft Azure.
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Spring Starter, Cache Redis
ms.assetid: 
ms.service: cache
ms.workload: na
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ce8202b48c6759a80560616492eab018434e9307
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a><span data-ttu-id="bd7cd-104">Como configurar o aplicativo Inicializador do Spring Boot para usar o Cache Redis</span><span class="sxs-lookup"><span data-stu-id="bd7cd-104">How to configure a Spring Boot Initializer app to use Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="bd7cd-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="bd7cd-105">Overview</span></span>

<span data-ttu-id="bd7cd-106">O **[Spring Framework]** é uma solução de software livre que ajuda os desenvolvedores Java criar aplicativos de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-106">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="bd7cd-107">Um dos projetos mais populares que é criado com base nessa plataforma é o [Spring Boot], que fornece uma abordagem simplificada para a criação de aplicativos Java autônomos.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-107">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="bd7cd-108">Para ajudar os desenvolvedores a começarem a usar o Spring Boot, vários exemplos de pacotes do Spring Boot estão disponíveis em <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="bd7cd-109">Além de escolher na lista de projetos básicos do Spring Boot, o  **[Spring Initializr]** ajuda os desenvolvedores a começarem a criar aplicativos personalizados do Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="bd7cd-110">Este artigo ensina a criar um cache Redis usando o Portal do Azure, em seguida, usar o **Spring Initializr** para criar um aplicativo personalizado e, depois disso, criar um aplicativo Web de Java que armazena e recupera os dados usando o cache Redis.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-110">This article walks you through creating a Redis cache using the Azure portal, then using the **Spring Initializr** to create a custom application, and then creating a Java web application that stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd7cd-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bd7cd-111">Prerequisites</span></span>

<span data-ttu-id="bd7cd-112">Os seguintes pré-requisitos são obrigatórios para que você siga as etapas neste artigo:</span><span class="sxs-lookup"><span data-stu-id="bd7cd-112">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="bd7cd-113">Uma assinatura do Azure; se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN] ou inscrever-se para uma [conta gratuita do Azure].</span><span class="sxs-lookup"><span data-stu-id="bd7cd-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="bd7cd-114">Um [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) versão 1.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="bd7cd-115">[Apache Maven](http://maven.apache.org/) versão 3.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="bd7cd-116">Criar um cache Redis no Azure</span><span class="sxs-lookup"><span data-stu-id="bd7cd-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="bd7cd-117">Navegue até o portal do Azure em <https://portal.azure.com/> e clique no item para **+Novo**.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-117">Browse to the Azure portal at <https://portal.azure.com/> and click the item for **+New**.</span></span>

   ![Portal do Azure][AZ01]

1. <span data-ttu-id="bd7cd-119">Clique em **Banco de Dados**e, em seguida, clique em **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Portal do Azure][AZ02]

1. <span data-ttu-id="bd7cd-121">Na página **Novo Cache Redis**, especifique as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="bd7cd-121">On the **New Redis Cache** page, specify the following information:</span></span>

   * <span data-ttu-id="bd7cd-122">Insira o **nome de DNS** para seu cache.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-122">Enter the **DNS name** for your cache.</span></span>
   * <span data-ttu-id="bd7cd-123">Especifique sua **Assinatura**, **Grupo de recursos**, **Local** e **Tipo de preço**.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-123">Specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span>
   * <span data-ttu-id="bd7cd-124">Neste tutorial, selecione **Desbloquear porta 6379**.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-124">For this tutorial, choose **Unblock port 6379**.</span></span>

   > [!NOTE]
   >
   > <span data-ttu-id="bd7cd-125">Você pode usar o SSL com caches Redis, mas você precisa usar um cliente Redis diferente, como o Jedis.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-125">You can use SSL with Redis caches, but you would need to use a different Redis client like Jedis.</span></span> <span data-ttu-id="bd7cd-126">Para mais informações, consulte [Como usar o Cache Redis do Azure com Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="bd7cd-126">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

   <span data-ttu-id="bd7cd-127">Quando você tiver especificado essas opções, clique em **Criar** para criar o cache.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-127">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Portal do Azure][AZ03]

1. <span data-ttu-id="bd7cd-129">Depois que o cache for concluído, você o verá listado no **Painel** do Azure, bem como nas páginas **Todos os Recursos** e **Caches Redis**.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-129">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="bd7cd-130">Você pode clicar no seu cache em qualquer um desses locais para abrir a página de propriedades do cache.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-130">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Portal do Azure][AZ04]

1. <span data-ttu-id="bd7cd-132">Quando a página que contém a lista de propriedades do cache for exibida, clique em **Chaves de acesso** e copie as chaves de acesso para o seu cache.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-132">When the page that contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Portal do Azure][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="bd7cd-134">Criar um aplicativo personalizado usando o Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="bd7cd-134">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="bd7cd-135">Navegue até <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-135">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="bd7cd-136">Especifique que você deseja gerar um projeto **Maven** com **Java**, insira os nomes de **Grupo** e **Artefato** para o seu aplicativo e, em seguida, clique no link para **Alternar para a versão completa** do Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-136">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Opções básicas do Initializr Basic][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="bd7cd-138">O Spring Initializr usa os nomes de **Grupo** e **Artefato** para criar o nome do pacote; por exemplo: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-138">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="bd7cd-139">Role para baixo até a seção **Web** e marque a caixa **Web**, em seguida, role para baixo até a seção **NoSQL** e marque a caixa **Redis**, em seguida, role até a parte inferior da página e clique no botão para **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-139">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Opções do Spring Initilializr Completo][SI02]

1. <span data-ttu-id="bd7cd-141">Quando solicitado, baixe o projeto para um caminho no computador local.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-141">When prompted, download the project to a path on your local computer.</span></span>

   ![Baixe o projeto personalizado do Spring Boot][SI03]

1. <span data-ttu-id="bd7cd-143">Depois de ter extraído os arquivos no sistema local, seu aplicativo Spring Boot personalizado estará pronto para edição.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-143">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Arquivos de projeto Spring Boot personalizados][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="bd7cd-145">Configurar o Spring Boot personalizado para usar o Cache Redis</span><span class="sxs-lookup"><span data-stu-id="bd7cd-145">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="bd7cd-146">Localize o arquivo *application.properties* no diretório *recursos* do seu aplicativo, ou crie o arquivo se ele ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-146">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Localize o arquivo application.properties][RE01]

1. <span data-ttu-id="bd7cd-148">Abra o arquivo *application.properties* em um editor de texto e adicione as seguintes linhas ao arquivo, então substitua os valores de exemplo pelas propriedades adequadas do seu cache:</span><span class="sxs-lookup"><span data-stu-id="bd7cd-148">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6379

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Edição do arquivo application.properties][RE02]

   > [!NOTE]
   >
   > <span data-ttu-id="bd7cd-150">Se você estivesse usando outro cliente Redis, como Jedis, que habilita o SSL, seria necessário especificar a porta 6380 no seu arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-150">If you were using a different Redis client like Jedis that enables SSL, you would specify port 6380 in your *application.properties* file.</span></span> <span data-ttu-id="bd7cd-151">Para mais informações, consulte [Como usar o Cache Redis do Azure com Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="bd7cd-151">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

1. <span data-ttu-id="bd7cd-152">Salve e feche o arquivo *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-152">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="bd7cd-153">Crie uma pasta chamada *controlador* sob a pasta de origem para o seu pacote; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bd7cd-153">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="bd7cd-154">-ou-</span><span class="sxs-lookup"><span data-stu-id="bd7cd-154">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="bd7cd-155">Crie um novo arquivo denominado *HelloController.java* na pasta *Controlador*.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-155">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="bd7cd-156">Abra o arquivo em um editor de texto e adicione o seguinte código a ele:</span><span class="sxs-lookup"><span data-stu-id="bd7cd-156">Open the file in a text editor and add the following code to it:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.data.redis.core.StringRedisTemplate;
   import org.springframework.data.redis.core.ValueOperations;

   @RestController
   public class HelloController {
   
      @Autowired
      private StringRedisTemplate template;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         ValueOperations<String, String> ops = this.template.opsForValue();

         // Add a Hello World string to your cache.
         String key = "greeting";
         if (!this.template.hasKey(key)) {
             ops.set(key, "Hello World!");
         }

         // Return the string from your cache.
         return ops.get(key);
      }
   }
   ```
   
   <span data-ttu-id="bd7cd-157">Onde você precisará substituir `com.contoso.myazuredemo` pelo nome do pacote para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-157">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="bd7cd-158">Salve e feche o arquivo *HelloController.java*.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-158">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="bd7cd-159">Crie seu aplicativo Spring Boot com Maven e execute-o; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bd7cd-159">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="bd7cd-160">Teste o aplicativo Web navegando até http://localhost:8080 com um navegador da Web ou use a sintaxe semelhante ao seguinte exemplo, se você tiver o curl disponível:</span><span class="sxs-lookup"><span data-stu-id="bd7cd-160">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="bd7cd-161">Você deve ver "Olá, Mundo!"</span><span class="sxs-lookup"><span data-stu-id="bd7cd-161">You should see the "Hello World!"</span></span> <span data-ttu-id="bd7cd-162">mensagem do seu controlador de exemplo exibido, que está sendo recuperado dinamicamente do seu cache Redis.</span><span class="sxs-lookup"><span data-stu-id="bd7cd-162">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd7cd-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd7cd-163">Next steps</span></span>

<span data-ttu-id="bd7cd-164">Para obter mais informações sobre como usar aplicativos Spring Boot no Azure, confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="bd7cd-164">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="bd7cd-165">Implantar um aplicativo Spring Boot no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="bd7cd-165">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="bd7cd-166">Executando um Aplicativo Spring Boot em um Cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="bd7cd-166">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="bd7cd-167">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="bd7cd-167">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="bd7cd-168">Para saber mais sobre como começar a usar o Cache Redis com Java no Azure, consulte [Como usar o Cache Redis do Azure com Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="bd7cd-168">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<!-- URL List -->

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[conta gratuita do Azure]: https://azure.microsoft.com/pricing/free-trial/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[benefício de assinante do MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: /azure/redis-cache/cache-java-get-started

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ01.png
[AZ02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ02.png
[AZ03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ03.png
[AZ04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ04.png
[AZ05]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ05.png

[SI01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI01.png
[SI02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI02.png
[SI03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI03.png
[SI04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI04.png

[RE01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE01.png
[RE02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE02.png
