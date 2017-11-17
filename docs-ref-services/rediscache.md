---
title: Bibliotecas do Cache Redis para Java
description: "Documentação de referência para as bibliotecas de gerenciamento e de cliente de Java para Cache Redis"
keywords: "Azure, Java, SDK, API, cache, redis, cache Web, chave-valor, em memória"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: redis-cache
ms.openlocfilehash: 6d436c49124fd0a406486e0c7bac4d1605de5d32
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2017
---
# <a name="redis-cache-libraries-for-java"></a><span data-ttu-id="ad3a7-104">Bibliotecas do Cache Redis para Java</span><span class="sxs-lookup"><span data-stu-id="ad3a7-104">Redis Cache libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="ad3a7-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ad3a7-105">Overview</span></span>

<span data-ttu-id="ad3a7-106">O Cache Redis do Azure é um repositório de chave-valor seguro e distribuído com base no popular cache [Redis](https://redis.io/) de software livre.</span><span class="sxs-lookup"><span data-stu-id="ad3a7-106">Azure Redis Cache is a secure, distributed key-value store based on the popular open source [Redis](https://redis.io/) cache.</span></span> 

<span data-ttu-id="ad3a7-107">Para começar a usar o Cache Redis do Azure, consulte [Como usar o Cache Redis do Azure com Java](/azure/redis-cache/cache-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="ad3a7-107">To get started with Azure Redis Cache, see [How to use Azure Redis Cache with Java](/azure/redis-cache/cache-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="ad3a7-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="ad3a7-108">Client library</span></span>

<span data-ttu-id="ad3a7-109">Conecte-se ao Cache Redis do Azure e armazene e recupere valores de cache usando o cliente [Jedis](https://github.com/xetorthio/jedis) de software livre.</span><span class="sxs-lookup"><span data-stu-id="ad3a7-109">Connect to Azure Redis Cache and store and retrieve values from the cache using the open-source [Jedis](https://github.com/xetorthio/jedis) client.</span></span>  

<span data-ttu-id="ad3a7-110">[Adicionar uma dependência](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) para seu arquivo `pom.xml` Maven para usar a biblioteca do cliente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="ad3a7-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a><span data-ttu-id="ad3a7-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ad3a7-111">Example</span></span>

<span data-ttu-id="ad3a7-112">Conectar-se ao Redis do Azure e inserir uma cadeia de caracteres no cache.</span><span class="sxs-lookup"><span data-stu-id="ad3a7-112">Connect to Azure Redis and insert a string into the cache.</span></span>

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a><span data-ttu-id="ad3a7-113">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="ad3a7-113">Management API</span></span>

<span data-ttu-id="ad3a7-114">Criar e dimensionar os recursos do Redis do Azure e gerenciar chaves de acesso com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="ad3a7-114">Create and scale Azure Redis resources and manage access keys to with the management API.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="ad3a7-115">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ad3a7-115">Example</span></span>

<span data-ttu-id="ad3a7-116">Criar um novo Cache Redis do Azure na [camada padrão de dois nós](https://azure.microsoft.com/services/cache/).</span><span class="sxs-lookup"><span data-stu-id="ad3a7-116">Create a new Azure Redis Cache in the [two-node standard tier](https://azure.microsoft.com/services/cache/).</span></span> 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad3a7-117">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="ad3a7-117">Explore the Management APIs</span></span>](/java/api/overview/azure/rediscache/managementapi)

## <a name="samples"></a><span data-ttu-id="ad3a7-118">Exemplos</span><span class="sxs-lookup"><span data-stu-id="ad3a7-118">Samples</span></span>

[<span data-ttu-id="ad3a7-119">Explorar o Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="ad3a7-119">Manage Azure Redis Cache</span></span>](https://github.com/Azure-Samples/redis-java-manage-cache)   

<span data-ttu-id="ad3a7-120">Explore mais [exemplos de código Java para o Cache Redis do Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ad3a7-120">Explore more [sample Java code for Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) you can use in your apps.</span></span>
