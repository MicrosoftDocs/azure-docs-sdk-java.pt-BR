---
title: Iniciadores do Spring Boot para Azure
description: "Este artigo descreve os vários iniciadores do Spring Boot disponíveis para o Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 678d4b279cecb83c95b3bf0f6bcdf1581924aa62
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="spring-boot-starters-for-azure"></a>Iniciadores do Spring Boot para Azure

Este artigo descreve os vários iniciadores do Spring Boot do [Spring Initializr] que fornecem aos desenvolvedores de Java os recursos de integração para trabalhar com o Microsoft Azure.

![Iniciadores Spring Boot para Azure][spring-boot-starters]

Os iniciadores do Spring Boot estão disponíveis atualmente para o Azure:

* **[Suporte do Azure](#azure-support)**

   Fornece suporte para configuração automática para serviços do Azure. Por exemplo, Barramento de Serviço, Armazenamento, Active Directory, etc.

* **[Azure Active Directory](#azure-active-directory)**

   Fornece suporte de integração ao Spring Security com o Azure Active Directory para autenticação.

* **[Azure Key Vault](#azure-key-vault)**

   Fornece suporte a Spring valor anotação para integração com os Segredos do Azure Key Vault.

* **[Armazenamento do Azure](#azure-storage)**

   Fornece suporte ao Spring Boot para serviços de Armazenamento do Azure.

<a name="azure-support"></a>
## <a name="azure-support"></a>Suporte do Azure

Este iniciador do Spring Boot fornece suporte de configuração automática para Serviços do Azure. Por exemplo: Barramento de Serviço, Armazenamento, Active Directory, Cosmos DB, o Key Vault, etc.

Para obter exemplos de como usar os vários recursos do Azure que são fornecidos por esse iniciador, consulte:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:

* A propriedade a seguir é adicionada ao elemento `<properties>`:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* A dependência `spring-boot-starter` padrão é substituída pelo seguinte:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* A seção a seguir é adicionada ao arquivo:

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
## <a name="azure-active-directory"></a>Azure Active Directory

Esse iniciador do Spring Boot fornece suporte de configuração automática para o Spring Security para fornecer integração com o Active Directory do Azure para autenticação.

Para obter exemplos de como usar os recursos do Azure Active Directory fornecidos por esse iniciador, consulte:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:

* A propriedade a seguir é adicionada ao elemento `<properties>`:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* A dependência `spring-boot-starter` padrão é substituída pelo seguinte:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* A seção a seguir é adicionada ao arquivo:

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
## <a name="azure-key-vault"></a>Cofre da Chave do Azure

Esse iniciador do Spring Boot fornece suporte de anotação ao valor do Spring para integração com os Segredos do Azure Key Vault.

Para obter exemplos de como usar os recursos do Azure Key Vault fornecidos por esse iniciador, consulte:

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:

* A propriedade a seguir é adicionada ao elemento `<properties>`:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* A dependência `spring-boot-starter` padrão é substituída pelo seguinte:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* A seção a seguir é adicionada ao arquivo:

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
## <a name="azure-storage"></a>Armazenamento do Azure

Esse iniciador do Spring Boot fornece suporte à integração do Spring Boot para serviços de Armazenamento do Azure.

Para obter exemplos de como usar os recursos do Armazenamento do Azure fornecidos por esse iniciador, consulte:

* [Como usar o iniciador do Spring Boot para Armazenamento do Azure](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

Quando você adiciona esse iniciador a um projeto do Spring Boot, as seguintes alterações são feitas ao arquivo *pom.xml*:

* A propriedade a seguir é adicionada ao elemento `<properties>`:

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* A dependência `spring-boot-starter` padrão é substituída pelo seguinte:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* A seção a seguir é adicionada ao arquivo:

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

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como usar aplicativos [Spring Boot] no Azure, consulte [Spring no Azure].

Para obter mais informações sobre como usar o Azure com o Java, veja os documentos [Azure para desenvolvedores Java] e [Ferramentas Java para Visual Studio Team Services].

Para obter ajuda na introdução a seus próprios aplicativos Spring Boot, confira **Spring Initializr** em https://start.spring.io/.

<!-- URL List -->

[Azure para desenvolvedores Java]: https://docs.microsoft.com/java/azure/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring no Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
