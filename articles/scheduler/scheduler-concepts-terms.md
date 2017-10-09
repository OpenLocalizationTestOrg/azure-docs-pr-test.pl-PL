---
title: "aaaScheduler pojęcia, warunki i jednostek | Dokumentacja firmy Microsoft"
description: "Pojęcia, terminologia oraz hierarchia jednostek związane z usługą Azure Scheduler, w tym zadania i kolekcje zadań.  Kompleksowy przykład zaplanowanego zadania."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="28845-104">Pojęcia i terminologia dotyczące usługi Scheduler oraz hierarchia jednostek</span><span class="sxs-lookup"><span data-stu-id="28845-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="28845-105">Hierarchia jednostek w ramach usługi Scheduler</span><span class="sxs-lookup"><span data-stu-id="28845-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="28845-106">Witaj poniższej tabeli opisano hello głównego widoczne lub zasoby używane przez hello API harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="28845-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="28845-107">Zasób</span><span class="sxs-lookup"><span data-stu-id="28845-107">Resource</span></span> | <span data-ttu-id="28845-108">Opis</span><span class="sxs-lookup"><span data-stu-id="28845-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28845-109">**Kolekcja zadań**</span><span class="sxs-lookup"><span data-stu-id="28845-109">**Job collection**</span></span> |<span data-ttu-id="28845-110">Kolekcja zadań zawiera grupy zadań i przechowuje ustawienia, przydziały i limity współużytkowane przez zadań w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="28845-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="28845-111">Kolekcja zadań jest tworzona przez właściciela subskrypcji i stanowi grupę zadań utworzoną na podstawie granic użycia lub zastosowania.</span><span class="sxs-lookup"><span data-stu-id="28845-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="28845-112">Jest ograniczone tooone regionu.</span><span class="sxs-lookup"><span data-stu-id="28845-112">It’s constrained tooone region.</span></span> <span data-ttu-id="28845-113">Umożliwia także przydziały hello Wymuszanie użycia hello tooconstrain wszystkich zadań w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="28845-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="28845-114">przydziały Hello obejmują MaxJobs i MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="28845-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="28845-115">**Zadanie**</span><span class="sxs-lookup"><span data-stu-id="28845-115">**Job**</span></span> |<span data-ttu-id="28845-116">Zadanie definiuje jedną powtarzającą się akcję powiązaną z prostymi lub złożonymi strategiami wykonania.</span><span class="sxs-lookup"><span data-stu-id="28845-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="28845-117">Akcje mogą obejmować żądania HTTP, żądania kolejki magazynu i żądania kolejki magistrali usług lub tematu magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="28845-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="28845-118">**Historia zadania**</span><span class="sxs-lookup"><span data-stu-id="28845-118">**Job history**</span></span> |<span data-ttu-id="28845-119">Historia zadania zawiera szczegółowe informacje dotyczące wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="28845-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="28845-120">Zawiera ona informacje na temat pomyślnych wykonań i niepowodzeń, a także wszelkie szczegóły odpowiedzi. niepowodzeń, a także wszelkie szczegóły odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="28845-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="28845-121">Zarządzanie jednostkami usługi Scheduler</span><span class="sxs-lookup"><span data-stu-id="28845-121">Scheduler entity management</span></span>
<span data-ttu-id="28845-122">Na wysokim poziomie harmonogram hello i interfejs API zarządzania usługami hello uwidacznia następujące operacje na zasobach hello hello:</span><span class="sxs-lookup"><span data-stu-id="28845-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="28845-123">Możliwości</span><span class="sxs-lookup"><span data-stu-id="28845-123">Capability</span></span> | <span data-ttu-id="28845-124">Opis i adres URI</span><span class="sxs-lookup"><span data-stu-id="28845-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="28845-125">**Zarządzanie kolekcją zadań**</span><span class="sxs-lookup"><span data-stu-id="28845-125">**Job collection management**</span></span> |<span data-ttu-id="28845-126">GET PUT i DELETE Obsługa tworzenia i modyfikowania kolekcji zadań i zadań hello zawartych w niej.</span><span class="sxs-lookup"><span data-stu-id="28845-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="28845-127">Kolekcja zadań jest kontenerem dla zadania oraz mapuje tooquotas i ustawienia udostępnione.</span><span class="sxs-lookup"><span data-stu-id="28845-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="28845-128">Przykłady przydziałów, które zostały opisane w dalszej części artykułu, dotyczą maksymalnej liczby zadań oraz najmniejszego interwału cyklu.</span><span class="sxs-lookup"><span data-stu-id="28845-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="28845-129">PUT i DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="28845-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="28845-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="28845-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="28845-131">**Zarządzanie zadaniami**</span><span class="sxs-lookup"><span data-stu-id="28845-131">**Job management**</span></span> |<span data-ttu-id="28845-132">Obsługa żądań GET, PUT, POST, PATCH i DELETE służących do tworzenia i modyfikowania zadań.</span><span class="sxs-lookup"><span data-stu-id="28845-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="28845-133">Wszystkie zadania muszą należeć tooa kolekcji zadań, która już istnieje, więc nie ma żadnych niejawne tworzenie.</span><span class="sxs-lookup"><span data-stu-id="28845-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="28845-134">**Zarządzanie historią zadania**</span><span class="sxs-lookup"><span data-stu-id="28845-134">**Job history management**</span></span> |<span data-ttu-id="28845-135">Obsługa żądania GET umożliwiającego pobranie historii wykonywania zadania z 60 dni obejmującej m.in. informacje o czasie, który upłynął podczas zadania, oraz o wynikach wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="28845-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="28845-136">Dodaje obsługę parametru ciągu zapytania służącego do filtrowania na podstawie stanu i statusu.</span><span class="sxs-lookup"><span data-stu-id="28845-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="28845-137">Typy zadań</span><span class="sxs-lookup"><span data-stu-id="28845-137">Job types</span></span>
<span data-ttu-id="28845-138">Istnieje wiele typów zadań: zadania HTTP (w tym zadania protokołu HTTPS, które obsługują protokół SSL), zadania kolejki magazynu, zadania kolejki magistrali usług i zadania tematu magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="28845-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="28845-139">Zadania HTTP są odpowiednie, jeśli istnieje punkt końcowy danego obciążenia lub usługi.</span><span class="sxs-lookup"><span data-stu-id="28845-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="28845-140">Możesz użyć magazynu kolejki zadań toopost wiadomości toostorage kolejki, dlatego te zadania są idealne rozwiązanie w przypadku obciążeń, które korzystają z magazynu kolejek.</span><span class="sxs-lookup"><span data-stu-id="28845-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="28845-141">Podobnie zadania magistrali usług są odpowiednie dla obciążeń wykorzystujących kolejki i tematy magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="28845-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="28845-142">Jednostka "zadania" Hello szczegółowo</span><span class="sxs-lookup"><span data-stu-id="28845-142">hello "job" entity in detail</span></span>
<span data-ttu-id="28845-143">Ogólna struktura zaplanowanego zadania obejmuje kilka elementów:</span><span class="sxs-lookup"><span data-stu-id="28845-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="28845-144">Witaj tooperform akcji po hello zadania czasomierza</span><span class="sxs-lookup"><span data-stu-id="28845-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="28845-145">Witaj (opcjonalnie) czas toorun hello zadania</span><span class="sxs-lookup"><span data-stu-id="28845-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="28845-146">(Opcjonalnie) Kiedy i jak często zadanie hello toorepeat</span><span class="sxs-lookup"><span data-stu-id="28845-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="28845-147">(Opcjonalnie) Toofire akcji, jeśli akcji głównej hello nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="28845-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="28845-148">Wewnętrznie zaplanowane zadanie zawiera także dane dostarczane przez system, takie jak następnym zaplanowanym terminie wykonywania hello.</span><span class="sxs-lookup"><span data-stu-id="28845-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="28845-149">Witaj następującego kodu zapewnia kompleksowy przykład zaplanowanego zadania.</span><span class="sxs-lookup"><span data-stu-id="28845-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="28845-150">Szczegóły można znaleźć w kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="28845-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="28845-151">Jak pokazano w hello próbki zaplanowane zadanie powyżej, definicji zadania ma kilka części:</span><span class="sxs-lookup"><span data-stu-id="28845-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="28845-152">Czas rozpoczęcia (“startTime”)</span><span class="sxs-lookup"><span data-stu-id="28845-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="28845-153">Akcja („action”), w tym akcja w przypadku błędu („errorAction”)</span><span class="sxs-lookup"><span data-stu-id="28845-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="28845-154">Cykl („recurrence”)</span><span class="sxs-lookup"><span data-stu-id="28845-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="28845-155">Stan („state”)</span><span class="sxs-lookup"><span data-stu-id="28845-155">State (“state”)</span></span>  
* <span data-ttu-id="28845-156">Status („status”)</span><span class="sxs-lookup"><span data-stu-id="28845-156">Status (“status”)</span></span>  
* <span data-ttu-id="28845-157">Zasady ponawiania („retryPolicy”)</span><span class="sxs-lookup"><span data-stu-id="28845-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="28845-158">Przeanalizujmy szczegółowo każdy z nich:</span><span class="sxs-lookup"><span data-stu-id="28845-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="28845-159">startTime</span><span class="sxs-lookup"><span data-stu-id="28845-159">startTime</span></span>
<span data-ttu-id="28845-160">Witaj "wartość startTime" jest czas rozpoczęcia hello i umożliwia toospecify wywołującego hello przesunięcie umieszczonego hello w strefie czasowej [formacie ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="28845-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="28845-161">action i errorAction</span><span class="sxs-lookup"><span data-stu-id="28845-161">action and errorAction</span></span>
<span data-ttu-id="28845-162">Hello: akcja jest wywoływana przy każdym wystąpieniu Akcja hello i opisuje typ wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="28845-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="28845-163">Akcja Hello jest, co ma zostać wykonany hello podany harmonogram.</span><span class="sxs-lookup"><span data-stu-id="28845-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="28845-164">Usługa Scheduler obsługuje akcje HTTP, akcje kolejki magazynu oraz akcje tematu i kolejki magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="28845-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="28845-165">Akcja Hello w powyższym przykładzie hello jest akcji HTTP.</span><span class="sxs-lookup"><span data-stu-id="28845-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="28845-166">Poniżej znajduje się przykład akcji kolejki magazynu:</span><span class="sxs-lookup"><span data-stu-id="28845-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="28845-167">Poniżej znajduje się przykład akcji tematu magistrali usług:</span><span class="sxs-lookup"><span data-stu-id="28845-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="28845-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="28845-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="28845-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Możliwe opcje to netMessaging i AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Wybrany komunikat", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="28845-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="28845-170">Poniżej znajduje się przykład akcji kolejki magistrali usług:</span><span class="sxs-lookup"><span data-stu-id="28845-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="28845-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="28845-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="28845-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Możliwe opcje to netMessaging i AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="28845-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="28845-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Wybrany komunikat",</span><span class="sxs-lookup"><span data-stu-id="28845-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="28845-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="28845-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="28845-175">Witaj "errorAction" jest hello błąd obsługi, hello Akcja wywoływana, gdy hello głównej akcji kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="28845-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="28845-176">Możesz użyć tej zmiennej toocall punktu końcowego obsługi błędów lub wysłać powiadomienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="28845-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="28845-177">Może to służyć do osiągnięcia dodatkowej punktu końcowego w przypadku hello tego hello podstawowy jest niedostępny (np. w przypadku hello awarii w lokacji hello punktu końcowego) lub może służyć do powiadamiania błąd obsługi punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="28845-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="28845-178">Podobnie jak akcji głównej hello hello akcji błędu może być proste i złożone logiki oparte na inne akcje.</span><span class="sxs-lookup"><span data-stu-id="28845-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="28845-179">jak toocreate tokenu sygnatury dostępu Współdzielonego, można znaleźć zbyt toolearn[tworzenia i używania sygnaturę dostępu współdzielonego](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="28845-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="28845-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="28845-180">recurrence</span></span>
<span data-ttu-id="28845-181">Na cykl składa się kilka elementów:</span><span class="sxs-lookup"><span data-stu-id="28845-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="28845-182">Częstotliwość (frequency): minuta, godzina, dzień, tydzień, miesiąc lub rok</span><span class="sxs-lookup"><span data-stu-id="28845-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="28845-183">: Interwał na powitania podana częstotliwość cyklu hello</span><span class="sxs-lookup"><span data-stu-id="28845-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="28845-184">Harmonogram wyznaczonych: Określ minuty, godziny, dni tygodnia, miesięcy i monthdays hello cyklu</span><span class="sxs-lookup"><span data-stu-id="28845-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="28845-185">Liczba (count): liczba wystąpień</span><span class="sxs-lookup"><span data-stu-id="28845-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="28845-186">Czas zakończenia: żadne zadania będą wykonywane po hello określony czas zakończenia</span><span class="sxs-lookup"><span data-stu-id="28845-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="28845-187">Zadanie określa się jako cykliczne, jeśli jego definicja JSON zawiera obiekt cykliczny.</span><span class="sxs-lookup"><span data-stu-id="28845-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="28845-188">Jeśli jest określony zarówno liczby, jak i endTime jest honorowane hello ukończenia regułę, która zostanie wykonane jako pierwsze.</span><span class="sxs-lookup"><span data-stu-id="28845-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="28845-189">state</span><span class="sxs-lookup"><span data-stu-id="28845-189">state</span></span>
<span data-ttu-id="28845-190">Stan Hello zadania hello jest jednym z cztery wartości: włączone, wyłączone, zakończone lub wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="28845-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="28845-191">Możesz też ZAZNACZYĆ lub poprawki zadania, tak jak tooupdate ich toohello włączenie lub wyłączenie stanu.</span><span class="sxs-lookup"><span data-stu-id="28845-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="28845-192">W przypadku zadania została wykonana lub wystąpił błąd, który jest stan końcowy, który nie można zaktualizować (ale nadal można usunąć zadania hello).</span><span class="sxs-lookup"><span data-stu-id="28845-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="28845-193">Przykład właściwość state hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="28845-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="28845-194">Zadania ukończone oraz zadania z błędami są usuwane po upływie 60 dni.</span><span class="sxs-lookup"><span data-stu-id="28845-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="28845-195">status</span><span class="sxs-lookup"><span data-stu-id="28845-195">status</span></span>
<span data-ttu-id="28845-196">Po rozpoczęciu zadania harmonogramu, zostaną zwrócone informacje o bieżący stan zadania hello hello.</span><span class="sxs-lookup"><span data-stu-id="28845-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="28845-197">Ten obiekt nie jest można ustawić przez użytkownika hello — jest on ustawiony przez hello system.</span><span class="sxs-lookup"><span data-stu-id="28845-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="28845-198">Jednak jest ona objęta hello obiektu zadania (a nie oddzielnych zasobu połączonego), aby jeden łatwo uzyskać hello stanu zadania.</span><span class="sxs-lookup"><span data-stu-id="28845-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="28845-199">Stan zadania zawiera czas hello hello poprzednie wykonanie (jeśli istnieje), hello czasu hello kolejne zaplanowane wykonanie (dla zadania w toku), a liczba wykonań hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="28845-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="28845-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="28845-200">retryPolicy</span></span>
<span data-ttu-id="28845-201">W przypadku niepowodzenia zadania harmonogramu jest możliwe toospecify toodetermine zasady ponawiania, czy i jak akcji hello próba zostanie ponowiona.</span><span class="sxs-lookup"><span data-stu-id="28845-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="28845-202">Jest to określane za pomocą hello **retryType** obiektu — ustawiono zbyt**Brak** Jeśli nie zasady ponawiania zgodnie z powyższym.</span><span class="sxs-lookup"><span data-stu-id="28845-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="28845-203">Ustaw zbyt**stałej** przypadku zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="28845-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="28845-204">tooset zasady ponawiania, można określić dodatkowe ustawienia w dwóch: interwał ponawiania prób (**retryInterval**) i hello liczby ponownych prób (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="28845-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="28845-205">Interwał ponawiania Hello, określony za pomocą hello **retryInterval** obiektu, jest hello interwał między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="28845-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="28845-206">Jego wartość domyślna to 30 sekund. Minimalna wartość, jaką można skonfigurować, wynosi 15 sekund, a wartość maksymalna — 18 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="28845-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="28845-207">W przypadku zadań z bezpłatnej kolekcji zadań minimalna wartość możliwa do skonfigurowania to 1 godzina.</span><span class="sxs-lookup"><span data-stu-id="28845-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="28845-208">Jest on zdefiniowany w formacie ISO 8601 hello.</span><span class="sxs-lookup"><span data-stu-id="28845-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="28845-209">Podobnie, określona jest wartość hello hello liczby ponownych prób z hello **retryCount** obiekt; jest hello liczbę razy, zostanie podjęta ponowna próba.</span><span class="sxs-lookup"><span data-stu-id="28845-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="28845-210">Wartość domyślna to 4, a wartość maksymalna jest 20\.</span><span class="sxs-lookup"><span data-stu-id="28845-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="28845-211">Zarówno **retryInterval** i **retryCount** są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="28845-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="28845-212">Są podane wartości domyślne, jeśli **retryType** ustawiono zbyt**stałej** i nie określono żadnych wartości jawnie.</span><span class="sxs-lookup"><span data-stu-id="28845-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="28845-213">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="28845-213">See also</span></span>
 [<span data-ttu-id="28845-214">Co to jest Scheduler?</span><span class="sxs-lookup"><span data-stu-id="28845-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="28845-215">Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="28845-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="28845-216">Plany i rozliczenia w usłudze Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="28845-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="28845-217">Jak planuje toobuild złożone i zaawansowane cyklu z Harmonogram systemu Azure</span><span class="sxs-lookup"><span data-stu-id="28845-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="28845-218">Dokumentacja interfejsu API REST usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="28845-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="28845-219">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="28845-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="28845-220">Wysoka dostępność i niezawodność usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="28845-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="28845-221">Limity, wartości domyślne i kody błędów usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="28845-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="28845-222">Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="28845-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

