---
title: Iniciadores do Spring Boot para Azure
description: "Este artigo descreve os vários iniciadores do Spring Boot disponíveis para o Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm
ms.openlocfilehash: ba5829407d03d275784a3a458d88ea47ac8494b8
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="87e9a-103">Iniciadores do Spring Boot para Azure</span><span class="sxs-lookup"><span data-stu-id="87e9a-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="87e9a-104">Este artigo descreve os vários iniciadores do Spring Boot do [Spring Initializr] que fornecem aos desenvolvedores de Java os recursos de integração para trabalhar com o Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="87e9a-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Iniciadores Spring Boot para Azure][spring-boot-starters]

<span data-ttu-id="87e9a-106">Os iniciadores do Spring Boot estão disponíveis atualmente para o Azure:</span><span class="sxs-lookup"><span data-stu-id="87e9a-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="87e9a-107">**[Suporte do Azure](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="87e9a-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="87e9a-108">Fornece suporte para configuração automática para serviços do Azure. Por exemplo, Barramento de Serviço, Armazenamento, Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="87e9a-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="87e9a-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="87e9a-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="87e9a-110">Fornece suporte de integração ao Spring Security com o Azure Active Directory para autenticação.</span><span class="sxs-lookup"><span data-stu-id="87e9a-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="87e9a-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="87e9a-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="87e9a-112">Fornece suporte a Spring valor anotação para integração com os Segredos do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="87e9a-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="87e9a-113">**[Armazenamento do Azure](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="87e9a-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="87e9a-114">Fornece suporte ao Spring Boot para serviços de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="87e9a-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="87e9a-115">Suporte do Azure</span><span class="sxs-lookup"><span data-stu-id="87e9a-115">Azure Support</span></span>

<span data-ttu-id="87e9a-116">Este iniciador do Spring Boot fornece suporte de configuração automática para Serviços do Azure. Por exemplo: Barramento de Serviço, Armazenamento, Active Directory, Cosmos DB, o Key Vault, etc.</span><span class="sxs-lookup"><span data-stu-id="87e9a-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="87e9a-117">Para obter exemplos de como usar os vários recursos do Azure que são fornecidos por esse iniciador, consulte:</span><span class="sxs-lookup"><span data-stu-id="87e9a-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="87e9a-118"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples></span><span class="sxs-lookup"><span data-stu-id="87e9a-118"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples></span></span>

<span data-ttu-id="87e9a-119">Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="87e9a-119">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="87e9a-120">A propriedade a seguir é adicionada ao elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="87e9a-120">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="87e9a-121">A dependência `spring-boot-starter` padrão é substituída pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="87e9a-121">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="87e9a-122">A seção a seguir é adicionada ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="87e9a-122">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="87e9a-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87e9a-123">Azure Active Directory</span></span>

<span data-ttu-id="87e9a-124">Esse iniciador do Spring Boot fornece suporte de configuração automática para o Spring Security para fornecer integração com o Active Directory do Azure para autenticação.</span><span class="sxs-lookup"><span data-stu-id="87e9a-124">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="87e9a-125">Para obter exemplos de como usar os recursos do Azure Active Directory fornecidos por esse iniciador, consulte:</span><span class="sxs-lookup"><span data-stu-id="87e9a-125">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="87e9a-126"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="87e9a-126"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample></span></span>

<span data-ttu-id="87e9a-127">Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="87e9a-127">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="87e9a-128">A propriedade a seguir é adicionada ao elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="87e9a-128">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="87e9a-129">A dependência `spring-boot-starter` padrão é substituída pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="87e9a-129">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="87e9a-130">A seção a seguir é adicionada ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="87e9a-130">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="87e9a-131">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="87e9a-131">Azure Key Vault</span></span>

<span data-ttu-id="87e9a-132">Esse iniciador do Spring Boot fornece suporte de anotação ao valor do Spring para integração com os Segredos do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="87e9a-132">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="87e9a-133">Para obter exemplos de como usar os recursos do Azure Key Vault fornecidos por esse iniciador, consulte:</span><span class="sxs-lookup"><span data-stu-id="87e9a-133">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <span data-ttu-id="87e9a-134"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="87e9a-134"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample></span></span>

<span data-ttu-id="87e9a-135">Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="87e9a-135">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="87e9a-136">A propriedade a seguir é adicionada ao elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="87e9a-136">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="87e9a-137">A dependência `spring-boot-starter` padrão é substituída pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="87e9a-137">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="87e9a-138">A seção a seguir é adicionada ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="87e9a-138">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="87e9a-139">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="87e9a-139">Azure Storage</span></span>

<span data-ttu-id="87e9a-140">Esse iniciador do Spring Boot fornece suporte à integração do Spring Boot para serviços de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="87e9a-140">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="87e9a-141">Para obter exemplos de como usar os recursos do Armazenamento do Azure fornecidos por esse iniciador, consulte:</span><span class="sxs-lookup"><span data-stu-id="87e9a-141">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="87e9a-142">Como usar o iniciador do Spring Boot para Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="87e9a-142">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <span data-ttu-id="87e9a-143"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample></span><span class="sxs-lookup"><span data-stu-id="87e9a-143"><https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample></span></span>

<span data-ttu-id="87e9a-144">Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:</span><span class="sxs-lookup"><span data-stu-id="87e9a-144">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="87e9a-145">A propriedade a seguir é adicionada ao elemento `<properties>`:</span><span class="sxs-lookup"><span data-stu-id="87e9a-145">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="87e9a-146">A dependência `spring-boot-starter` padrão é substituída pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="87e9a-146">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="87e9a-147">A seção a seguir é adicionada ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="87e9a-147">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="87e9a-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87e9a-148">Next steps</span></span>

<span data-ttu-id="87e9a-149">Para obter mais informações sobre como usar aplicativos [Spring Boot] no Azure, consulte [Spring no Azure].</span><span class="sxs-lookup"><span data-stu-id="87e9a-149">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="87e9a-150">Para saber mais sobre como usar o Azure com o Java, consulte [Azure para desenvolvedores Java] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="87e9a-150">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="87e9a-151">Para obter ajuda na introdução a seus próprios aplicativos Spring Boot, confira **Spring Initializr** em https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="87e9a-151">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring no Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
