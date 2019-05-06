---
title: Gerenciar Caches Redis utilizando o Azure Explorer para Eclipse
description: Saiba como gerenciar seus caches redis do Azure utilizando o Azure Explorer para Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 00f363e5dacc9c494b01eaa479db7e9e1aff6952
ms.sourcegitcommit: 4f1acf05e3bbb7eb6bca9b65300c1c5b9772185a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456051"
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="cca18-103">Gerenciar Caches Redis utilizando o Azure Explorer para Eclipse</span><span class="sxs-lookup"><span data-stu-id="cca18-103">Managing Redis Caches using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="cca18-104">O Azure Explorer, que faz parte do Kit de Ferramentas do Azure para Eclipse, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar caches redis em sua conta do Azure de dentro do IDE do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="cca18-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="cca18-105">Criar um Cache Redis utilizando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="cca18-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="cca18-106">As etapas a seguir guiarão você pelas etapas para criar um Cache Redis utilizando o Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="cca18-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="cca18-107">Entre em sua conta do Azure usando as etapas no artigo (Instruções de entrada para o Kit de ferramentas do Azure para Eclipse).</span><span class="sxs-lookup"><span data-stu-id="cca18-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="cca18-108">Na janela de ferramentas do **Azure Explorer**expanda o nó do **Azure**, clique com o botão direito do mouse em **Caches Redis** e, em seguida, clique em **Criar Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="cca18-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Criar menu Cache Redis][CR01]

1. <span data-ttu-id="cca18-110">Quando a caixa de diálogo **Novo Cache Redis** aparecer, especifique as seguinte opções:</span><span class="sxs-lookup"><span data-stu-id="cca18-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![Caixa de diálogo Criar Novo Cache Redis][CR02]

   <span data-ttu-id="cca18-112"> a.</span><span class="sxs-lookup"><span data-stu-id="cca18-112">a.</span></span> <span data-ttu-id="cca18-113">**Nome DNS**: especifica o subdomínio DNS para o novo Cache Redis, que é pré-anexado a ".redis.cache.windows.net"; por exemplo, *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="cca18-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which is prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="cca18-114">b.</span><span class="sxs-lookup"><span data-stu-id="cca18-114">b.</span></span> <span data-ttu-id="cca18-115">**Assinatura**: especifica a assinatura do Azure que será utilizada para o novo Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="cca18-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="cca18-116">c.</span><span class="sxs-lookup"><span data-stu-id="cca18-116">c.</span></span> <span data-ttu-id="cca18-117">**Grupo de Recursos**: especifica o grupo de recursos para seu Cache Redis; é necessário escolher uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="cca18-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span>
      * <span data-ttu-id="cca18-118">**Criar novo**: especifica que você deseja criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cca18-118">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="cca18-119">**Usar existente**: especifica que você escolherá entre uma lista dos grupos de recursos associados à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cca18-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="cca18-120">d.</span><span class="sxs-lookup"><span data-stu-id="cca18-120">d.</span></span> <span data-ttu-id="cca18-121">**Localização**: especifica a localização em que seu cache redis será criado; por exemplo, *Oeste dos EUA*.</span><span class="sxs-lookup"><span data-stu-id="cca18-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="cca18-122">e.</span><span class="sxs-lookup"><span data-stu-id="cca18-122">e.</span></span> <span data-ttu-id="cca18-123">**Tipo de preço**: especifica qual tipo de preço seu Cache Redis utiliza; é a configuração que determina o número de conexões do cliente.</span><span class="sxs-lookup"><span data-stu-id="cca18-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="cca18-124">(Para saber mais, veja [Preço do Cache Redis]).</span><span class="sxs-lookup"><span data-stu-id="cca18-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="cca18-125">f.</span><span class="sxs-lookup"><span data-stu-id="cca18-125">f.</span></span> <span data-ttu-id="cca18-126">**Porta não SSL**: especifica se o Cache Redis permite conexões não SSL; por padrão, apenas conexões SSL são permitidas.</span><span class="sxs-lookup"><span data-stu-id="cca18-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="cca18-127">Quando tiver especificado todas as configurações de cache redis, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cca18-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="cca18-128">Depois que o cache redis tiver sido criado, ele será exibido no Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="cca18-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Cache Redis no Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="cca18-130">Para saber mais sobre como definir as configurações do seu cache redis do Azure, veja [Como configurar o Cache Redis do Azure].</span><span class="sxs-lookup"><span data-stu-id="cca18-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="cca18-131">Exibir as propriedades para o Cache Redis no Eclipse</span><span class="sxs-lookup"><span data-stu-id="cca18-131">Display the properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="cca18-132">No Azure Explorer, clique com o botão direito do mouse no cache redis e clique em **Mostrar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="cca18-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Menu de contexto do Azure Explorer para exibir propriedades para um cache redis][SP01]

1. <span data-ttu-id="cca18-134">O Azure Explorer exibe as propriedades para o cache redis.</span><span class="sxs-lookup"><span data-stu-id="cca18-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Propriedades de cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="cca18-136">Excluir o Cache Redis utilizando o Eclipse</span><span class="sxs-lookup"><span data-stu-id="cca18-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="cca18-137">No Azure Explorer, clique com o botão direito do mouse no cache redis e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="cca18-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Menu de contexto do Azure Explorer para excluir um cache redis][DE01]

1. <span data-ttu-id="cca18-139">Clique em **OK** quando solicitado a excluir o cache redis.</span><span class="sxs-lookup"><span data-stu-id="cca18-139">Click **OK** when prompted to delete your redis cache.</span></span>

   ![Excluir prompt do cache redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="cca18-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cca18-141">Next steps</span></span>

<span data-ttu-id="cca18-142">Para saber mais sobre caches redis, configurações e preços do Azure, veja os seguintes links:</span><span class="sxs-lookup"><span data-stu-id="cca18-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="cca18-143">[Cache Redis do Azure]</span><span class="sxs-lookup"><span data-stu-id="cca18-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="cca18-144">[Documentação do Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="cca18-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="cca18-145">[Preço do Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="cca18-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="cca18-146">[Como configurar o Cache Redis do Azure]</span><span class="sxs-lookup"><span data-stu-id="cca18-146">[How to configure Azure Redis Cache]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Preço do Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Redis Cache Pricing]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis do Azure]: https://azure.microsoft.com/services/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Documentação do Cache Redis]: /azure/redis-cache/
[Redis Cache Documentation]: /azure/redis-cache/
[Como configurar o Cache Redis do Azure]: /azure/redis-cache/cache-configure
[How to configure Azure Redis Cache]: /azure/redis-cache/cache-configure

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
