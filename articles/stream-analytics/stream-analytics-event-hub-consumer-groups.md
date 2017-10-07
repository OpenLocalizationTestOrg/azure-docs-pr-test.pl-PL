---
title: "aaaDebug Azure Stream Analytics z odbiorników Centrum zdarzeń | Dokumentacja firmy Microsoft"
description: "Zapytanie najlepsze rozwiązania dotyczące uwzględnieniu grupy konsumentów centra zdarzeń w zadania usługi analiza strumienia."
keywords: "limit Centrum zdarzeń, grupy odbiorców"
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Debugowanie Azure Stream Analytics przy użyciu odbiorcy Centrum zdarzeń

Można użyć usługi Azure Event Hubs w danych tooingest lub dane wyjściowe z zadania usługi analiza strumienia Azure. Najlepsze rozwiązanie dotyczące korzystania z usługi Event Hubs jest toouse wiele grup odbiorców, tooensure zadania skalowalności. Jedną z przyczyn jest to, że hello liczbę czytników w zadaniu Stream Analytics hello na określone dane wejściowe ma wpływ na powitania liczbę czytników w grupie jednego konsumenta. Hello dokładna liczba odbiorcy jest oparta na szczegóły implementacji wewnętrzny hello logiki topologii skalowalnego w poziomie. numer Hello odbiorników nie był widoczny zewnętrznie. podczas uruchamiania zadania hello lub podczas uaktualniania zadania, można zmienić Hello liczbę czytników.

> [!NOTE]
> Po zmianie podczas uaktualniania zadania hello liczbę czytników przejściowej ostrzeżenia są zapisywane tooaudit dzienniki. Zadania usługi analiza strumienia automatycznie odzyskać te przejściowych problemów.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Liczba czytników dla każdej partycji przekracza limit usługi Event Hubs pięć

Scenariusze, w których hello liczbę czytników dla każdej partycji przekracza limit usługi Event Hubs hello pięć Uwzględnij hello następujące elementy:

* Wiele instrukcji "SELECT": użycie wielu instrukcji SELECT, które odwołują się zbyt**tego samego** wprowadzania Centrum zdarzeń, każda instrukcja SELECT powoduje, że nowe toobe odbiornika utworzony.
* Unia: Użycie Unii, jest możliwe toohave wielu danych wejściowych, które odwołują się toohello **tego samego** grupy koncentratora i odbiorców zdarzeń.
* SAMOSPRZĘŻENIE: Korzystając z operacją JOIN SAMOOBSŁUGOWEGO, jest możliwe toorefer toohello **tego samego** Centrum zdarzeń wiele razy.

## <a name="solution"></a>Rozwiązanie

Witaj następujące najlepsze rozwiązania może pomóc ograniczyć scenariusze, w których hello liczbę czytników dla każdej partycji przekracza limit usługi Event Hubs hello pięć.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>Podziel zapytanie na wielu kroków przy użyciu klauzuli WITH

Klauzula WITH Hello Określa tymczasowy nazwany zestaw wyników, który może odwoływać się klauzuli FROM w kwerendzie hello. Klauzula WITH hello należy zdefiniować w zakresie wykonywania hello jednej instrukcji SELECT.

Na przykład zamiast tego zapytania:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Skorzystaj z tej kwerendy:

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Upewnij się, że dane wejściowe powiązać toodifferent grupy konsumentów

Dla zapytania, w których co najmniej trzech dane wejściowe są połączone toohello konsumenta centra zdarzeń w tej samej grupy, tworzyć grupy konsumentów oddzielne. Wymaga to tworzenie hello dodatkowe usługi analiza strumienia danych wejściowych.


## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooStream analityka](stream-analytics-introduction.md)
* [Wprowadzenie do usługi analiza strumienia](stream-analytics-real-time-fraud-detection.md)
* [Zadania usługi analiza strumienia skali](stream-analytics-scale-jobs.md)
* [Dokumentacja języka zapytania usługi analiza strumienia](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Strumienia Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)
