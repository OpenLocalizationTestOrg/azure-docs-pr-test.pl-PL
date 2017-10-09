---
title: "toomonitor aaaHow pamięć podręczna Redis Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor hello kondycję i wydajność swoich wystąpień w pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>Jak toomonitor Azure pamięci podręcznej Redis
Pamięć podręczna Redis Azure używa [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) tooprovide kilka opcji monitorowania swoich wystąpień w pamięci podręcznej. Można wyświetlić metryki, przypiąć metryki wykresy toohello tablicy startowej, Dostosuj zakres dat i godzin hello monitorowania wykresy, dodać i usunąć metryki z wykresy hello i ustawić alerty, gdy zostaną spełnione określone warunki. Te narzędzia Włącz możesz toomonitor hello kondycji wystąpień z pamięci podręcznej Redis Azure i pomocne w zarządzaniu aplikacjami buforowania.

Metryki dla wystąpienia pamięci podręcznej Redis Azure są zbierane za pomocą hello Redis [informacji](http://redis.io/commands/info) polecenia około dwa razy na minutę i automatycznie przechowywane przez 30 dni (zobacz [eksportowania metryki pamięci podręcznej](#export-cache-metrics) tooconfigure zasady przechowywania różnych), mogą być wyświetlane na wykresach metryki hello i oceniane przez reguły alertów. Aby uzyskać więcej informacji na temat hello różne informacje o wartości używane dla każdego metryki pamięci podręcznej, zobacz [dostępne metryki i raportowania interwałów](#available-metrics-and-reporting-intervals).

<a name="view-cache-metrics"></a>

metryki pamięci podręcznej tooview, [Przeglądaj](cache-configure.md#configure-redis-cache-settings) tooyour wystąpienia pamięci podręcznej w hello [portalu Azure](https://portal.azure.com).  Pamięć podręczna Redis Azure udostępnia niektórych wbudowanych typów wykresów na powitania **omówienie** bloku i hello **Redis metryki** bloku. Każdy wykres można dostosowywać przez dodawanie lub usuwanie metryki i zmienianie hello Interwał raportowania.

![Redis metryk](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>Wyświetl wstępnie skonfigurowanej metryki wykresów

Witaj **omówienie** bloku ma hello następujące wstępnie skonfigurowane wykresy monitorowania.

* [Monitorowanie wykresów](#monitoring-charts)
* [Wykresy użycia](#usage-charts)

### <a name="monitoring-charts"></a>Monitorowanie wykresów
Witaj **monitorowanie** części hello **omówienie** ma bloku **trafienia i Chybienia**, **pobiera i ustawia**, **połączenia**, i **całkowita liczba poleceń** wykresów.

![Monitorowanie wykresów](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>Wykresy użycia
Hello **użycia** części hello **omówienie** ma bloku **obciążenia serwera Redis**, **użycie pamięci**, **przepustowość sieci** , i **użycie procesora CPU** wykresy, a także wyświetla hello **warstwa cenowa** hello wystąpienia pamięci podręcznej.

![Wykresy użycia](./media/cache-how-to-monitor/redis-cache-usage-part.png)

Witaj **warstwa cenowa** Wyświetla hello pamięci podręcznej cen warstwy i mogą być używane za[skali](cache-how-to-scale.md) hello inną warstwa cenowa tooa pamięci podręcznej.

## <a name="view-metrics-with-azure-monitor"></a>Wyświetlaj metryki z Monitorem systemu Azure
tooview Redis metryki i tworzenie wykresów niestandardowych przy użyciu monitora Azure, kliknij przycisk **metryki** z hello **zasobów menu**i dostosować wykres przy użyciu metryk hello potrzebne, raportowanie interwał, typ wykresu i więcej.

![Redis metryk](./media/cache-how-to-monitor/redis-cache-monitor.png)

Aby uzyskać więcej informacji na temat pracy z metryki za pomocą monitora Azure, zobacz [omówienie metryk w Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>Eksportuj metryki pamięci podręcznej
Domyślnie są metryki pamięci podręcznej w monitorze Azure [przechowywane przez 30 dni](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) , a następnie usuwany. toopersist Twojego metryki pamięci podręcznej przez czas dłuższy niż 30 dni, możesz [wyznaczyć konta magazynu](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) i określ **przechowywania (dni)** zasad dla użytkownika metryki pamięci podręcznej. 

tooconfigure konta magazynu dla Twojego metryki pamięci podręcznej:

1. Kliknij przycisk **diagnostyki** z hello **zasobów menu** w hello **pamięci podręcznej Redis** bloku.
2. Kliknij przycisk **na**.
3. Sprawdź **archiwum konta magazynu tooa**.
4. Wybierz konto magazynu hello, w których metryki toostore hello pamięci podręcznej.
5. Sprawdź hello **1 minuta** wyboru i określ **przechowywania (dni)** zasad. Jeśli nie chcesz tooapply dowolne zasady przechowywania i nieograniczony czas przechowywania danych, ustaw **przechowywania (dni)** za**0**.
6. Kliknij pozycję **Zapisz**.

![Redis diagnostyki](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>Dodanie tooarchiving Twojego toostorage metryki pamięci podręcznej, można też [strumienia ich Centrum zdarzeń tooan lub wysyłanie do nich tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

tooaccess Twojego metryki, można je wyświetlić w portalu Azure, jak opisano wcześniej w tym artykule hello i użytkownik może także uzyskiwać do nich dostęp przy użyciu hello [interfejsu API REST Azure Monitor metryki](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

> [!NOTE]
> W przypadku zmiany konta magazynu, dane hello na koncie magazynu hello wcześniej skonfigurowane pozostają dostępne do pobrania, ale nie jest wyświetlana w portalu Azure hello.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>Dostępne metryki i raportowania odstępach czasu
Metryki pamięci podręcznej są zgłaszane przy użyciu kilku raportowania odstępach czasu, w tym **Ostatnia godzina**, **dzisiaj**, **ostatni tydzień**, i **niestandardowy**. Witaj **Metryka** bloku dla każdego wykresu metryki Wyświetla hello średnią, minimalną i maksymalną wartość dla każdego metryki na wykresie hello, a niektóre metryki wyświetlić sumy hello Interwał raportowania. 

Wszystkie metryki obejmuje dwie wersje. Jedna Metryka mierzy wydajności hello całą pamięć podręczną i pamięci podręczne, które używają [klastrowanie](cache-how-to-premium-clustering.md), druga wersja metryki hello, która obejmuje `(Shard 0-9)` hello Nazwa miary wydajności dla jednego niezależnego fragmentu w pamięci podręcznej. Na przykład, jeśli pamięć podręczna ma 4 odłamków `Cache Hits` jest hello łączną ilość trafień dla całą pamięć podręczną hello i `Cache Hits (Shard 3)` jest po prostu hello trafień dla tego niezależnych hello pamięci podręcznej.

> [!NOTE]
> Nawet jeśli hello pamięci podręcznej jest w stanie bezczynności bez żadnych aplikacji podłączonych aktywnych klientów, mogą pojawić się niektóre działania pamięci podręcznej, takich jak połączonych klientów, użycie pamięci i wykonywania operacji. To działanie jest normalne podczas operacji hello wystąpienia pamięci podręcznej Redis Azure.
> 
> 

| Metryka | Opis |
| --- | --- |
| Trafień w pamięci podręcznej |Witaj liczba pomyślnych wyszukiwań klucza w określonym interwale raportowania hello. To pole mapuje zbyt`keyspace_hits` z hello Redis [informacje o](http://redis.io/commands/info) polecenia. |
| Chybienia pamięci podręcznej |Witaj liczba nieudanych klucza wyszukiwania w określonym interwale raportowania hello. To pole mapuje zbyt`keyspace_misses` z hello polecenie Redis informacji. Chybienia pamięci podręcznej nie musi oznaczać, że występuje problem z pamięci podręcznej hello. Na przykład używając hello Zarezerwuj pamięć podręczna programowania wzorca aplikacji wygląda pierwszy w pamięci podręcznej hello elementu. Jeśli hello element nie ma (Chybienie pamięci podręcznej), element hello są pobierane z bazy danych hello oraz dodano toohello pamięci podręcznej dla następnym razem. Chybienia pamięci podręcznej to normalne zachowanie hello Zarezerwuj pamięć podręczna programowania wzorca. Jeśli hello liczba chybień pamięci podręcznej jest większa niż oczekiwano, sprawdź logiki aplikacji hello wypełnia i odczytuje z pamięci podręcznej hello. Jeśli elementy są jest wykluczony z pamięci podręcznej hello powodu wykorzystania toomemory, a następnie może być niektórych Chybienia pamięci podręcznej, ale będzie lepiej toomonitor metryki dla wykorzystania pamięci `Used Memory` lub `Evicted Keys`. |
| Podłączeni klienci |Hello liczba połączeń toohello pamięci podręcznej na kliencie podczas hello określony interwał raportowania. To pole mapuje zbyt`connected_clients` z hello polecenie Redis informacji. Raz hello [limit połączeń](cache-configure.md#default-redis-server-configuration) osiągnięciu kolejne próby połączenia pamięci podręcznej toohello zakończy się niepowodzeniem. Należy pamiętać, że nawet jeśli nie mają żadnych aplikacji aktywnego klienta może jeszcze być kilka wystąpień podłączeni klienci toointernal procesy i połączeń. |
| Wykluczone kluczy |Witaj liczba elementów usunięty z pamięci podręcznej hello podczas hello określony interwał raportowania z powodu toohello `maxmemory` limit. To pole mapuje zbyt`evicted_keys` z hello polecenie Redis informacji. |
| Wygasłe kluczy |Hello liczba elementów wygasł z pamięci podręcznej hello w określonym interwale raportowania hello. Ta wartość mapuje zbyt`expired_keys` z hello polecenie Redis informacji. |
| Wszystkie klucze  | Witaj maksymalna liczba kluczy w pamięci podręcznej hello podczas powitania po okresie raportowania. To pole mapuje zbyt`keyspace` z hello polecenie Redis informacji. Ze względu na ograniczenia tooa hello podstawowy system metryki pamięci podręcznej z usługą klastrowania włączone wszystkie klucze zwraca hello maksymalną liczbę kluczy niezależnych hello, używany hello maksymalną liczbę kluczy w czasie hello Interwał raportowania.  |
| Pobiera |Hello liczba operacji get z pamięci podręcznej hello w określonym interwale raportowania hello. Ta wartość jest suma hello hello następujące wartości z hello Redis informacje o wszystkich poleceń: `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit`, i `cmdstat_getrange`, i jest równoważne toohello sumę trafień w pamięci podręcznej i Chybienia podczas hello Interwał raportowania. |
| Obciążenie serwera redis |Procent Hello cykle, w których hello Redis serwer jest zajęty przetwarzaniem i nie jest oczekiwane bezczynności dla wiadomości. Ten licznik osiągnie wartość 100 oznacza serwera Redis hello osiągnęła limit wydajności i nie może przetwarzać hello Procesora działać wszelkie szybciej. Jeśli widzisz wysokie obciążenie serwera Redis będą widzieć wyjątków przekroczenia limitu czasu w powitania klienta. W takim przypadku należy rozważyć skalowanie w lub partycjonowanie danych w wielu pamięciach podręcznych. |
| Zestawy |numer Hello zestaw operacji toohello w pamięci podręcznej podczas hello określony interwał raportowania. Ta wartość jest suma hello hello następujące wartości z hello Redis informacje o wszystkich poleceń: `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` , a `cmdstat_setnx`. |
| Całkowita liczba operacji |Całkowita liczba przetworzonych przez serwer pamięci podręcznej hello ciągu hello polecenia Hello określony interwał raportowania. Ta wartość mapuje zbyt`total_commands_processed` z hello polecenie Redis informacji. Należy pamiętać, że gdy pamięć podręczna Redis Azure jest używany wyłącznie w celu pub/sub będzie braku metryk dla `Cache Hits`, `Cache Misses`, `Gets`, lub `Sets`, ale będzie można `Total Operations` metryki, które odzwierciedlać hello użycia pamięci podręcznej dla operacji pub/sub. |
| Używana pamięć |Witaj ilość pamięć podręczna używana dla par klucz/wartość w pamięci podręcznej hello w MB podczas hello określony interwał raportowania. Ta wartość mapuje zbyt`used_memory` z hello polecenie Redis informacji. Nie zawiera metadanych lub fragmentacji. |
| Używana pamięć RSS |Hello ilość pamięci podręcznej używane w MB hello określonym interwale raportowania, łącznie z fragmentacją i metadanych. Ta wartość mapuje zbyt`used_memory_rss` z hello polecenie Redis informacji. |
| Procesor CPU |użycie procesora CPU serwera pamięci podręcznej Redis Azure hello jako procent podczas hello Hello określony interwał raportowania. Ta wartość mapuje systemu operacyjnego toohello `\Processor(_Total)\% Processor Time` licznika wydajności. |
| Odczyt z pamięci podręcznej |Witaj ilość danych odczytana z pamięci podręcznej hello w MB na sekundę (MB/s) podczas hello określony interwał raportowania. Ta wartość jest pochodną hello karty sieciowe obsługujące hello maszyny wirtualnej, która obsługuje hello pamięci podręcznej i jest nie Redis określone. **Ta wartość odpowiada toohello przepustowość sieci używanych przez pamięć podręczną. Jeśli chcesz tooset alerty dla limity przepustowości sieci po stronie serwera, to należy go utworzyć za pomocą tej `Cache Read` licznika. Zobacz [tej tabeli](cache-faq.md#cache-performance) dla hello obserwowanych limity przepustowości dla różnych pamięci podręcznej ceny warstw i rozmiary.** |
| Pamięć podręczna zapisu |Witaj ilość danych zapisane toohello pamięci podręcznej w MB na sekundę (MB/s) w określonym interwale raportowania hello. Ta wartość jest pochodną hello karty sieciowe obsługujące hello maszyny wirtualnej, która obsługuje hello pamięci podręcznej i jest nie Redis określone. Ta wartość odpowiada toohello przepustowość sieci wynosi dane przesyłane z powitania klienta toohello pamięci podręcznej. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Alerty
Można skonfigurować alerty tooreceive oparte na dzienniki metryki i działania. Azure Monitor pozwala tooconfigure toodo alertu powitania po wyzwala:

* Wyślij wiadomość e-mail z powiadomieniem
* Wywołanie elementu webhook
* Wywołanie aplikacji logiki platformy Azure

reguły alertów tooconfigure dla pamięci podręcznej, kliknij przycisk **reguły alertów** z hello **zasobów menu**.

![Monitorowanie](./media/cache-how-to-monitor/redis-cache-monitoring.png)

Aby uzyskać więcej informacji o konfigurowaniu i korzystanie z alertów, zobacz [Przegląd alertów](../monitoring-and-diagnostics/insights-alerts-portal.md).

## <a name="activity-logs"></a>Dzienniki aktywności
Dzienniki aktywności zapewniają wgląd w działania hello, wykonywane na swoich wystąpień w pamięci podręcznej Redis Azure. Został on wcześniej znana jako "dzienników inspekcji" lub "operacyjne dzienniki". Przy użyciu dzienników działania, można określić hello ", co, która i kiedy" dla operacji (PUT, POST, DELETE) podejmowaną w odniesieniu do swoich wystąpień w pamięci podręcznej Redis Azure żadnego zapisu. 

> [!NOTE]
> Dzienniki aktywności nie dołączaj operacje odczytu (GET).
>
>

Dzienniki aktywności tooview dla pamięci podręcznej, kliknij przycisk **Dzienniki aktywności** z hello **zasobów menu**.

Aby uzyskać więcej informacji o Dzienniki aktywności, zobacz [omówienie hello dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).











