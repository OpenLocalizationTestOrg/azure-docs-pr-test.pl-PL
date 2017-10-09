---
title: "tootroubleshoot aaaHow pamięć podręczna Redis Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooresolve typowe problemy związane z pamięcią podręczną Redis Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>Jak tootroubleshoot Azure pamięci podręcznej Redis
Ten artykuł zawiera wskazówki dotyczące rozwiązywania hello następujące kategorie problemy z pamięcią podręczną Redis Azure.

* [Rozwiązywanie problemów po stronie klienta](#client-side-troubleshooting) — ta sekcja zawiera wskazówki dotyczące identyfikowania i rozwiązywania problemów spowodowanych aplikacji hello łączenie tooAzure pamięci podręcznej Redis.
* [Rozwiązywanie problemów po stronie serwera](#server-side-troubleshooting) — ta sekcja zawiera wskazówki dotyczące identyfikowania i rozwiązywania problemów spowodował na powitania po stronie serwera pamięci podręcznej Redis Azure.
* [Wyjątków przekroczenia limitu czasu w programie StackExchange.Redis](#stackexchangeredis-timeout-exceptions) — ta sekcja zawiera informacje dotyczące rozwiązywania problemów, gdy za pomocą hello programie StackExchange.Redis klienta.

> [!NOTE]
> Kilka kroków w tym przewodniku rozwiązywania problemów hello instrukcje toorun Redis poleceń i monitorować różne metryki wydajności. Aby uzyskać więcej informacji oraz instrukcje, zobacz artykuły hello w hello [dodatkowe informacje](#additional-information) sekcji.
> 
> 

## <a name="client-side-troubleshooting"></a>Rozwiązywanie problemów po stronie klienta
W tej sekcji omówiono rozwiązywanie problemów, które wynika z warunkiem na powitania klienta aplikacji.

* [Wykorzystania pamięci na powitania klienta](#memory-pressure-on-the-client)
* [Serii ruchu](#burst-of-traffic)
* [Klient wysokie użycie procesora CPU](#high-client-cpu-usage)
* [Przekroczona przepustowość po stronie klienta](#client-side-bandwidth-exceeded)
* [Rozmiar dużych żądania/odpowiedzi](#large-requestresponse-size)
* [Jakie wystąpiły toomy dane w pamięci podręcznej Redis?](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>Wykorzystania pamięci na powitania klienta
#### <a name="problem"></a>Problem
Wykorzystania pamięci na komputerze klienckim hello prowadzi tooall rodzaje problemów z wydajnością, które mogą opóźnić proces przetwarzania danych, który został wysłany przez wystąpienie pamięci podręcznej Redis hello bez opóźnień. Gdy liczba trafień wykorzystania pamięci, hello system zwykle ma toopage dane z pamięci toovirtual pamięci fizycznej, która znajduje się na dysku. To *spowodowaniem błędu strony* przyczyny hello tooslow systemu dół znacznie.

#### <a name="measurement"></a>Miary
1. Monitorowanie użycia pamięci w komputerze toomake się, że nie przekracza ilość dostępnej pamięci. 
2. Monitor hello `Page Faults/Sec` licznika wydajności. Większość systemów będzie mieć niektórych błędów stron nawet podczas normalnego działania, tak obserwowania maksymalnej ten licznik wydajności błędów strony, które odpowiadają przekroczeń limitu czasu.

#### <a name="resolution"></a>Rozwiązanie
Uaktualnić klienta większy rozmiar maszyny Wirtualnej więcej pamięci tooa klienta lub dig do consuption użycia pamięci tooreduce wzorce z pamięci.

### <a name="burst-of-traffic"></a>Serii ruchu
#### <a name="problem"></a>Problem
Seria ruchu w połączeniu z słaby `ThreadPool` ustawień może spowodować opóźnienia w przetwarzaniu danych już wysłane przez powitania serwera Redis, ale nie została jeszcze używane na powitania po stronie klienta.

#### <a name="measurement"></a>Miary
Monitor jak Twoje `ThreadPool` statystyki zmieniać przy użyciu kodu [podobny](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs). Można również sprawdzić hello `TimeoutException` wiadomości w programie StackExchange.Redis. Oto przykład:

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

Hello powyżej wiadomości istnieją pewne problemy, które mogą być interesujące:

1. Zwróć uwagę, że hello w `IOCP` sekcji i hello `WORKER` sekcji masz `Busy` wartość, która jest większa niż hello `Min` wartość. Oznacza to, że Twoje `ThreadPool` ustawienia należy dostosowywania.
2. Możesz również sprawdzić `in: 64221`. Oznacza to, że 64211 bajtów odbieranych w hello jądra SSL, ale jeszcze nie zostały przeczytane przez aplikację hello (np. programie StackExchange.Redis). Zwykle oznacza to, że aplikacja będą nie jest odczytywania danych z hello sieci tak szybko, jak hello serwer wysyła on tooyou.

#### <a name="resolution"></a>Rozwiązanie
Konfigurowanie sieci [ustawienia puli wątków](https://gist.github.com/JonCole/e65411214030f0d823cb) toomake się upewnić, że w puli wątków będzie skalowanie w górę szybko w obszarze serii scenariuszy.

### <a name="high-client-cpu-usage"></a>Klient wysokie użycie procesora CPU
#### <a name="problem"></a>Problem
Wysokie użycie procesora CPU na powitania klienta jest wskazanie, że hello system nie może nadążyć z pracą hello, że ma został poproszony tooperform. Oznacza to, że powitania klienta może się nie powieść tooprocess odpowiedzi z pamięci podręcznej Redis w odpowiednim czasie, mimo że Redis wysyłane odpowiedzi hello bardzo szybko.

#### <a name="measurement"></a>Miary
Witaj Monitor użycia Procesora szeroki systemu za pośrednictwem portalu Azure hello lub hello skojarzonego licznika wydajności. Należy zachować ostrożność nie toomonitor *procesu* Procesora, ponieważ jeden proces może mieć niskie użycie Procesora hello sam czasu, że całego systemu Procesora może być wysokie. Obserwowania maksymalnej wykorzystania Procesora, które odpowiadają przekroczeń limitu czasu. Wyniku wysokiej Procesora może również zostać wyświetlony wysokiego `in: XXX` wartości w `TimeoutException` komunikaty o błędach zgodnie z opisem w hello [serii ruchu](#burst-of-traffic) sekcji.

> [!NOTE]
> Programie StackExchange.Redis 1.1.603 i nowszych obejmują hello `local-cpu` metryki w `TimeoutException` komunikaty o błędach. Upewnij się, używając najnowszej wersji hello hello [pakietu NuGet w programie StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/). Istnieją błędy stale ustalone w toomake kodu hello go bardziej niezawodne tootimeouts tak ważne jest posiadanie hello najnowszej wersji.
> 
> 

#### <a name="resolution"></a>Rozwiązanie
Uaktualnij tooa większy rozmiar maszyny Wirtualnej o większej pojemności procesora CPU lub zbadać przyczynę nagłego procesora CPU. 

### <a name="client-side-bandwidth-exceeded"></a>Przekroczona przepustowość po stronie klienta
#### <a name="problem"></a>Problem
Komputery klienckie o rozmiarze różnych podlegają ograniczeniom na przepustowość sieci, ile mają one dostępne. Jeśli powitania klienta przekracza hello dostępnej przepustowości, a następnie dane nie zostaną przetworzone po stronie klienta hello tak szybko, jak serwer hello wysyła go. Może to spowodować tootimeouts.

#### <a name="measurement"></a>Miary
Monitorowanie, w jaki sposób zmienić wykorzystanie przepustowości sieci w czasie przy użyciu kodu [podobny](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs). Należy pamiętać, że ten kod, mogą nie działać prawidłowo w niektórych środowiskach z ograniczonymi uprawnieniami (np. witryny sieci web platformy Azure).

#### <a name="resolution"></a>Rozwiązanie
Zwiększ rozmiar maszyny Wirtualnej klienta lub zmniejszyć wykorzystanie przepustowości sieci.

### <a name="large-requestresponse-size"></a>Rozmiar dużych żądania/odpowiedzi
#### <a name="problem"></a>Problem
Duże żądanie/odpowiedź może spowodować przekroczeń limitu czasu. Na przykład załóżmy, że skonfigurowany na komputerze klienckim wartość limitu czasu wynosi 1 s. Aplikacja żąda dwa klucze (np. "A" i "B") na powitania tym samym czasie (przy użyciu hello tego samego połączenia sieci fizycznej). Większość klientów obsługuje "Pipelining" żądań, w taki sposób, że zarówno żądania "A" i "B" są wysyłane na serwerze hello toohello danych przesyłanych w sieci, jeden po hello innych bez oczekiwania na odpowiedzi hello. Witaj serwer będzie wysyłał hello odpowiedzi z powrotem w hello sam kolejności. Jeśli odpowiedzi "A" jest duży wystarczająco go pochłaniają większość hello przekroczenia limitu czasu dla kolejnych żądań. 

Witaj poniższy przykład pokazuje, w tym scenariuszu. W tym scenariuszu żądania "" i "B" są wysyłane szybkiego hello serwer jest uruchamiany szybkie wysyłanie odpowiedzi na "A" i "B", ale z powodu czasu przesyłania danych, 'B' zatrzymywane za hello inne żądania i limit, mimo że hello serwer zwrócił szybko.

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>Miary
To jest trudne, co toomeasure. Zasadniczo masz tooinstrument Twojego kodu tootrack dużych żądań i odpowiedzi. 

#### <a name="resolution"></a>Rozwiązanie
1. Redis jest zoptymalizowana pod kątem dużą liczbę małych wartości, zamiast kilku dużych wartości. Witaj preferowane się, że rozwiązanie jest toobreak danych do powiązanych mniejsze wartości. Zobacz hello [co to jest zakres rozmiar idealny wartość hello redis? 100KB jest za duży? ](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) post szczegółowe wokół Dlaczego zalecane są mniejsze wartości.
2. Zwiększ rozmiar hello maszyny wirtualnej (w przypadku klienta i serwera pamięci podręcznej Redis) tooget wyższej przepustowości możliwości, zmniejszając danych transfer razy większy odpowiedzi. Należy pamiętać, tym wprowadzenie większą przepustowość na właśnie powitania serwera lub tylko na powitania klienta może nie być wystarczająca. Zmierz wykorzystanie przepustowości sieci i porównania go możliwości toohello hello rozmiaru maszyny wirtualnej ma obecnie.
3. Zwiększ liczbę hello `ConnectionMultiplexer` obiekty są użycia i okrężnego żądań za pośrednictwem różnych połączeń.

### <a name="what-happened-toomy-data-in-redis"></a>Jakie wystąpiły toomy dane w pamięci podręcznej Redis?
#### <a name="problem"></a>Problem
Oczekiwana dla niektórych danych toobe w mojej wystąpienia pamięci podręcznej Redis Azure, ale nie wydaje się toobe.

#### <a name="resolution"></a>Rozwiązanie
Zobacz [wystąpił toomy danych w pamięci podręcznej Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) możliwe przyczyny i rozwiązania.

## <a name="server-side-troubleshooting"></a>Rozwiązywanie problemów po stronie serwera
W tej sekcji omówiono rozwiązywanie problemów, które wynika z warunkiem na powitania serwera pamięci podręcznej.

* [Wykorzystania pamięci na powitania serwera](#memory-pressure-on-the-server)
* [Wysokie użycie procesora CPU / ładowania serwera](#high-cpu-usage-server-load)
* [Przekroczona przepustowość po stronie serwera](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>Wykorzystania pamięci na powitania serwera
#### <a name="problem"></a>Problem
Wykorzystania pamięci na powitania po stronie serwera prowadzi tooall rodzaje problemów z wydajnością, które mogą opóźnić proces przetwarzania żądania. Gdy liczba trafień wykorzystania pamięci, hello system zwykle ma toopage dane z pamięci toovirtual pamięci fizycznej, która znajduje się na dysku. To *spowodowaniem błędu strony* przyczyny hello tooslow systemu dół znacznie. Istnieje kilka możliwych przyczyn tego wykorzystania pamięci: 

1. Pojemność toofull pamięci podręcznej hello wypełnione z danymi. 
2. Redis ma do czynienia fragmentacji pamięci wysokiej - Najczęstszą przyczyną przechowywania dużych obiektów (Redis jest zoptymalizowana pod kątem małych obiektów — Zobacz hello [co to jest zakres rozmiar idealny wartość hello redis? 100KB jest za duży? ](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) post, aby uzyskać szczegółowe informacje). 

#### <a name="measurement"></a>Miary
Redis przedstawia dwa metryk, które mogą ułatwić identyfikację ten problem. najpierw jest Hello `used_memory` i innych hello jest `used_memory_rss`. [Te metryki](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) są dostępne w portalu Azure hello lub za pośrednictwem hello [Redis informacji](http://redis.io/commands/info) polecenia.

#### <a name="resolution"></a>Rozwiązanie
Istnieje kilka możliwych zmian umożliwia użycie pamięci Zachowaj toohelp dobrej kondycji:

1. [Skonfiguruj zasady pamięci](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) i ustaw czas wygaśnięcia w Twoje klucze. Należy pamiętać, że to może nie być wystarczające, jeśli masz fragmentacji.
2. [Skonfiguruj wartość maxmemory zastrzeżone](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) który jest wystarczająco duży toocompensate fragmentacji pamięci.
3. Rozdziel dużych obiektów pamięci podręcznej w mniejszych powiązanych obiektów.
4. [Skala](cache-how-to-scale.md) tooa większy rozmiar pamięci podręcznej.
5. Jeśli używasz [premium pamięci podręcznej Redis klastra włączone](cache-how-to-premium-clustering.md) można [zwiększyć liczbę hello odłamków](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache).

### <a name="high-cpu-usage--server-load"></a>Wysokie użycie procesora CPU / ładowania serwera
#### <a name="problem"></a>Problem
Wysokie użycie Procesora może oznaczać, że powitania po stronie klienta może zakończyć się niepowodzeniem tooprocess odpowiedzi z pamięci podręcznej Redis w odpowiednim czasie, mimo że Redis wysyłane odpowiedzi hello bardzo szybko.

#### <a name="measurement"></a>Miary
Witaj Monitor użycia Procesora szeroki systemu za pośrednictwem portalu Azure hello lub hello skojarzonego licznika wydajności. Należy zachować ostrożność nie toomonitor *procesu* Procesora, ponieważ jeden proces może mieć niskie użycie Procesora hello sam czasu, że całego systemu Procesora może być wysokie. Obserwowania maksymalnej wykorzystania Procesora, które odpowiadają przekroczeń limitu czasu.

#### <a name="resolution"></a>Rozwiązanie
[Skala](cache-how-to-scale.md) tooa większą pamięć podręczną warstwy o większej pojemności procesora CPU lub zbadać, co jest przyczyną nagłego procesora CPU. 

### <a name="server-side-bandwidth-exceeded"></a>Przekroczona przepustowość po stronie serwera
#### <a name="problem"></a>Problem
Wystąpienia inny rozmiar pamięci podręcznej mieć ograniczenia na przepustowość sieci, ile mają one dostępne. Jeśli serwera hello przekracza dostępną przepustowość hello, następnie zostanie nie można wysłać danych klienta toohello tak szybko. Może to spowodować tootimeouts.

#### <a name="measurement"></a>Miary
Można monitorować hello `Cache Read` metryki, czyli hello ilość danych odczytu z pamięci podręcznej hello w MB na sekundę (MB/s) w określonym interwale raportowania hello. Ta wartość odpowiada toohello przepustowość sieci używanych przez pamięć podręczną. Jeśli chcesz tooset alerty dla limity przepustowości sieci po stronie serwera, można utworzyć je za pomocą tej `Cache Read` licznika. Porównaj z odczyty z wartościami hello w [tej tabeli](cache-faq.md#cache-performance) dla hello obserwowanych limity przepustowości dla różnych pamięci podręcznej ceny warstw i rozmiary.

#### <a name="resolution"></a>Rozwiązanie
Jeśli jesteś spójnie niemal hello obserwowanych maksymalną przepustowość dla cenową rozmiar warstwy i pamięci podręcznej, należy wziąć pod uwagę [skalowanie](cache-how-to-scale.md) tooa cen warstwy lub rozmiar, która ma większą przepustowość sieci, używając wartości hello w [tej tabeli](cache-faq.md#cache-performance) jako przewodnika.

## <a name="stackexchangeredis-timeout-exceptions"></a>Wyjątków przekroczenia limitu czasu w programie StackExchange.Redis
Programie StackExchange.Redis używa konfiguracji ustawienie o nazwie `synctimeout` dla operacji synchronicznych, które ma wartość domyślną 1000 ms. Jeśli wywołania synchronicznego nie została zakończona w hello ustalić czas hello programie StackExchange.Redis klienta zgłasza limitu czasu błąd toohello podobne, poniższy przykład.

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


Ten komunikat o błędzie zawiera metryki, które pozwalają wskazać przyczynę i możliwe rozwiązania toohello hello problemu. Witaj Poniższa tabela zawiera szczegółowe informacje o hello błąd komunikat metryki.

| Metryka komunikat błędu | Szczegóły |
| --- | --- |
| inst |W hello ostatni przedział czasu: 0 polecenia zostały wydane |
| Mgr |Menedżer gniazda Hello wykonuje `socket.select` co oznacza, że jest zapytaniem tooindicate hello systemu operacyjnego gniazda, który ma element toodo; zasadniczo: hello czytnik nie jest aktywnie odczytu z sieci hello w ponieważ go nie wziąć pod uwagę coś toodo |
| Kolejki |73 całkowita operacji w toku |
| Ustawienia kol |6 hello w trakcie wykonywania operacji w kolejce niewysłane hello i nie zostały jeszcze jeszcze zapisane toohello wychodzących sieci |
| QS |67 he trwające operacje zostały wysłane toohello serwera, ale odpowiedź nie jest jeszcze dostępna. Witaj odpowiedzi może być `Not yet sent by hello server` lub`sent by hello server but not yet processed by hello client.` |
| QC |0 hello w trakcie wykonywania operacji odpowiedzi jak już wspomniano, ale nie jeszcze zostały oznaczone jako zakończone powodu toowaiting hello zakończenia pętli |
| wR |Brak aktywnych składnika zapisywania (co oznacza hello 6 niewysłane żądania nie są ignorowane) bajty/activewriters |
| W |Nie ma żadnych aktywnych czytników i zero bajtów są dostępne toobe odczytu na powitania kart bajty/activereaders |

### <a name="steps-tooinvestigate"></a>Kroki tooinvestigate
1. Jako najlepsze rozwiązanie upewnij się, że używasz powitania po tooconnect wzorzec, korzystając z klienta programie StackExchange.Redis hello.

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    Aby uzyskać więcej informacji, zobacz [połączyć toohello pamięci podręcznej za pomocą programie StackExchange.Redis](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).

1. Upewnij się, że pamięć podręczna Redis Azure i aplikacji klienckiej hello są w hello tego samego regionu w systemie Azure. Na przykład możesz może występować limity czasu gdy pamięć podręczna jest wschodnie stany USA, ale klient hello jest zachodnie stany USA i hello żądania nie zakończyła się w ciągu hello `synctimeout` interwał lub użytkownik może uzyskać przekroczeń limitu czasu podczas debugowania z komputera lokalnego rozwoju. 
   
    Jest zdecydowanie zalecane toohave hello w pamięci podręcznej, a w kliencie hello w hello sam region platformy Azure. Jeśli scenariusz, który zawiera wywołań między regionu, należy ustawić hello `synctimeout` interwał tooa wartość większą niż hello domyślny 1000 ms interwał, umieszczając w niej `synctimeout` właściwości w parametrach połączenia hello. Witaj poniższy przykład przedstawia fragment ciągu połączenia programie StackExchange.Redis pamięci podręcznej z `synctimeout` z 2000 ms.
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. Upewnij się, używając najnowszej wersji hello hello [pakietu NuGet w programie StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/). Istnieją błędy stale ustalone w toomake kodu hello go bardziej niezawodne tootimeouts tak ważne jest posiadanie hello najnowszej wersji.
3. W przypadku żądań pobierania powiązanych przez ograniczenia przepustowości na powitania serwera lub klienta będzie trwało dłużej dla nich toocomplete i spowodować przekroczeń limitu czasu. toosee Twojego limitu czasu jest powodu toonetwork przepustowość na powitania serwera, zobacz [Przekroczona przepustowość po stronie serwera](#server-side-bandwidth-exceeded). toosee w przypadku czasu z powodu tooclient przepustowość sieci, zobacz [Przekroczona przepustowość po stronie klienta](#client-side-bandwidth-exceeded).
4. Na serwerze hello lub na powitania klienta możesz pobierania Procesora powiązanych?
   
   * Sprawdź, czy możesz pobierania powiązanych przez procesor CPU na komputerze klienckim, co może spowodować hello toonot żądania przetwarzane w ramach hello `synctimeout` interwał, powodując przekroczenie limitu czasu. Przenoszenie tooa większego rozmiaru klienta lub dystrybucji obciążenia hello może pomóc toocontrol to. 
   * Sprawdź, czy występują procesora CPU związane na powitania serwera monitorowania hello `CPU` [pamięci podręcznej metryki wydajności](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Żądań przychodzących, gdy Redis jest powiązane z Procesora może powodować te żądania tootimeout. tooaddress to można rozpowszechniać hello obciążenia w wielu fragmentów w pamięci podręcznej premium lub uaktualnienie tooa większy rozmiar lub warstwy cenowej. Aby uzyskać więcej informacji, zobacz [Przekroczona przepustowość po stronie serwera](#server-side-bandwidth-exceeded).
5. Istnieją polecenia biorąc tooprocess dużo czasu na powitania serwera? Czas uruchamiania poleceń, które trwa długo tooprocess na serwer redis hello może spowodować przekroczeń limitu czasu. Oto kilka przykładów poleceń długotrwała `mget` z dużą liczbę kluczy, `keys *` lub niepoprawnie napisane skrypty lua. Możesz połączyć tooyour wystąpienia pamięci podręcznej Redis Azure za pomocą klienta infrastruktury cli redis hello lub użyć hello [Redis konsoli](cache-configure.md#redis-console) i wykonywania hello [SlowLog](http://redis.io/commands/slowlog) toosee polecenia, jeśli istnieją żądania trwa dłużej niż oczekiwano. Serwer redis i programie StackExchange.Redis są zoptymalizowane pod kątem wiele żądań małych zamiast mniej dużych żądania. Podział na mniejsze fragmenty danych może zwiększyć rzeczy w tym miejscu. 
   
    Informacje dotyczące łączenia punkt końcowy SSL pamięci podręcznej Redis Azure toohello przy użyciu interfejsu wiersza polecenia redis i stunnel, zobacz hello [Announcing ASP.NET dostawcę stanu sesji dla wersji zapoznawczej Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) wpis w blogu. Aby uzyskać więcej informacji, zobacz [SlowLog](http://redis.io/commands/slowlog).
6. Wysokie obciążenie serwera pamięci podręcznej Redis może spowodować przekroczeń limitu czasu. Można monitorować obciążenie serwera hello monitorowania hello `Redis Server Load` [pamięci podręcznej metryki wydajności](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Obciążenie serwera, 100 (wartość maksymalna) oznacza, czy ten serwer redis hello został zajęty, bez czasu bezczynności, przetwarzanie żądań. toosee w przypadku niektórych żądań zajmują się wszystkich funkcji serwera hello, uruchom polecenie SlowLog hello, zgodnie z opisem w poprzednim akapicie hello. Aby uzyskać więcej informacji, zobacz [użycie procesora CPU wysoka / Server załadować](#high-cpu-usage-server-load).
7. Na powitania po stronie klienta, który może to być spowodowane blip sieci były inne zdarzenia? Sprawdź na powitania klienta (sieć web, rolę procesu roboczego lub maszyn wirtualnych Iaas), jeśli został zdarzeń, takich jak skalowanie hello liczbą wystąpień klienta w górę lub w dół lub wdrażania nowej wersji klienta hello lub automatyczne skalowanie jest włączone? Podczas testów zostały znalezione, może spowodować błąd automatycznego skalowania lub skalowanie w górę/dół łączności sieciowej wychodzącego mogą zostać utracone przez kilka sekund. Kod programie StackExchange.Redis jest odporność toosuch zdarzeń i połączy się ponownie. W tym czasie ponowne połączenie żądań w kolejce hello może upłynął limit czasu.
8. Były poprzedzających kilka toohello małych żądań pamięci podręcznej Redis, który upłynął limit czasu żądania duży? Witaj parametru `qs` omyłkowo hello komunikat informujący, ile żądań zostały wysłane z powitania klienta toohello serwera, ale odpowiedź nie jest jeszcze przetworzone. Ta wartość może rosnące, ponieważ w programie StackExchange.Redis używa pojedynczego połączenia TCP i może odczytać tylko jedna odpowiedź w czasie. Mimo że przekroczono limit czasu operacji pierwszy hello, nie zatrzymuje hello dane wysyłane z serwera hello, a inne żądania są zablokowane, aż do jej zakończeniu, co powoduje limity czasu. Jedno rozwiązanie jest ryzyko hello toominimize limitów czasu zapewnia, że pamięć podręczna jest wystarczająco duży dla obciążenia i dzielenia dużych wartości na mniejsze fragmenty. Innym rozwiązaniem możliwe jest toouse puli `ConnectionMultiplexer` obiektów na kliencie, a następnie wybierz pozycję hello najmniej załadować `ConnectionMultiplexer` wysyłając żądanie nowego. To powinno zapobiec pojedynczego limitu czasu powoduje timeout tooalso innych żądań.
9. Jeśli używasz `RedisSessionStateprovider`, upewnij się, ma limit ponownych prób hello zostały prawidłowo skonfigurowane. `retrytimeoutInMilliseconds`powinien być większy niż `operationTimeoutinMilliseonds`, w przeciwnym razie wystąpi brak ponownych prób. W hello poniższy przykład `retrytimeoutInMilliseconds` ustawiono too3000. Aby uzyskać więcej informacji, zobacz [dostawcę stanu sesji ASP.NET dla pamięci podręcznej Redis Azure](cache-aspnet-session-state-provider.md) i [jak toouse hello parametry konfiguracji dostawcy stanu sesji i dostawcy wyjściowej pamięci podręcznej](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration).

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. Sprawdź użycie pamięci na serwerze usługi pamięć podręczna Redis Azure hello przez [monitorowania](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) `Used Memory RSS` i `Used Memory`. Czy zasady wykluczania znajduje się w miejscu, rozpoczyna się Redis wykluczania kluczy podczas `Used_Memory` osiągnie hello rozmiar pamięci podręcznej. W idealnym przypadku `Used Memory RSS` powinny być tylko nieznacznie wyższe niż `Used memory`. Duża różnica oznacza brak fragmentacji pamięci (wewnętrzne lub zewnętrzne. Gdy `Used Memory RSS` jest mniejsza niż `Used Memory`, oznacza to część pamięci podręcznej hello została zapisana przez system operacyjny hello. W takim przypadku można oczekiwać, że niektóre znaczne opóźnienia. Ponieważ Redis nie mają kontrolę nad jak alokacje są mapowane stron toomemory wysokiej `Used Memory RSS` często jest wynikiem hello kolekcji użycia pamięci. Po Redis zwalnia pamięć, pamięci hello jest ponownie określony alokatora toohello i przydzielania hello mogą lub może nie być hello pamięci wstecz toohello systemu. Może być rozbieżności między hello `Used Memory` zużycie wartość i pamięci podaną przez system operacyjny hello. Może być spowodowane fakt toohello pamięci został użyty i wydane przez Redis, ale nie podany wstecz toohello systemu. toohelp chroni przed wykonaniem hello następujące kroki problemy z pamięcią.
   
   * Uaktualnij hello pamięci podręcznej tooa większy rozmiar, aby nie zostały uruchomione w systemie hello sprawdzania ograniczenia ilości pamięci.
   * Ustaw czas wygaśnięcia kluczy hello starsze wartości są aktywne wykluczony.
   * Monitor Witaj Witaj `used_memory_rss` pamięci podręcznej metryki. Ta wartość koloru zbliża się hello rozmiar pamięci podręcznej, są prawdopodobnie toostart wyświetlanie problemy z wydajnością. Rozpowszechniają danych hello wielu odłamków korzystają z usługi pamięć podręczna premium, lub uaktualnieniu tooa większy rozmiar pamięci podręcznej.
   
   Aby uzyskać więcej informacji, zobacz [wykorzystania pamięci na serwerze hello](#memory-pressure-on-the-server).

## <a name="additional-information"></a>Dodatkowe informacje
* [Której oferty i jakiego rozmiaru usługi Redis Cache mam użyć?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [Jak testu wydajności i przetestować hello wydajności Moje pamięci podręcznej?](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Jak uruchomić polecenia Redis?](cache-faq.md#how-can-i-run-redis-commands)
* [Jak toomonitor Azure pamięci podręcznej Redis](cache-how-to-monitor.md)

