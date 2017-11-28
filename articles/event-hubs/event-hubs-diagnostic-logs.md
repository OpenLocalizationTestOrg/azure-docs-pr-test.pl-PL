---
title: "dzienniki diagnostyczne aaaAzure usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset zapasowe dzienników diagnostycznych usługi event hubs na platformie Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="a55c4-103">Dzienniki diagnostyczne centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="a55c4-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="a55c4-104">Dla usługi Azure Event Hubs można wyświetlić dwa typy dzienników:</span><span class="sxs-lookup"><span data-stu-id="a55c4-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="a55c4-105">**[Dzienniki aktywności](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="a55c4-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="a55c4-106">Te dzienniki ma informacje o operacji wykonywanych w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="a55c4-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="a55c4-107">Dzienniki Hello są zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="a55c4-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="a55c4-108">**[Dzienniki diagnostyczne](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="a55c4-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="a55c4-109">Dzienniki diagnostyczne bardziej zaawansowane funkcje dostępne w widoku wszystkich podejmowanych można skonfigurować za pomocą zadania.</span><span class="sxs-lookup"><span data-stu-id="a55c4-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="a55c4-110">Dzienniki diagnostyczne obejmują działania, od czasu hello, utworzenia zadania hello do momentu usunięcia zadania hello, w tym aktualizacje i działania, które są wykonywane, gdy jest wykonywane zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="a55c4-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="a55c4-111">Włączanie dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="a55c4-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="a55c4-112">Dzienniki diagnostyczne są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="a55c4-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="a55c4-113">dzienniki diagnostyczne tooenable:</span><span class="sxs-lookup"><span data-stu-id="a55c4-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="a55c4-114">W hello [portalu Azure](https://portal.azure.com)w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="a55c4-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Dzienniki toodiagnostic nawigacji bloku](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="a55c4-116">Kliknij zasób hello ma toomonitor.</span><span class="sxs-lookup"><span data-stu-id="a55c4-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="a55c4-117">Kliknij przycisk **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="a55c4-117">Click **Turn on diagnostics**.</span></span>

    ![Włączanie dzienników diagnostycznych](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="a55c4-119">Aby uzyskać **stan**, kliknij przycisk **na**.</span><span class="sxs-lookup"><span data-stu-id="a55c4-119">For **Status**, click **On**.</span></span>

    ![Zmiana stanu hello dzienników diagnostycznych](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="a55c4-121">Zestaw docelowy archiwum hello, który ma; na przykład konto magazynu, Centrum zdarzeń lub Analiza dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="a55c4-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="a55c4-122">Zapisz hello nowe ustawienia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="a55c4-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="a55c4-123">Nowe ustawienia zaczęły obowiązywać w ciągu około 10 minut.</span><span class="sxs-lookup"><span data-stu-id="a55c4-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="a55c4-124">Po wykonaniu tej dzienników pojawia się w celu archiwizacji hello skonfigurowane, na powitania **dzienników diagnostycznych** bloku.</span><span class="sxs-lookup"><span data-stu-id="a55c4-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="a55c4-125">Aby uzyskać więcej informacji na temat konfigurowania diagnostyki, zobacz hello [omówienie Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a55c4-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="a55c4-126">Dzienniki diagnostyczne kategorii</span><span class="sxs-lookup"><span data-stu-id="a55c4-126">Diagnostic logs categories</span></span>
<span data-ttu-id="a55c4-127">Centra zdarzeń przechwytuje dzienniki diagnostyczne dla dwóch kategorii:</span><span class="sxs-lookup"><span data-stu-id="a55c4-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="a55c4-128">**ArchiveLogs**: dzienniki powiązane tooEvent archiwów koncentratory, w szczególności rejestruje błędy tooarchive pokrewne.</span><span class="sxs-lookup"><span data-stu-id="a55c4-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="a55c4-129">**OperationalLogs**: informacje o tym, co dzieje podczas operacji usługi Event Hubs, w szczególności hello typ operacji, w tym tworzenia Centrum zdarzeń, zasoby używane i hello stan hello operacji.</span><span class="sxs-lookup"><span data-stu-id="a55c4-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="a55c4-130">Dzienniki diagnostyczne schematu</span><span class="sxs-lookup"><span data-stu-id="a55c4-130">Diagnostic logs schema</span></span>
<span data-ttu-id="a55c4-131">Wszystkie dzienniki są przechowywane w formacie JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="a55c4-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="a55c4-132">Każdy wpis ma pól ciągów, w formacie hello opisanego w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="a55c4-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="a55c4-133">Schemat dzienniki archiwum</span><span class="sxs-lookup"><span data-stu-id="a55c4-133">Archive logs schema</span></span>

<span data-ttu-id="a55c4-134">Ciągi JSON dziennika archiwum obejmują elementy wymienione w poniższej tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="a55c4-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="a55c4-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a55c4-135">Name</span></span> | <span data-ttu-id="a55c4-136">Opis</span><span class="sxs-lookup"><span data-stu-id="a55c4-136">Description</span></span>
------- | -------
<span data-ttu-id="a55c4-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="a55c4-137">TaskName</span></span> | <span data-ttu-id="a55c4-138">Opis hello zadań, które zakończyły się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a55c4-138">Description of hello task that failed.</span></span>
<span data-ttu-id="a55c4-139">Identyfikator działania</span><span class="sxs-lookup"><span data-stu-id="a55c4-139">ActivityId</span></span> | <span data-ttu-id="a55c4-140">Wewnętrzny identyfikator używany do śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a55c4-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="a55c4-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="a55c4-141">trackingId</span></span> | <span data-ttu-id="a55c4-142">Wewnętrzny identyfikator używany do śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a55c4-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="a55c4-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="a55c4-143">resourceId</span></span> | <span data-ttu-id="a55c4-144">Identyfikator usługi Azure Resource Manager zasobu.</span><span class="sxs-lookup"><span data-stu-id="a55c4-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="a55c4-145">EventHub</span><span class="sxs-lookup"><span data-stu-id="a55c4-145">eventHub</span></span> | <span data-ttu-id="a55c4-146">Centrum zdarzeń Pełna nazwa (w tym nazwę przestrzeni nazw).</span><span class="sxs-lookup"><span data-stu-id="a55c4-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="a55c4-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="a55c4-147">partitionId</span></span> | <span data-ttu-id="a55c4-148">Zapisywana partycji Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="a55c4-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="a55c4-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="a55c4-149">archiveStep</span></span> | <span data-ttu-id="a55c4-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="a55c4-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="a55c4-151">startTime</span><span class="sxs-lookup"><span data-stu-id="a55c4-151">startTime</span></span> | <span data-ttu-id="a55c4-152">Godzina rozpoczęcia awarii.</span><span class="sxs-lookup"><span data-stu-id="a55c4-152">Failure start time.</span></span>
<span data-ttu-id="a55c4-153">błędy</span><span class="sxs-lookup"><span data-stu-id="a55c4-153">failures</span></span> | <span data-ttu-id="a55c4-154">Liczba wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="a55c4-154">Number of times failure occurred.</span></span>
<span data-ttu-id="a55c4-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="a55c4-155">durationInSeconds</span></span> | <span data-ttu-id="a55c4-156">Czas trwania awarii.</span><span class="sxs-lookup"><span data-stu-id="a55c4-156">Duration of failure.</span></span>
<span data-ttu-id="a55c4-157">Komunikat</span><span class="sxs-lookup"><span data-stu-id="a55c4-157">message</span></span> | <span data-ttu-id="a55c4-158">Komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="a55c4-158">Error message.</span></span>
<span data-ttu-id="a55c4-159">category</span><span class="sxs-lookup"><span data-stu-id="a55c4-159">category</span></span> | <span data-ttu-id="a55c4-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="a55c4-160">ArchiveLogs</span></span>

<span data-ttu-id="a55c4-161">Witaj następujący kod jest przykładem dziennika archiwum ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="a55c4-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="a55c4-162">Schemat operacyjne dzienniki</span><span class="sxs-lookup"><span data-stu-id="a55c4-162">Operational logs schema</span></span>

<span data-ttu-id="a55c4-163">Dziennik operacyjny JSON ciągi zawierać elementy wymienione w poniższej tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="a55c4-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="a55c4-164">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a55c4-164">Name</span></span> | <span data-ttu-id="a55c4-165">Opis</span><span class="sxs-lookup"><span data-stu-id="a55c4-165">Description</span></span>
------- | -------
<span data-ttu-id="a55c4-166">Identyfikator działania</span><span class="sxs-lookup"><span data-stu-id="a55c4-166">ActivityId</span></span> | <span data-ttu-id="a55c4-167">Wewnętrzny identyfikator używany tootrack cel.</span><span class="sxs-lookup"><span data-stu-id="a55c4-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="a55c4-168">EventName</span><span class="sxs-lookup"><span data-stu-id="a55c4-168">EventName</span></span> | <span data-ttu-id="a55c4-169">Nazwa operacji.</span><span class="sxs-lookup"><span data-stu-id="a55c4-169">Operation name.</span></span>  
<span data-ttu-id="a55c4-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="a55c4-170">resourceId</span></span> | <span data-ttu-id="a55c4-171">Identyfikator usługi Azure Resource Manager zasobu.</span><span class="sxs-lookup"><span data-stu-id="a55c4-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="a55c4-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a55c4-172">SubscriptionId</span></span> | <span data-ttu-id="a55c4-173">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a55c4-173">Subscription ID.</span></span>
<span data-ttu-id="a55c4-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="a55c4-174">EventTimeString</span></span> | <span data-ttu-id="a55c4-175">Czas operacji.</span><span class="sxs-lookup"><span data-stu-id="a55c4-175">Operation time.</span></span>
<span data-ttu-id="a55c4-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="a55c4-176">EventProperties</span></span> | <span data-ttu-id="a55c4-177">Właściwości operacji.</span><span class="sxs-lookup"><span data-stu-id="a55c4-177">Operation properties.</span></span>
<span data-ttu-id="a55c4-178">Stan</span><span class="sxs-lookup"><span data-stu-id="a55c4-178">Status</span></span> | <span data-ttu-id="a55c4-179">Stan operacji.</span><span class="sxs-lookup"><span data-stu-id="a55c4-179">Operation status.</span></span>
<span data-ttu-id="a55c4-180">Obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="a55c4-180">Caller</span></span> | <span data-ttu-id="a55c4-181">Obiekt wywołujący operacji (Azure portalu lub zarządzania klienta).</span><span class="sxs-lookup"><span data-stu-id="a55c4-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="a55c4-182">category</span><span class="sxs-lookup"><span data-stu-id="a55c4-182">category</span></span> | <span data-ttu-id="a55c4-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="a55c4-183">OperationalLogs</span></span>

<span data-ttu-id="a55c4-184">Witaj następujący kod jest przykładem ciągu JSON dziennik operacji:</span><span class="sxs-lookup"><span data-stu-id="a55c4-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="a55c4-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a55c4-185">Next steps</span></span>
* [<span data-ttu-id="a55c4-186">Wprowadzenie tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="a55c4-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a55c4-187">Omówienie interfejsu API usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a55c4-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="a55c4-188">Rozpoczynanie pracy z usługą Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a55c4-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
