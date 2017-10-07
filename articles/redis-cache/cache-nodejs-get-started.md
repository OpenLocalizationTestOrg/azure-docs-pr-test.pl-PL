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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Jak toouse Azure pamięci podręcznej Redis za pomocą języka Node.js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Zapewnia pamięci podręcznej Redis Azure, możesz uzyskać dostęp tooa bezpiecznego, dedykowane pamięć podręczna Redis, zarządzany przez firmę Microsoft. Pamięć podręczna jest dostępna z poziomu dowolnej aplikacji na platformie Microsoft Azure.

W tym temacie przedstawiono sposób uruchamiania tooget z pamięci podręcznej Redis Azure za pomocą środowiska Node.js. Inny przykład użycia pamięci podręcznej Redis Azure w środowisku Node.js można znaleźć w temacie [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md) (Tworzenie aplikacji czatu środowiska Node.js za pomocą biblioteki Socket.IO w witrynie sieci Web platformy Azure).

## <a name="prerequisites"></a>Wymagania wstępne
Zainstaluj klienta [node_redis](https://github.com/mranney/node_redis):

    npm install redis

W tym samouczku jest używany klient [node_redis](https://github.com/mranney/node_redis). Przykłady użycia innych klientów Node.js, w dokumentacji hello poszczególnych klientów Node.js hello wymienione na [Node.js Redis klientów](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Tworzenie pamięci podręcznej Redis na platformie Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Pobieranie hello hosta nazwy i dostępu do kluczy
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Połączenie pamięci podręcznej toohello przy użyciu protokołu SSL
Najnowsza wersja kompilacji Hello [node_redis](https://github.com/mranney/node_redis) zapewniają obsługę łączenie tooAzure pamięci podręcznej Redis przy użyciu protokołu SSL. Witaj poniższy przykład pokazuje, jak przy użyciu pamięci podręcznej Redis tooAzure tooconnect hello punkt końcowy SSL 6380. Zastąp `<name>` o nazwie hello pamięć podręczną i `<key>` przy użyciu jednej klucz podstawowy lub pomocniczy zgodnie z opisem w hello poprzedniej [pobrać hello nazwy i dostęp za pomocą klucza hosta](#retrieve-the-host-name-and-access-keys) sekcji.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> port bez protokołu SSL Hello jest wyłączona dla nowego wystąpienia pamięci podręcznej Redis Azure. Jeśli korzystasz z innego klienta, który nie obsługuje protokołu SSL, zobacz [jak tooenable hello portu bez protokołu SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Dodaj element toohello pamięci podręcznej i pobranie
powitania po przykładzie pokazano, jak Redis Azure tooconnect tooan pamięci podręcznej wystąpienia i przechowywania i pobierania elementu z pamięci podręcznej hello. Więcej przykładów dotyczących przy użyciu pamięci podręcznej Redis z hello [node_redis](https://github.com/mranney/node_redis) klienta, zobacz [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Dane wyjściowe:

    OK
    value


## <a name="next-steps"></a>Następne kroki
* [Włącz diagnostykę w pamięci podręcznej](cache-how-to-monitor.md#enable-cache-diagnostics) można więc [monitor](cache-how-to-monitor.md) hello kondycji pamięci podręcznej.
* Oficjalne hello odczytu [Redis dokumentacji](http://redis.io/documentation).

