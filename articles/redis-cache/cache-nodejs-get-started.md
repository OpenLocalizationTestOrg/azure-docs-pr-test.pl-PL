---
title: "Jak korzystać z usługi Azure Redis Cache w środowisku Node.js | Microsoft Docs"
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
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="8125c-103">Jak korzystać z pamięci podręcznej Redis Azure w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="8125c-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8125c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8125c-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="8125c-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8125c-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="8125c-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="8125c-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="8125c-107">Java</span><span class="sxs-lookup"><span data-stu-id="8125c-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="8125c-108">Python</span><span class="sxs-lookup"><span data-stu-id="8125c-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="8125c-109">Pamięć podręczna Redis Azure umożliwia dostęp do bezpiecznej dedykowanej pamięci podręcznej Redis zarządzanej przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8125c-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="8125c-110">Pamięć podręczna jest dostępna z poziomu dowolnej aplikacji na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8125c-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="8125c-111">W tym temacie opisano sposób rozpoczęcia pracy z pamięcią podręczną Redis Azure w środowisku Node.js.</span><span class="sxs-lookup"><span data-stu-id="8125c-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="8125c-112">Inny przykład użycia pamięci podręcznej Redis Azure w środowisku Node.js można znaleźć w temacie [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md) (Tworzenie aplikacji czatu środowiska Node.js za pomocą biblioteki Socket.IO w witrynie sieci Web platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="8125c-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8125c-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8125c-113">Prerequisites</span></span>
<span data-ttu-id="8125c-114">Zainstaluj klienta [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="8125c-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="8125c-115">W tym samouczku jest używany klient [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="8125c-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="8125c-116">Przykłady użycia innych klientów Node.js można znaleźć w dokumentacji poszczególnych klientów Node.js wymienionych na stronie [klientów Node.js usługi Redis](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="8125c-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="8125c-117">Tworzenie pamięci podręcznej Redis na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="8125c-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="8125c-118">Pobieranie nazwy hosta i kluczy dostępu</span><span class="sxs-lookup"><span data-stu-id="8125c-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="8125c-119">Bezpieczne łączenie się z pamięcią podręczną przy użyciu protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="8125c-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="8125c-120">Najnowsze kompilacje klienta [node_redis](https://github.com/mranney/node_redis) umożliwiają łączenie się z usługą Azure Redis Cache przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="8125c-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="8125c-121">Poniższy przykład przedstawia, jak nawiązać połączenie z usługą Azure Redis Cache przy użyciu punktu końcowego 6380 protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="8125c-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="8125c-122">Zastąp parametr `<name>` nazwą Twojej pamięci podręcznej, a parametr `<key>` kluczem podstawowym lub dodatkowym, jak opisano w poprzedniej sekcji [Pobieranie nazwy hosta i kluczy dostępu](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="8125c-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="8125c-123">Port inny niż SSL jest wyłączony w przypadku nowych wystąpień usługi Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="8125c-123">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="8125c-124">Jeśli używasz innego klienta, który nie obsługuje protokołu SSL, zobacz [How to enable the non-SSL port](cache-configure.md#access-ports) (Jak włączyć port inny niż SSL).</span><span class="sxs-lookup"><span data-stu-id="8125c-124">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="8125c-125">Dodawanie elementu do pamięci podręcznej i pobieranie go</span><span class="sxs-lookup"><span data-stu-id="8125c-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="8125c-126">Poniższy przykład pokazuje, jak połączyć się z wystąpieniem usługi Azure Redis Cache oraz jak zapisać i pobrać element z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="8125c-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="8125c-127">Aby uzyskać więcej przykładów użycia usługi Redis z klientem [node_redis](https://github.com/mranney/node_redis), zobacz [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="8125c-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="8125c-128">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8125c-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="8125c-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8125c-129">Next steps</span></span>
* <span data-ttu-id="8125c-130">[Włącz diagnostykę pamięci podręcznej](cache-how-to-monitor.md#enable-cache-diagnostics), aby móc [monitorować](cache-how-to-monitor.md) jej kondycję.</span><span class="sxs-lookup"><span data-stu-id="8125c-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="8125c-131">Przeczytaj oficjalną [dokumentację magazynu Redis](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="8125c-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>

