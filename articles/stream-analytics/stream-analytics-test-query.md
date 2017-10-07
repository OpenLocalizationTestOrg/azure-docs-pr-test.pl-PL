---
title: "Testowanie zapytań usługi Stream Analytics aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak tootest zapytań w zadania usługi analiza strumienia."
keywords: "Testowanie kwerendy, rozwiązywanie problemów z kwerendy"
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a>Testowanie zapytań usługi Azure Stream Analytics w portalu Azure hello

Z usługi Azure Stream Analytics można przetestować zapytań w hello portalu Azure, bez konieczności toostart lub zatrzymać zadanie.

## <a name="test-hello-input"></a>Dane wejściowe hello testu

1. tootest przykładowych danych wejściowych, kliknij prawym przyciskiem myszy dane wejściowe, a następnie wybierz **przekazać dane przykładowe z pliku**.

    ![Edytor testów zapytania zapytań usługi Stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. Po zakończeniu przekazywania powitania kliknij **testu** tootest tego zapytania dotyczącego hello przykładowe dane, które zostały podane.

    ![Edytor testów przykładowych danych zapytań usługi Stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

dane wyjściowe Hello kwerendy jest wyświetlana w przeglądarce hello, łączem wyniki pobierania, powinien ma danych wyjściowych testu hello toosave do późniejszego użycia. Można teraz łatwo i wielokrotnie powtarzane zmodyfikuj zapytanie i przetestować go wielokrotnie toosee jak zmienia hello danych wyjściowych.

![Edytor przykładowe dane wyjściowe zapytań usługi Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

Z wielu wyjść użytych w zapytaniu możesz wyświetlić wyniki hello zarówno dane wyjściowe oddzielnie i łatwo przełączać się między nimi.

Po zakończeniu hello wyniki będą wyświetlane w przeglądarce hello, można zapisać zapytania, uruchom zadanie i pozwolić przetworzyć zdarzenia bez błędów.

## <a name="get-help"></a>Uzyskiwanie pomocy

Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)
