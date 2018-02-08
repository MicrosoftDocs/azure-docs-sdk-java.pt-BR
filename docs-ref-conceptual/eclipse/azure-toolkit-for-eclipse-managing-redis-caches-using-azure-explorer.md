---
title: Gerenciar Caches Redis utilizando o Azure Explorer para Eclipse
description: Saiba como gerenciar seus caches redis do Azure utilizando o Azure Explorer para Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 2d3f2363bd0b41808cd409417327b924cb86d85b
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a>Gerenciar Caches Redis utilizando o Azure Explorer para Eclipse

O Azure Explorer, que faz parte do Kit de Ferramentas do Azure para Eclipse, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar caches redis em sua conta do Azure de dentro do IDE do Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>Criar um Cache Redis utilizando o Eclipse

As etapas a seguir guiarão você pelas etapas para criar um Cache Redis utilizando o Azure Explorer.

1. Entre em sua conta do Azure usando as etapas no artigo (Instruções de entrada para o Kit de ferramentas do Azure para Eclipse).

1. Na janela de ferramentas do **Azure Explorer**expanda o nó do **Azure**, clique com o botão direito do mouse em **Caches Redis** e, em seguida, clique em **Criar Cache Redis**.

   ![Criar menu Cache Redis][CR01]

1. Quando a caixa de diálogo **Novo Cache Redis** aparecer, especifique as seguinte opções:

   ![Caixa de diálogo Criar Novo Cache Redis][CR02]

   a. **Nome DNS**: especifica o subdomínio DNS para o novo cache redis, que é pré-anexado a ".redis.cache.windows.net"; por exemplo: *wingtiptoys.redis.cache.windows.net*.

   b. **Assinatura**: especifica a assinatura do Azure que deseja utilizar para o novo cache redis.

   c. **Grupo de Recursos**: especifica o grupo de recursos para seu cache redis; é necessário escolher uma das seguintes opções:
      * **Criar Novo**: especifica que você deseja criar um novo grupo de recursos.
      * **Usar Existente**: especifica que você escolherá entre uma lista dos grupos de recursos associados à sua conta do Azure.

   d. **Localização**: especifica a localização em que seu cache redis será criado; por exemplo, *Oeste dos EUA*.

   e. **Tipo de Preços**: especifica qual tipo de preço seu cache redis utiliza; essa configuração determina o número de conexões do cliente. (Para saber mais, veja [Preços do Cache Redis]).

   f. **Porta não SSL**: especifica se o cache redis permite conexões não SSL; por padrão, apenas as conexões SSL são permitidas.

1. Quando tiver especificado todas as configurações de cache redis, clique em **OK**.

Depois que o cache redis tiver sido criado, ele será exibido no Azure Explorer.

   ![Cache Redis no Azure Explorer][CR03]

> [!NOTE]
>
> Para saber mais sobre como definir as configurações do seu cache redis do Azure, veja [Como configurar o Cache Redis do Azure].
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a>Exibir as propriedades para o Cache Redis no Eclipse

1. No Azure Explorer, clique com o botão direito do mouse no cache redis e clique em **Mostrar propriedades**.

   ![Menu de contexto do Azure Explorer para exibir propriedades para um cache redis][SP01]

1. O Azure Explorer exibe as propriedades para o cache redis.

   ![Propriedades de cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>Excluir o Cache Redis utilizando o Eclipse

1. No Azure Explorer, clique com o botão direito do mouse no cache redis e clique em **Excluir**.

   ![Menu de contexto do Azure Explorer para excluir um cache redis][DE01]

1. Clique em **OK** quando solicitado a excluir o cache redis.

   ![Excluir prompt do cache redis][DE02]

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre caches redis, configurações e preços do Azure, veja os seguintes links:

* [Cache Redis do Azure]
* [Documentação do Cache Redis]
* [Preços do Cache Redis]
* [Como configurar o Cache Redis do Azure]

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Preços do Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis do Azure]: https://azure.microsoft.com/services/cache/
[Documentação do Cache Redis]: /azure/redis-cache/
[Como configurar o Cache Redis do Azure]: /azure/redis-cache/cache-configure

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
