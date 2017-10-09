---
title: "aaaUnderstanding monitorowania zadania usługi analiza strumienia | Dokumentacja firmy Microsoft"
description: "Opis zadania usługi analiza strumienia monitorowania"
keywords: monitor kwerendy
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Zrozumienie monitorowania zadania usługi analiza strumienia i w jaki sposób toomonitor zapytań

## <a name="introduction-hello-monitor-page"></a>Wprowadzenie: hello monitor strony
Witaj portalu Azure, zarówno powierzchni metryki wydajności, które można toomonitor używane i rozwiązywanie problemów z wydajność zapytań i zadania. toosee tych metryk Przeglądaj zadanie usługi Stream Analytics toohello myślisz zobaczenia metryki i widoku hello **monitorowanie** sekcji na stronie Przegląd hello.  

![Monitorowanie łącza](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

zostanie wyświetlone okno Hello, jak pokazano:

![Monitorowanie zadań pulpitu nawigacyjnego](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Metryki dostępne dla usługi analiza strumienia
| Metryka                 | Definicja                               |
| ---------------------- | ---------------------------------------- |
| SU % wykorzystania       | wykorzystania Hello hello jednostek przesyłania strumieniowego przypisywane zadania tooa kartę Skala hello hello zadania. Jeżeli ten wskaźnik osiągnie 80%, lub powyżej, istnieje wysokie prawdopodobieństwo, czy przetwarzanie zdarzeń może zostać opóźnione lub zatrzymana czyni postępy. |
| Zdarzenia wejściowe           | Ilość danych odebranych przez zadanie usługi Stream Analytics hello, liczbę zdarzeń. Może to być używane toovalidate, że zdarzenia są wysyłane toohello źródło danych wejściowych. |
| Dane wyjściowe zdarzenia          | Ilość danych przesyłanych przez hello analiza strumienia zadania toohello dane wyjściowe obiektu docelowego w liczby zdarzeń. |
| Zdarzenia poza kolejnością.    | Liczba zdarzeń odebranych poza kolejnością, które zostały porzucone lub podane skorygowaną sygnatury czasowej, oparte na powitania zasady kolejność zdarzeń. Może to mieć wpływ hello konfigurację ustawienia porządku poza tolerancji hello. |
| Błędy konwersji danych | Liczba błędów konwersji danych poniesionych przez zadanie usługi Stream Analytics. |
| Błędy środowiska wykonawczego         | Witaj całkowita liczba błędów, które mają miejsce podczas wykonywania zadania usługi analiza strumienia. |
| Opóźnione zdarzenia wejściowe      | Liczba zdarzeń przybywających późne ze źródła hello, który albo została porzucona lub ich sygnatury czasowej została zmieniona na prawidłową, na podstawie konfiguracji zasady kolejność zdarzeń hello hello późne przyjęcia tolerancji ustawienia. |
| Funkcja żądania      | Liczba wywołań toohello funkcji usługi Azure Machine Learning (jeśli istnieje). |
| Żądania funkcji zakończonych niepowodzeniem | Liczba zakończonych niepowodzeniem wywołania funkcji usługi Azure Machine Learning (jeśli istnieje). |
| Zdarzenia — funkcja        | Liczba zdarzeń wysłanych funkcji usługi Azure Machine Learning toohello (jeśli istnieje). |
| Zdarzenie wejściowe w bajtach      | Ilość danych odebranych przez zadanie usługi Stream Analytics hello, w bajtach. Może to być używane toovalidate, że zdarzenia są wysyłane toohello źródło danych wejściowych. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Dostosowywanie monitorowania w hello portalu Azure
Można dopasować hello typ wykresu, metryki wyświetlane i zakres w ustawieniach Edytuj wykres hello czasu. Aby uzyskać więcej informacji, zobacz [jak tooCustomize monitorowanie](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Wykres monitorowania godziny zapytań](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

