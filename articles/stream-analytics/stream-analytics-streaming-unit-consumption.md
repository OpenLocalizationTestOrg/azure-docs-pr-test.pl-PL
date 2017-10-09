---
title: "Usługa Azure Stream Analytics: Optymalizacja toouse Twojego zadania jednostki przesyłania strumieniowego wydajnie | Dokumentacja firmy Microsoft"
description: "Zapytanie najlepsze rozwiązania dotyczące skalowania i wydajności w usługi Azure Stream Analytics."
keywords: "Jednostka, wydajność zapytań"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>Optymalizacja wydajnie toouse Twojego zadania jednostki przesyłania strumieniowego

Usługa Azure Stream Analytics agreguje wydajności hello "waga" uruchamiania zadania do jednostek przesyłania strumieniowego (SUs). Usługi SUs reprezentują hello zasobów obliczeniowych, które są wykorzystanych tooexecute zadania. Usługi SUs zapewniają sposób toodescribe hello względną przetwarzania zdarzeń pojemności oparte na mieszanych pomiarach Procesora, pamięci, Odczyt i zapis stawki. Pozwala to wydajność można skupić się na powitania logikę kwerendy i usuwa z konieczności tooknow magazynu warstwy zagadnienia dotyczące wydajności, ręcznie przydzielić pamięci dla zadania, a przybliżona hello Procesora core-liczby potrzebnych toorun zadania w odpowiednim czasie.

## <a name="how-many-sus-are-required-for-a-job"></a>Ile SUs są wymagane w przypadku zadania?

Wybór hello liczba SUs wymagane dla określonego zadania zależy od konfiguracji partycji hello hello dane wejściowe i hello zapytania, który jest zdefiniowany w ramach zadania hello. Witaj **skali** bloku pozwala tooset hello prawo liczba SUs. Jest najlepszym rozwiązaniem tooallocate SUs więcej niż jest to potrzebne. aparat przetwarzania Stream Analytics Hello optymalizuje opóźnienia i przepływności na powitania koszt przydzielania dodatkowych pamięci.

Ogólnie rzecz biorąc, najlepiej hello jest toostart z 6 SUs zapytań, które nie używają *PARTITION BY*. Następnie określ hello słodka miejscu przy użyciu metody prób i błędów, w którym można zmodyfikować hello liczba SUs po przekazać reprezentatywny ilości danych i sprawdź, czy hello SU % wykorzystania metryki.

Usługa Azure Stream Analytics śledzi zdarzenia w oknie o nazwie hello "zmiany kolejności buforu" przed rozpoczęciem jakiegokolwiek przetwarzania. Zdarzenia są sortowane w obrębie okna zmiany kolejności hello czasu, a kolejne operacje są wykonywane na powitania tymczasowo sortowane zdarzenia. Ponowne porządkowanie zdarzenia według czasu zapewnia operatora hello ma dostęp do wszystkich zdarzeń hello w hello określone przedziale czasu. Ponadto pozwala on usłudze operator hello przetwarzania wymagane hello i utworzenie danych wyjściowych. Efektem ubocznym ten mechanizm jest, że przetwarzania jest opóźniony o hello zmiany kolejności przedział czasu hello. zużycie pamięci Hello zadania hello, (co wpływa na zużycie SU) to funkcja hello rozmiaru tej zmiany kolejności okno i hello liczba zdarzeń w nim zawarte.

> [!NOTE]
> Po zmianie podczas uaktualniania zadania hello liczbę czytników przejściowej ostrzeżenia są zapisywane tooaudit dzienniki. Zadania usługi analiza strumienia automatycznie odzyskać te przejściowych problemów.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>Typowe przyczyny wysokiej pamięci wzrost wykorzystania SU dla uruchomionych zadań

### <a name="high-cardinality-for-group-by"></a>Dużej kardynalności Grupuj według

Kardynalność Hello zdarzenia przychodzące nakazują użycie pamięci hello zadania.

Na przykład w `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello numer skojarzony z **klastrowanych** jest Kardynalność hello hello zapytania.

toomitigate problemów, które są spowodowane dużej kardynalności skalowanie w poziomie zapytania hello zwiększając partycje przy użyciu **PARTITION BY**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

Witaj liczba *klastrowanych* jest hello Kardynalność GROUP BY w tym miejscu.

Po zapytania hello jest podzielona na partycje, jego jest rozproszone na wielu węzłach. W związku z tym hello zdarzenia wchodzących w każdym węźle ograniczono liczbę, co z kolei zmniejsza rozmiar hello hello zmiany kolejności buforu. Należy również partycji partycji Centrum zdarzeń według identyfikatora partitionid.

### <a name="high-unmatched-event-count-for-join"></a>Liczba wysokiej niedopasowane zdarzeń w celu utworzenia sprzężenia

Hello liczba zdarzeń niedopasowane sprzężenia wpływa na powitania użycie pamięci przez program hello zapytania. Na przykład wykonać kwerendę, która potrzebuje toofind hello liczba ad wyświetleń generujący kliknięć:

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

W tym scenariuszu jest możliwe, że podano wiele reklam i są generowane kilku kliknięć. Takie wynik wymagają hello zadania tookeep wszystkie zdarzenia hello w hello przedział czasu. Hello ilości pamięci używanej to okno toohello proporcjonalny szybkość rozmiaru i zdarzeń. 

toomitigate takiej sytuacji skalowania w poziomie zapytania hello zwiększając partycje przy użyciu PARTITION BY. 

Po zapytania hello jest podzielona na partycje, jego jest rozproszone na wielu węzłach przetwarzania. W związku z tym hello zdarzenia wchodzących w każdym węźle ograniczono liczbę, co z kolei zmniejsza rozmiar hello hello zmiany kolejności buforu.

### <a name="large-number-of-out-of-order-events"></a>Duża liczba zdarzeń poza kolejnością 

Dużą liczbę zdarzenia poza kolejnością w przedziale czasu dużych powoduje, że rozmiar hello toobe "Zmień kolejność buforu" hello większy. toomitigate takiej sytuacji zapytania hello skali, zwiększając partycje przy użyciu PARTITION BY. Po zapytania hello jest podzielona na partycje, jego jest rozproszone na wielu węzłach. W związku z tym hello zdarzenia wchodzących w każdym węźle ograniczono liczbę, co z kolei zmniejsza rozmiar hello hello zmiany kolejności buforu. 


## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Dokumentacja języka zapytań usługi Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Odwołania API REST zarządzania usługi analiza strumienia Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
