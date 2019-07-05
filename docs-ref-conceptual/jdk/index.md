---
title: JDKs do Java e suporte de longo prazo para desenvolvimento do Azure
description: Este artigo apresenta links de download e uma declaração do Suporte do Azure para desenvolvimento e execução de aplicativos Java.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 1bb93f775686b5b0f127c586dda802f4eb5f775d
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533634"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a>Suporte de longo prazo do Java para o Azure e o Azure Stack

Como desenvolvedor de Java no Microsoft Azure e no Azure Stack, você pode compilar e executar aplicativos Java de produção usando o [Azul Zulu Enterprise para Azure](https://www.azul.com/downloads/azure-only/zulu/) sem gerar custos adicionais de suporte. Você pode usar qualquer tempo de execução do Java desejado no Azure, mas ao usar o Zulu, você obtém atualizações de manutenção gratuitas e pode resolver problemas de suporte com a Microsoft.

> [!div class="nextstepaction"]
> [Baixar e Instalar Java](java-jdk-install.md)

## <a name="long-term-support"></a>Suporte de longo prazo

* [Java 11](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [Java 7](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a>Visualização técnica

* [Java 12](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a>O que é o Zulu OpenJDK para o Azure?

Os builds do OpenJDK do Azul Zulu Enterprise são uma distribuição sem nenhum custo, multiplataforma e pronta para produção do OpenJDK para Azure e Azure Stack com suporte da Microsoft e da Azul Systems. Essas distribuições são:

* Builds 100% open-source do OpenJDK empacotados como JDKs (Java Development Kit), JREs (Java Runtime Environment) e JREs sem periféricos. Esses binários são totalmente compatíveis e estão em conformidade com builds comerciais do Java SE (Standard Edition) que podem ser usados com aplicativos Java ou componentes no Azure e no Azure Stack.
* Fornecidas com LTS (suporte de longo prazo), que inclui correções de bug, melhorias de desempenho e patches de segurança.
* Disponíveis para desenvolvimento e execução de aplicativos Java no Windows, no Linux e no macOS.
* Disponíveis como imagens de contêiner no Docker Hub e como máquinas virtuais (Windows e Linux) no Azure Marketplace.
* Usadas pelo Azure para ativar muitos serviços do Azure, como:
  * Serviço de Aplicativo do Azure (Windows)
  * Serviço de Aplicativo do Azure (Linux)
  * Funções do Azure
  * Azure Service Fabric
  * Azure HDInsight
  * Azure Search
  * Azure DevOps
  * Azure Cloud Shell  

## <a name="supported-java-versions-and-update-schedule"></a>Versões com suporte de Java e agendamento de atualização

A Azul Systems fornece [builds do OpenJDK para Azure do Zulu Enterprise](https://www.azul.com/downloads/azure-only/zulu/) com suporte completo para todas as versões LTS do Java, no Java SE 7, 8 e 11. Para obter mais informações, confira o [comunicado à imprensa da Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).

|Java SE LTS  |Suporte até  |
|---------|----------|
|[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7) |Julho de 2023 |
|[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8) |Março de 2025|
|[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11) |Setembro de 2026|
|[![Java 12](../media/jdk/java-12.png)]() |**Visualização**|

Essas versões do JDK têm atualizações de segurança trimestrais, correções de bugs e atualizações e patches não planejados críticos conforme necessário. Esse suporte inclui backports de atualizações de segurança e correções de bug para Java 7 e 8 que são relatadas em versões mais recentes do Java, como Java 11. O suporte garante a estabilidade e a segurança contínuas de versões mais antigas do Java. Os clientes do Azure podem obter essas atualizações de segurança e correções de bug da plataforma sem incorrer em nenhuma taxa de assinatura não planejada do Java SE.

A Azul Systems mantém um [roteiro do Java SE](https://www.azul.com/products/azul_support_roadmap/) para essas versões.

## <a name="benefits-for-developers"></a>Benefícios para os desenvolvedores

As versões do Azul Zulu JDK são:

* Compatíveis com a Microsoft e a Azul Systems, tendo o suporte delas.

   * Os binários do Zulu estão prontos para produção e têm o suporte da Microsoft e da Azul Systems.
   * O Zulu é fornecido com LTS sem nenhum custo para o Java 7, 8 e 11 (o LTS também será fornecido para o Java 17). Você pode atualizar versões do Java somente quando você precisa.
   * Há suporte para o Java 7 até julho de 2023. Os Java 8 e 11 terão suporte além de 2024.
   * A Microsoft está comprometida a executar o Zulu internamente em computadores que potencializam muitos serviços do Azure.

* Pronto para produção.

   * 100% open-source para seus builds do OpenJDK.
   * Substituições prontas para muitas distribuições do Java SE.
   * JDK, JRE e JRE sem periféricos.
   * Java 7, 8 e 11.
   * Em conformidade verificada com as especificações do Java SE que usam o TCK (Kit de Compatibilidade de Tecnologia) da Comunidade do OpenJDK.
   * Como desenvolvedor, você continuará recebendo atualizações de produção para o Java SE, incluindo correções de bug, melhorias de desempenho e patches de segurança para o Java SE 7, 8 e 11.

* Compatíveis com multiplataforma. O Zulu é compatível com binários para várias plataformas e versões, incluindo:

   * Windows Client
     * 10
     * 8.1
     * 8, 7
   * Windows Server
     * 2016 R2
     * 2016
     * 2012 R2
     * 2012
     * 2008 R2
   * Linux, incluindo
     * RHEL
     * CentOS
     * Ubuntu
     * SLES
     * Debian
     * Oracle Linux
   * macOS X
   * Entrega em vários tipos de pacotes:
     * MSI, ZIP, TAR, DEB, RPM e DMG

    Imagens de contêiner do Docker certificadas para o Zulu JDK, JRE e JRE sem periféricos em várias imagens de SO base estão disponíveis no Docker.

    Hub:

    * [JDK](https://hub.docker.com/_/microsoft-java-jdk)
    * [JRE](https://hub.docker.com/_/microsoft-java-jre)
    * [JRE sem periféricos](https://hub.docker.com/_/microsoft-java-jre-headless)

* Sem custo.

   * A Microsoft fornece tudo o que você precisa para criar e dimensionar aplicativos Java no Azure, sem nenhum custo para você. Por meio do Zulu, você receberá atualizações de segurança e correções de bug de plataforma gratuitas para aplicativos Java sem nenhuma taxa.
   * [O Flight Recorder Java e o Mission Control](java-jdk-flight-recorder-and-mission-control.md) estão disponíveis no Zulu Java 8, 11 e 12 (Versão Prévia).

* Disponível como uma versão prévia técnica de versões não LTS.

   * Com as versões prévias técnicas, você pode testar progressivamente novos recursos conforme eles são entregues, em versões de curto prazo que acabarão sendo atualizadas para o Java 17 LTS.

* As alterações no OpenJDK são enviadas upstream.

   * Os confirmadores da Azul Systems enviam as alterações do Zulu por push ao OpenJDK, o que torna o repositório upstream abrangente e inclusivo.

Como sempre, como desenvolvedor de Java, você pode levar ao Azure seus próprios tempos de execução de Java, incluindo o Oracle JDK e o Red Hat JDK. Você também pode usar a infraestrutura segura e os serviços repletos de recursos. A edição de produção do Oracle Java SE está disponível para você para execução de cargas de trabalho Java em máquinas virtuais do Windows ou do Linux no Azure.

## <a name="use-java-jdks-for-local-development"></a>Usar JDKs do Java para desenvolvimento local 

[Baixe os JDKs do Java para o Azure e o Azure Stack](https://www.azul.com/downloads/azure-only/zulu/) para uso nos ambientes de desenvolvimento local. Há downloads disponíveis para Windows, Linux e macOS. Se estiver trabalhando no Linux, obtenha pacotes também por meio dos gerenciadores de pacotes [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) e [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

Para obter mais diretrizes, confira [Imagens do Docker para o Azure](java-jdk-docker-images.md).
