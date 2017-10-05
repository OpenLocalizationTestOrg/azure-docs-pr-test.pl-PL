---
title: "Metryki Monitor Azure - obsługiwanych metryki na typ zasobu | Dokumentacja firmy Microsoft"
description: "Lista dostępnych dla każdego typu zasobu z monitorem Azure metryk."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 4cd72c8193d66f164d9afa53af4b5203369b32dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Obsługiwane metryki z monitorem Azure
Azure Monitor udostępnia kilka metod do interakcji z metryk, takich jak wykresy je w portalu, dostępu do nich za pośrednictwem interfejsu API REST lub zapytań je przy użyciu programu PowerShell lub interfejsu wiersza polecenia. Poniżej przedstawiono pełną listę wszystkich metryki obecnie z potoku metryki Azure monitora.

> [!NOTE]
> Inne metryki mogą być dostępne w portalu lub przy użyciu starszej wersji interfejsów API. Ta lista zawiera tylko publicznej wersji zapoznawczej metryk dostępnych za pośrednictwem publicznej wersji zapoznawczej skonsolidowanych potoku metryki Azure Monitor.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|qpu_metric|QPU|Licznik|Średnia|QPU. Zakres 0-100 S1, 0 – 200 S2 i 0-400 dla S4|
|memory_metric|Memory (Pamięć)|Bajty|Średnia|Pamięci. W zakresie 0 – 25 GB na S1, 0 – 50 GB na S2 i 0 – 100 GB dla S4|
|TotalConnectionRequests|Całkowita liczba połączeń żądań|Licznik|Średnia|Całkowita liczba połączeń żądania. Są to przyjęcia.|
|SuccessfullConnectionsPerSec|Udane połączenia na sekundę|CountPerSecond|Średnia|Szybkość zakończeń udane połączenie.|
|TotalConnectionFailures|Całkowita liczba awarii|Licznik|Średnia|Całkowita liczba nieudanych prób połączenia.|
|CurrentUserSessions|Bieżące sesje użytkowników|Licznik|Średnia|Bieżąca liczba ustanowionych sesji użytkownika.|
|QueryPoolBusyThreads|Zapytanie z puli wątków zajęty|Licznik|Średnia|Liczba zajętych wątków w puli wątków zapytania.|
|CommandPoolJobQueueLength|Długość kolejki zadań puli polecenia|Licznik|Średnia|Liczba zadań w kolejce polecenia puli wątków.|
|ProcessingPoolJobQueueLength|Długość kolejki zadań przetwarzania w puli|Licznik|Średnia|Liczba zadań z systemem innym niż — I/O kolejki puli wątków przetwarzania.|
|CurrentConnections|Połączenia: Bieżąca liczba połączeń|Licznik|Średnia|Bieżąca liczba połączeń klienta.|
|CleanerCurrentPrice|Pamięci: Czyszczący bieżąca cena|Licznik|Średnia|Bieżąca cena pamięci $/ byte/godzina znormalizowane do 1000.|
|CleanerMemoryShrinkable|Pamięci: Zmniejszania pamięci czyszczący|Bajty|Średnia|Ilość pamięci w bajtach, mogą ulec czyszcząca przeczyszczanie w tle.|
|CleanerMemoryNonshrinkable|Pamięci: Czyszczący nonshrinkable pamięci|Bajty|Średnia|Ilość pamięci w bajtach, nie może ulec czyszcząca przeczyszczanie w tle.|
|MemoryUsage|Pamięci: Użycie pamięci|Bajty|Średnia|Użycie pamięci przez proces serwera jako używaną przy obliczaniu czyszczący cena pamięci. Taki sam jak licznika Process\PrivateBytes powiększony o rozmiar danych mapowanych na pamięć, ignorując wszystkie pamięci, która została zamapowana lub przydzielone przez aparat analizy w pamięci xVelocity (VertiPaq) przekracza Limit pamięci silnik xVelocity.|
|MemoryLimitHard|Pamięci: Twarde Limit pamięci|Bajty|Średnia|Limit pamięci twardym z pliku konfiguracji.|
|MemoryLimitHigh|Pamięć: Wysoki Limit pamięci|Bajty|Średnia|Limit pamięci wysokiej z pliku konfiguracji.|
|MemoryLimitLow|Pamięci: Niski Limit pamięci|Bajty|Średnia|Limit pamięci z pliku konfiguracji.|
|MemoryLimitVertiPaq|Pamięci: VertiPaq Limit pamięci|Bajty|Średnia|Limit w pamięci z pliku konfiguracji.|
|Przydział|Pamięć: limit przydziału|Bajty|Średnia|Limit przydziału pamięci, w bajtach. Limit przydziału pamięci jest nazywana rezerwacji pamięci grant lub pamięci.|
|QuotaBlocked|Pamięci: Zablokowane przydziału|Licznik|Średnia|Bieżąca liczba żądań przydziału, które są zablokowane, dopóki nie są zwalniane innych przydziałów pamięci.|
|VertiPaqNonpaged|Pamięci: Niestronicowana VertiPaq|Bajty|Średnia|Zablokowane bajtów pamięci zestawu do użycia przez aparat w pamięci roboczego.|
|VertiPaqPaged|Pamięci: Stronicowanej VertiPaq|Bajty|Średnia|Liczba bajtów stronicowanej pamięci dla danych w pamięci.|
|RowsReadPerSec|Przetwarzanie: Wiersze do odczytu na sekundę|CountPerSecond|Średnia|Liczba wierszy odczytywać wszystkie relacyjnych baz danych.|
|RowsConvertedPerSec|Przetwarzanie: Wierszy przekonwertowane na sekundę|CountPerSecond|Średnia|Liczba wierszy przekonwertować podczas przetwarzania.|
|RowsWrittenPerSec|Przetwarzanie: Wierszy, zapisany na sekundę|CountPerSecond|Średnia|Liczba wierszy, zapisany podczas przetwarzania.|
|CommandPoolBusyThreads|Wątki: Polecenie zajęty z puli wątków|Licznik|Średnia|Liczba zajętych wątków w puli wątków polecenia.|
|CommandPoolIdleThreads|Wątków: Polecenie puli wątków bezczynności|Licznik|Średnia|Liczba bezczynności wątków w puli wątków polecenia.|
|LongParsingBusyThreads|Wątków: Podczas analizowania zajęty wątków Long|Licznik|Średnia|Liczba zajętych wątków w puli wątków długo analizy.|
|LongParsingIdleThreads|Wątków: Podczas analizowania bezczynności wątków Long|Licznik|Średnia|Liczba bezczynności wątków w puli wątków długo analizy.|
|LongParsingJobQueueLength|Wątki: Czas analizowania długość kolejki zadań|Licznik|Średnia|Liczba zadań w kolejce długo analizy puli wątków.|
|ProcessingPoolBusyIOJobThreads|Wątki: Przetwarzania puli wątków zajęty zadania we/wy|Licznik|Średnia|Liczba wątków uruchomionych zadań we/wy w puli wątków przetwarzania.|
|ProcessingPoolBusyNonIOThreads|Wątków: Zajęty z puli wątków nie I/O przetwarzania|Licznik|Średnia|Liczba wątków uruchomionych zadań nie I/O w puli wątków przetwarzania.|
|ProcessingPoolIOJobQueueLength|Wątki: Przetwarzanie puli długość kolejki zadania we/wy|Licznik|Średnia|Liczba operacji We/Wy zadań w kolejce puli wątków przetwarzania.|
|ProcessingPoolIdleIOJobThreads|Wątki: Przetwarzania puli wątków bezczynności zadania we/wy|Licznik|Średnia|Liczba wątków bezczynności zadań we/wy w puli wątków przetwarzania.|
|ProcessingPoolIdleNonIOThreads|Wątki: Przetwarzanie bezczynności z puli wątków nie I/E|Licznik|Średnia|Liczba bezczynności wątków w puli wątków przetwarzania dedykowane dla zadań innych niż — I/O.|
|QueryPoolIdleThreads|Wątków: Wątki bezczynności puli zapytania|Licznik|Średnia|Liczba wątków bezczynności zadań we/wy w puli wątków przetwarzania.|
|QueryPoolJobQueueLength|Wątków: Lengt kolejki zadań puli zapytania|Licznik|Średnia|Liczba zadań w kolejce zapytań puli wątków.|
|ShortParsingBusyThreads|Wątków: Podczas analizowania zajęty wątków krótkiej|Licznik|Średnia|Liczba wątków zajęty w krótkim analizy puli wątków.|
|ShortParsingIdleThreads|Wątków: Podczas analizowania bezczynności wątków krótkiej|Licznik|Średnia|Liczba wątków bezczynności w krótkim analizy puli wątków.|
|ShortParsingJobQueueLength|Wątków: Podczas analizowania długość kolejki zadań krótkiej|Licznik|Średnia|Liczba zadań w kolejce krótkich analizy puli wątków.|
|memory_thrashing_metric|Wykonywania niepotrzebnych replik pamięci|Procent|Średnia|Średnia pamięci wykonywania niepotrzebnych replik.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|TotalRequests|Brama całkowita liczba żądań|Licznik|Łącznie|Liczba żądań bramy|
|SuccessfulRequests|Bramy pomyślnych żądań|Licznik|Łącznie|Liczba żądań pomyślnie bramy|
|UnauthorizedRequests|Brama nieautoryzowanych żądań|Licznik|Łącznie|Liczba żądań nieautoryzowanych bramy|
|FailedRequests|Żądań zakończonych niepowodzeniem bramy|Licznik|Łącznie|Liczba błędów w żądaniach bramy|
|OtherRequests|Inne żądania bramy|Licznik|Łącznie|Liczba innych żądań bramy|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|CoreCount|Dedykowany liczby rdzeni|Licznik|Łącznie|Całkowita liczba rdzeni dedykowanego konta usługi partia zadań|
|TotalNodeCount|Liczba dedykowanych węzłów|Licznik|Łącznie|Całkowita liczba dedykowanych węzłów w ramach konta usługi partia zadań|
|LowPriorityCoreCount|Liczby rdzeni LowPriority|Licznik|Łącznie|Całkowita liczba rdzeni niskiego priorytetu konta usługi partia zadań|
|TotalLowPriorityNodeCount|Liczba węzłów o niskim priorytecie|Licznik|Łącznie|Całkowita liczba węzłów niskiego priorytetu w ramach konta usługi partia zadań|
|CreatingNodeCount|Tworzenie liczba węzłów|Licznik|Łącznie|Liczba węzłów tworzona|
|StartingNodeCount|Początkowa liczba węzłów|Licznik|Łącznie|Liczba węzłów uruchamiania|
|WaitingForStartTaskNodeCount|Liczba węzłów zadań Start oczekiwania|Licznik|Łącznie|Liczba węzłów oczekiwanie na zakończenie zadania Start|
|StartTaskFailedNodeCount|Zadania uruchamiania nie powiodło się liczba węzłów|Licznik|Łącznie|Liczba węzłów, gdzie uruchomić zadanie nie powiodło się|
|IdleNodeCount|Liczba węzłów w stanie bezczynności|Licznik|Łącznie|Liczba węzłów bezczynności|
|OfflineNodeCount|Liczba węzłów w trybie offline|Licznik|Łącznie|Liczba węzłów w trybie offline|
|RebootingNodeCount|Liczba węzłów ponowny rozruch|Licznik|Łącznie|Liczba ponowny rozruch węzłów|
|ReimagingNodeCount|Liczba węzłów ponownej instalacji systemu|Licznik|Łącznie|Liczba węzłów, ponownej instalacji systemu|
|RunningNodeCount|Liczba węzłów|Licznik|Łącznie|Liczba uruchomionych węzłach|
|LeavingPoolNodeCount|Pozostawienie liczba węzłów w puli|Licznik|Łącznie|Liczba węzłów, pozostawiając puli|
|UnusableNodeCount|Nie można użyć liczba węzłów|Licznik|Łącznie|Liczba węzłów bezużyteczne|
|PreemptedNodeCount|Wywłaszczone liczba węzłów|Licznik|Łącznie|Liczba węzłów przeniesiona|
|TaskStartEvent|Zadanie rozpoczęcia zdarzenia|Licznik|Łącznie|Całkowita liczba zadań, które zostały uruchomione|
|TaskCompleteEvent|Zadania ukończone zdarzenia|Licznik|Łącznie|Całkowita liczba zadań, które zostały ukończone|
|TaskFailEvent|Zdarzenia błędów zadań|Licznik|Łącznie|Całkowita liczba zadań, które zostały ukończone w stanie niepowodzenia|
|PoolCreateEvent|Pula Tworzenie zdarzenia|Licznik|Łącznie|Całkowita liczba pul, które zostały utworzone|
|PoolResizeStartEvent|Zdarzenia rozpoczęcia zmiany rozmiaru puli|Licznik|Łącznie|Całkowita liczba zmienia rozmiar puli, które zostały uruchomione|
|PoolResizeCompleteEvent|Zakończenie zdarzenia zmiany rozmiaru puli|Licznik|Łącznie|Całkowita liczba zmienia rozmiar puli, które zostały ukończone|
|PoolDeleteStartEvent|Pula Usuń rozpoczęcia zdarzenia|Licznik|Łącznie|Całkowita liczba usuwa puli, które zostały uruchomione|
|PoolDeleteCompleteEvent|Zakończenie zdarzenia Delete puli|Licznik|Łącznie|Całkowita liczba usuwa puli, które zostały ukończone|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|connectedclients|Podłączeni klienci|Licznik|Maksymalna||
|totalcommandsprocessed|Całkowita liczba operacji|Licznik|Łącznie||
|Trafienia w pamięci podręcznej|Trafień w pamięci podręcznej|Licznik|Łącznie||
|cachemisses|Chybienia pamięci podręcznej|Licznik|Łącznie||
|getcommands|Pobiera|Licznik|Łącznie||
|setcommands|Zestawy|Licznik|Łącznie||
|evictedkeys|Wykluczone kluczy|Licznik|Łącznie||
|totalkeys|Wszystkie klucze|Licznik|Maksymalna||
|expiredkeys|Wygasłe kluczy|Licznik|Łącznie||
|usedmemory|Używana pamięć|Bajty|Maksymalna||
|usedmemoryRss|Używana pamięć RSS|Bajty|Maksymalna||
|serverLoad|Obciążenie serwera|Procent|Maksymalna||
|cacheWrite|Pamięć podręczna zapisu|BytesPerSecond|Maksymalna||
|cacheRead|Odczyt z pamięci podręcznej|BytesPerSecond|Maksymalna||
|percentProcessorTime|Procesor CPU|Procent|Maksymalna||
|connectedclients0|Podłączeni klienci (niezależnego fragmentu 0)|Licznik|Maksymalna||
|totalcommandsprocessed0|Całkowita liczba operacji (identyfikator niezależnego fragmentu 0)|Licznik|Łącznie||
|cachehits0|Trafień w pamięci podręcznej (niezależnego fragmentu 0)|Licznik|Łącznie||
|cachemisses0|Chybienia pamięci podręcznej (niezależnego fragmentu 0)|Licznik|Łącznie||
|getcommands0|Pobiera (niezależnego fragmentu 0)|Licznik|Łącznie||
|setcommands0|Zestawy (niezależnego fragmentu 0)|Licznik|Łącznie||
|evictedkeys0|Klucze wykluczonym (niezależnego fragmentu 0)|Licznik|Łącznie||
|totalkeys0|Wszystkie klucze (niezależnego fragmentu 0)|Licznik|Maksymalna||
|expiredkeys0|Wygasłe kluczy (niezależnego fragmentu 0)|Licznik|Łącznie||
|usedmemory0|Używana pamięć (niezależnego fragmentu 0)|Bajty|Maksymalna||
|usedmemoryRss0|Używana pamięć RSS (niezależnego fragmentu 0)|Bajty|Maksymalna||
|serverLoad0|Obciążenia serwera (niezależnego fragmentu 0)|Procent|Maksymalna||
|cacheWrite0|Pamięć podręczna zapisu (niezależnego fragmentu 0)|BytesPerSecond|Maksymalna||
|cacheRead0|Odczytu pamięci podręcznej (niezależnego fragmentu 0)|BytesPerSecond|Maksymalna||
|percentProcessorTime0|Procesor (niezależnego fragmentu 0)|Procent|Maksymalna||
|connectedclients1|Podłączeni klienci (niezależnego fragmentu 1)|Licznik|Maksymalna||
|totalcommandsprocessed1|Całkowita liczba operacji (identyfikator niezależnego fragmentu 1)|Licznik|Łącznie||
|cachehits1|Trafień w pamięci podręcznej (niezależnego fragmentu 1)|Licznik|Łącznie||
|cachemisses1|Chybienia pamięci podręcznej (niezależnego fragmentu 1)|Licznik|Łącznie||
|getcommands1|Pobiera (niezależnego fragmentu 1)|Licznik|Łącznie||
|setcommands1|Zestawy (niezależnego fragmentu 1)|Licznik|Łącznie||
|evictedkeys1|Klucze wykluczonym (niezależnego fragmentu 1)|Licznik|Łącznie||
|totalkeys1|Wszystkie klucze (niezależnego fragmentu 1)|Licznik|Maksymalna||
|expiredkeys1|Wygasłe kluczy (niezależnego fragmentu 1)|Licznik|Łącznie||
|usedmemory1|Używana pamięć (niezależnego fragmentu 1)|Bajty|Maksymalna||
|usedmemoryRss1|Używana pamięć RSS (niezależnego fragmentu 1)|Bajty|Maksymalna||
|serverLoad1|Obciążenia serwera (niezależnego fragmentu 1)|Procent|Maksymalna||
|cacheWrite1|Pamięć podręczna zapisu (niezależnego fragmentu 1)|BytesPerSecond|Maksymalna||
|cacheRead1|Odczytu pamięci podręcznej (niezależnego fragmentu 1)|BytesPerSecond|Maksymalna||
|percentProcessorTime1|Procesor (niezależnego fragmentu 1)|Procent|Maksymalna||
|connectedclients2|Podłączeni klienci (niezależnego fragmentu 2)|Licznik|Maksymalna||
|totalcommandsprocessed2|Całkowita liczba operacji (identyfikator niezależnego fragmentu 2)|Licznik|Łącznie||
|cachehits2|Trafień w pamięci podręcznej (niezależnego fragmentu 2)|Licznik|Łącznie||
|cachemisses2|Chybienia pamięci podręcznej (niezależnego fragmentu 2)|Licznik|Łącznie||
|getcommands2|Pobiera (niezależnego fragmentu 2)|Licznik|Łącznie||
|setcommands2|Zestawy (niezależnego fragmentu 2)|Licznik|Łącznie||
|evictedkeys2|Klucze wykluczonym (niezależnego fragmentu 2)|Licznik|Łącznie||
|totalkeys2|Wszystkie klucze (niezależnego fragmentu 2)|Licznik|Maksymalna||
|expiredkeys2|Wygasłe kluczy (niezależnego fragmentu 2)|Licznik|Łącznie||
|usedmemory2|Używana pamięć (niezależnego fragmentu 2)|Bajty|Maksymalna||
|usedmemoryRss2|Używana pamięć RSS (niezależnego fragmentu 2)|Bajty|Maksymalna||
|serverLoad2|Obciążenia serwera (niezależnego fragmentu 2)|Procent|Maksymalna||
|cacheWrite2|Pamięć podręczna zapisu (niezależnego fragmentu 2)|BytesPerSecond|Maksymalna||
|cacheRead2|Odczytu pamięci podręcznej (niezależnego fragmentu 2)|BytesPerSecond|Maksymalna||
|percentProcessorTime2|Procesor (niezależnego fragmentu 2)|Procent|Maksymalna||
|connectedclients3|Podłączeni klienci (niezależnego fragmentu 3)|Licznik|Maksymalna||
|totalcommandsprocessed3|Całkowita liczba operacji (identyfikator niezależnego fragmentu 3)|Licznik|Łącznie||
|cachehits3|Trafień w pamięci podręcznej (niezależnego fragmentu 3)|Licznik|Łącznie||
|cachemisses3|Chybienia pamięci podręcznej (niezależnego fragmentu 3)|Licznik|Łącznie||
|getcommands3|Pobiera (niezależnego fragmentu 3)|Licznik|Łącznie||
|setcommands3|Zestawy (niezależnego fragmentu 3)|Licznik|Łącznie||
|evictedkeys3|Klucze wykluczonym (niezależnego fragmentu 3)|Licznik|Łącznie||
|totalkeys3|Wszystkie klucze (niezależnego fragmentu 3)|Licznik|Maksymalna||
|expiredkeys3|Wygasłe kluczy (niezależnego fragmentu 3)|Licznik|Łącznie||
|usedmemory3|Używana pamięć (niezależnego fragmentu 3)|Bajty|Maksymalna||
|usedmemoryRss3|Używana pamięć RSS (niezależnego fragmentu 3)|Bajty|Maksymalna||
|serverLoad3|Obciążenia serwera (niezależnego fragmentu 3)|Procent|Maksymalna||
|cacheWrite3|Pamięć podręczna zapisu (niezależnego fragmentu 3)|BytesPerSecond|Maksymalna||
|cacheRead3|Odczytu pamięci podręcznej (niezależnego fragmentu 3)|BytesPerSecond|Maksymalna||
|percentProcessorTime3|Procesor (niezależnego fragmentu 3)|Procent|Maksymalna||
|connectedclients4|Podłączeni klienci (niezależnego fragmentu 4)|Licznik|Maksymalna||
|totalcommandsprocessed4|Całkowita liczba operacji (identyfikator niezależnego fragmentu 4)|Licznik|Łącznie||
|cachehits4|Trafień w pamięci podręcznej (niezależnego fragmentu 4)|Licznik|Łącznie||
|cachemisses4|Chybienia pamięci podręcznej (niezależnego fragmentu 4)|Licznik|Łącznie||
|getcommands4|Pobiera (niezależnego fragmentu 4)|Licznik|Łącznie||
|setcommands4|Zestawy (niezależnego fragmentu 4)|Licznik|Łącznie||
|evictedkeys4|Klucze wykluczonym (niezależnego fragmentu 4)|Licznik|Łącznie||
|totalkeys4|Wszystkie klucze (niezależnego fragmentu 4)|Licznik|Maksymalna||
|expiredkeys4|Wygasłe kluczy (niezależnego fragmentu 4)|Licznik|Łącznie||
|usedmemory4|Używana pamięć (niezależnego fragmentu 4)|Bajty|Maksymalna||
|usedmemoryRss4|Używana pamięć RSS (niezależnego fragmentu 4)|Bajty|Maksymalna||
|serverLoad4|Obciążenia serwera (niezależnego fragmentu 4)|Procent|Maksymalna||
|cacheWrite4|Pamięć podręczna zapisu (niezależnego fragmentu 4)|BytesPerSecond|Maksymalna||
|cacheRead4|Odczytu pamięci podręcznej (niezależnego fragmentu 4)|BytesPerSecond|Maksymalna||
|percentProcessorTime4|Procesor (niezależnego fragmentu 4)|Procent|Maksymalna||
|connectedclients5|Podłączeni klienci (niezależnego fragmentu 5)|Licznik|Maksymalna||
|totalcommandsprocessed5|Całkowita liczba operacji (identyfikator niezależnego fragmentu 5)|Licznik|Łącznie||
|cachehits5|Trafień w pamięci podręcznej (niezależnego fragmentu 5)|Licznik|Łącznie||
|cachemisses5|Chybienia pamięci podręcznej (niezależnego fragmentu 5)|Licznik|Łącznie||
|getcommands5|Pobiera (niezależnego fragmentu 5)|Licznik|Łącznie||
|setcommands5|Zestawy (niezależnego fragmentu 5)|Licznik|Łącznie||
|evictedkeys5|Klucze wykluczonym (niezależnego fragmentu 5)|Licznik|Łącznie||
|totalkeys5|Wszystkie klucze (niezależnego fragmentu 5)|Licznik|Maksymalna||
|expiredkeys5|Wygasłe kluczy (niezależnego fragmentu 5)|Licznik|Łącznie||
|usedmemory5|Używana pamięć (niezależnego fragmentu 5)|Bajty|Maksymalna||
|usedmemoryRss5|Używana pamięć RSS (niezależnego fragmentu 5)|Bajty|Maksymalna||
|serverLoad5|Obciążenia serwera (niezależnego fragmentu 5)|Procent|Maksymalna||
|cacheWrite5|Pamięć podręczna zapisu (niezależnego fragmentu 5)|BytesPerSecond|Maksymalna||
|cacheRead5|Odczytu pamięci podręcznej (niezależnego fragmentu 5)|BytesPerSecond|Maksymalna||
|percentProcessorTime5|Procesor (niezależnego fragmentu 5)|Procent|Maksymalna||
|connectedclients6|Podłączeni klienci (niezależnego fragmentu 6)|Licznik|Maksymalna||
|totalcommandsprocessed6|Całkowita liczba operacji (identyfikator niezależnego fragmentu 6)|Licznik|Łącznie||
|cachehits6|Trafień w pamięci podręcznej (niezależnego fragmentu 6)|Licznik|Łącznie||
|cachemisses6|Chybienia pamięci podręcznej (niezależnego fragmentu 6)|Licznik|Łącznie||
|getcommands6|Pobiera (niezależnego fragmentu 6)|Licznik|Łącznie||
|setcommands6|Zestawy (niezależnego fragmentu 6)|Licznik|Łącznie||
|evictedkeys6|Klucze wykluczonym (niezależnego fragmentu 6)|Licznik|Łącznie||
|totalkeys6|Wszystkie klucze (niezależnego fragmentu 6)|Licznik|Maksymalna||
|expiredkeys6|Wygasłe kluczy (niezależnego fragmentu 6)|Licznik|Łącznie||
|usedmemory6|Używana pamięć (niezależnego fragmentu 6)|Bajty|Maksymalna||
|usedmemoryRss6|Używana pamięć RSS (niezależnego fragmentu 6)|Bajty|Maksymalna||
|serverLoad6|Obciążenia serwera (niezależnego fragmentu 6)|Procent|Maksymalna||
|cacheWrite6|Pamięć podręczna zapisu (niezależnego fragmentu 6)|BytesPerSecond|Maksymalna||
|cacheRead6|Odczytu pamięci podręcznej (niezależnego fragmentu 6)|BytesPerSecond|Maksymalna||
|percentProcessorTime6|Procesor (niezależnego fragmentu 6)|Procent|Maksymalna||
|connectedclients7|Podłączeni klienci (niezależnego fragmentu 7)|Licznik|Maksymalna||
|totalcommandsprocessed7|Całkowita liczba operacji (identyfikator niezależnego fragmentu 7)|Licznik|Łącznie||
|cachehits7|Trafień w pamięci podręcznej (niezależnego fragmentu 7)|Licznik|Łącznie||
|cachemisses7|Chybienia pamięci podręcznej (niezależnego fragmentu 7)|Licznik|Łącznie||
|getcommands7|Pobiera (niezależnego fragmentu 7)|Licznik|Łącznie||
|setcommands7|Zestawy (niezależnego fragmentu 7)|Licznik|Łącznie||
|evictedkeys7|Klucze wykluczonym (niezależnego fragmentu 7)|Licznik|Łącznie||
|totalkeys7|Wszystkie klucze (niezależnego fragmentu 7)|Licznik|Maksymalna||
|expiredkeys7|Wygasłe kluczy (niezależnego fragmentu 7)|Licznik|Łącznie||
|usedmemory7|Używana pamięć (niezależnego fragmentu 7)|Bajty|Maksymalna||
|usedmemoryRss7|Używana pamięć RSS (niezależnego fragmentu 7)|Bajty|Maksymalna||
|serverLoad7|Obciążenia serwera (niezależnego fragmentu 7)|Procent|Maksymalna||
|cacheWrite7|Pamięć podręczna zapisu (niezależnego fragmentu 7)|BytesPerSecond|Maksymalna||
|cacheRead7|Odczytu pamięci podręcznej (niezależnego fragmentu 7)|BytesPerSecond|Maksymalna||
|percentProcessorTime7|Procesor (niezależnego fragmentu 7)|Procent|Maksymalna||
|connectedclients8|Podłączeni klienci (niezależnego fragmentu 8)|Licznik|Maksymalna||
|totalcommandsprocessed8|Całkowita liczba operacji (identyfikator niezależnego fragmentu 8)|Licznik|Łącznie||
|cachehits8|Trafień w pamięci podręcznej (niezależnego fragmentu 8)|Licznik|Łącznie||
|cachemisses8|Chybienia pamięci podręcznej (niezależnego fragmentu 8)|Licznik|Łącznie||
|getcommands8|Pobiera (niezależnego fragmentu 8)|Licznik|Łącznie||
|setcommands8|Zestawy (niezależnego fragmentu 8)|Licznik|Łącznie||
|evictedkeys8|Klucze wykluczonym (niezależnego fragmentu 8)|Licznik|Łącznie||
|totalkeys8|Wszystkie klucze (niezależnego fragmentu 8)|Licznik|Maksymalna||
|expiredkeys8|Wygasłe kluczy (niezależnego fragmentu 8)|Licznik|Łącznie||
|usedmemory8|Używana pamięć (niezależnego fragmentu 8)|Bajty|Maksymalna||
|usedmemoryRss8|Używana pamięć RSS (niezależnego fragmentu 8)|Bajty|Maksymalna||
|serverLoad8|Obciążenia serwera (niezależnego fragmentu 8)|Procent|Maksymalna||
|cacheWrite8|Pamięć podręczna zapisu (niezależnego fragmentu 8)|BytesPerSecond|Maksymalna||
|cacheRead8|Odczytu pamięci podręcznej (niezależnego fragmentu 8)|BytesPerSecond|Maksymalna||
|percentProcessorTime8|Procesor (niezależnego fragmentu 8)|Procent|Maksymalna||
|connectedclients9|Podłączeni klienci (niezależnego fragmentu 9)|Licznik|Maksymalna||
|totalcommandsprocessed9|Całkowita liczba operacji (identyfikator niezależnego fragmentu 9)|Licznik|Łącznie||
|cachehits9|Trafień w pamięci podręcznej (niezależnego fragmentu 9)|Licznik|Łącznie||
|cachemisses9|Chybienia pamięci podręcznej (niezależnego fragmentu 9)|Licznik|Łącznie||
|getcommands9|Pobiera (niezależnego fragmentu 9)|Licznik|Łącznie||
|setcommands9|Zestawy (niezależnego fragmentu 9)|Licznik|Łącznie||
|evictedkeys9|Klucze wykluczonym (niezależnego fragmentu 9)|Licznik|Łącznie||
|totalkeys9|Wszystkie klucze (niezależnego fragmentu 9)|Licznik|Maksymalna||
|expiredkeys9|Wygasłe kluczy (niezależnego fragmentu 9)|Licznik|Łącznie||
|usedmemory9|Używana pamięć (niezależnego fragmentu 9)|Bajty|Maksymalna||
|usedmemoryRss9|Używana pamięć RSS (niezależnego fragmentu 9)|Bajty|Maksymalna||
|serverLoad9|Obciążenia serwera (niezależnego fragmentu 9)|Procent|Maksymalna||
|cacheWrite9|Pamięć podręczna zapisu (niezależnego fragmentu 9)|BytesPerSecond|Maksymalna||
|cacheRead9|Odczytu pamięci podręcznej (niezależnego fragmentu 9)|BytesPerSecond|Maksymalna||
|percentProcessorTime9|Procesor (niezależnego fragmentu 9)|Procent|Maksymalna||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|TotalCalls|Całkowita liczba wywołań|Licznik|Łącznie|Całkowita liczba połączeń.|
|SuccessfulCalls|Pomyślnych wywołań|Licznik|Łącznie|Liczba pomyślnych wywołań.|
|TotalErrors|Całkowita liczba błędów|Licznik|Łącznie|Całkowita liczba wywołań z odpowiedzi na błąd (4xx kod odpowiedzi HTTP lub 5xx).|
|BlockedCalls|Wywołania zablokowanych|Licznik|Łącznie|Liczba wywołań tej Przekroczono szybkość lub limit przydziału.|
|ServerErrors|Błędy serwera|Licznik|Łącznie|Liczba wywołań z powodu błędu wewnętrznego usługi (5xx kod odpowiedzi HTTP).|
|ClientErrors|Klientów z błędami|Licznik|Łącznie|Liczba wywołań z powodu błędu po stronie klienta (4xx kod odpowiedzi HTTP).|
|DataIn|Dane w|Bajty|Łącznie|Rozmiar danych przychodzących w bajtach.|
|DataOut|Dla danych wychodzących|Bajty|Łącznie|Rozmiar danych wychodzących w bajtach.|
|Opóźnienie|Opóźnienie|W milisekundach|Średnia|Opóźnienie w milisekundach.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|Procent procesora CPU|Procent procesora CPU|Procent|Średnia|Wartość procentowa obliczeniowe przydzielone jednostki, które są obecnie używane przez maszyny wirtualne|
|Sieci w|Sieci w|Bajty|Łącznie|Liczba bajtów odebranych na wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch przychodzący)|
|Sieci limit|Sieci limit|Bajty|Łącznie|Liczba bajtów na wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch wychodzący)|
|Bajty odczytu dysku|Bajty odczytu dysku|Bajty|Łącznie|Całkowita liczba bajtów do odczytu z dysku podczas okresu monitorowania|
|Bajty zapisu dysku|Bajty zapisu dysku|Bajty|Łącznie|Całkowita liczba bajtów zapisywanych na dysku podczas okresu monitorowania|
|Dysk operacje odczytu/s|Dysk operacje odczytu/s|CountPerSecond|Średnia|Czas odczytu dyskowego IOPS|
|Operacje zapisu dysku/s|Operacje zapisu dysku/s|CountPerSecond|Średnia|Zapisu dyskowego IOPS|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|Procent procesora CPU|Procent procesora CPU|Procent|Średnia|Wartość procentowa obliczeniowe przydzielone jednostki, które są obecnie używane przez maszyny wirtualne|
|Sieci w|Sieci w|Bajty|Łącznie|Liczba bajtów odebranych na wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch przychodzący)|
|Sieci limit|Sieci limit|Bajty|Łącznie|Liczba bajtów na wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch wychodzący)|
|Bajty odczytu dysku|Bajty odczytu dysku|Bajty|Łącznie|Całkowita liczba bajtów do odczytu z dysku podczas okresu monitorowania|
|Bajty zapisu dysku|Bajty zapisu dysku|Bajty|Łącznie|Całkowita liczba bajtów zapisywanych na dysku podczas okresu monitorowania|
|Dysk operacje odczytu/s|Dysk operacje odczytu/s|CountPerSecond|Średnia|Czas odczytu dyskowego IOPS|
|Operacje zapisu dysku/s|Operacje zapisu dysku/s|CountPerSecond|Średnia|Zapisu dyskowego IOPS|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|Procent procesora CPU|Procent procesora CPU|Procent|Średnia|Wartość procentowa obliczeniowe przydzielone jednostki, które są obecnie używane przez maszyny wirtualne|
|Sieci w|Sieci w|Bajty|Łącznie|Liczba bajtów odebranych na wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch przychodzący)|
|Sieci limit|Sieci limit|Bajty|Łącznie|Liczba bajtów na wszystkich interfejsach sieciowych przez maszyny wirtualne (ruch wychodzący)|
|Bajty odczytu dysku|Bajty odczytu dysku|Bajty|Łącznie|Całkowita liczba bajtów do odczytu z dysku podczas okresu monitorowania|
|Bajty zapisu dysku|Bajty zapisu dysku|Bajty|Łącznie|Całkowita liczba bajtów zapisywanych na dysku podczas okresu monitorowania|
|Dysk operacje odczytu/s|Dysk operacje odczytu/s|CountPerSecond|Średnia|Czas odczytu dyskowego IOPS|
|Operacje zapisu dysku/s|Operacje zapisu dysku/s|CountPerSecond|Średnia|Zapisu dyskowego IOPS|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|DCIApiCalls|Wywołania Insights interfejsu API klienta|Licznik|Łącznie||
|DCIMappingImportOperationSuccessfulLines|Mapowanie wierszy pomyślnych operacji importu|Licznik|Łącznie||
|DCIMappingImportOperationFailedLines|Mapowanie operacji importowania nie powiodła się wierszy|Licznik|Łącznie||
|DCIMappingImportOperationTotalLines|Całkowita liczba wierszy operacji importu mapowania|Licznik|Łącznie||
|DCIMappingImportOperationRuntimeInSeconds|Mapowanie importu operacji w czasie wykonywania w sekundach|Sekundy|Łącznie||
|DCIOutboundProfileExportSucceeded|Eksportowanie profilu ruchu wychodzącego zakończyło się pomyślnie|Licznik|Łącznie||
|DCIOutboundProfileExportFailed|Eksportowanie profilu ruchu wychodzącego nie powiodło się|Licznik|Łącznie||
|DCIOutboundProfileExportDuration|Czas trwania eksportowania profilu ruchu wychodzącego|Sekundy|Łącznie||
|DCIOutboundKpiExportSucceeded|Wychodzące eksportowanie Kpi powiodło się|Licznik|Łącznie||
|DCIOutboundKpiExportFailed|Wychodzące eksportowanie wskaźnika Kpi nie powiodło się|Licznik|Łącznie||
|DCIOutboundKpiExportDuration|Czas trwania wychodzącego eksportu wskaźnika Kpi|Sekundy|Łącznie||
|DCIOutboundKpiExportStarted|Rozpoczęto eksportu wychodzącego kluczowego wskaźnika wydajności|Sekundy|Łącznie||
|DCIOutboundKpiRecordCount|Liczba rekordów wychodzącego wskaźnika Kpi|Sekundy|Łącznie||
|DCIOutboundProfileExportCount|Liczba eksportowania profilu ruchu wychodzącego|Sekundy|Łącznie||
|DCIOutboundInitialProfileExportFailed|Eksportowanie wychodzącego początkowej profilu nie powiodło się|Sekundy|Łącznie||
|DCIOutboundInitialProfileExportSucceeded|Wychodzące profilu początkowej eksportu|Sekundy|Łącznie||
|DCIOutboundInitialKpiExportFailed|Wychodzące początkowej eksportowanie wskaźnika Kpi nie powiodło się|Sekundy|Łącznie||
|DCIOutboundInitialKpiExportSucceeded|Wychodzące początkowej eksportu kluczowego wskaźnika wydajności zakończyło się pomyślnie.|Sekundy|Łącznie||
|DCIOutboundInitialProfileExportDurationInSeconds|Wychodzące profilu początkowej eksportu czas w sekundach|Sekundy|Łącznie||
|AdlaJobForStandardKpiFailed|Zadanie Adla dla standardowych wskaźnika Kpi nie powiodło się w sekundach|Sekundy|Łącznie||
|AdlaJobForStandardKpiTimeOut|Zadanie Adla standardowa wskaźnika Kpi limitu czasu w sekundach|Sekundy|Łącznie||
|AdlaJobForStandardKpiCompleted|Zadanie Adla standardowe kluczowego wskaźnika wydajności w sekundach|Sekundy|Łącznie||
|ImportASAValuesFailed|Wartości ASA importu nie powiodła się, liczba|Licznik|Łącznie||
|ImportASAValuesSucceeded|Wartości ASA importowanie zakończyło się pomyślnie, liczba|Licznik|Łącznie||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|JobEndedSuccess|Zadania zakończone pomyślnie|Licznik|Łącznie|Liczba zadań zakończonych pomyślnie.|
|JobEndedFailure|Zadania zakończone niepowodzeniem|Licznik|Łącznie|Liczba zadań zakończonych niepowodzeniem.|
|JobEndedCancelled|Anulowane zadania|Licznik|Łącznie|Liczba zadań zostało anulowane.|
|JobAUEndedSuccess|Pomyślne czasu Australia|Sekundy|Łącznie|Łączny czas Australia zadań zakończonych pomyślnie.|
|JobAUEndedFailure|Czas Australia nie powiodło się|Sekundy|Łącznie|Łączny czas Australia zadania zakończone niepowodzeniem.|
|JobAUEndedCancelled|Anulowane czasu Australia|Sekundy|Łącznie|Łączny czas Australia anulowane zadania.|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|cpu_percent|Procent procesora CPU|Procent|Średnia|Procent procesora CPU|
|compute_limit|Obliczenia bazy danych limit jednostki|Licznik|Średnia|Obliczenia bazy danych limit jednostki|
|compute_consumption_percent|Obliczenia bazy danych procent jednostki|Procent|Średnia|Obliczenia bazy danych procent jednostki|
|memory_percent|Procent pamięci|Procent|Średnia|Procent pamięci|
|io_consumption_percent|Procent we/wy|Procent|Średnia|Procent we/wy|
|storage_percent|Procent użycia magazynu|Procent|Średnia|Procent użycia magazynu|
|storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|
|storage_limit|Limit magazynu|Bajty|Średnia|Limit magazynu|
|active_connections|Całkowita liczba aktywnych połączeń|Licznik|Średnia|Całkowita liczba aktywnych połączeń|
|connections_failed|Całkowita liczba połączeń nie powiodło się|Licznik|Średnia|Całkowita liczba połączeń nie powiodło się|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|cpu_percent|Procent procesora CPU|Procent|Średnia|Procent procesora CPU|
|compute_limit|Obliczenia bazy danych limit jednostki|Licznik|Średnia|Obliczenia bazy danych limit jednostki|
|compute_consumption_percent|Obliczenia bazy danych procent jednostki|Procent|Średnia|Obliczenia bazy danych procent jednostki|
|memory_percent|Procent pamięci|Procent|Średnia|Procent pamięci|
|io_consumption_percent|Procent we/wy|Procent|Średnia|Procent we/wy|
|storage_percent|Procent użycia magazynu|Procent|Średnia|Procent użycia magazynu|
|storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|
|storage_limit|Limit magazynu|Bajty|Średnia|Limit magazynu|
|active_connections|Całkowita liczba aktywnych połączeń|Licznik|Średnia|Całkowita liczba aktywnych połączeń|
|connections_failed|Całkowita liczba połączeń nie powiodło się|Licznik|Średnia|Całkowita liczba połączeń nie powiodło się|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Próby wysłania wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów telemetrii urządzenia do chmury próby wysłania do Centrum IoT|
|d2c.telemetry.ingress.SUCCESS|Wysłane wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów telemetrii urządzenia do chmury pomyślnie wysłane do Centrum IoT|
|c2d.Commands.egress.COMPLETE.SUCCESS|Polecenia zakończona|Licznik|Łącznie|Liczba poleceń chmury do urządzenia, które zakończyło się powodzeniem, urządzenia|
|c2d.Commands.egress.Abandon.SUCCESS|Porzucone poleceń|Licznik|Łącznie|Liczba poleceń chmury do urządzenia porzucone przez urządzenie|
|c2d.Commands.egress.Reject.SUCCESS|Polecenia odrzucone|Licznik|Łącznie|Liczba odrzuconych przez urządzenie poleceń chmury do urządzenia|
|devices.totalDevices|Łączna liczba urządzeń|Licznik|Łącznie|Liczba urządzeń zarejestrowanych do Centrum IoT|
|devices.connectedDevices.allProtocol|Połączonych urządzeń|Licznik|Łącznie|Liczba urządzeń połączonych z Centrum IoT|
|d2c.telemetry.egress.SUCCESS|Dostarczane wiadomości telemetrii|Licznik|Łącznie|Liczba komunikatów pomyślnie zostały zapisane do punktów końcowych (łącznie)|
|d2c.telemetry.egress.dropped|Porzucone komunikaty|Licznik|Łącznie|Liczba wiadomości porzuconych z powodu braku punktu końcowego dostarczania|
|d2c.telemetry.egress.orphaned|Oddzielone wiadomości|Licznik|Łącznie|Aktualna liczba wiadomości nie zgodnych żadnych tras, łącznie z rezerwowego trasy|
|d2c.telemetry.egress.invalid|Nieprawidłowy wiadomości|Licznik|Łącznie|Aktualna liczba wiadomości nie są dostarczane z powodu niezgodności z punktu końcowego|
|d2c.telemetry.egress.Fallback|Wiadomości pasujące rezerwowy warunku|Licznik|Łącznie|Liczba komunikatów zapisanych do rezerwowego punktu końcowego|
|d2c.endpoints.egress.eventHubs|Komunikaty dostarczone do Centrum zdarzeń punkty końcowe|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie zapisane punkty końcowe Centrum zdarzeń|
|d2c.endpoints.latency.eventHubs|Opóźnienie komunikat dla punktów końcowych Centrum zdarzeń|w milisekundach|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego Centrum zdarzeń, w milisekundach|
|d2c.endpoints.egress.serviceBusQueues|Komunikaty dostarczone do punktów końcowych z kolejką usługi Service Bus|Licznik|Łącznie|Liczba wiadomości kolejką usługi Service Bus punkty końcowe zostały pomyślnie zapisane|
|d2c.endpoints.latency.serviceBusQueues|Czas oczekiwania na wiadomość dla punktów końcowych z kolejką usługi Service Bus|w milisekundach|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego kolejką usługi Service Bus, w milisekundach|
|d2c.endpoints.egress.serviceBusTopics|Komunikaty dostarczone do punktów końcowych temat magistrali usług|Licznik|Łącznie|Liczba wiadomości zostały pomyślnie zapisane punkty końcowe temat magistrali usług|
|d2c.endpoints.latency.serviceBusTopics|Opóźnienie komunikat dla punktów końcowych temat magistrali usług|w milisekundach|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i komunikat przychodzący do punktu końcowego Service Bus tematu w milisekundach|
|d2c.endpoints.egress.builtIn.events|Wiadomość dostarczona do wbudowanej punktu końcowego (wiadomości/zdarzeń)|Licznik|Łącznie|Liczba komunikatów wbudowanym punktem końcowym (wiadomości/zdarzeń) zostały pomyślnie zapisane|
|d2c.endpoints.latency.builtIn.events|Czas oczekiwania wiadomości na wbudowanym punktem końcowym (wiadomości/zdarzeń)|w milisekundach|Średnia|Średnie opóźnienie między komunikat przychodzący z Centrum IoT i transfer danych przychodzących wiadomości na wbudowanym punktem końcowym (wiadomości/zdarzeń), w milisekundach |
|d2c.Twin.Read.SUCCESS|Pomyślne dwie odczytuje z urządzeń|Licznik|Łącznie|Liczba wszystkich pomyślnych odczyty dwie inicjowanych przez urządzenie.|
|d2c.Twin.Read.failure|Nie powiodło się dwie odczyty z urządzeń|Licznik|Łącznie|Liczba wszystkich nie odczyty dwie inicjowanych przez urządzenie.|
|d2c.Twin.Read.size|Rozmiar odpowiedzi odczytów dwie z urządzeń|Bajty|Średnia|Średnia, min i max z wszystkie udane, inicjowanych przez urządzenie dwie odczytów.|
|d2c.Twin.Update.SUCCESS|Pomyślne dwie aktualizacje z urządzeń|Licznik|Łącznie|Liczba wszystkich pomyślnych aktualizacji dwie inicjowanych przez urządzenie.|
|d2c.Twin.Update.failure|Nie powiodło się dwie aktualizacje z urządzeń|Licznik|Łącznie|Liczba wszystkich nie aktualizacje dwie inicjowanych przez urządzenie.|
|d2c.Twin.Update.size|Rozmiar aktualizacji dwie z urządzeń|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wszystkich pomyślnych, inicjowanych przez urządzenie dwie aktualizacji.|
|c2d.Methods.SUCCESS|Pomyślne bezpośrednie wywołania metod|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań metody bezpośredniego.|
|c2d.Methods.failure|Nie powiodło się bezpośrednie wywołania metod|Licznik|Łącznie|Liczba wszystkich nie wywołania metody bezpośredniego.|
|c2d.Methods.requestSize|Rozmiar żądania bezpośrednie wywołania metod|Bajty|Średnia|Średnia, min i max wszystkich pomyślnych żądań metoda bezpośrednia.|
|c2d.Methods.responseSize|Rozmiar odpowiedzi bezpośrednie wywołania metod|Bajty|Średnia|Średnia, minimum i maksimum wszystkie udane metoda bezpośrednia odpowiedzi.|
|c2d.Twin.Read.SUCCESS|Pomyślne dwie odczytuje z zaplecza|Licznik|Łącznie|Liczba wszystkich pomyślnie zainicjował zakończenia wstecz dwie odczytuje.|
|c2d.Twin.Read.failure|Nie powiodło się dwie odczytuje z zaplecza|Licznik|Łącznie|Liczba wszystkich nie odczyty wstecz zakończenia inicjowane przez dwie.|
|c2d.Twin.Read.size|Rozmiar odpowiedzi odczytów dwie z wewnętrznego|Bajty|Średnia|Średnia, min i max z wszystkie udane, Wstecz zakończenia inicjowane przez dwie odczytów.|
|c2d.Twin.Update.SUCCESS|Pomyślne dwie aktualizacje z wewnętrznego|Licznik|Łącznie|Liczba wszystkich pomyślnych aktualizacji inicjowane zakończenia wstecz dwie.|
|c2d.Twin.Update.failure|Nie powiodło się dwie aktualizacje z wewnętrznego|Licznik|Łącznie|Liczba wszystkich nie powiodło się wstecz zakończenia inicjowane przez dwie aktualizacje.|
|c2d.Twin.Update.size|Rozmiar aktualizacji dwie z wewnętrznego|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wszystkich pomyślnych, Wstecz zakończenia inicjowane przez dwie aktualizacji.|
|twinQueries.success|Dwie pomyślne zapytania|Licznik|Łącznie|Liczba wszystkich zapytań dwie powiodło się.|
|twinQueries.failure|Nie powiodło się dwie zapytań|Licznik|Łącznie|Liczba wszystkich zapytań dwie nie powiodło się.|
|twinQueries.resultSize|Rozmiar wyników zapytania dwie|Bajty|Średnia|Średnia, minimum i maksymalny rozmiar wyników wszystkich zapytań dwie powiodło się.|
|jobs.createTwinUpdateJob.success|Pomyślne utworzenie kont dwie aktualizacji zadań|Licznik|Łącznie|Liczba wszystkich pomyślnym utworzeniu zadania aktualizacji dwie.|
|jobs.createTwinUpdateJob.failure|Nie powiodło się tworzenie dwie aktualizacji zadań|Licznik|Łącznie|Liczba wszystkich nie powiodło się tworzenie zadań aktualizacji dwie.|
|jobs.createDirectMethodJob.success|Pomyślne tworzenia zadań wywołania — metoda|Licznik|Łącznie|Liczba wszystkich pomyślnym utworzeniu zadania wywołania metody bezpośredniego.|
|jobs.createDirectMethodJob.failure|Nie powiodło się tworzenie zadań wywołania — metoda|Licznik|Łącznie|Liczba wszystkich nie powiodło się tworzenie zadań wywołania metody bezpośredniego.|
|jobs.listJobs.success|Pomyślnych wywołań do listy zadań|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań do listy zadań.|
|jobs.listJobs.failure|Nie powiodło się wywołania do listy zadań|Licznik|Łącznie|Liczba zakończonych niepowodzeniem wywołania do listy zadań.|
|jobs.cancelJob.success|Anulowane zadania powiodło się|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań, aby anulować zadanie.|
|jobs.cancelJob.failure|Anulowanie zadania nie powiodło się|Licznik|Łącznie|Liczba wszystkich wywołań nie powiodło się, aby anulować zadanie.|
|jobs.queryJobs.success|Pomyślnie wykonane zadanie zapytań|Licznik|Łącznie|Liczba wszystkich pomyślnych wywołań do zadań zapytania.|
|jobs.queryJobs.failure|Nie powiodło się zadanie odpytuje|Licznik|Łącznie|Liczba wszystkie wywołania zakończone niepowodzeniem zadania zapytania.|
|Jobs.Completed|Zadania ukończone|Licznik|Łącznie|Liczba wszystkich zakończonych zadań.|
|Jobs.failed|Zadania zakończone niepowodzeniem|Licznik|Łącznie|Liczba wszystkie zadania zakończone niepowodzeniem.|
|d2c.telemetry.ingress.sendThrottle|Liczba błędów ograniczania przepustowości|Licznik|Łącznie|Ogranicza liczbę błędów ograniczania przepustowości z powodu przepływności urządzenia|
|dailyMessageQuotaUsed|Całkowita liczba komunikatów używany|Licznik|Średnia|Liczba całkowita liczba komunikatów używany w tej chwili|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|INREQS|Przychodzących żądań wysłania|Licznik|Łącznie|Całkowita liczba przychodzących wysyłać żądania dla Centrum powiadomień|
|SUCCREQ|Liczba pomyślnych żądań|Licznik|Łącznie|Całkowita liczba pomyślnych żądań dla przestrzeni nazw|
|FAILREQ|Żądań zakończonych niepowodzeniem|Licznik|Łącznie|Całkowita liczba żądań zakończonych niepowodzeniem w przypadku przestrzeni nazw|
|SVRBSY|Błędy zajęty serwera|Licznik|Łącznie|Błędy zajęty całego serwera w przypadku przestrzeni nazw|
|INTERR|Błędy wewnętrzne serwera|Licznik|Łącznie|Błędy całkowita wewnętrznego serwera w przypadku przestrzeni nazw|
|MISCERR|Inne błędy|Licznik|Łącznie|Całkowita liczba żądań zakończonych niepowodzeniem w przypadku przestrzeni nazw|
|INMSGS|Przychodzące komunikaty|Licznik|Łącznie|Całkowita liczba komunikatów przychodzących w przypadku przestrzeni nazw|
|OUTMSGS|Wysyła komunikaty wychodzące|Licznik|Łącznie|Całkowita liczba wychodzących wiadomości w przypadku przestrzeni nazw|
|EHINMBS|Przychodzące bajty|Bajty|Łącznie|Zdarzenia koncentratora przychodzącego komunikatu przepływność dla przestrzeni nazw|
|EHOUTMBS|Wychodzące bajty|Bajty|Łącznie|Całkowita liczba wychodzących wiadomości w przypadku przestrzeni nazw|
|EHABL|Archiwum zaległości komunikatów|Licznik|Łącznie|Komunikaty o zdarzeniach Centrum archiwum zaległe dla przestrzeni nazw|
|EHAMSGS|Archiwizowanie komunikatów|Licznik|Łącznie|Centrum zdarzeń zarchiwizowane wiadomości w przestrzeni nazw|
|EHAMBS|Przepływność komunikat archiwum|Bajty|Łącznie|Centrum zdarzeń zarchiwizowane przepływności komunikatu w przestrzeni nazw|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|RunsStarted|Uruchamia uruchomiona|Licznik|Łącznie|Liczba rozpoczętych przebiegów przepływu pracy.|
|RunsCompleted|Zakończonych uruchomień|Licznik|Łącznie|Liczba ukończonych przebiegów przepływu pracy.|
|RunsSucceeded|Uruchamia powiodło się.|Licznik|Łącznie|Liczba przebiegów przepływu pracy zakończonych powodzeniem.|
|RunsFailed|Uruchamia nie powiodło się|Licznik|Łącznie|Liczba przebiegów przepływu pracy zakończonych niepowodzeniem.|
|RunsCancelled|Uruchamia anulowane|Licznik|Łącznie|Liczba anulowanych przebiegów przepływu pracy.|
|RunLatency|Opóźnienia uruchomienia|Sekundy|Średnia|Opóźnienie ukończonych przebiegów przepływu pracy.|
|RunSuccessLatency|Uruchom opóźnienia Powodzenie|Sekundy|Średnia|Opóźnienie przebiegów przepływu pracy zakończonych powodzeniem.|
|RunThrottledEvents|Uruchom z ograniczeniem przepustowości zdarzenia|Licznik|Łącznie|Liczba zdarzeń ograniczenia akcji lub wyzwalacza przepływu pracy.|
|RunFailurePercentage|Uruchom procent awarii|Procent|Łącznie|Procent przepływu pracy jest uruchamiane nie powiodło się.|
|ActionsStarted|Akcje uruchomiona |Licznik|Łącznie|Liczba rozpoczętych akcji przepływu pracy.|
|ActionsCompleted|Działania ukończone |Licznik|Łącznie|Liczba ukończonych akcji przepływu pracy.|
|ActionsSucceeded|Akcje powiodło się. |Licznik|Łącznie|Liczba akcji przepływu pracy zakończonych powodzeniem.|
|ActionsFailed|Akcje nie powiodło się|Licznik|Łącznie|Liczba akcji przepływu pracy zakończonych niepowodzeniem.|
|ActionsSkipped|Akcje pominięty |Licznik|Łącznie|Liczba pominiętych akcji przepływu pracy.|
|ActionLatency|Opóźnienie akcji |Sekundy|Średnia|Opóźnienie ukończonych akcji przepływu pracy.|
|ActionSuccessLatency|Działanie sukces opóźnienia |Sekundy|Średnia|Opóźnienie akcji przepływu pracy zakończonych powodzeniem.|
|ActionThrottledEvents|Akcja ograniczany zdarzenia|Licznik|Łącznie|Liczba zdarzeń ograniczenia akcji przepływu pracy.|
|TriggersStarted|Wyzwalacze uruchomiona |Licznik|Łącznie|Liczba rozpoczętych wyzwalaczy przepływu pracy.|
|TriggersCompleted|Wyzwalacze ukończone |Licznik|Łącznie|Liczba ukończonych wyzwalaczy przepływu pracy.|
|TriggersSucceeded|Wyzwalacze powiodło się. |Licznik|Łącznie|Liczba wyzwalaczy przepływu pracy zakończonych powodzeniem.|
|TriggersFailed|Wyzwalacze nie powiodło się |Licznik|Łącznie|Liczba wyzwalaczy przepływu pracy zakończonych niepowodzeniem.|
|TriggersSkipped|Wyzwalacze pominięty|Licznik|Łącznie|Liczba pominiętych wyzwalaczy przepływu pracy.|
|TriggersFired|Wyzwalacze uruchamiany |Licznik|Łącznie|Liczba uaktywnionych wyzwalaczy przepływu pracy.|
|TriggerLatency|Opóźnienia wyzwalacza |Sekundy|Średnia|Opóźnienie ukończonych wyzwalaczy przepływu pracy.|
|TriggerFireLatency|Wyzwalacz Fire opóźnienia |Sekundy|Średnia|Opóźnienie uaktywnionych wyzwalaczy przepływu pracy.|
|TriggerSuccessLatency|Wyzwalacz Powodzenie opóźnienia |Sekundy|Średnia|Opóźnienie wyzwalaczy przepływu pracy zakończonych powodzeniem.|
|TriggerThrottledEvents|Wyzwalacz ograniczany zdarzenia|Licznik|Łącznie|Liczba zdarzeń ograniczenia wyzwalacza przepływu pracy.|
|BillableActionExecutions|Wykonaniami rozliczeniowy akcji|Licznik|Łącznie|Liczba pobierania rozliczane wykonania akcji przepływu pracy.|
|BillableTriggerExecutions|Wykonaniami rozliczeniowy wyzwalacza|Licznik|Łącznie|Liczba pobierania rozliczane wykonaniami wyzwalacz przepływu pracy.|
|TotalBillableExecutions|Całkowita liczba wykonaniami rozliczeń|Licznik|Łącznie|Liczba pobierania rozliczane wykonania przepływu pracy.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|Przepływność|Przepływność|BytesPerSecond|Średnia||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|BytesIn|BytesIn|Licznik|Łącznie||
|BytesOut|BytesOut|Licznik|Łącznie||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|Registration.all|Operacja rejestracji|Licznik|Łącznie|Liczba wszystkich operacji pomyślną rejestrację (tworzenie zapytań aktualizacji i usunięć). |
|Registration.Create|Operacje tworzenia rejestracji|Licznik|Łącznie|Liczba wszystkich przypadków pomyślną rejestrację.|
|Registration.Update|Operacje aktualizacji rejestracji|Licznik|Łącznie|Liczba wszystkich aktualizacji pomyślną rejestrację.|
|Registration.Get|Operacje odczytu rejestracji|Licznik|Łącznie|Liczba wszystkich zapytań pomyślną rejestrację.|
|Registration.delete|Operacje usuwania rejestracji|Licznik|Łącznie|Liczba wszystkich usunięć pomyślną rejestrację.|
|przychodzące|Przychodzące komunikaty|Licznik|Łącznie|Liczba wszystkich powiodło się wysyłanie wywołań interfejsu API. |
|Incoming.scheduled|Powiadomienia wypychane zaplanowane wysyłane|Licznik|Łącznie|Powiadomienia wypychane zaplanowane anulowane|
|Incoming.scheduled.Cancel|Powiadomienia wypychane zaplanowane anulowane|Licznik|Łącznie|Powiadomienia wypychane zaplanowane anulowane|
|scheduled.Pending|Oczekujące powiadomienia według harmonogramu|Licznik|Łącznie|Oczekujące powiadomienia według harmonogramu|
|Installation.all|Operacje zarządzania instalacji|Licznik|Łącznie|Operacje zarządzania instalacji|
|Installation.Get|Pobierz operacje instalacji|Licznik|Łącznie|Pobierz operacje instalacji|
|Installation.UPSERT|Utwórz lub zaktualizuj operacje instalacji|Licznik|Łącznie|Utwórz lub zaktualizuj operacje instalacji|
|Installation.Patch|Operacje instalacji poprawki|Licznik|Łącznie|Operacje instalacji poprawki|
|Installation.delete|Usuwanie operacji instalacji|Licznik|Łącznie|Usuwanie operacji instalacji|
|Outgoing.allpns.SUCCESS|Powiadomienia o pomyślnym|Licznik|Łącznie|Liczba wszystkich powiadomień powiodło się.|
|Outgoing.allpns.invalidpayload|Błędy ładunku|Licznik|Łącznie|Liczba wypchnięć, których nie powiodła się, ponieważ systemu powiadomień platformy zwrócił błąd zły ładunku.|
|Outgoing.allpns.pnserror|Zewnętrzne powiadomienia błędów systemu|Licznik|Łącznie|Liczba wypchnięć, których nie powiodła się, ponieważ wystąpił problem podczas komunikacji z systemem powiadomień platformy (z wykluczeniem problemom z uwierzytelnianiem).|
|Outgoing.allpns.channelerror|Błędy kanału|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem, ponieważ kanał był nieprawidłowy nie są skojarzone z aplikacją prawidłowe ograniczenie lub wygasła.|
|Outgoing.allpns.badorexpiredchannel|Błędy nieprawidłowych lub wygasłych kanałów|Licznik|Łącznie|Liczba wypycha zakończonych niepowodzeniem z powodu wygasły lub nieprawidłowy kanał/token/registrationId w rejestracji.|
|Outgoing.wns.SUCCESS|Pomyślne powiadomień WNS|Licznik|Łącznie|Liczba wszystkich powiadomień powiodło się.|
|Outgoing.wns.invalidcredentials|Błędy autoryzacji WNS (nieprawidłowe poświadczenia)|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptowała podanych poświadczeń lub poświadczenia są blokowane. (Windows Live nie rozpoznaje poświadczeń).|
|Outgoing.wns.badchannel|Błąd kanału zły WNS|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ ChannelURI w rejestracji nie został rozpoznany (stanu usługi WNS: nie znaleziono 404).|
|Outgoing.wns.expiredchannel|Błąd kanału wygasł WNS|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ wygasł ChannelURI (stan usługi WNS: 410 Gone).|
|Outgoing.wns.throttled|WNS ograniczany powiadomienia|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ usługi WNS jest ograniczanie tej aplikacji (stan usługi WNS: 406 nie do przyjęcia).|
|Outgoing.wns.tokenproviderunreachable|Błędy autoryzacji WNS (nieosiągalne)|Licznik|Łącznie|Windows Live jest nieosiągalny.|
|Outgoing.wns.invalidtoken|Błędy autoryzacji WNS (nieprawidłowy Token)|Licznik|Łącznie|Token dostarczony do usługi WNS jest nieprawidłowy (stan usługi WNS: 401 nieautoryzowane).|
|Outgoing.wns.wrongtoken|Błędy autoryzacji WNS (nieprawidłowy Token)|Licznik|Łącznie|Dostarczony do WNS token jest prawidłowy, ale dla innej aplikacji (stan usługi WNS: 403 Zabroniony). Może to nastąpić, jeśli ChannelURI w rejestracji jest skojarzony z innej aplikacji. Sprawdź, czy aplikacja kliencka jest skojarzony z tą samą aplikacją, którego poświadczenia znajdują się w Centrum powiadomień.|
|Outgoing.wns.invalidnotificationformat|Format nieprawidłowy powiadomień WNS|Licznik|Łącznie|Format powiadomienia jest nieprawidłowy (stan usługi WNS: 400). Należy pamiętać, że usługi WNS nie odrzucić wszystkie ładunki nieprawidłowy.|
|Outgoing.wns.invalidnotificationsize|Błąd nieprawidłowego rozmiaru powiadomienia usługi WNS|Licznik|Łącznie|Ładunek powiadomienia jest za duży (stan usługi WNS: 413).|
|Outgoing.wns.channelthrottled|Ograniczenie kanału usługi WNS|Licznik|Łącznie|Powiadomienia został porzucony, ponieważ jest ograniczany ChannelURI w rejestracji (nagłówek odpowiedzi usługi WNS: X-WNS-NotificationStatus:channelThrottled).|
|Outgoing.wns.channeldisconnected|Kanał WNS odłączona|Licznik|Łącznie|Powiadomienia został porzucony, ponieważ jest ograniczany ChannelURI w rejestracji (nagłówek odpowiedzi usługi WNS: DeviceConnectionStatus-X-WNS: odłączony).|
|Outgoing.wns.dropped|Powiadomienia porzucone WNS|Licznik|Łącznie|Powiadomienia został porzucony, ponieważ jest ograniczany ChannelURI w rejestracji (X-WNS-NotificationStatus: porzucone, ale nie X-WNS-DeviceConnectionStatus: odłączony).|
|Outgoing.wns.pnserror|Błędy WNS|Licznik|Łącznie|Powiadomienie nie są dostarczane z powodu błędów komunikacji z usługą WNS.|
|Outgoing.wns.authenticationerror|Błędy uwierzytelniania usługi WNS|Licznik|Łącznie|Powiadomienie nie są dostarczane z powodu błędów komunikacji z usługi Windows Live nieprawidłowych poświadczeń lub nieprawidłowy token.|
|Outgoing.apns.SUCCESS|Powiadomienia o pomyślnym APNS|Licznik|Łącznie|Liczba wszystkich powiadomień powiodło się.|
|Outgoing.apns.invalidcredentials|Błędy autoryzacji APNS|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptowała podanych poświadczeń lub poświadczenia są blokowane.|
|Outgoing.apns.badchannel|Błąd kanału zły APNS|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ token jest nieprawidłowy (kod stanu APNS: 8).|
|Outgoing.apns.expiredchannel|APNS wygasł błąd kanału|Licznik|Łącznie|Liczba token, który został unieważniony przez kanał opinii APNS.|
|Outgoing.apns.invalidnotificationsize|Błąd nieprawidłowego rozmiaru powiadomienia usługi APNS|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ ładunku jest zbyt duży (kod stanu APNS: 7).|
|Outgoing.apns.pnserror|Błędy APNS|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem z powodu błędów komunikacji z usługą APNS.|
|Outgoing.gcm.SUCCESS|Pomyślne powiadomienia usługi GCM|Licznik|Łącznie|Liczba wszystkich powiadomień powiodło się.|
|Outgoing.gcm.invalidcredentials|Błędy autoryzacji GCM (nieprawidłowe poświadczenia)|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptowała podanych poświadczeń lub poświadczenia są blokowane.|
|Outgoing.gcm.badchannel|Błąd usługi GCM zły kanału|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ registrationId w rejestracji nie został rozpoznany. (wynik GCM: nieprawidłowy rejestracji).|
|Outgoing.gcm.expiredchannel|Błąd kanału wygasł usługi GCM|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ wygasła registrationId w rejestracji (usługi GCM wynik: NotRegistered).|
|Outgoing.gcm.throttled|GCM ograniczany powiadomienia|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ GCM ograniczany tej aplikacji (kod stanu usługi GCM: 501 599 lub wynik: niedostępny).|
|Outgoing.gcm.invalidnotificationformat|Format nieprawidłowy powiadomienia usługi GCM|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ ładunku nie został poprawnie sformatowany. (wynik GCM: InvalidDataKey lub InvalidTtl).|
|Outgoing.gcm.invalidnotificationsize|Błąd nieprawidłowego rozmiaru powiadomienia usługi GCM|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ ładunku jest zbyt duży (wynik GCM: MessageTooBig).|
|Outgoing.gcm.wrongchannel|Błąd usługi GCM niewłaściwego kanału|Licznik|Łącznie|Liczba wypchnięć, których nie powiodła się, ponieważ nie jest skojarzony z bieżącej aplikacji registrationId w rejestracji (usługi GCM wynik: InvalidPackageName).|
|Outgoing.gcm.pnserror|Błędy usługi GCM|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem z powodu błędów komunikacji z usługą GCM.|
|Outgoing.gcm.authenticationerror|Błędy uwierzytelniania usługi GCM|Licznik|Łącznie|Liczba wypchnięć, których nie powiodła się, ponieważ system powiadomień platformy nie akceptuje poświadczeń dostarczonych poświadczeń jest zablokowany lub SenderId nie została poprawnie skonfigurowana w aplikacji (wynik GCM: MismatchedSenderId).|
|Outgoing.mpns.SUCCESS|Powiadomienia o pomyślnym usługi MPNS|Licznik|Łącznie|Liczba wszystkich powiadomień powiodło się.|
|Outgoing.mpns.invalidcredentials|Nieprawidłowe poświadczenia usługi MPNS|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptowała podanych poświadczeń lub poświadczenia są blokowane.|
|Outgoing.mpns.badchannel|Błąd kanału zły usługi MPNS|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ ChannelURI w rejestracji nie został rozpoznany (stan usługi MPNS: nie znaleziono 404).|
|Outgoing.mpns.throttled|Usługi MPNS ograniczany powiadomienia|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ usługi MPNS jest ograniczanie tej aplikacji (WNS MPNS: 406 nie do przyjęcia).|
|Outgoing.mpns.invalidnotificationformat|Format nieprawidłowy powiadomienia usługi MPNS|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem, ponieważ ładunek powiadomienia był za duży.|
|Outgoing.mpns.channeldisconnected|Odłączony kanału usługi MPNS|Licznik|Łącznie|Liczba wypchnięcia, które zakończyły się niepowodzeniem, ponieważ ChannelURI w rejestracji została rozłączona (stan usługi MPNS: nie można odnaleźć 412).|
|Outgoing.mpns.dropped|Usługi MPNS porzucony powiadomienia|Licznik|Łącznie|Liczba wypchnięć, które zostały porzucone przez usługi MPNS (nagłówek odpowiedzi usługi MPNS: X NotificationStatus: Kolejka zapełniona lub Suppressed).|
|Outgoing.mpns.pnserror|Błędy usługi MPNS|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem z powodu błędów komunikacji z usługi MPNS.|
|Outgoing.mpns.authenticationerror|Błędy uwierzytelniania usługi MPNS|Licznik|Łącznie|Liczba wypycha, które zakończyły się niepowodzeniem, ponieważ system powiadomień platformy nie zaakceptowała podanych poświadczeń lub poświadczenia są blokowane.|
|notificationhub.pushes|Wszystkie wychodzące powiadomienia|Licznik|Łącznie|Wszystkie wychodzące powiadomienia w Centrum powiadomień|
|Incoming.all.Requests|Wszystkie żądania przychodzące|Licznik|Łącznie|Całkowita liczba żądań przychodzących do Centrum powiadomień|
|Incoming.all.failedrequests|Wszystkich przychodzących żądań zakończonych niepowodzeniem|Licznik|Łącznie|Całkowita liczba nieudanych żądań przychodzących dla Centrum powiadomień|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|qpu_metric|QPU|Licznik|Średnia|QPU. Zakres 0-100 S1, 0 – 200 S2 i 0-400 dla S4|
|memory_metric|Memory (Pamięć)|Bajty|Średnia|Pamięci. W zakresie 0 – 25 GB na S1, 0 – 50 GB na S2 i 0 – 100 GB dla S4|
|TotalConnectionRequests|Całkowita liczba połączeń żądań|Licznik|Średnia|Całkowita liczba połączeń żądania. Są to przyjęcia.|
|SuccessfullConnectionsPerSec|Udane połączenia na sekundę|CountPerSecond|Średnia|Szybkość zakończeń udane połączenie.|
|TotalConnectionFailures|Całkowita liczba awarii|Licznik|Średnia|Całkowita liczba nieudanych prób połączenia.|
|CurrentUserSessions|Bieżące sesje użytkowników|Licznik|Średnia|Bieżąca liczba ustanowionych sesji użytkownika.|
|QueryPoolBusyThreads|Zapytanie z puli wątków zajęty|Licznik|Średnia|Liczba zajętych wątków w puli wątków zapytania.|
|CommandPoolJobQueueLength|Długość kolejki zadań puli polecenia|Licznik|Średnia|Liczba zadań w kolejce polecenia puli wątków.|
|ProcessingPoolJobQueueLength|Długość kolejki zadań przetwarzania w puli|Licznik|Średnia|Liczba zadań z systemem innym niż — I/O kolejki puli wątków przetwarzania.|
|CurrentConnections|Połączenia: Bieżąca liczba połączeń|Licznik|Średnia|Bieżąca liczba połączeń klienta.|
|CleanerCurrentPrice|Pamięci: Czyszczący bieżąca cena|Licznik|Średnia|Bieżąca cena pamięci $/ byte/godzina znormalizowane do 1000.|
|CleanerMemoryShrinkable|Pamięci: Zmniejszania pamięci czyszczący|Bajty|Średnia|Ilość pamięci w bajtach, mogą ulec czyszcząca przeczyszczanie w tle.|
|CleanerMemoryNonshrinkable|Pamięci: Czyszczący nonshrinkable pamięci|Bajty|Średnia|Ilość pamięci w bajtach, nie może ulec czyszcząca przeczyszczanie w tle.|
|MemoryUsage|Pamięci: Użycie pamięci|Bajty|Średnia|Użycie pamięci przez proces serwera jako używaną przy obliczaniu czyszczący cena pamięci. Taki sam jak licznika Process\PrivateBytes powiększony o rozmiar danych mapowanych na pamięć, ignorując wszystkie pamięci, która została zamapowana lub przydzielone przez aparat analizy w pamięci xVelocity (VertiPaq) przekracza Limit pamięci silnik xVelocity.|
|MemoryLimitHard|Pamięci: Twarde Limit pamięci|Bajty|Średnia|Limit pamięci twardym z pliku konfiguracji.|
|MemoryLimitHigh|Pamięć: Wysoki Limit pamięci|Bajty|Średnia|Limit pamięci wysokiej z pliku konfiguracji.|
|MemoryLimitLow|Pamięci: Niski Limit pamięci|Bajty|Średnia|Limit pamięci z pliku konfiguracji.|
|MemoryLimitVertiPaq|Pamięci: VertiPaq Limit pamięci|Bajty|Średnia|Limit w pamięci z pliku konfiguracji.|
|Przydział|Pamięć: limit przydziału|Bajty|Średnia|Limit przydziału pamięci, w bajtach. Limit przydziału pamięci jest nazywana rezerwacji pamięci grant lub pamięci.|
|QuotaBlocked|Pamięci: Zablokowane przydziału|Licznik|Średnia|Bieżąca liczba żądań przydziału, które są zablokowane, dopóki nie są zwalniane innych przydziałów pamięci.|
|VertiPaqNonpaged|Pamięci: Niestronicowana VertiPaq|Bajty|Średnia|Zablokowane bajtów pamięci zestawu do użycia przez aparat w pamięci roboczego.|
|VertiPaqPaged|Pamięci: Stronicowanej VertiPaq|Bajty|Średnia|Liczba bajtów stronicowanej pamięci dla danych w pamięci.|
|RowsReadPerSec|Przetwarzanie: Wiersze do odczytu na sekundę|CountPerSecond|Średnia|Liczba wierszy odczytywać wszystkie relacyjnych baz danych.|
|RowsConvertedPerSec|Przetwarzanie: Wierszy przekonwertowane na sekundę|CountPerSecond|Średnia|Liczba wierszy przekonwertować podczas przetwarzania.|
|RowsWrittenPerSec|Przetwarzanie: Wierszy, zapisany na sekundę|CountPerSecond|Średnia|Liczba wierszy, zapisany podczas przetwarzania.|
|CommandPoolBusyThreads|Wątki: Polecenie zajęty z puli wątków|Licznik|Średnia|Liczba zajętych wątków w puli wątków polecenia.|
|CommandPoolIdleThreads|Wątków: Polecenie puli wątków bezczynności|Licznik|Średnia|Liczba bezczynności wątków w puli wątków polecenia.|
|LongParsingBusyThreads|Wątków: Podczas analizowania zajęty wątków Long|Licznik|Średnia|Liczba zajętych wątków w puli wątków długo analizy.|
|LongParsingIdleThreads|Wątków: Podczas analizowania bezczynności wątków Long|Licznik|Średnia|Liczba bezczynności wątków w puli wątków długo analizy.|
|LongParsingJobQueueLength|Wątki: Czas analizowania długość kolejki zadań|Licznik|Średnia|Liczba zadań w kolejce długo analizy puli wątków.|
|ProcessingPoolBusyIOJobThreads|Wątki: Przetwarzania puli wątków zajęty zadania we/wy|Licznik|Średnia|Liczba wątków uruchomionych zadań we/wy w puli wątków przetwarzania.|
|ProcessingPoolBusyNonIOThreads|Wątków: Zajęty z puli wątków nie I/O przetwarzania|Licznik|Średnia|Liczba wątków uruchomionych zadań nie I/O w puli wątków przetwarzania.|
|ProcessingPoolIOJobQueueLength|Wątki: Przetwarzanie puli długość kolejki zadania we/wy|Licznik|Średnia|Liczba operacji We/Wy zadań w kolejce puli wątków przetwarzania.|
|ProcessingPoolIdleIOJobThreads|Wątki: Przetwarzania puli wątków bezczynności zadania we/wy|Licznik|Średnia|Liczba wątków bezczynności zadań we/wy w puli wątków przetwarzania.|
|ProcessingPoolIdleNonIOThreads|Wątki: Przetwarzanie bezczynności z puli wątków nie I/E|Licznik|Średnia|Liczba bezczynności wątków w puli wątków przetwarzania dedykowane dla zadań innych niż — I/O.|
|QueryPoolIdleThreads|Wątków: Wątki bezczynności puli zapytania|Licznik|Średnia|Liczba wątków bezczynności zadań we/wy w puli wątków przetwarzania.|
|QueryPoolJobQueueLength|Wątków: Lengt kolejki zadań puli zapytania|Licznik|Średnia|Liczba zadań w kolejce zapytań puli wątków.|
|ShortParsingBusyThreads|Wątków: Podczas analizowania zajęty wątków krótkiej|Licznik|Średnia|Liczba wątków zajęty w krótkim analizy puli wątków.|
|ShortParsingIdleThreads|Wątków: Podczas analizowania bezczynności wątków krótkiej|Licznik|Średnia|Liczba wątków bezczynności w krótkim analizy puli wątków.|
|ShortParsingJobQueueLength|Wątków: Podczas analizowania długość kolejki zadań krótkiej|Licznik|Średnia|Liczba zadań w kolejce krótkich analizy puli wątków.|
|memory_thrashing_metric|Wykonywania niepotrzebnych replik pamięci|Procent|Średnia|Średnia pamięci wykonywania niepotrzebnych replik.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|SearchLatency|Czas oczekiwania wyszukiwania|Sekundy|Średnia|Opóźnienie średni wyszukiwania dla usługi wyszukiwania|
|SearchQueriesPerSecond|Zapytania wyszukiwania na sekundę|CountPerSecond|Średnia|Zapytania wyszukiwania na sekundę dla usługi wyszukiwania|
|ThrottledSearchQueriesPercentage|Procent zapytania wyszukiwania z ograniczeniem przepustowości|Procent|Średnia|Procent zapytania wyszukiwania, które zostały ograniczany usługi wyszukiwania|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|CPUXNS|Użycie procesora CPU na przestrzeń nazw|Procent|Maksymalna|Przestrzeń nazw Procesora użycia metryki dla usługi magistrali — wersja premium|
|WSXNS|Użycie rozmiaru pamięci na przestrzeń nazw|Procent|Maksymalna|Metryki użycia pamięci przestrzeni nazw w premium magistrali usługi|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|cpu_percent|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|
|physical_data_read_percent|Procent użycia operacji we/wy na danych|Procent|Średnia|Procent użycia operacji we/wy na danych|
|log_write_percent|Procent we/wy dziennika|Procent|Średnia|Procent we/wy dziennika|
|dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|
|Magazyn|Rozmiar całkowitą bazy danych|Bajty|Maksymalna|Rozmiar całkowitą bazy danych|
|connection_successful|Udane połączenia|Licznik|Łącznie|Udane połączenia|
|connection_failed|Połączenia nie powiodło się|Licznik|Łącznie|Połączenia nie powiodło się|
|blocked_by_firewall|Blokowane przez zaporę|Licznik|Łącznie|Blokowane przez zaporę|
|Zakleszczenie|Zakleszczenie|Licznik|Łącznie|Zakleszczenie|
|storage_percent|Procent użycia rozmiaru bazy danych|Procent|Maksymalna|Procent użycia rozmiaru bazy danych|
|xtp_storage_percent|Procent magazynu OLTP w pamięci|Procent|Średnia|Procent magazynu OLTP w pamięci|
|workers_percent|Procent pracowników|Procent|Średnia|Procent pracowników|
|sessions_percent|Procent sesji|Procent|Średnia|Procent sesji|
|dtu_limit|Limit jednostek dtu w warstwie|Licznik|Średnia|Limit jednostek dtu w warstwie|
|dtu_used|Jednostek dtu w warstwie używane|Licznik|Średnia|Jednostek dtu w warstwie używane|
|dwu_limit|Jednostka DWU limit|Licznik|Maksymalna|Jednostka DWU limit|
|dwu_consumption_percent|Procent jednostka DWU|Procent|Maksymalna|Procent jednostka DWU|
|dwu_used|Jednostka DWU używane|Licznik|Maksymalna|Jednostka DWU używane|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|cpu_percent|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|
|database_cpu_percent|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|
|physical_data_read_percent|Procent użycia operacji we/wy na danych|Procent|Średnia|Procent użycia operacji we/wy na danych|
|database_physical_data_read_percent|Procent użycia operacji we/wy na danych|Procent|Średnia|Procent użycia operacji we/wy na danych|
|log_write_percent|Procent we/wy dziennika|Procent|Średnia|Procent we/wy dziennika|
|database_log_write_percent|Procent we/wy dziennika|Procent|Średnia|Procent we/wy dziennika|
|dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|
|database_dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|
|storage_percent|Procent użycia magazynu|Procent|Średnia|Procent użycia magazynu|
|workers_percent|Procent pracowników|Procent|Średnia|Procent pracowników|
|database_workers_percent|Procent pracowników|Procent|Średnia|Procent pracowników|
|sessions_percent|Procent sesji|Procent|Średnia|Procent sesji|
|database_sessions_percent|Procent sesji|Procent|Średnia|Procent sesji|
|eDTU_limit|limit liczby jednostek eDTU|Licznik|Średnia|limit liczby jednostek eDTU|
|storage_limit|Limit magazynu|Bajty|Średnia|Limit magazynu|
|eDTU_used|eDTU używane|Licznik|Średnia|eDTU używane|
|storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|
|database_storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|
|xtp_storage_percent|Procent magazynu OLTP w pamięci|Procent|Średnia|Procent magazynu OLTP w pamięci|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|
|database_dtu_consumption_percent|Procent użycia jednostek DTU|Procent|Średnia|Procent użycia jednostek DTU|
|storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|
|database_storage_used|Użyty magazyn|Bajty|Średnia|Użyty magazyn|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|ResourceUtilization|SU % wykorzystania|Procent|Maksymalna|SU % wykorzystania|
|InputEvents|Zdarzenia wejściowe|Licznik|Łącznie|Zdarzenia wejściowe|
|InputEventBytes|Zdarzenie wejściowe w bajtach|Bajty|Łącznie|Zdarzenie wejściowe w bajtach|
|LateInputEvents|Opóźnione zdarzenia wejściowe|Licznik|Łącznie|Opóźnione zdarzenia wejściowe|
|OutputEvents|Dane wyjściowe zdarzenia|Licznik|Łącznie|Dane wyjściowe zdarzenia|
|ConversionErrors|Błędy konwersji danych|Licznik|Łącznie|Błędy konwersji danych|
|Błędy|Błędy środowiska wykonawczego|Licznik|Łącznie|Błędy środowiska wykonawczego|
|DroppedOrAdjustedEvents|Zdarzenia poza kolejnością|Licznik|Łącznie|Zdarzenia poza kolejnością|
|AMLCalloutRequests|Funkcja żądania|Licznik|Łącznie|Funkcja żądania|
|AMLCalloutFailedRequests|Żądania funkcji zakończonych niepowodzeniem|Licznik|Łącznie|Żądania funkcji zakończonych niepowodzeniem|
|AMLCalloutInputEvents|Zdarzenia — funkcja|Licznik|Łącznie|Zdarzenia — funkcja|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|CpuPercentage|Procent użycia procesora CPU|Procent|Średnia|Procent użycia procesora CPU|
|MemoryPercentage|Procent pamięci|Procent|Średnia|Procent pamięci|
|DiskQueueLength|Długość kolejki dysku|Licznik|Łącznie|Długość kolejki dysku|
|HttpQueueLength|Długość kolejki http|Licznik|Łącznie|Długość kolejki http|
|BytesReceived|Dane w|Bajty|Łącznie|Dane w|
|Żądania|Dla danych wychodzących|Bajty|Łącznie|Dla danych wychodzących|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (z wyjątkiem funkcji)

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|CpuTime|Czas procesora CPU|Sekundy|Łącznie|Czas procesora CPU|
|Żądania|Żądania|Licznik|Łącznie|Żądania|
|BytesReceived|Dane w|Bajty|Łącznie|Dane w|
|Żądania|Dla danych wychodzących|Bajty|Łącznie|Dla danych wychodzących|
|Http101|HTTP 101|Licznik|Łącznie|HTTP 101|
|Http2xx|Http 2xx|Licznik|Łącznie|Http 2xx|
|Http3xx|Http 3xx|Licznik|Łącznie|Http 3xx|
|Http401|HTTP 401|Licznik|Łącznie|HTTP 401|
|Http403|HTTP 403|Licznik|Łącznie|HTTP 403|
|Http404|HTTP 404|Licznik|Łącznie|HTTP 404|
|Http406|HTTP 406|Licznik|Łącznie|HTTP 406|
|Http4xx|Http 4xx|Licznik|Łącznie|Http 4xx|
|Http5xx|Błędy HTTP serwera|Licznik|Łącznie|Błędy HTTP serwera|
|MemoryWorkingSet|Zestaw roboczy pamięci|Bajty|Średnia|Zestaw roboczy pamięci|
|AverageMemoryWorkingSet|Pamięć średni zestaw roboczy|Bajty|Średnia|Pamięć średni zestaw roboczy|
|AverageResponseTime|Średni czas odpowiedzi|Sekundy|Średnia|Średni czas odpowiedzi|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (funkcje)

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|BytesReceived|Dane w|Bajty|Łącznie|Dane w|
|Żądania|Dla danych wychodzących|Bajty|Łącznie|Dla danych wychodzących|
|Http5xx|Błędy HTTP serwera|Licznik|Łącznie|Błędy HTTP serwera|
|MemoryWorkingSet|Zestaw roboczy pamięci|Bajty|Średnia|Zestaw roboczy pamięci|
|AverageMemoryWorkingSet|Pamięć średni zestaw roboczy|Bajty|Średnia|Pamięć średni zestaw roboczy|
|FunctionExecutionUnits|Funkcja wykonywania jednostki|Licznik|Średnia|Funkcja wykonywania jednostki|
|FunctionExecutionCount|Liczba wykonań — funkcja|Licznik|Średnia|Liczba wykonań — funkcja|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Metryka|Nazwa wyświetlana metryki|Jednostka|Typ agregacji|Opis|
|---|---|---|---|---|
|CpuTime|Czas procesora CPU|Sekundy|Łącznie|Czas procesora CPU|
|Żądania|Żądania|Licznik|Łącznie|Żądania|
|BytesReceived|Dane w|Bajty|Łącznie|Dane w|
|Żądania|Dla danych wychodzących|Bajty|Łącznie|Dla danych wychodzących|
|Http101|HTTP 101|Licznik|Łącznie|HTTP 101|
|Http2xx|Http 2xx|Licznik|Łącznie|Http 2xx|
|Http3xx|Http 3xx|Licznik|Łącznie|Http 3xx|
|Http401|HTTP 401|Licznik|Łącznie|HTTP 401|
|Http403|HTTP 403|Licznik|Łącznie|HTTP 403|
|Http404|HTTP 404|Licznik|Łącznie|HTTP 404|
|Http406|HTTP 406|Licznik|Łącznie|HTTP 406|
|Http4xx|Http 4xx|Licznik|Łącznie|Http 4xx|
|Http5xx|Błędy HTTP serwera|Licznik|Łącznie|Błędy HTTP serwera|
|MemoryWorkingSet|Zestaw roboczy pamięci|Bajty|Średnia|Zestaw roboczy pamięci|
|AverageMemoryWorkingSet|Pamięć średni zestaw roboczy|Bajty|Średnia|Pamięć średni zestaw roboczy|
|AverageResponseTime|Średni czas odpowiedzi|Sekundy|Średnia|Średni czas odpowiedzi|
|FunctionExecutionUnits|Funkcja wykonywania jednostki|Licznik|Średnia|Funkcja wykonywania jednostki|
|FunctionExecutionCount|Liczba wykonań — funkcja|Licznik|Średnia|Liczba wykonań — funkcja|

## <a name="next-steps"></a>Następne kroki
* [Przeczytaj informacje o metryki w monitorze Azure](monitoring-overview-metrics.md)
* [Utwórz alerty na metryk](insights-receive-alert-notifications.md)
* [Eksportuj metryk do magazynu, Centrum zdarzeń lub analizy dzienników](monitoring-overview-of-diagnostic-logs.md)
