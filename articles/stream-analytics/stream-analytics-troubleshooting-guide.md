---
title: "Przewodnik aaaTroubleshooting dla usługi Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot zadania usługi analiza strumienia"
keywords: "Rozwiązywanie problemów z przewodnika"
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
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Podręcznik rozwiązywania problemów dotyczących usługi Azure Stream Analytics

Rozwiązywanie problemów z usługi Azure Stream Analytics może występować na pierwszy rzut oka toobe złożonych nakładu pracy. Po zakończeniu pracy z wieloma użytkownikami, możemy utworzono ten przewodnik toohelp usprawnienia hello proces i Usuń czynności hello o wejść, wyjść, kwerendy i funkcje.

## <a name="troubleshoot-your-stream-analytics-job"></a>Rozwiązywanie problemów z zadania usługi analiza strumienia

Aby uzyskać najlepsze wyniki przy rozwiązywaniu zadania usługi analiza strumienia Użyj hello następujące wytyczne:

1.  Przetestuj połączenie:
    - Sprawdź łączność tooinputs i danych wyjściowych za pomocą hello **Testuj połączenie** przycisk dla każdego wejścia i wyjścia.

2.  Sprawdź dane wejściowe:
    - tooverify, że dane wejściowe jest otrzymywanych przez Centrum zdarzeń, użyj [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooAzure tooconnect Centrum zdarzeń (Jeśli dane wejściowe Centrum zdarzeń są używane).  
    - Użyj hello [ **przykładowych danych** ](stream-analytics-sample-data-input.md) przycisk dla każdego danych wejściowych i Pobierz hello wejściowych przykładowych danych.
    - Sprawdź hello kształtu hello toounderstand danych przykładowych danych hello: hello schematu i hello [typy danych](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  Testowanie kwerendy:
    - Na powitania **zapytania** Użyj hello **Test** przycisk tootest hello zapytania i Użyj danych przykładowych hello pobrane za[zapytania hello testu](stream-analytics-test-query.md). Sprawdź błędy i spróbuj toocorrect je.
    - Jeśli używasz [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), sprawdź, czy zdarzenia hello sygnatur czasowych jest większa niż hello [godzina rozpoczęcia zadania](stream-analytics-out-of-order-and-late-events.md).

4.  Debugowanie kwerendy:
    - Odbuduj kwerendy hello stopniowo z prostej instrukcji select toomore złożonych agregacji za pomocą kroków. Użyj toobuild się logikę kwerendy hello krok po kroku [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) klauzul.
    - Użyj [SELECT INTO](stream-analytics-select-into.md) toodebug kroki zapytań.

5.  Eliminowanie typowych problemów, takich jak:
    - A [ **gdzie** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) klauzuli w zapytaniu hello odfiltrowane wszystkie zdarzenia generowane uniemożliwia żadnych danych wyjściowych.
    - Podczas korzystania z funkcji okna, poczekaj na powitania całe okno czasu trwania toosee wyjściem z elementu hello zapytania.
    - Godzina rozpoczęcia zadania hello poprzedza sygnatury czasowej Hello zdarzeń i w związku z tym zdarzeń są usuwane.

6.  Użyj kolejności zdarzeń:
    - Jeśli wszystkie hello poprzednie kroki działał prawidłowo, przejdź toohello **ustawienia** bloku, a następnie wybierz [ **kolejność zdarzeń**](stream-analytics-out-of-order-and-late-events.md). Sprawdź, czy ta zasada jest skonfigurowana do co ma sens w danym scenariuszu. zasada Hello jest *nie* stosowane przy użyciu hello **testu** przycisk tootest hello zapytania. Ten wynik jest jeden różnica między testowania w przeglądarce i uruchomienie zadania hello w środowisku produkcyjnym.

7.  Debugowanie przy użyciu metryk:
    - Jeśli żadne dane wyjściowe można uzyskać po hello oczekiwany czas trwania (na podstawie hello zapytania), spróbuj następujących hello:
        - Przyjrzyj się [ **monitorowania metryki** ](stream-analytics-monitoring.md) na powitania **Monitor** kartę. Ponieważ są agregowane wartości hello, metryki hello opóźnienia za kilka minut.
            - Jeśli zdarzenia wejściowe > 0, zadanie hello jest możliwe tooread danych wejściowych. Jeśli dane wejściowe zdarzeń nie jest > 0, następnie:
                - toosee czy hello źródła danych zawiera prawidłowe dane, sprawdź go za pomocą [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). Ta sprawdzenie jest stosowane Jeśli zadanie hello używa Centrum zdarzeń jako dane wejściowe.
                - Toosee należy sprawdzić, czy format serializacji danych hello i kodowania danych są zgodne z oczekiwaniami.
                - Jeśli zadanie hello używa Centrum zdarzeń, sprawdź toosee czy treść wiadomości powitania hello jest *Null*.
            - Jeśli błędy konwersji danych > 0 i typu hello mogą być spełnione następujące warunki:
                - zadanie Hello może nie być możliwe toode-serializować hello zdarzenia.
                - Witaj schematu zdarzeń mogą być niezgodne hello zdefiniowany lub oczekiwano elementu schema hello zdarzeń w zapytaniu hello.
                - typy danych Hello niektórych pól hello w zdarzeniu hello mogą być niezgodne z oczekiwań.
            - Jeśli błędy podczas wykonywania > 0, oznacza to zadanie hello może odbierać dane hello, ale generuje błędy podczas przetwarzania zapytania hello.
                - toofind hello błędy, przejdź toohello [dzienników inspekcji](../azure-resource-manager/resource-group-audit.md) i odfiltrować ** stanu.
            - Jeśli InputEvents > 0 i OutputEvents = 0, oznacza to, że jest spełniony jeden z następujących hello:
                - W wyniku przetwarzania zapytania nie zostało zwrócone żadne zdarzenie wyjściowe.
                - Zdarzenia lub jego pól może być nieprawidłowo uformowany, w efekcie zero wynik po zakończeniu przetwarzania zapytania.
                - Hello zadanie było toohello danych toopush [ujście danych wyjściowych](stream-analytics-select-into.md) łączności lub uwierzytelnianie przyczyn.
        - Wszystkie hello wcześniej wymienionych w przypadku wystąpienia błędów, operacje komunikaty dziennika opisano dodatkowe szczegóły (w tym działania wykonywane), z wyjątkiem przypadków, w którym logiki kwerendy hello odfiltrowane wszystkich zdarzeń. Jeśli przetwarzanie hello wiele zdarzeń generuje błędy, Stream Analytics dzienniki hello pierwsze trzy komunikaty o błędach z tego samego typu w ciągu 10 minut tooOperations hello rejestruje. Następnie pomija dodatkowe błędy identyczne z następującym komunikatem o treści "Błędy są wykonywane zbyt szybko te są pomijane."

8. Debugowanie przy użyciu inspekcji i dzienniki diagnostyczne:
    - Użyj [dzienników inspekcji](../azure-resource-manager/resource-group-audit.md)i błędy tooidentify i debugowania filtru.
    - Użyj [zadania dzienników diagnostycznych](stream-analytics-job-diagnostic-logs.md) błędów tooidentify i debugowania.

9. Sprawdź dane wyjściowe hello:
    - Gdy stan zadania hello jest *systemem*w oparciu o czas trwania hello, który określono w zapytaniu hello widać danych wyjściowych hello w źródle danych zbiornika hello.
    - Jeśli nie widać danych wyjściowych, które mają typ danych wyjściowych określonych tooa przekierować je tooan typ danych wyjściowych, który jest mniej złożona, takich jak obiektów Blob platformy Azure. Za pomocą Eksploratora usługi Storage, sprawdź toosee, czy dane wyjściowe hello są widoczne. Ponadto należy sprawdzić, czy limity ograniczania przepustowości w danych wyjściowych hello uniemożliwiają danych odbierane.

10. Analiza przepływu danych za pomocą zadania diagram metryki:
    - dane tooanalyze przepływu i zidentyfikować problemy, użyj hello [diagram zadania z metryki](stream-analytics-job-diagram-with-metrics.md).

11. Otwieranie sprawy pomocy technicznej:
    - Na koniec Jeśli wszystkie inne nie powiedzie się, otwórz sprawę pomocy technicznej firmy Microsoft za pomocą hello SubscriptionID, który zawiera zadania.

## <a name="get-help"></a>Uzyskiwanie pomocy

Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)
