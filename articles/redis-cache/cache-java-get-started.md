---
title: "toouse aaaHow pamięci podręcznej Redis Azure z językiem Java | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="86840-103">Jak toouse Azure pamięci podręcznej Redis z językiem Java</span><span class="sxs-lookup"><span data-stu-id="86840-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86840-104">.NET</span><span class="sxs-lookup"><span data-stu-id="86840-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="86840-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="86840-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="86840-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="86840-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="86840-107">Java</span><span class="sxs-lookup"><span data-stu-id="86840-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="86840-108">Python</span><span class="sxs-lookup"><span data-stu-id="86840-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="86840-109">Azure zapewnia pamięci podręcznej Redis dostęp tooa dedykowanej pamięci podręcznej Redis pamięci podręcznej, zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="86840-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="86840-110">Pamięć podręczna jest dostępna z poziomu dowolnej aplikacji na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="86840-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="86840-111">W tym temacie przedstawiono sposób uruchamiania tooget z pamięci podręcznej Redis Azure za pomocą języka Java.</span><span class="sxs-lookup"><span data-stu-id="86840-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86840-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="86840-112">Prerequisites</span></span>
<span data-ttu-id="86840-113">[Jedis](https://github.com/xetorthio/jedis) — klient Java dla usługi Redis</span><span class="sxs-lookup"><span data-stu-id="86840-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="86840-114">W tym samouczku używany jest klient Jedis, ale można użyć dowolnego klienta Java wymienionego pod adresem [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="86840-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="86840-115">Tworzenie pamięci podręcznej Redis na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="86840-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="86840-116">Pobieranie hello hosta nazwy i dostępu do kluczy</span><span class="sxs-lookup"><span data-stu-id="86840-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="86840-117">Połączenie pamięci podręcznej toohello przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="86840-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="86840-118">Najnowsza wersja kompilacji Hello [jedis](https://github.com/xetorthio/jedis) zapewniają obsługę łączenie tooAzure pamięci podręcznej Redis przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="86840-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="86840-119">Witaj poniższy przykład pokazuje, jak przy użyciu pamięci podręcznej Redis tooAzure tooconnect hello punkt końcowy SSL 6380.</span><span class="sxs-lookup"><span data-stu-id="86840-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="86840-120">Zastąp `<name>` o nazwie hello pamięć podręczną i `<key>` przy użyciu jednej klucz podstawowy lub pomocniczy zgodnie z opisem w hello poprzedniej [pobrać hello nazwy i dostęp za pomocą klucza hosta](#retrieve-the-host-name-and-access-keys) sekcji.</span><span class="sxs-lookup"><span data-stu-id="86840-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="86840-121">port bez protokołu SSL Hello jest wyłączona dla nowego wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="86840-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="86840-122">Jeśli korzystasz z innego klienta, który nie obsługuje protokołu SSL, zobacz [jak tooenable hello portu bez protokołu SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="86840-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="86840-123">Dodaj element toohello pamięci podręcznej i pobranie</span><span class="sxs-lookup"><span data-stu-id="86840-123">Add something toohello cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="86840-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86840-124">Next steps</span></span>
* <span data-ttu-id="86840-125">[Włącz diagnostykę w pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) można więc [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello kondycji pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="86840-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="86840-126">Oficjalne hello odczytu [Redis dokumentacji](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="86840-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
