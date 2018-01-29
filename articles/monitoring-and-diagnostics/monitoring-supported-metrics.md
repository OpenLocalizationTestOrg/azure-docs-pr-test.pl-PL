---
title: "Metryki Monitor Azure - obsługiwanych metryki na typ zasobu | Dokumentacja firmy Microsoft"
description: "Lista dostępnych dla każdego typu zasobu z monitorem Azure metryk."
author: anirudhcavale
manager: ashwink
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/18/2017
ms.author: ancav
ms.openlocfilehash: 673f5a5cd6832adb031ef72ce25f8a1622717cfd
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Obsługiwane metryki z monitorem Azure
Azure Monitor udostępnia kilka metod do interakcji z metryk, takich jak wykresy je w portalu, dostępu do nich za pośrednictwem interfejsu API REST lub zapytań je przy użyciu programu PowerShell lub interfejsu wiersza polecenia. Poniżej przedstawiono pełną listę wszystkich metryki obecnie z potoku metryki Azure monitora.

> [!NOTE]
> Inne metryki mogą być dostępne w portalu lub przy użyciu starszej wersji interfejsów API. Ta lista zawiera tylko metryk dostępnych za pośrednictwem potoku metryki skonsolidowanych Azure Monitor. Wykonanie kwerendy i dostępu do metryki z wymiarów, użyj [wersja interfejsu api 2017-05-01-preview](https://docs.microsoft.com/rest/api/monitor/metricdefinitions)
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|qpu_metric|QPU|Licznik|Średnia|QPU. Zakres 0-100 S1, 0 – 200 S2 i 0-400 dla S4|ServerResourceType|
|memory_metric|Memory (Pamięć)|Bajty|Średnia|Pamięci. W zakresie 0 – 25 GB na S1, 0 – 50 GB na S2 i 0 – 100 GB dla S4|ServerResourceType|
|TotalConnectionRequests|Całkowita liczba połączeń żądań|Licznik|Średnia|Całkowita liczba połączeń żądania. Są to przyjęcia.|ServerResourceType|
|SuccessfullConnectionsPerSec|Udane połączenia na sekundę|CountPerSecond|Średnia|Szybkość zakończeń udane połączenie.|ServerResourceType|
|TotalConnectionFailures|Całkowita liczba awarii|Licznik|Średnia|Całkowita liczba nieudanych prób połączenia.|ServerResourceType|
|CurrentUserSessions|Bieżące sesje użytkowników|Licznik|Średnia|Bieżąca liczba ustanowionych sesji użytkownika.|ServerResourceType|
|QueryPoolBusyThreads|Zapytanie z puli wątków zajęty|Licznik|Średnia|Liczba zajętych wątków w puli wątków zapytania.|ServerResourceType|
|CommandPoolJobQueueLength|Długość kolejki zadań puli polecenia|Licznik|Średnia|Liczba zadań w kolejce polecenia puli wątków.|ServerResourceType|
|ProcessingPoolJobQueueLength|Długość kolejki zadań przetwarzania w puli|Licznik|Średnia|Liczba zadań z systemem innym niż — I/O kolejki puli wątków przetwarzania.|ServerResourceType|
|CurrentConnections|Połączenia: Bieżąca liczba połączeń|Licznik|Średnia|Bieżąca liczba połączeń klienta.|ServerResourceType|
|CleanerCurrentPrice|Pamięci: Czyszczący bieżąca cena|Licznik|Średnia|Bieżąca cena pamięci $/ byte/godzina znormalizowane do 1000.|ServerResourceType|
|CleanerMemoryShrinkable|Pamięci: Zmniejszania pamięci czyszczący|Bajty|Średnia|Ilość pamięci w bajtach, mogą ulec czyszcząca przeczyszczanie w tle.|ServerResourceType|
|CleanerMemoryNonshrinkable|Pamięci: Czyszczący nonshrinkable pamięci|Bajty|Średnia|Ilość pamięci w bajtach, nie może ulec czyszcząca przeczyszczanie w tle.|ServerResourceType|
|MemoryUsage|Pamięci: Użycie pamięci|Bajty|Średnia|Użycie pamięci przez proces serwera jako używaną przy obliczaniu czyszczący cena pamięci. Taki sam jak licznika Process\PrivateBytes powiększony o rozmiar danych mapowanych na pamięć, ignorując wszystkie pamięci, która została zamapowana lub przydzielone przez aparat analizy w pamięci xVelocity (VertiPaq) przekracza Limit pamięci silnik xVelocity.|ServerResourceType|
|MemoryLimitHard|Pamięci: Twarde Limit pamięci|Bajty|Średnia|Limit pamięci twardym z pliku konfiguracji.|ServerResourceType|
|MemoryLimitHigh|Pamięć: Wysoki Limit pamięci|Bajty|Średnia|Limit pamięci wysokiej z pliku konfiguracji.|ServerResourceType|
|MemoryLimitLow|Pamięci: Niski Limit pamięci|Bajty|Średnia|Limit pamięci z pliku konfiguracji.|ServerResourceType|
|MemoryLimitVertiPaq|Pamięci: VertiPaq Limit pamięci|Bajty|Średnia|Limit w pamięci z pliku konfiguracji.|ServerResourceType|
|Przydział|Pamięć: limit przydziału|Bajty|Średnia|Limit przydziału pamięci, w bajtach. Limit przydziału pamięci jest nazywana rezerwacji pamięci grant lub pamięci.|ServerResourceType|
|QuotaBlocked|Pamięci: Zablokowane przydziału|Licznik|Średnia|Bieżąca liczba żądań przydziału, które są zablokowane, dopóki nie są zwalniane innych przydziałów pamięci.|ServerResourceType|
|VertiPaqNonpaged|Pamięci: Niestronicowana VertiPaq|Bajty|Średnia|Zablokowane bajtów pamięci zestawu do użycia przez aparat w pamięci roboczego.|ServerResourceType|
|VertiPaqPaged|Pamięci: Stronicowanej VertiPaq|Bajty|Średnia|Liczba bajtów stronicowanej pamięci dla danych w pamięci.|ServerResourceType|
|RowsReadPerSec|Przetwarzanie: Wiersze do odczytu na sekundę|CountPerSecond|Średnia|Liczba wierszy odczytywać wszystkie relacyjnych baz danych.|ServerResourceType|
|RowsConvertedPerSec|Przetwarzanie: Wierszy przekonwertowane na sekundę|CountPerSecond|Średnia|Liczba wierszy przekonwertować podczas przetwarzania.|ServerResourceType|
|RowsWrittenPerSec|Przetwarzanie: Wierszy, zapisany na sekundę|CountPerSecond|Średnia|Liczba wierszy, zapisany podczas przetwarzania.|ServerResourceType|
|CommandPoolBusyThreads|Wątki: Polecenie zajęty z puli wątków|Licznik|Średnia|Liczba zajętych wątków w puli wątków polecenia.|ServerResourceType|
|CommandPoolIdleThreads|Wątków: Polecenie puli wątków bezczynności|Licznik|Średnia|Liczba bezczynności wątków w puli wątków polecenia.|ServerResourceType|
|LongParsingBusyThreads|Wątków: Podczas analizowania zajęty wątków Long|Licznik|Średnia|Liczba zajętych wątków w puli wątków długo analizy.|ServerResourceType|
|LongParsingIdleThreads|Wątków: Podczas analizowania bezczynności wątków Long|Licznik|Średnia|Liczba bezczynności wątków w puli wątków długo analizy.|ServerResourceType|
|LongParsingJobQueueLength|Wątki: Czas analizowania długość kolejki zadań|Licznik|Średnia|Liczba zadań w kolejce długo analizy puli wątków.|ServerResourceType|
|ProcessingPoolBusyIOJobThreads|Wątki: Przetwarzania puli wątków zajęty zadania we/wy|Licznik|Średnia|Liczba wątków uruchomionych zadań we/wy w puli wątków przetwarzania.|ServerResourceType|
|ProcessingPoolBusyNonIOThreads|Wątków: Zajęty z puli wątków nie I/O przetwarzania|Licznik|Średnia|Liczba wątków uruchomionych zadań nie I/O w puli wątków przetwarzania.|ServerResourceType|
|ProcessingPoolIOJobQueueLength|Wątki: Przetwarzanie puli długość kolejki zadania we/wy|Licznik|Średnia|Liczba operacji We/Wy zadań w kolejce puli wątków przetwarzania.|ServerResourceType|
|ProcessingPoolIdleIOJobThreads|Wątki: Przetwarzania puli wątków bezczynności zadania we/wy|Licznik|Średnia|Liczba wątków bezczynności zadań we/wy w puli wątków przetwarzania.|ServerResourceType|
|ProcessingPoolIdleNonIOThreads|Wątki: Przetwarzanie bezczynności z puli wątków nie I/E|Licznik|Średnia|Liczba bezczynności wątków w puli wątków przetwarzania dedykowane dla zadań innych niż — I/O.|ServerResourceType|
|QueryPoolIdleThreads|Wątków: Wątki bezczynności puli zapytania|Licznik|Średnia|Liczba wątków bezczynności zadań we/wy w puli wątków przetwarzania.|ServerResourceType|
|QueryPoolJobQueueLength|Wątków: Lengt kolejki zadań puli zapytania|Licznik|Średnia|Liczba zadań w kolejce zapytań puli wątków.|ServerResourceType|
|ShortParsingBusyThreads|Wątków: Podczas analizowania zajęty wątków krótkiej|Licznik|Średnia|Liczba wątków zajęty w krótkim analizy puli wątków.|ServerResourceType|
|ShortParsingIdleThreads|Wątków: Podczas analizowania bezczynności wątków krótkiej|Licznik|Średnia|Liczba wątków bezczynności w krótkim analizy puli wątków.|ServerResourceType|
|ShortParsingJobQueueLength|Wątków: Podczas analizowania długość kolejki zadań krótkiej|Licznik|Średnia|Liczba zadań w kolejce krótkich analizy puli wątków.|ServerResourceType|
|memory_thrashing_metric|Wykonywania niepotrzebnych replik pamięci|Procent|Średnia|Średnia pamięci wykonywania niepotrzebnych replik.|ServerResourceType|
|mashup_engine_qpu_metric|Aparat M QPU|Licznik|Średnia|Użycie QPU przez procesy wyszukiwarek zestawu połączonych danych|ServerResourceType|
|mashup_engine_memory_metric|M aparat pamięci|Bajty|Średnia|Użycie pamięci przez procesy wyszukiwarek zestawu połączonych danych|ServerResourceType|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|TotalRequests|Brama całkowita liczba żądań|Licznik|Łącznie|Liczba żądań bramy|Lokalizacja, nazwy hosta|
|SuccessfulRequests|Bramy pomyślnych żądań|Licznik|Łącznie|Liczba żądań pomyślnie bramy|Lokalizacja, nazwy hosta|
|UnauthorizedRequests|Brama nieautoryzowanych żądań|Licznik|Łącznie|Liczba żądań nieautoryzowanych bramy|Lokalizacja, nazwy hosta|
|FailedRequests|Żądań zakończonych niepowodzeniem bramy|Licznik|Łącznie|Liczba błędów w żądaniach bramy|Lokalizacja, nazwy hosta|
|OtherRequests|Inne żądania bramy|Licznik|Łącznie|Liczba innych żądań bramy|Lokalizacja, nazwy hosta|
|Czas trwania|Łączny czas realizacji żądania bramy|Milisekundy|Średnia|Ogólny czas trwania z bramy żądań w milisekundach|Lokalizacja, nazwy hosta|
|Pojemność|Wydajność (wersja zapoznawcza)|Procent|Maksimum|Metryki użycia usługi ApiManagement|Lokalizacja|

## <a name="microsoftautomationautomationaccounts"></a>Microsoft.Automation/automationAccounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|TotalJob|Całkowita liczba zadań|Licznik|Łącznie|Całkowita liczba zadań|RunbookName, stan|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|CoreCount|Dedykowany liczby rdzeni|Licznik|Łącznie|Całkowita liczba rdzeni dedykowanego konta usługi partia zadań|Nie wymiarów|
|TotalNodeCount|Liczba dedykowanych węzłów|Licznik|Łącznie|Całkowita liczba dedykowanych węzłów w ramach konta usługi partia zadań|Nie wymiarów|
|LowPriorityCoreCount|Liczby rdzeni LowPriority|Licznik|Łącznie|Całkowita liczba rdzeni niskiego priorytetu konta usługi partia zadań|Nie wymiarów|
|TotalLowPriorityNodeCount|Liczba węzłów o niskim priorytecie|Licznik|Łącznie|Całkowita liczba węzłów niskiego priorytetu w ramach konta usługi partia zadań|Nie wymiarów|
|CreatingNodeCount|Tworzenie liczba węzłów|Licznik|Łącznie|Liczba węzłów tworzona|Nie wymiarów|
|StartingNodeCount|Początkowa liczba węzłów|Licznik|Łącznie|Liczba węzłów uruchamiania|Nie wymiarów|
|WaitingForStartTaskNodeCount|Liczba węzłów zadań Start oczekiwania|Licznik|Łącznie|Liczba węzłów oczekiwanie na zakończenie zadania Start|Nie wymiarów|
|StartTaskFailedNodeCount|Zadania uruchamiania nie powiodło się liczba węzłów|Licznik|Łącznie|Liczba węzłów, gdzie uruchomić zadanie nie powiodło się|Nie wymiarów|
|IdleNodeCount|Liczba węzłów w stanie bezczynności|Licznik|Łącznie|Liczba węzłów bezczynności|Nie wymiarów|
|OfflineNodeCount|Liczba węzłów w trybie offline|Licznik|Łącznie|Liczba węzłów w trybie offline|Nie wymiarów|
|RebootingNodeCount|Liczba węzłów ponowny rozruch|Licznik|Łącznie|Liczba ponowny rozruch węzłów|Nie wymiarów|
|ReimagingNodeCount|Liczba węzłów ponownej instalacji systemu|Licznik|Łącznie|Liczba węzłów, ponownej instalacji systemu|Nie wymiarów|
|RunningNodeCount|Liczba węzłów|Licznik|Łącznie|Liczba uruchomionych węzłach|Nie wymiarów|
|LeavingPoolNodeCount|Pozostawienie liczba węzłów w puli|Licznik|Łącznie|Liczba węzłów, pozostawiając puli|Nie wymiarów|
|UnusableNodeCount|Nie można użyć liczba węzłów|Licznik|Łącznie|Liczba węzłów bezużyteczne|Nie wymiarów|
|PreemptedNodeCount|Wywłaszczone liczba węzłów|Licznik|Łącznie|Liczba węzłów przeniesiona|Nie wymiarów|
|TaskStartEvent|Zadanie rozpoczęcia zdarzenia|Licznik|Łącznie|Całkowita liczba zadań, które zostały uruchomione|Nie wymiarów|
|TaskCompleteEvent|Zadania ukończone zdarzenia|Licznik|Łącznie|Całkowita liczba zadań, które zostały ukończone|Nie wymiarów|
|TaskFailEvent|Zdarzenia błędów zadań|Licznik|Łącznie|Całkowita liczba zadań, które zostały ukończone w stanie niepowodzenia|Nie wymiarów|
|PoolCreateEvent|Pula Tworzenie zdarzenia|Licznik|Łącznie|Całkowita liczba pul, które zostały utworzone|Nie wymiarów|
|PoolResizeStartEvent|Zdarzenia rozpoczęcia zmiany rozmiaru puli|Licznik|Łącznie|Całkowita liczba zmienia rozmiar puli, które zostały uruchomione|Nie wymiarów|
|PoolResizeCompleteEvent|Zakończenie zdarzenia zmiany rozmiaru puli|Licznik|Łącznie|Całkowita liczba zmienia rozmiar puli, które zostały ukończone|Nie wymiarów|
|PoolDeleteStartEvent|Pula Usuń rozpoczęcia zdarzenia|Licznik|Łącznie|Całkowita liczba usuwa puli, które zostały uruchomione|Nie wymiarów|
|PoolDeleteCompleteEvent|Zakończenie zdarzenia Delete puli|Licznik|Łącznie|Całkowita liczba usuwa puli, które zostały ukończone|Nie wymiarów|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|connectedclients|Połączeni klienci|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed|Łączna liczba operacji|Licznik|Łącznie||Nie wymiarów|
|Trafienia w pamięci podręcznej|Trafienia w pamięci podręcznej|Licznik|Łącznie||Nie wymiarów|
|cachemisses|Chybienia w pamięci podręcznej|Licznik|Łącznie||Nie wymiarów|
|getcommands|Pobrania|Licznik|Łącznie||Nie wymiarów|
|setcommands|Zestawy|Licznik|Łącznie||Nie wymiarów|
|evictedkeys|Wykluczone klucze|Licznik|Łącznie||Nie wymiarów|
|totalkeys|Całkowita liczba kluczy|Licznik|Maksimum||Nie wymiarów|
|expiredkeys|Wygasłe klucze|Licznik|Łącznie||Nie wymiarów|
|usedmemory|Użyta pamięć|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss|Używana pamięć RSS|Bajty|Maksimum||Nie wymiarów|
|serverLoad|Obciążenie serwera|Procent|Maksimum||Nie wymiarów|
|cacheWrite|Zapis w pamięci podręcznej|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead|Odczyt pamięci podręcznej|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime|Procesor CPU|Procent|Maksimum||Nie wymiarów|
|connectedclients0|Podłączeni klienci (niezależnego fragmentu 0)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed0|Całkowita liczba operacji (identyfikator niezależnego fragmentu 0)|Licznik|Łącznie||Nie wymiarów|
|cachehits0|Trafień w pamięci podręcznej (niezależnego fragmentu 0)|Licznik|Łącznie||Nie wymiarów|
|cachemisses0|Chybienia pamięci podręcznej (niezależnego fragmentu 0)|Licznik|Łącznie||Nie wymiarów|
|getcommands0|Pobiera (niezależnego fragmentu 0)|Licznik|Łącznie||Nie wymiarów|
|setcommands0|Zestawy (niezależnego fragmentu 0)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys0|Klucze wykluczonym (niezależnego fragmentu 0)|Licznik|Łącznie||Nie wymiarów|
|totalkeys0|Wszystkie klucze (niezależnego fragmentu 0)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys0|Wygasłe kluczy (niezależnego fragmentu 0)|Licznik|Łącznie||Nie wymiarów|
|usedmemory0|Używana pamięć (niezależnego fragmentu 0)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss0|Używana pamięć RSS (niezależnego fragmentu 0)|Bajty|Maksimum||Nie wymiarów|
|serverLoad0|Obciążenia serwera (niezależnego fragmentu 0)|Procent|Maksimum||Nie wymiarów|
|cacheWrite0|Pamięć podręczna zapisu (niezależnego fragmentu 0)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead0|Odczytu pamięci podręcznej (niezależnego fragmentu 0)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime0|Procesor (niezależnego fragmentu 0)|Procent|Maksimum||Nie wymiarów|
|connectedclients1|Podłączeni klienci (niezależnego fragmentu 1)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed1|Całkowita liczba operacji (identyfikator niezależnego fragmentu 1)|Licznik|Łącznie||Nie wymiarów|
|cachehits1|Trafień w pamięci podręcznej (niezależnego fragmentu 1)|Licznik|Łącznie||Nie wymiarów|
|cachemisses1|Chybienia pamięci podręcznej (niezależnego fragmentu 1)|Licznik|Łącznie||Nie wymiarów|
|getcommands1|Pobiera (niezależnego fragmentu 1)|Licznik|Łącznie||Nie wymiarów|
|setcommands1|Zestawy (niezależnego fragmentu 1)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys1|Klucze wykluczonym (niezależnego fragmentu 1)|Licznik|Łącznie||Nie wymiarów|
|totalkeys1|Wszystkie klucze (niezależnego fragmentu 1)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys1|Wygasłe kluczy (niezależnego fragmentu 1)|Licznik|Łącznie||Nie wymiarów|
|usedmemory1|Używana pamięć (niezależnego fragmentu 1)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss1|Używana pamięć RSS (niezależnego fragmentu 1)|Bajty|Maksimum||Nie wymiarów|
|serverLoad1|Obciążenia serwera (niezależnego fragmentu 1)|Procent|Maksimum||Nie wymiarów|
|cacheWrite1|Pamięć podręczna zapisu (niezależnego fragmentu 1)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead1|Odczytu pamięci podręcznej (niezależnego fragmentu 1)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime1|Procesor (niezależnego fragmentu 1)|Procent|Maksimum||Nie wymiarów|
|connectedclients2|Podłączeni klienci (niezależnego fragmentu 2)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed2|Całkowita liczba operacji (identyfikator niezależnego fragmentu 2)|Licznik|Łącznie||Nie wymiarów|
|cachehits2|Trafień w pamięci podręcznej (niezależnego fragmentu 2)|Licznik|Łącznie||Nie wymiarów|
|cachemisses2|Chybienia pamięci podręcznej (niezależnego fragmentu 2)|Licznik|Łącznie||Nie wymiarów|
|getcommands2|Pobiera (niezależnego fragmentu 2)|Licznik|Łącznie||Nie wymiarów|
|setcommands2|Zestawy (niezależnego fragmentu 2)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys2|Klucze wykluczonym (niezależnego fragmentu 2)|Licznik|Łącznie||Nie wymiarów|
|totalkeys2|Wszystkie klucze (niezależnego fragmentu 2)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys2|Wygasłe kluczy (niezależnego fragmentu 2)|Licznik|Łącznie||Nie wymiarów|
|usedmemory2|Używana pamięć (niezależnego fragmentu 2)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss2|Używana pamięć RSS (niezależnego fragmentu 2)|Bajty|Maksimum||Nie wymiarów|
|serverLoad2|Obciążenia serwera (niezależnego fragmentu 2)|Procent|Maksimum||Nie wymiarów|
|cacheWrite2|Pamięć podręczna zapisu (niezależnego fragmentu 2)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead2|Odczytu pamięci podręcznej (niezależnego fragmentu 2)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime2|Procesor (niezależnego fragmentu 2)|Procent|Maksimum||Nie wymiarów|
|connectedclients3|Podłączeni klienci (niezależnego fragmentu 3)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed3|Całkowita liczba operacji (identyfikator niezależnego fragmentu 3)|Licznik|Łącznie||Nie wymiarów|
|cachehits3|Trafień w pamięci podręcznej (niezależnego fragmentu 3)|Licznik|Łącznie||Nie wymiarów|
|cachemisses3|Chybienia pamięci podręcznej (niezależnego fragmentu 3)|Licznik|Łącznie||Nie wymiarów|
|getcommands3|Pobiera (niezależnego fragmentu 3)|Licznik|Łącznie||Nie wymiarów|
|setcommands3|Zestawy (niezależnego fragmentu 3)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys3|Klucze wykluczonym (niezależnego fragmentu 3)|Licznik|Łącznie||Nie wymiarów|
|totalkeys3|Wszystkie klucze (niezależnego fragmentu 3)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys3|Wygasłe kluczy (niezależnego fragmentu 3)|Licznik|Łącznie||Nie wymiarów|
|usedmemory3|Używana pamięć (niezależnego fragmentu 3)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss3|Używana pamięć RSS (niezależnego fragmentu 3)|Bajty|Maksimum||Nie wymiarów|
|serverLoad3|Obciążenia serwera (niezależnego fragmentu 3)|Procent|Maksimum||Nie wymiarów|
|cacheWrite3|Pamięć podręczna zapisu (niezależnego fragmentu 3)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead3|Odczytu pamięci podręcznej (niezależnego fragmentu 3)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime3|Procesor (niezależnego fragmentu 3)|Procent|Maksimum||Nie wymiarów|
|connectedclients4|Podłączeni klienci (niezależnego fragmentu 4)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed4|Całkowita liczba operacji (identyfikator niezależnego fragmentu 4)|Licznik|Łącznie||Nie wymiarów|
|cachehits4|Trafień w pamięci podręcznej (niezależnego fragmentu 4)|Licznik|Łącznie||Nie wymiarów|
|cachemisses4|Chybienia pamięci podręcznej (niezależnego fragmentu 4)|Licznik|Łącznie||Nie wymiarów|
|getcommands4|Pobiera (niezależnego fragmentu 4)|Licznik|Łącznie||Nie wymiarów|
|setcommands4|Zestawy (niezależnego fragmentu 4)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys4|Klucze wykluczonym (niezależnego fragmentu 4)|Licznik|Łącznie||Nie wymiarów|
|totalkeys4|Wszystkie klucze (niezależnego fragmentu 4)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys4|Wygasłe kluczy (niezależnego fragmentu 4)|Licznik|Łącznie||Nie wymiarów|
|usedmemory4|Używana pamięć (niezależnego fragmentu 4)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss4|Używana pamięć RSS (niezależnego fragmentu 4)|Bajty|Maksimum||Nie wymiarów|
|serverLoad4|Obciążenia serwera (niezależnego fragmentu 4)|Procent|Maksimum||Nie wymiarów|
|cacheWrite4|Pamięć podręczna zapisu (niezależnego fragmentu 4)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead4|Odczytu pamięci podręcznej (niezależnego fragmentu 4)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime4|Procesor (niezależnego fragmentu 4)|Procent|Maksimum||Nie wymiarów|
|connectedclients5|Podłączeni klienci (niezależnego fragmentu 5)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed5|Całkowita liczba operacji (identyfikator niezależnego fragmentu 5)|Licznik|Łącznie||Nie wymiarów|
|cachehits5|Trafień w pamięci podręcznej (niezależnego fragmentu 5)|Licznik|Łącznie||Nie wymiarów|
|cachemisses5|Chybienia pamięci podręcznej (niezależnego fragmentu 5)|Licznik|Łącznie||Nie wymiarów|
|getcommands5|Pobiera (niezależnego fragmentu 5)|Licznik|Łącznie||Nie wymiarów|
|setcommands5|Zestawy (niezależnego fragmentu 5)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys5|Klucze wykluczonym (niezależnego fragmentu 5)|Licznik|Łącznie||Nie wymiarów|
|totalkeys5|Wszystkie klucze (niezależnego fragmentu 5)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys5|Wygasłe kluczy (niezależnego fragmentu 5)|Licznik|Łącznie||Nie wymiarów|
|usedmemory5|Używana pamięć (niezależnego fragmentu 5)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss5|Używana pamięć RSS (niezależnego fragmentu 5)|Bajty|Maksimum||Nie wymiarów|
|serverLoad5|Obciążenia serwera (niezależnego fragmentu 5)|Procent|Maksimum||Nie wymiarów|
|cacheWrite5|Pamięć podręczna zapisu (niezależnego fragmentu 5)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead5|Odczytu pamięci podręcznej (niezależnego fragmentu 5)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime5|Procesor (niezależnego fragmentu 5)|Procent|Maksimum||Nie wymiarów|
|connectedclients6|Podłączeni klienci (niezależnego fragmentu 6)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed6|Całkowita liczba operacji (identyfikator niezależnego fragmentu 6)|Licznik|Łącznie||Nie wymiarów|
|cachehits6|Trafień w pamięci podręcznej (niezależnego fragmentu 6)|Licznik|Łącznie||Nie wymiarów|
|cachemisses6|Chybienia pamięci podręcznej (niezależnego fragmentu 6)|Licznik|Łącznie||Nie wymiarów|
|getcommands6|Pobiera (niezależnego fragmentu 6)|Licznik|Łącznie||Nie wymiarów|
|setcommands6|Zestawy (niezależnego fragmentu 6)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys6|Klucze wykluczonym (niezależnego fragmentu 6)|Licznik|Łącznie||Nie wymiarów|
|totalkeys6|Wszystkie klucze (niezależnego fragmentu 6)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys6|Wygasłe kluczy (niezależnego fragmentu 6)|Licznik|Łącznie||Nie wymiarów|
|usedmemory6|Używana pamięć (niezależnego fragmentu 6)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss6|Używana pamięć RSS (niezależnego fragmentu 6)|Bajty|Maksimum||Nie wymiarów|
|serverLoad6|Obciążenia serwera (niezależnego fragmentu 6)|Procent|Maksimum||Nie wymiarów|
|cacheWrite6|Pamięć podręczna zapisu (niezależnego fragmentu 6)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead6|Odczytu pamięci podręcznej (niezależnego fragmentu 6)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime6|Procesor (niezależnego fragmentu 6)|Procent|Maksimum||Nie wymiarów|
|connectedclients7|Podłączeni klienci (niezależnego fragmentu 7)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed7|Całkowita liczba operacji (identyfikator niezależnego fragmentu 7)|Licznik|Łącznie||Nie wymiarów|
|cachehits7|Trafień w pamięci podręcznej (niezależnego fragmentu 7)|Licznik|Łącznie||Nie wymiarów|
|cachemisses7|Chybienia pamięci podręcznej (niezależnego fragmentu 7)|Licznik|Łącznie||Nie wymiarów|
|getcommands7|Pobiera (niezależnego fragmentu 7)|Licznik|Łącznie||Nie wymiarów|
|setcommands7|Zestawy (niezależnego fragmentu 7)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys7|Klucze wykluczonym (niezależnego fragmentu 7)|Licznik|Łącznie||Nie wymiarów|
|totalkeys7|Wszystkie klucze (niezależnego fragmentu 7)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys7|Wygasłe kluczy (niezależnego fragmentu 7)|Licznik|Łącznie||Nie wymiarów|
|usedmemory7|Używana pamięć (niezależnego fragmentu 7)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss7|Używana pamięć RSS (niezależnego fragmentu 7)|Bajty|Maksimum||Nie wymiarów|
|serverLoad7|Obciążenia serwera (niezależnego fragmentu 7)|Procent|Maksimum||Nie wymiarów|
|cacheWrite7|Pamięć podręczna zapisu (niezależnego fragmentu 7)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead7|Odczytu pamięci podręcznej (niezależnego fragmentu 7)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime7|Procesor (niezależnego fragmentu 7)|Procent|Maksimum||Nie wymiarów|
|connectedclients8|Podłączeni klienci (niezależnego fragmentu 8)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed8|Całkowita liczba operacji (identyfikator niezależnego fragmentu 8)|Licznik|Łącznie||Nie wymiarów|
|cachehits8|Trafień w pamięci podręcznej (niezależnego fragmentu 8)|Licznik|Łącznie||Nie wymiarów|
|cachemisses8|Chybienia pamięci podręcznej (niezależnego fragmentu 8)|Licznik|Łącznie||Nie wymiarów|
|getcommands8|Pobiera (niezależnego fragmentu 8)|Licznik|Łącznie||Nie wymiarów|
|setcommands8|Zestawy (niezależnego fragmentu 8)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys8|Klucze wykluczonym (niezależnego fragmentu 8)|Licznik|Łącznie||Nie wymiarów|
|totalkeys8|Wszystkie klucze (niezależnego fragmentu 8)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys8|Wygasłe kluczy (niezależnego fragmentu 8)|Licznik|Łącznie||Nie wymiarów|
|usedmemory8|Używana pamięć (niezależnego fragmentu 8)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss8|Używana pamięć RSS (niezależnego fragmentu 8)|Bajty|Maksimum||Nie wymiarów|
|serverLoad8|Obciążenia serwera (niezależnego fragmentu 8)|Procent|Maksimum||Nie wymiarów|
|cacheWrite8|Pamięć podręczna zapisu (niezależnego fragmentu 8)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead8|Odczytu pamięci podręcznej (niezależnego fragmentu 8)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime8|Procesor (niezależnego fragmentu 8)|Procent|Maksimum||Nie wymiarów|
|connectedclients9|Podłączeni klienci (niezależnego fragmentu 9)|Licznik|Maksimum||Nie wymiarów|
|totalcommandsprocessed9|Całkowita liczba operacji (identyfikator niezależnego fragmentu 9)|Licznik|Łącznie||Nie wymiarów|
|cachehits9|Trafień w pamięci podręcznej (niezależnego fragmentu 9)|Licznik|Łącznie||Nie wymiarów|
|cachemisses9|Chybienia pamięci podręcznej (niezależnego fragmentu 9)|Licznik|Łącznie||Nie wymiarów|
|getcommands9|Pobiera (niezależnego fragmentu 9)|Licznik|Łącznie||Nie wymiarów|
|setcommands9|Zestawy (niezależnego fragmentu 9)|Licznik|Łącznie||Nie wymiarów|
|evictedkeys9|Klucze wykluczonym (niezależnego fragmentu 9)|Licznik|Łącznie||Nie wymiarów|
|totalkeys9|Wszystkie klucze (niezależnego fragmentu 9)|Licznik|Maksimum||Nie wymiarów|
|expiredkeys9|Wygasłe kluczy (niezależnego fragmentu 9)|Licznik|Łącznie||Nie wymiarów|
|usedmemory9|Używana pamięć (niezależnego fragmentu 9)|Bajty|Maksimum||Nie wymiarów|
|usedmemoryRss9|Używana pamięć RSS (niezależnego fragmentu 9)|Bajty|Maksimum||Nie wymiarów|
|serverLoad9|Obciążenia serwera (niezależnego fragmentu 9)|Procent|Maksimum||Nie wymiarów|
|cacheWrite9|Pamięć podręczna zapisu (niezależnego fragmentu 9)|Bajty na sekundę|Maksimum||Nie wymiarów|
|cacheRead9|Odczytu pamięci podręcznej (niezależnego fragmentu 9)|Bajty na sekundę|Maksimum||Nie wymiarów|
|percentProcessorTime9|Procesor (niezależnego fragmentu 9)|Procent|Maksimum||Nie wymiarów|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.ClassicCompute/virtualMachines

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Procentowe użycie procesora CPU|Procentowe użycie procesora CPU|Procent|Średnia|Procent przydzielonych jednostek obliczeniowych, które są obecnie używane przez maszyny wirtualne.|Nie wymiarów|
|Sieć — wejście|Sieć — wejście|Bajty|Łącznie|Liczba bajtów odebranych ze wszystkich interfejsów sieciowych przez maszyny wirtualne (ruch przychodzący).|Nie wymiarów|
|Sieć — wyjście|Sieć — wyjście|Bajty|Łącznie|Liczba bajtów wysłanych we wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch wychodzący).|Nie wymiarów|
|Bajty odczytu dysku/s|Odczyt dysku|Bajty na sekundę|Średnia|Średnia liczba bajtów odczytanych z dysku w okresie monitorowania.|Nie wymiarów|
|Bajty zapisu dysku/s|Zapis dysku|Bajty na sekundę|Średnia|Średnia liczba bajtów zapisanych na dysku w okresie monitorowania.|Nie wymiarów|
|Operacje odczytu dysku/s|Operacje odczytu dysku/s|CountPerSecond|Średnia|Operacje we/wy na sekundę dotyczące odczytu z dysku.|Nie wymiarów|
|Operacje zapisu dysku/s|Operacje zapisu dysku/s|CountPerSecond|Średnia|Operacje we/wy na sekundę dotyczące zapisu na dysku.|Nie wymiarów|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|TotalCalls|Łączna liczba wywołań|Licznik|Łącznie|Łączna liczba wywołań.|Nie wymiarów|
|SuccessfulCalls|Wywołania zakończone powodzeniem|Licznik|Łącznie|Liczba wywołań zakończonych powodzeniem.|Nie wymiarów|
|TotalErrors|Łączna liczba błędów|Licznik|Łącznie|Łączna liczba wywołań z odpowiedzią oznaczającą błąd (odpowiedź HTTP o kodzie 4xx lub 5xx).|Nie wymiarów|
|BlockedCalls|Zablokowane wywołania|Licznik|Łącznie|Liczba wywołań, które przekraczają limit szybkości lub przydziału.|Nie wymiarów|
|ServerErrors|Błędy serwera|Licznik|Łącznie|Liczba wywołań z błędem wewnętrznym usługi (odpowiedź HTTP o kodzie 5xx).|Nie wymiarów|
|ClientErrors|Błędy klienta|Licznik|Łącznie|Liczba wywołań z błędem po stronie klienta (odpowiedź HTTP o kodzie 4xx).|Nie wymiarów|
|DataIn|Dane wejściowe|Bajty|Łącznie|Rozmiar danych przychodzących (w bajtach).|Nie wymiarów|
|DataOut|Dane wyjściowe|Bajty|Łącznie|Rozmiar danych wychodzących (w bajtach).|Nie wymiarów|
|Opóźnienie|Opóźnienie|W milisekundach|Średnia|Opóźnienie w milisekundach.|Nie wymiarów|
|CharactersTranslated|Przetłumaczone znaki|Licznik|Łącznie|Łączna liczba znaków w przychodzącym żądaniu tekstowym.|Nie wymiarów|
|SpeechSessionDuration|Czas trwania sesji mowy|Sekundy|Łącznie|Łączny czas trwania sesji mowy w sekundach.|Nie wymiarów|
|TotalTransactions|Całkowita liczba transakcji|Licznik|Łącznie|Całkowita liczba transakcji|Nie wymiarów|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Procentowe użycie procesora CPU|Procentowe użycie procesora CPU|Procent|Średnia|Procent przydzielonych jednostek obliczeniowych, które są obecnie używane przez maszyny wirtualne|Nie wymiarów|
|Sieć — wejście|Sieć — wejście|Bajty|Łącznie|Liczba bajtów odebranych ze wszystkich interfejsów sieciowych przez maszyny wirtualne (ruch przychodzący)|Nie wymiarów|
|Sieć — wyjście|Sieć — wyjście|Bajty|Łącznie|Liczba bajtów wysłanych we wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch wychodzący)|Nie wymiarów|
|Bajty odczytane z dysku|Bajty odczytane z dysku|Bajty|Łącznie|Całkowita liczba bajtów odczytanych z dysku w okresie monitorowania|Nie wymiarów|
|Bajty zapisane na dysku|Bajty zapisane na dysku|Bajty|Łącznie|Całkowita liczba bajtów zapisanych na dysku w okresie monitorowania|Nie wymiarów|
|Operacje odczytu dysku/s|Operacje odczytu dysku/s|CountPerSecond|Średnia|Operacje we/wy odczytu dysku|Nie wymiarów|
|Operacje zapisu dysku/s|Operacje zapisu dysku/s|CountPerSecond|Średnia|Operacje we/wy zapisu dysku|Nie wymiarów|
|Pozostałe środki na procesory CPU|Pozostałe środki na procesory CPU|Licznik|Średnia|Łączna ilość środków dostępnych na potrzeby serii|Nie wymiarów|
|Wykorzystane środki na procesory CPU|Wykorzystane środki na procesory CPU|Licznik|Średnia|Łączna ilość środków wykorzystanych przez maszynę wirtualną|Nie wymiarów|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Procentowe użycie procesora CPU|Procentowe użycie procesora CPU|Procent|Średnia|Procent przydzielonych jednostek obliczeniowych, które są obecnie używane przez maszyny wirtualne|Nie wymiarów|
|Sieć — wejście|Sieć — wejście|Bajty|Łącznie|Liczba bajtów odebranych ze wszystkich interfejsów sieciowych przez maszyny wirtualne (ruch przychodzący)|Nie wymiarów|
|Sieć — wyjście|Sieć — wyjście|Bajty|Łącznie|Liczba bajtów wysłanych we wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch wychodzący)|Nie wymiarów|
|Bajty odczytane z dysku|Bajty odczytane z dysku|Bajty|Łącznie|Całkowita liczba bajtów odczytanych z dysku w okresie monitorowania|Nie wymiarów|
|Bajty zapisane na dysku|Bajty zapisane na dysku|Bajty|Łącznie|Całkowita liczba bajtów zapisanych na dysku w okresie monitorowania|Nie wymiarów|
|Operacje odczytu dysku/s|Operacje odczytu dysku/s|CountPerSecond|Średnia|Operacje we/wy odczytu dysku|Nie wymiarów|
|Operacje zapisu dysku/s|Operacje zapisu dysku/s|CountPerSecond|Średnia|Operacje we/wy zapisu dysku|Nie wymiarów|
|Pozostałe środki na procesory CPU|Pozostałe środki na procesory CPU|Licznik|Średnia|Łączna ilość środków dostępnych na potrzeby serii|Nie wymiarów|
|Wykorzystane środki na procesory CPU|Wykorzystane środki na procesory CPU|Licznik|Średnia|Łączna ilość środków wykorzystanych przez maszynę wirtualną|Nie wymiarów|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Procentowe użycie procesora CPU|Procentowe użycie procesora CPU|Procent|Średnia|Procent przydzielonych jednostek obliczeniowych, które są obecnie używane przez maszyny wirtualne|Nie wymiarów|
|Sieć — wejście|Sieć — wejście|Bajty|Łącznie|Liczba bajtów odebranych ze wszystkich interfejsów sieciowych przez maszyny wirtualne (ruch przychodzący)|Nie wymiarów|
|Sieć — wyjście|Sieć — wyjście|Bajty|Łącznie|Liczba bajtów wysłanych we wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch wychodzący)|Nie wymiarów|
|Bajty odczytane z dysku|Bajty odczytane z dysku|Bajty|Łącznie|Całkowita liczba bajtów odczytanych z dysku w okresie monitorowania|Nie wymiarów|
|Bajty zapisane na dysku|Bajty zapisane na dysku|Bajty|Łącznie|Całkowita liczba bajtów zapisanych na dysku w okresie monitorowania|Nie wymiarów|
|Operacje odczytu dysku/s|Operacje odczytu dysku/s|CountPerSecond|Średnia|Operacje we/wy odczytu dysku|Nie wymiarów|
|Operacje zapisu dysku/s|Operacje zapisu dysku/s|CountPerSecond|Średnia|Operacje we/wy zapisu dysku|Nie wymiarów|
|Pozostałe środki na procesory CPU|Pozostałe środki na procesory CPU|Licznik|Średnia|Łączna ilość środków dostępnych na potrzeby serii|Nie wymiarów|
|Wykorzystane środki na procesory CPU|Wykorzystane środki na procesory CPU|Licznik|Średnia|Łączna ilość środków wykorzystanych przez maszynę wirtualną|Nie wymiarów|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|DCIApiCalls|Wywołania Insights interfejsu API klienta|Licznik|Łącznie||Nie wymiarów|
|DCIMappingImportOperationSuccessfulLines|Mapowanie wierszy pomyślnych operacji importu|Licznik|Łącznie||Nie wymiarów|
|DCIMappingImportOperationFailedLines|Mapowanie operacji importowania nie powiodła się wierszy|Licznik|Łącznie||Nie wymiarów|
|DCIMappingImportOperationTotalLines|Całkowita liczba wierszy operacji importu mapowania|Licznik|Łącznie||Nie wymiarów|
|DCIMappingImportOperationRuntimeInSeconds|Mapowanie importu operacji w czasie wykonywania w sekundach|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundProfileExportSucceeded|Eksportowanie profilu ruchu wychodzącego zakończyło się pomyślnie|Licznik|Łącznie||Nie wymiarów|
|DCIOutboundProfileExportFailed|Eksportowanie profilu ruchu wychodzącego nie powiodło się|Licznik|Łącznie||Nie wymiarów|
|DCIOutboundProfileExportDuration|Czas trwania eksportowania profilu ruchu wychodzącego|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundKpiExportSucceeded|Wychodzące eksportowanie Kpi powiodło się|Licznik|Łącznie||Nie wymiarów|
|DCIOutboundKpiExportFailed|Wychodzące eksportowanie wskaźnika Kpi nie powiodło się|Licznik|Łącznie||Nie wymiarów|
|DCIOutboundKpiExportDuration|Czas trwania wychodzącego eksportu wskaźnika Kpi|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundKpiExportStarted|Rozpoczęto eksportu wychodzącego kluczowego wskaźnika wydajności|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundKpiRecordCount|Liczba rekordów wychodzącego wskaźnika Kpi|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundProfileExportCount|Liczba eksportowania profilu ruchu wychodzącego|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundInitialProfileExportFailed|Eksportowanie wychodzącego początkowej profilu nie powiodło się|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundInitialProfileExportSucceeded|Wychodzące profilu początkowej eksportu|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundInitialKpiExportFailed|Wychodzące początkowej eksportowanie wskaźnika Kpi nie powiodło się|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundInitialKpiExportSucceeded|Wychodzące początkowej eksportu kluczowego wskaźnika wydajności zakończyło się pomyślnie.|Sekundy|Łącznie||Nie wymiarów|
|DCIOutboundInitialProfileExportDurationInSeconds|Wychodzące profilu początkowej eksportu czas w sekundach|Sekundy|Łącznie||Nie wymiarów|
|AdlaJobForStandardKpiFailed|Zadanie Adla dla standardowych wskaźnika Kpi nie powiodło się w sekundach|Sekundy|Łącznie||Nie wymiarów|
|AdlaJobForStandardKpiTimeOut|Zadanie Adla standardowa wskaźnika Kpi limitu czasu w sekundach|Sekundy|Łącznie||Nie wymiarów|
|AdlaJobForStandardKpiCompleted|Zadanie Adla standardowe kluczowego wskaźnika wydajności w sekundach|Sekundy|Łącznie||Nie wymiarów|
|ImportASAValuesFailed|Wartości ASA importu nie powiodła się, liczba|Licznik|Łącznie||Nie wymiarów|
|ImportASAValuesSucceeded|Wartości ASA importowanie zakończyło się pomyślnie, liczba|Licznik|Łącznie||Nie wymiarów|
|DCIProfilesCount|Liczba wystąpień profilu|Licznik|Ostatnia||Nie wymiarów|
|DCIInteractionsPerMonthCount|Interakcje na liczba miesięcy|Licznik|Ostatnia||Nie wymiarów|
|DCIKpisCount|Liczba wskaźnika KPI|Licznik|Ostatnia||Nie wymiarów|
|DCISegmentsCount|Liczba segmentów|Licznik|Ostatnia||Nie wymiarów|
|DCIPredictiveMatchPoliciesCount|Liczba dopasowań predykcyjnej|Licznik|Ostatnia||Nie wymiarów|
|DCIPredictionsCount|Liczba prognozowania|Licznik|Ostatnia||Nie wymiarów|

## <a name="microsoftdatafactorydatafactories"></a>Microsoft.DataFactory/datafactories

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|SuccessfulRuns|Pomyślne uruchomienia|Licznik|Łącznie|Liczba pomyślnych działa.|Nie wymiarów|
|FailedRuns|Nieudane uruchomienia|Licznik|Łącznie|Liczba uruchomień nie powiodło się.|Nie wymiarów|

## <a name="microsoftdatafactoryfactories"></a>Microsoft.DataFactory/factories

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|PipelineFailedRuns|Nie powiodło się metryki uruchamia potoku|Licznik|Łącznie||Nie wymiarów|
|PipelineSucceededRuns|Pomyślnie metryki uruchamia potoku|Licznik|Łącznie||Nie wymiarów|
|ActivityFailedRuns|Nie powiodło się metryki uruchomień działania|Licznik|Łącznie||Nie wymiarów|
|ActivitySucceededRuns|Pomyślnie metryki uruchomień działania|Licznik|Łącznie||Nie wymiarów|
|TriggerFailedRuns|Nie powiodło się wyzwalacz uruchamia metryk|Licznik|Łącznie||Nie wymiarów|
|TriggerSucceededRuns|Pomyślnie metryki uruchamia wyzwalacz|Licznik|Łącznie||Nie wymiarów|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|JobEndedSuccess|Zadania zakończone pomyślnie|Licznik|Łącznie|Liczba zadań zakończonych pomyślnie.|Nie wymiarów|
|JobEndedFailure|Zadania zakończone niepowodzeniem|Licznik|Łącznie|Liczba zadań zakończonych niepowodzeniem.|Nie wymiarów|
|JobEndedCancelled|Anulowane zadania|Licznik|Łącznie|Liczba zadań zostało anulowane.|Nie wymiarów|
|JobAUEndedSuccess|Pomyślne czasu Australia|Sekundy|Łącznie|Łączny czas Australia zadań zakończonych pomyślnie.|Nie wymiarów|
|JobAUEndedFailure|Czas Australia nie powiodło się|Sekundy|Łącznie|Łączny czas Australia zadania zakończone niepowodzeniem.|Nie wymiarów|
|JobAUEndedCancelled|Anulowane czasu Australia|Sekundy|Łącznie|Łączny czas Australia anulowane zadania.|Nie wymiarów|

## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.DataLakeStore/accounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|TotalStorage|Całkowita ilość miejsca|Bajty|Maksimum|Całkowita ilość danych przechowywanych w ramach konta.|Nie wymiarów|
|DataWritten|Dane zapisywane|Bajty|Łącznie|Całkowita ilość danych zapisywane na koncie.|Nie wymiarów|
|Odczyt danych|Odczyt danych|Bajty|Łącznie|Łączna ilość danych do odczytu z konta.|Nie wymiarów|
|WriteRequests|Żądania zapisu|Licznik|Łącznie|Liczba danych żądań zapisu do konta.|Nie wymiarów|
|ReadRequests|Żądania odczytu|Licznik|Łącznie|Liczba danych do odczytu żądania do tego konta.|Nie wymiarów|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|cpu_percent|Procent procesora CPU|Procent|Średnia|Procent procesora CPU|Nie wymiarów|
|compute_limit|Obliczenia bazy danych limit jednostki|Licznik|Średnia|Obliczenia bazy danych limit jednostki|Nie wymiarów|
|compute_consumption_percent|Obliczenia bazy danych procent jednostki|Procent|Średnia|Obliczenia bazy danych procent jednostki|Nie wymiarów|
|memory_percent|Procent pamięci|Procent|Średnia|Procent pamięci|Nie wymiarów|
|io_consumption_percent|Procent we/wy|Procent|Średnia|Procent we/wy|Nie wymiarów|
|storage_percent|Procent użycia magazynu|Procent|Średnia|Procent użycia magazynu|Nie wymiarów|
|storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|Nie wymiarów|
|storage_limit|Limit magazynu|Bajty|Średnia|Limit magazynu|Nie wymiarów|
|active_connections|Całkowita liczba aktywnych połączeń|Licznik|Średnia|Całkowita liczba aktywnych połączeń|Nie wymiarów|
|connections_failed|Całkowita liczba połączeń nie powiodło się|Licznik|Średnia|Całkowita liczba połączeń nie powiodło się|Nie wymiarów|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|cpu_percent|Procent procesora CPU|Procent|Średnia|Procent procesora CPU|Nie wymiarów|
|compute_limit|Obliczenia bazy danych limit jednostki|Licznik|Średnia|Obliczenia bazy danych limit jednostki|Nie wymiarów|
|compute_consumption_percent|Obliczenia bazy danych procent jednostki|Procent|Średnia|Obliczenia bazy danych procent jednostki|Nie wymiarów|
|memory_percent|Procent pamięci|Procent|Średnia|Procent pamięci|Nie wymiarów|
|io_consumption_percent|Procent we/wy|Procent|Średnia|Procent we/wy|Nie wymiarów|
|storage_percent|Procent użycia magazynu|Procent|Średnia|Procent użycia magazynu|Nie wymiarów|
|storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|Nie wymiarów|
|storage_limit|Limit magazynu|Bajty|Średnia|Limit magazynu|Nie wymiarów|
|active_connections|Całkowita liczba aktywnych połączeń|Licznik|Średnia|Całkowita liczba aktywnych połączeń|Nie wymiarów|
|connections_failed|Całkowita liczba połączeń nie powiodło się|Licznik|Średnia|Całkowita liczba połączeń nie powiodło się|Nie wymiarów|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Próby wysłania wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów telemetrii urządzenia do chmury próby wysłania do Centrum IoT|Nie wymiarów|
|d2c.telemetry.ingress.SUCCESS|Wysłane wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów telemetrii urządzenia do chmury pomyślnie wysłane do Centrum IoT|Nie wymiarów|
|c2d.Commands.egress.COMPLETE.SUCCESS|Polecenia zakończona|Licznik|Łącznie|Liczba poleceń chmury do urządzenia, które zakończyło się powodzeniem, urządzenia|Nie wymiarów|
|c2d.Commands.egress.Abandon.SUCCESS|Porzucone poleceń|Licznik|Łącznie|Liczba poleceń chmury do urządzenia porzucone przez urządzenie|Nie wymiarów|
|c2d.Commands.egress.Reject.SUCCESS|Polecenia odrzucone|Licznik|Łącznie|Liczba odrzuconych przez urządzenie poleceń chmury do urządzenia|Nie wymiarów|
|devices.totalDevices|Łączna liczba urządzeń|Licznik|Łącznie|Liczba urządzeń zarejestrowanych do Centrum IoT|Nie wymiarów|
|devices.connectedDevices.allProtocol|Połączonych urządzeń|Licznik|Łącznie|Liczba urządzeń połączonych z Centrum IoT|Nie wymiarów|
|d2c.telemetry.egress.SUCCESS|Dostarczane wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów pomyślnie zostały zapisane do punktów końcowych (łącznie)|Nie wymiarów|
|d2c.telemetry.egress.dropped|Porzucone komunikaty|Licznik|Łącznie|Liczba wiadomości porzuconych z powodu braku punktu końcowego dostarczania|Nie wymiarów|
|d2c.telemetry.egress.orphaned|Oddzielone wiadomości|Licznik|Łącznie|Aktualna liczba wiadomości nie zgodnych żadnych tras, łącznie z rezerwowego trasy|Nie wymiarów|
|d2c.telemetry.egress.invalid|Nieprawidłowy wiadomości|Licznik|Łącznie|Aktualna liczba wiadomości nie są dostarczane z powodu niezgodności z punktu końcowego|Nie wymiarów|
|d2c.telemetry.egress.Fallback|Wiadomości pasujące rezerwowy warunku|Licznik|Łącznie|Liczba komunikatów zapisanych do rezerwowego punktu końcowego|Nie wymiarów|
|d2c.endpoints.egress.eventHubs|Komunikaty dostarczone do Centrum zdarzeń punkty końcowe|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie zapisane punkty końcowe Centrum zdarzeń|Nie wymiarów|
|d2c.endpoints.latency.eventHubs|Opóźnienie komunikat dla punktów końcowych Centrum zdarzeń|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego Centrum zdarzeń, w milisekundach|Nie wymiarów|
|d2c.endpoints.egress.serviceBusQueues|Komunikaty dostarczone do punktów końcowych z kolejką usługi Service Bus|Licznik|Łącznie|Liczba wiadomości kolejką usługi Service Bus punkty końcowe zostały pomyślnie zapisane|Nie wymiarów|
|d2c.endpoints.latency.serviceBusQueues|Czas oczekiwania na wiadomość dla punktów końcowych z kolejką usługi Service Bus|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego kolejką usługi Service Bus, w milisekundach|Nie wymiarów|
|d2c.endpoints.egress.serviceBusTopics|Komunikaty dostarczone do punktów końcowych temat magistrali usług|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie zapisane punkty końcowe temat magistrali usług|Nie wymiarów|
|d2c.endpoints.latency.serviceBusTopics|Opóźnienie komunikat dla punktów końcowych temat magistrali usług|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego Service Bus tematu w milisekundach|Nie wymiarów|
|d2c.endpoints.egress.builtIn.events|Wiadomość dostarczona do wbudowanej punktu końcowego (wiadomości/zdarzeń)|Licznik|Łącznie|Liczba komunikatów wbudowanym punktem końcowym (wiadomości/zdarzeń) zostały pomyślnie zapisane|Nie wymiarów|
|d2c.endpoints.latency.builtIn.events|Czas oczekiwania wiadomości na wbudowanym punktem końcowym (wiadomości/zdarzeń)|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i transfer danych przychodzących wiadomości na wbudowanym punktem końcowym (wiadomości/zdarzeń), w milisekundach |Nie wymiarów|
|d2c.endpoints.egress.Storage|Komunikaty dostarczone do punktów końcowych magazynu|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie zapisane punkty końcowe usługi storage|Nie wymiarów|
|d2c.endpoints.latency.Storage|Opóźnienie komunikat dla punktów końcowych magazynu|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego magazynu (w milisekundach)|Nie wymiarów|
|d2c.endpoints.egress.Storage.Bytes|Dane zapisywane w pamięci masowej|Bajty|Łącznie|Ilość danych w bajtach, zapisane punkty końcowe usługi storage|Nie wymiarów|
|d2c.endpoints.egress.Storage.blobs|Zapisane do magazynu obiektów blob|Licznik|Łącznie|Liczba zapisywane do punktów końcowych magazynu obiektów blob|Nie wymiarów|
|d2c.Twin.Read.SUCCESS|Pomyślne dwie odczytuje z urządzeń|Licznik|Łącznie|Liczba wszystkich pomyślnych odczyty dwie inicjowanych przez urządzenie.|Nie wymiarów|
|d2c.Twin.Read.failure|Nie powiodło się dwie odczyty z urządzeń|Licznik|Łącznie|Liczba wszystkich nie odczyty dwie inicjowanych przez urządzenie.|Nie wymiarów|
|d2c.Twin.Read.size|Rozmiar odpowiedzi odczytów dwie z urządzeń|Bajty|Średnia|Średnia, min i max z wszystkie udane, inicjowanych przez urządzenie dwie odczytów.|Nie wymiarów|
|d2c.Twin.Update.SUCCESS|Pomyślne dwie aktualizacje z urządzeń|Licznik|Łącznie|Liczba wszystkich pomyślnych aktualizacji dwie inicjowanych przez urządzenie.|Nie wymiarów|
|d2c.Twin.Update.failure|Nie powiodło się dwie aktualizacje z urządzeń|Licznik|Łącznie|Liczba wszystkich nie aktualizacje dwie inicjowanych przez urządzenie.|Nie wymiarów|
|d2c.Twin.Update.size|Rozmiar aktualizacji dwie z urządzeń|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wszystkich pomyślnych, inicjowanych przez urządzenie dwie aktualizacji.|Nie wymiarów|
|c2d.Methods.SUCCESS|Pomyślne bezpośrednie wywołania metod|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań metody bezpośredniego.|Nie wymiarów|
|c2d.Methods.failure|Nie powiodło się bezpośrednie wywołania metod|Licznik|Łącznie|Liczba wszystkich nie wywołania metody bezpośredniego.|Nie wymiarów|
|c2d.Methods.requestSize|Rozmiar żądania bezpośrednie wywołania metod|Bajty|Średnia|Średnia, min i max wszystkich pomyślnych żądań metoda bezpośrednia.|Nie wymiarów|
|c2d.Methods.responseSize|Rozmiar odpowiedzi bezpośrednie wywołania metod|Bajty|Średnia|Średnia, minimum i maksimum wszystkie udane metoda bezpośrednia odpowiedzi.|Nie wymiarów|
|c2d.Twin.Read.SUCCESS|Pomyślne dwie odczytuje z zaplecza|Licznik|Łącznie|Liczba wszystkich pomyślnie zainicjował zakończenia wstecz dwie odczytuje.|Nie wymiarów|
|c2d.Twin.Read.failure|Nie powiodło się dwie odczytuje z zaplecza|Licznik|Łącznie|Liczba wszystkich nie odczyty wstecz zakończenia inicjowane przez dwie.|Nie wymiarów|
|c2d.Twin.Read.size|Rozmiar odpowiedzi odczytów dwie z wewnętrznego|Bajty|Średnia|Średnia, min i max z wszystkie udane, Wstecz zakończenia inicjowane przez dwie odczytów.|Nie wymiarów|
|c2d.Twin.Update.SUCCESS|Pomyślne dwie aktualizacje z wewnętrznego|Licznik|Łącznie|Liczba wszystkich pomyślnych aktualizacji inicjowane zakończenia wstecz dwie.|Nie wymiarów|
|c2d.Twin.Update.failure|Nie powiodło się dwie aktualizacje z wewnętrznego|Licznik|Łącznie|Liczba wszystkich nie powiodło się wstecz zakończenia inicjowane przez dwie aktualizacje.|Nie wymiarów|
|c2d.Twin.Update.size|Rozmiar aktualizacji dwie z wewnętrznego|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wszystkich pomyślnych, Wstecz zakończenia inicjowane przez dwie aktualizacji.|Nie wymiarów|
|twinQueries.success|Dwie pomyślne zapytania|Licznik|Łącznie|Liczba wszystkich zapytań dwie powiodło się.|Nie wymiarów|
|twinQueries.failure|Nie powiodło się dwie zapytań|Licznik|Łącznie|Liczba wszystkich zapytań dwie nie powiodło się.|Nie wymiarów|
|twinQueries.resultSize|Rozmiar wyników zapytania dwie|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wyników wszystkich zapytań dwie powiodło się.|Nie wymiarów|
|jobs.createTwinUpdateJob.success|Pomyślne utworzenie kont dwie aktualizacji zadań|Licznik|Łącznie|Liczba wszystkich pomyślnym utworzeniu zadania aktualizacji dwie.|Nie wymiarów|
|jobs.createTwinUpdateJob.failure|Nie powiodło się tworzenie dwie aktualizacji zadań|Licznik|Łącznie|Liczba wszystkich nie powiodło się tworzenie zadań aktualizacji dwie.|Nie wymiarów|
|jobs.createDirectMethodJob.success|Pomyślne tworzenia zadań wywołania — metoda|Licznik|Łącznie|Liczba wszystkich pomyślnym utworzeniu zadania wywołania metody bezpośredniego.|Nie wymiarów|
|jobs.createDirectMethodJob.failure|Nie powiodło się tworzenie zadań wywołania — metoda|Licznik|Łącznie|Liczba wszystkich nie powiodło się tworzenie zadań wywołania metody bezpośredniego.|Nie wymiarów|
|jobs.listJobs.success|Pomyślnych wywołań do listy zadań|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań do listy zadań.|Nie wymiarów|
|jobs.listJobs.failure|Nie powiodło się wywołania do listy zadań|Licznik|Łącznie|Liczba zakończonych niepowodzeniem wywołania do listy zadań.|Nie wymiarów|
|jobs.cancelJob.success|Anulowane zadania powiodło się|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań, aby anulować zadanie.|Nie wymiarów|
|jobs.cancelJob.failure|Anulowanie zadania nie powiodło się|Licznik|Łącznie|Liczba wszystkich wywołań nie powiodło się, aby anulować zadanie.|Nie wymiarów|
|jobs.queryJobs.success|Pomyślnie wykonane zadanie zapytań|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań do zadań zapytania.|Nie wymiarów|
|jobs.queryJobs.failure|Nie powiodło się zadanie odpytuje|Licznik|Łącznie|Liczba wszystkie wywołania zakończone niepowodzeniem zadania zapytania.|Nie wymiarów|
|Jobs.Completed|Ukończone zadania|Licznik|Łącznie|Liczba wszystkich zakończonych zadań.|Nie wymiarów|
|Jobs.failed|Zadania zakończone niepowodzeniem|Licznik|Łącznie|Liczba wszystkie zadania zakończone niepowodzeniem.|Nie wymiarów|
|d2c.telemetry.ingress.sendThrottle|Liczba błędów ograniczania przepustowości|Licznik|Łącznie|Ogranicza liczbę błędów ograniczania przepustowości z powodu przepływności urządzenia|Nie wymiarów|
|dailyMessageQuotaUsed|Całkowita liczba komunikatów używany|Licznik|Średnia|Liczba całkowita liczba komunikatów używany w tej chwili. Jest to wartość zbiorcza, która jest resetowany do zera w formacie UTC 00:00 każdego dnia.|Nie wymiarów|

## <a name="microsoftdevicesprovisioningservices"></a>Microsoft.Devices/provisioningServices

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|RegistrationAttempts|Prób rejestracji|Licznik|Łącznie|Liczba prób rejestracji urządzenia|Stan ProvisioningServiceName, IotHubName,|
|DeviceAssignments|Urządzenia przypisane|Licznik|Łącznie|Liczba urządzenia przypisane do Centrum IoT|ProvisioningServiceName, IotHubName|
|AttestationAttempts|Poświadczenie prób|Licznik|Łącznie|Liczba podjęto poświadczenia urządzenia|Protokół ProvisioningServiceName, stan,|

## <a name="microsoftdeviceselasticpools"></a>Microsoft.Devices/ElasticPools

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|elasticPool.requestedUsageRate|szybkość żądanego użycia|Procent|Średnia|szybkość żądanego użycia|Nie wymiarów|

## <a name="microsoftdeviceselasticpoolsiothubtenants"></a>Microsoft.Devices/ElasticPools/IotHubTenants

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|tenantHub.requestedUsageRate|szybkość żądanego użycia|Procent|Średnia|szybkość żądanego użycia|Nie wymiarów|
|deviceDataUsage|Całkowita liczba devicedata użycia|Licznik|Łącznie|Bajtów przesłanych do i z wszelkich urządzeń połączonych z Centrum IotHub|Nie wymiarów|
|d2c.telemetry.ingress.allProtocol|Próby wysłania wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów telemetrii urządzenia do chmury próby wysłania do Centrum IoT|Nie wymiarów|
|d2c.telemetry.ingress.SUCCESS|Wysłane wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów telemetrii urządzenia do chmury pomyślnie wysłane do Centrum IoT|Nie wymiarów|
|c2d.Commands.egress.COMPLETE.SUCCESS|Polecenia zakończona|Licznik|Łącznie|Liczba poleceń chmury do urządzenia, które zakończyło się powodzeniem, urządzenia|Nie wymiarów|
|c2d.Commands.egress.Abandon.SUCCESS|Porzucone poleceń|Licznik|Łącznie|Liczba poleceń chmury do urządzenia porzucone przez urządzenie|Nie wymiarów|
|c2d.Commands.egress.Reject.SUCCESS|Polecenia odrzucone|Licznik|Łącznie|Liczba odrzuconych przez urządzenie poleceń chmury do urządzenia|Nie wymiarów|
|devices.totalDevices|Łączna liczba urządzeń|Licznik|Łącznie|Liczba urządzeń zarejestrowanych do Centrum IoT|Nie wymiarów|
|devices.connectedDevices.allProtocol|Połączonych urządzeń|Licznik|Łącznie|Liczba urządzeń połączonych z Centrum IoT|Nie wymiarów|
|d2c.telemetry.egress.SUCCESS|Dostarczane wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów pomyślnie zostały zapisane do punktów końcowych (łącznie)|Nie wymiarów|
|d2c.telemetry.egress.dropped|Porzucone komunikaty|Licznik|Łącznie|Liczba wiadomości porzuconych z powodu braku punktu końcowego dostarczania|Nie wymiarów|
|d2c.telemetry.egress.orphaned|Oddzielone wiadomości|Licznik|Łącznie|Aktualna liczba wiadomości nie zgodnych żadnych tras, łącznie z rezerwowego trasy|Nie wymiarów|
|d2c.telemetry.egress.invalid|Nieprawidłowy wiadomości|Licznik|Łącznie|Aktualna liczba wiadomości nie są dostarczane z powodu niezgodności z punktu końcowego|Nie wymiarów|
|d2c.telemetry.egress.Fallback|Wiadomości pasujące rezerwowy warunku|Licznik|Łącznie|Liczba komunikatów zapisanych do rezerwowego punktu końcowego|Nie wymiarów|
|d2c.endpoints.egress.eventHubs|Komunikaty dostarczone do Centrum zdarzeń punkty końcowe|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie zapisane punkty końcowe Centrum zdarzeń|Nie wymiarów|
|d2c.endpoints.latency.eventHubs|Opóźnienie komunikat dla punktów końcowych Centrum zdarzeń|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego Centrum zdarzeń, w milisekundach|Nie wymiarów|
|d2c.endpoints.egress.serviceBusQueues|Komunikaty dostarczone do punktów końcowych z kolejką usługi Service Bus|Licznik|Łącznie|Liczba wiadomości kolejką usługi Service Bus punkty końcowe zostały pomyślnie zapisane|Nie wymiarów|
|d2c.endpoints.latency.serviceBusQueues|Czas oczekiwania na wiadomość dla punktów końcowych z kolejką usługi Service Bus|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego kolejką usługi Service Bus, w milisekundach|Nie wymiarów|
|d2c.endpoints.egress.serviceBusTopics|Komunikaty dostarczone do punktów końcowych temat magistrali usług|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie zapisane punkty końcowe temat magistrali usług|Nie wymiarów|
|d2c.endpoints.latency.serviceBusTopics|Opóźnienie komunikat dla punktów końcowych temat magistrali usług|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego Service Bus tematu w milisekundach|Nie wymiarów|
|d2c.endpoints.egress.builtIn.events|Wiadomość dostarczona do wbudowanej punktu końcowego (wiadomości/zdarzeń)|Licznik|Łącznie|Liczba komunikatów wbudowanym punktem końcowym (wiadomości/zdarzeń) zostały pomyślnie zapisane|Nie wymiarów|
|d2c.endpoints.latency.builtIn.events|Czas oczekiwania wiadomości na wbudowanym punktem końcowym (wiadomości/zdarzeń)|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i transfer danych przychodzących wiadomości na wbudowanym punktem końcowym (wiadomości/zdarzeń), w milisekundach |Nie wymiarów|
|d2c.endpoints.egress.Storage|Komunikaty dostarczone do punktów końcowych magazynu|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie zapisane punkty końcowe usługi storage|Nie wymiarów|
|d2c.endpoints.latency.Storage|Opóźnienie komunikat dla punktów końcowych magazynu|Milisekundy|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego magazynu (w milisekundach)|Nie wymiarów|
|d2c.endpoints.egress.Storage.Bytes|Dane zapisywane w pamięci masowej|Bajty|Łącznie|Ilość danych w bajtach, zapisane punkty końcowe usługi storage|Nie wymiarów|
|d2c.endpoints.egress.Storage.blobs|Zapisane do magazynu obiektów blob|Licznik|Łącznie|Liczba zapisywane do punktów końcowych magazynu obiektów blob|Nie wymiarów|
|d2c.Twin.Read.SUCCESS|Pomyślne dwie odczytuje z urządzeń|Licznik|Łącznie|Liczba wszystkich pomyślnych odczyty dwie inicjowanych przez urządzenie.|Nie wymiarów|
|d2c.Twin.Read.failure|Nie powiodło się dwie odczyty z urządzeń|Licznik|Łącznie|Liczba wszystkich nie odczyty dwie inicjowanych przez urządzenie.|Nie wymiarów|
|d2c.Twin.Read.size|Rozmiar odpowiedzi odczytów dwie z urządzeń|Bajty|Średnia|Średnia, min i max z wszystkie udane, inicjowanych przez urządzenie dwie odczytów.|Nie wymiarów|
|d2c.Twin.Update.SUCCESS|Pomyślne dwie aktualizacje z urządzeń|Licznik|Łącznie|Liczba wszystkich pomyślnych aktualizacji dwie inicjowanych przez urządzenie.|Nie wymiarów|
|d2c.Twin.Update.failure|Nie powiodło się dwie aktualizacje z urządzeń|Licznik|Łącznie|Liczba wszystkich nie aktualizacje dwie inicjowanych przez urządzenie.|Nie wymiarów|
|d2c.Twin.Update.size|Rozmiar aktualizacji dwie z urządzeń|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wszystkich pomyślnych, inicjowanych przez urządzenie dwie aktualizacji.|Nie wymiarów|
|c2d.Methods.SUCCESS|Pomyślne bezpośrednie wywołania metod|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań metody bezpośredniego.|Nie wymiarów|
|c2d.Methods.failure|Nie powiodło się bezpośrednie wywołania metod|Licznik|Łącznie|Liczba wszystkich nie wywołania metody bezpośredniego.|Nie wymiarów|
|c2d.Methods.requestSize|Rozmiar żądania bezpośrednie wywołania metod|Bajty|Średnia|Średnia, min i max wszystkich pomyślnych żądań metoda bezpośrednia.|Nie wymiarów|
|c2d.Methods.responseSize|Rozmiar odpowiedzi bezpośrednie wywołania metod|Bajty|Średnia|Średnia, minimum i maksimum wszystkie udane metoda bezpośrednia odpowiedzi.|Nie wymiarów|
|c2d.Twin.Read.SUCCESS|Pomyślne dwie odczytuje z zaplecza|Licznik|Łącznie|Liczba wszystkich pomyślnie zainicjował zakończenia wstecz dwie odczytuje.|Nie wymiarów|
|c2d.Twin.Read.failure|Nie powiodło się dwie odczytuje z zaplecza|Licznik|Łącznie|Liczba wszystkich nie odczyty wstecz zakończenia inicjowane przez dwie.|Nie wymiarów|
|c2d.Twin.Read.size|Rozmiar odpowiedzi odczytów dwie z wewnętrznego|Bajty|Średnia|Średnia, min i max z wszystkie udane, Wstecz zakończenia inicjowane przez dwie odczytów.|Nie wymiarów|
|c2d.Twin.Update.SUCCESS|Pomyślne dwie aktualizacje z wewnętrznego|Licznik|Łącznie|Liczba wszystkich pomyślnych aktualizacji inicjowane zakończenia wstecz dwie.|Nie wymiarów|
|c2d.Twin.Update.failure|Nie powiodło się dwie aktualizacje z wewnętrznego|Licznik|Łącznie|Liczba wszystkich nie powiodło się wstecz zakończenia inicjowane przez dwie aktualizacje.|Nie wymiarów|
|c2d.Twin.Update.size|Rozmiar aktualizacji dwie z wewnętrznego|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wszystkich pomyślnych, Wstecz zakończenia inicjowane przez dwie aktualizacji.|Nie wymiarów|
|twinQueries.success|Dwie pomyślne zapytania|Licznik|Łącznie|Liczba wszystkich zapytań dwie powiodło się.|Nie wymiarów|
|twinQueries.failure|Nie powiodło się dwie zapytań|Licznik|Łącznie|Liczba wszystkich zapytań dwie nie powiodło się.|Nie wymiarów|
|twinQueries.resultSize|Rozmiar wyników zapytania dwie|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wyników wszystkich zapytań dwie powiodło się.|Nie wymiarów|
|jobs.createTwinUpdateJob.success|Pomyślne utworzenie kont dwie aktualizacji zadań|Licznik|Łącznie|Liczba wszystkich pomyślnym utworzeniu zadania aktualizacji dwie.|Nie wymiarów|
|jobs.createTwinUpdateJob.failure|Nie powiodło się tworzenie dwie aktualizacji zadań|Licznik|Łącznie|Liczba wszystkich nie powiodło się tworzenie zadań aktualizacji dwie.|Nie wymiarów|
|jobs.createDirectMethodJob.success|Pomyślne tworzenia zadań wywołania — metoda|Licznik|Łącznie|Liczba wszystkich pomyślnym utworzeniu zadania wywołania metody bezpośredniego.|Nie wymiarów|
|jobs.createDirectMethodJob.failure|Nie powiodło się tworzenie zadań wywołania — metoda|Licznik|Łącznie|Liczba wszystkich nie powiodło się tworzenie zadań wywołania metody bezpośredniego.|Nie wymiarów|
|jobs.listJobs.success|Pomyślnych wywołań do listy zadań|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań do listy zadań.|Nie wymiarów|
|jobs.listJobs.failure|Nie powiodło się wywołania do listy zadań|Licznik|Łącznie|Liczba zakończonych niepowodzeniem wywołania do listy zadań.|Nie wymiarów|
|jobs.cancelJob.success|Anulowane zadania powiodło się|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań, aby anulować zadanie.|Nie wymiarów|
|jobs.cancelJob.failure|Anulowanie zadania nie powiodło się|Licznik|Łącznie|Liczba wszystkich wywołań nie powiodło się, aby anulować zadanie.|Nie wymiarów|
|jobs.queryJobs.success|Pomyślnie wykonane zadanie zapytań|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań do zadań zapytania.|Nie wymiarów|
|jobs.queryJobs.failure|Nie powiodło się zadanie odpytuje|Licznik|Łącznie|Liczba wszystkie wywołania zakończone niepowodzeniem zadania zapytania.|Nie wymiarów|
|Jobs.Completed|Ukończone zadania|Licznik|Łącznie|Liczba wszystkich zakończonych zadań.|Nie wymiarów|
|Jobs.failed|Zadania zakończone niepowodzeniem|Licznik|Łącznie|Liczba wszystkie zadania zakończone niepowodzeniem.|Nie wymiarów|
|d2c.telemetry.ingress.sendThrottle|Liczba błędów ograniczania przepustowości|Licznik|Łącznie|Ogranicza liczbę błędów ograniczania przepustowości z powodu przepływności urządzenia|Nie wymiarów|
|dailyMessageQuotaUsed|Całkowita liczba komunikatów używany|Licznik|Średnia|Liczba całkowita liczba komunikatów używany w tej chwili. Jest to wartość zbiorcza, która jest resetowany do zera w formacie UTC 00:00 każdego dnia.|Nie wymiarów|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.DocumentDB/databaseAccounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|MetadataRequests|Żądania metadanych|Licznik|Licznik|Liczba żądań metadanych. Rozwiązania cosmos DB przechowuje kolekcji metadanych systemu dla każdego konta, które pozwala wyliczyć kolekcje, baz danych, itp., i ich konfiguracji bezpłatnie.|GlobalDatabaseAccountName, DatabaseName, CollectionName, Region, StatusCode|
|MongoRequestCharge|MONGO żądania opłat|Licznik|Łącznie|Jednostki żądania MONGO używane|GlobalDatabaseAccountName, DatabaseName, CollectionName, Region, CommandName, kod błędu|
|MongoRequests|MONGO żądań|Licznik|Licznik|Liczba złożonych żądań Mongo|GlobalDatabaseAccountName, DatabaseName, CollectionName, Region, CommandName, kod błędu|
|TotalRequestUnits|Całkowita liczba żądań jednostki|Licznik|Łącznie|Używane jednostki żądania|GlobalDatabaseAccountName, DatabaseName, CollectionName, Region, StatusCode|
|TotalRequests|Łączna liczba żądań|Licznik|Licznik|Liczba żądań|GlobalDatabaseAccountName, DatabaseName, CollectionName, Region, StatusCode|


## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|SuccessfulRequests|Liczba pomyślnych żądań (wersja zapoznawcza)|Licznik|Łącznie|Żądania zakończone powodzeniem dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|ServerErrors|Błędy serwera. (Wersja zapoznawcza)|Licznik|Łącznie|Błędy serwera dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|UserErrors|Błędy użytkowników. (Wersja zapoznawcza)|Licznik|Łącznie|Błędy użytkowników dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|QuotaExceededErrors|Błędy przekroczenia przydziału. (Wersja zapoznawcza)|Licznik|Łącznie|Błędy przekroczenia przydziału dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|ThrottledRequests|Żądania ograniczone. (Wersja zapoznawcza)|Licznik|Łącznie|Żądania ograniczone dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|IncomingRequests|Przychodzące żądania (wersja zapoznawcza)|Licznik|Łącznie|Żądania przychodzące dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|IncomingMessages|Komunikaty przychodzące (wersja zapoznawcza)|Licznik|Łącznie|Komunikaty przychodzące dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|OutgoingMessages|Wysyła komunikaty wychodzące (wersja zapoznawcza)|Licznik|Łącznie|Komunikaty wychodzące dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|IncomingBytes|Bajty przychodzące. (Wersja zapoznawcza)|Bajty|Łącznie|Bajty przychodzące dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|OutgoingBytes|Bajty wychodzące. (Wersja zapoznawcza)|Bajty|Łącznie|Bajty wychodzące dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|ActiveConnections|ActiveConnections (wersja zapoznawcza)|Licznik|Łącznie|Całkowita liczba aktywnych połączeń dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|ConnectionsOpened|Połączenia otwarte. (Wersja zapoznawcza)|Licznik|Łącznie|Połączenia otwarte dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|ConnectionsClosed|Połączenia zamknięte. (Wersja zapoznawcza)|Licznik|Łącznie|Połączenia zamknięte dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|CaptureBacklog|Lista prac przechwytywania. (Wersja zapoznawcza)|Licznik|Łącznie|Lista prac przechwytywania dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|CapturedMessages|Przechwycone komunikaty. (Wersja zapoznawcza)|Licznik|Łącznie|Przechwycone komunikaty dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|CapturedBytes|Przechwycone bajty. (Wersja zapoznawcza)|Bajty|Łącznie|Przechwycone bajty dla elementu Microsoft.EventHub. (Wersja zapoznawcza)|Nazwa jednostki|
|INREQS|Żądania przychodzące|Licznik|Łącznie|Łączna liczba żądań wysłania dla przestrzeni nazw|Nie wymiarów|
|SUCCREQ|Żądania zakończone powodzeniem|Licznik|Łącznie|Łączna liczba udanych żądań dla przestrzeni nazw|Nie wymiarów|
|FAILREQ|Żądania zakończone niepowodzeniem|Licznik|Łącznie|Łączna liczba nieudanych żądań dla przestrzeni nazw|Nie wymiarów|
|SVRBSY|Błędy typu Serwer zajęty|Licznik|Łącznie|Łączna liczba błędów zajętego serwera dla przestrzeni nazw|Nie wymiarów|
|INTERR|Wewnętrzne błędy serwera|Licznik|Łącznie|Łączna liczba wewnętrznych błędów serwera dla przestrzeni nazw|Nie wymiarów|
|MISCERR|Inne błędy|Licznik|Łącznie|Łączna liczba nieudanych żądań dla przestrzeni nazw|Nie wymiarów|
|INMSGS|Komunikaty przychodzące (przestarzałe)|Licznik|Łącznie|Całkowita liczba komunikatów przychodzących w przypadku przestrzeni nazw. Ta metryka jest przestarzały. Zamiast tego użyj Metryka wiadomości przychodzących|Nie wymiarów|
|EHINMSGS|Wiadomości przychodzące|Licznik|Łącznie|Łączna liczba komunikatów przychodzących dla przestrzeni nazw|Nie wymiarów|
|OUTMSGS|Komunikaty wychodzące (przestarzałe)|Licznik|Łącznie|Całkowita liczba wychodzących wiadomości w przypadku przestrzeni nazw. Ta metryka jest przestarzały. Zamiast tego użyj Metryka wysyła komunikaty wychodzące|Nie wymiarów|
|EHOUTMSGS|Wiadomości wychodzące|Licznik|Łącznie|Łączna liczba komunikatów wychodzących dla przestrzeni nazw|Nie wymiarów|
|EHINMBS|Bajty przychodzące (przestarzałe)|Bajty|Łącznie|Zdarzenia koncentratora przychodzącego komunikatu przepływność dla przestrzeni nazw. Ta metryka jest przestarzały. Zamiast tego użyj Metryka Bajty przychodzące|Nie wymiarów|
|EHINBYTES|Bajty przychodzące|Bajty|Łącznie|Przepływność komunikatów przychodzących centrum zdarzeń usługi Event Hubs w przestrzeni nazw|Nie wymiarów|
|EHOUTMBS|Bajty wychodzące (przestarzałe)|Bajty|Łącznie|Zdarzenia koncentratora wychodzących wiadomości przepływność dla przestrzeni nazw. Ta metryka jest przestarzały. Zamiast tego użyj Wychodzące bajty metryki|Nie wymiarów|
|EHOUTBYTES|Bajty wychodzące|Bajty|Łącznie|Przepływność komunikatów wychodzących centrum zdarzeń usługi Event Hubs w przestrzeni nazw|Nie wymiarów|
|EHABL|Archiwizuj komunikaty listy prac|Licznik|Łącznie|Zarchiwizowane komunikaty centrum zdarzeń usługi Event Hubs na liście prac dla przestrzeni nazw|Nie wymiarów|
|EHAMSGS|Archiwizowanie komunikatów|Licznik|Łącznie|Zarchiwizowane komunikaty centrum zdarzeń usługi Event Hubs w przestrzeni nazw|Nie wymiarów|
|EHAMBS|Przepływność archiwizowania komunikatów|Bajty|Łącznie|Przepływność zarchiwizowanych komunikatów centrum zdarzeń usługi Event Hubs w przestrzeni nazw|Nie wymiarów|

## <a name="microsoftinsightsautoscalesettings"></a>Microsoft.Insights/AutoscaleSettings

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|ObservedMetricValue|Zaobserwowana wartość metryki|Licznik|Średnia|Wartość obliczona przez automatyczne skalowanie podczas wykonywania|MetricTriggerSource|
|MetricThreshold|Próg metryki|Licznik|Średnia|Skonfigurowany próg automatycznego skalowania podczas uruchamiania automatycznego skalowania.|MetricTriggerRule|
|ObservedCapacity|Zaobserwowana wydajność|Licznik|Średnia|Wydajność zgłoszona do automatycznego skalowania podczas jego wykonywania.|Nie wymiarów|
|ScaleActionsInitiated|Zainicjowane akcje skalowania|Licznik|Łącznie|Kierunek operacji skalowania.|ScaleDirection|

## <a name="microsoftlocationbasedservicesaccounts"></a>Microsoft.LocationBasedServices/accounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Opóźnienie|Opóźnienie|Milisekundy|Średnia|Czas trwania wywołań interfejsu API|OperationName, klasy OperationResult|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|RunsStarted|Przebiegi rozpoczęte|Licznik|Łącznie|Liczba rozpoczętych przebiegów przepływu pracy.|Nie wymiarów|
|RunsCompleted|Przebiegi ukończone|Licznik|Łącznie|Liczba ukończonych przebiegów przepływu pracy.|Nie wymiarów|
|RunsSucceeded|Przebiegi zakończone powodzeniem|Licznik|Łącznie|Liczba przebiegów przepływu pracy zakończonych powodzeniem.|Nie wymiarów|
|RunsFailed|Przebiegi zakończone niepowodzeniem|Licznik|Łącznie|Liczba przebiegów przepływu pracy zakończonych niepowodzeniem.|Nie wymiarów|
|RunsCancelled|Przebiegi anulowane|Licznik|Łącznie|Liczba anulowanych przebiegów przepływu pracy.|Nie wymiarów|
|RunLatency|Opóźnienie przebiegów|Sekundy|Średnia|Opóźnienie ukończonych przebiegów przepływu pracy.|Nie wymiarów|
|RunSuccessLatency|Opóźnienie przebiegów zakończonych powodzeniem|Sekundy|Średnia|Opóźnienie przebiegów przepływu pracy zakończonych powodzeniem.|Nie wymiarów|
|RunThrottledEvents|Zdarzenia ograniczenia przebiegu|Licznik|Łącznie|Liczba zdarzeń ograniczenia akcji lub wyzwalacza przepływu pracy.|Nie wymiarów|
|RunFailurePercentage|Procent niepowodzeń przebiegów|Procent|Łącznie|Procent przebiegów przepływu pracy zakończonych niepowodzeniem.|Nie wymiarów|
|ActionsStarted|Rozpoczęte akcje |Licznik|Łącznie|Liczba rozpoczętych akcji przepływu pracy.|Nie wymiarów|
|ActionsCompleted|Ukończone akcje |Licznik|Łącznie|Liczba ukończonych akcji przepływu pracy.|Nie wymiarów|
|ActionsSucceeded|Akcje zakończone powodzeniem |Licznik|Łącznie|Liczba akcji przepływu pracy zakończonych powodzeniem.|Nie wymiarów|
|ActionsFailed|Akcje zakończone niepowodzeniem|Licznik|Łącznie|Liczba akcji przepływu pracy zakończonych niepowodzeniem.|Nie wymiarów|
|ActionsSkipped|Pominięte akcje |Licznik|Łącznie|Liczba pominiętych akcji przepływu pracy.|Nie wymiarów|
|ActionLatency|Opóźnienie akcji |Sekundy|Średnia|Opóźnienie ukończonych akcji przepływu pracy.|Nie wymiarów|
|ActionSuccessLatency|Opóźnienie akcji – powodzenie |Sekundy|Średnia|Opóźnienie akcji przepływu pracy zakończonych powodzeniem.|Nie wymiarów|
|ActionThrottledEvents|Zdarzenia ograniczenia akcji|Licznik|Łącznie|Liczba zdarzeń ograniczenia akcji przepływu pracy.|Nie wymiarów|
|TriggersStarted|Rozpoczęte wyzwalacze |Licznik|Łącznie|Liczba rozpoczętych wyzwalaczy przepływu pracy.|Nie wymiarów|
|TriggersCompleted|Ukończone wyzwalacze |Licznik|Łącznie|Liczba ukończonych wyzwalaczy przepływu pracy.|Nie wymiarów|
|TriggersSucceeded|Udane wyzwalacze |Licznik|Łącznie|Liczba wyzwalaczy przepływu pracy zakończonych powodzeniem.|Nie wymiarów|
|TriggersFailed|Nieudane wyzwalacze |Licznik|Łącznie|Liczba wyzwalaczy przepływu pracy zakończonych niepowodzeniem.|Nie wymiarów|
|TriggersSkipped|Pominięte wyzwalacze|Licznik|Łącznie|Liczba pominiętych wyzwalaczy przepływu pracy.|Nie wymiarów|
|TriggersFired|Uruchomione wyzwalacze |Licznik|Łącznie|Liczba uaktywnionych wyzwalaczy przepływu pracy.|Nie wymiarów|
|TriggerLatency|Opóźnienie wyzwalacza |Sekundy|Średnia|Opóźnienie ukończonych wyzwalaczy przepływu pracy.|Nie wymiarów|
|TriggerFireLatency|Opóźnienie uruchomienia wyzwalacza |Sekundy|Średnia|Opóźnienie uaktywnionych wyzwalaczy przepływu pracy.|Nie wymiarów|
|TriggerSuccessLatency|Opóźnienie udanego wyzwalacza |Sekundy|Średnia|Opóźnienie wyzwalaczy przepływu pracy zakończonych powodzeniem.|Nie wymiarów|
|TriggerThrottledEvents|Zdarzenia ograniczenia wyzwalacza|Licznik|Łącznie|Liczba zdarzeń ograniczenia wyzwalacza przepływu pracy.|Nie wymiarów|
|BillableActionExecutions|Rozliczane wykonania akcji|Licznik|Łącznie|Liczba rozliczanych wykonań akcji przepływu pracy.|Nie wymiarów|
|BillableTriggerExecutions|Rozliczane wykonania wyzwalaczy|Licznik|Łącznie|Liczba rozliczanych wykonań wyzwalaczy przepływu pracy.|Nie wymiarów|
|TotalBillableExecutions|Łączna liczba rozliczanych wykonań|Licznik|Łącznie|Liczba rozliczanych wykonań przepływu pracy.|Nie wymiarów|

## <a name="microsoftnetworknetworkinterfaces"></a>Microsoft.Network/networkInterfaces

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|BytesSentRate|Wysłane bajty|Licznik|Łącznie|Liczba bajtów wysłanych interfejsu sieciowego|Nie wymiarów|
|BytesReceivedRate|Odebrane bajty|Licznik|Łącznie|Liczba bajtów odebranych interfejsu sieciowego|Nie wymiarów|
|PacketsSentRate|Wysłanych pakietów|Licznik|Łącznie|Liczba pakietów wysłanych interfejsu sieciowego|Nie wymiarów|
|PacketsReceivedRate|Odebrane pakiety|Licznik|Łącznie|Liczba pakietów odebranych interfejsu sieciowego|Nie wymiarów|

## <a name="microsoftnetworkloadbalancers"></a>Microsoft.Network/loadBalancers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|VipAvailability|Dostępność adresu VIP|Licznik|Średnia|Dostępność punktów końcowych VIP, na podstawie wyników badania|Wirtualny adres IP, VipPort|
|DipAvailability|Dostępność DIP|Licznik|Średnia|Dostępność punktów końcowych DIP, na podstawie wyników badania|ProtocolType, DipPort, wirtualny adres IP, VipPort, DipAddress|
|ByteCount|Liczba bajtów|Licznik|Łącznie|Całkowita liczba bajtów przesłanych w określonym przedziale czasu|Wirtualny adres IP, VipPort, kierunku|
|PacketCount|Liczba pakietów|Licznik|Łącznie|Całkowita liczba pakietów wysłanych w ciągu okresu czasu|Wirtualny adres IP, VipPort, kierunku|
|SYNCount|Liczba SYN|Licznik|Łącznie|Całkowita liczba pakietów SYN transmitowane w określonym przedziale czasu|Wirtualny adres IP, VipPort, kierunku|
|SnatConnectionCount|Liczba połączeń SNAT|Licznik|Łącznie|Całkowita liczba nowych połączeń SNAT utworzona w okresie czasu|Element ConnectionState wirtualny adres IP, DipAddress,|

## <a name="microsoftnetworkpublicipaddresses"></a>Microsoft.Network/publicIPAddresses

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|PacketsInDDoS|Liczba przychodzących pakietów DDoS|CountPerSecond|Maksimum|Liczba przychodzących pakietów DDoS|Nie wymiarów|
|PacketsDroppedDDoS|Liczba porzuconych pakietów przychodzących DDoS|CountPerSecond|Maksimum|Liczba porzuconych pakietów przychodzących DDoS|Nie wymiarów|
|PacketsForwardedDDoS|Pakiety przychodzące przekazywane przed atakami DDoS|CountPerSecond|Maksimum|Pakiety przychodzące przekazywane przed atakami DDoS|Nie wymiarów|
|TCPPacketsInDDoS|Liczba przychodzących pakietów TCP przed atakami DDoS|CountPerSecond|Maksimum|Liczba przychodzących pakietów TCP przed atakami DDoS|Nie wymiarów|
|TCPPacketsDroppedDDoS|Pakiety przychodzące TCP porzucony przed atakami DDoS|CountPerSecond|Maksimum|Pakiety przychodzące TCP porzucony przed atakami DDoS|Nie wymiarów|
|TCPPacketsForwardedDDoS|Pakiety przychodzące TCP przekazywane przed atakami DDoS|CountPerSecond|Maksimum|Pakiety przychodzące TCP przekazywane przed atakami DDoS|Nie wymiarów|
|UDPPacketsInDDoS|Liczba przychodzących pakietów UDP DDoS|CountPerSecond|Maksimum|Liczba przychodzących pakietów UDP DDoS|Nie wymiarów|
|UDPPacketsDroppedDDoS|Przychodzących pakietów UDP porzucony przed atakami DDoS|CountPerSecond|Maksimum|Przychodzących pakietów UDP porzucony przed atakami DDoS|Nie wymiarów|
|UDPPacketsForwardedDDoS|Przekazywane DDoS przychodzących pakietów UDP|CountPerSecond|Maksimum|Przekazywane DDoS przychodzących pakietów UDP|Nie wymiarów|
|BytesInDDoS|Przychodzące bajty przed atakami DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty przed atakami DDoS|Nie wymiarów|
|BytesDroppedDDoS|Przychodzące bajty porzucony przed atakami DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty porzucony przed atakami DDoS|Nie wymiarów|
|BytesForwardedDDoS|Przychodzące bajty przekazywane przed atakami DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty przekazywane przed atakami DDoS|Nie wymiarów|
|TCPBytesInDDoS|Przychodzące bajty TCP przed atakami DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty TCP przed atakami DDoS|Nie wymiarów|
|TCPBytesDroppedDDoS|Przychodzące bajty TCP porzucony przed atakami DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty TCP porzucony przed atakami DDoS|Nie wymiarów|
|TCPBytesForwardedDDoS|Przychodzące bajty TCP przekazywane przed atakami DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty TCP przekazywane przed atakami DDoS|Nie wymiarów|
|UDPBytesInDDoS|Przychodzące bajty UDP DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty UDP DDoS|Nie wymiarów|
|UDPBytesDroppedDDoS|Przychodzące bajty UDP porzucony przed atakami DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty UDP porzucony przed atakami DDoS|Nie wymiarów|
|UDPBytesForwardedDDoS|Przychodzące bajty UDP przekazywane przed atakami DDoS|Bajty na sekundę|Maksimum|Przychodzące bajty UDP przekazywane przed atakami DDoS|Nie wymiarów|
|IfUnderDDoSAttack|W obszarze DDoS ataku lub nie|Licznik|Maksimum|W obszarze DDoS ataku lub nie|Nie wymiarów|
|DDoSTriggerTCPPackets|Liczba przychodzących pakietów TCP do wyzwolenia ograniczenie DDoS|CountPerSecond|Maksimum|Liczba przychodzących pakietów TCP do wyzwolenia ograniczenie DDoS|Nie wymiarów|
|DDoSTriggerUDPPackets|Liczba przychodzących pakietów UDP do wyzwolenia ograniczenie DDoS|CountPerSecond|Maksimum|Liczba przychodzących pakietów UDP do wyzwolenia ograniczenie DDoS|Nie wymiarów|
|DDoSTriggerSYNPackets|Liczba przychodzących pakietów SYN do wyzwolenia ograniczenie DDoS|CountPerSecond|Maksimum|Liczba przychodzących pakietów SYN do wyzwolenia ograniczenie DDoS|Nie wymiarów|
|VipAvailability|Dostępność|Licznik|Średnia|Średnia dostępność adres IP w przedziale czasu|Port|
|ByteCount|Liczba bajtów|Licznik|Łącznie|Całkowita liczba bajtów przesłanych w określonym przedziale czasu|Portu i kierunek|
|PacketCount|Liczba pakietów|Licznik|Łącznie|Całkowita liczba pakietów wysłanych w ciągu okresu czasu|Portu i kierunek|
|SynCount|Liczba SYN|Licznik|Łącznie|Całkowita liczba pakietów SYN transmitowane w określonym przedziale czasu|Portu i kierunek|

## <a name="microsoftnetworkvirtualnetworks"></a>Microsoft.Network/virtualNetworks

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|PacketsInDroppedVMProtection|Liczba porzuconych pakietów przychodzących do ochrony maszyny Wirtualnej|CountPerSecond|Średnia|Liczba porzuconych pakietów przychodzących do ochrony maszyny Wirtualnej|Nie wymiarów|
|PacketsOutDroppedVMProtection|Liczba porzuconych pakietów wychodzących do ochrony maszyny Wirtualnej|CountPerSecond|Średnia|Liczba porzuconych pakietów wychodzących do ochrony maszyny Wirtualnej|Nie wymiarów|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Przepływność|Przepływność|Bajty na sekundę|Łącznie|Liczba bajtów na sekundę, ma obsłużone bramy aplikacji|Nie wymiarów|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.Network/virtualNetworkGateways

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|TunnelAverageBandwidth|Tunel przepustowości|Bajty na sekundę|Średnia|Średnia przepustowość tunelu w bajtach na sekundę|ConnectionName, RemoteIP|
|TunnelEgressBytes|Tunel wyjście bajtów|Bajty|Łącznie|Wychodzące bajty tunelu|ConnectionName, RemoteIP|
|TunnelIngressBytes|Tunel bajtów wejściowych|Bajty|Łącznie|Przychodzące bajty tunelu|ConnectionName, RemoteIP|
|TunnelEgressPackets|Tunel wyjście pakietów|Licznik|Łącznie|Wychodzące liczba pakietów tunelu|ConnectionName, RemoteIP|
|TunnelIngressPackets|Tunel pakietów wejściowych|Licznik|Łącznie|Liczba pakietów przychodząca tunelu|ConnectionName, RemoteIP|
|TunnelEgressPacketDropTSMismatch|Porzucanie pakietów niezgodność wyjście TS tunelu|Licznik|Łącznie|Wychodzące liczby porzucenia pakietów z niezgodność selektor ruchu tunelu|ConnectionName, RemoteIP|
|TunnelIngressPacketDropTSMismatch|Porzucanie pakietów niezgodność ruch przychodzący serwera terminali tunelu|Licznik|Łącznie|Liczba przychodząca listy pakietów z niezgodność selektor ruchu tunelu|ConnectionName, RemoteIP|

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|BitsInPerSecond|BitsInPerSecond|CountPerSecond|Średnia|Usługa BITS ingressing Azure na sekundę|Nie wymiarów|
|BitsOutPerSecond|BitsOutPerSecond|CountPerSecond|Średnia|Usługa BITS egressing Azure na sekundę|Nie wymiarów|

## <a name="microsoftnetworktrafficmanagerprofiles"></a>Microsoft.Network/trafficManagerProfiles

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|QpsByEndpoint|Zapytania przez punkt końcowy zwrócił|Licznik|Łącznie|Ile razy punkt końcowy Menedżera ruchu został zwrócony w określonym przedziale czasu|EndpointName|
|ProbeAgentCurrentEndpointStateByProfileResourceId|Stan punktu końcowego przez punkt końcowy|Licznik|Maksimum|1, jeśli punkt końcowy sondowania stanu jest "włączone", w przeciwnym razie 0.|EndpointName|

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Registration.all|Operacje rejestracji|Licznik|Łącznie|Liczba wszystkich operacji rejestracji zakończonych powodzeniem (operacje tworzenia, aktualizacje, zapytania i operacje usuwania). |Nie wymiarów|
|Registration.Create|Operacje tworzenia rejestracji|Licznik|Łącznie|Liczba wszystkich operacji tworzenia rejestracji zakończonych powodzeniem.|Nie wymiarów|
|Registration.Update|Operacje aktualizacji operacji|Licznik|Łącznie|Liczba wszystkich aktualizacji rejestracji zakończonych powodzeniem.|Nie wymiarów|
|Registration.Get|Operacje odczytu operacji|Licznik|Łącznie|Liczba wszystkich zapytań dotyczących rejestracji zakończonych powodzeniem.|Nie wymiarów|
|Registration.delete|Operacje usuwania rejestracji|Licznik|Łącznie|Liczba wszystkich operacji usuwania rejestracji zakończonych powodzeniem.|Nie wymiarów|
|przychodzące|Wiadomości przychodzące|Licznik|Łącznie|Liczba wszystkich operacji wysyłania wywołania interfejsu API zakończonych powodzeniem. |Nie wymiarów|
|Incoming.scheduled|Wysłano zaplanowane powiadomienia wypychane|Licznik|Łącznie|Anulowano zaplanowane powiadomienia wypychane|Nie wymiarów|
|Incoming.scheduled.Cancel|Anulowano zaplanowane powiadomienia wypychane|Licznik|Łącznie|Anulowano zaplanowane powiadomienia wypychane|Nie wymiarów|
|scheduled.Pending|Oczekujące zaplanowane powiadomienia|Licznik|Łącznie|Oczekujące zaplanowane powiadomienia|Nie wymiarów|
|Installation.all|Operacje zarządzania instalacją|Licznik|Łącznie|Operacje zarządzania instalacją|Nie wymiarów|
|Installation.Get|Pobierz operacje instalacji|Licznik|Łącznie|Pobierz operacje instalacji|Nie wymiarów|
|Installation.UPSERT|Utwórz lub zaktualizuj operacje instalacji|Licznik|Łącznie|Utwórz lub zaktualizuj operacje instalacji|Nie wymiarów|
|Installation.Patch|Operacje instalacji poprawki|Licznik|Łącznie|Operacje instalacji poprawki|Nie wymiarów|
|Installation.delete|Usuń operacje instalacji|Licznik|Łącznie|Usuń operacje instalacji|Nie wymiarów|
|Outgoing.allpns.SUCCESS|Powiadomienia zakończone powodzeniem|Licznik|Łącznie|Liczba wszystkich powiadomień zakończonych powodzeniem.|Nie wymiarów|
|Outgoing.allpns.invalidpayload|Błędy ładunku|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy zwrócił błąd oznaczający nieprawidłowy ładunek.|Nie wymiarów|
|Outgoing.allpns.pnserror|Błędy zewnętrznych systemów powiadamiania|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ wystąpił problem podczas komunikowania się z systemem powiadomień platformy (nie obejmuje problemów z uwierzytelnianiem).|Nie wymiarów|
|Outgoing.allpns.channelerror|Błędy kanału|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ kanał był nieprawidłowy i nie został skojarzony z poprawną aplikacją (ograniczoną lub wygasłą).|Nie wymiarów|
|Outgoing.allpns.badorexpiredchannel|Błędy nieprawidłowych lub wygasłych kanałów|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ kanał/token/identyfikator rejestracji w rejestracji wygasł lub był nieprawidłowy.|Nie wymiarów|
|Outgoing.wns.SUCCESS|Powiadomienia usługi WNS zakończone powodzeniem|Licznik|Łącznie|Liczba wszystkich powiadomień zakończonych powodzeniem.|Nie wymiarów|
|Outgoing.wns.invalidcredentials|Błędy autoryzacji usługi WNS (nieprawidłowe poświadczenia)|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptował podanych poświadczeń lub poświadczenia zostały zablokowane. (Windows Live nie rozpoznaje poświadczeń).|Nie wymiarów|
|Outgoing.wns.badchannel|Błąd nieprawidłowego kanału usługi WNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ identyfikator ChannelURI w rejestracji nie został rozpoznany (stan usługi WNS: 404 Nie znaleziono).|Nie wymiarów|
|Outgoing.wns.expiredchannel|Błąd wygasłego kanału usługi WNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ identyfikator ChannelURI wygasł (stan usługi WNS: 410 Przeniesiono).|Nie wymiarów|
|Outgoing.wns.throttled|Powiadomienia usługi WNS z ograniczoną przepływnością|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ usługa WNS ogranicza tę aplikację (stan usługi WNS: 406 Niedozwolone).|Nie wymiarów|
|Outgoing.wns.tokenproviderunreachable|Błędy autoryzacji usługi WNS (niedostępna)|Licznik|Łącznie|Nie można połączyć się z usługą Windows Live.|Nie wymiarów|
|Outgoing.wns.invalidtoken|Błędy autoryzacji usługi WNS (nieprawidłowy token)|Licznik|Łącznie|Token przekazany do usługi WNS jest nieprawidłowy (stan usługi: 401 Brak autoryzacji).|Nie wymiarów|
|Outgoing.wns.wrongtoken|Błędy autoryzacji usługi WNS (niepoprawny token)|Licznik|Łącznie|Dostarczony do WNS token jest prawidłowy, ale dla innej aplikacji (stan usługi WNS: 403 Zabroniony). Może to nastąpić, jeśli ChannelURI w rejestracji jest skojarzony z innej aplikacji. Sprawdź, czy aplikacja kliencka jest skojarzony z tą samą aplikacją, którego poświadczenia znajdują się w Centrum powiadomień.|Nie wymiarów|
|Outgoing.wns.invalidnotificationformat|Nieprawidłowy format powiadomienia usługi WNS|Licznik|Łącznie|Format powiadomienia jest nieprawidłowy (stan usługi WNS: 400). Należy pamiętać, że usługi WNS nie odrzucić wszystkie ładunki nieprawidłowy.|Nie wymiarów|
|Outgoing.wns.invalidnotificationsize|Błąd nieprawidłowego rozmiaru powiadomienia usługi WNS|Licznik|Łącznie|Ładunek powiadomienia jest zbyt duży (stan usługi WNS: 413).|Nie wymiarów|
|Outgoing.wns.channelthrottled|Ograniczono przepływność kanału usługi WNS|Licznik|Łącznie|Powiadomienie zostało porzucone, ponieważ identyfikator ChannelURI w rejestracji jest ograniczany (nagłówek odpowiedzi usługi WNS: X-WNS-NotificationStatus: channelThrottled).|Nie wymiarów|
|Outgoing.wns.channeldisconnected|Rozłączono kanał usługi WNS|Licznik|Łącznie|Powiadomienie zostało porzucone, ponieważ identyfikator ChannelURI w rejestracji jest ograniczany (nagłówek odpowiedzi usługi WNS: X-WNS-DeviceConnectionStatus: rozłączono).|Nie wymiarów|
|Outgoing.wns.dropped|Porzucone powiadomienia usługi WNS|Licznik|Łącznie|Powiadomienie zostało porzucone, ponieważ identyfikator ChannelURI w rejestracji jest ograniczany (X-WNS-NotificationStatus: porzucono, ale nie X-WNS-DeviceConnectionStatus: rozłączono).|Nie wymiarów|
|Outgoing.wns.pnserror|Błędy usługi WNS|Licznik|Łącznie|Nie dostarczono powiadomienia z powodu błędów podczas komunikowania się z usługą WNS.|Nie wymiarów|
|Outgoing.wns.authenticationerror|Błędy uwierzytelniania usługi WNS|Licznik|Łącznie|Nie dostarczono powiadomienia z powodu błędów podczas komunikowania się z błędnym tokenem lub nieprawidłowymi poświadczeniami usługi Windows Live.|Nie wymiarów|
|Outgoing.apns.SUCCESS|Powiadomienia usługi APNS zakończone powodzeniem|Licznik|Łącznie|Liczba wszystkich powiadomień zakończonych powodzeniem.|Nie wymiarów|
|Outgoing.apns.invalidcredentials|Błędy autoryzacji usługi APNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptował podanych poświadczeń lub poświadczenia zostały zablokowane.|Nie wymiarów|
|Outgoing.apns.badchannel|Błąd nieprawidłowego kanału usługi APNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ token jest nieprawidłowy (kod stanu usługi APNS: 8).|Nie wymiarów|
|Outgoing.apns.expiredchannel|Błąd nieprawidłowego kanału usługi APNS|Licznik|Łącznie|Liczba tokenów unieważnionych przy użyciu kanału sprzężenia zwrotnego usługi APNS.|Nie wymiarów|
|Outgoing.apns.invalidnotificationsize|Błąd nieprawidłowego rozmiaru powiadomienia usługi APNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ ładunek powiadomienia był zbyt duży (kod stanu usługi APNS: 7).|Nie wymiarów|
|Outgoing.apns.pnserror|Błędy usługi APNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem z powodu błędów podczas komunikowania się z usługą APNS.|Nie wymiarów|
|Outgoing.gcm.SUCCESS|Powiadomienia usługi GCM zakończone powodzeniem|Licznik|Łącznie|Liczba wszystkich powiadomień zakończonych powodzeniem.|Nie wymiarów|
|Outgoing.gcm.invalidcredentials|Błędy autoryzacji usługi GCM (nieprawidłowe poświadczenia)|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptował podanych poświadczeń lub poświadczenia zostały zablokowane.|Nie wymiarów|
|Outgoing.gcm.badchannel|Błąd nieprawidłowego kanału usługi GCM|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ identyfikator rejestracji wygasł (wynik usługi GSM: nieprawidłowa rejestracja).|Nie wymiarów|
|Outgoing.gcm.expiredchannel|Błąd wygasłego kanału usługi GCM|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ identyfikator rejestracji wygasł (wynik usługi GSM: NotRegistered).|Nie wymiarów|
|Outgoing.gcm.throttled|Powiadomienia usługi GCM z ograniczoną przepływnością|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ usługa GCM ograniczyła tę aplikację (kod stanu usługi GCM: 501–599 lub wynik: Niedostępne).|Nie wymiarów|
|Outgoing.gcm.invalidnotificationformat|Nieprawidłowy format powiadomienia usługi GCM|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ ładunek został nieprawidłowo sformatowany (stan usługi GCM: InvalidDataKey lub InvalidTtl).|Nie wymiarów|
|Outgoing.gcm.invalidnotificationsize|Błąd nieprawidłowego rozmiaru powiadomienia usługi GCM|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ ładunek powiadomienia był zbyt duży (wynik usługi GCM: MessageTooBig).|Nie wymiarów|
|Outgoing.gcm.wrongchannel|Błąd nieprawidłowego kanału usługi GCM|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ identyfikator rejestracji nie został skojarzony z bieżącą aplikacją (wynik usługi GSM: InvalidpackageName).|Nie wymiarów|
|Outgoing.gcm.pnserror|Błędy usługi GCM|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem z powodu błędów podczas komunikowania się z usługą GCM.|Nie wymiarów|
|Outgoing.gcm.authenticationerror|Błędy uwierzytelniania usługi GCM|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptował podanych poświadczeń, poświadczenia zostały zablokowane lub element SenderId został nieprawidłowo skonfigurowany w aplikacji (wynik usługi GSM: MismatchedSenderId).|Nie wymiarów|
|Outgoing.mpns.SUCCESS|Powiadomienia usługi MPNS zakończone powodzeniem|Licznik|Łącznie|Liczba wszystkich powiadomień zakończonych powodzeniem.|Nie wymiarów|
|Outgoing.mpns.invalidcredentials|Nieprawidłowe poświadczenia usługi MPNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptował podanych poświadczeń lub poświadczenia zostały zablokowane.|Nie wymiarów|
|Outgoing.mpns.badchannel|Błąd nieprawidłowego kanału usługi MPNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ identyfikator ChannelURI w rejestracji nie został rozpoznany (stan usługi MPNS: 404 Nie znaleziono).|Nie wymiarów|
|Outgoing.mpns.throttled|Powiadomienia usługi MPNS z ograniczoną przepływnością|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ usługa MPNS ogranicza tę aplikację (WNS MPNS: 406 Niedozwolone).|Nie wymiarów|
|Outgoing.mpns.invalidnotificationformat|Nieprawidłowy format powiadomienia usługi MPNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ ładunek powiadomienia był zbyt duży.|Nie wymiarów|
|Outgoing.mpns.channeldisconnected|Rozłączono kanał usługi MPNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ identyfikator ChannelURI w rejestracji został rozłączony (stan usługi MPNS: 412 Nie znaleziono).|Nie wymiarów|
|Outgoing.mpns.dropped|Porzucone powiadomienia usługi MPNS|Licznik|Łącznie|Liczba wypchnięć porzuconych przez usługę MPNS (nagłówek odpowiedzi MPNS: X-NotificationStatus: QueueFull lub Suppressed).|Nie wymiarów|
|Outgoing.mpns.pnserror|Błędy usługi MPNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem z powodu błędów podczas komunikowania się z usługą MPNS.|Nie wymiarów|
|Outgoing.mpns.authenticationerror|Błędy uwierzytelniania usługi MPNS|Licznik|Łącznie|Liczba wypchnięć, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptował podanych poświadczeń lub poświadczenia zostały zablokowane.|Nie wymiarów|
|notificationhub.pushes|Wszystkie powiadomienia wychodzące|Licznik|Łącznie|Wszystkie powiadomienia wychodzące w centrum powiadomień|Nie wymiarów|
|Incoming.all.Requests|Wszystkie żądania przychodzące|Licznik|Łącznie|Łączna liczba żądań przychodzących dla centrum powiadomień|Nie wymiarów|
|Incoming.all.failedrequests|Wszystkie nieudane żądania przychodzące|Licznik|Łącznie|Łączna liczba nieudanych żądań przychodzących dla centrum powiadomień|Nie wymiarów|

## <a name="microsoftrelaynamespaces"></a>Microsoft.Relay/namespaces

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|ListenerConnections-Success|ListenerConnections-Success|Licznik|Łącznie|Pomyślne połączenia ListenerConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|ListenerConnections-ClientError|ListenerConnections-ClientError|Licznik|Łącznie|Błąd ClientError w połączeniach ListenerConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|ListenerConnections-ServerError|ListenerConnections-ServerError|Licznik|Łącznie|Błąd ServerError w połączeniach ListenerConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|SenderConnections-Success|SenderConnections-Success|Licznik|Łącznie|Pomyślne połączenia SenderConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|SenderConnections-ClientError|SenderConnections-ClientError|Licznik|Łącznie|Błąd ClientError w połączeniach SenderConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|SenderConnections-ServerError|SenderConnections-ServerError|Licznik|Łącznie|Błąd ServerError w elemencie SenderConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|ListenerConnections-TotalRequests|ListenerConnections-TotalRequests|Licznik|Łącznie|Łączna liczba połączeń ListenerConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|SenderConnections-TotalRequests|SenderConnections-TotalRequests|Licznik|Łącznie|Łączna liczba żądań SenderConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|ActiveConnections|ActiveConnections|Licznik|Łącznie|Łączna liczba połączeń ActiveConnections dla elementu Microsoft.Relay.|Nazwa jednostki|
|ActiveListeners|ActiveListeners|Licznik|Łącznie|Łączna liczba odbiorników ActiveListeners dla elementu Microsoft.Relay.|Nazwa jednostki|
|BytesTransferred|BytesTransferred|Licznik|Łącznie|Łączna liczba bajtów BytesTransferred dla elementu Microsoft.Relay.|Nazwa jednostki|
|ListenerDisconnects|ListenerDisconnects|Licznik|Łącznie|Łączna liczba rozłączeń ListenerDisconnects dla elementu Microsoft.Relay.|Nazwa jednostki|
|SenderDisconnects|SenderDisconnects|Licznik|Łącznie|Łączna liczba rozłączeń SenderDisconnects dla elementu Microsoft.Relay.|Nazwa jednostki|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|SearchLatency|Czas oczekiwania wyszukiwania|Sekundy|Średnia|Opóźnienie średni wyszukiwania dla usługi wyszukiwania|Nie wymiarów|
|SearchQueriesPerSecond|Zapytania wyszukiwania na sekundę|CountPerSecond|Średnia|Zapytania wyszukiwania na sekundę dla usługi wyszukiwania|Nie wymiarów|
|ThrottledSearchQueriesPercentage|Procent zapytań wyszukiwania z ograniczoną przepustowością|Procent|Średnia|Procent zapytania wyszukiwania, które zostały ograniczany usługi wyszukiwania|Nie wymiarów|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|SuccessfulRequests|Liczba pomyślnych żądań (wersja zapoznawcza)|Licznik|Łącznie|Całkowita liczba pomyślnych żądań dla przestrzeni nazw (wersja zapoznawcza)|Nazwa jednostki|
|ServerErrors|Błędy serwera. (Wersja zapoznawcza)|Licznik|Łącznie|Błędy serwera dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|UserErrors|Błędy użytkowników. (Wersja zapoznawcza)|Licznik|Łącznie|Błędy użytkowników dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|ThrottledRequests|Żądania ograniczone. (Wersja zapoznawcza)|Licznik|Łącznie|Żądania ograniczone dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|IncomingRequests|Przychodzące żądania (wersja zapoznawcza)|Licznik|Łącznie|Żądania przychodzące dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|IncomingMessages|Komunikaty przychodzące (wersja zapoznawcza)|Licznik|Łącznie|Komunikaty przychodzące dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|OutgoingMessages|Wysyła komunikaty wychodzące (wersja zapoznawcza)|Licznik|Łącznie|Komunikaty wychodzące dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|ActiveConnections|ActiveConnections (wersja zapoznawcza)|Licznik|Łącznie|Całkowita liczba aktywnych połączeń dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|ConnectionsOpened|Połączenia otwarte. (Wersja zapoznawcza)|Licznik|Łącznie|Połączenia otwarte dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|ConnectionsClosed|Połączenia zamknięte. (Wersja zapoznawcza)|Licznik|Łącznie|Połączenia zamknięte dla elementu Microsoft.ServiceBus. (Wersja zapoznawcza)|Nazwa jednostki|
|CPUXNS|Użycie procesora na przestrzeń nazw|Procent|Maksimum|Metryka użycia procesora przestrzeni nazw w usłudze Service Bus w warstwie Premium|Nie wymiarów|
|WSXNS|Użycie rozmiaru pamięci na przestrzeń nazw|Procent|Maksimum|Metryka użycia pamięci przestrzeni nazw w usłudze Service Bus w warstwie Premium|Nie wymiarów|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|cpu_percent|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|Nie wymiarów|
|physical_data_read_percent|Procent użycia operacji we/wy na danych|Procent|Średnia|Procent użycia operacji we/wy na danych|Nie wymiarów|
|log_write_percent|Procent we/wy dziennika|Procent|Średnia|Procent we/wy dziennika|Nie wymiarów|
|dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|Nie wymiarów|
|magazyn|Rozmiar całkowitą bazy danych|Bajty|Maksimum|Rozmiar całkowitą bazy danych|Nie wymiarów|
|connection_successful|Udane połączenia|Licznik|Łącznie|Udane połączenia|Nie wymiarów|
|connection_failed|Połączenia nie powiodło się|Licznik|Łącznie|Połączenia nie powiodło się|Nie wymiarów|
|blocked_by_firewall|Blokowane przez zaporę|Licznik|Łącznie|Blokowane przez zaporę|Nie wymiarów|
|Zakleszczenie|Zakleszczenie|Licznik|Łącznie|Zakleszczenie|Nie wymiarów|
|storage_percent|Procent użycia rozmiaru bazy danych|Procent|Maksimum|Procent użycia rozmiaru bazy danych|Nie wymiarów|
|xtp_storage_percent|Procent magazynu OLTP w pamięci|Procent|Średnia|Procent magazynu OLTP w pamięci|Nie wymiarów|
|workers_percent|Procent pracowników|Procent|Średnia|Procent pracowników|Nie wymiarów|
|sessions_percent|Procent sesji|Procent|Średnia|Procent sesji|Nie wymiarów|
|dtu_limit|Limit jednostek dtu w warstwie|Licznik|Średnia|Limit jednostek dtu w warstwie|Nie wymiarów|
|dtu_used|Jednostek dtu w warstwie używane|Licznik|Średnia|Jednostek dtu w warstwie używane|Nie wymiarów|
|dwu_limit|Jednostka DWU limit|Licznik|Maksimum|Jednostka DWU limit|Nie wymiarów|
|dwu_consumption_percent|Procent jednostka DWU|Procent|Maksimum|Procent jednostka DWU|Nie wymiarów|
|dwu_used|Jednostka DWU używane|Licznik|Maksimum|Jednostka DWU używane|Nie wymiarów|
|dw_cpu_percent|Poziom węzła DW procent użycia procesora CPU|Procent|Średnia|Poziom węzła DW procent użycia procesora CPU|dw_logical_node_id|
|dw_physical_data_read_percent|Procent dane we/wy poziomu węzła magazynu danych|Procent|Średnia|Procent dane we/wy poziomu węzła magazynu danych|dw_logical_node_id|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|cpu_percent|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|Nie wymiarów|
|database_cpu_percent|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|DatabaseResourceId|
|physical_data_read_percent|Procent użycia operacji we/wy na danych|Procent|Średnia|Procent użycia operacji we/wy na danych|Nie wymiarów|
|database_physical_data_read_percent|Procent użycia operacji we/wy na danych|Procent|Średnia|Procent użycia operacji we/wy na danych|DatabaseResourceId|
|log_write_percent|Procent we/wy dziennika|Procent|Średnia|Procent we/wy dziennika|Nie wymiarów|
|database_log_write_percent|Procent we/wy dziennika|Procent|Średnia|Procent we/wy dziennika|DatabaseResourceId|
|dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|Nie wymiarów|
|database_dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|DatabaseResourceId|
|storage_percent|Procent użycia magazynu|Procent|Średnia|Procent użycia magazynu|Nie wymiarów|
|workers_percent|Procent pracowników|Procent|Średnia|Procent pracowników|Nie wymiarów|
|database_workers_percent|Procent pracowników|Procent|Średnia|Procent pracowników|DatabaseResourceId|
|sessions_percent|Procent sesji|Procent|Średnia|Procent sesji|Nie wymiarów|
|database_sessions_percent|Procent sesji|Procent|Średnia|Procent sesji|DatabaseResourceId|
|eDTU_limit|limit liczby jednostek eDTU|Licznik|Średnia|limit liczby jednostek eDTU|Nie wymiarów|
|storage_limit|Limit magazynu|Bajty|Średnia|Limit magazynu|Nie wymiarów|
|eDTU_used|eDTU używane|Licznik|Średnia|eDTU używane|Nie wymiarów|
|storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|Nie wymiarów|
|database_storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|DatabaseResourceId|
|xtp_storage_percent|Procent magazynu OLTP w pamięci|Procent|Średnia|Procent magazynu OLTP w pamięci|Nie wymiarów|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|ElasticPoolResourceId|
|database_dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|DatabaseResourceId, ElasticPoolResourceId|
|storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|ElasticPoolResourceId|
|database_storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|DatabaseResourceId, ElasticPoolResourceId|

## <a name="microsoftstoragestorageaccounts"></a>Microsoft.Storage/storageAccounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|UsedCapacity|Używana pojemność|Bajty|Średnia|Używana pojemność konta|Nie wymiarów|
|Transakcje|Transakcje|Licznik|Łącznie|Liczba żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API. Liczba ta obejmuje udane i nieudane żądania, a także żądań, które wyprodukowane błędy. Wymiar wartość ResponseType używany dla wielu różnych typ odpowiedzi.|Wartość ResponseType, GeoType, Nazwa_funkcji_api|
|Zdarzenia związane z transferem danych przychodzących|Zdarzenia związane z transferem danych przychodzących|Bajty|Łącznie|Ilość danych wejściowych, w bajtach. Liczba ta obejmuje transfer danych przychodzących z zewnętrznego klienta do usługi Azure Storage, a także ruch przychodzący w obrębie platformy Azure.|GeoType, Nazwa_funkcji_api|
|Ruch wychodzący|Ruch wychodzący|Bajty|Łącznie|Ilość danych wyjściowych, w bajtach. Liczba ta obejmuje wyjście z zewnętrznego klienta do usługi Azure Storage, a także Wyjście w obrębie platformy Azure. W związku z tym ta liczba nie odzwierciedla wyjście rozliczeniowy.|GeoType, Nazwa_funkcji_api|
|SuccessServerLatency|Opóźnienie serwera dla opóźnienia|Milisekundy|Średnia|Średni czas oczekiwania, używane przez usługi Azure Storage do przetwarzania żądanie zakończy się powodzeniem (w milisekundach). Ta wartość nie obejmuje opóźnienia sieci, określona w AverageE2ELatency.|GeoType, Nazwa_funkcji_api|
|SuccessE2ELatency|Opóźnienie E2E dla powodzenia|Milisekundy|Średnia|Średnie opóźnienie end-to-end pomyślnych żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API (w milisekundach). Ta wartość obejmuje wymagany czas przetwarzania w ramach usługi Azure Storage do odczytu żądania, wysyłania odpowiedzi i otrzyma odpowiedź.|GeoType, Nazwa_funkcji_api|
|Dostępność|Dostępność|Procent|Średnia|Procent dostępności usługi magazynu lub określonej operacji interfejsu API. Dostępność jest obliczana przez pobranie wartość TotalBillableRequests i podzielenie go przez liczbę odpowiednie żądania, w tym te, które tworzone nieoczekiwane błędy. Wszystkie powodować nieoczekiwane błędy zmniejszona dostępność usługi magazynu lub określonej operacji interfejsu API.|GeoType, Nazwa_funkcji_api|

## <a name="microsoftstoragestorageaccountsblobservices"></a>Microsoft.Storage/storageAccounts/blobServices

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|BlobCapacity|Pojemność obiektu blob|Bajty|Średnia|Ilość miejsca w magazynie (w bajtach) używana przez usługę obiektów blob konta magazynu.|BlobType|
|Liczba obiektów blob|Liczba obiektów blob|Licznik|Średnia|Liczba obiektów blob w usłudze obiektów blob konta magazynu.|BlobType|
|ContainerCount|Liczba kontenerów obiektów blob|Licznik|Średnia|Liczba kontenerów w usłudze obiektów blob konta magazynu.|Nie wymiarów|
|Transakcje|Transakcje|Licznik|Łącznie|Liczba żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API. Liczba ta obejmuje udane i nieudane żądania, a także żądań, które wyprodukowane błędy. Wymiar wartość ResponseType używany dla wielu różnych typ odpowiedzi.|Wartość ResponseType, GeoType, Nazwa_funkcji_api|
|Zdarzenia związane z transferem danych przychodzących|Zdarzenia związane z transferem danych przychodzących|Bajty|Łącznie|Ilość danych wejściowych, w bajtach. Liczba ta obejmuje transfer danych przychodzących z zewnętrznego klienta do usługi Azure Storage, a także ruch przychodzący w obrębie platformy Azure.|GeoType, Nazwa_funkcji_api|
|Ruch wychodzący|Ruch wychodzący|Bajty|Łącznie|Ilość danych wyjściowych, w bajtach. Liczba ta obejmuje wyjście z zewnętrznego klienta do usługi Azure Storage, a także Wyjście w obrębie platformy Azure. W związku z tym ta liczba nie odzwierciedla wyjście rozliczeniowy.|GeoType, Nazwa_funkcji_api|
|SuccessServerLatency|Opóźnienie serwera dla opóźnienia|Milisekundy|Średnia|Średni czas oczekiwania, używane przez usługi Azure Storage do przetwarzania żądanie zakończy się powodzeniem (w milisekundach). Ta wartość nie obejmuje opóźnienia sieci, określona w AverageE2ELatency.|GeoType, Nazwa_funkcji_api|
|SuccessE2ELatency|Opóźnienie E2E dla powodzenia|Milisekundy|Średnia|Średnie opóźnienie end-to-end pomyślnych żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API (w milisekundach). Ta wartość obejmuje wymagany czas przetwarzania w ramach usługi Azure Storage do odczytu żądania, wysyłania odpowiedzi i otrzyma odpowiedź.|GeoType, Nazwa_funkcji_api|
|Dostępność|Dostępność|Procent|Średnia|Procent dostępności usługi magazynu lub określonej operacji interfejsu API. Dostępność jest obliczana przez pobranie wartość TotalBillableRequests i podzielenie go przez liczbę odpowiednie żądania, w tym te, które tworzone nieoczekiwane błędy. Wszystkie powodować nieoczekiwane błędy zmniejszona dostępność usługi magazynu lub określonej operacji interfejsu API.|GeoType, Nazwa_funkcji_api|

## <a name="microsoftstoragestorageaccountstableservices"></a>Microsoft.Storage/storageAccounts/tableServices

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|TableCapacity|Pojemność tabeli|Bajty|Średnia|Ilość miejsca w magazynie (w bajtach) używanego przez usługę tabeli konta magazynu.|Nie wymiarów|
|TableCount|Liczba tabel|Licznik|Średnia|Liczba tabel w usłudze tabeli konta magazynu.|Nie wymiarów|
|TableEntityCount|Liczba jednostek tabel|Licznik|Średnia|Liczba jednostek tabel w usłudze tabeli konta magazynu.|Nie wymiarów|
|Transakcje|Transakcje|Licznik|Łącznie|Liczba żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API. Liczba ta obejmuje udane i nieudane żądania, a także żądań, które wyprodukowane błędy. Wymiar wartość ResponseType używany dla wielu różnych typ odpowiedzi.|Wartość ResponseType, GeoType, Nazwa_funkcji_api|
|Zdarzenia związane z transferem danych przychodzących|Zdarzenia związane z transferem danych przychodzących|Bajty|Łącznie|Ilość danych wejściowych, w bajtach. Liczba ta obejmuje transfer danych przychodzących z zewnętrznego klienta do usługi Azure Storage, a także ruch przychodzący w obrębie platformy Azure.|GeoType, Nazwa_funkcji_api|
|Ruch wychodzący|Ruch wychodzący|Bajty|Łącznie|Ilość danych wyjściowych, w bajtach. Liczba ta obejmuje wyjście z zewnętrznego klienta do usługi Azure Storage, a także Wyjście w obrębie platformy Azure. W związku z tym ta liczba nie odzwierciedla wyjście rozliczeniowy.|GeoType, Nazwa_funkcji_api|
|SuccessServerLatency|Opóźnienie serwera dla opóźnienia|Milisekundy|Średnia|Średni czas oczekiwania, używane przez usługi Azure Storage do przetwarzania żądanie zakończy się powodzeniem (w milisekundach). Ta wartość nie obejmuje opóźnienia sieci, określona w AverageE2ELatency.|GeoType, Nazwa_funkcji_api|
|SuccessE2ELatency|Opóźnienie E2E dla powodzenia|Milisekundy|Średnia|Średnie opóźnienie end-to-end pomyślnych żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API (w milisekundach). Ta wartość obejmuje wymagany czas przetwarzania w ramach usługi Azure Storage do odczytu żądania, wysyłania odpowiedzi i otrzyma odpowiedź.|GeoType, Nazwa_funkcji_api|
|Dostępność|Dostępność|Procent|Średnia|Procent dostępności usługi magazynu lub określonej operacji interfejsu API. Dostępność jest obliczana przez pobranie wartość TotalBillableRequests i podzielenie go przez liczbę odpowiednie żądania, w tym te, które tworzone nieoczekiwane błędy. Wszystkie powodować nieoczekiwane błędy zmniejszona dostępność usługi magazynu lub określonej operacji interfejsu API.|GeoType, Nazwa_funkcji_api|

## <a name="microsoftstoragestorageaccountsqueueservices"></a>Microsoft.Storage/storageAccounts/queueServices

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|QueueCapacity|Pojemność kolejki|Bajty|Średnia|Ilość miejsca w magazynie (w bajtach) używanego przez usługę kolejki konta magazynu.|Nie wymiarów|
|QueueCount|Liczba kolejek|Licznik|Średnia|Liczba kolejek w usłudze kolejki konta magazynu.|Nie wymiarów|
|QueueMessageCount|Liczba komunikatów w kolejce|Licznik|Średnia|Przybliżona liczba komunikatów w kolejce w usłudze kolejki konta magazynu.|Nie wymiarów|
|Transakcje|Transakcje|Licznik|Łącznie|Liczba żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API. Liczba ta obejmuje udane i nieudane żądania, a także żądań, które wyprodukowane błędy. Wymiar wartość ResponseType używany dla wielu różnych typ odpowiedzi.|Wartość ResponseType, GeoType, Nazwa_funkcji_api|
|Zdarzenia związane z transferem danych przychodzących|Zdarzenia związane z transferem danych przychodzących|Bajty|Łącznie|Ilość danych wejściowych, w bajtach. Liczba ta obejmuje transfer danych przychodzących z zewnętrznego klienta do usługi Azure Storage, a także ruch przychodzący w obrębie platformy Azure.|GeoType, Nazwa_funkcji_api|
|Ruch wychodzący|Ruch wychodzący|Bajty|Łącznie|Ilość danych wyjściowych, w bajtach. Liczba ta obejmuje wyjście z zewnętrznego klienta do usługi Azure Storage, a także Wyjście w obrębie platformy Azure. W związku z tym ta liczba nie odzwierciedla wyjście rozliczeniowy.|GeoType, Nazwa_funkcji_api|
|SuccessServerLatency|Opóźnienie serwera dla opóźnienia|Milisekundy|Średnia|Średni czas oczekiwania, używane przez usługi Azure Storage do przetwarzania żądanie zakończy się powodzeniem (w milisekundach). Ta wartość nie obejmuje opóźnienia sieci, określona w AverageE2ELatency.|GeoType, Nazwa_funkcji_api|
|SuccessE2ELatency|Opóźnienie E2E dla powodzenia|Milisekundy|Średnia|Średnie opóźnienie end-to-end pomyślnych żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API (w milisekundach). Ta wartość obejmuje wymagany czas przetwarzania w ramach usługi Azure Storage do odczytu żądania, wysyłania odpowiedzi i otrzyma odpowiedź.|GeoType, Nazwa_funkcji_api|
|Dostępność|Dostępność|Procent|Średnia|Procent dostępności usługi magazynu lub określonej operacji interfejsu API. Dostępność jest obliczana przez pobranie wartość TotalBillableRequests i podzielenie go przez liczbę odpowiednie żądania, w tym te, które tworzone nieoczekiwane błędy. Wszystkie powodować nieoczekiwane błędy zmniejszona dostępność usługi magazynu lub określonej operacji interfejsu API.|GeoType, Nazwa_funkcji_api|

## <a name="microsoftstoragestorageaccountsfileservices"></a>Microsoft.Storage/storageAccounts/fileServices

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|FileCapacity|Pojemność plików|Bajty|Średnia|Ilość miejsca w magazynie (w bajtach) używanego przez usługę plików konta magazynu.|Nie wymiarów|
|FileCount|Liczba plików|Licznik|Średnia|Liczba plików w usłudze plików konta magazynu.|Nie wymiarów|
|FileShareCount|Liczba udziałów plików|Licznik|Średnia|Liczba udziałów plików w usłudze plików konta magazynu.|Nie wymiarów|
|Transakcje|Transakcje|Licznik|Łącznie|Liczba żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API. Liczba ta obejmuje udane i nieudane żądania, a także żądań, które wyprodukowane błędy. Wymiar wartość ResponseType używany dla wielu różnych typ odpowiedzi.|Wartość ResponseType, GeoType, Nazwa_funkcji_api|
|Zdarzenia związane z transferem danych przychodzących|Zdarzenia związane z transferem danych przychodzących|Bajty|Łącznie|Ilość danych wejściowych, w bajtach. Liczba ta obejmuje transfer danych przychodzących z zewnętrznego klienta do usługi Azure Storage, a także ruch przychodzący w obrębie platformy Azure.|GeoType, Nazwa_funkcji_api|
|Ruch wychodzący|Ruch wychodzący|Bajty|Łącznie|Ilość danych wyjściowych, w bajtach. Liczba ta obejmuje wyjście z zewnętrznego klienta do usługi Azure Storage, a także Wyjście w obrębie platformy Azure. W związku z tym ta liczba nie odzwierciedla wyjście rozliczeniowy.|GeoType, Nazwa_funkcji_api|
|SuccessServerLatency|Opóźnienie serwera dla opóźnienia|Milisekundy|Średnia|Średni czas oczekiwania, używane przez usługi Azure Storage do przetwarzania żądanie zakończy się powodzeniem (w milisekundach). Ta wartość nie obejmuje opóźnienia sieci, określona w AverageE2ELatency.|GeoType, Nazwa_funkcji_api|
|SuccessE2ELatency|Opóźnienie E2E dla powodzenia|Milisekundy|Średnia|Średnie opóźnienie end-to-end pomyślnych żądań wysyłanych do usługi magazynu lub określonej operacji interfejsu API (w milisekundach). Ta wartość obejmuje wymagany czas przetwarzania w ramach usługi Azure Storage do odczytu żądania, wysyłania odpowiedzi i otrzyma odpowiedź.|GeoType, Nazwa_funkcji_api|
|Dostępność|Dostępność|Procent|Średnia|Procent dostępności usługi magazynu lub określonej operacji interfejsu API. Dostępność jest obliczana przez pobranie wartość TotalBillableRequests i podzielenie go przez liczbę odpowiednie żądania, w tym te, które tworzone nieoczekiwane błędy. Wszystkie powodować nieoczekiwane błędy zmniejszona dostępność usługi magazynu lub określonej operacji interfejsu API.|GeoType, Nazwa_funkcji_api|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|ResourceUtilization|% wykorzystania SU|Procent|Maksimum|% wykorzystania SU|Nie wymiarów|
|InputEvents|Zdarzenia wejściowe|Licznik|Łącznie|Zdarzenia wejściowe|Nie wymiarów|
|InputEventBytes|Zdarzenia wejściowe (bajty)|Bajty|Łącznie|Zdarzenia wejściowe (bajty)|Nie wymiarów|
|LateInputEvents|Opóźnione zdarzenia wejściowe|Licznik|Łącznie|Opóźnione zdarzenia wejściowe|Nie wymiarów|
|OutputEvents|Zdarzenia wyjściowe|Licznik|Łącznie|Zdarzenia wyjściowe|Nie wymiarów|
|ConversionErrors|Błędy konwersji danych|Licznik|Łącznie|Błędy konwersji danych|Nie wymiarów|
|Błędy|Błędy w czasie wykonywania|Licznik|Łącznie|Błędy w czasie wykonywania|Nie wymiarów|
|DroppedOrAdjustedEvents|Zdarzenia poza kolejnością|Licznik|Łącznie|Zdarzenia poza kolejnością|Nie wymiarów|
|AMLCalloutRequests|Żądania funkcji|Licznik|Łącznie|Żądania funkcji|Nie wymiarów|
|AMLCalloutFailedRequests|Żądania funkcji zakończone niepowodzeniem|Licznik|Łącznie|Żądania funkcji zakończone niepowodzeniem|Nie wymiarów|
|AMLCalloutInputEvents|Zdarzenia funkcji|Licznik|Łącznie|Zdarzenia funkcji|Nie wymiarów|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|CpuPercentage|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|Wystąpienie|
|MemoryPercentage|Procent pamięci|Procent|Średnia|Procent pamięci|Wystąpienie|
|DiskQueueLength|Długość kolejki dysku|Licznik|Średnia|Długość kolejki dysku|Wystąpienie|
|HttpQueueLength|Długość kolejki HTTP|Licznik|Średnia|Długość kolejki HTTP|Wystąpienie|
|BytesReceived|Dane wejściowe|Bajty|Łącznie|Dane wejściowe|Wystąpienie|
|Żądania|Dane wyjściowe|Bajty|Łącznie|Dane wyjściowe|Wystąpienie|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (z wyjątkiem funkcji)

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|CpuTime|Czas procesora CPU|Sekundy|Łącznie|Czas procesora CPU|Wystąpienie|
|Żądania|Żądania|Licznik|Łącznie|Żądania|Wystąpienie|
|BytesReceived|Dane wejściowe|Bajty|Łącznie|Dane wejściowe|Wystąpienie|
|Żądania|Dane wyjściowe|Bajty|Łącznie|Dane wyjściowe|Wystąpienie|
|Http101|HTTP 101|Licznik|Łącznie|HTTP 101|Wystąpienie|
|Http2xx|HTTP 2xx|Licznik|Łącznie|HTTP 2xx|Wystąpienie|
|Http3xx|HTTP 3xx|Licznik|Łącznie|HTTP 3xx|Wystąpienie|
|Http401|HTTP 401|Licznik|Łącznie|HTTP 401|Wystąpienie|
|Http403|HTTP 403|Licznik|Łącznie|HTTP 403|Wystąpienie|
|Http404|HTTP 404|Licznik|Łącznie|HTTP 404|Wystąpienie|
|Http406|HTTP 406|Licznik|Łącznie|HTTP 406|Wystąpienie|
|Http4xx|HTTP 4xx|Licznik|Łącznie|HTTP 4xx|Wystąpienie|
|Http5xx|Błędy serwera HTTP|Licznik|Łącznie|Błędy serwera HTTP|Wystąpienie|
|MemoryWorkingSet|Zestaw roboczy pamięci|Bajty|Średnia|Zestaw roboczy pamięci|Wystąpienie|
|AverageMemoryWorkingSet|Średni zestaw roboczy pamięci|Bajty|Średnia|Średni zestaw roboczy pamięci|Wystąpienie|
|AverageResponseTime|Średni czas odpowiedzi|Sekundy|Średnia|Średni czas odpowiedzi|Wystąpienie|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (funkcje)

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|BytesReceived|Dane wejściowe|Bajty|Łącznie|Dane wejściowe|Wystąpienie|
|Żądania|Dane wyjściowe|Bajty|Łącznie|Dane wyjściowe|Wystąpienie|
|Http5xx|Błędy serwera HTTP|Licznik|Łącznie|Błędy serwera HTTP|Wystąpienie|
|MemoryWorkingSet|Zestaw roboczy pamięci|Bajty|Średnia|Zestaw roboczy pamięci|Wystąpienie|
|AverageMemoryWorkingSet|Średni zestaw roboczy pamięci|Bajty|Średnia|Średni zestaw roboczy pamięci|Wystąpienie|
|FunctionExecutionUnits|Jednostki wykonawcze funkcji|Licznik|Łącznie|Jednostki wykonawcze funkcji|Wystąpienie|
|FunctionExecutionCount|Liczba wykonań funkcji|Licznik|Łącznie|Liczba wykonań funkcji|Wystąpienie|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|CpuTime|Czas procesora CPU|Sekundy|Łącznie|Czas procesora CPU|Wystąpienie|
|Żądania|Żądania|Licznik|Łącznie|Żądania|Wystąpienie|
|BytesReceived|Dane wejściowe|Bajty|Łącznie|Dane wejściowe|Wystąpienie|
|Żądania|Dane wyjściowe|Bajty|Łącznie|Dane wyjściowe|Wystąpienie|
|Http101|HTTP 101|Licznik|Łącznie|HTTP 101|Wystąpienie|
|Http2xx|HTTP 2xx|Licznik|Łącznie|HTTP 2xx|Wystąpienie|
|Http3xx|HTTP 3xx|Licznik|Łącznie|HTTP 3xx|Wystąpienie|
|Http401|HTTP 401|Licznik|Łącznie|HTTP 401|Wystąpienie|
|Http403|HTTP 403|Licznik|Łącznie|HTTP 403|Wystąpienie|
|Http404|HTTP 404|Licznik|Łącznie|HTTP 404|Wystąpienie|
|Http406|HTTP 406|Licznik|Łącznie|HTTP 406|Wystąpienie|
|Http4xx|HTTP 4xx|Licznik|Łącznie|HTTP 4xx|Wystąpienie|
|Http5xx|Błędy serwera HTTP|Licznik|Łącznie|Błędy serwera HTTP|Wystąpienie|
|MemoryWorkingSet|Zestaw roboczy pamięci|Bajty|Średnia|Zestaw roboczy pamięci|Wystąpienie|
|AverageMemoryWorkingSet|Średni zestaw roboczy pamięci|Bajty|Średnia|Średni zestaw roboczy pamięci|Wystąpienie|
|AverageResponseTime|Średni czas odpowiedzi|Sekundy|Średnia|Średni czas odpowiedzi|Wystąpienie|
|FunctionExecutionUnits|Jednostki wykonawcze funkcji|Licznik|Średnia|Jednostki wykonawcze funkcji|Wystąpienie|
|FunctionExecutionCount|Liczba wykonań funkcji|Licznik|Średnia|Liczba wykonań funkcji|Wystąpienie|

## <a name="microsoftwebhostingenvironmentsmultirolepools"></a>Microsoft.Web/hostingEnvironments/multiRolePools

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Żądania|Żądania|Licznik|Łącznie|Żądania|Wystąpienie|
|BytesReceived|Dane wejściowe|Bajty|Łącznie|Dane wejściowe|Wystąpienie|
|Żądania|Dane wyjściowe|Bajty|Łącznie|Dane wyjściowe|Wystąpienie|
|Http101|HTTP 101|Licznik|Łącznie|HTTP 101|Wystąpienie|
|Http2xx|HTTP 2xx|Licznik|Łącznie|HTTP 2xx|Wystąpienie|
|Http3xx|HTTP 3xx|Licznik|Łącznie|HTTP 3xx|Wystąpienie|
|Http401|HTTP 401|Licznik|Łącznie|HTTP 401|Wystąpienie|
|Http403|HTTP 403|Licznik|Łącznie|HTTP 403|Wystąpienie|
|Http404|HTTP 404|Licznik|Łącznie|HTTP 404|Wystąpienie|
|Http406|HTTP 406|Licznik|Łącznie|HTTP 406|Wystąpienie|
|Http4xx|HTTP 4xx|Licznik|Łącznie|HTTP 4xx|Wystąpienie|
|Http5xx|Błędy serwera HTTP|Licznik|Łącznie|Błędy serwera HTTP|Wystąpienie|
|AverageResponseTime|Średni czas odpowiedzi|Sekundy|Średnia|Średni czas odpowiedzi|Wystąpienie|
|CpuPercentage|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|Wystąpienie|
|MemoryPercentage|Procent pamięci|Procent|Średnia|Procent pamięci|Wystąpienie|
|DiskQueueLength|Długość kolejki dysku|Licznik|Średnia|Długość kolejki dysku|Wystąpienie|
|HttpQueueLength|Długość kolejki HTTP|Licznik|Średnia|Długość kolejki HTTP|Wystąpienie|
|ActiveRequests|Aktywne żądania|Licznik|Łącznie|Aktywne żądania|Wystąpienie|
|TotalFrontEnds|Łącznie frontonów|Licznik|Średnia|Łącznie frontonów|Wystąpienie|
|SmallAppServicePlanInstances|Mała liczba procesów roboczych dla planu usługi App Service|Licznik|Średnia|Mała liczba procesów roboczych dla planu usługi App Service|Wystąpienie|
|MediumAppServicePlanInstances|Średnia liczba procesów roboczych dla planu usługi App Service|Licznik|Średnia|Średnia liczba procesów roboczych dla planu usługi App Service|Wystąpienie|
|LargeAppServicePlanInstances|Duża liczba procesów roboczych dla planu usługi App Service|Licznik|Średnia|Duża liczba procesów roboczych dla planu usługi App Service|Wystąpienie|

## <a name="microsoftwebhostingenvironmentsworkerpools"></a>Microsoft.Web/hostingEnvironments/workerPools

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|Wymiary|
|---|---|---|---|---|---|
|Łączna|Łączna liczba procesów roboczych|Licznik|Średnia|Łączna liczba procesów roboczych|Wystąpienie|
|WorkersAvailable|Dostępne procesy robocze|Licznik|Średnia|Dostępne procesy robocze|Wystąpienie|
|WorkersUsed|Używane procesy robocze|Licznik|Średnia|Używane procesy robocze|Wystąpienie|
|CpuPercentage|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|Wystąpienie|
|MemoryPercentage|Procent pamięci|Procent|Średnia|Procent pamięci|Wystąpienie|

## <a name="next-steps"></a>Kolejne kroki
* [Przeczytaj informacje o metryki w monitorze Azure](monitoring-overview-metrics.md)
* [Utwórz alerty na metryk](insights-receive-alert-notifications.md)
* [Eksportuj metryk do magazynu, Centrum zdarzeń lub analizy dzienników](monitoring-overview-of-diagnostic-logs.md)
