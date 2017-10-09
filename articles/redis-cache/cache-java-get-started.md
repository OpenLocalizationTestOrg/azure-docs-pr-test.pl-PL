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
# <a name="how-toouse-azure-redis-cache-with-java"></a>Jak toouse Azure pamięci podręcznej Redis z językiem Java
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure zapewnia pamięci podręcznej Redis dostęp tooa dedykowanej pamięci podręcznej Redis pamięci podręcznej, zarządzany przez firmę Microsoft. Pamięć podręczna jest dostępna z poziomu dowolnej aplikacji na platformie Microsoft Azure.

W tym temacie przedstawiono sposób uruchamiania tooget z pamięci podręcznej Redis Azure za pomocą języka Java.

## <a name="prerequisites"></a>Wymagania wstępne
[Jedis](https://github.com/xetorthio/jedis) — klient Java dla usługi Redis

W tym samouczku używany jest klient Jedis, ale można użyć dowolnego klienta Java wymienionego pod adresem [http://redis.io/clients](http://redis.io/clients).

## <a name="create-a-redis-cache-on-azure"></a>Tworzenie pamięci podręcznej Redis na platformie Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Pobieranie hello hosta nazwy i dostępu do kluczy
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Połączenie pamięci podręcznej toohello przy użyciu protokołu SSL
Najnowsza wersja kompilacji Hello [jedis](https://github.com/xetorthio/jedis) zapewniają obsługę łączenie tooAzure pamięci podręcznej Redis przy użyciu protokołu SSL. Witaj poniższy przykład pokazuje, jak przy użyciu pamięci podręcznej Redis tooAzure tooconnect hello punkt końcowy SSL 6380. Zastąp `<name>` o nazwie hello pamięć podręczną i `<key>` przy użyciu jednej klucz podstawowy lub pomocniczy zgodnie z opisem w hello poprzedniej [pobrać hello nazwy i dostęp za pomocą klucza hosta](#retrieve-the-host-name-and-access-keys) sekcji.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> port bez protokołu SSL Hello jest wyłączona dla nowego wystąpienia pamięci podręcznej Redis Azure. Jeśli korzystasz z innego klienta, który nie obsługuje protokołu SSL, zobacz [jak tooenable hello portu bez protokołu SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Dodaj element toohello pamięci podręcznej i pobranie
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


## <a name="next-steps"></a>Następne kroki
* [Włącz diagnostykę w pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) można więc [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello kondycji pamięci podręcznej.
* Oficjalne hello odczytu [Redis dokumentacji](http://redis.io/documentation).
