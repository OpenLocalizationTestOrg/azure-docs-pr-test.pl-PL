---
title: zadania Centrum IoT Azure aaaUnderstand | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — Planowanie zadań toorun na wielu urządzeniach połączone tooyour Centrum IoT. Zadania można zaktualizować znaczniki i odpowiednie właściwości i wywołania metod bezpośrednio na wielu urządzeniach."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Planowanie zadań na wielu urządzeniach
## <a name="overview"></a>Omówienie
Zgodnie z opisem w poprzedniej artykuły, Centrum IoT Azure umożliwia liczba bloków konstrukcyjnych ([dwie właściwości i urządzenia tagi] [ lnk-twin-devguide] i [bezpośrednie metody] [ lnk-dev-methods]).  Zazwyczaj zaplecza aplikacji Włącz tooupdate Administratorzy i operatory urządzenia i interakcję z urządzeń IoT zbiorcze i w zaplanowanym terminie.  Zadania hermetyzować hello wykonywania aktualizacji dwie urządzenia i metod bezpośrednio pod kątem zestawu urządzeń naraz harmonogramu.  Na przykład operator użyje aplikacji zaplecza, która będzie inicjowania i śledzić zadania tooreboot urządzeń z tworzeniem 43 i piętro 3 w czasie, które nie będą toohello zakłócenie działania budynku hello.

### <a name="when-toouse"></a>Gdy toouse
Należy wziąć pod uwagę przy użyciu zadaniach przy: tooschedule potrzeb zaplecza rozwiązania i Śledź postęp żadnego hello następujące czynności na zbiór urządzeń:

* Aktualizowanie żądanych właściwości
* Tagi aktualizacji
* Wywołanie metody bezpośredniego

## <a name="job-lifecycle"></a>Cykl życia zadania
Zadania są inicjowane przez zaplecza rozwiązania hello i obsługiwanego przez Centrum IoT.  Możesz zainicjować zadania za pomocą identyfikatora URI usługi połączonej (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) i zapytanie o postęp wykonywania zadania za pomocą identyfikatora URI usługi połączonej (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Po zainicjowaniu zadania wykonywania zapytania dotyczącego zadania umożliwia hello zaplecza aplikacji toorefresh hello stan uruchomionych zadań.

> [!NOTE]
> Po zainicjowaniu zadania, nazwy i wartości właściwości mogą zawierać tylko US-ASCII drukowalnych alfanumeryczne, z wyjątkiem tych w hello następującego zestawu: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Tematy odwołań:
Hello następujące tematy dokumentacji udostępniają więcej informacji o używaniu zadania.

## <a name="jobs-tooexecute-direct-methods"></a>Metody bezpośredniego tooexecute zadania
Hello poniżej przedstawiono szczegóły żądania protokołu HTTP 1.1 hello wykonywania [metoda bezpośrednia] [ lnk-dev-methods] na zbiór urządzeń przy użyciu zadania:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
Warunek kwerendy Hello można też na jednym urządzeniu identyfikator lub na liście identyfikatorów urządzenia w sposób przedstawiony poniżej

**Przykłady**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[Język zapytań Centrum IoT] [ lnk-query] obejmuje język zapytań Centrum IoT w dodatkowych szczegółów.

## <a name="jobs-tooupdate-device-twin-properties"></a>Zadania tooupdate urządzenia dwie właściwości
Aktualizowanie właściwości dwie urządzenia przy użyciu zadania szczegóły żądania hello protokołu HTTP 1.1 jest następujący Hello:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>Wykonanie zapytania dotyczącego postępu zadania
Witaj Oto hello szczegółów żądania protokołu HTTP 1.1 dla [wykonywania zapytania dotyczącego zadania][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

Hello continuationToken jest dostarczany z hello odpowiedzi.  

## <a name="jobs-properties"></a>Właściwości zadania
Witaj poniżej przedstawiono listę właściwości i odpowiednie opisy, które mogą być używane podczas wykonywania zapytań dotyczących zadań lub wyniki zadania.

| Właściwość | Opis |
| --- | --- |
| **Identyfikator zadania** |Aplikacji podany identyfikator hello zadania. |
| **czas rozpoczęcia** |Godzina rozpoczęcia określonej aplikacji (ISO 8601) dla zadania hello. |
| **wartość endTime** |Centrum IoT przewidzianych Data (ISO 8601) po ukończeniu zadania hello. Jest prawidłowy tylko wtedy, gdy zadanie hello osiągnie stan "ukończona" hello. |
| **Typ** |Typy zadań: |
| **scheduledUpdateTwin**: tooupdate zadania używany zestaw żądaną właściwości bądź tagi. | |
| **scheduledDeviceMethod**: tooinvoke zadania używana metoda urządzenia na zestawie twins urządzenia. | |
| **Stan** |Bieżący stan zadania hello. Dopuszczalne wartości stanu: |
| **Oczekujące** : Zaplanowane i toobe oczekiwania pobrania przez hello zadania usługi. | |
| **Zaplanowane** : Zaplanowane na godzinę w przyszłości hello. | |
| **uruchomiona** : aktualnie aktywnego zadania. | |
| **Anulowane** : zadanie zostało anulowane. | |
| **nie powiodło się** : zadanie nie powiodło się. | |
| **Ukończono** : zadania zakończone. | |
| **deviceJobStatistics** |Statystyka wykonywania hello zadania. |

**deviceJobStatistics** właściwości.

| Właściwość | Opis |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Liczba urządzeń w zadaniu hello. |
| **deviceJobStatistics.failedCount** |Liczba urządzeń, których hello zadania nie powiodło się. |
| **deviceJobStatistics.succeededCount** |Liczba urządzeń, w którym hello zadanie zakończyło się pomyślnie. |
| **deviceJobStatistics.runningCount** |Liczba urządzeń, które są aktualnie uruchomione zadanie hello. |
| **deviceJobStatistics.pendingCount** |Liczba urządzeń, które oczekują na toorun hello zadania. |

### <a name="additional-reference-material"></a>Odwołanie dodatkowe materiały
Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:

* [Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.
* [Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello, stosowane toohello usługi IoT Hub, które hello ograniczania tooexpect zachowanie, gdy używasz usługi hello.
* [Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK można używany podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.
* [Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości] [ lnk-query] opisuje hello tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend Centrum IoT.
* [Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.

## <a name="next-steps"></a>Następne kroki
Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello samouczka Centrum IoT:

* [Zadania harmonogramu i emisji][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
