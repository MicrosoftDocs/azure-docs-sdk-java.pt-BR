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
ms.openlocfilehash: 924ccf9bdaad4bc635f133adbcfcc8f797d06644
ms.sourcegitcommit: acc83bb537d77568b2a5427479d6354d6ae30885
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2017
ms.locfileid: "23982158"
---
# <a name="release-notes"></a><span data-ttu-id="51edd-104">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="51edd-104">Release Notes</span></span> 

## <a name="october-5-2017---130"></a><span data-ttu-id="51edd-105">5 de outubro de 2017 - 1.3.0</span><span class="sxs-lookup"><span data-stu-id="51edd-105">October 5, 2017 - 1.3.0</span></span> 

<span data-ttu-id="51edd-106">A versão 1.3.0 é compatível com versões anteriores para serviços e uso de recursos que atingiram o estágio de disponibilidade geral (estável) em versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="51edd-106">Version 1.3.0 is backwards compatible with previous versions for services and features use that reached the general availability (stable) stage in previous releases.</span></span>

<span data-ttu-id="51edd-107">As alterações de última hora de versões de visualização para esses serviços são marcadas com a anotação @Beta.</span><span class="sxs-lookup"><span data-stu-id="51edd-107">Any breaking changes from Preview versions for those services are marked with the @Beta annotation.</span></span>

<span data-ttu-id="51edd-108">Se você estiver migrando seu código para a versão 1.3.0, pode usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) para preparar o seu código existente para a versão 1.3.</span><span class="sxs-lookup"><span data-stu-id="51edd-108">If you are migrating your code to 1.3.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) to prepare your existing code for the 1.3 version.</span></span>

### <a name="generally-availabile-in-v13"></a><span data-ttu-id="51edd-109">Geralmente disponível na V1.3</span><span class="sxs-lookup"><span data-stu-id="51edd-109">Generally availabile in V1.3</span></span>

<span data-ttu-id="51edd-110">Algumas das APIs que ainda estavam em versões Beta anteriores estão agora na fase de Disponibilidade Geral (GA), em particular:</span><span class="sxs-lookup"><span data-stu-id="51edd-110">Some of the APIs that were still in Beta in previous releases are now GA, in particular:</span></span>

- <span data-ttu-id="51edd-111">métodos assíncronos</span><span class="sxs-lookup"><span data-stu-id="51edd-111">async methods</span></span>
- <span data-ttu-id="51edd-112">todos os métodos na CDN que estavam anteriormente na versão Beta</span><span class="sxs-lookup"><span data-stu-id="51edd-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="51edd-113">todos os métodos e interfaces no Gateway de Aplicativo que estavam anteriormente em versão Beta</span><span class="sxs-lookup"><span data-stu-id="51edd-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="51edd-114">Algumas partes da biblioteca ainda estão em Versão Prévia.</span><span class="sxs-lookup"><span data-stu-id="51edd-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="51edd-115">Consulte a tabela abaixo para saber o estado atual das bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="51edd-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="51edd-116">Serviço ou recurso</span><span class="sxs-lookup"><span data-stu-id="51edd-116">Service or feature</span></span> | <span data-ttu-id="51edd-117">Disponível como Disponibilidade Geral (GA)</span><span class="sxs-lookup"><span data-stu-id="51edd-117">Available as GA</span></span> | <span data-ttu-id="51edd-118">Disponível como versão prévia</span><span class="sxs-lookup"><span data-stu-id="51edd-118">Available as Preview</span></span> 
---------|---------|---------|-
<span data-ttu-id="51edd-119">Computação</span><span class="sxs-lookup"><span data-stu-id="51edd-119">Compute</span></span>  | <span data-ttu-id="51edd-120">Máquinas virtuais e extensões de VM, conjuntos de dimensionamento de máquina virtual, discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="51edd-120">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="51edd-121">Serviço de contêiner do Azure, registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="51edd-121">Azure container service, Azure container registry</span></span> 
<span data-ttu-id="51edd-122">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="51edd-122">Storage</span></span>   |  <span data-ttu-id="51edd-123">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="51edd-123">Storage accounts</span></span>       |    <span data-ttu-id="51edd-124">Criptografia</span><span class="sxs-lookup"><span data-stu-id="51edd-124">Encryption</span></span>     
<span data-ttu-id="51edd-125">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="51edd-125">SQL Database</span></span>  | <span data-ttu-id="51edd-126">Bancos de dados, firewalls, pools elásticos</span><span class="sxs-lookup"><span data-stu-id="51edd-126">Databases, firewalls, elastic pools</span></span>              
<span data-ttu-id="51edd-127">Rede</span><span class="sxs-lookup"><span data-stu-id="51edd-127">Networking</span></span>    |  <span data-ttu-id="51edd-128">Redes virtuais, interfaces de rede, endereços IP, tabelas de roteamento, grupos de segurança de rede, DNS, gerenciadores de tráfego, gateways de aplicativo</span><span class="sxs-lookup"><span data-stu-id="51edd-128">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="51edd-129">Balanceadores de carga, Emparelhamento de rede, Gateway de Rede Virtual, Inspetores de rede</span><span class="sxs-lookup"><span data-stu-id="51edd-129">Load balancers, Network peering, Virtual Network Gateway, Network watchers</span></span> 
<span data-ttu-id="51edd-130">Mais serviços</span><span class="sxs-lookup"><span data-stu-id="51edd-130">More services</span></span>    |  <span data-ttu-id="51edd-131">Gerenciador de Recursos, Cofre de Chaves, Redis, CDN, Lote</span><span class="sxs-lookup"><span data-stu-id="51edd-131">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="51edd-132">Aplicativos Web, Aplicativos de funções, Barramento de Serviço, Gráfico RBAC, Cosmos DB, Pesquisar</span><span class="sxs-lookup"><span data-stu-id="51edd-132">Web apps, Function apps, Service Bus, Graph RBAC, Cosmos DB, Search</span></span>  
<span data-ttu-id="51edd-133">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="51edd-133">Fundamentals</span></span>     |   <span data-ttu-id="51edd-134">Autenticação - núcleo, métodos assíncronos, identidade de serviço gerenciado</span><span class="sxs-lookup"><span data-stu-id="51edd-134">Authentication - core , Async methods , Managed Service Identity</span></span>      |      |

> <span data-ttu-id="51edd-135">Os recursos de visualização são marcados com uma anotação `@Beta` no nível de classe, interface ou método em bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="51edd-135">Preview features are marked with a `@Beta` annotation at the class or interface or method level in libraries.</span></span> <span data-ttu-id="51edd-136">Esses recursos estão sujeitos a alterações.</span><span class="sxs-lookup"><span data-stu-id="51edd-136">These features are subject to change.</span></span> <span data-ttu-id="51edd-137">Eles podem ser modificados de alguma forma, ou até mesmo removidos, no futuro.</span><span class="sxs-lookup"><span data-stu-id="51edd-137">They can be modified in any way, or even removed, in the future.</span></span>

### <a name="import-with-maven"></a><span data-ttu-id="51edd-138">Importar com Maven</span><span class="sxs-lookup"><span data-stu-id="51edd-138">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="51edd-139">Obter ajuda e fazer comentários</span><span class="sxs-lookup"><span data-stu-id="51edd-139">Get help and give feedback</span></span>

<span data-ttu-id="51edd-140">Confira a comunidade de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obter ajuda usando as bibliotecas em seu próprio código.</span><span class="sxs-lookup"><span data-stu-id="51edd-140">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="51edd-141">Se você encontrar quaisquer bugs ou tiver sugestões para melhorar essas bibliotecas, arquive todas as questões através do [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="51edd-141">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>


