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
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a><span data-ttu-id="9cb42-103">Usando o JFR (Java Flight Recorder) e o Mission Control</span><span class="sxs-lookup"><span data-stu-id="9cb42-103">Using Java Flight Recorder (JFR) and Mission Control</span></span>

<span data-ttu-id="9cb42-104">O Zulu Mission Control é um build totalmente testado do JDK Mission Control, que foi tornado software livre pela Oracle em 2018 e é gerenciado como um projeto sob o contexto do OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="9cb42-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="9cb42-105">Junto com o Flight Recorder, o Mission Control oferece funcionalidades de gerenciamento e de monitoramento interativos de baixa sobrecarga para cargas de trabalho Java.</span><span class="sxs-lookup"><span data-stu-id="9cb42-105">Coupled with Flight Recorder, Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="9cb42-106">O Zulu Mission Control é compatível com os seguintes JDKs/JREs:</span><span class="sxs-lookup"><span data-stu-id="9cb42-106">Zulu Mission Control is compatible with the following JDKs/JREs:</span></span>

* <span data-ttu-id="9cb42-107">Zulu 12.1 e posteriores</span><span class="sxs-lookup"><span data-stu-id="9cb42-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="9cb42-108">Zulu 11.0 e posteriores</span><span class="sxs-lookup"><span data-stu-id="9cb42-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="9cb42-109">Zulu 8u202 (8.36) e posteriores</span><span class="sxs-lookup"><span data-stu-id="9cb42-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="9cb42-110">Oracle OpenJDK 11+15 e posteriores</span><span class="sxs-lookup"><span data-stu-id="9cb42-110">Oracle OpenJDK 11+15 and later</span></span>
* <span data-ttu-id="9cb42-111">Oracle Java 11.0 e posteriores</span><span class="sxs-lookup"><span data-stu-id="9cb42-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="9cb42-112">Oracle Java 8.0 e posteriores</span><span class="sxs-lookup"><span data-stu-id="9cb42-112">Oracle Java 8.0 and later</span></span>

<span data-ttu-id="9cb42-113">Siga as etapas abaixo para instalar o Zulu Mission Control, conectar-se a uma JVM (Máquina Virtual Java) e obter visibilidade em tempo real de todos os aspectos de um aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="9cb42-113">Follow the steps below to install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application.</span></span>

1.  <span data-ttu-id="9cb42-114">[Instalar um JDK/JRE compatível com Zulu Mission Control](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="9cb42-114">[Install a Zulu Mission Control compatible JDK/JRE](java-jdk-install.md).</span></span>

2.  <span data-ttu-id="9cb42-115">Baixe o Zulu Mission Control do [site de download da Azul](https://www.azul.com/products/zulu-mission-control/), escolha a versão apropriada para seu sistema, salve-o localmente e altere para o respectivo diretório.</span><span class="sxs-lookup"><span data-stu-id="9cb42-115">Download Zulu Mission Control from [the Azul download site](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

3.  <span data-ttu-id="9cb42-116">Expanda o arquivo baixado.</span><span class="sxs-lookup"><span data-stu-id="9cb42-116">Expand the downloaded file.</span></span>

    <span data-ttu-id="9cb42-117">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="9cb42-117">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="9cb42-118">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="9cb42-118">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="9cb42-119">**MacOS:**</span><span class="sxs-lookup"><span data-stu-id="9cb42-119">**MacOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

4.  <span data-ttu-id="9cb42-120">Inicie seu aplicativo Java usando um dos JDKs compatíveis.</span><span class="sxs-lookup"><span data-stu-id="9cb42-120">Start your Java application using one of the compatible JDKs.</span></span> <span data-ttu-id="9cb42-121">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9cb42-121">E.g.:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  <span data-ttu-id="9cb42-122">Iniciar o Zulu Mission Control</span><span class="sxs-lookup"><span data-stu-id="9cb42-122">Start Zulu Mission Control</span></span>

    <span data-ttu-id="9cb42-123">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="9cb42-123">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="9cb42-124">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="9cb42-124">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="9cb42-125">**MacOS:**</span><span class="sxs-lookup"><span data-stu-id="9cb42-125">**MacOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

6.  <span data-ttu-id="9cb42-126">Alternar a instalação da JVM para Mission Control (opcional)</span><span class="sxs-lookup"><span data-stu-id="9cb42-126">Switch the JVM installation for Mission Control (Optional)</span></span>

    <span data-ttu-id="9cb42-127">No Windows, *zmc.exe* usará a instalação da JVM padrão configurada no Registro.</span><span class="sxs-lookup"><span data-stu-id="9cb42-127">On Windows, *zmc.exe* will use the default JVM installation configured in the registry.</span></span> <span data-ttu-id="9cb42-128">O Zulu Mission Control deve ser iniciado de um JDK completo para conseguir detectar instâncias locais da JVM automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9cb42-128">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="9cb42-129">Se esse for um JRE, você verá o aviso abaixo:</span><span class="sxs-lookup"><span data-stu-id="9cb42-129">If this is a JRE, you will see the warning below:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="9cb42-130">![Aviso se a instalação do JDK for somente para JRE](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="9cb42-130">![Warning if JDK install is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="9cb42-131">Para alterar a JVM usada pelo Mission Control, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="9cb42-131">To change the JVM used by Mission Control, follow these steps:</span></span> 
    1.  <span data-ttu-id="9cb42-132">Abra o arquivo de configuração *zmc.ini*, localizado no mesmo diretório que o *zmc.exe*</span><span class="sxs-lookup"><span data-stu-id="9cb42-132">Open *zmc.ini* configuration file, located in the same directory as the *zmc.exe*</span></span>
    2.  <span data-ttu-id="9cb42-133">Antes da linha `-vmargs`, adicione duas linhas:</span><span class="sxs-lookup"><span data-stu-id="9cb42-133">Before the line `-vmargs`, add two lines:</span></span>
        * <span data-ttu-id="9cb42-134">Na primeira linha, escreva `–vm`</span><span class="sxs-lookup"><span data-stu-id="9cb42-134">On the first line, write `–vm`</span></span>
        * <span data-ttu-id="9cb42-135">Na segunda linha, escreva o caminho para a instalação do JDK.</span><span class="sxs-lookup"><span data-stu-id="9cb42-135">On the second line, write the path to your JDK installation.</span></span> <span data-ttu-id="9cb42-136">(Por exemplo, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="9cb42-136">(For example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

7.  <span data-ttu-id="9cb42-137">Localize a JVM que está executando seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="9cb42-137">Locate the JVM running your application</span></span>
    1.  <span data-ttu-id="9cb42-138">No painel superior esquerdo da janela de Zulu Mission Control, clique na guia rotulada **Navegador da JVM**.</span><span class="sxs-lookup"><span data-stu-id="9cb42-138">In the upper left pane of the Zulu Mission Control window click on the tab labelled **JVM Browser**.</span></span>
    2.  <span data-ttu-id="9cb42-139">Selecione e expanda o item de lista no canto superior esquerdo para a instância da JVM que está executando seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9cb42-139">Select and expand the list item in the upper left for your the JVM instance running your application.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="9cb42-140">![Expanda o item de lista no canto superior esquerdo para sua instância da JVM](../media/jdk/azul-jfr-2.png)</span><span class="sxs-lookup"><span data-stu-id="9cb42-140">![Expand the list item in the upper-left for your JVM instance](../media/jdk/azul-jfr-2.png)</span></span>


8.  <span data-ttu-id="9cb42-141">Inicie uma Gravação de Voo, se necessário</span><span class="sxs-lookup"><span data-stu-id="9cb42-141">Start a Flight Recording, if necessary</span></span>
    1.  <span data-ttu-id="9cb42-142">Se o Flight Recorder exibe "Nenhuma Gravação", inicie uma clicando com o botão direito do mouse na linha do Flight Recorder na guia Navegador da JVM e selecionando **Iniciar Gravação de Voo...**</span><span class="sxs-lookup"><span data-stu-id="9cb42-142">If the Flight Recorder displays "No Recordings", start one by right-clicking on the Flight Recorder line in the JVM Browser tab and selecting **Start Flight Recording...**</span></span>
    2.  <span data-ttu-id="9cb42-143">Selecione uma gravação de duração fixa ou uma gravação contínua e uma configuração de Criação de Perfil (refinada) ou uma configuração Contínua (sobrecarga mais baixa) e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="9cb42-143">Select either a fixed duration recording or a continuous recording, and either a Profiling configuration (fine-grained) or a Continuous configuration (lower overhead), then click **Finish**.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="9cb42-144">![Iniciar uma Gravação de Voo](../media/jdk/azul-jfr-3.png)</span><span class="sxs-lookup"><span data-stu-id="9cb42-144">![Start a Flight Recording](../media/jdk/azul-jfr-3.png)</span></span>

9.  <span data-ttu-id="9cb42-145">Despejar a Gravação de Voo</span><span class="sxs-lookup"><span data-stu-id="9cb42-145">Dump the Flight Recording</span></span>
    1.  <span data-ttu-id="9cb42-146">Uma gravação de voo deve aparecer embaixo da linha do Flight Recorder no navegador da JVM.</span><span class="sxs-lookup"><span data-stu-id="9cb42-146">A Flight Recording should appear below the Flight Recorder line in the JVM Browser.</span></span> <span data-ttu-id="9cb42-147">Clique com o botão direito do mouse na linha que representa a Gravação de Voo e selecione **Despejar toda a gravação**.</span><span class="sxs-lookup"><span data-stu-id="9cb42-147">Right-click on the line representing the Flight Recording and select **Dump whole recording**.</span></span>
    2.  <span data-ttu-id="9cb42-148">Uma nova guia será exibida no painel grande à direita da janela do Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="9cb42-148">A new tab will appear in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="9cb42-149">Esse painel representa a gravação de voo que acaba de ser despejada da JVM que está executando seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9cb42-149">This pane represents the Flight Recording just dumped from the JVM running your application.</span></span>

10. <span data-ttu-id="9cb42-150">Examinar a gravação de voo usando o Zulu Mission Control</span><span class="sxs-lookup"><span data-stu-id="9cb42-150">Examine the Flight Recording using Zulu Mission Control</span></span>
    1.  <span data-ttu-id="9cb42-151">Se ainda não estiver ativada, selecione a guia rotulada **Estrutura de tópicos** no painel esquerdo da Janela do Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="9cb42-151">If not already activated, select the tab labelled **Outline** in the left pane of the Zulu Mission Control Window.</span></span> <span data-ttu-id="9cb42-152">Essa guia contém diferentes exibições dos dados coletados na Gravação de Voo.</span><span class="sxs-lookup"><span data-stu-id="9cb42-152">This tab contains different views of the data collected in the Flight Recording.</span></span>
 
    > [!div class="mx-imgBorder"]
    <span data-ttu-id="9cb42-153">![Examinar a Gravação de Voo](../media/jdk/azul-jfr-4.png)</span><span class="sxs-lookup"><span data-stu-id="9cb42-153">![Review the Fliight Recording](../media/jdk/azul-jfr-4.png)</span></span>

## <a name="resources"></a><span data-ttu-id="9cb42-154">Recursos</span><span class="sxs-lookup"><span data-stu-id="9cb42-154">Resources</span></span>

<span data-ttu-id="9cb42-155">Também preparamos uma [demonstração em vídeo](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) narrada pelo diretor executivo interino de tecnologia da Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="9cb42-155">We have also prepared a [demonstration video](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="9cb42-156">O vídeo explica a configuração e a instalação do Flight Recorder Voo e do Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="9cb42-156">The video walks you through the configuration and setup of both Flight Recorder and Zulu Mission Control.</span></span> <span data-ttu-id="9cb42-157">A discussão sobre o Flight Recorder começa em 31:30.</span><span class="sxs-lookup"><span data-stu-id="9cb42-157">The Flight Recorder discussion starts at 31:30.</span></span>

