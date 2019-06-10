---
title: Java Flight Recorder e Mission Control
description: Orientação para usar o Java Flight Recorder e o Mission Control para coletar e examinar os dados de aplicativo.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: b27e0f741f1322b7e8e1df363dbb2f40a3d34d53
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568559"
---
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a>Usando o JFR (Java Flight Recorder) e o Mission Control

O Zulu Mission Control é um build totalmente testado do JDK Mission Control, que foi tornado software livre pela Oracle em 2018 e é gerenciado como um projeto sob o contexto do OpenJDK. Junto com o Flight Recorder, o Mission Control oferece funcionalidades de gerenciamento e de monitoramento interativos de baixa sobrecarga para cargas de trabalho Java.

O Zulu Mission Control é compatível com os seguintes JDKs/JREs:

* Zulu 12.1 e posteriores
* Zulu 11.0 e posteriores
* Zulu 8u202 (8.36) e posteriores
* Oracle OpenJDK 11+15 e posteriores
* Oracle Java 11.0 e posteriores
* Oracle Java 8.0 e posteriores

Siga as etapas abaixo para instalar o Zulu Mission Control, conectar-se a uma JVM (Máquina Virtual Java) e obter visibilidade em tempo real de todos os aspectos de um aplicativo em execução.

1.  [Instalar um JDK/JRE compatível com Zulu Mission Control](java-jdk-install.md).

2.  Baixe o Zulu Mission Control do [site de download da Azul](https://www.azul.com/products/zulu-mission-control/), escolha a versão apropriada para seu sistema, salve-o localmente e altere para o respectivo diretório.

3.  Expanda o arquivo baixado.

    **Linux:**

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    **Windows:**

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    **MacOS:**

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

4.  Inicie seu aplicativo Java usando um dos JDKs compatíveis. Por exemplo:

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  Iniciar o Zulu Mission Control

    **Linux:**

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    **Windows:**

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    **MacOS:**

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

6.  Alternar a instalação da JVM para Mission Control (opcional)

    No Windows, *zmc.exe* usará a instalação da JVM padrão configurada no Registro. O Zulu Mission Control deve ser iniciado de um JDK completo para conseguir detectar instâncias locais da JVM automaticamente. Se esse for um JRE, você verá o aviso abaixo:

    > [!div class="mx-imgBorder"]
    ![Aviso se a instalação do JDK for somente para JRE](../media/jdk/azul-jfr-1.png)

    Para alterar a JVM usada pelo Mission Control, siga estas etapas: 
    1.  Abra o arquivo de configuração *zmc.ini*, localizado no mesmo diretório que o *zmc.exe*
    2.  Antes da linha `-vmargs`, adicione duas linhas:
        * Na primeira linha, escreva `–vm`
        * Na segunda linha, escreva o caminho para a instalação do JDK. (Por exemplo, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).

7.  Localize a JVM que está executando seu aplicativo
    1.  No painel superior esquerdo da janela de Zulu Mission Control, clique na guia rotulada **Navegador da JVM**.
    2.  Selecione e expanda o item de lista no canto superior esquerdo para a instância da JVM que está executando seu aplicativo.

    > [!div class="mx-imgBorder"]
    ![Expanda o item de lista no canto superior esquerdo para sua instância da JVM](../media/jdk/azul-jfr-2.png)


8.  Inicie uma Gravação de Voo, se necessário
    1.  Se o Flight Recorder exibe "Nenhuma Gravação", inicie uma clicando com o botão direito do mouse na linha do Flight Recorder na guia Navegador da JVM e selecionando **Iniciar Gravação de Voo...**
    2.  Selecione uma gravação de duração fixa ou uma gravação contínua e uma configuração de Criação de Perfil (refinada) ou uma configuração Contínua (sobrecarga mais baixa) e clique em **Concluir**.

    > [!div class="mx-imgBorder"]
    ![Iniciar uma Gravação de Voo](../media/jdk/azul-jfr-3.png)

9.  Despejar a Gravação de Voo
    1.  Uma gravação de voo deve aparecer embaixo da linha do Flight Recorder no navegador da JVM. Clique com o botão direito do mouse na linha que representa a Gravação de Voo e selecione **Despejar toda a gravação**.
    2.  Uma nova guia será exibida no painel grande à direita da janela do Zulu Mission Control. Esse painel representa a gravação de voo que acaba de ser despejada da JVM que está executando seu aplicativo.

10. Examinar a gravação de voo usando o Zulu Mission Control
    1.  Se ainda não estiver ativada, selecione a guia rotulada **Estrutura de tópicos** no painel esquerdo da Janela do Zulu Mission Control. Essa guia contém diferentes exibições dos dados coletados na Gravação de Voo.
 
    > [!div class="mx-imgBorder"]
    ![Examinar a Gravação de Voo](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>Recursos

Também preparamos uma [demonstração em vídeo](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) narrada pelo diretor executivo interino de tecnologia da Azul Systems. O vídeo explica a configuração e a instalação do Flight Recorder Voo e do Zulu Mission Control. A discussão sobre o Flight Recorder começa em 31:30.

