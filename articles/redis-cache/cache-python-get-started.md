---
title: "toouse aaaHow pamięci podręcznej Redis Azure języka Python | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a><span data-ttu-id="ee211-103">Jak toouse Azure pamięci podręcznej Redis języka Python</span><span class="sxs-lookup"><span data-stu-id="ee211-103">How toouse Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee211-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ee211-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="ee211-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ee211-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="ee211-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ee211-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="ee211-107">Java</span><span class="sxs-lookup"><span data-stu-id="ee211-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="ee211-108">Python</span><span class="sxs-lookup"><span data-stu-id="ee211-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="ee211-109">W tym temacie przedstawiono sposób uruchamiania tooget z pamięci podręcznej Redis Azure za pomocą języka Python.</span><span class="sxs-lookup"><span data-stu-id="ee211-109">This topic shows you how tooget started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee211-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ee211-110">Prerequisites</span></span>
<span data-ttu-id="ee211-111">Zainstaluj klienta [redis-py](https://github.com/andymccurdy/redis-py).</span><span class="sxs-lookup"><span data-stu-id="ee211-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="ee211-112">Tworzenie pamięci podręcznej Redis na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ee211-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="ee211-113">Pobieranie hello hosta nazwy i dostępu do kluczy</span><span class="sxs-lookup"><span data-stu-id="ee211-113">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a><span data-ttu-id="ee211-114">Włącz hello endpoint bez użycia protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="ee211-114">Enable hello non-SSL endpoint</span></span>
<span data-ttu-id="ee211-115">Niektórzy klienci Redis nie obsługuje protokołu SSL i przez domyślny hello [portu bez protokołu SSL jest wyłączone dla nowego wystąpienia pamięci podręcznej Redis Azure](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="ee211-115">Some Redis clients don't support SSL, and by default hello [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="ee211-116">W czasie hello pisania tego dokumentu, hello [redis py](https://github.com/andymccurdy/redis-py) klienta nie obsługuje protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="ee211-116">At hello time of this writing, hello [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="ee211-117">Dodaj element toohello pamięci podręcznej i pobranie</span><span class="sxs-lookup"><span data-stu-id="ee211-117">Add something toohello cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="ee211-118">Zastąp element `<name>` swoją nazwą pamięci podręcznej i element `key` swoim kluczem dostępu.</span><span class="sxs-lookup"><span data-stu-id="ee211-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
