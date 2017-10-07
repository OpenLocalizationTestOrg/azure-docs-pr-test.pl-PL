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
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="a4295-104">Planowanie zadań na wielu urządzeniach</span><span class="sxs-lookup"><span data-stu-id="a4295-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="a4295-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a4295-105">Overview</span></span>
<span data-ttu-id="a4295-106">Zgodnie z opisem w poprzedniej artykuły, Centrum IoT Azure umożliwia liczba bloków konstrukcyjnych ([dwie właściwości i urządzenia tagi] [ lnk-twin-devguide] i [bezpośrednie metody] [ lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="a4295-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="a4295-107">Zazwyczaj zaplecza aplikacji Włącz tooupdate Administratorzy i operatory urządzenia i interakcję z urządzeń IoT zbiorcze i w zaplanowanym terminie.</span><span class="sxs-lookup"><span data-stu-id="a4295-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="a4295-108">Zadania hermetyzować hello wykonywania aktualizacji dwie urządzenia i metod bezpośrednio pod kątem zestawu urządzeń naraz harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="a4295-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="a4295-109">Na przykład operator użyje aplikacji zaplecza, która będzie inicjowania i śledzić zadania tooreboot urządzeń z tworzeniem 43 i piętro 3 w czasie, które nie będą toohello zakłócenie działania budynku hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="a4295-110">Gdy toouse</span><span class="sxs-lookup"><span data-stu-id="a4295-110">When toouse</span></span>
<span data-ttu-id="a4295-111">Należy wziąć pod uwagę przy użyciu zadaniach przy: tooschedule potrzeb zaplecza rozwiązania i Śledź postęp żadnego hello następujące czynności na zbiór urządzeń:</span><span class="sxs-lookup"><span data-stu-id="a4295-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="a4295-112">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="a4295-112">Update desired properties</span></span>
* <span data-ttu-id="a4295-113">Tagi aktualizacji</span><span class="sxs-lookup"><span data-stu-id="a4295-113">Update tags</span></span>
* <span data-ttu-id="a4295-114">Wywołanie metody bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="a4295-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="a4295-115">Cykl życia zadania</span><span class="sxs-lookup"><span data-stu-id="a4295-115">Job lifecycle</span></span>
<span data-ttu-id="a4295-116">Zadania są inicjowane przez zaplecza rozwiązania hello i obsługiwanego przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4295-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="a4295-117">Możesz zainicjować zadania za pomocą identyfikatora URI usługi połączonej (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) i zapytanie o postęp wykonywania zadania za pomocą identyfikatora URI usługi połączonej (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="a4295-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="a4295-118">Po zainicjowaniu zadania wykonywania zapytania dotyczącego zadania umożliwia hello zaplecza aplikacji toorefresh hello stan uruchomionych zadań.</span><span class="sxs-lookup"><span data-stu-id="a4295-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="a4295-119">Po zainicjowaniu zadania, nazwy i wartości właściwości mogą zawierać tylko US-ASCII drukowalnych alfanumeryczne, z wyjątkiem tych w hello następującego zestawu: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="a4295-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="a4295-120">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="a4295-120">Reference topics:</span></span>
<span data-ttu-id="a4295-121">Hello następujące tematy dokumentacji udostępniają więcej informacji o używaniu zadania.</span><span class="sxs-lookup"><span data-stu-id="a4295-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="a4295-122">Metody bezpośredniego tooexecute zadania</span><span class="sxs-lookup"><span data-stu-id="a4295-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="a4295-123">Hello poniżej przedstawiono szczegóły żądania protokołu HTTP 1.1 hello wykonywania [metoda bezpośrednia] [ lnk-dev-methods] na zbiór urządzeń przy użyciu zadania:</span><span class="sxs-lookup"><span data-stu-id="a4295-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="a4295-124">Warunek kwerendy Hello można też na jednym urządzeniu identyfikator lub na liście identyfikatorów urządzenia w sposób przedstawiony poniżej</span><span class="sxs-lookup"><span data-stu-id="a4295-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="a4295-125">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="a4295-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="a4295-126">[Język zapytań Centrum IoT] [ lnk-query] obejmuje język zapytań Centrum IoT w dodatkowych szczegółów.</span><span class="sxs-lookup"><span data-stu-id="a4295-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="a4295-127">Zadania tooupdate urządzenia dwie właściwości</span><span class="sxs-lookup"><span data-stu-id="a4295-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="a4295-128">Aktualizowanie właściwości dwie urządzenia przy użyciu zadania szczegóły żądania hello protokołu HTTP 1.1 jest następujący Hello:</span><span class="sxs-lookup"><span data-stu-id="a4295-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="a4295-129">Wykonanie zapytania dotyczącego postępu zadania</span><span class="sxs-lookup"><span data-stu-id="a4295-129">Querying for progress on jobs</span></span>
<span data-ttu-id="a4295-130">Witaj Oto hello szczegółów żądania protokołu HTTP 1.1 dla [wykonywania zapytania dotyczącego zadania][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="a4295-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="a4295-131">Hello continuationToken jest dostarczany z hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a4295-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="a4295-132">Właściwości zadania</span><span class="sxs-lookup"><span data-stu-id="a4295-132">Jobs Properties</span></span>
<span data-ttu-id="a4295-133">Witaj poniżej przedstawiono listę właściwości i odpowiednie opisy, które mogą być używane podczas wykonywania zapytań dotyczących zadań lub wyniki zadania.</span><span class="sxs-lookup"><span data-stu-id="a4295-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="a4295-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a4295-134">Property</span></span> | <span data-ttu-id="a4295-135">Opis</span><span class="sxs-lookup"><span data-stu-id="a4295-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a4295-136">**Identyfikator zadania**</span><span class="sxs-lookup"><span data-stu-id="a4295-136">**jobId**</span></span> |<span data-ttu-id="a4295-137">Aplikacji podany identyfikator hello zadania.</span><span class="sxs-lookup"><span data-stu-id="a4295-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="a4295-138">**czas rozpoczęcia**</span><span class="sxs-lookup"><span data-stu-id="a4295-138">**startTime**</span></span> |<span data-ttu-id="a4295-139">Godzina rozpoczęcia określonej aplikacji (ISO 8601) dla zadania hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="a4295-140">**wartość endTime**</span><span class="sxs-lookup"><span data-stu-id="a4295-140">**endTime**</span></span> |<span data-ttu-id="a4295-141">Centrum IoT przewidzianych Data (ISO 8601) po ukończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="a4295-142">Jest prawidłowy tylko wtedy, gdy zadanie hello osiągnie stan "ukończona" hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="a4295-143">**Typ**</span><span class="sxs-lookup"><span data-stu-id="a4295-143">**type**</span></span> |<span data-ttu-id="a4295-144">Typy zadań:</span><span class="sxs-lookup"><span data-stu-id="a4295-144">Types of jobs:</span></span> |
| <span data-ttu-id="a4295-145">**scheduledUpdateTwin**: tooupdate zadania używany zestaw żądaną właściwości bądź tagi.</span><span class="sxs-lookup"><span data-stu-id="a4295-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="a4295-146">**scheduledDeviceMethod**: tooinvoke zadania używana metoda urządzenia na zestawie twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a4295-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="a4295-147">**Stan**</span><span class="sxs-lookup"><span data-stu-id="a4295-147">**status**</span></span> |<span data-ttu-id="a4295-148">Bieżący stan zadania hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-148">Current state of hello job.</span></span> <span data-ttu-id="a4295-149">Dopuszczalne wartości stanu:</span><span class="sxs-lookup"><span data-stu-id="a4295-149">Possible values for status:</span></span> |
| <span data-ttu-id="a4295-150">**Oczekujące** : Zaplanowane i toobe oczekiwania pobrania przez hello zadania usługi.</span><span class="sxs-lookup"><span data-stu-id="a4295-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="a4295-151">**Zaplanowane** : Zaplanowane na godzinę w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="a4295-152">**uruchomiona** : aktualnie aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="a4295-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="a4295-153">**Anulowane** : zadanie zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="a4295-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="a4295-154">**nie powiodło się** : zadanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="a4295-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="a4295-155">**Ukończono** : zadania zakończone.</span><span class="sxs-lookup"><span data-stu-id="a4295-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="a4295-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="a4295-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="a4295-157">Statystyka wykonywania hello zadania.</span><span class="sxs-lookup"><span data-stu-id="a4295-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="a4295-158">**deviceJobStatistics** właściwości.</span><span class="sxs-lookup"><span data-stu-id="a4295-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="a4295-159">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a4295-159">Property</span></span> | <span data-ttu-id="a4295-160">Opis</span><span class="sxs-lookup"><span data-stu-id="a4295-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a4295-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="a4295-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="a4295-162">Liczba urządzeń w zadaniu hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="a4295-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="a4295-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="a4295-164">Liczba urządzeń, których hello zadania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="a4295-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="a4295-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="a4295-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="a4295-166">Liczba urządzeń, w którym hello zadanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a4295-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="a4295-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="a4295-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="a4295-168">Liczba urządzeń, które są aktualnie uruchomione zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="a4295-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="a4295-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="a4295-170">Liczba urządzeń, które oczekują na toorun hello zadania.</span><span class="sxs-lookup"><span data-stu-id="a4295-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="a4295-171">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="a4295-171">Additional reference material</span></span>
<span data-ttu-id="a4295-172">Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:</span><span class="sxs-lookup"><span data-stu-id="a4295-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="a4295-173">[Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="a4295-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="a4295-174">[Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello, stosowane toohello usługi IoT Hub, które hello ograniczania tooexpect zachowanie, gdy używasz usługi hello.</span><span class="sxs-lookup"><span data-stu-id="a4295-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="a4295-175">[Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK można używany podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4295-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="a4295-176">[Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości] [ lnk-query] opisuje hello tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4295-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="a4295-177">[Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.</span><span class="sxs-lookup"><span data-stu-id="a4295-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4295-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4295-178">Next steps</span></span>
<span data-ttu-id="a4295-179">Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello samouczka Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="a4295-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="a4295-180">[Zadania harmonogramu i emisji][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="a4295-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
