---
title: Funkcje okna Analytics tooStream aaaIntroduction | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello trzy funkcje okna w Stream Analytics (wirowania, skaczące, przedłużanie)."
keywords: "Okno przesuwanego okna, Skaczące okno wirowania"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Funkcje okna Analytics tooStream wprowadzenie
W czasie rzeczywistym wiele przesyłania strumieniowego scenariuszy jest konieczne tooperform operacje tylko na powitania dane zawarte w danych czasowych systemu windows. Macierzystą obsługę funkcji okien jest kluczowym elementem usługi Azure Stream Analytics, który przenosi kręci hello na produktywność deweloperów podczas tworzenia złożonych strumienia zadania przetwarzania. Analiza strumienia umożliwia deweloperom toouse [ **wirowania**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) i [ **ruchomej** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform danych czasowych operacje na danych. Warto zauważyć, że wszystkie [okna](https://msdn.microsoft.com/library/dn835019.aspx) operacji output wyników na powitania **zakończenia** hello okna. dane wyjściowe Hello okna hello będzie pojedyncze zdarzenie oparte na funkcji agregującej hello używane. o stałej długości, definiowane są wszystkie funkcje okna i Hello zdarzeń będzie mieć sygnaturę czasową hello hello koniec hello okna. Na koniec jest ważne toonote, które mają być używane wszystkie funkcje okna w [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) klauzuli.

![Pojęcia dotyczące funkcji okno Analiza strumienia](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>Okno wirowania
Funkcje okno wirowania są używane toosegment strumienia danych do czasu odrębnych segmentach i funkcji, takich jak w poniższym przykładzie hello. Hello wyróżniającymi klucza z okno wirowania są, że powtarzają, nie nakładają się i zdarzenia nie może należeć toomore niż jedno okno wirowania.

![Funkcje okna usługi analiza strumienia wirowania wprowadzenie](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>Okno przeskoku
Przeskoku okna funkcji przeskok do przodu w czasie w ustalonym okresie. Łatwe toothink ich jako wirowania systemu windows, które mogą nakładać się na, może być tak zdarzeń mogą należeć toomore niż jeden zestaw wyników okna Hopping. toomake okna Hopping hello takie same jak okno wirowania jeden po prostu określić toobe rozmiar przeskoku hello hello takie same jak hello rozmiar okna. 

![Okno Analiza strumienia funkcje przeskoku wprowadzenie](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>Na metodzie przesuwanego okna
Funkcje przesuwanego okna, w odróżnieniu od wirowania lub skaczące systemu windows, utworzenie danych wyjściowych **tylko** po wystąpieniu zdarzenia. Co okno będzie zawierać co najmniej jedno zdarzenie i okno hello stale przenosi do przodu € (epsilon). Podobnie jak skaczące Windows zdarzenia mogą należeć toomore niż jedno okno przedłużanie.

![Przedłużanie wprowadzenie funkcje okno Analiza strumienia](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Uzyskiwanie pomocy z funkcji okna
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

