---
title: "Przykłady pamięci podręcznej Redis aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure pamięci podręcznej Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Przykłady pamięci podręcznej Redis Azure
Ten temat zawiera listę próbek pamięć podręczna Redis Azure, obejmujące scenariusze, takie jak łączenie tooa pamięci podręcznej, odczytywanie i zapisywanie tooand danych z pamięci podręcznej i przy użyciu dostawców pamięci podręcznej Redis ASP.NET hello. Niektóre przykłady hello są projekty do pobrania, a niektóre zawierają wskazówki krok po kroku i zawierać fragmentów kodu, ale nie łączy tooa projektu do pobrania.

## <a name="hello-world-samples"></a>Witaj świecie próbek
Przykłady Hello w tej sekcji Pokaż podstawy hello łączenie tooan wystąpienia pamięci podręcznej Redis Azure i odczytywanie i zapisywanie pamięci podręcznej toohello danych przy użyciu różnych języków i Redis klientów.

Witaj [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) przykładowe pokazuje, jak tooperform różnych pamięci podręcznej operacji za pomocą hello [programie StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) klienta .NET.

W tym przykładzie pokazano sposób:

* Użyj różnych opcji połączenia
* Odczyt i zapis tooand obiektów z pamięci podręcznej hello przy użyciu operacje synchroniczne i asynchroniczne
* Użyj polecenia Redis MGET/MSET tooreturn wartości określone klucze
* Wykonywanie operacji transakcyjnych z pamięci podręcznej Redis
* Praca z listy Redis i posortowane zestawów
* Przechowywania obiektów platformy .NET przy użyciu serializatorów JsonConvert
* Użycie pamięci podręcznej Redis ustawia znakowanie tooimplement
* Praca z pamięci podręcznej Redis klastra

Aby uzyskać więcej informacji, zobacz hello [programie StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) dokumentacji w witrynie github i dla scenariuszy użycia Zobacz hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) testów jednostkowych.

[Jak toouse Azure pamięci podręcznej Redis języka Python](cache-python-get-started.md) pokazuje, jak tooget pracę z pamięci podręcznej Redis Azure za pomocą języka Python i hello [redis py](https://github.com/andymccurdy/redis-py) klienta.

[Praca z obiektami .NET w pamięci podręcznej hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) pokazuje obiekty można jednokierunkowej tooserialize .NET, użytkownik może zapisać tooand z nimi zapoznać z wystąpienia pamięci podręcznej Redis Azure. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>Używanie pamięci podręcznej Redis jako płyty montażowej skalowania SignalR platformy ASP.NET
Witaj [użycia pamięci podręcznej Redis jako skalowania płyty montażowej dla produktu ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) przykładzie pokazano, jak skorzystać z pamięci podręcznej Redis Azure jako płyty montażowej SignalR. Aby uzyskać więcej informacji na temat płyty montażowej, zobacz [skalowania SignalR z pamięci podręcznej Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).

## <a name="redis-cache-customer-query-sample"></a>Przykładowe zapytania klienta pamięci podręcznej redis
W tym przykładzie przedstawiono porównanie wydajności między dostęp do danych z pamięci podręcznej i uzyskiwanie dostępu do danych z magazynu trwałości. Ten przykład ma dwa projekty.

* [Pokaz, jak poprawić wydajność przez buforowanie danych pamięci podręcznej Redis](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [Inicjatora hello bazy danych i pamięci podręcznej dla pokaz hello](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>Stan sesji programu ASP.NET i buforowanie danych wyjściowych
Witaj [toostore pamięci podręcznej Redis Azure Użyj ASP.NET SessionState i OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) przykładzie pokazano, jak można toouse pamięć podręczna Redis Azure toostore sesji programu ASP.NET i pamięci podręcznej danych wyjściowych z użyciem hello SessionState i OutputCache dostawców dla Pamięci podręcznej redis.

## <a name="manage-azure-redis-cache-with-maml"></a>Zarządzanie z MAML pamięć podręczna Azure Redis
Hello [zarządzania pamięcią podręczną Redis Azure za pomocą biblioteki zarządzania Azure](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) przykładzie pokazano, jak można użyć bibliotek usługi Azure Management toomanage - (Utwórz / zaktualizuj / delete) pamięci podręcznej. 

## <a name="custom-monitoring-sample"></a>Niestandardowa monitorowania próbki
Witaj [dostępu Redis monitorowanie pamięci podręcznej danych](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) przykładzie pokazano, jak można pobrać danych monitorowania dla pamięć podręczną Redis Azure poza hello portalu Azure.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>Klon stylu serwisu Twitter napisane przy użyciu języka PHP i pamięci podręcznej Redis
Witaj [Retwis](https://github.com/SyntaxC4-MSFT/retwis) próbka jest hello Redis Hello World. Jest minimalnym klonowania sieci społecznościowych stylu serwisu Twitter napisane przy użyciu pamięci podręcznej Redis i PHP przy użyciu hello [Predis](https://github.com/nrk/predis) klienta. Kod źródłowy Hello jest zaprojektowana toobe bardzo proste i na powitania sam czasu tooshow różnych struktur danych Redis.

## <a name="bandwidth-monitor"></a>Monitor przepustowości
Witaj [monitor przepustowości](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) próbki pozwala toomonitor hello przepustowość na powitania klienta. toomeasure hello przepustowości Uruchom próbkę hello na komputerze klienckim pamięci podręcznej hello, upewnij toohello wywołań w pamięci podręcznej, a obserwować przepustowości hello zgłoszone przez hello przepustowości monitor próbki.

