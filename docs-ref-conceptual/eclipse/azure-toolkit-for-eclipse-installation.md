---
title: "Instalação do Kit de Ferramentas do Azure para o Eclipse"
description: Saiba como instalar o Kit de Ferramentas do Azure para o Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 59a8bfb6ab4db8ea8c6c9025ca3ced8a13192628
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Instalação do Kit de Ferramentas do Azure para o Eclipse

O Kit de Ferramentas do Azure para Eclipse fornece modelos e funcionalidade que permitem criar, desenvolver, testar e implantar com facilidade aplicativos Azure usando o ambiente de desenvolvimento do Eclipse. O Kit de Ferramentas do Azure para Eclipse é um projeto de software livre. O código-fonte está disponível sob a licença do MIT em <https://github.com/microsoft/azure-tools-for-java>.

As etapas a seguir mostram como instalar o Kit de Ferramentas do Azure para o Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Para instalar o Kit de Ferramentas do Azure para o Eclipse

1. Inicie o Eclipse.

1. Clique no menu **Ajuda** e, em seguida, clique em **Instalar Novo Software**, conforme mostrado na ilustração a seguir.
   
   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][01]

1. Na caixa de diálogo **Software Disponível** na caixa de texto **Trabalhar com**, digite `http://dl.microsoft.com/eclipse/` seguido pela tecla **Enter**.

1. No painel **Nome**, marque **Kit de Ferramentas do Azure para o Eclipse** e desmarque **Entrar em contato com todos os sites de atualização durante a instalação para encontrar o software necessário**. Sua tela será semelhante à seguinte:
   
   ![Instalação do Kit de Ferramentas do Azure para o Eclipse][02]

1. Se você expandir o **Kit de Ferramentas do Azure para Eclipse**, verá uma lista de itens como um exemplo a seguir:
   
   * **Plug-in do Application Insights para Java**: este componente permite que você use os serviços de registro em log e análise de telemetria do Azure para seus aplicativos e instâncias de servidor.
   * **Filtro dos Serviços de Controle de Acesso do Azure**: esse componente oferece suporte para autenticar usuários de aplicativo com o Azure ACS, habilitar cenários de logon únicos e externalização lógica da identidade do aplicativo.
   * **Plug-in comum do Azure**: esse componente fornece a funcionalidade comum necessária para outros componentes do kit de ferramentas.
   * **Azure Explorer para Eclipse**: esse componente fornece a funcionalidade comum necessária para outros componentes do kit de ferramentas.
   * **Plug-in do azure para Eclipse com Java**: esse componente oferece suporte para o desenvolvimento de projetos que ajudam a criar, testar e implantar aplicativos Java para a nuvem do Microsoft Azure no Eclipse e via linha de comando.
   * **Plug-in de aplicativos Web do Azure com Java**: esse componente oferece suporte para implantar os aplicativos Web Java para contêineres de aplicativo Web do Microsoft Azure.
   * **Microsoft JDBC Driver 4.2 para SQL Server**: esse componente fornece a API JDBC para SQL Server e Banco de Dados SQL do Microsoft Azure para Java Platform Enterprise Edition 8.
   * **Pacote para Bibliotecas de Cliente do Apache Qpid para JMS**: esse componente fornece o componente de cliente JMS a partir do projeto do Apache Qpid para habilitar seu aplicativo a usar o sistema de mensagens baseado no protocolo AMQP no Microsoft Azure.
   * **Pacote para Bibliotecas do Microsoft Azure para Java**: esse componente fornece APIs para acessar serviços do Microsoft Azure, como armazenamento, barramento de serviço, tempo de execução do serviço, etc.

1. Clique em **Avançar**. (Se você experimentar atrasos incomuns ao instalar o kit de ferramentas, certifique-se de que a opção **Contatar todos os sites de atualização durante a instalação para encontrar o software necessário** está desmarcada.)

1. No diálogo **Instalar Detalhes**, clique em **Avançar**.
   
   ![Revisão dos detalhes de instalação][03]

1. No diálogo **Examinar Licenças** , leia os termos dos contratos de licença. Se você aceitar os termos dos contratos de licença, clique em **Aceito os termos dos contratos de licença** e clique em **Concluir**. (As etapas restantes supõem que você aceite os termos dos contratos de licença. Se você não aceitar os termos dos contratos de licença, saia do processo de instalação.)
   
   ![Examinar Licenças][04]
   
   O Eclipse baixará e instalará os pacotes necessários.
   
   ![Progresso da Instalação][05]

1. Se for solicitado a reiniciar o Eclipse para concluir a instalação, clique em **Sim**.
   
   ![Reinicie o prompt][06]

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
