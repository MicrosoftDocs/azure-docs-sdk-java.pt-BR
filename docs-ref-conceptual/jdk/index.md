---
title: JDKs do Java e suporte de longo prazo para desenvolvimento do Azure
description: Downloads e instrução de suporte do Azure para desenvolver e executar aplicativos Java.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 340f6149ffe39ccbb2d7de534ed63b8784d1f63a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270880"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="f83bc-103">Suporte de longo prazo do Java para o Azure e o Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f83bc-103">Java Long-Term Support for Azure and Azure Stack</span></span>

<span data-ttu-id="f83bc-104">Os desenvolvedores de Java no Azure e Azure Stack podem compilar e executar aplicativos Java de produção usando [Azul Zulu Enterprise para Azure](https://www.azul.com/downloads/azure-only/zulu/) sem incorrer em custos adicionais de suporte.</span><span class="sxs-lookup"><span data-stu-id="f83bc-104">Java developers on Azure and Azure Stack can build and run production Java applications using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="f83bc-105">É possível usar qualquer tempo de execução do Java que desejar no Azure, mas quando você usa o Zulu, você recebe atualizações de manutenção gratuitas e pode criar problemas de suporte com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f83bc-105">You can use any Java runtime you want on Azure, but when you use Zulu you get free maintenance updates and can create support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f83bc-106">Baixar e Instalar Java</span><span class="sxs-lookup"><span data-stu-id="f83bc-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support-lts"></a><span data-ttu-id="f83bc-107">LTS (suporte de longo prazo)</span><span class="sxs-lookup"><span data-stu-id="f83bc-107">Long-term support (LTS)</span></span>

* [<span data-ttu-id="f83bc-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="f83bc-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [<span data-ttu-id="f83bc-109">Java 8</span><span class="sxs-lookup"><span data-stu-id="f83bc-109">Java 8</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [<span data-ttu-id="f83bc-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="f83bc-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="f83bc-111">Visualização técnica</span><span class="sxs-lookup"><span data-stu-id="f83bc-111">Technical preview</span></span>

* [<span data-ttu-id="f83bc-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="f83bc-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="f83bc-113">O que é o Zulu OpenJDK para o Azure?</span><span class="sxs-lookup"><span data-stu-id="f83bc-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="f83bc-114">Builds do Azul Zulu Enterprise do OpenJDK são uma distribuição sem custo, multiplataforma e pronta para produção do OpenJDK para Azure e Azure Stack da Microsoft e da Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="f83bc-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="f83bc-115">Essas distribuições são:</span><span class="sxs-lookup"><span data-stu-id="f83bc-115">These distributions are:</span></span>

* <span data-ttu-id="f83bc-116">Builds 100% software livre do OpenJDK empacotados como JDKs (Kits de Desenvolvimento Java), JRE (Java Runtime Environment) e JREs Sem Periféricos.</span><span class="sxs-lookup"><span data-stu-id="f83bc-116">100% open source builds of OpenJDK packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="f83bc-117">Esses binários são totalmente compatíveis e estão em conformidade com builds comerciais do Java SE (Standard Edition) que podem ser usados com aplicativos Java ou componentes no Azure e no Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f83bc-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="f83bc-118">Fornecidas com suporte de longo prazo, incluindo correções de bug, aprimoramentos de desempenho e patches de segurança.</span><span class="sxs-lookup"><span data-stu-id="f83bc-118">Provided with long-term support including bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="f83bc-119">Disponíveis para desenvolver e executar aplicativos Java no Windows, no Linux e no MacOS.</span><span class="sxs-lookup"><span data-stu-id="f83bc-119">Available for developing and running Java applications on Windows, Linux, and MacOS.</span></span>
* <span data-ttu-id="f83bc-120">Disponíveis como imagens de contêiner no Docker Hub e máquinas virtuais (Windows e Linux) no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f83bc-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) on Azure Marketplace.</span></span>
* <span data-ttu-id="f83bc-121">Usadas pelo Microsoft Azure para potencializar muitos serviços do Azure, como:</span><span class="sxs-lookup"><span data-stu-id="f83bc-121">Used by Microsoft Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="f83bc-122">Serviço de Aplicativo Windows</span><span class="sxs-lookup"><span data-stu-id="f83bc-122">App Service Windows</span></span>
  * <span data-ttu-id="f83bc-123">Serviço de Aplicativo Linux</span><span class="sxs-lookup"><span data-stu-id="f83bc-123">App Service Linux</span></span>
  * <span data-ttu-id="f83bc-124">Funções</span><span class="sxs-lookup"><span data-stu-id="f83bc-124">Functions</span></span>
  * <span data-ttu-id="f83bc-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f83bc-125">Service Fabric</span></span>
  * <span data-ttu-id="f83bc-126">HDInsight</span><span class="sxs-lookup"><span data-stu-id="f83bc-126">HDInsight</span></span>
  * <span data-ttu-id="f83bc-127">Search</span><span class="sxs-lookup"><span data-stu-id="f83bc-127">Search</span></span>
  * <span data-ttu-id="f83bc-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="f83bc-128">Azure DevOps</span></span>
  * <span data-ttu-id="f83bc-129">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="f83bc-129">Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="f83bc-130">Versões com suporte de Java e agendamento de atualização</span><span class="sxs-lookup"><span data-stu-id="f83bc-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="f83bc-131">A Azul Systems fornece [builds da Zulu Enterprise do OpenJDK para o Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) com suporte completo para todas as versões com LTS (suporte de longo prazo) do Java, começando com o Java SE 7, 8 e 11.</span><span class="sxs-lookup"><span data-stu-id="f83bc-131">Azul Systems provides fully-supported [Zulu Enterprise builds of OpenJDK for Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) for all long-term support (LTS) versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="f83bc-132">Mais informações podem ser encontradas no [comunicado à imprensa da Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="f83bc-132">More information can be found in the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="f83bc-133">Java SE LTS</span><span class="sxs-lookup"><span data-stu-id="f83bc-133">Java SE LTS</span></span>  |<span data-ttu-id="f83bc-134">Suporte até</span><span class="sxs-lookup"><span data-stu-id="f83bc-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="f83bc-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="f83bc-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="f83bc-136">Julho de 2023</span><span class="sxs-lookup"><span data-stu-id="f83bc-136">July 2023</span></span> |
|<span data-ttu-id="f83bc-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="f83bc-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="f83bc-138">Março de 2025</span><span class="sxs-lookup"><span data-stu-id="f83bc-138">March 2025</span></span>|
|<span data-ttu-id="f83bc-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="f83bc-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="f83bc-140">Setembro de 2026</span><span class="sxs-lookup"><span data-stu-id="f83bc-140">Sept. 2026</span></span>|
|<span data-ttu-id="f83bc-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="f83bc-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="f83bc-142">**VERSÃO PRÉVIA**</span><span class="sxs-lookup"><span data-stu-id="f83bc-142">**PREVIEW**</span></span>|

<span data-ttu-id="f83bc-143">Essas versões do JDK têm atualizações de segurança trimestrais, correções de bugs e atualizações e patches não planejados críticos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f83bc-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span>  <span data-ttu-id="f83bc-144">Esse suporte inclui a portabilidade de atualizações de segurança e correções de bugs para Java 7 e 8 relatadas nas versões mais recentes do Java, como Java 11, o que garante a estabilidade e a segurança contínuas de versões mais antigas do Java.</span><span class="sxs-lookup"><span data-stu-id="f83bc-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 reported in newer versions of Java such as Java 11, which ensures the continued stability and security of older versions of Java.</span></span>  <span data-ttu-id="f83bc-145">Os clientes do Azure podem obter essas atualizações de segurança e correções de bug da plataforma sem incorrer em nenhuma taxa de assinatura não planejada do Java SE.</span><span class="sxs-lookup"><span data-stu-id="f83bc-145">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="f83bc-146">A Azul Systems mantém um [roteiro do Java SE](https://www.azul.com/products/azul_support_roadmap/) para essas versões.</span><span class="sxs-lookup"><span data-stu-id="f83bc-146">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="f83bc-147">Benefícios para os desenvolvedores</span><span class="sxs-lookup"><span data-stu-id="f83bc-147">Benefits for developers</span></span>

<span data-ttu-id="f83bc-148">As versões do Azul Zulu JDK são:</span><span class="sxs-lookup"><span data-stu-id="f83bc-148">The Azul Zulu JDK releases are:</span></span>

1. <span data-ttu-id="f83bc-149">Compatíveis com a Microsoft e a Azul Systems</span><span class="sxs-lookup"><span data-stu-id="f83bc-149">Backed and supported by both Microsoft and Azul Systems</span></span>

   * <span data-ttu-id="f83bc-150">Os binários do Zulu estão prontos para produção e têm o suporte da Microsoft e da Azul Systems</span><span class="sxs-lookup"><span data-stu-id="f83bc-150">Zulu binaries are production-ready and backed by Microsoft and Azul Systems</span></span>
   * <span data-ttu-id="f83bc-151">O Zulu vem com LTS (suporte de longo prazo) sem custo nenhum para Java 7, 8 e 11.</span><span class="sxs-lookup"><span data-stu-id="f83bc-151">Zulu comes with zero-cost long-term support (LTS) for Java 7, 8, and 11.</span></span> <span data-ttu-id="f83bc-152">(LTS será fornecido para Java 17 também.)</span><span class="sxs-lookup"><span data-stu-id="f83bc-152">(LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="f83bc-153">Você pode atualizar versões do Java somente quando você precisa.</span><span class="sxs-lookup"><span data-stu-id="f83bc-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="f83bc-154">O Java 7 terá suporte até julho de 2023.</span><span class="sxs-lookup"><span data-stu-id="f83bc-154">Java 7 supported until July 2023.</span></span> <span data-ttu-id="f83bc-155">Os Java 8 e 11 terão suporte além de 2024.</span><span class="sxs-lookup"><span data-stu-id="f83bc-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="f83bc-156">A Microsoft está comprometida a executar o Zulu internamente em computadores que potencializam muitos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="f83bc-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

2. <span data-ttu-id="f83bc-157">Prontas para produção</span><span class="sxs-lookup"><span data-stu-id="f83bc-157">Production-ready</span></span>

   * <span data-ttu-id="f83bc-158">100% open-source para seus builds do OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f83bc-158">100% open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="f83bc-159">Substituições prontas para muitas distribuições do Java SE.</span><span class="sxs-lookup"><span data-stu-id="f83bc-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="f83bc-160">JDK, JRE e JRE sem periféricos</span><span class="sxs-lookup"><span data-stu-id="f83bc-160">JDK, JRE, and JRE-headless</span></span>
   * <span data-ttu-id="f83bc-161">Java 7, 8 e 11</span><span class="sxs-lookup"><span data-stu-id="f83bc-161">Java 7, 8, and 11</span></span>
   * <span data-ttu-id="f83bc-162">Em conformidade verificada com as especificações de Java SE usando o TCK (Kit de Compatibilidade de Tecnologia) da Comunidade do OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f83bc-162">Verified compliant with the Java SE  specifications using the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="f83bc-163">Os desenvolvedores continuarão a receber atualizações de produção para Java SE, incluindo correções de bugs, aprimoramentos de desempenho e patches de segurança para Java SE 7, 8 e 11.</span><span class="sxs-lookup"><span data-stu-id="f83bc-163">Developers will continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

3. <span data-ttu-id="f83bc-164">Compatíveis com multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="f83bc-164">Supported for multi-platform.</span></span> <span data-ttu-id="f83bc-165">O Zulu é compatível com binários para várias plataformas e versões, incluindo:</span><span class="sxs-lookup"><span data-stu-id="f83bc-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="f83bc-166">Windows Client</span><span class="sxs-lookup"><span data-stu-id="f83bc-166">Windows Client</span></span>
     * <span data-ttu-id="f83bc-167">10</span><span class="sxs-lookup"><span data-stu-id="f83bc-167">10</span></span>
     * <span data-ttu-id="f83bc-168">8.1</span><span class="sxs-lookup"><span data-stu-id="f83bc-168">8.1</span></span>
     * <span data-ttu-id="f83bc-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="f83bc-169">8, 7</span></span>
   * <span data-ttu-id="f83bc-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="f83bc-170">Windows Server</span></span>
     * <span data-ttu-id="f83bc-171">2016R2</span><span class="sxs-lookup"><span data-stu-id="f83bc-171">2016R2</span></span>
     * <span data-ttu-id="f83bc-172">2016</span><span class="sxs-lookup"><span data-stu-id="f83bc-172">2016</span></span>
     * <span data-ttu-id="f83bc-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="f83bc-173">2012 R2</span></span>
     * <span data-ttu-id="f83bc-174">2012</span><span class="sxs-lookup"><span data-stu-id="f83bc-174">2012</span></span>
     * <span data-ttu-id="f83bc-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="f83bc-175">2008 R2</span></span>
   * <span data-ttu-id="f83bc-176">Linux, incluindo</span><span class="sxs-lookup"><span data-stu-id="f83bc-176">Linux, including</span></span>
     * <span data-ttu-id="f83bc-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="f83bc-177">RHEL</span></span>
     * <span data-ttu-id="f83bc-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="f83bc-178">CentOS</span></span>
     * <span data-ttu-id="f83bc-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f83bc-179">Ubuntu</span></span>
     * <span data-ttu-id="f83bc-180">SLES</span><span class="sxs-lookup"><span data-stu-id="f83bc-180">SLES</span></span>
     * <span data-ttu-id="f83bc-181">Debian</span><span class="sxs-lookup"><span data-stu-id="f83bc-181">Debian</span></span>
     * <span data-ttu-id="f83bc-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="f83bc-182">Oracle Linux</span></span>
   * <span data-ttu-id="f83bc-183">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="f83bc-183">Mac OS X</span></span>
   * <span data-ttu-id="f83bc-184">entregue em vários tipos de pacote:</span><span class="sxs-lookup"><span data-stu-id="f83bc-184">delivered in multiple package types:</span></span>
     * <span data-ttu-id="f83bc-185">MSI, ZIP, TAR, DEB, RPM e DMG</span><span class="sxs-lookup"><span data-stu-id="f83bc-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="f83bc-186">Imagens de contêiner do Docker certificadas para o Zulu JDK, JRE e JRE sem periféricos em várias imagens de SO base estão disponíveis no Docker.</span><span class="sxs-lookup"><span data-stu-id="f83bc-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="f83bc-187">Hub:</span><span class="sxs-lookup"><span data-stu-id="f83bc-187">Hub:</span></span>

    * [<span data-ttu-id="f83bc-188">JDK</span><span class="sxs-lookup"><span data-stu-id="f83bc-188">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
    * [<span data-ttu-id="f83bc-189">JRE</span><span class="sxs-lookup"><span data-stu-id="f83bc-189">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
    * [<span data-ttu-id="f83bc-190">JRE sem periféricos</span><span class="sxs-lookup"><span data-stu-id="f83bc-190">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

4. <span data-ttu-id="f83bc-191">Sem custo</span><span class="sxs-lookup"><span data-stu-id="f83bc-191">No cost</span></span>

   * <span data-ttu-id="f83bc-192">A Microsoft fornece tudo de que você precisa para compilar e dimensionar aplicativos Java no Azure sem custo para você.</span><span class="sxs-lookup"><span data-stu-id="f83bc-192">Microsoft provides everything you need to build and scale Java apps on Azure at no cost to you.</span></span> <span data-ttu-id="f83bc-193">Por meio do Zulu, você receberá atualizações de segurança e correções de bug de plataforma gratuitas para aplicativos Java sem nenhuma taxa.</span><span class="sxs-lookup"><span data-stu-id="f83bc-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="f83bc-194">[O Flight Recorder Java e o Mission Control](java-jdk-flight-recorder-and-mission-control.md) estão disponíveis no Zulu Java 8, 11 e 12 (Versão Prévia).</span><span class="sxs-lookup"><span data-stu-id="f83bc-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

5. <span data-ttu-id="f83bc-195">Visualização técnica de versões não LTS</span><span class="sxs-lookup"><span data-stu-id="f83bc-195">Tech Preview of Non-LTS versions</span></span>

   * <span data-ttu-id="f83bc-196">Visualizações técnicas dão oportunidades para testar progressivamente novos recursos conforme eles são entregues em versões de curto prazo que acabarão passando para Java 17 LTS.</span><span class="sxs-lookup"><span data-stu-id="f83bc-196">Tech previews provide you with opportunities to progressively test new features as they are delivered in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

6. <span data-ttu-id="f83bc-197">As alterações do OpenJDK são transmitidas para cima</span><span class="sxs-lookup"><span data-stu-id="f83bc-197">Changes to OpenJDK are up-streamed</span></span>

   * <span data-ttu-id="f83bc-198">Os confirmadores da Azul Systems enviam por push as alterações do OpenJDK ao Zulu, o que torna o repositório upstream abrangente e inclusivo.</span><span class="sxs-lookup"><span data-stu-id="f83bc-198">Azul Systems committers push Zulu changes to OpenJDK which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="f83bc-199">Como sempre, os desenvolvedores Java podem trazer seus próprios tempos de execução Java, incluindo o Oracle JDK e o Red Hat JDK, para o Azure e usar a infraestrutura segura e os serviços repletos de recursos.</span><span class="sxs-lookup"><span data-stu-id="f83bc-199">As always, Java developers can bring their own Java run-times, including Oracle JDK and Red Hat JDK, to Azure and use  the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="f83bc-200">A edição de produção do Oracle Java SE também está disponível para desenvolvedores de Java executando cargas de trabalho Java nas máquinas virtuais do Linux ou do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="f83bc-200">The production edition of Oracle Java SE is also available to Java developers for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-for-local-development"></a><span data-ttu-id="f83bc-201">Uso para desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="f83bc-201">Use for local development</span></span> 

<span data-ttu-id="f83bc-202">Os desenvolvedores podem [baixar](https://www.azul.com/downloads/azure-only/zulu/) os JDKs do Java para o Azure e o Azure Stack para uso nos ambientes de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f83bc-202">Developers can [download](https://www.azul.com/downloads/azure-only/zulu/) Java JDKs for Azure and Azure Stack for use in local development environments.</span></span> <span data-ttu-id="f83bc-203">Há downloads disponíveis para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="f83bc-203">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f83bc-204">Os desenvolvedores que trabalham no Linux também podem obter pacotes por meio dos gerenciadores de pacotes [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) e [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).</span><span class="sxs-lookup"><span data-stu-id="f83bc-204">Developers working on Linux can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="f83bc-205">Para obter outras diretrizes, confira [Imagens do Docker para Azure](java-jdk-docker-images.md).</span><span class="sxs-lookup"><span data-stu-id="f83bc-205">For additional guidance see [Docker images for Azure](java-jdk-docker-images.md).</span></span>