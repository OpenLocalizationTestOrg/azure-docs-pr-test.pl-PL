---
title: "Jak używać usługi Azure Redis Cache za pomocą języka Java | Microsoft Docs"
description: "Rozpoczęcie pracy z usługą Azure Redis Cache za pomocą języka Java"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 3cfad3a7279b5f9bbff1e6cd9794c492e3544752
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-java"></a><span data-ttu-id="eae9a-103">Jak używać pamięci podręcznej Redis Azure za pomocą języka Java</span><span class="sxs-lookup"><span data-stu-id="eae9a-103">How to use Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eae9a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="eae9a-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="eae9a-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="eae9a-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="eae9a-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="eae9a-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="eae9a-107">Java</span><span class="sxs-lookup"><span data-stu-id="eae9a-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="eae9a-108">Python</span><span class="sxs-lookup"><span data-stu-id="eae9a-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="eae9a-109">Usługa Azure Redis Cache umożliwia dostęp do dedykowanej pamięci podręcznej Redis, zarządzanej przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eae9a-109">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="eae9a-110">Pamięć podręczna jest dostępna z poziomu dowolnej aplikacji na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eae9a-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="eae9a-111">W tym temacie opisano sposób rozpoczęcia pracy z usługą Azure Redis Cache za pomocą języka Java.</span><span class="sxs-lookup"><span data-stu-id="eae9a-111">This topic shows you how to get started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eae9a-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eae9a-112">Prerequisites</span></span>
<span data-ttu-id="eae9a-113">[Jedis](https://github.com/xetorthio/jedis) — klient Java dla usługi Redis</span><span class="sxs-lookup"><span data-stu-id="eae9a-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="eae9a-114">W tym samouczku używany jest klient Jedis, ale można użyć dowolnego klienta Java wymienionego pod adresem [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="eae9a-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="eae9a-115">Tworzenie pamięci podręcznej Redis na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eae9a-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="eae9a-116">Pobieranie nazwy hosta i kluczy dostępu</span><span class="sxs-lookup"><span data-stu-id="eae9a-116">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="eae9a-117">Bezpieczne łączenie się z pamięcią podręczną przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="eae9a-117">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="eae9a-118">Najnowsze kompilacje klienta [jedis](https://github.com/xetorthio/jedis) umożliwiają łączenie się z usługą Azure Redis Cache przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="eae9a-118">The latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="eae9a-119">Poniższy przykład przedstawia, jak nawiązać połączenie z usługą Azure Redis Cache przy użyciu punktu końcowego 6380 protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="eae9a-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="eae9a-120">Zastąp parametr `<name>` nazwą Twojej pamięci podręcznej, a parametr `<key>` kluczem podstawowym lub dodatkowym, jak opisano w poprzedniej sekcji [Pobieranie nazwy hosta i kluczy dostępu](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="eae9a-120">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="eae9a-121">Port inny niż SSL jest wyłączony w przypadku nowych wystąpień usługi Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="eae9a-121">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="eae9a-122">Jeśli używasz innego klienta, który nie obsługuje protokołu SSL, zobacz [How to enable the non-SSL port](cache-configure.md#access-ports) (Jak włączyć port inny niż SSL).</span><span class="sxs-lookup"><span data-stu-id="eae9a-122">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="eae9a-123">Dodawanie elementu do pamięci podręcznej i pobieranie go</span><span class="sxs-lookup"><span data-stu-id="eae9a-123">Add something to the cache and retrieve it</span></span>
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a><span data-ttu-id="eae9a-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eae9a-124">Next steps</span></span>
* <span data-ttu-id="eae9a-125">[Włącz diagnostykę pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics), aby móc [monitorować](https://msdn.microsoft.com/library/azure/dn763945.aspx) jej kondycję.</span><span class="sxs-lookup"><span data-stu-id="eae9a-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) the health of your cache.</span></span>
* <span data-ttu-id="eae9a-126">Przeczytaj oficjalną [dokumentację magazynu Redis](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="eae9a-126">Read the official [Redis documentation](http://redis.io/documentation).</span></span>
