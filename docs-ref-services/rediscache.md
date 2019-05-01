---
title: Bibliotecas do Cache Redis para Java
description: Documentação de referência para as bibliotecas de gerenciamento e de cliente de Java para Cache Redis
keywords: Azure, Java, SDK, API, cache, redis, cache Web, chave-valor, em memória
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: redis-cache
ms.openlocfilehash: 6f19587d3caeaccd2805007f60bd4ba96fee0bf7
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593301"
---
# <a name="redis-cache-libraries-for-java"></a>Bibliotecas do Cache Redis para Java

## <a name="overview"></a>Visão geral

O Cache Redis do Azure é um repositório de chave-valor seguro e distribuído com base no popular cache [Redis](https://redis.io/) de software livre. 

Para começar a usar o Cache Redis do Azure, consulte [Como usar o Cache Redis do Azure com Java](/azure/redis-cache/cache-java-get-started).

## <a name="client-library"></a>Biblioteca do cliente

Conecte-se ao Cache Redis do Azure e armazene e recupere valores de cache usando o cliente [Jedis](https://github.com/xetorthio/jedis) de software livre.  

[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a>Exemplo

Conectar-se ao Redis do Azure e inserir uma cadeia de caracteres no cache.

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a>API de gerenciamento

Criar e dimensionar os recursos do Redis do Azure e gerenciar chaves de acesso com a API de gerenciamento.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Exemplo

Criar um novo Cache Redis do Azure na [camada padrão de dois nós](https://azure.microsoft.com/services/cache/). 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/java/api/overview/azure/rediscache/management)

## <a name="samples"></a>Exemplos

[Explorar o Cache Redis do Azure](https://github.com/Azure-Samples/redis-java-manage-cache)   

Explore mais [exemplos de código Java para o Cache Redis do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) que você pode usar em seus aplicativos.
