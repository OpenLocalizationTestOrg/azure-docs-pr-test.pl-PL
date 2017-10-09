---
title: "tooconfigure aaaHow pamięć podręczna Redis Azure | Dokumentacja firmy Microsoft"
description: "Omówienie hello domyślną konfigurację pamięci podręcznej Redis pamięć podręczna Redis Azure i Dowiedz się, jak tooconfigure Azure Redis wystąpień pamięci podręcznej"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>Jak tooconfigure Azure pamięci podręcznej Redis
W tym temacie opisano, jak aktualizacja i tooreview hello konfiguracji dla swoich wystąpień w pamięci podręcznej Redis Azure i konfigurację domyślną hello obejmuje serwera Redis dla wystąpienia pamięci podręcznej Redis Azure.

> [!NOTE]
> Aby uzyskać więcej informacji na temat konfigurowania przy użyciu funkcji pamięci podręcznej premium, zobacz [jak trwałości tooconfigure](cache-how-to-premium-persistence.md), [jak tooconfigure klastrowanie](cache-how-to-premium-clustering.md), i [obsługi tooconfigure sieci wirtualnej ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Skonfiguruj ustawienia pamięci podręcznej Redis
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Ustawienia pamięci podręcznej Redis Azure są wyświetlane i skonfigurowane na powitania **pamięci podręcznej Redis** bloku przy użyciu hello **zasobów Menu**.

![Ustawienia pamięci podręcznej redis](./media/cache-configure/redis-cache-settings.png)

Można wyświetlić i skonfigurować następujące ustawienia za pomocą hello hello **zasobów Menu**.

* [Omówienie](#overview)
* [Dziennik aktywności](#activity-log)
* [Kontrola dostępu (IAM)](#access-control-iam)
* [Tagi](#tags)
* [Diagnozowanie i rozwiązywanie problemów](#diagnose-and-solve-problems)
* [Ustawienia](#settings)
    * [Klawisze dostępu](#access-keys)
    * [Ustawienia zaawansowane](#advanced-settings)
    * [Klasyfikator pamięci podręcznej redis](#redis-cache-advisor)
    * [Skalowanie](#scale)
    * [Rozmiar klastra redis](#cluster-size)
    * [Trwałość danych redis](#redis-data-persistence)
    * [Aktualizacje harmonogramu](#schedule-updates)
    * [Geo-replication](#geo-replication) (Replikacja geograficzna)
    * [Virtual Network](#virtual-network)
    * [Zapora](#firewall)
    * [Właściwości](#properties)
    * [Blokady](#locks)
    * [Skrypt automatyzacji](#automation-script)
* [Administracja](#administration)
    * [Importowanie danych](#importexport)
    * [Eksportowanie danych](#importexport)
    * [Ponowne uruchamianie](#reboot)
* [Monitorowanie](#monitoring)
    * [Redis metryk](#redis-metrics)
    * [Reguły alertów](#alert-rules)
    * [Diagnostyka](#diagnostics)
* [Rozwiązywanie problemów z ustawieniami i pomoc techniczna](#support-amp-troubleshooting-settings)
    * [Kondycja zasobów](#resource-health)
    * [Nowe żądanie pomocy technicznej](#new-support-request)


## <a name="overview"></a>Omówienie

**Omówienie** zapewnia możesz podstawowych informacji o pamięci podręcznej, takie jak nazwa, porty, warstwa cenowa i metryki wybranego pamięci podręcznej.

### <a name="activity-log"></a>Dziennik aktywności

Kliknij przycisk **dziennik aktywności** tooview akcje wykonywane w pamięci podręcznej. Można również użyć filtrowania tooexpand tooinclude tego widoku inne zasoby. Aby uzyskać więcej informacji na temat pracy z dziennikami inspekcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md). Aby uzyskać więcej informacji dotyczących monitorowania zdarzeń pamięć podręczna Redis Azure, zobacz [operacji i alerty](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Kontrola dostępu (IAM)

Witaj **(IAM) kontroli dostępu** sekcji zapewnia obsługę kontroli dostępu opartej na rolach (RBAC) w hello Azure toohelp portalu organizacji spełniają ich wymagania dotyczące zarządzania dostępu po prostu i dokładnie. Aby uzyskać więcej informacji, zobacz [kontroli dostępu opartej na rolach w portalu Azure hello](../active-directory/role-based-access-control-configure.md).

### <a name="tags"></a>Tagi

Witaj **tagi** sekcji pomaga organizować zasobów. Aby uzyskać więcej informacji, zobacz [używanie tagów tooorganize zasobów platformy Azure](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Diagnozowanie i rozwiązywanie problemów

Kliknij przycisk **diagnozowanie i rozwiązywanie problemów** toobe dostarczone z najczęściej występujących problemów i strategii w celu ich rozwiązania.



## <a name="settings"></a>Ustawienia
Witaj **ustawienia** sekcji pozwala tooaccess i skonfiguruj następujące ustawienia dla pamięci podręcznej hello.

* [Klawisze dostępu](#access-keys)
* [Ustawienia zaawansowane](#advanced-settings)
* [Klasyfikator pamięci podręcznej redis](#redis-cache-advisor)
* [Skalowanie](#scale)
* [Rozmiar klastra redis](#cluster-size)
* [Trwałość danych redis](#redis-data-persistence)
* [Aktualizacje harmonogramu](#schedule-updates)
* [Geo-replication](#geo-replication) (Replikacja geograficzna)
* [Virtual Network](#virtual-network)
* [Zapora](#firewall)
* [Właściwości](#properties)
* [Blokady](#locks)
* [Skrypt automatyzacji](#automation-script)



### <a name="access-keys"></a>Klawisze dostępu
Kliknij przycisk **klucze dostępu** tooview lub regenerate hello dostępu do kluczy dla pamięci podręcznej. Klucze te są używane przez klientów hello łączenie tooyour pamięci podręcznej.

![Klucze dostępu pamięci podręcznej redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Ustawienia zaawansowane
Witaj następujące ustawienia są konfigurowane na powitania **Zaawansowane ustawienia** bloku.

* [Porty dostępu](#access-ports)
* [Zasady pamięci](#memory-policies)
* [Powiadomienia przestrzeni kluczy (ustawienia zaawansowane)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>Porty dostępu
Domyślnie dostęp inny niż za pomocą protokołu SSL jest zablokowany dla nowych pamięci podręcznych. tooenable hello bez użycia protokołu SSL portu, kliknij przycisk **nr** dla **zezwolić na dostęp tylko za pośrednictwem protokołu SSL** na powitania **Zaawansowane ustawienia** bloku, a następnie kliknij przycisk **zapisać**.

![Porty dostępu pamięci podręcznej redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Zasady pamięci
Witaj **zasad Maxmemory**, **zastrzeżone maxmemory**, i **zastrzeżone maxfragmentationmemory** ustawień na powitania **Zaawansowane ustawienia**bloku konfigurowania zasad pamięci hello hello pamięci podręcznej.

![Zasady Maxmemory pamięci podręcznej redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Zasady Maxmemory** skonfiguruje zasady wykluczania hello hello pamięci podręcznej i pozwala toochoose z hello następujące zasady wykluczenia:

* `volatile-lru`— jest to domyślna hello.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Aby uzyskać więcej informacji na temat `maxmemory` zasad, zobacz [zasady wykluczania](http://redis.io/topics/lru-cache#eviction-policies).

Witaj **zastrzeżone maxmemory** skonfigurowanie hello ilość pamięci w Megabajtach, które jest zastrzeżone dla operacji-cache, takich jak replikacji w trybie failover. Ustawienie tej wartości umożliwia toohave więcej spójne środowisko serwera Redis gdy zmienia się obciążenia. Ta wartość musi być ustawiona wyższych obciążeń, które są zapisu ciężki. Pamięć jest zarezerwowana dla takich operacji, jest niedostępna dla magazynu danych z pamięci podręcznej.

Witaj **zastrzeżone maxfragmentationmemory** skonfigurowanie hello ilość pamięci w Megabajtach, które jest zastrzeżone tooaccommodate fragmentacji pamięci. Ustawienie tej wartości umożliwia toohave więcej spójne środowisko serwera Redis hello pamięć podręczna jest pełna lub Współczynnik zamknięcia toofull i hello fragmentacji również jest wysoka. Pamięć jest zarezerwowana dla takich operacji, jest niedostępna dla magazynu danych z pamięci podręcznej.

Tooconsider rzecz, wybierając nową wartość rezerwacji pamięci (**zastrzeżone maxmemory** lub **zastrzeżone maxfragmentationmemory**) jest jak tej zmiany mogą wpłynąć na pamięci podręcznej, który jest już uruchomione z duże ilości danych. Na przykład jeśli użytkownik ma 53 GB pamięci podręcznej z 49 GB danych, a następnie zmień hello rezerwacji wartość too8 GB, to spowoduje porzucenie hello maksymalna dostępna pamięć dla systemu hello too45 GB. Jeśli bieżące `used_memory` lub `used_memory_rss` wartości są wyższe niż hello nowego limitu 45 GB, a następnie hello system będzie mieć danych tooevict przed zakończeniem `used_memory` i `used_memory_rss` są poniżej 45 GB. Wykluczanie może zwiększyć fragmentacji pamięci i obciążenia serwera. Aby uzyskać więcej informacji w pamięci podręcznej metryk, takich jak `used_memory` i `used_memory_rss`, zobacz [dostępne metryki i raportowania interwałów](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).

> [!IMPORTANT]
> Witaj **zastrzeżone maxmemory** i **zastrzeżone maxfragmentationmemory** ustawienia są dostępne tylko dla Standard i Premium przechowuje w pamięci podręcznej.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Powiadomienia przestrzeni kluczy (ustawienia zaawansowane)
Redis na powitania skonfigurowano powiadomienia przestrzeni kluczy **Zaawansowane ustawienia** bloku. Powiadomienia przestrzeni kluczy pozwalają klientom tooreceive powiadomienia w przypadku wystąpienia określonych zdarzeń.

![Zaawansowane ustawienia pamięci podręcznej redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Przestrzeni kluczy powiadomień i hello **powiadomienia przestrzeni kluczy zdarzenia** ustawienia są dostępne tylko dla pamięci podręcznej standardowa i Premium.
> 
> 

Aby uzyskać więcej informacji, zobacz [Redis powiadomienia przestrzeni kluczy](http://redis.io/topics/notifications). Przykładowy kod, zobacz hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) pliku w hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) próbki.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Klasyfikator pamięci podręcznej redis
Witaj **Advisor pamięci podręcznej Redis** blok zawiera zalecenia dotyczące pamięci podręcznej. Podczas wykonywania normalnych operacji zostaną wyświetlone żadnych zaleceń. 

![Zalecenia](./media/cache-configure/redis-cache-no-recommendations.png)

Jeśli wszystkie warunki wystąpić w jego trakcie hello operacje takie jak wysokie użycie pamięci przepustowości sieci i obciążenie serwera pamięci podręcznej, zostanie wyświetlony alert na powitania **pamięci podręcznej Redis** bloku.

![Zalecenia](./media/cache-configure/redis-cache-recommendations-alert.png)

Dalsze informacje znajdują się na powitania **zalecenia** bloku.

![Zalecenia](./media/cache-configure/redis-cache-recommendations.png)

Można monitorować te metryki na powitania [monitorowania wykresy](cache-how-to-monitor.md#monitoring-charts) i [wykresy użycia](cache-how-to-monitor.md#usage-charts) sekcje hello **pamięci podręcznej Redis** bloku.

Każda warstwa cenowa ma inną limity dla połączeń klienckich, pamięci oraz przepustowości. Jeśli pamięć podręczna zbliża się do maksymalnej pojemności dla tych metryk przez dłuższy czas, zostanie utworzony zalecenia. Aby uzyskać więcej informacji o hello metryki i limity przeglądane przez hello **zalecenia** narzędzie, zobacz hello w poniższej tabeli:

| Metryki pamięci podręcznej redis | Więcej informacji |
| --- | --- |
| Wykorzystanie przepustowości sieci |[Wydajność pamięci podręcznej - dostępną przepustowość](cache-faq.md#cache-performance) |
| Podłączeni klienci |[Domyślna konfiguracja serwera Redis - maxclients](#maxclients) |
| Obciążenie serwera |[Wykresy użycia - obciążenia serwera Redis](cache-how-to-monitor.md#usage-charts) |
| Użycie pamięci |[Wydajność pamięci podręcznej — rozmiar](cache-faq.md#cache-performance) |

tooupgrade pamięć podręczną, kliknij przycisk **Uaktualnij teraz** hello toochange warstwy cenowej i [skali](#scale) pamięci podręcznej. Aby uzyskać więcej informacji o wyborze warstwy cenowej, zobacz [jakie oferty pamięć podręczna Redis i rozmiar należy używać?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Skalowanie
Kliknij przycisk **skali** hello tooview lub Zmień warstwę cenową dla pamięci podręcznej. Aby uzyskać więcej informacji na temat skalowania, zobacz [jak tooScale Azure pamięci podręcznej Redis](cache-how-to-scale.md).

![Warstwa cenowa pamięci podręcznej redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Rozmiar klastra redis
Kliknij przycisk **rozmiar klastra Redis (wersja ZAPOZNAWCZA)** rozmiar klastra hello toochange uruchomionych Premium pamięci podręcznej z włączoną funkcją klastrowania.

> [!NOTE]
> Należy pamiętać, że podczas hello Azure Redis Premium usługi pamięć podręczna warstwy zostało zwolnione tooGeneral dostępności, funkcja Redis rozmiar klastra hello jest obecnie w przeglądzie.
> 
> 

![Rozmiar klastra redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

rozmiar klastra hello toochange, za pomocą suwaka hello lub wpisz liczbę z zakresu od 1 do 10 w hello **liczby niezależnych** polu tekstowym i kliknij przycisk **OK** toosave.

> [!IMPORTANT]
> Klaster redis jest dostępna tylko dla pamięci podręcznej Premium. Aby uzyskać więcej informacji, zobacz [jak tooconfigure klastrowania podręczna Redis Azure Premium](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Trwałość danych redis
Kliknij przycisk **trwałość danych Redis** tooenable, wyłączyć lub konfigurowanie trwałości danych dla pamięci podręcznej premium. Pamięć podręczna Redis Azure oferuje trwałość Redis przy użyciu [trwałości RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) lub [trwałości AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).

Aby uzyskać więcej informacji, zobacz [jak tooconfigure trwałości dla podręczna Redis Azure Premium](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> Trwałości danych pamięci podręcznej redis jest dostępna tylko dla pamięci podręcznej Premium. 
> 
> 

### <a name="schedule-updates"></a>Aktualizacje harmonogramu
Witaj **Zaplanuj aktualizacje** bloku umożliwia toodesignate okna obsługi aktualizacji serwera Redis dla pamięci podręcznej. 

> [!IMPORTANT]
> okna obsługi Hello stosuje tylko aktualizacje serwera tooRedis i nie tooany Azure aktualizacji lub aktualizacji systemu operacyjnego toohello hello maszyn wirtualnych, obsługujące hello pamięci podręcznej.
> 
> 

![Aktualizacje harmonogramu](./media/cache-configure/redis-schedule-updates.png)

Sprawdź dni hello potrzeby toospecify okna konserwacji i określ hello godzina rozpoczęcia okna konserwacji dla każdego dnia i kliknij **OK**. Należy pamiętać, że czas okna obsługi hello jest w formacie UTC. 

> [!IMPORTANT]
> Witaj **Zaplanuj aktualizacje** funkcjonalność jest dostępna tylko dla pamięci podręcznej warstwy Premium. Aby uzyskać więcej informacji oraz instrukcje, zobacz [administrowanie pamięć podręczna Redis Azure — Zaplanuj aktualizacje](cache-administration.md#schedule-updates).
> 
> 

### <a name="geo-replication"></a>Replikacja geograficzna

Witaj **— replikacja geograficzna** bloku udostępnia mechanizm do konsolidacji dwa wystąpienia pamięci podręcznej Redis Azure warstwy Premium. Jedna pamięć podręczna jest wyznaczony jako hello głównej połączonego pamięci podręcznej i hello innych jako hello dodatkowej połączonego pamięci podręcznej. Hello pamięci podręcznej połączonego dodatkowej staje się tylko do odczytu i jest zapisany toohello głównej pamięci podręcznej danych replikowane toohello dodatkowej połączonego pamięci podręcznej. Ta funkcja może być używana tooreplicate pamięci podręcznej w regionach platformy Azure.

> [!IMPORTANT]
> **Replikacja geograficzna** jest dostępna tylko dla pamięci podręcznej warstwy Premium. Aby uzyskać więcej informacji oraz instrukcje, zobacz [jak tooconfigure — replikacja geograficzna dla pamięci podręcznej Redis Azure](cache-how-to-geo-replication.md).
> 
> 

### <a name="virtual-network"></a>Virtual Network
Witaj **sieci wirtualnej** sekcja umożliwia ustawień sieci wirtualnej hello tooconfigure dla pamięci podręcznej. Informacje na temat tworzenia pamięci podręcznej premium z sieciami Wirtualnymi obsługują i aktualizowanie jej ustawień, zobacz [jak tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> Ustawienia sieci wirtualnej są dostępne tylko dla pamięci podręcznej premium, które zostały skonfigurowane z obsługą sieci Wirtualnej podczas tworzenia pamięci podręcznej. 
> 
> 

### <a name="firewall"></a>Zapora

Kliknij przycisk **zapory** tooview i konfigurowanie reguł zapory dla pamięć podręczna Redis Azure Premium.

![Zapora](./media/cache-configure/redis-firewall-rules.png)

Początek i koniec zakresu adresów IP można określić reguły zapory. Jeśli reguły zapory są skonfigurowane, tylko połączenia klienckie z hello określony, zakresów adresów IP można połączyć toohello pamięci podręcznej. Po zapisaniu regułę zapory jest krótkie opóźnienie przed obowiązuje zasada hello. To opóźnienie jest zazwyczaj mniej niż minutę.

> [!IMPORTANT]
> Połączenia z pamięcią podręczną Redis Azure monitorowania systemów będą zawsze dozwolone, nawet jeśli reguły zapory są skonfigurowane.
> 
> Reguły zapory są dostępne tylko dla pamięci podręcznej warstwy Premium.
> 
> 

### <a name="properties"></a>Właściwości
Kliknij przycisk **właściwości** tooview informacji o pamięci podręcznej, łącznie z punktu końcowego pamięci podręcznej hello i portów.

![Właściwości pamięci podręcznej redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Blokady
Witaj **blokuje** sekcja pozwala toolock subskrypcji, grupy zasobów lub tooprevent zasobów innym użytkownikom w organizacji przypadkowo usuwanie i modyfikowanie kluczowych zasobów. Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).

### <a name="automation-script"></a>Skrypt automatyzacji

Kliknij przycisk **skryptu automatyzacji** toobuild i eksportowanie szablonu wdrożonych zasobów do przyszłych wdrożeń. Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [wdrożenie zasobów przy użyciu szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Ustawienia administracji
Witaj ustawienia w hello **administracji** sekcji pozwalają hello tooperform następujące zadania administracyjne dla pamięci podręcznej. 

![Administracja](./media/cache-configure/redis-cache-administration.png)

* [Importowanie danych](#importexport)
* [Eksportowanie danych](#importexport)
* [Ponowne uruchamianie](#reboot)


### <a name="importexport"></a>Import/Export
Import/Eksport jest operacji zarządzania pamięcią podręczną Redis Azure danych, która umożliwia tooimport i eksportowanie danych w pamięci podręcznej hello przez importowanie i Eksportowanie migawki Redis pamięci podręcznej bazy danych (RDB) z premium pamięci podręcznej tooa stronicowy obiekt blob na koncie magazynu Azure. Narzędzie importu/eksportu umożliwia toomigrate między różnymi wystąpieniami usługi pamięć podręczna Redis Azure lub wypełnienia pamięci podręcznej hello danych przed użyciem.

Import może być używane toobring Redis zgodne RDB plików z dowolnego serwera Redis uruchomiona w chmurze lub środowiska, w tym Redis w systemie Linux, Windows albo dowolnego dostawcy chmury, takich jak usług Amazon Web Services i innych użytkowników. Importowanie danych jest łatwe toocreate pamięci podręcznej z wstępnie wypełnione danych. Podczas procesu importowania hello pamięć podręczna Redis Azure ładuje hello RDB pliki z magazynu Azure do pamięci i wstawia hello klucze do pamięci podręcznej hello.

Eksport umożliwia tooexport hello danych przechowywanych w pamięci podręcznej Redis Azure tooRedis zgodne pliki RDB. Można użyć tych danych toomove funkcji z jednego tooanother wystąpienia pamięci podręcznej Redis Azure lub tooanother serwera Redis. W procesie eksportu hello plik tymczasowy zostanie utworzony na powitania wirtualna hostów hello wystąpienie serwera pamięci podręcznej Redis Azure, czy plik hello jest przekazany toohello wyznaczony konta magazynu. Po ukończeniu operacji eksportowania hello ze stanem powodzenie lub niepowodzenie hello plik tymczasowy zostanie usunięty.

> [!IMPORTANT]
> Narzędzie importu/eksportu jest dostępna tylko dla pamięci podręcznej warstwy Premium. Aby uzyskać więcej informacji oraz instrukcje, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Ponowne uruchamianie
Witaj **ponowny rozruch** bloku umożliwia tooreboot hello węzłów pamięci podręcznej. Ta możliwość ponownego uruchomienia umożliwia tootest możesz aplikacji zapewnia odporność na awarie w przypadku awarii węzła pamięci podręcznej.

![Ponowne uruchamianie](./media/cache-configure/redis-cache-reboot.png)

Jeśli pamięć podręczna premium z włączoną funkcją klastrowania, można wybrać, które odłamków hello tooreboot pamięci podręcznej.

![Ponowne uruchamianie](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot co najmniej jeden węzeł z pamięci podręcznej, wybierz węzeł hello potrzebne i kliknij przycisk **ponowny rozruch**. Jeśli masz usługi pamięć podręczna premium z włączoną funkcją klastrowania, wybierz hello shard(s) tooreboot, a następnie kliknij przycisk **ponowny rozruch**. Po kilku minutach hello ponownego uruchomienia wybranych węzłów i jest znowu w trybie online później za kilka minut.

> [!IMPORTANT]
> Ponowne uruchomienie jest teraz dostępna dla wszystkich warstw cenowych. Aby uzyskać więcej informacji oraz instrukcje, zobacz [administrowanie pamięć podręczna Redis Azure — ponowne uruchomienie](cache-administration.md#reboot).
> 
> 


## <a name="monitoring"></a>Monitorowanie

Witaj **monitorowanie** sekcja pozwala tooconfigure Diagnostyka i monitorowanie dla pamięci podręcznej Redis. Aby uzyskać więcej informacji o pamięci podręcznej Redis Azure monitorowania i diagnostyki, zobacz [jak toomonitor Azure pamięci podręcznej Redis](cache-how-to-monitor.md).

![Diagnostyka](./media/cache-configure/redis-cache-diagnostics.png)

* [Redis metryk](#redis-metrics)
* [Reguły alertów](#alert-rules)
* [Diagnostyka](#diagnostics)

### <a name="redis-metrics"></a>Redis metryk
Kliknij przycisk **Redis metryki** za[wyświetlić metryki](cache-how-to-monitor.md#view-cache-metrics) dla pamięci podręcznej.

### <a name="alert-rules"></a>Reguły alertów

Kliknij przycisk **reguły alertów** tooconfigure alertów w oparciu metryki pamięci podręcznej Redis. Aby uzyskać więcej informacji, zobacz [alerty](cache-how-to-monitor.md#alerts).

### <a name="diagnostics"></a>Diagnostyka

Domyślnie są metryki pamięci podręcznej w monitorze Azure [przechowywane przez 30 dni](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) , a następnie usuwany. toopersist Twojego metryki pamięci podręcznej przez czas dłuższy niż 30 dni, kliknij przycisk **diagnostyki** za[Konfigurowanie konta magazynu hello](cache-how-to-monitor.md#export-cache-metrics) używane toostore Diagnostyka pamięci podręcznej.

>[!NOTE]
>Dodanie tooarchiving Twojego toostorage metryki pamięci podręcznej, można też [strumienia ich Centrum zdarzeń tooan lub wysyłanie do nich tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Rozwiązywanie problemów z ustawieniami i pomoc techniczna
Witaj ustawienia w hello **pomocy technicznej i rozwiązywania problemów** sekcja zawiera opcje rozwiązywania problemów związanych z pamięci podręcznej.

![Pomocy technicznej i rozwiązywania problemów](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Kondycja zasobów](#resource-health)
* [Nowe żądanie pomocy technicznej](#new-support-request)

### <a name="resource-health"></a>Kondycja zasobów
**Kondycja zasobów** oczekuje zasobu i informuje, czy działa on zgodnie z oczekiwaniami. Aby uzyskać więcej informacji na temat hello usługi kondycji zasobów Azure, zobacz [Przegląd kondycji zasobów Azure](../resource-health/resource-health-overview.md).

> [!NOTE]
> Kondycja zasobu jest aktualnie w stanie tooreport na powitania kondycji wystąpień pamięci podręcznej Redis Azure hostowanej w sieci wirtualnej. Aby uzyskać więcej informacji, zobacz [wszystkie funkcje pamięci podręcznej działają odnośnie do hostowania pamięci podręcznej w sieci Wirtualnej?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>Nowe żądanie pomocy technicznej
Kliknij przycisk **nowy obsługuje żądania** tooopen żądania pomocy technicznej dla pamięci podręcznej.





## <a name="default-redis-server-configuration"></a>Domyślna konfiguracja serwera Redis
Nowe wystąpienia pamięci podręcznej Redis Azure są skonfigurowane z hello następujących domyślnych wartości konfiguracji pamięci podręcznej Redis.

> [!NOTE]
> Ustawienia Hello w tej sekcji nie można zmienić za pomocą hello `StackExchange.Redis.IServer.ConfigSet` metody. Jeśli ta metoda jest wywoływana z jednego z poleceń hello w tej sekcji, zostanie zgłoszony następujący wyjątek podobne toohello:  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> Wartości, które można skonfigurować, takie jak **Maksymalna pamięć zasady**, można konfigurować za pośrednictwem portalu Azure hello lub narzędzia do zarządzania wiersza polecenia takich jak wiersza polecenia platformy Azure lub programu PowerShell.
> 
> 

| Ustawienie | Wartość domyślna | Opis |
| --- | --- | --- |
| `databases` |16 |Witaj domyślną liczbę baz danych jest 16, ale można skonfigurować inny numer hello na podstawie warstwy cenowej. <sup>1</sup> hello domyślna baza danych jest DB 0, możesz wybrać inną na podstawę dla każdego połączenia przy użyciu `connection.GetDatabase(dbid)` gdzie `dbid` jest liczbą z zakresu od `0` i `databases - 1`. |
| `maxclients` |Zależy od warstwy cenowej hello<sup>2</sup> |Jest to maksymalna liczba podłączonych klientów dozwolone na powitania sam hello czasu. Po osiągnięciu limitu hello Redis zamyka wszystkie hello nowych połączeń, zwróci komunikat "Maksymalna liczba klientów osiągnięto". |
| `maxmemory-policy` |`volatile-lru` |Zasady Maxmemory jest ustawienie hello jak Redis wybiera jakie tooremove podczas `maxmemory` osiągnięciu (hello rozmiar pamięci podręcznej hello oferty wybranej podczas tworzenia pamięci podręcznej hello). Z pamięci podręcznej Redis Azure hello domyślne ustawienie to `volatile-lru`, które powoduje usunięcie kluczy hello z wygaśnięciem ustawić za pomocą algorytmu LRU. To ustawienie można skonfigurować w hello portalu Azure. Aby uzyskać więcej informacji, zobacz [zasady pamięci](#memory-policies). |
| `maxmemory-samples` |3 |toosave pamięci, LRU i minimalny czas wygaśnięcia algorytmy są przybliżona algorytmy zamiast dokładne algorytmów. Domyślnie Redis kontroli trzy klucze i pobrania hello jedną używany mniej ostatnio. |
| `lua-time-limit` |5,000 |Maksymalny czas wykonywania skryptu Lua (w milisekundach). Po osiągnięciu maksymalnego czasu wykonywania hello Redis rejestruje skryptu nadal trwa wykonywanie po hello maksymalny dozwolony czas i uruchamia tooreply tooqueries z powodu błędu. |
| `lua-event-limit` |500 |Maksymalny rozmiar kolejki zdarzeń skryptu. |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 mb 032 8mb 60 |Witaj limity buforu wyjściowego klienta mogą być używane rozłączenia tooforce klientów, które nie są odczytywanie danych z serwera hello wystarczająca jakiegoś powodu (typową przyczyną jest, że klient Pub/Sub nie mogą korzystać z wiadomości tak szybko, jak wydawcy hello może utworzyć je). Aby uzyskać więcej informacji, zobacz [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup>hello limit `databases` jest różne dla każdego pamięć podręczna Redis Azure warstwy cenowej i można ustawić na tworzenie pamięci podręcznej. Jeśli nie `databases` ustawienie jest określone podczas tworzenia pamięci podręcznej hello domyślna to 16.

* Podstawowa i standardowa pamięci podręczne
  * C0 (250 MB) pamięci podręcznej - zapasowe too16 baz danych
  * C1 pamięci podręcznej (1 GB) — zapasowe too16 baz danych
  * C2 (2,5 GB) pamięci podręcznej - zapasowe too16 baz danych
  * C3 (6 GB) pamięci podręcznej - zapasowe too16 baz danych
  * C4 (13 GB) pamięci podręcznej - zapasowe too32 baz danych
  * C5 (26 GB) pamięci podręcznej - zapasowe too48 baz danych
  * C6 (53 GB) pamięci podręcznej - zapasowe too64 baz danych
* Pamięci podręczne — wersja Premium
  * P1 (6 GB — 60 GB) — zapasowe too16 baz danych
  * P2 (13 GB - 130 GB) — zapasowe too32 baz danych
  * P3 (26 GB - 260 GB) — zapasowe too48 baz danych
  * P4 (53 GB - 530 GB) — zapasowe too64 baz danych
  * Wszystkie bufory premium z klastrem Redis enabled - Redis klastra obsługuje tylko tekst hello korzystania z bazy danych 0 `databases` limit dla dowolnego pamięć podręczna premium z klastrem Redis włączone jest 1 i hello [wybierz](http://redis.io/commands/select) polecenia jest niedozwolone. Aby uzyskać więcej informacji, zobacz [należy toomake wszelkie zmiany toomy klienta aplikacji toouse klastra?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

Aby uzyskać więcej informacji na temat baz danych, zobacz [co to są Redis baz danych?](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> Witaj `databases` ustawienie może być skonfigurowany tylko podczas tworzenia pamięci podręcznej i tylko przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych klientów zarządzania. Aby uzyskać przykład konfigurowania `databases` podczas tworzenia pamięci podręcznej przy użyciu programu PowerShell, zobacz [AzureRmRedisCache nowy](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a>
<sup>2</sup> `maxclients` jest różne dla każdego pamięć podręczna Redis Azure warstwy cenowej.

* Podstawowa i standardowa pamięci podręczne
  * C0 (250 MB) pamięci podręcznej - too256 połączenia
  * C1 pamięci podręcznej (1 GB) — się too1, 000 połączenia
  * C2 (2,5 GB) pamięci podręcznej - się too2, 000 połączenia
  * C3 (6 GB) pamięci podręcznej - się too5, 000 połączenia
  * C4 (13 GB) pamięci podręcznej - się too10, 000 połączenia
  * C5 (26 GB) pamięci podręcznej - się too15, 000 połączenia
  * C6 (53 GB) pamięci podręcznej - się too20, 000 połączenia
* Pamięci podręczne — wersja Premium
  * P1 (6 GB — 60 GB) — się too7, połączenia o szybkości 500
  * P2 (13 GB - 130 GB) — się too15, 000 połączeń
  * P3 (26 GB - 260 GB) — się too30, 000 połączeń
  * P4 (53 GB - 530 GB) — się too40, 000 połączeń

> [!NOTE]
> Podczas każdego rozmiaru pamięci podręcznej umożliwia *do* określonej liczby połączeń, każdy tooRedis połączenia obciążenie ma skojarzonych z nim. Przykładem takich obciążenie będzie użycia Procesora i pamięci w wyniku szyfrowania TLS/SSL. Hello limit maksymalnej liczby połączeń dla rozmiaru pamięci podręcznej danego zakłada lekkim załadować pamięci podręcznej. Czy ładowanie z połączenia koszty *plus* obciążenia z operacjami klienta przekracza pojemność systemu hello, hello pamięci podręcznej można doświadczyć problemów dotyczących pojemności, nawet jeśli nie przekroczono limit połączenia hello hello bieżący rozmiar pamięci podręcznej.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Redis polecenia nie są obsługiwane w pamięci podręcznej Redis Azure
> [!IMPORTANT]
> Ponieważ konfiguracji i zarządzania wystąpienia pamięci podręcznej Redis Azure jest zarządzany przez firmę Microsoft, hello poniższe polecenia są wyłączone. Jeśli spróbujesz tooinvoke ich zbyt otrzymasz komunikat o błędzie podobny`"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * KONFIGURACJI
> * DEBUGOWANIA
> * MIGRACJA
> * ZAPISZ
> * ZAMKNIĘCIE
> * SLAVEOF
> * KLASTER - klaster zapisu, które polecenia są wyłączone, ale tylko do odczytu klastra polecenia są dozwolone.
> 
> 

Aby uzyskać więcej informacji o poleceniach Redis, zobacz [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Redis konsoli
Można bezpiecznie wysyłać polecenia tooyour wystąpienia pamięci podręcznej Redis Azure za pomocą hello **Redis konsoli**, która jest dostępna w hello portalu Azure dla wszystkich warstw pamięci podręcznej.

> [!IMPORTANT]
> - Witaj konsoli Redis nie działa z [sieci Wirtualnej](cache-how-to-premium-vnet.md). Jeśli pamięć podręczna jest częścią sieci Wirtualnej, tylko klienci w sieci Wirtualnej hello można uzyskać dostępu do pamięci podręcznej hello. Ponieważ Redis konsola jest uruchamiana w przeglądarce lokalnego znajduje się poza hello sieci Wirtualnej, nie można połączyć z pamięci podręcznej tooyour.
> - Nie wszystkie polecenia Redis są obsługiwane w pamięci podręcznej Redis Azure. Listę poleceń pamięci podręcznej Redis, które są wyłączone dla pamięci podręcznej Redis Azure, zobacz hello poprzedniej [polecenia nie są obsługiwane w pamięci podręcznej Redis Azure Redis](#redis-commands-not-supported-in-azure-redis-cache) sekcji. Aby uzyskać więcej informacji o poleceniach Redis, zobacz [http://redis.io/commands](http://redis.io/commands).
> 
> 

Witaj tooaccess Redis konsoli, kliknij przycisk **konsoli** z hello **pamięci podręcznej Redis** bloku.

![Redis konsoli](./media/cache-configure/redis-console-menu.png)

tooissue polecenia dla wystąpienia pamięci podręcznej, po prostu typu hello żądanego polecenia do konsoli hello.

![Redis konsoli](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>Przy użyciu hello Redis konsoli z premium w klastrze pamięci podręcznej

Przy użyciu hello Redis konsoli premium pamięć podręczna klastra można wydać polecenia tooa jednego niezależnego fragmentu hello pamięci podręcznej. tooissue niezależnych określonych tooa polecenia, najpierw połączyć toohello żądany identyfikator niezależnego fragmentu, klikając hello niezależnego fragmentu selektora.

![Redis konsoli](./media/cache-configure/redis-console-premium-cluster.png)

Przy próbie tooaccess klucz, który znajduje się w różnych niezależnego fragmentu niż hello niezależnych połączonych otrzymujesz błąd komunikat podobny toohello następującą wiadomości.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

W poprzednim przykładzie hello niezależnego fragmentu 1 jest wybrany niezależnego fragmentu hello, ale `myKey` znajduje się w niezależnych 0, wskazywany przez hello `(shard 0)` część komunikatu o błędzie hello. W tym przykładzie tooaccess `myKey`, wybierz za pomocą niezależnego fragmentu 0 hello selektora niezależnego fragmentu, a następnie polecenie hello potrzeby problem.


## <a name="move-your-cache-tooa-new-subscription"></a>Przenieś nowej subskrypcji tooa pamięci podręcznej
Przenieś z nowej subskrypcji tooa pamięci podręcznej, klikając **Przenieś**.

![Przenieś pamięci podręcznej Redis](./media/cache-configure/redis-cache-move.png)

Aby uzyskać informacje na temat przenoszenia zasobów z jednego zasobu grupy tooanother i tooanother jedną subskrypcję, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat pracy z pamięci podręcznej Redis poleceń, zobacz [jak uruchomić polecenia Redis?](cache-faq.md#how-can-i-run-redis-commands)

