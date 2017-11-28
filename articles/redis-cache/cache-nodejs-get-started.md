---
title: "toouse aaaHow pamięci podręcznej Redis Azure za pomocą języka Node.js | Dokumentacja firmy Microsoft"
description: "Rozpoczęcie pracy z pamięcią podręczną Redis Azure za pomocą środowiska Node.js i klienta node_redis."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="58049-103">Jak toouse Azure pamięci podręcznej Redis za pomocą języka Node.js</span><span class="sxs-lookup"><span data-stu-id="58049-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58049-104">.NET</span><span class="sxs-lookup"><span data-stu-id="58049-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="58049-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="58049-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="58049-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="58049-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="58049-107">Java</span><span class="sxs-lookup"><span data-stu-id="58049-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="58049-108">Python</span><span class="sxs-lookup"><span data-stu-id="58049-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="58049-109">Zapewnia pamięci podręcznej Redis Azure, możesz uzyskać dostęp tooa bezpiecznego, dedykowane pamięć podręczna Redis, zarządzany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="58049-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="58049-110">Pamięć podręczna jest dostępna z poziomu dowolnej aplikacji na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="58049-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="58049-111">W tym temacie przedstawiono sposób uruchamiania tooget z pamięci podręcznej Redis Azure za pomocą środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="58049-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="58049-112">Inny przykład użycia pamięci podręcznej Redis Azure w środowisku Node.js można znaleźć w temacie [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md) (Tworzenie aplikacji czatu środowiska Node.js za pomocą biblioteki Socket.IO w witrynie sieci Web platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="58049-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58049-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="58049-113">Prerequisites</span></span>
<span data-ttu-id="58049-114">Zainstaluj klienta [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="58049-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="58049-115">W tym samouczku jest używany klient [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="58049-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="58049-116">Przykłady użycia innych klientów Node.js, w dokumentacji hello poszczególnych klientów Node.js hello wymienione na [Node.js Redis klientów](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="58049-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="58049-117">Tworzenie pamięci podręcznej Redis na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="58049-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="58049-118">Pobieranie hello hosta nazwy i dostępu do kluczy</span><span class="sxs-lookup"><span data-stu-id="58049-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="58049-119">Połączenie pamięci podręcznej toohello przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="58049-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="58049-120">Najnowsza wersja kompilacji Hello [node_redis](https://github.com/mranney/node_redis) zapewniają obsługę łączenie tooAzure pamięci podręcznej Redis przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="58049-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="58049-121">Witaj poniższy przykład pokazuje, jak przy użyciu pamięci podręcznej Redis tooAzure tooconnect hello punkt końcowy SSL 6380.</span><span class="sxs-lookup"><span data-stu-id="58049-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="58049-122">Zastąp `<name>` o nazwie hello pamięć podręczną i `<key>` przy użyciu jednej klucz podstawowy lub pomocniczy zgodnie z opisem w hello poprzedniej [pobrać hello nazwy i dostęp za pomocą klucza hosta](#retrieve-the-host-name-and-access-keys) sekcji.</span><span class="sxs-lookup"><span data-stu-id="58049-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="58049-123">port bez protokołu SSL Hello jest wyłączona dla nowego wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="58049-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="58049-124">Jeśli korzystasz z innego klienta, który nie obsługuje protokołu SSL, zobacz [jak tooenable hello portu bez protokołu SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="58049-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="58049-125">Dodaj element toohello pamięci podręcznej i pobranie</span><span class="sxs-lookup"><span data-stu-id="58049-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="58049-126">powitania po przykładzie pokazano, jak Redis Azure tooconnect tooan pamięci podręcznej wystąpienia i przechowywania i pobierania elementu z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="58049-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="58049-127">Więcej przykładów dotyczących przy użyciu pamięci podręcznej Redis z hello [node_redis](https://github.com/mranney/node_redis) klienta, zobacz [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="58049-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="58049-128">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="58049-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="58049-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="58049-129">Next steps</span></span>
* <span data-ttu-id="58049-130">[Włącz diagnostykę w pamięci podręcznej](cache-how-to-monitor.md#enable-cache-diagnostics) można więc [monitor](cache-how-to-monitor.md) hello kondycji pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="58049-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="58049-131">Oficjalne hello odczytu [Redis dokumentacji](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="58049-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

