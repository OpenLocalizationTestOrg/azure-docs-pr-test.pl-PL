---
title: "Dokumentacja host.JSON dla usługi Azure Functions"
description: "Dokumentacja referencyjna dla pliku host.json usługi Azure Functions."
services: functions
author: tdykstra
manager: cfowler
editor: 
tags: 
keywords: 
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/09/2017
ms.author: tdykstra
ms.openlocfilehash: 522d0590595b0fc0fef503599f1677658f223bd8
ms.sourcegitcommit: cfd1ea99922329b3d5fab26b71ca2882df33f6c2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/30/2017
---
# <a name="hostjson-reference-for-azure-functions"></a>Dokumentacja host.JSON dla usługi Azure Functions

*Host.json* pliku metadanych zawiera opcje konfiguracji globalne, które mają wpływ na wszystkie funkcje dla aplikacji funkcja. W tym artykule wymieniono ustawienia, które są dostępne. Schematu JSON jest na http://json.schemastore.org/host.

Istnieją inne opcje konfiguracji globalnej w [ustawień aplikacji](functions-app-settings.md) i [local.settings.json](functions-run-local.md#local-settings-file) pliku.

## <a name="sample-hostjson-file"></a>Przykładowy plik host.json

Poniższy przykład *host.json* plik zawiera wszystkie opcje określone.

```json
{
    "aggregator": {
        "batchSize": 1000,
        "flushTimeout": "00:00:30"
    },
    "applicationInsights": {
        "sampling": {
          "isEnabled": true,
          "maxTelemetryItemsPerSecond" : 5
        }
    },
    "eventHub": {
      "maxBatchSize": 64,
      "prefetchCount": 256,
      "batchCheckpointFrequency": 1
    },
    "functions": [ "QueueProcessor", "GitHubWebHook" ],
    "functionTimeout": "00:05:00",
    "http": {
        "routePrefix": "api",
        "maxOutstandingRequests": 20,
        "maxConcurrentRequests": 10,
        "dynamicThrottlesEnabled": false
    },
    "id": "9f4ea53c5136457d883d685e57164f08",
    "logger": {
        "categoryFilter": {
            "defaultLevel": "Information",
            "categoryLevels": {
                "Host": "Error",
                "Function": "Error",
                "Host.Aggregator": "Information"
            }
        }
    },
    "queues": {
      "maxPollingInterval": 2000,
      "visibilityTimeout" : "00:00:30",
      "batchSize": 16,
      "maxDequeueCount": 5,
      "newBatchThreshold": 8
    },
    "serviceBus": {
      "maxConcurrentCalls": 16,
      "prefetchCount": 100,
      "autoRenewTimeout": "00:05:00"
    },
    "singleton": {
      "lockPeriod": "00:00:15",
      "listenerLockPeriod": "00:01:00",
      "listenerLockRecoveryPollingInterval": "00:01:00",
      "lockAcquisitionTimeout": "00:01:00",
      "lockAcquisitionPollingInterval": "00:00:03"
    },
    "tracing": {
      "consoleLevel": "verbose",
      "fileLoggingMode": "debugOnly"
    },
    "watchDirectories": [ "Shared" ],
}
```

W poniższych sekcjach tego artykułu opisano poszczególne właściwości najwyższego poziomu. Wszystkie są opcjonalne, o ile nie wskazano inaczej.

## <a name="aggregator"></a>Agregator

Określa, ile wywołania funkcji są agregowane kiedy [obliczanie metryki dla usługi Application Insights](functions-monitoring.md#configure-the-aggregator). 

```json
{
    "aggregator": {
        "batchSize": 1000,
        "flushTimeout": "00:00:30"
    }
}
```

|Właściwość  |Domyślne | Opis |
|---------|---------|---------| 
|batchSize|1000|Maksymalna liczba żądań do zagregowania.| 
|flushTimeout|00:00:30|Maksymalny czas okresu do zagregowania.| 

Wywołania funkcji są agregowane, jeśli pierwszy z dwóch ogranicza osiągnięciu.

## <a name="applicationinsights"></a>applicationInsights

Formanty [funkcji próbkowania w usłudze Application Insights](functions-monitoring.md#configure-sampling).

```json
{
    "applicationInsights": {
        "sampling": {
          "isEnabled": true,
          "maxTelemetryItemsPerSecond" : 5
        }
    }
}
```

|Właściwość  |Domyślne | Opis |
|---------|---------|---------| 
|IsEnabled|fałsz|Włącza lub wyłącza próbkowania.| 
|maxTelemetryItemsPerSecond|5|Rozpoczyna się progu, w których próbkowania.| 

## <a name="eventhub"></a>EventHub

Ustawienia konfiguracji dla [Centrum zdarzeń wyzwalaczy i powiązań](functions-bindings-event-hubs.md).

[!INCLUDE [functions-host-json-event-hubs](../../includes/functions-host-json-event-hubs.md)]

## <a name="functions"></a>funkcje

Lista funkcji, które host zadania zostanie uruchomiony.  Pusta tablica oznacza uruchamiać wszystkie funkcje.  Przeznaczony do użytku tylko wtedy, gdy [uruchomiony lokalnie](functions-run-local.md). W aplikacjach funkcji, należy użyć *function.json* `disabled` właściwości zamiast tej właściwości w *host.json*.

```json
{
    "functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```

## <a name="functiontimeout"></a>functionTimeout

Wskazuje wartość limitu czasu dla wszystkich funkcji. W planie zużycie prawidłowy zakres to od 1 sekundy do 10 minut, a wartość domyślna to 5 minut. W planie usługi aplikacji nie ma żadnego limitu, a wartość domyślna to null, co oznacza brak limitu czasu.

```json
{
    "functionTimeout": "00:05:00"
}
```

## <a name="http"></a>http

Ustawienia konfiguracji dla [http wyzwalaczy i powiązań](functions-bindings-http-webhook.md).

[!INCLUDE [functions-host-json-http](../../includes/functions-host-json-http.md)]

## <a name="id"></a>id

Unikatowy identyfikator dla hosta zadania. Małe litery identyfikatora GUID z kreskami usunięciem. Wymagany w przypadku uruchomionej na komputerze lokalnym. Podczas działania w funkcji platformy Azure, identyfikator jest generowane automatycznie, jeśli `id` zostanie pominięty.

```json
{
    "id": "9f4ea53c5136457d883d685e57164f08"
}
```

## <a name="logger"></a>Rejestratora

Formanty filtrowania dla dzienników napisane przez [obiektu ILogger](functions-monitoring.md#write-logs-in-c-functions) lub [context.log](functions-monitoring.md#write-logs-in-javascript-functions).

```json
{
    "logger": {
        "categoryFilter": {
            "defaultLevel": "Information",
            "categoryLevels": {
                "Host": "Error",
                "Function": "Error",
                "Host.Aggregator": "Information"
            }
        }
    }
}
```

|Właściwość  |Domyślne | Opis |
|---------|---------|---------| 
|categoryFilter|Nie dotyczy|Określa filtrowanie według kategorii| 
|defaultLevel|Informacje|Do kategorii nie została określona w `categoryLevels` tablicy, wysyłaj dzienniki na tym poziomie i w nowszych wersjach do usługi Application Insights.| 
|categoryLevels|Nie dotyczy|Tablica kategorie określa poziom dziennika minimalna do wysłania do usługi Application Insights dla każdej kategorii. Wszystkie kategorie, które zaczynają się taką samą wartość steruje tutaj określonej kategorii i wartości dłużej wyższy priorytet. W poprzednim przykładzie *host.json* pliku, wszystkie kategorie, które zaczynają się od "Host.Aggregator" dziennika w `Information` poziom. Wszystkie kategorie, które zaczynają się od "Host", takie jak "Host.Executor", zaloguj się na `Error` poziom.| 

## <a name="queues"></a>Kolejki

Ustawienia konfiguracji dla [magazynu kolejki wyzwalaczy i powiązań](functions-bindings-storage-queue.md).

```json
{
    "queues": {
      "maxPollingInterval": 2000,
      "visibilityTimeout" : "00:00:30",
      "batchSize": 16,
      "maxDequeueCount": 5,
      "newBatchThreshold": 8
    }
}
```

|Właściwość  |Domyślne | Opis |
|---------|---------|---------| 
|maxPollingInterval|60000|Maksymalny interwał w milisekundach między sond kolejki.| 
|visibilityTimeout|0|Przedział czasu między kolejnymi próbami podczas przetwarzania komunikatu nie powiedzie się.| 
|batchSize|16|Liczba wiadomości w kolejce do pobrania i przetwarzanie równoległe. Wartość maksymalna to 32.| 
|maxDequeueCount|5|Liczba prób przetwarzania przed jego przeniesieniem do skażone kolejki wiadomości.| 
|newBatchThreshold|batchSize/2|Próg pobrane nową partię komunikatów.| 

## <a name="servicebus"></a>Magistrali usług

Ustawienia konfiguracji dla [usługi Service Bus wyzwalaczy i powiązań](functions-bindings-service-bus.md).

[!INCLUDE [functions-host-json-service-bus](../../includes/functions-host-json-service-bus.md)]

## <a name="singleton"></a>pojedyncze

Ustawienia konfiguracji dla pojedynczych blokady zachowanie. Aby uzyskać więcej informacji, zobacz [GitHub problem o obsłudze singleton](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```json
    "singleton": {
      "lockPeriod": "00:00:15",
      "listenerLockPeriod": "00:01:00",
      "listenerLockRecoveryPollingInterval": "00:01:00",
      "lockAcquisitionTimeout": "00:01:00",
      "lockAcquisitionPollingInterval": "00:00:03"
    }
}
```

|Właściwość  |Domyślne | Opis |
|---------|---------|---------| 
|lockPeriod|00:00:15|Funkcja poziomu blokady są pobierane dla okresu. Blokad automatyczne odnawianie.| 
|listenerLockPeriod|00:01:00|Odbiornik blokady są pobierane dla okresu.| 
|listenerLockRecoveryPollingInterval|00:01:00|Interwał użyty do odzyskiwania blokady odbiornika, jeśli nie można uzyskać blokady odbiornika podczas uruchamiania.| 
|lockAcquisitionTimeout|00:01:00|Maksymalna ilość czasu środowiska uruchomieniowego podejmie próbę uzyskania blokady.| 
|lockAcquisitionPollingInterval|Nie dotyczy|Interwał między próbami przejęcie blokady.| 

## <a name="tracing"></a>Śledzenie

Ustawienia konfiguracji dla dzienników, które utworzono za pomocą `TraceWriter` obiektu. Zobacz [C# rejestrowania](functions-reference-csharp.md#logging) i [rejestrowania Node.js](functions-reference-node.md#writing-trace-output-to-the-console). 

```json
{
    "tracing": {
      "consoleLevel": "verbose",
      "fileLoggingMode": "debugOnly"
    }
}
```

|Właściwość  |Domyślne | Opis |
|---------|---------|---------| 
|consoleLevel|Informacje o|Poziom śledzenia dla konsoli rejestrowania. Opcje to: `off`, `error`, `warning`, `info`, i `verbose`.|
|fileLoggingMode|debugOnly|Poziom śledzenia dla rejestrowania w pliku. Opcje są `never`, `always`, `debugOnly`.| 

## <a name="watchdirectories"></a>watchDirectories

Zestaw [udostępnionych katalogów kodu](functions-reference-csharp.md#watched-directories) powinny być monitorowane zmian.  Zapewnia, że zmiana kodu w tych katalogach zmiany są pobierane przez funkcji.

```json
{
    "watchDirectories": [ "Shared" ]
}
```

## <a name="durabletask"></a>durableTask

[Zadanie Centrum](durable-functions-task-hubs.md) nazwę [trwałe funkcji](durable-functions-overview.md).

```json
{
  "durableTask": {
    "HubName": "MyTaskHub"
  }
}
```

Nazwy Centrum dla zadań musi zaczynać się literą i zawierać tylko litery i cyfry. Jeśli nie zostanie określony, jest domyślną nazwę koncentratora zadań dla aplikacji funkcja **DurableFunctionsHub**. Aby uzyskać więcej informacji, zobacz [zadań koncentratory](durable-functions-task-hubs.md).


## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dowiedz się, jak zaktualizować pliku host.json](functions-reference.md#fileupdate)

> [!div class="nextstepaction"]
> [Zobacz ustawienia globalne w zmiennych środowiskowych](functions-app-settings.md)
