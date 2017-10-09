---
title: "aaaHow tooconfigure Redis klastrowania podręczna Redis Azure Premium | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i zarządzanie nimi Redis klastrowania warstwę Premium wystąpienia pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Jak tooconfigure Redis klastrowania podręczna Redis Azure Premium
Pamięć podręczna Redis Azure ma inną pamięci podręcznej oferty, które zapewniają elastyczność w wyborze hello rozmiar pamięci podręcznej i funkcji, łącznie z funkcji warstwy Premium, takich jak klastrowanie, trwałości i obsługi sieci wirtualnej. W tym artykule opisano, jak tooconfigure klastrów w warstwie premium Azure pamięci podręcznej Redis wystąpienia.

Aby uzyskać informacji o innych funkcjach pamięci podręcznej premium, zobacz [warstwy pamięci podręcznej Redis Azure Premium toohello wprowadzenie](cache-premium-tier-intro.md).

## <a name="what-is-redis-cluster"></a>Co to jest Redis klastra?
Pamięć podręczna Redis Azure oferuje klaster Redis jako [zaimplementowana w pamięci podręcznej Redis](http://redis.io/topics/cluster-tutorial). Redis klastra można uzyskać hello następujące korzyści: 

* tooautomatically możliwości Hello podzielić zestawu danych między wieloma węzłami. 
* Hello możliwości toocontinue operacje podczas podzbioru węzłów hello występują błędy lub są toocommunicate z pozostałą hello hello klastra. 
* Więcej przepustowości: przepływności zwiększa liniowo zwiększyć liczbę hello fragmentów. 
* Więcej rozmiar pamięci: zwiększa liniowo zwiększania hello liczbę fragmentów.  

Aby uzyskać więcej informacji o rozmiarze, przepływności i przepustowości z pamięci podręcznych premium, zobacz [jakie oferty pamięć podręczna Redis i rozmiar należy używać?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

Na platformie Azure Redis klastra jest oferowany jako model podstawowy/repliki, gdzie każdy identyfikator niezależnego fragmentu ma parę podstawowy/repliki z replikacją, gdzie replikacji hello jest zarządzane przez usługę pamięć podręczna Redis Azure. 

## <a name="clustering"></a>Klaster
Klaster jest włączona na powitania **nowa pamięć podręczna Redis** bloku podczas tworzenia pamięci podręcznej. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Klaster jest skonfigurowany na powitania **klaster Redis** bloku.

![Klaster][redis-cache-clustering]

Użytkownik może zawierać maksymalnie odłamków too10 hello klastra. Kliknij przycisk **włączone** i przesuń suwak hello, lub wpisz liczbę z zakresu od 1 do 10 dla **liczby niezależnych** i kliknij przycisk **OK**.

Każdy identyfikator niezależnego fragmentu jest zarządzane przez usługę Azure parę pamięć podręczna podstawowy/repliki, a hello całkowity rozmiar pamięci podręcznej hello jest obliczana przez pomnożenie hello liczba odłamków przez wybrany w hello warstwy cenowej rozmiar pamięci podręcznej hello. 

![Klaster][redis-cache-clustering-selected]

Po utworzeniu pamięci podręcznej hello połączyć tooit i użyj go tylko pamięci podręcznej niedziałającego w klastrze, takich jak i Redis dystrybuuje hello danych w całym hello odłamków pamięci podręcznej. W przypadku diagnostyki [włączone](cache-how-to-monitor.md#enable-cache-diagnostics), metryki są przechwytywane osobno dla każdej niezależnych i może być [wyświetlić](cache-how-to-monitor.md) w hello bloku pamięci podręcznej Redis. 

> [!NOTE]
> 
> Istnieją pewne niewielkie różnice w aplikacji klienta wymagane, jeśli klaster jest skonfigurowany. Aby uzyskać więcej informacji, zobacz [należy toomake wszelkie zmiany toomy klienta aplikacji toouse klastra?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Przykładowy kod na temat pracy z usługą klastrowania z hello programie StackExchange.Redis klienta, zobacz hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) część hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) próbki.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>Zmień rozmiar klastra hello na uruchomionej usługi pamięć podręczna premium
rozmiar klastra hello toochange w uruchomionej premium pamięci podręcznej z klastrowania włączone, kliknij przycisk **Redis rozmiar klastra** z hello **zasobów menu**.

> [!NOTE]
> Gdy hello Azure Redis Premium usługi pamięć podręczna została warstwy wydaniu dostępności tooGeneral hello Redis rozmiar klastra funkcja jest obecnie w przeglądzie.
> 
> 

![Rozmiar klastra redis][redis-cache-redis-cluster-size]

rozmiar klastra hello toochange, za pomocą suwaka hello lub wpisz liczbę z zakresu od 1 do 10 w hello **liczby niezależnych** polu tekstowym i kliknij przycisk **OK** toosave.

> [!NOTE]
> Skalowanie klastra działa hello [migracji](https://redis.io/commands/migrate) polecenia, która jest kosztowna polecenia, dlatego dla minimalny wpływ, należy rozważyć uruchomieniem tej operacji podczas godziny poza szczytem. Podczas procesu migracji hello zobaczysz kolekcji w obciążenia serwera. Skalowanie klastra długi działa procesu i hello czas zależy hello liczba kluczy i rozmiar hello wartości związane z tych kluczy.
> 
> 

## <a name="clustering-faq"></a>Klaster — często zadawane pytania
Witaj Poniższa lista zawiera toocommonly odpowiedzi zadawane pytania dotyczące klastrowania pamięć podręczna Redis Azure.

* [Należy toomake wszelkie zmiany toomy klienta aplikacji toouse klastra?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [Jak klucze są rozpowszechniane w klastrze?](#how-are-keys-distributed-in-a-cluster)
* [Co to jest hello największy rozmiar pamięci podręcznej, który można utworzyć?](#what-is-the-largest-cache-size-i-can-create)
* [Wszyscy klienci Redis obsługują klastra?](#do-all-redis-clients-support-clustering)
* [Jak połączyć toomy pamięci podręcznej, gdy włączono klaster?](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [Mogą bezpośrednio łączyć z poszczególnych odłamków toohello Moje pamięci podręcznej?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [Można skonfigurować klaster utworzonej wcześniej pamięci podręcznej?](#can-i-configure-clustering-for-a-previously-created-cache)
* [Można skonfigurować klaster na potrzeby pamięci podręcznej planu basic lub standard?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [Czy można użyć klastrowania z dostawcami hello stanu sesji ASP.NET dla pamięci podręcznej Redis i buforowanie danych wyjściowych](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [Otrzymuję przenoszenie wyjątków, używając programie StackExchange.Redis i klastrowania, co należy zrobić?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>Należy toomake wszelkie zmiany toomy klienta aplikacji toouse klastra?
* Jeśli klaster jest włączone, tylko bazy danych 0 jest dostępna. Jeśli aplikacja kliencka używa wielu baz danych i próbuje tooread zapisu tooa bazy danych lub innych niż 0, hello następującego wyjątku. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  Aby uzyskać więcej informacji, zobacz [Redis specyfikacji klastra - zaimplementowanym podzestawu](http://redis.io/topics/cluster-spec#implemented-subset).
* Jeśli używasz [programie StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), należy użyć 1.0.481 lub nowszym. Połączenie pamięci podręcznej toohello przy użyciu hello sam [punktów końcowych, portów i kluczy](cache-configure.md#properties) używanej podczas łączenia z pamięcią podręczną tooa, która nie ma włączoną funkcją klastrowania. Witaj jedyna różnica polega na tym, że wszystkie odczyty i zapisy musi zostać wykonane toodatabase 0.
  
  * Inni klienci mogą mieć inne wymagania. Zobacz [wszystkich klientów pamięci podręcznej Redis obsługują klastra?](#do-all-redis-clients-support-clustering)
* Jeśli aplikacja używa wielu operacji klucza przetwarzane wsadowo w jedno polecenie, wszystkie klucze musi znajdować się w hello sam identyfikator niezależnego fragmentu. klucze toolocate w hello sam identyfikator niezależnego fragmentu, zobacz [klucze rozkład w klastrze?](#how-are-keys-distributed-in-a-cluster)
* Jeśli używasz dostawcy stanu sesji ASP.NET dla pamięci podręcznej Redis należy użyć 2.0.1 lub nowszej. Zobacz [użyć, klastra z dostawcami stanu sesji ASP.NET dla pamięci podręcznej Redis i buforowanie danych wyjściowych hello?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>Jak klucze są rozpowszechniane w klastrze?
Na powitania Redis [modelu dystrybucji kluczy](http://redis.io/topics/cluster-spec#keys-distribution-model) dokumentacji: hello klucza miejsca jest podzielony na 16384 gniazda. Każdy klucz jest mieszany i przypisane tooone tych gniazd, które są dystrybuowane między węzłami hello hello klastra. Można skonfigurować, która część klucza hello jest skrótem tooensure, w którym znajduje się wiele kluczy w hello sam identyfikator niezależnego fragmentu przy użyciu tagów wyznaczania wartości skrótu.

* Klucze z tagiem skrótu — Jeśli dowolną część klucza hello jest ujęta w `{` i `}`, tylko część klucza hello jest wartość skrótu do celów hello określenia miejsca skrótu hello klucza. Na przykład hello następujące klucze 3 znajduje się w hello sam identyfikator niezależnego fragmentu: `{key}1`, `{key}2`, i `{key}3` od tylko hello `key` część nazwy hello jest wartość skrótu. Pełną listę klawiszy skrótu tag specyfikacji zobacz [klawiszy skrótu tagi](http://redis.io/topics/cluster-spec#keys-hash-tags).
* Klucze bez tagu skrótu - całą nazwę klucza hello jest używany do tworzenia skrótów. W efekcie statystycznie nawet dystrybucji między odłamków hello hello pamięci podręcznej.

Aby uzyskać najlepszą wydajność i przepływność zaleca się dystrybucji kluczy hello równomiernie. Jeśli korzystasz z kluczy z tagiem wyznaczania wartości skrótu jest równomiernie aplikacji hello odpowiedzialność tooensure hello kluczy.

Aby uzyskać więcej informacji, zobacz [modelu dystrybucji kluczy](http://redis.io/topics/cluster-spec#keys-distribution-model), [dzielenia na fragmenty danych Redis klastra](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding), i [klawiszy skrótu tagi](http://redis.io/topics/cluster-spec#keys-hash-tags).

Przykładowy kod na temat pracy z klastra i lokalizowania kluczy w hello sam identyfikator niezależnego fragmentu z hello programie StackExchange.Redis klienta, zobacz hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) część hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) próbki.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>Co to jest hello największy rozmiar pamięci podręcznej, który można utworzyć?
największy rozmiar pamięci podręcznej premium Hello jest 53 GB. Możesz utworzyć zapasowej odłamków too10, umożliwiając maksymalny rozmiar 530 GB. Jeśli potrzebujesz większy rozmiar można [żądania więcej](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). Aby uzyskać więcej informacji, zobacz [cennik usługi Azure Redis pamięci podręcznej](https://azure.microsoft.com/pricing/details/cache/).

### <a name="do-all-redis-clients-support-clustering"></a>Wszyscy klienci Redis obsługują klastra?
Na powitania obecny czas nie obsługiwać klientów pamięci podręcznej Redis klastra. Programie StackExchange.Redis to taki, który obsługuje dla niego. Aby uzyskać więcej informacji na innych klientów, zobacz hello [odtwarzanie z klastrem hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) sekcji hello [samouczek klaster Redis](http://redis.io/topics/cluster-tutorial).

> [!NOTE]
> Jeśli używasz programie StackExchange.Redis jako klienta, upewnij się, używane są hello najnowszą wersję [programie StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 lub nowszej do klastrowania toowork poprawnie. Jeśli masz problemy z wyjątków przenoszenia, zobacz [przenoszenie wyjątków](#move-exceptions) Aby uzyskać więcej informacji.
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>Jak połączyć toomy pamięci podręcznej, gdy włączono klaster?
Możesz połączyć tooyour pamięci podręcznej przy użyciu hello sam [punkty końcowe](cache-configure.md#properties), [porty](cache-configure.md#properties), i [klucze](cache-configure.md#access-keys) używanej podczas łączenia z pamięcią podręczną tooa, która nie ma włączoną funkcją klastrowania. Redis zarządza hello usługi klastrowania na powitania wewnętrznej bazy danych, dzięki czemu nie trzeba toomanage go z tego klienta.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>Mogą bezpośrednio łączyć z poszczególnych odłamków toohello Moje pamięci podręcznej?
To nie jest oficjalnie obsługiwana. Z tym powiedział każdy identyfikator niezależnego fragmentu składa się z pary pamięci podręcznej podstawowy/repliki, nazywanych zbiorczo wystąpienia pamięci podręcznej. Możesz połączyć za pomocą narzędzia interfejsu wiersza polecenia redis hello w hello wystąpienia pamięci podręcznej toothese [niestabilny](http://redis.io/download) gałęzi repozytorium Redis hello w witrynie GitHub. Ta wersja implementuje podstawowa pomoc techniczna podczas pracy z hello `-c` przełącznika. Aby uzyskać więcej informacji, zobacz [odtwarzanie z klastrem hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) na [http://redis.io](http://redis.io) w hello [samouczek klaster Redis](http://redis.io/topics/cluster-tutorial).

Bez protokołu ssl można użyć hello następujące polecenia.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

Dla protokołu ssl, należy zastąpić `1300N` z `1500N`.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>Można skonfigurować klaster utworzonej wcześniej pamięci podręcznej?
Obecnie można włączyć tylko klastra podczas tworzenia pamięci podręcznej. Rozmiar klastra hello można zmienić po utworzeniu hello pamięci podręcznej, ale nie można dodać pamięć podręczna premium tooa klastrowania lub usunąć klastrowanie z pamięci podręcznej premium po utworzeniu hello pamięci podręcznej. Pamięć podręczna premium z włączoną funkcją klastrowania i tylko jeden identyfikator niezależnego fragmentu są inne niż premium pamięci podręcznej hello samej wielkości z klastrowaniem nie.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>Można skonfigurować klaster na potrzeby pamięci podręcznej planu basic lub standard?
Klaster jest dostępna tylko dla pamięci podręcznej premium.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>Czy można użyć klastrowania z dostawcami hello stanu sesji ASP.NET dla pamięci podręcznej Redis i buforowanie danych wyjściowych
* **Dostawcy wyjściowej pamięci podręcznej redis** -żadne zmiany wymagane.
* **Dostawca stanu sesji w pamięci podręcznej redis** -toouse klastrowania, należy użyć [pakietu RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 lub nowszej albo wyjątek zostanie zgłoszony. Jest to istotne zmiany; Aby uzyskać więcej informacji, zobacz [v2.0.0 fundamentalne zmiany szczegółów](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>Otrzymuję przenoszenie wyjątków, używając programie StackExchange.Redis i klastrowania, co należy zrobić?
Jeśli używasz programie StackExchange.Redis i odbierać `MOVE` wyjątków podczas korzystania z klastra, upewnij się, że używasz [programie StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) lub nowszym. Aby uzyskać instrukcje dotyczące konfigurowania programu .NET aplikacji toouse w programie StackExchange.Redis, zobacz [Konfigurowanie klientów pamięci podręcznej hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak toouse premium więcej pamięci podręcznej funkcji.

* [Wprowadzenie toohello pamięci podręcznej Redis Azure Premium warstwy](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







