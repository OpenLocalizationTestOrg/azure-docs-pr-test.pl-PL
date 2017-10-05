---
title: "Obsługa kolejność zdarzeń i opóźnienie z usługą Azure Stream Analytics | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a48e48c5fc65d0ffbb7c23f426a4b06dcd568821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Obsługa kolejność zdarzeń w usłudze Azure Stream Analytics

Każdego zdarzenia jest zarejestrowany w strumieniu danych czasowych zdarzenia, czas odebrania zdarzenia. Niektóre warunki może spowodować strumieni zdarzeń do od czasu do czasu otrzymania niektóre zdarzenia w innym porządku niż, które zostały wysłane. Proste retransmisji TCP lub nawet przesunięcia czasowego zegara między urządzeniem wysyłania i odbierania Centrum zdarzeń może spowodować to możliwe. "Znaki interpunkcyjne" zdarzenia również są dodawane do strumieni zdarzeń odebranych, można poprawić czasu braku Przyjazdy zdarzeń. Są potrzebne w scenariuszach, takich jak "Powiadom mnie, jeśli nie logowania dla 3 minuty występują."

Strumienie wejściowe, które nie znajdują się w kolejności są:
* Sortowane (i w związku z tym **opóźnione**).
* Dostosowane przez system, zgodnie z zasadami określonymi przez użytkownika.


## <a name="lateness-tolerance"></a>Opóźnienie tolerancji
Analiza strumienia zaakceptować tego rodzaju scenariusze. Analiza strumienia ma obsługi dla zdarzenia "poza kolejnością" i "późne". Obsługuje on tych zdarzeń w następujący sposób:

* Zdarzenia przychodzące poza kolejnością, ale w granicach tolerancji zestawu są **ponownie uporządkowane według znaczników czasu**.
* Zdarzenia przychodzące później niż uszkodzenia są **porzucone lub dostosowywana**.
    * **Dostosowana**: dostosowana do wydają się przybyły najnowszych akceptowalnego czasu.
    * **Porzucone**: odrzucone.

![Obsługa zdarzeń usługi analiza strumienia](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-the-number-of-out-of-order-events"></a>Zmniejsz liczbę zdarzeń poza kolejnością.

Ponieważ Stream Analytics stosuje transformację danych czasowych podczas przetwarzania zdarzenia przychodzącego (na przykład w przypadku agregacjami lub sprzężenia danych czasowych), Stream Analytics sortuje zdarzenia przychodzące według kolejności znaczników czasu.

Gdy jest słowo kluczowe "sygnatury czasowej przez" **nie** , czas umieścić w kolejce zdarzeń usługi Azure Event Hubs jest używany domyślnie. Centra zdarzeń gwarantuje monotonicity znacznika czasu na każdej partycji Centrum zdarzeń. Gwarantuje również, że zostaną scalone zdarzenia ze wszystkich partycji w kolejności sygnatury czasowej. Upewnij się, te dwie usługi Event Hubs gwarancje żadne zdarzenia poza kolejnością.

Czasami jest ważne w przypadku użycia sygnatury czasowej nadawcy. W takim przypadku sygnatury czasowej z ładunku zdarzenia jest wybierany przy użyciu "sygnatura czasowa przez". W tych scenariuszach może zostać wprowadzony jeden lub więcej źródeł zdarzeń misorder:

* Producenci zdarzeń ma pochyla zegara. Jest to typowe, gdy producentów są z różnych komputerów, więc mają różne zegary.
* Opóźnienie sieci ze źródła zdarzeń do Centrum zdarzeń docelowy nie istnieje.
* Zegar pochyla istnieje między partycji Centrum zdarzeń. Analiza strumienia najpierw sortuje zdarzenia ze wszystkich partycji Centrum zdarzeń przez czas trwania zdarzenia umieścić w kolejce. Następnie to sprawdza, czy strumień danych zdarzeń w nieprawidłowej kolejności.

Na karcie Konfiguracja pojawić następujące wartości domyślne:

![Obsługa poza kolejnością analiza strumienia](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Jeśli używasz 0 sekund jako poza kolejnością tolerancji, są potwierdzające, że wszystkie zdarzenia są w kolejności cały czas. Biorąc pod uwagę trzech źródeł w nieprawidłowej kolejności zdarzeń, jest mało prawdopodobne, że jest to wartość true. 

Aby umożliwić Stream Analytics poprawić misorder zdarzeń, można określić tolerancji niezerowy poza kolejnością. Analiza strumienia buforuje zdarzenia do tego okna, a następnie zmienia kolejność ich przy użyciu sygnatury czasowej, wybrana. Następnie ma to zastosowanie transformacji danych czasowych. Można rozpoczynać okna 3 sekundy i dostosować wartość, aby zmniejszyć liczbę zdarzeń, które są dostosowywane w czasie. 

Efektem ubocznym buforowania jest dane wyjściowe **opóźniony o tej samej ilość czasu**. Można dostosować wartość, aby zmniejszyć liczbę zdarzeń poza kolejnością i Zachowaj Niskie opóźnienie zadania.

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do usługi analiza strumienia](stream-analytics-introduction.md)
* [Wprowadzenie do usługi analiza strumienia](stream-analytics-real-time-fraud-detection.md)
* [Zadania usługi analiza strumienia skali](stream-analytics-scale-jobs.md)
* [Dokumentacja języka zapytania usługi analiza strumienia](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Strumienia Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)