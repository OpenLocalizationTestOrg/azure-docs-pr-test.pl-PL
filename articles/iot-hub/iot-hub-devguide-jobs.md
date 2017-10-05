---
title: Zrozumienie zadania Centrum IoT Azure | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — Planowanie zadań do uruchamiania na wielu urządzeniach połączona z Centrum IoT. Zadania można zaktualizować znaczniki i odpowiednie właściwości i wywołania metod bezpośrednio na wielu urządzeniach."
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
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Planowanie zadań na wielu urządzeniach
## <a name="overview"></a>Omówienie
Zgodnie z opisem w poprzedniej artykuły, Centrum IoT Azure umożliwia liczba bloków konstrukcyjnych ([dwie właściwości i urządzenia tagi] [ lnk-twin-devguide] i [bezpośrednie metody] [ lnk-dev-methods]).  Zazwyczaj zaplecza aplikacji Włącz Administratorzy urządzenia i operatory do aktualizacji i interakcji z urządzeń IoT zbiorcze i w zaplanowanym terminie.  Zadania hermetyzować wykonywania aktualizacji dwie urządzenia i metod bezpośrednio pod kątem zestawu urządzeń naraz harmonogramu.  Na przykład operator użyje aplikacji zaplecza, która będzie inicjowania i śledzić zadania ponownego uruchomienia urządzeń z tworzeniem 43 i piętro 3 w czasie, który nie jest znaczący wpływ na operacje budynku.

### <a name="when-to-use"></a>Kiedy stosować
Należy wziąć pod uwagę przy użyciu zadaniach przy: rozwiązanie zaplecza należy zaplanować i śledzić postęp żadnego z następujących czynności na zbiór urządzeń:

* Aktualizowanie żądanych właściwości
* Tagi aktualizacji
* Wywołanie metody bezpośredniego

## <a name="job-lifecycle"></a>Cykl życia zadania
Zadania są inicjowane przez zaplecze rozwiązania i obsługiwanego przez Centrum IoT.  Możesz zainicjować zadania za pomocą identyfikatora URI usługi połączonej (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) i zapytanie o postęp wykonywania zadania za pomocą identyfikatora URI usługi połączonej (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Po zainicjowaniu zadania wykonywania zapytania dotyczącego zadania umożliwia aplikacji zaplecza odświeżyć stan uruchomionych zadań.

> [!NOTE]
> Po zainicjowaniu zadania, nazwy i wartości właściwości mogą zawierać tylko US-ASCII drukowalnych alfanumeryczne, z wyjątkiem tych z następującego zestawu: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Tematy odwołań:
Następujące tematy dokumentacji dostarczają więcej informacji o używaniu zadania.

## <a name="jobs-to-execute-direct-methods"></a>Zadania do wykonania metody bezpośredniego
Poniżej przedstawiono szczegóły żądania protokołu HTTP 1.1 wykonywania [metoda bezpośrednia] [ lnk-dev-methods] na zbiór urządzeń przy użyciu zadania:

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
Warunek kwerendy można też na jednym urządzeniu identyfikator lub na liście identyfikatorów, jak pokazano poniżej urządzenia

**Przykłady**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[Język zapytań Centrum IoT] [ lnk-query] obejmuje język zapytań Centrum IoT w dodatkowych szczegółów.

## <a name="jobs-to-update-device-twin-properties"></a>Zadania, aby zaktualizować urządzenie dwie właściwości
Poniżej przedstawiono szczegóły żądania protokołu HTTP 1.1 aktualizowanie właściwości dwie urządzenia przy użyciu zadania:

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
Poniżej przedstawiono szczegóły żądania protokołu HTTP 1.1 [wykonywania zapytania dotyczącego zadania][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

ContinuationToken jest dostarczany z odpowiedzi.  

## <a name="jobs-properties"></a>Właściwości zadania
Oto lista właściwości wraz z opisami odpowiednie, które mogą być używane podczas wykonywania zapytań dotyczących zadań lub wyniki zadania.

| Właściwość | Opis |
| --- | --- |
| **Identyfikator zadania** |Aplikacja podany identyfikator zadania. |
| **czas rozpoczęcia** |Aplikacja podany czas rozpoczęcia (ISO 8601) dla zadania. |
| **wartość endTime** |Centrum IoT podać datę (ISO 8601) ukończenia zadania. Jest prawidłowy tylko wtedy, gdy zadanie osiągnie stan "ukończone". |
| **Typ** |Typy zadań: |
| **scheduledUpdateTwin**: zadanie używane do aktualizowania zestaw żądaną właściwości bądź tagi. | |
| **scheduledDeviceMethod**: zadanie służy do wywoływania metody urządzenia na zestawie twins urządzenia. | |
| **Stan** |Bieżący stan zadania. Dopuszczalne wartości stanu: |
| **Oczekujące** : Zaplanowane, oczekuje do pobrania przez usługę zadania. | |
| **Zaplanowane** : Zaplanowane na czas w przyszłości. | |
| **uruchomiona** : aktualnie aktywnego zadania. | |
| **Anulowane** : zadanie zostało anulowane. | |
| **nie powiodło się** : zadanie nie powiodło się. | |
| **Ukończono** : zadania zakończone. | |
| **deviceJobStatistics** |Statystyka wykonywania zadania. |

**deviceJobStatistics** właściwości.

| Właściwość | Opis |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Liczba urządzeń w zadaniu. |
| **deviceJobStatistics.failedCount** |Liczba urządzeń, w których zadanie nie powiodło się. |
| **deviceJobStatistics.succeededCount** |Liczba urządzeń, w którym zadanie zakończyło się pomyślnie. |
| **deviceJobStatistics.runningCount** |Liczba urządzeń, które są aktualnie uruchomione zadanie. |
| **deviceJobStatistics.pendingCount** |Liczba urządzeń, które oczekują, aby uruchomić to zadanie. |

### <a name="additional-reference-material"></a>Odwołanie dodatkowe materiały
Inne tematy referencyjne w Podręczniku dewelopera Centrum IoT obejmują:

* [Punkty końcowe Centrum IoT] [ lnk-endpoints] opisano różne punkty końcowe, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.
* [Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziałów, które dotyczą usługi IoT Hub i ograniczania przepustowości zachowania można oczekiwać podczas korzystania z usługi.
* [Azure IoT urządzenia i usługi SDK] [ lnk-sdks] Wyświetla listę różnych zestawów SDK języka należy używany podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.
* [Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości] [ lnk-query] opisuje język zapytań Centrum IoT można pobrać z Centrum IoT informacji o twins urządzenia i zadania.
* [Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zapewnia więcej informacji na temat Centrum IoT obsługi protokołu MQTT.

## <a name="next-steps"></a>Następne kroki
Jeśli chcesz wypróbować niektóre pojęcia opisane w tym artykule, mogą być zainteresowane w następujących instrukcji Centrum IoT:

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
