---
title: "aaaError & obsługi wyjątków — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wzorce dla błędów i obsługa wyjątków w aplikacjach logiki platformy Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Obsługa błędów i wyjątków w aplikacjach logiki platformy Azure

Aplikacje logiki platformy Azure udostępnia zaawansowane narzędzia i wzorce toohelp możesz upewnij się, że Twoje integracji są niezawodne i podatne na błędy. Wszelkie architektury integracji stanowi wyzwanie hello dokonywania tooappropriately się, że dojście przestój lub problemów z systemów zależnych. Logic Apps ułatwia obsługi błędów najwyższej jakości środowisko, umożliwiając hello narzędzia potrzebne tooact na wyjątków i błędów w swoich przepływach pracy.

## <a name="retry-policies"></a>Spróbuj ponownie zasad

Zasady ponawiania jest hello najbardziej podstawowym typem wyjątku i obsługa błędów. Jeśli upłynął limit czasu żądania początkowego, lub nie powiodło się (każde żądanie, która powoduje 429 lub odpowiedź 5xx), te zasady określa, czy akcja hello powinna ponowić. Domyślnie wszystkie akcje próbę 4 razy dodatkowe za pośrednictwem 20 sekund. Dlatego w przypadku pierwszego żądania hello odbiera `500 Internal Server Error` odpowiedzi, aparatu przepływu pracy hello wstrzymuje 20 sekund i prób hello żądanie ponownie. Jeśli po wszystkich próbach odpowiedź hello jest nadal wyjątku lub awarii, nadal hello przepływu pracy oraz znaczniki hello stanu akcji jako `Failed`.

Można skonfigurować zasady ponawiania w hello **dane wejściowe** dla określonej akcji. Na przykład skonfigurować tootry zasady ponawiania maksymalnie 4 czasy przez 1 godzinę. Aby uzyskać szczegółowe informacje o właściwościach wejściowego, zobacz [działania przepływu pracy i wyzwalaczy][retryPolicyMSDN].

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Jeśli chciał Twojej tooretry akcji HTTP 4 godziny, a następnie odczekaj 10 minut między kolejnymi próbami, należy użyć powitania po definicji:

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

Aby uzyskać więcej informacji o obsługiwanych składni, zobacz hello [części zasady ponawiania akcji przepływu pracy i wyzwalaczy][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>Błędy z hello właściwości RunAfter catch

Każde działanie aplikacji logiki deklaruje akcje, które muszą zostać zakończone przed uruchomieniem akcji hello, takich jak kolejność kroków hello w przepływie pracy. W definicji działania hello, ta kolejność nosi nazwę hello `runAfter` właściwości. Ta właściwość jest obiekt, który opisano, które akcje i stany akcji wykonać hello akcji. Domyślnie wszystkie akcje dodane za pomocą projektanta aplikacji logiki hello są ustawiane za`runAfter` hello poprzedniego kroku, jeśli hello poprzedniego kroku `Succeeded`. Jednak dostosować ten akcje toofire wartość podczas poprzedniej akcji ma `Failed`, `Skipped`, lub zestaw możliwych tych wartości. Jeśli potrzebujesz tooadd tooa elementu wyznaczony tematu usługi Service Bus po określonym działaniu `Insert_Row` kończy się niepowodzeniem, można użyć następującego hello `runAfter` konfiguracji:

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

Powiadomienie hello `runAfter` ustawiono właściwość toofire Jeśli hello `Insert_Row` akcji jest `Failed`. Akcja hello toorun, jeśli jest w stanie akcji hello `Succeeded`, `Failed`, lub `Skipped`, należy użyć następującej składni:

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Akcje, które są uruchomione i pomyślnie zakończone po poprzednim akcja nie powiodła się, są oznaczone jako `Succeeded`. Oznacza to zachowanie, że jeśli możesz pomyślnie catch wszystkich błędów w przepływie pracy, hello uruchamiane samoczynnie jest oznaczone jako `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Akcje tooevaluate zakresy i wyniki

Podobne toohow można uruchomić po poszczególnych działań, można także pogrupować Akcje wewnątrz [zakres](../logic-apps/logic-apps-loops-and-scopes.md), działających jako logiczne grupowanie akcje. Zakresy są przydatne, zarówno do organizowania akcji aplikacji logiki, jak i do wykonywania agregacji oceny stanu hello zakresu. zakres Hello, sama przechodzi w stan po ukończeniu wszystkich działań w zakresie. stan zakresu Hello jest określany hello te same kryteria jak Uruchom. Jeśli akcja końcowego hello w gałęzi wykonywania jest `Failed` lub `Aborted`, jest w stanie hello `Failed`.

toofire określonych akcji dla wszystkich błędów, które wystąpiły w zakresie hello, można użyć `runAfter` z zakresem, który jest oznaczony jako `Failed`. Jeśli *żadnych* akcje w zakresie hello zakończyć się niepowodzeniem, po zakresu zakończy się niepowodzeniem pozwala utworzyć toocatch jednej akcji błędów.

### <a name="getting-hello-context-of-failures-with-results"></a>Uzyskanie kontekstu hello niepowodzeń z wynikami

Mimo że przechwytywanie błędów z zakresu jest przydatne, można także toohelp kontekstu zrozumieć dokładnie akcje, które nie powiodło się, a jakiekolwiek błędy i kodów stanu, które zostały zwrócone. Witaj `@result()` funkcji przepływu pracy zawierają kontekst o wyniku hello wszystkich działań w zakresie.

`@result()`przyjmuje jeden parametr, nazwa zakresu i zwraca tablicę wszystkich wyników akcji hello z tego zakresu. Te obiekty działania obejmują takie same atrybuty jako hello hello `@actions()` generuje obiekt, w tym czas rozpoczęcia działania, czas zakończenia działania stanu akcji, dane wejściowe działań, identyfikatorów korelacji działania i akcji. kontekst toosend wszystkie akcje, które nie powiodło się w zakresie, można łatwo parowania `@result()` działać z `runAfter`.

tooexecute akcji *dla każdego* akcji w zakresie który `Failed`, filtr hello tablicę tooactions wyników zakończonych niepowodzeniem, może łączyć `@result()` z  **[tablicy filtrów](../connectors/connectors-native-query.md)**  akcji i  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  pętli. Możesz pobrać tablica wynikowa filtrowane hello i wykonania czynności dla każdego błędu przy użyciu hello **ForEach** pętli. Oto przykład, a następnie szczegółowy opis, który wysyła żądanie HTTP POST z treści odpowiedzi hello wszystkie akcje, które nie powiodło się w zakresie hello `My_Scope`.

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

Oto toodescribe szczegółowy przewodnik, co się stanie:

1. wynik hello tooget wszystkich akcji w obrębie `My_Scope`, hello **tablicy filtrów** filtry akcji `@result('My_Scope')`.

2. Witaj warunek **tablicy filtrów** dowolnego `@result()` element, który ma stan równa zbyt`Failed`. Ten warunek filtruje hello tablicy o wszystkich wyników akcji z `My_Scope` tablicy tooan tylko z wyników akcji nie powiodło się.

3. Wykonaj **dla każdego** akcji na powitania **filtrowane tablicy** danych wyjściowych. Ten krok wykonuje akcję *dla każdego* nie powiodło się wynik akcji, która wcześniej została przefiltrowana.

    Jeśli jednej akcji w zakresie hello zakończyło się niepowodzeniem, hello akcje w hello `foreach` uruchomić tylko raz. 
    Wiele zakończonych niepowodzeniem akcje mogą spowodować jedną akcję na błąd.

4. Wyślij HTTP POST na powitania `foreach` elementu treści odpowiedzi lub `@item()['outputs']['body']`. Witaj `@result()` kształt element jest sama hello jako hello `@actions()` kształtu i może być analizowana hello sam sposób.

5. Obejmują dwa Nagłówki niestandardowe o nazwie nieudanych akcji hello `@item()['name']` i powitania klienta uruchamiania, identyfikator śledzenia nie powiodło się `@item()['clientTrackingId']`.

Odwołania, Oto przykład jedną `@result()` elementu przedstawiający hello `name`, `body`, i `clientTrackingId` właściwości, które są parsowane w poprzednim przykładzie hello. Poza `foreach`, `@result()` zwraca tablicę tych obiektów.

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

tooperform obsługi wyjątków różne wzorce, można użyć wyrażenia hello przedstawione wcześniej. Może wybrać tooexecute pojedynczego wyjątków, Obsługa akcji poza zakres hello, który akceptuje hello całego tablicy filtrowane niepowodzeń i Usuń hello `foreach`. Możesz również uwzględnić innych przydatnych właściwości hello `@result()` odpowiedzi przedstawione wcześniej.

## <a name="azure-diagnostics-and-telemetry"></a>Diagnostyka Azure i telemetrii

Hello poprzedniej wzorce to doskonały sposób toohandle błędy i wyjątki w Uruchom, ale można również zidentyfikować i odpowiadać tooerrors niezależnie od hello uruchomienia. 
[Diagnostyka Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) zapewnia toosend prosty sposób wszystkie konta magazynu Azure tooan przepływu pracy zdarzenia (w tym wszystkie stany akcji i uruchom) lub usługi Azure Event Hub. tooevaluate Uruchom stany, Monitoruj dzienniki hello i metryki lub publikować je do dowolnego narzędzia monitorowania preferowany. Jedną z opcji potencjalnych jest toostream wszystkie zdarzenia hello za pośrednictwem Centrum zdarzeń Azure do [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). W Stream Analytics można zapisywać zapytania na żywo poza wszelkie nieprawidłowości, średnie lub błędy z hello dzienników diagnostycznych. Analiza strumienia może łatwo output tooother źródeł danych, takich jak kolejki, tematy, SQL, bazy danych rozwiązania Cosmos Azure i usługi Power BI.

## <a name="next-steps"></a>Następne kroki

* [Zobacz, jak klient tworzy błąd obsługi z usługi Azure Logic Apps](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Znajdź więcej Logic Apps przykłady i scenariusze](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Dowiedz się, jak toocreate automatycznego wdrożenia dla aplikacji logiki](../logic-apps/logic-apps-create-deploy-template.md)
* [Tworzenie i wdrażanie aplikacji logiki w programie Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
