---
title: "Jak korzystać z usługi Azure Redis Cache za pomocą języka Python | Microsoft Docs"
description: "Rozpoczęcie pracy z pamięcią podręczną Redis Azure za pomocą języka Python"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: cdbee52574d0ffbe82ef3dc98f2848f4d00ba2ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-python"></a><span data-ttu-id="177b8-103">Jak korzystać z pamięci podręcznej Redis Azure za pomocą języka Python</span><span class="sxs-lookup"><span data-stu-id="177b8-103">How to use Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="177b8-104">.NET</span><span class="sxs-lookup"><span data-stu-id="177b8-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="177b8-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="177b8-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="177b8-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="177b8-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="177b8-107">Java</span><span class="sxs-lookup"><span data-stu-id="177b8-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="177b8-108">Python</span><span class="sxs-lookup"><span data-stu-id="177b8-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="177b8-109">W tym temacie opisano sposób rozpoczęcia pracy z usługą Azure Redis Cache za pomocą języka Python.</span><span class="sxs-lookup"><span data-stu-id="177b8-109">This topic shows you how to get started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="177b8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="177b8-110">Prerequisites</span></span>
<span data-ttu-id="177b8-111">Zainstaluj klienta [redis-py](https://github.com/andymccurdy/redis-py).</span><span class="sxs-lookup"><span data-stu-id="177b8-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="177b8-112">Tworzenie pamięci podręcznej Redis na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="177b8-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="177b8-113">Pobieranie nazwy hosta i kluczy dostępu</span><span class="sxs-lookup"><span data-stu-id="177b8-113">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-the-non-ssl-endpoint"></a><span data-ttu-id="177b8-114">Włączanie punktu końcowego bez obsługi protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="177b8-114">Enable the non-SSL endpoint</span></span>
<span data-ttu-id="177b8-115">Niektórzy klienci Redis nie obsługują protokołu SSL, a domyślnie [port nieobsługujący protokołu SSL jest wyłączony dla nowych wystąpień pamięci podręcznej Redis Azure](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="177b8-115">Some Redis clients don't support SSL, and by default the [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="177b8-116">Obecnie klient [redis-py](https://github.com/andymccurdy/redis-py) nie obsługuje protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="177b8-116">At the time of this writing, the [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="177b8-117">Dodawanie elementu do pamięci podręcznej i pobieranie go</span><span class="sxs-lookup"><span data-stu-id="177b8-117">Add something to the cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="177b8-118">Zastąp element `<name>` swoją nazwą pamięci podręcznej i element `key` swoim kluczem dostępu.</span><span class="sxs-lookup"><span data-stu-id="177b8-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
