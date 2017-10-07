---
title: "Azure Stream Analytics aaa opartych na danych debugowanie przy użyciu diagramu zadania hello | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z zadania Stream Analytics przy użyciu diagramu zadania hello i metryki."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Oparte na danych debugowanie przy użyciu hello zadania diagramu

diagram zadania Hello na powitania **monitorowanie** bloku w hello portalu Azure może pomóc w potoku zadania sieci wizualizacji. Przedstawia on wejść, wyjść i kroki zapytań. Można użyć hello zadania diagram tooexamine hello metryki dla każdego kroku, toomore możesz szybko znaleźć hello źródła problemu podczas rozwiązywania problemów.

## <a name="using-hello-job-diagram"></a>Przy użyciu hello zadania diagramu

W hello portalu Azure podczas gdy w zadaniu Stream Analytics, w obszarze **pomocy technicznej i rozwiązywania problemów**, wybierz pozycję **diagram zadania**:

![Diagram zadania z metryki - lokalizacji](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Wybierz każdego zapytania krok toosee hello odpowiedniej sekcji w zapytaniu edycji okienka. Wykres metryki dla kroku hello jest wyświetlany w dolnym okienku na stronie powitania.

![Diagram zadania z metryki — podstawowe zadania](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

partycje hello toosee hello Azure Event Hubs danych wejściowych, wybierz **...** Zostanie wyświetlone menu kontekstowego. Można również sprawdzić połączenie wejściowych hello.

![Diagram zadania z metryki - rozwiń partycji](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

toosee hello metryki wykresu dla tylko jednej partycji, wybierz hello węzła partycji. metryki Hello są wyświetlane u dołu hello hello strony.

![Diagram zadania z metryki - więcej metryk](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

toosee hello wykres metryki dotyczące łączenia, wybierz hello fuzji węzła. powitania po wykres pokazuje, że zdarzenia nie zostały porzucone lub dostosowana.

![Diagram zadania z metryki - siatki](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

Szczegóły hello toosee hello wartość metryki i czasu, toohello punkt wykresu.

![Diagram z metryki zadania — wskaźnik myszy](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Rozwiązywanie problemów przy użyciu metryk

Witaj **QueryLastProcessedTime** Metryka wskazuje podczas odbierania danych w określonym kroku. Analizując topologii hello, można pracować wstecz od procesora toosee dane wyjściowe hello, który krok nie odbiera danych. Jeśli krok nie jest pobieranie danych, przejdź kroku zapytania toohello tuż przed. Sprawdź, czy hello poprzedniego kroku zapytania ma przedział czasu i upłynęło dostatecznie dużo czasu na jego toooutput danych. (Uwaga tego czasu systemu windows są godzinę toohello przypięty.)
 
Jeśli hello poprzedniego kroku zapytania wejściowej procesora, użyj hello wejściowych metryki toohelp odpowiedzi hello następujące pytania docelowych. One może pomóc w określeniu, czy zadanie jest pobieranie danych z jego źródeł danych wejściowych. Jeśli zapytanie hello jest podzielona na partycje, sprawdź każdej partycji.
 
### <a name="how-much-data-is-being-read"></a>Trwa odczytywanie ilość danych?

*   **InputEventsSourcesTotal** jest hello liczbę jednostek danych do odczytu. Na przykład hello liczbę obiektów blob.
*   **InputEventsTotal** hello liczba zdarzeń, do odczytu. Ta metryka jest dostępna dla każdej partycji.
*   **InputEventsInBytesTotal** jest hello liczba bajtów odczytanych.
*   **InputEventsLastArrivalTime** został zaktualizowany o czasie umieszczonych w kolejce co otrzymane zdarzenie.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>Czas jest przenoszona do przodu? Jeśli rzeczywiste zdarzenia są odczytywane, znaki interpunkcyjne nie może zostać wygenerowany.

*   **InputEventsLastPunctuationTime** wskazuje, kiedy interpunkcją został wystawiony tookeep czas przenoszenia do przodu. Jeśli nie jest wystawiany znaki interpunkcyjne, mogą zablokowane przepływu danych.
 
### <a name="are-there-any-errors-in-hello-input"></a>Istnieją błędy w danych wejściowych hello?

*   **InputEventsEventDataNullTotal** to liczba zdarzeń, które zawierają dane wartości null.
*   **InputEventsSerializerErrorsTotal** to liczba zdarzeń, które może nie być prawidłowo zdeserializowana.
*   **InputEventsDegradedTotal** to liczba zdarzeń, które wystąpiły problemy innych niż z deserializacji.
 
### <a name="are-events-being-dropped-or-adjusted"></a>Są zdarzenia porzucone lub dostosować?

*   **InputEventsEarlyTotal** hello liczba zdarzeń, których sygnatury czasowej aplikacji przed hello górny limit.
*   **InputEventsLateTotal** hello liczba zdarzeń, których sygnatury czasowej aplikacji po hello górny limit.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** jest hello zdarzenia numer usunięta, zanim godzinę rozpoczęcia zadania hello.
 
### <a name="are-we-falling-behind-in-reading-data"></a>Czy możemy objętych odczytywanie danych?

*   **InputEventsSourcesBackloggedTotal** informuje, ile komunikatów więcej muszą toobe odczytu dla danych wejściowych centra zdarzeń i Azure IoT Hub.


## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooStream analityka](stream-analytics-introduction.md)
* [Wprowadzenie do usługi analiza strumienia](stream-analytics-real-time-fraud-detection.md)
* [Zadania usługi analiza strumienia skali](stream-analytics-scale-jobs.md)
* [Dokumentacja języka zapytania usługi analiza strumienia](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Strumienia Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)
