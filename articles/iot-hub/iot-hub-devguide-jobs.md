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
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="abfc6-104">Planowanie zadań na wielu urządzeniach</span><span class="sxs-lookup"><span data-stu-id="abfc6-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="abfc6-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="abfc6-105">Overview</span></span>
<span data-ttu-id="abfc6-106">Zgodnie z opisem w poprzedniej artykuły, Centrum IoT Azure umożliwia liczba bloków konstrukcyjnych ([dwie właściwości i urządzenia tagi] [ lnk-twin-devguide] i [bezpośrednie metody] [ lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="abfc6-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="abfc6-107">Zazwyczaj zaplecza aplikacji Włącz Administratorzy urządzenia i operatory do aktualizacji i interakcji z urządzeń IoT zbiorcze i w zaplanowanym terminie.</span><span class="sxs-lookup"><span data-stu-id="abfc6-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="abfc6-108">Zadania hermetyzować wykonywania aktualizacji dwie urządzenia i metod bezpośrednio pod kątem zestawu urządzeń naraz harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="abfc6-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="abfc6-109">Na przykład operator użyje aplikacji zaplecza, która będzie inicjowania i śledzić zadania ponownego uruchomienia urządzeń z tworzeniem 43 i piętro 3 w czasie, który nie jest znaczący wpływ na operacje budynku.</span><span class="sxs-lookup"><span data-stu-id="abfc6-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="abfc6-110">Kiedy stosować</span><span class="sxs-lookup"><span data-stu-id="abfc6-110">When to use</span></span>
<span data-ttu-id="abfc6-111">Należy wziąć pod uwagę przy użyciu zadaniach przy: rozwiązanie zaplecza należy zaplanować i śledzić postęp żadnego z następujących czynności na zbiór urządzeń:</span><span class="sxs-lookup"><span data-stu-id="abfc6-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="abfc6-112">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="abfc6-112">Update desired properties</span></span>
* <span data-ttu-id="abfc6-113">Tagi aktualizacji</span><span class="sxs-lookup"><span data-stu-id="abfc6-113">Update tags</span></span>
* <span data-ttu-id="abfc6-114">Wywołanie metody bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="abfc6-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="abfc6-115">Cykl życia zadania</span><span class="sxs-lookup"><span data-stu-id="abfc6-115">Job lifecycle</span></span>
<span data-ttu-id="abfc6-116">Zadania są inicjowane przez zaplecze rozwiązania i obsługiwanego przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="abfc6-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="abfc6-117">Możesz zainicjować zadania za pomocą identyfikatora URI usługi połączonej (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) i zapytanie o postęp wykonywania zadania za pomocą identyfikatora URI usługi połączonej (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="abfc6-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="abfc6-118">Po zainicjowaniu zadania wykonywania zapytania dotyczącego zadania umożliwia aplikacji zaplecza odświeżyć stan uruchomionych zadań.</span><span class="sxs-lookup"><span data-stu-id="abfc6-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="abfc6-119">Po zainicjowaniu zadania, nazwy i wartości właściwości mogą zawierać tylko US-ASCII drukowalnych alfanumeryczne, z wyjątkiem tych z następującego zestawu: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="abfc6-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="abfc6-120">Tematy odwołań:</span><span class="sxs-lookup"><span data-stu-id="abfc6-120">Reference topics:</span></span>
<span data-ttu-id="abfc6-121">Następujące tematy dokumentacji dostarczają więcej informacji o używaniu zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="abfc6-122">Zadania do wykonania metody bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="abfc6-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="abfc6-123">Poniżej przedstawiono szczegóły żądania protokołu HTTP 1.1 wykonywania [metoda bezpośrednia] [ lnk-dev-methods] na zbiór urządzeń przy użyciu zadania:</span><span class="sxs-lookup"><span data-stu-id="abfc6-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="abfc6-124">Warunek kwerendy można też na jednym urządzeniu identyfikator lub na liście identyfikatorów, jak pokazano poniżej urządzenia</span><span class="sxs-lookup"><span data-stu-id="abfc6-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="abfc6-125">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="abfc6-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="abfc6-126">[Język zapytań Centrum IoT] [ lnk-query] obejmuje język zapytań Centrum IoT w dodatkowych szczegółów.</span><span class="sxs-lookup"><span data-stu-id="abfc6-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="abfc6-127">Zadania, aby zaktualizować urządzenie dwie właściwości</span><span class="sxs-lookup"><span data-stu-id="abfc6-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="abfc6-128">Poniżej przedstawiono szczegóły żądania protokołu HTTP 1.1 aktualizowanie właściwości dwie urządzenia przy użyciu zadania:</span><span class="sxs-lookup"><span data-stu-id="abfc6-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="abfc6-129">Wykonanie zapytania dotyczącego postępu zadania</span><span class="sxs-lookup"><span data-stu-id="abfc6-129">Querying for progress on jobs</span></span>
<span data-ttu-id="abfc6-130">Poniżej przedstawiono szczegóły żądania protokołu HTTP 1.1 [wykonywania zapytania dotyczącego zadania][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="abfc6-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="abfc6-131">ContinuationToken jest dostarczany z odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="abfc6-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="abfc6-132">Właściwości zadania</span><span class="sxs-lookup"><span data-stu-id="abfc6-132">Jobs Properties</span></span>
<span data-ttu-id="abfc6-133">Oto lista właściwości wraz z opisami odpowiednie, które mogą być używane podczas wykonywania zapytań dotyczących zadań lub wyniki zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="abfc6-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="abfc6-134">Property</span></span> | <span data-ttu-id="abfc6-135">Opis</span><span class="sxs-lookup"><span data-stu-id="abfc6-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="abfc6-136">**Identyfikator zadania**</span><span class="sxs-lookup"><span data-stu-id="abfc6-136">**jobId**</span></span> |<span data-ttu-id="abfc6-137">Aplikacja podany identyfikator zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="abfc6-138">**czas rozpoczęcia**</span><span class="sxs-lookup"><span data-stu-id="abfc6-138">**startTime**</span></span> |<span data-ttu-id="abfc6-139">Aplikacja podany czas rozpoczęcia (ISO 8601) dla zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="abfc6-140">**wartość endTime**</span><span class="sxs-lookup"><span data-stu-id="abfc6-140">**endTime**</span></span> |<span data-ttu-id="abfc6-141">Centrum IoT podać datę (ISO 8601) ukończenia zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="abfc6-142">Jest prawidłowy tylko wtedy, gdy zadanie osiągnie stan "ukończone".</span><span class="sxs-lookup"><span data-stu-id="abfc6-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="abfc6-143">**Typ**</span><span class="sxs-lookup"><span data-stu-id="abfc6-143">**type**</span></span> |<span data-ttu-id="abfc6-144">Typy zadań:</span><span class="sxs-lookup"><span data-stu-id="abfc6-144">Types of jobs:</span></span> |
| <span data-ttu-id="abfc6-145">**scheduledUpdateTwin**: zadanie używane do aktualizowania zestaw żądaną właściwości bądź tagi.</span><span class="sxs-lookup"><span data-stu-id="abfc6-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="abfc6-146">**scheduledDeviceMethod**: zadanie służy do wywoływania metody urządzenia na zestawie twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="abfc6-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="abfc6-147">**Stan**</span><span class="sxs-lookup"><span data-stu-id="abfc6-147">**status**</span></span> |<span data-ttu-id="abfc6-148">Bieżący stan zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-148">Current state of the job.</span></span> <span data-ttu-id="abfc6-149">Dopuszczalne wartości stanu:</span><span class="sxs-lookup"><span data-stu-id="abfc6-149">Possible values for status:</span></span> |
| <span data-ttu-id="abfc6-150">**Oczekujące** : Zaplanowane, oczekuje do pobrania przez usługę zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="abfc6-151">**Zaplanowane** : Zaplanowane na czas w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="abfc6-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="abfc6-152">**uruchomiona** : aktualnie aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="abfc6-153">**Anulowane** : zadanie zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="abfc6-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="abfc6-154">**nie powiodło się** : zadanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="abfc6-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="abfc6-155">**Ukończono** : zadania zakończone.</span><span class="sxs-lookup"><span data-stu-id="abfc6-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="abfc6-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="abfc6-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="abfc6-157">Statystyka wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="abfc6-158">**deviceJobStatistics** właściwości.</span><span class="sxs-lookup"><span data-stu-id="abfc6-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="abfc6-159">Właściwość</span><span class="sxs-lookup"><span data-stu-id="abfc6-159">Property</span></span> | <span data-ttu-id="abfc6-160">Opis</span><span class="sxs-lookup"><span data-stu-id="abfc6-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="abfc6-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="abfc6-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="abfc6-162">Liczba urządzeń w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="abfc6-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="abfc6-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="abfc6-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="abfc6-164">Liczba urządzeń, w których zadanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="abfc6-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="abfc6-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="abfc6-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="abfc6-166">Liczba urządzeń, w którym zadanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="abfc6-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="abfc6-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="abfc6-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="abfc6-168">Liczba urządzeń, które są aktualnie uruchomione zadanie.</span><span class="sxs-lookup"><span data-stu-id="abfc6-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="abfc6-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="abfc6-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="abfc6-170">Liczba urządzeń, które oczekują, aby uruchomić to zadanie.</span><span class="sxs-lookup"><span data-stu-id="abfc6-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="abfc6-171">Odwołanie dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="abfc6-171">Additional reference material</span></span>
<span data-ttu-id="abfc6-172">Inne tematy referencyjne w Podręczniku dewelopera Centrum IoT obejmują:</span><span class="sxs-lookup"><span data-stu-id="abfc6-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="abfc6-173">[Punkty końcowe Centrum IoT] [ lnk-endpoints] opisano różne punkty końcowe, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="abfc6-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="abfc6-174">[Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziałów, które dotyczą usługi IoT Hub i ograniczania przepustowości zachowania można oczekiwać podczas korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="abfc6-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="abfc6-175">[Azure IoT urządzenia i usługi SDK] [ lnk-sdks] Wyświetla listę różnych zestawów SDK języka należy używany podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="abfc6-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="abfc6-176">[Język zapytań Centrum IoT urządzenia twins, zadań i rozsyłania wiadomości] [ lnk-query] opisuje język zapytań Centrum IoT można pobrać z Centrum IoT informacji o twins urządzenia i zadania.</span><span class="sxs-lookup"><span data-stu-id="abfc6-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="abfc6-177">[Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zapewnia więcej informacji na temat Centrum IoT obsługi protokołu MQTT.</span><span class="sxs-lookup"><span data-stu-id="abfc6-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abfc6-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abfc6-178">Next steps</span></span>
<span data-ttu-id="abfc6-179">Jeśli chcesz wypróbować niektóre pojęcia opisane w tym artykule, mogą być zainteresowane w następujących instrukcji Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="abfc6-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="abfc6-180">[Zadania harmonogramu i emisji][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="abfc6-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
