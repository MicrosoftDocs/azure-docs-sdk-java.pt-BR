---
title: Ferramentas para desenvolvedores de Java do Azure | Microsoft Docs
description: "Integrações do IDE, emuladores, gerenciadores de recursos e interfaces de linha de comando para desenvolvedores de Java trabalhando no Azure."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 01fe31f2c59810f972875331d49ce5130755c8f2
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-tools-for-java-developers"></a>Ferramentas do Azure para desenvolvedores Java

## <a name="client-and-management-libraries"></a>Bibliotecas de cliente e gerenciamento

Conectar-se aos serviços e gerenciar recursos do Azure a partir de seus aplicativos com as bibliotecas do Azure para Java. Importar as bibliotecas de gerenciamento para seus projetos Maven adicionando essa dependência ao seu projeto *pom.xml*.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

Exibição da [lista completa das bibliotecas](java-sdk-azure-install.md) e [introdução](java-sdk-azure-get-started.md) para as bibliotecas do Azure para Java.

## <a name="eclipse-and-intellij-plugins"></a>Plug-ins Eclipse e IntelliJ

Gerenciar recursos do Azure e implantar aplicativos do seu IDE com o kit de ferramentas do Azure para [Eclipse](https://docs.microsoft.com/azure/azure-toolkit-for-eclipse) e [IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij).   

![Kit de ferramentas de IntelliJ mostrando o Gerenciador do Azure](media/intelliJ-azure-explorer.png)

[Introdução ao kit de ferramentas do Azure para Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Introdução ao kit de ferramentas do Azure para IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app) 

## <a name="azure-cli-20"></a>CLI do Azure 2.0

A CLI do Azure 2.0 fornece uma experiência de linha de comando para gerenciar recursos do Azure. Você pode usá-lo no seu navegador com o [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) ou pode [instalá-lo](https://docs.microsoft.com/cli/azure/install-azure-cli) no macOS, Linux e Windows e executá-lo da linha de comando.

[Introdução à CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).

## <a name="azure-storage-explorer"></a>Gerenciador de Armazenamento do Azure 

Gerenciar contas de armazenamento do Azure, contêineres e blobs/arquivos da área de trabalho. O Gerenciador de Armazenamento do Azure está atualmente em Versão prévia e funciona no Windows, macOS e Linux.

[Introdução ao Explorer do Armazenamento do Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)