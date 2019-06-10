---
title: Instalar o JDK do Azul Zulu para o Azure e o Azure Stack
description: Como instalar os JDKs (Kits de Desenvolvimento Java) do Azul Zulu para desenvolvimento no Azure com Windows, Linux e Mac
author: erickson-doug
manager: douge
ms.author: douge
ms.date: 4/19/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 33d2206f9a0a1cc9fadc60b17c1a93f66c592fe3
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568589"
---
# <a name="install-the-jdk-for-azure-and-azure-stack"></a><span data-ttu-id="33d86-103">Instalar o JDK para o Azure e o Azure Stack</span><span class="sxs-lookup"><span data-stu-id="33d86-103">Install the JDK for Azure and Azure Stack</span></span>

<span data-ttu-id="33d86-104">Builds do Azul Zulu Enterprise do OpenJDK são uma distribuição sem custo, multiplataforma e pronta para produção do OpenJDK para Azure e Azure Stack da Microsoft e da Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="33d86-104">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="33d86-105">Eles contêm todos os componentes para criar e executar aplicativos Java SE.</span><span class="sxs-lookup"><span data-stu-id="33d86-105">They contain all the components for building and running Java SE applications.</span></span>

<span data-ttu-id="33d86-106">Há [suporte para vários tipos de pacote de download para cada sistema operacional cliente](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="33d86-106">There are [multiple download package types supported for each client OS](https://www.azul.com/downloads/azure-only/zulu/).</span></span> <span data-ttu-id="33d86-107">Você também pode obter uma imagem de máquina virtual da Galeria do Azure Marketplace para as seguintes plataformas:</span><span class="sxs-lookup"><span data-stu-id="33d86-107">You can also get a virtual machine image from the Azure Marketplace Gallery for the following platforms:</span></span>

  * [<span data-ttu-id="33d86-108">Azul Zulu: Java 8 no Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="33d86-108">Azul Zulu: Java 8 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [<span data-ttu-id="33d86-109">Azul Zulu: Java 8 no Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="33d86-109">Azul Zulu: Java 8 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [<span data-ttu-id="33d86-110">Azul Zulu: Java 11 no Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="33d86-110">Azul Zulu: Java 11 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [<span data-ttu-id="33d86-111">Azul Zulu: Java 11 no Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="33d86-111">Azul Zulu: Java 11 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> <span data-ttu-id="33d86-112">Estas instruções destinam-se à versão Java 8 de 64 bits do JDK.</span><span class="sxs-lookup"><span data-stu-id="33d86-112">These instructions target the 64-bit Java 8 version of the JDK.</span></span> <span data-ttu-id="33d86-113">A Azul também fornece o JRE (Java Runtime Environment) como uma instalação autônoma.</span><span class="sxs-lookup"><span data-stu-id="33d86-113">Azul also provides the Java Run-time Environment (JRE) as a stand-alone installation.</span></span> <span data-ttu-id="33d86-114">O JRE está incluído com a instalação do JDK.</span><span class="sxs-lookup"><span data-stu-id="33d86-114">The JRE is included with the JDK install.</span></span>
>
>  <span data-ttu-id="33d86-115">Os pacotes Java 11 também são fornecidos na [página de downloads do Azure do Azul](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="33d86-115">Java 11 packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a><span data-ttu-id="33d86-116">Baixar e instalar os Azul Zulu JDKs para Windows</span><span class="sxs-lookup"><span data-stu-id="33d86-116">Download and install the Azul Zulu JDKs for Windows</span></span> 

1. <span data-ttu-id="33d86-117">[Baixe o JDK 8 de 64 bits Azul Zulu como um MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) para um local no seu cliente, como `C:\Users\<your_login>\Downloads`.</span><span class="sxs-lookup"><span data-stu-id="33d86-117">[Download the 64-bit Azul Zulu JDK 8 as an MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) to a location on your client, such as `C:\Users\<your_login>\Downloads`.</span></span> <span data-ttu-id="33d86-118">(Os pacotes .ZIP também são fornecidos na [página de downloads do Azure do Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="33d86-118">(.ZIP packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="33d86-119">Navegue até o diretório e clique duas vezes no arquivo MSI baixado para iniciar a instalação.</span><span class="sxs-lookup"><span data-stu-id="33d86-119">Navigate to the directory and double-click the downloaded MSI file to begin installation.</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a><span data-ttu-id="33d86-120">Baixar e instalar o Azul Zulu JDKs para Mac</span><span class="sxs-lookup"><span data-stu-id="33d86-120">Download and install the Azul Zulu JDKs for Mac</span></span> 

<span data-ttu-id="33d86-121">Estas etapas baixam um arquivo ZIP para o Mac.</span><span class="sxs-lookup"><span data-stu-id="33d86-121">These steps download a ZIP file to your Mac.</span></span> <span data-ttu-id="33d86-122">Também há uma versão DMG disponível.</span><span class="sxs-lookup"><span data-stu-id="33d86-122">There is also a DMG version available.</span></span>

1. <span data-ttu-id="33d86-123">[Baixe o JDK 8 de 64 bits Azul Zulu como um arquivo ZIP](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) para um local no seu cliente, como `/Library/Java/JavaVirtualMachines/`.</span><span class="sxs-lookup"><span data-stu-id="33d86-123">[Download the 64-bit Azul Zulu JDK 8 as a ZIP file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) to a location on your client, such as `/Library/Java/JavaVirtualMachines/`.</span></span> <span data-ttu-id="33d86-124">(Os pacotes .DMG também são fornecidos na [página de downloads do Azure do Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="33d86-124">(.DMG packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="33d86-125">Inicie o Localizador, navegue até o diretório de downloads e clique duas vezes no arquivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="33d86-125">Launch Finder, navigate to the download directory, and double-click the ZIP file.</span></span> <span data-ttu-id="33d86-126">Como alternativa, inicie uma janela de comando do terminal, navegue até o diretório e execute:</span><span class="sxs-lookup"><span data-stu-id="33d86-126">Alternatively, you can launch a terminal command window, navigate to the directory, and run:</span></span>

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a><span data-ttu-id="33d86-127">Baixar e instalar o Azul Zulu JDKs para Alpine Linux</span><span class="sxs-lookup"><span data-stu-id="33d86-127">Download and install the Azul Zulu JDKs for Alpine Linux</span></span>

1. <span data-ttu-id="33d86-128">[Baixe o JDK 8 de 64 bits Azul Zulu como um arquivo TAR](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) para um local no seu cliente, como `/usr/lib/jvm`.</span><span class="sxs-lookup"><span data-stu-id="33d86-128">[Download the 64-bit Azul Zulu JDK 8 as a TAR file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) to a location on your client, such as `/usr/lib/jvm`.</span></span> <span data-ttu-id="33d86-129">(Os pacotes .RPM e .DEB também são fornecidos na [página de downloads do Azure do Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="33d86-129">(.RPM and .DEB packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="33d86-130">Vá para seu diretório e execute o seguinte comando para descompactar e expandir o arquivo:</span><span class="sxs-lookup"><span data-stu-id="33d86-130">Go to your directory and run the following command to unzip and expand the file:</span></span>

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a><span data-ttu-id="33d86-131">Confirmar sua instalação</span><span class="sxs-lookup"><span data-stu-id="33d86-131">Confirm your installation</span></span>

<span data-ttu-id="33d86-132">Para confirmar sua instalação, vá para a linha de comando e execute `java -version`.</span><span class="sxs-lookup"><span data-stu-id="33d86-132">To confirm your installation, go to the command-line and run `java -version`.</span></span>

<span data-ttu-id="33d86-133">A saída do comando deve ser:</span><span class="sxs-lookup"><span data-stu-id="33d86-133">The output of the command should be:</span></span>

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a><span data-ttu-id="33d86-134">Baixar e instalar os JDKs do Azul Zulu de um repositório Yum</span><span class="sxs-lookup"><span data-stu-id="33d86-134">Download and install the Azul Zulu JDKs from a Yum repository</span></span>

<span data-ttu-id="33d86-135">Os JDKs do Azul Zulu são fornecidos em um [repositório Yum](http://repos.azul.com/azure-only/zulu-azure.repo) pela Azul.</span><span class="sxs-lookup"><span data-stu-id="33d86-135">The Azul Zulu JDKs are provided in a [Yum repository](http://repos.azul.com/azure-only/zulu-azure.repo) by Azul.</span></span>

<span data-ttu-id="33d86-136">**Para instalar o JDK do Azul Zulu para Java 8, execute os seguintes comandos da sua CLI:**</span><span class="sxs-lookup"><span data-stu-id="33d86-136">**To install the Azul Zulu JDK for Java 8, run the following commands from your CLI:**</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="33d86-137">Para Java 11, execute:</span><span class="sxs-lookup"><span data-stu-id="33d86-137">For Java 11, run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

<span data-ttu-id="33d86-138">Para Java 12 (Versão Prévia), execute:</span><span class="sxs-lookup"><span data-stu-id="33d86-138">For Java 12 (Preview), run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

<span data-ttu-id="33d86-139">**Para atualizar um pacote do Zulu JDK 8 de um repositório Yum:**</span><span class="sxs-lookup"><span data-stu-id="33d86-139">**To update a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="33d86-140">(Altere o número de versão no comando acima se você estiver usando a versão 11 ou 12.)</span><span class="sxs-lookup"><span data-stu-id="33d86-140">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="33d86-141">**Para remover um pacote do Zulu JDK 8 de um repositório Yum:**</span><span class="sxs-lookup"><span data-stu-id="33d86-141">**To remove a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -y erase zulu-8-azure-jdk
```
<span data-ttu-id="33d86-142">(Altere o número de versão no comando acima se você estiver usando a versão 11 ou 12.)</span><span class="sxs-lookup"><span data-stu-id="33d86-142">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a><span data-ttu-id="33d86-143">Baixar e instalar os JDKs do Azul Zulu de um repositório apt-get</span><span class="sxs-lookup"><span data-stu-id="33d86-143">Download and install the Azul Zulu JDKs from an apt-get repository</span></span>

<span data-ttu-id="33d86-144">Os JDKs do Azul Zulu também são fornecidos em um [repositório apt-get](http://repos.azul.com/azure-only/zulu/apt) pela Azul.</span><span class="sxs-lookup"><span data-stu-id="33d86-144">The Azul Zulu JDKs are also provided in an [apt-get repository](http://repos.azul.com/azure-only/zulu/apt) by Azul.</span></span>

<span data-ttu-id="33d86-145">**Para instalar o JDK do Azul Zulu para Java 8 com apt-get, execute os seguintes comandos da sua CLI:**</span><span class="sxs-lookup"><span data-stu-id="33d86-145">**To install the Azul Zulu JDK for Java 8 with apt-get, run the following commands from your CLI:**</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="33d86-146">Para Java 11, execute:</span><span class="sxs-lookup"><span data-stu-id="33d86-146">For Java 11, run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

<span data-ttu-id="33d86-147">Para Java 12 (Versão Prévia), execute:</span><span class="sxs-lookup"><span data-stu-id="33d86-147">For Java 12 (Preview), run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

<span data-ttu-id="33d86-148">**Para atualizar um pacote do Zulu JDK 8 de um repositório apt-get:**</span><span class="sxs-lookup"><span data-stu-id="33d86-148">**To update a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="33d86-149">A versão anterior será removida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="33d86-149">The previous release will be automatically removed.</span></span>
<span data-ttu-id="33d86-150">(Altere o número de versão no comando acima se você estiver usando a versão 11 ou 12.)</span><span class="sxs-lookup"><span data-stu-id="33d86-150">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="33d86-151">**Para remover um pacote do Zulu JDK 8 de um repositório apt-get:**</span><span class="sxs-lookup"><span data-stu-id="33d86-151">**To remove a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

<span data-ttu-id="33d86-152">(Altere o número de versão no comando acima se você estiver usando a versão 11 ou 12.)</span><span class="sxs-lookup"><span data-stu-id="33d86-152">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="33d86-153">Para obter mais diretrizes sobre como preparar, instalar e gerenciar seus JDKs do Azul Zulu para o desenvolvimento do Azure, leia os [documentos oficiais do Zulu](https://docs.azul.com/zulu/zuludocs/index.htm).</span><span class="sxs-lookup"><span data-stu-id="33d86-153">For more detailed guidance on preparing, installing, and managing your Azul Zulu JDKs for Azure development, read [the official Zulu docs](https://docs.azul.com/zulu/zuludocs/index.htm).</span></span>

