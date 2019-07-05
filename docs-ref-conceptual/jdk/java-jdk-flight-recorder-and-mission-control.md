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
# <a name="use-java-flight-recorder-and-mission-control"></a><span data-ttu-id="7a474-103">Usar o Java Flight Recorder e o Mission Control</span><span class="sxs-lookup"><span data-stu-id="7a474-103">Use Java Flight Recorder and Mission Control</span></span>

<span data-ttu-id="7a474-104">O Zulu Mission Control é um build totalmente testado do JDK Mission Control, que passou a ser open-source pela Oracle em 2018 e é gerenciado como um projeto na família do OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="7a474-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open-sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="7a474-105">Combinado com o JFR (Java Flight Recorder), o Mission Control oferece funcionalidades de gerenciamento e monitoramento interativos de baixa sobrecarga para cargas de trabalho Java.</span><span class="sxs-lookup"><span data-stu-id="7a474-105">Coupled with Java Flight Recorder (JFR), Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="7a474-106">O Zulu Mission Control é compatível com os seguintes JDKs (Java Development Kit) e JREs (Java Runtime Environment):</span><span class="sxs-lookup"><span data-stu-id="7a474-106">Zulu Mission Control is compatible with the following Java Development Kits (JDKs) and Java Runtime Environments (JREs):</span></span>

* <span data-ttu-id="7a474-107">Zulu 12.1 e posteriores</span><span class="sxs-lookup"><span data-stu-id="7a474-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="7a474-108">Zulu 11.0 e posteriores</span><span class="sxs-lookup"><span data-stu-id="7a474-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="7a474-109">Zulu 8u202 (8.36) e posteriores</span><span class="sxs-lookup"><span data-stu-id="7a474-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="7a474-110">Oracle OpenJDK 11 e 15 e posterior</span><span class="sxs-lookup"><span data-stu-id="7a474-110">Oracle OpenJDK 11 and 15 and later</span></span>
* <span data-ttu-id="7a474-111">Oracle Java 11.0 e posteriores</span><span class="sxs-lookup"><span data-stu-id="7a474-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="7a474-112">Oracle Java 8.0 e posteriores</span><span class="sxs-lookup"><span data-stu-id="7a474-112">Oracle Java 8.0 and later</span></span>

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a><span data-ttu-id="7a474-113">Instalar o Zulu Mission Control e conectá-lo a uma JVM</span><span class="sxs-lookup"><span data-stu-id="7a474-113">Install Zulu Mission Control and connect to a JVM</span></span>

<span data-ttu-id="7a474-114">Para instalar o Zulu Mission Control, conecte-se a uma JVM (Máquina Virtual Java) e obtenha visibilidade em tempo real de todos os aspectos de um aplicativo em execução fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a474-114">To install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application, do the following:</span></span>

1.  <span data-ttu-id="7a474-115">[Instale um JDK e um JRE compatível com o Zulu Mission Control](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="7a474-115">[Install a Zulu Mission Control-compatible JDK and JRE](java-jdk-install.md).</span></span>

1.  <span data-ttu-id="7a474-116">[Baixe o Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), escolha a versão apropriada para seu sistema, salve-o localmente e altere-o para esse diretório.</span><span class="sxs-lookup"><span data-stu-id="7a474-116">[Download Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

1.  <span data-ttu-id="7a474-117">Expanda o arquivo baixado.</span><span class="sxs-lookup"><span data-stu-id="7a474-117">Expand the downloaded file.</span></span>

    <span data-ttu-id="7a474-118">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="7a474-118">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="7a474-119">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="7a474-119">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="7a474-120">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="7a474-120">**macOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  <span data-ttu-id="7a474-121">Inicie o aplicativo Java usando um dos JDKs compatíveis.</span><span class="sxs-lookup"><span data-stu-id="7a474-121">Start your Java application by using one of the compatible JDKs.</span></span> <span data-ttu-id="7a474-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7a474-122">For example:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  <span data-ttu-id="7a474-123">Inicie o Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="7a474-123">Start Zulu Mission Control.</span></span>

    <span data-ttu-id="7a474-124">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="7a474-124">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="7a474-125">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="7a474-125">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="7a474-126">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="7a474-126">**macOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  <span data-ttu-id="7a474-127">(Opcional) Alterne a instalação da JVM para o Mission Control.</span><span class="sxs-lookup"><span data-stu-id="7a474-127">(Optional) Switch the JVM installation for Mission Control.</span></span>

    <span data-ttu-id="7a474-128">Em dispositivos Windows, *zmc.exe* usa a instalação padrão da JVM configurada no Registro.</span><span class="sxs-lookup"><span data-stu-id="7a474-128">On Windows devices, *zmc.exe* uses the default JVM installation that's configured in the registry.</span></span> <span data-ttu-id="7a474-129">O Zulu Mission Control deve ser iniciado de um JDK completo para conseguir detectar instâncias locais da JVM automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7a474-129">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="7a474-130">Se a instalação for um JRE, nenhuma JVM será detectada e você receberá o seguinte aviso:</span><span class="sxs-lookup"><span data-stu-id="7a474-130">If the installation is a JRE, no JVM will be detected, and you will receive the following warning:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="7a474-131">![Aviso se a instalação do JDK for somente para JRE](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="7a474-131">![Warning if JDK installation is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="7a474-132">Para alterar a JVM usada pelo Mission Control, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a474-132">To change the JVM that's used by Mission Control, do the following:</span></span> 

    <span data-ttu-id="7a474-133">a.</span><span class="sxs-lookup"><span data-stu-id="7a474-133">a.</span></span> <span data-ttu-id="7a474-134">Abra o arquivo de configuração *zmc.ini*, localizado no mesmo diretório do *zmc.exe*.</span><span class="sxs-lookup"><span data-stu-id="7a474-134">Open the *zmc.ini* configuration file, which is in the same directory as the *zmc.exe* file.</span></span>

    <span data-ttu-id="7a474-135">b.</span><span class="sxs-lookup"><span data-stu-id="7a474-135">b.</span></span> <span data-ttu-id="7a474-136">Antes da linha `-vmargs`, adicione duas linhas:</span><span class="sxs-lookup"><span data-stu-id="7a474-136">Before the line `-vmargs`, add two lines:</span></span>  

       * <span data-ttu-id="7a474-137">Na primeira linha, insira `–vm`.</span><span class="sxs-lookup"><span data-stu-id="7a474-137">On the first line, enter `–vm`.</span></span>  
       * <span data-ttu-id="7a474-138">Na segunda linha, insira o caminho para a instalação do JDK (por exemplo, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="7a474-138">On the second line, enter the path to your JDK installation (for example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

1.  <span data-ttu-id="7a474-139">Localize a JVM que está executando o aplicativo fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a474-139">Locate the JVM that's running your application by doing the following:</span></span>

    <span data-ttu-id="7a474-140">a.</span><span class="sxs-lookup"><span data-stu-id="7a474-140">a.</span></span> <span data-ttu-id="7a474-141">No painel esquerdo da janela do Zulu Mission Control, selecione a guia **Navegador da JVM**.</span><span class="sxs-lookup"><span data-stu-id="7a474-141">In the left pane of the Zulu Mission Control window, select the **JVM Browser** tab.</span></span>

    <span data-ttu-id="7a474-142">b.</span><span class="sxs-lookup"><span data-stu-id="7a474-142">b.</span></span> <span data-ttu-id="7a474-143">Na lista, selecione e expanda a instância da JVM que está executando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7a474-143">In the list, select and expand the JVM instance that's running your application.</span></span>

    ![A instância da JVM na lista expandida](../media/jdk/azul-jfr-2.png)


1.  <span data-ttu-id="7a474-145">Inicie uma gravação de versão piloto, se necessário.</span><span class="sxs-lookup"><span data-stu-id="7a474-145">Start a flight recording, if necessary.</span></span>

    <span data-ttu-id="7a474-146">a.</span><span class="sxs-lookup"><span data-stu-id="7a474-146">a.</span></span> <span data-ttu-id="7a474-147">No painel esquerdo, em **Flight Recorder**, se a mensagem *Sem Gravações* for exibida, inicie uma gravação clicando com o botão direito do mouse em **Flight Recorder** e, em seguida, selecionando **Iniciar Gravação de Versão Piloto**.</span><span class="sxs-lookup"><span data-stu-id="7a474-147">In the left pane, under **Flight Recorder**, if a *No Recordings* message is displayed, start a recording by right-clicking **Flight Recorder** and then selecting **Start Flight Recording**.</span></span>

    <span data-ttu-id="7a474-148">b.</span><span class="sxs-lookup"><span data-stu-id="7a474-148">b.</span></span> <span data-ttu-id="7a474-149">Selecione **Gravação de tempo fixo** ou **Gravação contínua** e uma configuração **Criação de Perfil** (refinada) ou uma configuração **Contínua** (sobrecarga mais baixa) e, em seguida, selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="7a474-149">Select either **Time fixed recording** or **Continuous recording**, and either a **Profiling** configuration (fine-grained) or a **Continuous** configuration (lower overhead), and then select **Finish**.</span></span>

    ![Iniciar uma gravação de versão piloto](../media/jdk/azul-jfr-3.png)

    <span data-ttu-id="7a474-151">Uma gravação de versão piloto deverá ser exibida embaixo da linha **Flight Recorder** no navegador da JVM.</span><span class="sxs-lookup"><span data-stu-id="7a474-151">A flight recording should appear below the **Flight Recorder** line in the JVM browser.</span></span>

1. <span data-ttu-id="7a474-152">Despeje a gravação de versão piloto.</span><span class="sxs-lookup"><span data-stu-id="7a474-152">Dump the flight recording.</span></span> <span data-ttu-id="7a474-153">Para fazer isso, clique com o botão direito do mouse na linha que representa a gravação de versão piloto e, em seguida, selecione **Despejar toda a gravação**.</span><span class="sxs-lookup"><span data-stu-id="7a474-153">To do so, right-click the line that represents the flight recording, and then select **Dump whole recording**.</span></span>

    <span data-ttu-id="7a474-154">Uma nova guia será exibida no painel grande, no lado direito da janela do Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="7a474-154">A new tab appears in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="7a474-155">Esse painel representa a gravação de versão piloto recém-despejada da JVM que está executando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7a474-155">This pane represents the flight recording that was just dumped from the JVM that's running your application.</span></span>

1. <span data-ttu-id="7a474-156">Examine a gravação de versão piloto usando o Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="7a474-156">Examine the flight recording by using Zulu Mission Control.</span></span> <span data-ttu-id="7a474-157">Para fazer isso, selecione a guia **Estrutura do Código** no painel esquerdo da janela do Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="7a474-157">To do so, select the **Outline** tab in the left pane of the Zulu Mission Control window.</span></span> <span data-ttu-id="7a474-158">Essa guia mostra várias exibições dos dados que são coletados na gravação de versão piloto.</span><span class="sxs-lookup"><span data-stu-id="7a474-158">This tab displays various views of the data that's collected in the flight recording.</span></span>
 
    ![Examinar a gravação de versão piloto](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a><span data-ttu-id="7a474-160">Recursos</span><span class="sxs-lookup"><span data-stu-id="7a474-160">Resources</span></span>

<span data-ttu-id="7a474-161">Para saber mais, acesse o site da Azul Systems e exiba [Webinar da Azul: Flight Recorder e Mission Control de software livre – Como gerenciar e medir o desempenho do OpenJDK 8](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/).</span><span class="sxs-lookup"><span data-stu-id="7a474-161">To learn more, go to the Azul Systems site and view [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/).</span></span> <span data-ttu-id="7a474-162">O vídeo é narrado pelo CTO Adjunto da Azul Systems, Simon Ritter.</span><span class="sxs-lookup"><span data-stu-id="7a474-162">The video is narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="7a474-163">A discussão sobre o Flight Recorder começa em 31:30.</span><span class="sxs-lookup"><span data-stu-id="7a474-163">The Flight Recorder discussion starts at 31:30.</span></span>

