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
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a><span data-ttu-id="1ffb9-104">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="1ffb9-104">Release Notes</span></span> 

## <a name="june-30-2017---110"></a><span data-ttu-id="1ffb9-105">30 de junho de 2017 - 1.1.0</span><span class="sxs-lookup"><span data-stu-id="1ffb9-105">June 30, 2017 - 1.1.0</span></span> 

<span data-ttu-id="1ffb9-106">A V1.1 é retrocompatível com a V1.0 nas APIs destinadas a uso público que atingiram o estágio de disponibilidade geral (estável) na V1.0.</span><span class="sxs-lookup"><span data-stu-id="1ffb9-106">V1.1 is backwards compatible with V1.0 in the APIs intended for public use that reached the general availability (stable) stage in V1.0.</span></span>

<span data-ttu-id="1ffb9-107">Algumas alterações foram introduzidas em APIs marcadas com a anotação @Beta na V.0</span><span class="sxs-lookup"><span data-stu-id="1ffb9-107">Some breaking changes were introduced in APIs marked with the @Beta annotation in V.0</span></span>

<span data-ttu-id="1ffb9-108">Se você estiver migrando seu código para a versão 1.1.0, você pode usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) para preparar o seu código para a versão 1.1.0 a partir da versão 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="1ffb9-108">If you are migrating your code to 1.1.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) for preparing your code for 1.1.0 from 1.0.0.</span></span>

### <a name="generally-availabile-in-v11"></a><span data-ttu-id="1ffb9-109">Geralmente disponível na V1.1</span><span class="sxs-lookup"><span data-stu-id="1ffb9-109">Generally availabile in V1.1</span></span>

<span data-ttu-id="1ffb9-110">Algumas das APIs que ainda estavam em versão Beta na V1.0 estão agora na fase de Disponibilidade Geral (GA) na V1.1, em particular:</span><span class="sxs-lookup"><span data-stu-id="1ffb9-110">Some of the APIs that were still in Beta in V1.0 are now GA in V1.1, in particular:</span></span>

- <span data-ttu-id="1ffb9-111">métodos assíncronos</span><span class="sxs-lookup"><span data-stu-id="1ffb9-111">async methods</span></span>
- <span data-ttu-id="1ffb9-112">todos os métodos na CDN que estavam anteriormente na versão Beta</span><span class="sxs-lookup"><span data-stu-id="1ffb9-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="1ffb9-113">todos os métodos e interfaces no Gateway de Aplicativo que estavam anteriormente em versão Beta</span><span class="sxs-lookup"><span data-stu-id="1ffb9-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="1ffb9-114">Algumas partes da biblioteca ainda estão em Versão Prévia.</span><span class="sxs-lookup"><span data-stu-id="1ffb9-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="1ffb9-115">Consulte a tabela abaixo para saber o estado atual das bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="1ffb9-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="1ffb9-116">Serviço ou recurso</span><span class="sxs-lookup"><span data-stu-id="1ffb9-116">Service or feature</span></span> | <span data-ttu-id="1ffb9-117">Disponível como Disponibilidade Geral (GA)</span><span class="sxs-lookup"><span data-stu-id="1ffb9-117">Available as GA</span></span> | <span data-ttu-id="1ffb9-118">Disponível como versão prévia</span><span class="sxs-lookup"><span data-stu-id="1ffb9-118">Available as Preview</span></span>  | <span data-ttu-id="1ffb9-119">Em breve</span><span class="sxs-lookup"><span data-stu-id="1ffb9-119">Coming soon</span></span> |
---------|---------|---------|---------|
<span data-ttu-id="1ffb9-120">Computação</span><span class="sxs-lookup"><span data-stu-id="1ffb9-120">Compute</span></span>  | <span data-ttu-id="1ffb9-121">Máquinas virtuais e extensões de VM, conjuntos de dimensionamento de máquina virtual, discos gerenciados</span><span class="sxs-lookup"><span data-stu-id="1ffb9-121">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="1ffb9-122">Serviço de contêiner do Azure, registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="1ffb9-122">Azure container service, Azure container registry</span></span> |    |
<span data-ttu-id="1ffb9-123">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="1ffb9-123">Storage</span></span>   |  <span data-ttu-id="1ffb9-124">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1ffb9-124">Storage accounts</span></span>       |         |   <span data-ttu-id="1ffb9-125">Criptografia</span><span class="sxs-lookup"><span data-stu-id="1ffb9-125">Encryption</span></span>      |
<span data-ttu-id="1ffb9-126">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="1ffb9-126">SQL Database</span></span>  | <span data-ttu-id="1ffb9-127">Bancos de dados, firewalls, pools elásticos</span><span class="sxs-lookup"><span data-stu-id="1ffb9-127">Databases, firewalls, elastic pools</span></span>        |         |   <span data-ttu-id="1ffb9-128">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="1ffb9-128">More features</span></span>      |
<span data-ttu-id="1ffb9-129">Rede</span><span class="sxs-lookup"><span data-stu-id="1ffb9-129">Networking</span></span>    |  <span data-ttu-id="1ffb9-130">Redes virtuais, interfaces de rede, endereços IP, tabelas de roteamento, grupos de segurança de rede, DNS, gerenciadores de tráfego, gateways de aplicativo</span><span class="sxs-lookup"><span data-stu-id="1ffb9-130">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="1ffb9-131">Balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="1ffb9-131">Load balancers</span></span>     |   <span data-ttu-id="1ffb9-132">VPN, observadores de rede</span><span class="sxs-lookup"><span data-stu-id="1ffb9-132">VPN, Network watchers</span></span>   |
<span data-ttu-id="1ffb9-133">Mais serviços</span><span class="sxs-lookup"><span data-stu-id="1ffb9-133">More services</span></span>    |  <span data-ttu-id="1ffb9-134">Gerenciador de Recursos, Cofre de Chaves, Redis, CDN, Lote</span><span class="sxs-lookup"><span data-stu-id="1ffb9-134">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="1ffb9-135">Aplicativos Web, Aplicativos de Funções, Barramento de Serviço, Grafo RBAC, DocumentDB</span><span class="sxs-lookup"><span data-stu-id="1ffb9-135">Web apps, Function apps, Service Bus, Graph RBAC, DocumentDB</span></span>   | <span data-ttu-id="1ffb9-136">Monitor, Agendador, gerenciamento de Funções, Pesquisa, mais recursos do Grafo RBAC</span><span class="sxs-lookup"><span data-stu-id="1ffb9-136">Monitor ,Scheduler, Functions management, Search, more Graph RBAC features</span></span>        |
<span data-ttu-id="1ffb9-137">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="1ffb9-137">Fundamentals</span></span>     |   <span data-ttu-id="1ffb9-138">Autenticação - básica, assíncrona</span><span class="sxs-lookup"><span data-stu-id="1ffb9-138">Authentication - core , Async methods</span></span>       |      |         |

### <a name="import-with-maven"></a><span data-ttu-id="1ffb9-139">Importar com Maven</span><span class="sxs-lookup"><span data-stu-id="1ffb9-139">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="1ffb9-140">Obter ajuda e fazer comentários</span><span class="sxs-lookup"><span data-stu-id="1ffb9-140">Get help and give feedback</span></span>

<span data-ttu-id="1ffb9-141">Confira a comunidade de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obter ajuda usando as bibliotecas em seu próprio código.</span><span class="sxs-lookup"><span data-stu-id="1ffb9-141">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="1ffb9-142">Se você encontrar quaisquer bugs ou tiver sugestões para melhorar essas bibliotecas, arquive todas as questões através do [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="1ffb9-142">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>

### <a name="migrate-from-previous-releases"></a><span data-ttu-id="1ffb9-143">Migrar de versões anteriores</span><span class="sxs-lookup"><span data-stu-id="1ffb9-143">Migrate from previous releases</span></span>

<span data-ttu-id="1ffb9-144">[Migrar da versão 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [Migrar da versão 1.1.0  ](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span><span class="sxs-lookup"><span data-stu-id="1ffb9-144">[Migrate from 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migrate from 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span></span>


