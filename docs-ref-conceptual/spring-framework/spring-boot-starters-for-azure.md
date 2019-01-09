---
title: Iniciadores do Spring Boot para Azure
description: Este artigo descreve os vários iniciadores do Spring Boot disponíveis para o Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 69c0381313994796af31d5301ceadb9f6f40dcb5
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991550"
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="d35ed-103">Iniciadores do Spring Boot para Azure</span><span class="sxs-lookup"><span data-stu-id="d35ed-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="d35ed-104">Este artigo descreve os vários iniciadores do Spring Boot do [Spring Initializr] que fornecem aos desenvolvedores de Java os recursos de integração para trabalhar com o Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d35ed-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Iniciadores Spring Boot para Azure][spring-boot-starters]

<span data-ttu-id="d35ed-106">Os iniciadores do Spring Boot estão disponíveis atualmente para o Azure:</span><span class="sxs-lookup"><span data-stu-id="d35ed-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="d35ed-107">**[Suporte do Azure](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="d35ed-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="d35ed-108">Fornece suporte para configuração automática para serviços do Azure. Por exemplo, Barramento de Serviço, Armazenamento, Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="d35ed-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="d35ed-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="d35ed-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="d35ed-110">Fornece suporte de integração ao Spring Security com o Azure Active Directory para autenticação.</span><span class="sxs-lookup"><span data-stu-id="d35ed-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="d35ed-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="d35ed-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="d35ed-112">Fornece suporte a Spring valor anotação para integração com os Segredos do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d35ed-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="d35ed-113">**[Armazenamento do Azure](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="d35ed-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="d35ed-114">Fornece suporte ao Spring Boot para serviços de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d35ed-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="d35ed-115">Suporte do Azure</span><span class="sxs-lookup"><span data-stu-id="d35ed-115">Azure Support</span></span>

<span data-ttu-id="d35ed-116">Esse iniciador do Spring Boot fornece suporte à configuração automática para Serviços do Azure; por exemplo: Barramento de Serviço, Armazenamento, Active Directory, Cosmos DB, Cofre de chaves etc.</span><span class="sxs-lookup"><span data-stu-id="d35ed-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="d35ed-117">Para obter exemplos de como usar os vários recursos do Azure que são fornecidos por esse iniciador, consulte:</span><span class="sxs-lookup"><span data-stu-id="d35ed-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

<span data-ttu-id="d35ed-118">Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="d35ed-118">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="d35ed-119">A propriedade a seguir é adicionada ao elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="d35ed-119">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="d35ed-120">A dependência `spring-boot-starter` padrão é substituída pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="d35ed-120">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="d35ed-121">A seção a seguir é adicionada ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="d35ed-121">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-active-directory"></a>
## <a name="azure-active-directory"></a><span data-ttu-id="d35ed-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d35ed-122">Azure Active Directory</span></span>

<span data-ttu-id="d35ed-123">Esse iniciador do Spring Boot fornece suporte de configuração automática para o Spring Security para fornecer integração com o Active Directory do Azure para autenticação.</span><span class="sxs-lookup"><span data-stu-id="d35ed-123">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="d35ed-124">Para obter exemplos de como usar os recursos do Azure Active Directory fornecidos por esse iniciador, consulte:</span><span class="sxs-lookup"><span data-stu-id="d35ed-124">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

<span data-ttu-id="d35ed-125">Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="d35ed-125">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="d35ed-126">A propriedade a seguir é adicionada ao elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="d35ed-126">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="d35ed-127">A dependência `spring-boot-starter` padrão é substituída pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="d35ed-127">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="d35ed-128">A seção a seguir é adicionada ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="d35ed-128">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-key-vault"></a>
## <a name="azure-key-vault"></a><span data-ttu-id="d35ed-129">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="d35ed-129">Azure Key Vault</span></span>

<span data-ttu-id="d35ed-130">Esse iniciador do Spring Boot fornece suporte de anotação ao valor do Spring para integração com os Segredos do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d35ed-130">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="d35ed-131">Para obter exemplos de como usar os recursos do Azure Key Vault fornecidos por esse iniciador, consulte:</span><span class="sxs-lookup"><span data-stu-id="d35ed-131">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

<span data-ttu-id="d35ed-132">Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="d35ed-132">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="d35ed-133">A propriedade a seguir é adicionada ao elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="d35ed-133">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="d35ed-134">A dependência `spring-boot-starter` padrão é substituída pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="d35ed-134">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="d35ed-135">A seção a seguir é adicionada ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="d35ed-135">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-storage"></a>
## <a name="azure-storage"></a><span data-ttu-id="d35ed-136">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d35ed-136">Azure Storage</span></span>

<span data-ttu-id="d35ed-137">Esse iniciador do Spring Boot fornece suporte à integração do Spring Boot para serviços de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d35ed-137">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="d35ed-138">Para obter exemplos de como usar os recursos do Armazenamento do Azure fornecidos por esse iniciador, consulte:</span><span class="sxs-lookup"><span data-stu-id="d35ed-138">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="d35ed-139">Como usar o iniciador do Spring Boot para Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d35ed-139">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

<span data-ttu-id="d35ed-140">Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="d35ed-140">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="d35ed-141">A propriedade a seguir é adicionada ao elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="d35ed-141">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="d35ed-142">A dependência `spring-boot-starter` padrão é substituída pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="d35ed-142">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="d35ed-143">A seção a seguir é adicionada ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="d35ed-143">The following section is added to the file:</span></span>

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

## <a name="next-steps"></a><span data-ttu-id="d35ed-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d35ed-144">Next steps</span></span>

<span data-ttu-id="d35ed-145">Para saber mais sobre o Spring e o Azure, continue no Spring no Centro de Documentação do Azure.</span><span class="sxs-lookup"><span data-stu-id="d35ed-145">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d35ed-146">Spring no Azure</span><span class="sxs-lookup"><span data-stu-id="d35ed-146">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="d35ed-147">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d35ed-147">Additional Resources</span></span>

<span data-ttu-id="d35ed-148">Para obter mais informações sobre como usar aplicativos [Spring Boot] no Azure, consulte [Spring no Azure].</span><span class="sxs-lookup"><span data-stu-id="d35ed-148">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="d35ed-149">Para obter mais informações sobre como usar o Azure com Java, confira [Azure para Desenvolvedores Java] e [Trabalhando com o Java e Azure DevOps].</span><span class="sxs-lookup"><span data-stu-id="d35ed-149">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="d35ed-150">Para obter ajuda na introdução a seus próprios aplicativos Spring Boot, confira **Spring Initializr** em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="d35ed-150">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure para desenvolvedores Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Trabalhando com o Java e Azure DevOps]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring no Azure]: /java/azure/spring-framework/
[Spring on Azure]: /java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
