---
title: "Notas de versão de bibliotecas de gerenciamento do Azure para Java | Microsoft Docs"
description: "Veja o que há de novo e fique de olho em alterações significativas nas bibliotecas de gerenciamento do Azure para Java"
keywords: "Azure, Java, API, referência, anotações, atualizações, substituir, obsoleto"
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: fc246d499b2f5f20a7efbaed16c4b4193d8d8e6c
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="release-notes"></a><span data-ttu-id="a1457-104">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="a1457-104">Release Notes</span></span> 

## <a name="june-30-2017---110"></a><span data-ttu-id="a1457-105">30 de junho de 2017 - 1.1.0</span><span class="sxs-lookup"><span data-stu-id="a1457-105">June 30, 2017 - 1.1.0</span></span> 

<span data-ttu-id="a1457-106">A V1.1 é retrocompatível com a V1.0 nas APIs destinadas a uso público que atingiram o estágio de disponibilidade geral (estável) na V1.0.</span><span class="sxs-lookup"><span data-stu-id="a1457-106">V1.1 is backwards compatible with V1.0 in the APIs intended for public use that reached the general availability (stable) stage in V1.0.</span></span>

<span data-ttu-id="a1457-107">Algumas alterações foram introduzidas em APIs marcadas com a anotação @Beta na V.0</span><span class="sxs-lookup"><span data-stu-id="a1457-107">Some breaking changes were introduced in APIs marked with the @Beta annotation in V.0</span></span>

<span data-ttu-id="a1457-108">Se você estiver migrando seu código para a versão 1.1.0, você pode usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) para preparar o seu código para a versão 1.1.0 a partir da versão 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a1457-108">If you are migrating your code to 1.1.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) for preparing your code for 1.1.0 from 1.0.0.</span></span>

### <a name="generally-availabile-in-v11"></a><span data-ttu-id="a1457-109">Geralmente disponível na V1.1</span><span class="sxs-lookup"><span data-stu-id="a1457-109">Generally availabile in V1.1</span></span>

<span data-ttu-id="a1457-110">Algumas das APIs que ainda estavam em versão Beta na V1.0 estão agora na fase de Disponibilidade Geral (GA) na V1.1, em particular:</span><span class="sxs-lookup"><span data-stu-id="a1457-110">Some of the APIs that were still in Beta in V1.0 are now GA in V1.1, in particular:</span></span>

- <span data-ttu-id="a1457-111">métodos assíncronos</span><span class="sxs-lookup"><span data-stu-id="a1457-111">async methods</span></span>
- <span data-ttu-id="a1457-112">todos os métodos na CDN que estavam anteriormente na versão Beta</span><span class="sxs-lookup"><span data-stu-id="a1457-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="a1457-113">todos os métodos e interfaces no Gateway de Aplicativo que estavam anteriormente em versão Beta</span><span class="sxs-lookup"><span data-stu-id="a1457-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="a1457-114">Algumas partes da biblioteca ainda estão em Versão Prévia.</span><span class="sxs-lookup"><span data-stu-id="a1457-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="a1457-115">Consulte a tabela abaixo para saber o estado atual das bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="a1457-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="a1457-116">Serviço ou recurso</span><span class="sxs-lookup"><span data-stu-id="a1457-116">Service or feature</span></span> | <span data-ttu-id="a1457-117">Disponível como Disponibilidade Geral (GA)</span><span class="sxs-lookup"><span data-stu-id="a1457-117">Available as GA</span></span> | <span data-ttu-id="a1457-118">Disponível como Versão Prévia</span><span class="sxs-lookup"><span data-stu-id="a1457-118">Available as Preview</span></span>  | <span data-ttu-id="a1457-119">Em breve</span><span class="sxs-lookup"><span data-stu-id="a1457-119">Coming soon</span></span> |
---------|---------|---------|---------|
<span data-ttu-id="a1457-120">Computação</span><span class="sxs-lookup"><span data-stu-id="a1457-120">Compute</span></span>  | <span data-ttu-id="a1457-121">Máquinas virtuais e extensões de VM, conjuntos de dimensionamento de máquina virtual, discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="a1457-121">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="a1457-122">Serviço de contêiner do Azure, registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="a1457-122">Azure container service, Azure container registry</span></span> |    |
<span data-ttu-id="a1457-123">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="a1457-123">Storage</span></span>   |  <span data-ttu-id="a1457-124">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a1457-124">Storage accounts</span></span>       |         |   <span data-ttu-id="a1457-125">Criptografia</span><span class="sxs-lookup"><span data-stu-id="a1457-125">Encryption</span></span>      |
<span data-ttu-id="a1457-126">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="a1457-126">SQL Database</span></span>  | <span data-ttu-id="a1457-127">Bancos de dados, firewalls, pools elásticos</span><span class="sxs-lookup"><span data-stu-id="a1457-127">Databases, firewalls, elastic pools</span></span>        |         |   <span data-ttu-id="a1457-128">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="a1457-128">More features</span></span>      |
<span data-ttu-id="a1457-129">Rede</span><span class="sxs-lookup"><span data-stu-id="a1457-129">Networking</span></span>    |  <span data-ttu-id="a1457-130">Redes virtuais, interfaces de rede, endereços IP, tabelas de roteamento, grupos de segurança de rede, DNS, gerenciadores de tráfego, gateways de aplicativo</span><span class="sxs-lookup"><span data-stu-id="a1457-130">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="a1457-131">Balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="a1457-131">Load balancers</span></span>     |   <span data-ttu-id="a1457-132">VPN, observadores de rede</span><span class="sxs-lookup"><span data-stu-id="a1457-132">VPN, Network watchers</span></span>   |
<span data-ttu-id="a1457-133">Mais serviços</span><span class="sxs-lookup"><span data-stu-id="a1457-133">More services</span></span>    |  <span data-ttu-id="a1457-134">Gerenciador de Recursos, Cofre de Chaves, Redis, CDN, Lote</span><span class="sxs-lookup"><span data-stu-id="a1457-134">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="a1457-135">Aplicativos Web, Aplicativos de Funções, Barramento de Serviço, Grafo RBAC, DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a1457-135">Web apps, Function apps, Service Bus, Graph RBAC, DocumentDB</span></span>   | <span data-ttu-id="a1457-136">Monitor, Agendador, gerenciamento de Funções, Pesquisa, mais recursos do Grafo RBAC</span><span class="sxs-lookup"><span data-stu-id="a1457-136">Monitor ,Scheduler, Functions management, Search, more Graph RBAC features</span></span>        |
<span data-ttu-id="a1457-137">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="a1457-137">Fundamentals</span></span>     |   <span data-ttu-id="a1457-138">Autenticação - básica, assíncrona</span><span class="sxs-lookup"><span data-stu-id="a1457-138">Authentication - core , Async methods</span></span>       |      |         |

### <a name="import-with-maven"></a><span data-ttu-id="a1457-139">Importar com Maven</span><span class="sxs-lookup"><span data-stu-id="a1457-139">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="a1457-140">Obter ajuda e fazer comentários</span><span class="sxs-lookup"><span data-stu-id="a1457-140">Get help and give feedback</span></span>

<span data-ttu-id="a1457-141">Confira a comunidade de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obter ajuda usando as bibliotecas em seu próprio código.</span><span class="sxs-lookup"><span data-stu-id="a1457-141">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="a1457-142">Se você encontrar quaisquer bugs ou tiver sugestões para melhorar essas bibliotecas, arquive todas as questões através do [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="a1457-142">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>

### <a name="migrate-from-previous-releases"></a><span data-ttu-id="a1457-143">Migrar de versões anteriores</span><span class="sxs-lookup"><span data-stu-id="a1457-143">Migrate from previous releases</span></span>

[<span data-ttu-id="a1457-144">Migrar da versão 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [Migrar da versão 1.1.0  </span><span class="sxs-lookup"><span data-stu-id="a1457-144">Migrate from 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migrate from 1.1.0</span></span>](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)


