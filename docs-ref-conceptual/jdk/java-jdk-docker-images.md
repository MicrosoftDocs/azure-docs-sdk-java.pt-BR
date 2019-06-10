---
title: Usar imagens do Docker com um JDK para desenvolvimento em Java do Azure
description: ''
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: ee8df2a08b23d090965cb42e2c15b934d4785e7c
ms.sourcegitcommit: 03379369346974c6e80f86e7129b885112b5c1a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910235"
---
# <a name="use-docker-with-a-jdk-for-azure"></a><span data-ttu-id="f5864-102">Usar o Docker com um JDK para o Azure</span><span class="sxs-lookup"><span data-stu-id="f5864-102">Use Docker with a JDK for Azure</span></span> 

<span data-ttu-id="f5864-103">Imagens do Docker criadas previamente para Java 7, 8 e 11 estão disponíveis por meio do [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span><span class="sxs-lookup"><span data-stu-id="f5864-103">Pre-built Docker images for Java 7, 8, and 11 are available through [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span></span>

<span data-ttu-id="f5864-104">Imagens de contêiner do Docker certificadas para o JDK do Zulu, o JRE e o JRE sem periféricos em várias imagens de SO base estão disponíveis no Docker Hub:</span><span class="sxs-lookup"><span data-stu-id="f5864-104">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker Hub:</span></span>

* [<span data-ttu-id="f5864-105">JDK</span><span class="sxs-lookup"><span data-stu-id="f5864-105">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
* [<span data-ttu-id="f5864-106">JRE</span><span class="sxs-lookup"><span data-stu-id="f5864-106">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
* [<span data-ttu-id="f5864-107">JRE sem periféricos</span><span class="sxs-lookup"><span data-stu-id="f5864-107">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

## <a name="running-a-docker-image"></a><span data-ttu-id="f5864-108">Como executar uma imagem do Docker</span><span class="sxs-lookup"><span data-stu-id="f5864-108">Running a Docker image</span></span>

<span data-ttu-id="f5864-109">Imagens do Docker podem ser executadas usando a sintaxe `$ docker run mcr.microsoft.com/java/jdk:tag java`, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f5864-109">Docker images can be run using the syntax `$ docker run mcr.microsoft.com/java/jdk:tag java` as shown in the following example.</span></span>

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a><span data-ttu-id="f5864-110">Como criar uma imagem do Docker</span><span class="sxs-lookup"><span data-stu-id="f5864-110">Creating a Docker image</span></span>

<span data-ttu-id="f5864-111">Você pode criar uma imagem usando imagens do Docker Hub oficiais da Microsoft, conforme mostrado nos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="f5864-111">You can create an image using Microsoft's official Docker Hub images as shown in the following examples.</span></span>

### <a name="create-a-docker-file"></a><span data-ttu-id="f5864-112">Crie uma imagem do Docker</span><span class="sxs-lookup"><span data-stu-id="f5864-112">Create a Docker file</span></span>

```cli
FROM mcr.microsoft.com/java/jdk:8u212-zulu-alpine 
  
RUN echo $' \
  
public class HelloWorld { \
   public static void main(String[] args) { \
      // Prints "Hello, World" in the terminal window. \
      System.out.println("Hello, World - From Microsoft Azure !!!"); \
   } \
}' > HelloWorld.java
  
RUN javac HelloWorld.java
  
CMD ["java", "HelloWorld"]
```

### <a name="build-a-docker-image"></a><span data-ttu-id="f5864-113">Compilar uma imagem do docker</span><span class="sxs-lookup"><span data-stu-id="f5864-113">Build a Docker image</span></span>

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a><span data-ttu-id="f5864-114">Executar a nova imagem</span><span class="sxs-lookup"><span data-stu-id="f5864-114">Run the new image</span></span>

```cli
docker run hello-world
```

<span data-ttu-id="f5864-115">Você verá esta saída:</span><span class="sxs-lookup"><span data-stu-id="f5864-115">You will see the following output:</span></span>

```output
Hello World - From Microsoft Azure !!!
```
