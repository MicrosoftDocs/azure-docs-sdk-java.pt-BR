---
title: Java Flight Recorder e Mission Control
description: Orientação para usar o Java Flight Recorder e o Mission Control para coletar e examinar os dados de aplicativo.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 64f64f2e5891fccf9d62510f39bd99d73457d590
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533629"
---
# <a name="use-java-flight-recorder-and-mission-control"></a>Usar o Java Flight Recorder e o Mission Control

O Zulu Mission Control é um build totalmente testado do JDK Mission Control, que passou a ser open-source pela Oracle em 2018 e é gerenciado como um projeto na família do OpenJDK. Combinado com o JFR (Java Flight Recorder), o Mission Control oferece funcionalidades de gerenciamento e monitoramento interativos de baixa sobrecarga para cargas de trabalho Java.

O Zulu Mission Control é compatível com os seguintes JDKs (Java Development Kit) e JREs (Java Runtime Environment):

* Zulu 12.1 e posteriores
* Zulu 11.0 e posteriores
* Zulu 8u202 (8.36) e posteriores
* Oracle OpenJDK 11 e 15 e posterior
* Oracle Java 11.0 e posteriores
* Oracle Java 8.0 e posteriores

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a>Instalar o Zulu Mission Control e conectá-lo a uma JVM

Para instalar o Zulu Mission Control, conecte-se a uma JVM (Máquina Virtual Java) e obtenha visibilidade em tempo real de todos os aspectos de um aplicativo em execução fazendo o seguinte:

1.  [Instale um JDK e um JRE compatível com o Zulu Mission Control](java-jdk-install.md).

1.  [Baixe o Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), escolha a versão apropriada para seu sistema, salve-o localmente e altere-o para esse diretório.

1.  Expanda o arquivo baixado.

    **Linux:**

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    **Windows:**

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    **macOS:**

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  Inicie o aplicativo Java usando um dos JDKs compatíveis. Por exemplo:

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  Inicie o Zulu Mission Control.

    **Linux:**

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    **Windows:**

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    **macOS:**

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  (Opcional) Alterne a instalação da JVM para o Mission Control.

    Em dispositivos Windows, *zmc.exe* usa a instalação padrão da JVM configurada no Registro. O Zulu Mission Control deve ser iniciado de um JDK completo para conseguir detectar instâncias locais da JVM automaticamente. Se a instalação for um JRE, nenhuma JVM será detectada e você receberá o seguinte aviso:

    > [!div class="mx-imgBorder"]
    ![Aviso se a instalação do JDK for somente para JRE](../media/jdk/azul-jfr-1.png)

    Para alterar a JVM usada pelo Mission Control, faça o seguinte: 

    a. Abra o arquivo de configuração *zmc.ini*, localizado no mesmo diretório do *zmc.exe*.

    b. Antes da linha `-vmargs`, adicione duas linhas:  

       * Na primeira linha, insira `–vm`.  
       * Na segunda linha, insira o caminho para a instalação do JDK (por exemplo, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).

1.  Localize a JVM que está executando o aplicativo fazendo o seguinte:

    a. No painel esquerdo da janela do Zulu Mission Control, selecione a guia **Navegador da JVM**.

    b. Na lista, selecione e expanda a instância da JVM que está executando o aplicativo.

    ![A instância da JVM na lista expandida](../media/jdk/azul-jfr-2.png)


1.  Inicie uma gravação de versão piloto, se necessário.

    a. No painel esquerdo, em **Flight Recorder**, se a mensagem *Sem Gravações* for exibida, inicie uma gravação clicando com o botão direito do mouse em **Flight Recorder** e, em seguida, selecionando **Iniciar Gravação de Versão Piloto**.

    b. Selecione **Gravação de tempo fixo** ou **Gravação contínua** e uma configuração **Criação de Perfil** (refinada) ou uma configuração **Contínua** (sobrecarga mais baixa) e, em seguida, selecione **Concluir**.

    ![Iniciar uma gravação de versão piloto](../media/jdk/azul-jfr-3.png)

    Uma gravação de versão piloto deverá ser exibida embaixo da linha **Flight Recorder** no navegador da JVM.

1. Despeje a gravação de versão piloto. Para fazer isso, clique com o botão direito do mouse na linha que representa a gravação de versão piloto e, em seguida, selecione **Despejar toda a gravação**.

    Uma nova guia será exibida no painel grande, no lado direito da janela do Zulu Mission Control. Esse painel representa a gravação de versão piloto recém-despejada da JVM que está executando o aplicativo.

1. Examine a gravação de versão piloto usando o Zulu Mission Control. Para fazer isso, selecione a guia **Estrutura do Código** no painel esquerdo da janela do Zulu Mission Control. Essa guia mostra várias exibições dos dados que são coletados na gravação de versão piloto.
 
    ![Examinar a gravação de versão piloto](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>Recursos

Para saber mais, acesse o site da Azul Systems e exiba [Webinar da Azul: Flight Recorder e Mission Control de software livre – Como gerenciar e medir o desempenho do OpenJDK 8](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/). O vídeo é narrado pelo CTO Adjunto da Azul Systems, Simon Ritter. A discussão sobre o Flight Recorder começa em 31:30.

