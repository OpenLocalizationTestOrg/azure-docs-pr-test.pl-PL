---
title: "dane wejściowe próbkowania aaa Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Identyfikowanie problemów podczas rozwiązywania zadania usługi analiza strumienia."
keywords: "Rozwiązywanie problemów z wejściowych, wejściowych próbkowania"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Azure Stream Analytics strumienia danych wejściowych próbkowania

Za pomocą usługi Azure Stream Analytics, możesz przykładowe zdarzenia wejściowe, które pochodzą z pliku i testowanie zapytań w portalu hello bez konieczności toostart lub zatrzymać zadanie.

## <a name="testing-your-query"></a>Testowanie kwerendy

W okienku szczegółów zadania usługi analiza strumienia hello Otwórz hello **edytora zapytań** bloku, klikając nazwę zapytania hello w obszarze **zapytania**. (W naszym przykładowym scenariuszu, ponieważ bez określenia zapytania nie utworzono jeszcze, kliknij przycisk hello **< >** symbolu zastępczego.)

![Edytor zapytań usługi Stream Analytics Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

jak w poprzedniej wersji hello, zostanie wyświetlony Hello bloku Zaawansowany edytor do tworzenia zapytania. Teraz bloku hello zostały zaktualizowane o nową lewe okienko ten przedstawia hello wejściach i wyjściach, używany przez zapytanie hello i zdefiniowanych dla tego zadania.

![Edytor zapytań usługi Stream Analytics Hello danych wejściowych i wyprowadza list](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

Także wyświetlane są dodatkowe dane wejściowe i wyjściowe, które nie zostały zdefiniowane. Pochodzą z hello nowego zapytania szablonu rozpoczynających się od. Zmień lub nawet niewidoczny, edycji hello zapytania. Można bezpiecznie zignorować je teraz.

tootest przykładowych danych wejściowych, kliknij prawym przyciskiem myszy dane wejściowe, a następnie wybierz **przekazać dane przykładowe z pliku**.

![Witaj Stream Analytics query Edytor przekazywania przykładowych danych z plik — polecenie](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Po zakończeniu przekazywania powitania kliknij **testu** tootest tego zapytania dotyczącego hello przykładowe dane, które zostały podane.

![przycisk Test edytora zapytań usługi Stream Analytics Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

Jeśli chcesz danych wyjściowych testu hello toosave do późniejszego użycia, dane wyjściowe hello kwerendy jest wyświetlana w przeglądarce hello z łącza toohello pobierania wyników. Można teraz łatwo i wielokrotnie powtarzane zmodyfikuj zapytanie i przetestować go wielokrotnie toosee jak zmienia hello danych wyjściowych.

![Edytor przykładowe dane wyjściowe zapytań usługi Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

W hello poprzedzających obrazu, został dodany drugi dane wyjściowe, nazywany **HighAvgTempOutput**.

Użycie wielu wyjść w zapytaniu, możesz wyświetlić hello wyników dla każdego danych wyjściowych oddzielnie i łatwo przełączać się między nimi.

Po zakończeniu hello wyników można zapisać kwerendę, uruchom zadanie, zaczekaj i obejrzyj magic hello usługi Stream Analytics.

## <a name="get-help"></a>Uzyskiwanie pomocy

Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)
