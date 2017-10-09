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
# <a name="how-toouse-azure-redis-cache-with-python"></a>Jak toouse Azure pamięci podręcznej Redis języka Python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

W tym temacie przedstawiono sposób uruchamiania tooget z pamięci podręcznej Redis Azure za pomocą języka Python.

## <a name="prerequisites"></a>Wymagania wstępne
Zainstaluj klienta [redis-py](https://github.com/andymccurdy/redis-py).

## <a name="create-a-redis-cache-on-azure"></a>Tworzenie pamięci podręcznej Redis na platformie Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Pobieranie hello hosta nazwy i dostępu do kluczy
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a>Włącz hello endpoint bez użycia protokołu SSL
Niektórzy klienci Redis nie obsługuje protokołu SSL i przez domyślny hello [portu bez protokołu SSL jest wyłączone dla nowego wystąpienia pamięci podręcznej Redis Azure](cache-configure.md#access-ports). W czasie hello pisania tego dokumentu, hello [redis py](https://github.com/andymccurdy/redis-py) klienta nie obsługuje protokołu SSL. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Dodaj element toohello pamięci podręcznej i pobranie
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


Zastąp element `<name>` swoją nazwą pamięci podręcznej i element `key` swoim kluczem dostępu.

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
