---
title: Instalação do Kit de Ferramentas do Azure para IntelliJ
description: Saiba como instalar o Kit de Ferramentas do Azure para o plug-in IntelliJ para criar e implantar aplicativos de nuvem no Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 86cef07873ae7a2ba75aab1044fe4d241cd5b13e
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270878"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a>Instalação do Kit de Ferramentas do Azure para IntelliJ

O Kit de Ferramentas do Azure para IntelliJ fornece modelos e funcionalidade que permitem criar, desenvolver, testar e implantar com facilidade aplicativos de nuvem ao Azure usando o ambiente de desenvolvimento IDEA do IntelliJ.

> [!NOTE] 
> 
> O Kit de Ferramentas do Azure para IntelliJ é um projeto de código-fonte aberto, cujo código-fonte está disponível de acordo com a Licença do MIT no site do projeto no GitHub na seguinte URL: 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

Há dois métodos de instalação do Kit de Ferramentas do Azure para IntelliJ: usando a caixa de diálogo **Configurações** e o menu **Configurar** na tela inicial. Ambos os métodos de instalação serão demonstrados nas etapas a seguir.

## <a name="prerequisites"></a>Pré-requisitos

O Azure Toolkit for IntelliJ requer os seguintes componentes de software:

* Um JDK (Java Development Kit) 8+ instalado, por exemplo: [OpenJDK](https://openjdk.java.net/) ou [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* Um [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition ou Community Edition instalado

> [!NOTE]
> 
> A página [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) no repositório de plug-in JetBrains lista as compilações compatíveis com o kit de ferramentas.
> 

<!--
> [!IMPORTANT]
> 
> If you are using the Azure Toolkit for IntelliJ on Windows, the toolkit requires installing the Azure SDK 2.9.6 or later in order to use the Azure emulator. You have two options for installing the Azure SDK:
> 
> * You can download and install the Azure SDK by using the [Web Platform Installer (WebPI)](http://go.microsoft.com/fwlink/?LinkID=252838).
> * If you do not have the Azure SDK installed when you create your first Azure deployment project, you will be prompted to automatically download install the requisite version of the Azure SDK.
> 
> Note that the Azure SDK is only required on Windows.
> 
-->


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a>Para instalar o Kit de Ferramentas do Azure para IntelliJ na caixa de diálogo de configurações

1. Inicie o IDEA do IntelliJ.

1. Quando o IDEA do IntelliJ é aberto, clique em **Arquivo**, em seguida, clique em **Configurações**.
   
   ![Abra a caixa de diálogo Configurações do IDEA do IntelliJ][01a]

1. Na caixa de diálogo Configurações, clique em **Plug-ins** e, em seguida, clique em **Procurar repositórios**.
   
   ![Caixa de diálogo Configurações do IDEA do IntelliJ][02a]

1. Na caixa de diálogo **Procurar repositórios** , digite "Azure" na caixa de pesquisa. Realce **Kit de Ferramentas do Azure para IntelliJ** e, em seguida, clique em **Instalar**.
   
   ![Procure o Kit de Ferramentas do Azure para IntelliJ][03]
   
   O IDEA do IntelliJ exibe o progresso da instalação em uma caixa de diálogo.
   
   ![Progresso da instalação][04]

1. Quando a instalação for concluída, clique em **Reiniciar IDEA do IntelliJ**.
   
   ![Reiniciar IDEA do IntelliJ][05]

1. Clique em **OK** para fechar a caixa de diálogo Configurações.
   
   ![Feche a caixa de diálogo Configurações do IDEA do IntelliJ][06]

1. Quando for solicitado a reiniciar o IDEA do IntelliJ ou adiar, clique em **Reiniciar**.
   
1   ![Reiniciar IDEA do IntelliJ][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a>Para instalar o Kit de Ferramentas do Azure para IntelliJ a partir da tela inicial

1. Inicie o IDEA do IntelliJ.

1. Quando for exibida a tela inicial do IDEA do IntelliJ, clique em **Configurar**, em seguida, clique em **Plug-ins**.
   
   ![Instale os plug-ins do IDEA do IntelliJ][01b]

1. Na caixa de diálogo **Plug-ins**, clique em **Procurar repositórios**.
   
   ![Procure os repositórios de plug-in do IDEA do IntelliJ][02b]

1. Na caixa de diálogo **Procurar repositórios** , digite "Azure" na caixa de pesquisa. Realce **Kit de Ferramentas do Azure para IntelliJ** e, em seguida, clique em **Instalar**.
   
   ![Procure o Kit de Ferramentas do Azure para IntelliJ][03]
   
   O IDEA do IntelliJ exibirá o progresso da instalação em uma caixa de diálogo.
   
   ![Progresso da instalação][04]

1. Quando a instalação for concluída, clique em **Reiniciar IDEA do IntelliJ**.
   
   ![Reiniciar IDEA do IntelliJ][05]

1. Quando for solicitado a reiniciar o IDEA do IntelliJ ou adiar, clique em **Reiniciar**.
   
   ![Reiniciar IDEA do IntelliJ][07]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[01a]: media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
