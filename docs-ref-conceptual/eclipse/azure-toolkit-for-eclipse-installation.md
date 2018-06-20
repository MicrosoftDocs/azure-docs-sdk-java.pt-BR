---
title: Instalar o Kit de Ferramentas do Azure para Eclipse
description: Saiba como instalar o Kit de Ferramentas do Azure para o plug-in Eclipse para criar e implantar aplicativos de nuvem no Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: d5f685fa62ad74c8b8cd842b3667f8161e7c5760
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33887746"
---
# <a name="install-the-azure-toolkit-for-eclipse"></a>Instalar o Kit de Ferramentas do Azure para Eclipse

O Kit de Ferramentas do Azure para Eclipse fornece modelos e funcionalidades que permitem criar, desenvolver, testar e implantar facilmente aplicativos de nuvem para o Azure a partir do ambiente de desenvolvimento do Eclipse.

> [!NOTE] 
> 
> O Kit de Ferramentas do Azure para Eclipse é um projeto de código-fonte aberto, cujo código-fonte está disponível de acordo com a Licença do MIT no site do projeto no GitHub na seguinte URL: 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

As etapas a seguir mostram como instalar o Kit de Ferramentas do Azure para o Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Para instalar o Kit de Ferramentas do Azure para o Eclipse

1. Inicie o Eclipse.

1. Clique no menu **Ajuda** e, em seguida, clique em **Instalar Novo Software**, conforme mostrado na ilustração a seguir.
   
   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][01]

1. Na caixa de diálogo **Software Disponível** na caixa de texto **Trabalhar com**, digite `http://dl.microsoft.com/eclipse/` seguido pela tecla **Enter**.

1. No painel **Nome**, marque **Kit de Ferramentas do Azure para Java** e desmarque **Entrar em contato com todos os sites de atualização durante a instalação para encontrar o software necessário**. Sua tela será semelhante à seguinte:
   
   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][02]

1. Se você expandir o **Kit de Ferramentas do Azure para Eclipse**, verá uma lista de componentes que serão instalados; por exemplo:

   | Recurso | DESCRIÇÃO | 
   |---|---| 
   | **Plug-in do Application Insights para Java** | Permite que você use os serviços de registro em log e análise de telemetria do Azure para seus aplicativos e instâncias do servidor. | 
   | **Plug-in Comum do Azure** | fornece a funcionalidade comum necessária para outros componentes do kit de ferramentas. | 
   | **Ferramentas de Contêiner do Azure para Eclipse** | Permite que você crie e implante um .WAR como um contêiner do Docker em uma máquina do docker. | 
   | **Contêineres do Azure para Eclipse** | Permite que você implante um artefato .WAR ou .JAR como um contêiner do Docker em uma máquina virtual do Azure. | 
   | **Gerenciador do Azure para Eclipse** | Fornece uma interface do gerenciador para gerenciar os recursos do Azure. | 
   | **Microsoft JDBC Driver 6.1 para SQL Server** | Fornece a API JDBC para o SQL Server e o Banco de Dados SQL do Microsoft Azure para o Java Platform Enterprise Edition 8. | 
   | **Pacote para as Bibliotecas do Microsoft Azure para Java** | Fornece APIs para acessar os serviços do Microsoft Azure, como armazenamento, barramento de serviço, execução do serviço etc. | 

1. Clique em **Próximo**. (Se você experimentar atrasos incomuns ao instalar o kit de ferramentas, certifique-se de que a opção **Contatar todos os sites de atualização durante a instalação para encontrar o software necessário** está desmarcada.)

1. No diálogo **Instalar Detalhes**, clique em **Avançar**.
   
   ![Revisão dos detalhes de instalação][03]

1. No diálogo **Examinar Licenças** , leia os termos dos contratos de licença. Se você aceitar os termos dos contratos de licença, clique em **Aceito os termos dos contratos de licença** e clique em **Concluir**. (As etapas restantes supõem que você aceite os termos dos contratos de licença. Se você não aceitar os termos dos contratos de licença, saia do processo de instalação.)
   
   ![Examinar Licenças][04]
   
   O Eclipse baixará e instalará os pacotes necessários.
   
   ![Progresso da Instalação][05]

1. Se for solicitado a reiniciar o Eclipse para concluir a instalação, clique em **Sim**.
   
   ![Reinicie o prompt][06]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
