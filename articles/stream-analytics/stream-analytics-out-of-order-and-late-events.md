---
title: "aaaHandling kolejność zdarzeń i opóźnienie z usługą Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej na temat działania usługi analiza strumienia poza kolejnością lub opóźnione zdarzenia w strumieniach danych."
keywords: "zdarzenia poza kolejnością, późne,"
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Obsługa kolejność zdarzeń w usłudze Azure Stream Analytics

W strumieniu danych czasowych zdarzeń każde zdarzenie jest rejestrowane z czasem hello otrzymania tego zdarzenia hello. Niektóre warunki może spowodować strumieni zdarzeń toooccasionally odbierać niektóre zdarzenia w innym porządku niż, które zostały wysłane. Przesłania prosty protokół TCP lub nawet niedokładność zegara między hello wysyłania urządzenia i hello odbieranie Centrum zdarzeń może spowodować, że ten toooccur. "Znaki interpunkcyjne" zdarzenia również są dodawane strumieni zdarzeń tooreceived, tooadvance hello czasu braku hello Przyjazdy zdarzeń. Są potrzebne w scenariuszach, takich jak "Powiadom mnie, jeśli nie logowania dla 3 minuty występują."

Strumienie wejściowe, które nie znajdują się w kolejności są:
* Sortowane (i w związku z tym **opóźnione**).
* Dostosowane przez system hello, zgodnie z tooa zasad określonych przez użytkownika.


## <a name="lateness-tolerance"></a>Opóźnienie tolerancji
Analiza strumienia zaakceptować tego rodzaju scenariusze. Analiza strumienia ma obsługi dla zdarzenia "poza kolejnością" i "późne". Obsługuje on tych zdarzeń w hello następujące sposoby:

* Zdarzenia, które pojawiają się poza kolejnością, ale w ramach hello ustawiona tolerancja są **ponownie uporządkowane według znaczników czasu**.
* Zdarzenia przychodzące później niż uszkodzenia są **porzucone lub dostosowywana**.
    * **Dostosowana**: toohave tooappear skorygowaną dotarły akceptowalnego czasu najnowszych hello.
    * **Porzucone**: odrzucone.

![Obsługa zdarzeń usługi analiza strumienia](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>Zmniejsz liczbę hello zdarzenia poza kolejnością.

Ponieważ Stream Analytics stosuje transformację danych czasowych podczas przetwarzania zdarzenia przychodzącego (na przykład w przypadku agregacjami lub sprzężenia danych czasowych), Stream Analytics sortuje zdarzenia przychodzące według kolejności znaczników czasu.

Gdy jest słowo kluczowe hello "sygnatury czasowej przez" **nie** , czas umieścić w kolejce zdarzenia usługi Azure Event Hubs hello jest używany domyślnie. Centra zdarzeń gwarantuje monotonicity sygnatury czasowej hello na każdej partycji Centrum zdarzeń hello. Gwarantuje również, że zostaną scalone zdarzenia ze wszystkich partycji w kolejności sygnatury czasowej. Upewnij się, te dwie usługi Event Hubs gwarancje żadne zdarzenia poza kolejnością.

Czasami jest ważne w przypadku sygnatury czasowej należy toouse hello nadawcy. W takim przypadku sygnatury czasowej z hello ładunku zdarzenia jest wybierany przy użyciu "sygnatura czasowa przez". W tych scenariuszach może zostać wprowadzony jeden lub więcej źródeł zdarzeń misorder:

* Producenci zdarzeń ma pochyla zegara. Jest to typowe, gdy producentów są z różnych komputerów, więc mają różne zegary.
* Opóźnienie sieci ze źródła hello Centrum zdarzeń hello zdarzenia toohello docelowy nie istnieje.
* Zegar pochyla istnieje między partycji Centrum zdarzeń. Analiza strumienia najpierw sortuje zdarzenia ze wszystkich partycji Centrum zdarzeń przez czas trwania zdarzenia umieścić w kolejce. Następnie bada hello strumień danych zdarzeń w nieprawidłowej kolejności.

Na karcie Konfiguracja hello zobacz temat hello następujące wartości domyślne:

![Obsługa poza kolejnością analiza strumienia](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Jeśli używasz 0 sekund jako hello poza kolejnością tolerancji są potwierdzające, że wszystkie zdarzenia są w kolejności cały czas hello. Podana hello trzech źródeł zdarzeń w nieprawidłowej kolejności, jest mało prawdopodobne, że jest to true. 

toocorrect Stream Analytics tooallow misorder zdarzeń, można określić tolerancji niezerowy poza kolejnością. Stream Analytics buforuje zdarzenia zapasowej toothat okna, a następnie ponowne zamówienia hello nimi przy użyciu sygnatury czasowej, którą wybrano. Następnie stosowane hello przekształcania danych czasowych. Można rozpoczynać okna 3 sekundy i dostrajania hello wartość tooreduce hello liczbę zdarzeń, które są dostosowywane w czasie. 

Efektem ubocznym buforowanie hello jest dane wyjściowe hello **opóźniony o hello sam czas**. Dostosuj hello wartość tooreduce hello liczbą zdarzeń poza kolejnością i zachować opóźnienie zadania hello niski.

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooStream analityka](stream-analytics-introduction.md)
* [Wprowadzenie do usługi analiza strumienia](stream-analytics-real-time-fraud-detection.md)
* [Zadania usługi analiza strumienia skali](stream-analytics-scale-jobs.md)
* [Dokumentacja języka zapytania usługi analiza strumienia](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Strumienia Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)