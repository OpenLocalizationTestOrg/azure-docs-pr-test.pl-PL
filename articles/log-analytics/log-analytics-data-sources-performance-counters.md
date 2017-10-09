---
title: "aaaCollect i analizować liczniki wydajności w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Liczniki wydajności są zbierane przez wydajności tooanalyze analizy dzienników dla agentów systemu Windows i Linux.  W tym artykule opisano, jak kolekcji tooconfigure wydajności liczników dla agentów systemów Windows i Linux, ich szczegóły są przechowywane w repozytorium OMS hello i w jaki sposób tooanalyze je w portalu OMS hello."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>System Windows i Linux źródła danych wydajności w analizy dzienników
Liczniki wydajności w systemie Windows i Linux zapewniają wgląd w wydajności hello składniki sprzętowe, systemów operacyjnych i aplikacji.  Analizy dzienników można zebrać liczników wydajności w odstępach częste do analizy w pobliżu czasu rzeczywistego (NRT) dodanie tooaggregating danych dotyczących wydajności o dłuższy okres analizy i raportowania.

![Liczniki wydajności](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>Konfigurowanie liczników wydajności
Konfigurowanie liczników wydajności w portalu OMS hello na powitania [danych menu Ustawienia usługi Analiza dzienników](log-analytics-data-sources.md#configuring-data-sources).

Podczas pierwszej konfiguracji systemu Windows lub liczniki wydajności systemu Linux dla nowy obszar roboczy OMS są podane hello tooquickly opcję Utwórz kilka typowych liczników.  Są one wyświetlane z tooeach dalej wyboru.  Upewnij się, że liczników ma tooinitially utworzyć są zaznaczone, a następnie kliknij przycisk **hello Dodaj wybrane liczniki wydajności**.

Do liczników wydajności systemu Windows można wybrać określonego wystąpienia dla każdego licznika wydajności. Liczniki wydajności systemu Linux wystąpienia hello poszczególnych liczników, którą można wybrać dotyczy liczniki podrzędnych tooall hello nadrzędnego licznika. Witaj poniższej tabeli przedstawiono typowe wystąpień hello tooboth dostępne liczniki wydajności systemu Linux i Windows.

| Nazwa wystąpienia | Opis |
| --- | --- |
| \_Całkowita liczba |Całkowita liczba wszystkich wystąpień hello |
| \* |Wszystkie wystąpienia |
| (/ &#124; / var) |Dopasowuje wystąpienia o nazwie: / lub /var |

### <a name="windows-performance-counters"></a>Liczniki wydajności systemu Windows

![Konfigurowanie liczników wydajności systemu Windows](media/log-analytics-data-sources-performance-counters/configure-windows.png)

Postępuj zgodnie z tej procedury tooadd nowe toocollect licznika wydajności systemu Windows.

1. Nazwa typu hello licznika hello w polu tekstowym hello w formacie hello *\counter obiektu (wystąpienia)*.  Po rozpoczęciu wprowadzania, są prezentowane z listą zgodnych wspólnej liczników.  Licznik możesz wybrać z listy hello lub wpisz własny.  Wszystkie wystąpienia określonego licznika można także wrócić, określając *object\counter*.  

    Podczas zbierania liczników wydajności programu SQL Server z nazwanego wystąpienia, wszystkie o nazwie Nazwa wystąpienia liczników rozpoczyna się od *MSSQL$* i następuje nazwa hello hello wystąpienia.  Na przykład toocollect hello Stosunek trafień w pamięci podręcznej dziennika licznika dla wszystkich baz danych z hello obiektu wydajności bazy danych dla serwera SQL o nazwie wystąpienia INST2, określ `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`.

2. Kliknij przycisk  **+**  lub naciśnij klawisz **Enter** tooadd hello licznika toohello listy.
3. Po dodaniu licznik używa hello domyślną 10 sekund na jego **interwału próbkowania**.  Jeśli wymagania dotyczące magazynu hello tooreduce hello zbieranych danych dotyczących wydajności, można zmienić tego tooa wyższa wartość zapasową too1800 sekund (30 minut).
4. Po zakończeniu dodawania liczników kliknij hello **zapisać** u góry hello hello ekranu toosave hello konfiguracji.

### <a name="linux-performance-counters"></a>Liczniki wydajności systemu Linux

![Konfigurowanie liczników wydajności systemu Linux](media/log-analytics-data-sources-performance-counters/configure-linux.png)

Postępuj zgodnie z tej procedury tooadd nowe toocollect licznika wydajności systemu Linux.

1. Domyślnie wszystkie zmiany konfiguracji są automatycznie wypychana agentów tooall.  Dla agentów systemów Linux plik konfiguracji jest wysyłany toohello Fluentd modułów zbierających dane.  Jeśli chcesz toomodify ten plik ręcznie na każdym agenta systemu Linux, usuń zaznaczenie pola hello *Zastosuj poniżej maszyny z systemem Linux toomy konfiguracji* i wykonaj poniższe wskazówki hello.
2. Nazwa typu hello licznika hello w polu tekstowym hello w formacie hello *\counter obiektu (wystąpienia)*.  Po rozpoczęciu wprowadzania, są prezentowane z listą zgodnych wspólnej liczników.  Licznik możesz wybrać z listy hello lub wpisz własny.  
3. Kliknij przycisk  **+**  lub naciśnij klawisz **Enter** tooadd hello licznika toohello listy inne liczniki dla obiekt hello.
4. Wszystkie liczniki dla użycie obiektu hello sam **interwału próbkowania**.  Witaj domyślna to 10 sekund.  Możesz zmienić tooa wyższa wartość zapasową too1800 sekund (30 minut), jeśli wymagania dotyczące magazynu hello tooreduce hello zbieranych danych dotyczących wydajności.
5. Po zakończeniu dodawania liczników kliknij hello **zapisać** u góry hello hello ekranu toosave hello konfiguracji.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>Konfigurowanie liczników wydajności systemu Linux w pliku konfiguracji
Zamiast konfigurować przy użyciu portalu OMS hello liczniki wydajności systemu Linux, można skorzystać z opcji hello edycję plików konfiguracyjnych na powitania agenta systemu Linux.  Toocollect metryki wydajności są kontrolowane przez konfigurację hello w **/etc/opt/microsoft/omsagent/\<identyfikator obszaru roboczego\>/conf/omsagent.conf**.

Każdy obiekt lub kategorii toocollect metryki wydajności powinien być zdefiniowany w pliku konfiguracyjnym hello jako pojedynczy `<source>` elementu. Składnia Hello zgodny wzorcem hello poniżej.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


w hello w poniższej tabeli opisano parametry Hello w tym elemencie.

| Parametry | Opis |
|:--|:--|
| obiekt\_nazwy | Nazwa obiektu hello kolekcji. |
| wystąpienie\_wyrażeń regularnych |  A *wyrażenia regularnego* Definiowanie które toocollect wystąpień. Witaj wartość: `.*` określa wszystkich wystąpień. metryki procesora toocollect tylko hello \_całkowita liczba wystąpień, można określić `_Total`. Metryka procesu toocollect dla hello tylko wystąpienia crond lub sshd, można określić: "(crond\|sshd) ". |
| Licznik\_nazwa\_wyrażeń regularnych | A *wyrażenia regularnego* Definiowanie które toocollect liczniki (dla obiekt hello). Określ wszystkie liczniki dla obiekt hello toocollect: `.*`. toocollect wymiany tylko miejsca liczniki dla obiekt pamięci hello, na przykład można określić:`.+Swap.+` |
| interval | Częstotliwość, w których hello są zbierane liczniki obiektu. |


Witaj poniższej tabeli wymieniono hello obiektów i liczników, które można określić w pliku konfiguracyjnym hello.  Dostępne są dodatkowe liczniki dla określonych aplikacji zgodnie z opisem w [zebrać liczników wydajności dla aplikacji systemu Linux w analizy dzienników](log-analytics-data-sources-linux-applications.md).

| Nazwa obiektu | Nazwa licznika |
|:--|:--|
| Dysk logiczny | % Wolnych węzłów i |
| Dysk logiczny | % Wolnego miejsca |
| Dysk logiczny | % Użytych węzłów i |
| Dysk logiczny | Używany obszar % |
| Dysk logiczny | Bajty odczytu dysku/s |
| Dysk logiczny | Odczyty dysku/s |
| Dysk logiczny | Transfery dyskowe/s |
| Dysk logiczny | Bajty zapisu dysku/s |
| Dysk logiczny | Zapisy dysku/s |
| Dysk logiczny | Wolne megabajty |
| Dysk logiczny | Bajty dysku logicznego/s |
| Memory (Pamięć) | % Dostępnej pamięci |
| Memory (Pamięć) | % Dostępnego obszaru wymiany |
| Memory (Pamięć) | Procent wykorzystania pamięci |
| Memory (Pamięć) | Używany obszar wymiany (MB) % |
| Memory (Pamięć) | Dostępna pamięć (MB) |
| Memory (Pamięć) | Dostępny obszar wymiany |
| Memory (Pamięć) | Odczyty stron/s |
| Memory (Pamięć) | Zapisy stron/s |
| Memory (Pamięć) | Strony/s |
| Memory (Pamięć) | Używany obszar wymiany (MB) miejsca |
| Memory (Pamięć) | Używana pamięć (MB) |
| Sieć | Całkowita liczba przesłanych bajtów |
| Sieć | Całkowita liczba odebranych bajtów |
| Sieć | Całkowita liczba bajtów |
| Sieć | Łączna liczba pakietów wysłanych |
| Sieć | Całkowita liczba odebranych pakietów |
| Sieć | Błędy odbioru całkowita |
| Sieć | Błędy wysyłania całkowita |
| Sieć | Całkowita liczba kolizji |
| Dysk fizyczny | Średni Czas dysku w s/Odczyt |
| Dysk fizyczny | Średni Dysku w s/Transfer |
| Dysk fizyczny | Średni Dysku w s/Zapis |
| Dysk fizyczny | Bajty dysku fizycznego/s |
| Proces | Czas uprzywilejowany PCT |
| Proces | Czas użytkownika protokołu PCT |
| Proces | Używane KB pamięci |
| Proces | Wirtualnej pamięci współużytkowanej |
| Procesor | Czas DPC (%) |
| Procesor | Czas bezczynności (%) |
| Procesor | Czas przerwań (%) |
| Procesor | Czas oczekiwania operacji We/Wy (%) |
| Procesor | Czas nieuprzywilejowany (%) |
| Procesor | Czas uprzywilejowany % |
| Procesor | Czas procesora (%) |
| Procesor | Czas użytkownika (%) |
| System | Wolnej pamięci fizycznej |
| System | Wolne miejsce w plikach stronicowania |
| System | Wolnej pamięci wirtualnej |
| System | Procesy |
| System | Rozmiar zapisanych w plikach stronicowania |
| System | Czas działania |
| System | Użytkownicy |


Poniżej znajduje się hello konfigurację domyślną dla metryki wydajności.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>Zbieranie danych
Analizy dzienników zbiera wszystkie liczniki wydajności określony w ich określonego interwału dla wszystkich agentów, na których zainstalowane licznika.  Hello danych nie jest agregowany i danych pierwotnych hello jest dostępna we wszystkich widokach wyszukiwania dziennika hello czas określony przez subskrypcję pakietu OMS.

## <a name="performance-record-properties"></a>Właściwości rekordu wydajności
Rejestruje wydajności mieć typu **wydajności** i mają właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Computer (Komputer) |Komputer, który hello zdarzeń zostały zebrane. |
| CounterName |Nazwa licznika wydajności hello |
| Ścieżka_licznika |Pełna ścieżka licznika hello w postaci hello \\ \\ \<komputera >\\obiekt(wystąpienie)\\licznika. |
| Równowartości |Wartość liczbowa hello licznika. |
| InstanceName |Nazwa wystąpienia zdarzenia hello.  Pusta, jeśli żadne wystąpienie. |
| Nazwa obiektu |Nazwa obiektu wydajności hello |
| SourceSystem |Typ danych hello agenta zostały zebrane. <br><br>Połącz OpsManager — agent systemu Windows, bądź bezpośrednio lub SCOM <br> Linux — wszystkich agentów systemu Linux  <br> AzureStorage — Diagnostyka Azure |
| TimeGenerated |Data i godzina danych hello zostało pobrane. |

## <a name="sizing-estimates"></a>Szacuje zmiany rozmiaru
 Oszacowanie dla kolekcji określonego licznika na 10 sekund jest około 1 MB na dzień dla każdego wystąpienia.  Z hello następującej formuły można oszacować wymagania dotyczące magazynu hello określonego licznika.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>Dziennik wyszukiwania z rekordami wydajności
Witaj poniższej tabeli przedstawiono różne przykłady wyszukiwania dziennika, które pobierają rekordy wydajności.

| Zapytanie | Opis |
|:--- |:--- |
| Typ = wydajności |Wszystkie dane dotyczące wydajności |
| Typ = wydajności komputer = "Mój komputer" |Wszystkie dane dotyczące wydajności z określonego komputera |
| Typ = CounterName wydajności = "Bieżąca długość kolejki dysku" |Wszystkie dane wydajności dla określonego licznika |
| Typ = wydajności (ObjectName = procesora) CounterName = "% czasu procesora" InstanceName = _Total &#124; Miara Avg(Average) jako AVGCPU przez komputer |Średnie wykorzystanie procesora CPU na wszystkich komputerach |
| Typ = wydajności (CounterName = "% czasu procesora") &#124;  max(Max) miary w przeliczeniu na komputer |Maksymalne wykorzystanie procesora CPU na wszystkich komputerach |
| Typ = wydajności ObjectName = dysk logiczny CounterName = "Długość kolejki dysku bieżącego" komputer = "MyComputerName" &#124; Miara Avg(Average) przez InstanceName |Średnia długość kolejki dysku bieżącego we wszystkich wystąpieniach hello danego komputera |
| Typ = CounterName wydajności = "Na sekundę DiskTransfers" &#124; percentile95(Average) miary w przeliczeniu na komputer |95 percentylu z transfery dyskowe/s na wszystkich komputerach |
| Typ = CounterName wydajności = "% czasu procesora" InstanceName = "_łącznie" &#124; Pomiar avg(CounterValue) interwał komputera 1 godzina |Średniej godzinowej użycia procesora CPU na wszystkich komputerach |
| Typ = wydajności komputer = "Mój komputer" CounterName = % * InstanceName = _Total &#124; Miara percentile70(CounterValue) interwał CounterName 1 godzina |Co godzinę percentyl 70 co licznika procent % dla określonego komputera |
| Typ = CounterName wydajności = "% czasu procesora" InstanceName = "_łącznie" (komputer = "Mój komputer") &#124; Pomiar min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) interwał komputera 1 godzina |Co godzinę średnia, minimalne, maksymalne i percentyl 75 użycia procesora CPU dla określonego komputera |
| Typ = wydajności ObjectName = "MSSQL$ INST2: bazy danych" InstanceName = wzorca | Wszystkie dane dotyczące wydajności z wydajność bazy danych hello obiekt dla bazy danych master hello z hello nazwane wystąpienie programu SQL Server INST2.  

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.

> | Zapytanie | Opis |
|:--- |:--- |
| Wydajności |Wszystkie dane dotyczące wydajności |
| Wydajności &#124; gdy komputer == "Mój komputer" |Wszystkie dane dotyczące wydajności z określonego komputera |
| Wydajności &#124; w przypadku, gdy CounterName == "Bieżąca długość kolejki dysku" |Wszystkie dane wydajności dla określonego licznika |
| Wydajności &#124; Gdzie ObjectName == "Procesor" i CounterName == "% czasu procesora" i InstanceName == "_łącznie" &#124; Podsumuj AVGCPU = avg(Average) przez komputer |Średnie wykorzystanie procesora CPU na wszystkich komputerach |
| Wydajności &#124; w przypadku, gdy CounterName == "% czasu procesora" &#124; Podsumuj AggregatedValue = max(Max) przez komputer |Maksymalne wykorzystanie procesora CPU na wszystkich komputerach |
| Wydajności &#124; Gdzie ObjectName == "Dysk logiczny" i CounterName == "Bieżąca długość kolejki dysku" i komputer == "MyComputerName" &#124; Podsumuj AggregatedValue = avg(Average) przez InstanceName |Średnia długość kolejki dysku bieżącego we wszystkich wystąpieniach hello danego komputera |
| Wydajności &#124; w przypadku, gdy CounterName == "Na sekundę DiskTransfers" &#124; Podsumuj AggregatedValue = percentyl (średnia, 95) przez komputer |95 percentylu z transfery dyskowe/s na wszystkich komputerach |
| Wydajności &#124; w przypadku, gdy CounterName == "% czasu procesora" i InstanceName == "_łącznie" &#124; Podsumuj AggregatedValue = avg(CounterValue) przez bin (TimeGenerated, 1 godz.), komputer |Średniej godzinowej użycia procesora CPU na wszystkich komputerach |
| Wydajności &#124; gdy komputer == "Mój komputer" i CounterName startswith_cs "%" i InstanceName == "_łącznie" &#124; Podsumuj AggregatedValue = bin (TimeGenerated, 1 godz.), CounterName percentyl (równowartości 70) | Co godzinę percentyl 70 co licznika procent % dla określonego komputera |
| Wydajności &#124; w przypadku, gdy CounterName == "% czasu procesora" i InstanceName == "_łącznie" i komputer == "Mój komputer" &#124; Podsumuj ["min(CounterValue)"] = min(CounterValue), ["avg(CounterValue)"] = avg(CounterValue), ["percentile75(CounterValue)"] = percentyl (równowartości, 75), ["max(CounterValue)"] = max(CounterValue) przez bin (TimeGenerated, 1 godz.), komputer |Co godzinę średnia, minimalne, maksymalne i percentyl 75 użycia procesora CPU dla określonego komputera |
| Wydajności &#124; Gdzie ObjectName == "MSSQL$ INST2: bazy danych" i InstanceName == "główna" | Wszystkie dane dotyczące wydajności z wydajność bazy danych hello obiekt dla bazy danych master hello z hello nazwane wystąpienie programu SQL Server INST2.  

## <a name="viewing-performance-data"></a>Wyświetlanie danych wydajności
Podczas uruchamiania dziennika wyszukiwania danych dotyczących wydajności hello **listy** widoku jest wyświetlane domyślnie.  tooview hello danych w formie graficznej, kliknij przycisk **metryki**.  Widok szczegółowy graficznego kliknij hello  **+**  dalej tooa licznika.  

![Metryki widoku zwiniętego](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

dane wydajności tooaggregate w wyszukiwaniu dziennika, zobacz [agregacji metryki na żądanie i wizualizację w OMS](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/).


## <a name="next-steps"></a>Następne kroki
* [Zbierania liczników wydajności z aplikacje w systemie Linux](log-analytics-data-sources-linux-applications.md) tym MySQL i Apache HTTP Server.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.  
* Eksportuj dane zebrane za[usługi Power BI](log-analytics-powerbi.md) dodatkowe wizualizacje i analizy.
