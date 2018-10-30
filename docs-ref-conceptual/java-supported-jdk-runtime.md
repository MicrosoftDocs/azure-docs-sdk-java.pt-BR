---
title: JDKs do Java e suporte de longo prazo para desenvolvimento do Azure
description: Downloads e instrução de suporte do Azure para desenvolver e executar aplicativos Java.
author: rloutlaw
manager: angerobe
ms.devlang: java
ms.topic: article
ms.date: 10/15/2017
ms.author: routlaw
ms.openlocfilehash: 2865219f350990e8b07f7d2cd99f536168a6b8d4
ms.sourcegitcommit: 7df2d442ad7cbdb235e5dd35302a9b73379c23d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50026992"
---
# <a name="get-java-jdk-downloads-and-support-when-developing-for-azure"></a>Obtenha downloads do JDK do Java e suporte ao desenvolver para o Azure

Desenvolvedores de Java no Azure e Azure Stack podem compilar e executar aplicativos Java de produção usando [builds da Azul Systems Zulu Enterprise do OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) sem incorrer em custos adicionais de suporte. É possível usar qualquer tempo de execução do Java que desejar no Azure, mas quando usa o Zulu você recebe atualizações de manutenção gratuitas e pode criar suporte para problemas com a Microsoft com um [plano de suporte qualificado do Azure](https://azure.microsoft.com/support/plans/).

## <a name="supported-java-versions-and-update-schedule"></a>Versões com suporte de Java e agendamento de atualização

A Azul Systems fornecerá [builds da Zulu Enterprise do OpenJDK para o Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) com suporte completo para todas as versões com suporte de longo prazo (LTS) do Java, começando com o Java SE 7, 8 e 11. Mais informações podem ser encontradas no [comunicado à imprensa da Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).


Essas versões JDK receberão atualizações de segurança e correções de bugs trimestrais, bem como atualizações e patches não planejados críticos conforme necessário.  Esse suporte inclui a portabilidade de atualizações de segurança e correções de bugs para Java 7 e 8 relatadas nas versões mais recentes do Java, como Java 11 e garante a continuidade da estabilidade e segurança de versões mais antigas do Java.  Os clientes do Azure têm direito a essas atualizações de segurança e correções de bug da plataforma sem incorrer em qualquer taxa de assinatura não planejada do Java SE. As datas de suporte para cada versão do Java SE estão destacadas na imagem abaixo.

![Linha do tempo de suporte de JDK para o Azure](media/azure-jdk-support.png)

A Azul Systems mantém um [roteiro do Java SE](https://www.azul.com/products/azul_support_roadmap/) para essas versões.

## <a name="use-for-local-development"></a>Uso para desenvolvimento local 

Os desenvolvedores podem baixar JDKs do Java para o Azure e Azure Stack no [site da Azul Systems](https://www.azul.com/downloads/azure-only/zulu/). Há downloads disponíveis para Windows, Linux e macOS. Os desenvolvedores que trabalham no Linux também podem obter pacotes por meio dos gerenciadores de pacotes [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) e [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

O suporte ao produto do Azul Zulu JDK com suporte do Azure está disponível durante o desenvolvimento para Azure ou Microsoft Azure Stack com um [plano de suporte qualificado do Azure](https://azure.microsoft.com/support/plans/).

## <a name="use-in-docker-containers"></a>Uso em contêineres do Docker

Você pode criar imagens do Docker ilimitadas usando builds da Zulu Enterprise do OpenJDK em quaisquer distribuições de sua escolha. Estão disponíveis imagens Docker do Zulu baseadas no Azul Zulu Enterprise para os JDKs do Azure no [repositório do Docker público da Microsoft](https://hub.docker.com/r/microsoft/java-jdk/). Os Dockerfiles que são usados para criar essas imagens estão disponíveis no [repositório GitHub do Java da Microsoft](https://github.com/Microsoft/java/tree/master/docker).

Para colocar seus aplicativos em contêineres usando essas imagens, você precisará definir uma instrução `FROM` em seu Dockerfile e, em seguida, configurar o contêiner com as dependências do aplicativo. Por exemplo, executar o aplicativo do Java SE empacotado com o arquivo JAR vinculado à porta 8080:

```Dockerfile
FROM  microsoft/java-jdk:<tag>
EXPOSE 8080
ADD target/hello.jar hello.jar
ENTRYPOINT ["java", "-jar","/hello.jar"]
```

## <a name="azure-service-runtime-support"></a>Suporte de tempo de execução do serviço do Azure

Serviços da plataforma do Azure, como [Serviço de Aplicativo](/azure/app-service/containers/), [Functions](/azure/azure-functions/functions-create-first-java-maven), [Service Fabric](/azure/service-fabric/) e [HDInsight](/azure/hdinsight/) utilizam builds da Zulu Enterprise do OpenJDK com aplicação de patch automática incorporada de versões secundárias do Java com patches de segurança e correções de bugs.