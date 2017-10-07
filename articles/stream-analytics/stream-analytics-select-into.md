---
title: "Azure Stream Analytics aaaDebug zapytania przy użyciu SELECT INTO | Dokumentacja firmy Microsoft"
description: "Przykładowe zapytanie pośredniej danych przy użyciu instrukcji SELECT INTO w analiza strumienia"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>Debugowania zapytania przy użyciu instrukcji SELECT INTO

Podczas przetwarzania danych w czasie rzeczywistym wiedząc, jakie dane hello wygląda w środku hello hello zapytania mogą być pomocne. Ponieważ dane wejściowe lub kroki zadanie usługi analiza strumienia Azure może zostać odczytany wiele razy, można napisać dodatkowy instrukcji SELECT INTO. Dzięki temu generuje pośrednich danych do magazynu i można sprawdzić poprawności hello hello danych, podobnie jak *Obejrzyj zmienne* czy podczas debugowania programu.

## <a name="use-select-into-toocheck-hello-data-stream"></a>Użyj SELECT INTO toocheck hello strumienia danych

Hello następujące przykładowe zapytanie do zadania usługi analiza strumienia Azure ma jednego strumienia danych wejściowych, dwóch parametrów wejściowych danych odwołania, a dane wyjściowe tooAzure magazynu tabel. Zapytanie Hello łączy dane z Centrum zdarzeń hello i dwa obiekty BLOB tooget hello nazwą i kategorią informacje:

![Przykładowe zapytanie SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

Należy pamiętać, że hello zadanie jest uruchomione, ale żadne zdarzenia nie są tworzonym w danych wyjściowych hello. Na powitania **monitorowanie** kafelka, w tym miejscu pokazano widać, że dane wejściowe hello jest zwracające dane, ale nie wiadomo, który krok hello **JOIN** spowodowane hello wszystkie zdarzenia toobe porzucony.

![Kafelek monitorowanie Hello](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
W takiej sytuacji można dodać kilka dodatkowych instrukcji SELECT INTO zbyt "" hello pośrednich wyników sprzężenia i dziennika hello dane, które są odczytywane z danych wejściowych hello.

W tym przykładzie dodano dwa nowe "tymczasowego danych wyjściowych." Mogą to być wszystkie zbiornika, który chcesz. W tym miejscu używamy usługi Azure Storage, na przykład:

![Dodawanie dodatkowych instrukcji SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

Następnie można ponownie napisać zapytanie hello następująco:

![Ponownie zapisane zapytanie SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

Teraz ponownie uruchomić zadanie hello i pozwól mu Uruchom kilka minut. Następnie zbadać temp1 i temp2 za pomocą programu Visual Studio Cloud Explorer tooproduce hello następujących tabel:

**Tabela temp1**
![SELECT INTO tabeli temp1](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**Tabela temp2**
![SELECT INTO tabeli temp2](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

Jak widać, temp1 i temp2 znajdują się dane, a w temp2 hello w kolumnie Nazwa została wpisana poprawnie. Jednak ponieważ nie jeszcze żadnych danych w danych wyjściowych, element jest nieprawidłowy:

![Wybierz do tabeli output1 bez danych](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

Poprzez próbkowanie hello danych, można prawie pewność, że problem hello jest z hello drugie sprzężenia. Można pobrać danych referencyjnych hello z obiektu blob hello i zapoznaj się z:

![Wybierz do tabeli referencyjnej](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

Jak widać, format hello hello identyfikator GUID w tym danych referencyjnych różni się od formatu hello hello [z] kolumny temp2. Dlatego hello danych nie zostało dostarczone w output1 zgodnie z oczekiwaniami.

Można rozwiązać hello format danych, przekaż go tooreference obiektów blob i spróbuj ponownie:

![Wybierz do tabeli tymczasowej](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

Ten czas danych hello w danych wyjściowych hello jest sformatowany i wypełniane zgodnie z oczekiwaniami.

![Wybierz do tabeli końcowej](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>Uzyskiwanie pomocy

Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

