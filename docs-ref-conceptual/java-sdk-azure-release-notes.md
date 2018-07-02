---
title: Notas de versão de bibliotecas de gerenciamento do Azure para Java | Microsoft Docs
description: Veja o que há de novo e fique de olho em alterações significativas nas bibliotecas de gerenciamento do Azure para Java
keywords: Azure, Java, API, referência, anotações, atualizações, substituir, obsoleto
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 0aaa83ceb42192441decb5972baae56fed337fb2
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090679"
---
# <a name="release-notes"></a><span data-ttu-id="b1df6-104">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="b1df6-104">Release Notes</span></span> 

## <a name="october-5-2017---130"></a><span data-ttu-id="b1df6-105">5 de outubro de 2017 - 1.3.0</span><span class="sxs-lookup"><span data-stu-id="b1df6-105">October 5, 2017 - 1.3.0</span></span> 

<span data-ttu-id="b1df6-106">A versão 1.3.0 é compatível com versões anteriores para serviços e uso de recursos que atingiram o estágio de disponibilidade geral (estável) em versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="b1df6-106">Version 1.3.0 is backwards compatible with previous versions for services and features use that reached the general availability (stable) stage in previous releases.</span></span>

<span data-ttu-id="b1df6-107">As alterações de última hora de versões de visualização para esses serviços são marcadas com a anotação @Beta.</span><span class="sxs-lookup"><span data-stu-id="b1df6-107">Any breaking changes from Preview versions for those services are marked with the @Beta annotation.</span></span>

<span data-ttu-id="b1df6-108">Se você estiver migrando seu código para a versão 1.3.0, pode usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) para preparar o seu código existente para a versão 1.3.</span><span class="sxs-lookup"><span data-stu-id="b1df6-108">If you are migrating your code to 1.3.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) to prepare your existing code for the 1.3 version.</span></span>

### <a name="generally-availabile-in-v13"></a><span data-ttu-id="b1df6-109">Geralmente disponível na V1.3</span><span class="sxs-lookup"><span data-stu-id="b1df6-109">Generally availabile in V1.3</span></span>

<span data-ttu-id="b1df6-110">Algumas das APIs que ainda estavam em versões Beta anteriores estão agora na fase de Disponibilidade Geral (GA), em particular:</span><span class="sxs-lookup"><span data-stu-id="b1df6-110">Some of the APIs that were still in Beta in previous releases are now GA, in particular:</span></span>

- <span data-ttu-id="b1df6-111">métodos assíncronos</span><span class="sxs-lookup"><span data-stu-id="b1df6-111">async methods</span></span>
- <span data-ttu-id="b1df6-112">todos os métodos na CDN que estavam anteriormente na versão Beta</span><span class="sxs-lookup"><span data-stu-id="b1df6-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="b1df6-113">todos os métodos e interfaces no Gateway de Aplicativo que estavam anteriormente em versão Beta</span><span class="sxs-lookup"><span data-stu-id="b1df6-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

  <span data-ttu-id="b1df6-114">Algumas partes da biblioteca ainda estão em Versão Prévia.</span><span class="sxs-lookup"><span data-stu-id="b1df6-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="b1df6-115">Consulte a tabela abaixo para saber o estado atual das bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="b1df6-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="b1df6-116">Serviço ou recurso</span><span class="sxs-lookup"><span data-stu-id="b1df6-116">Service or feature</span></span> | <span data-ttu-id="b1df6-117">Disponível como Disponibilidade Geral (GA)</span><span class="sxs-lookup"><span data-stu-id="b1df6-117">Available as GA</span></span> | <span data-ttu-id="b1df6-118">Disponível como versão prévia</span><span class="sxs-lookup"><span data-stu-id="b1df6-118">Available as Preview</span></span> 
---------|---------|---------|-
<span data-ttu-id="b1df6-119">Computação</span><span class="sxs-lookup"><span data-stu-id="b1df6-119">Compute</span></span>  | <span data-ttu-id="b1df6-120">Máquinas virtuais e extensões de VM, conjuntos de dimensionamento de máquina virtual, discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="b1df6-120">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="b1df6-121">Serviço de contêiner do Azure, registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="b1df6-121">Azure container service, Azure container registry</span></span> 
<span data-ttu-id="b1df6-122">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="b1df6-122">Storage</span></span>   |  <span data-ttu-id="b1df6-123">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b1df6-123">Storage accounts</span></span>       |    <span data-ttu-id="b1df6-124">Criptografia</span><span class="sxs-lookup"><span data-stu-id="b1df6-124">Encryption</span></span>     
<span data-ttu-id="b1df6-125">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="b1df6-125">SQL Database</span></span>  | <span data-ttu-id="b1df6-126">Bancos de dados, firewalls, pools elásticos</span><span class="sxs-lookup"><span data-stu-id="b1df6-126">Databases, firewalls, elastic pools</span></span>              
<span data-ttu-id="b1df6-127">Rede</span><span class="sxs-lookup"><span data-stu-id="b1df6-127">Networking</span></span>    |  <span data-ttu-id="b1df6-128">Redes virtuais, interfaces de rede, endereços IP, tabelas de roteamento, grupos de segurança de rede, DNS, gerenciadores de tráfego, gateways de aplicativo</span><span class="sxs-lookup"><span data-stu-id="b1df6-128">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="b1df6-129">Balanceadores de carga, Emparelhamento de rede, Gateway de Rede Virtual, Inspetores de rede</span><span class="sxs-lookup"><span data-stu-id="b1df6-129">Load balancers, Network peering, Virtual Network Gateway, Network watchers</span></span> 
<span data-ttu-id="b1df6-130">Mais serviços</span><span class="sxs-lookup"><span data-stu-id="b1df6-130">More services</span></span>    |  <span data-ttu-id="b1df6-131">Gerenciador de Recursos, Cofre de Chaves, Redis, CDN, Lote</span><span class="sxs-lookup"><span data-stu-id="b1df6-131">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="b1df6-132">Aplicativos Web, Aplicativos de funções, Barramento de Serviço, Grafo RBAC, Cosmos DB, Pesquisar</span><span class="sxs-lookup"><span data-stu-id="b1df6-132">Web apps, Function apps, Service Bus, Graph RBAC, Cosmos DB, Search</span></span>  
<span data-ttu-id="b1df6-133">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="b1df6-133">Fundamentals</span></span>     |   <span data-ttu-id="b1df6-134">Autenticação - núcleo, métodos assíncronos, identidade de serviço gerenciado</span><span class="sxs-lookup"><span data-stu-id="b1df6-134">Authentication - core , Async methods , Managed Service Identity</span></span>      |      |

> <span data-ttu-id="b1df6-135">Os recursos de visualização são marcados com uma anotação `@Beta` no nível de classe, interface ou método em bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="b1df6-135">Preview features are marked with a `@Beta` annotation at the class or interface or method level in libraries.</span></span> <span data-ttu-id="b1df6-136">Esses recursos estão sujeitos a alterações.</span><span class="sxs-lookup"><span data-stu-id="b1df6-136">These features are subject to change.</span></span> <span data-ttu-id="b1df6-137">Eles podem ser modificados de alguma forma, ou até mesmo removidos, no futuro.</span><span class="sxs-lookup"><span data-stu-id="b1df6-137">They can be modified in any way, or even removed, in the future.</span></span>

### <a name="import-with-maven"></a><span data-ttu-id="b1df6-138">Importar com Maven</span><span class="sxs-lookup"><span data-stu-id="b1df6-138">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="b1df6-139">Obter ajuda e fazer comentários</span><span class="sxs-lookup"><span data-stu-id="b1df6-139">Get help and give feedback</span></span>

<span data-ttu-id="b1df6-140">Confira a comunidade de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obter ajuda usando as bibliotecas em seu próprio código.</span><span class="sxs-lookup"><span data-stu-id="b1df6-140">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="b1df6-141">Se você encontrar quaisquer bugs ou tiver sugestões para melhorar essas bibliotecas, arquive todas as questões através do [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="b1df6-141">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>


