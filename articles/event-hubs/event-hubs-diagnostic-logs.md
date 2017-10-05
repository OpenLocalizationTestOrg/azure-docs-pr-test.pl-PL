---
title: "Azure Event Hubs dzienników diagnostycznych | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania dzienników diagnostycznych usługi event hubs na platformie Azure."
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
ms.openlocfilehash: 09bc62f4918635419d74ef3ae400a41d4ce58b5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="06d73-103">Dzienniki diagnostyczne centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="06d73-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="06d73-104">Dla usługi Azure Event Hubs można wyświetlić dwa typy dzienników:</span><span class="sxs-lookup"><span data-stu-id="06d73-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="06d73-105">**[Dzienniki aktywności](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="06d73-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="06d73-106">Te dzienniki ma informacje o operacji wykonywanych w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="06d73-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="06d73-107">Dzienniki są zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="06d73-107">The logs are always enabled.</span></span>
* <span data-ttu-id="06d73-108">**[Dzienniki diagnostyczne](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="06d73-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="06d73-109">Dzienniki diagnostyczne bardziej zaawansowane funkcje dostępne w widoku wszystkich podejmowanych można skonfigurować za pomocą zadania.</span><span class="sxs-lookup"><span data-stu-id="06d73-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="06d73-110">Dzienniki diagnostyczne obejmują działania, od czasu utworzenia zadania do momentu usunięcia zadania, w tym aktualizacje i działania, które są wykonywane, gdy zadanie jest uruchomione.</span><span class="sxs-lookup"><span data-stu-id="06d73-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="06d73-111">Włączanie dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="06d73-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="06d73-112">Dzienniki diagnostyczne są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="06d73-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="06d73-113">Aby włączyć dzienniki diagnostyczne:</span><span class="sxs-lookup"><span data-stu-id="06d73-113">To enable diagnostic logs:</span></span>

1.  <span data-ttu-id="06d73-114">W [portalu Azure](https://portal.azure.com)w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="06d73-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Nawigacja bloku do dzienników diagnostycznych](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="06d73-116">Kliknij zasób, który chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="06d73-116">Click the resource you want to monitor.</span></span>

3.  <span data-ttu-id="06d73-117">Kliknij przycisk **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="06d73-117">Click **Turn on diagnostics**.</span></span>

    ![Włączanie dzienników diagnostycznych](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="06d73-119">Aby uzyskać **stan**, kliknij przycisk **na**.</span><span class="sxs-lookup"><span data-stu-id="06d73-119">For **Status**, click **On**.</span></span>

    ![Zmień stan dzienników diagnostycznych](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="06d73-121">Ustaw element docelowy archiwum, które mają; na przykład konto magazynu, Centrum zdarzeń lub Analiza dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="06d73-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="06d73-122">Zapisz nowe ustawienia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="06d73-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="06d73-123">Nowe ustawienia zaczęły obowiązywać w ciągu około 10 minut.</span><span class="sxs-lookup"><span data-stu-id="06d73-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="06d73-124">Po wykonaniu tej dzienników pojawia się w celu archiwizacji skonfigurowane, na **dzienników diagnostycznych** bloku.</span><span class="sxs-lookup"><span data-stu-id="06d73-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="06d73-125">Aby uzyskać więcej informacji na temat konfigurowania diagnostyki, zobacz [omówienie Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="06d73-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="06d73-126">Dzienniki diagnostyczne kategorii</span><span class="sxs-lookup"><span data-stu-id="06d73-126">Diagnostic logs categories</span></span>
<span data-ttu-id="06d73-127">Centra zdarzeń przechwytuje dzienniki diagnostyczne dla dwóch kategorii:</span><span class="sxs-lookup"><span data-stu-id="06d73-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="06d73-128">**ArchiveLogs**: dzienniki związane z archiwami usługi Event Hubs, w szczególności, dzienniki związane z archiwum błędy.</span><span class="sxs-lookup"><span data-stu-id="06d73-128">**ArchiveLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span></span>
* <span data-ttu-id="06d73-129">**OperationalLogs**: informacje o tym, co dzieje się podczas operacji usługi Event Hubs, w szczególności operacji typu, łącznie z tworzenia Centrum zdarzeń, zasoby używane i stan operacji.</span><span class="sxs-lookup"><span data-stu-id="06d73-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="06d73-130">Dzienniki diagnostyczne schematu</span><span class="sxs-lookup"><span data-stu-id="06d73-130">Diagnostic logs schema</span></span>
<span data-ttu-id="06d73-131">Wszystkie dzienniki są przechowywane w formacie JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="06d73-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="06d73-132">Każdy wpis ma pól ciągów, które używają formatu opisane w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="06d73-132">Each entry has string fields that use the format described in the following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="06d73-133">Schemat dzienniki archiwum</span><span class="sxs-lookup"><span data-stu-id="06d73-133">Archive logs schema</span></span>

<span data-ttu-id="06d73-134">Ciągi JSON dziennika archiwum obejmują elementy wymienione w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="06d73-134">Archive log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="06d73-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="06d73-135">Name</span></span> | <span data-ttu-id="06d73-136">Opis</span><span class="sxs-lookup"><span data-stu-id="06d73-136">Description</span></span>
------- | -------
<span data-ttu-id="06d73-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="06d73-137">TaskName</span></span> | <span data-ttu-id="06d73-138">Opis zadań, które zakończyły się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="06d73-138">Description of the task that failed.</span></span>
<span data-ttu-id="06d73-139">Identyfikator działania</span><span class="sxs-lookup"><span data-stu-id="06d73-139">ActivityId</span></span> | <span data-ttu-id="06d73-140">Wewnętrzny identyfikator używany do śledzenia.</span><span class="sxs-lookup"><span data-stu-id="06d73-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="06d73-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="06d73-141">trackingId</span></span> | <span data-ttu-id="06d73-142">Wewnętrzny identyfikator używany do śledzenia.</span><span class="sxs-lookup"><span data-stu-id="06d73-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="06d73-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="06d73-143">resourceId</span></span> | <span data-ttu-id="06d73-144">Identyfikator usługi Azure Resource Manager zasobu.</span><span class="sxs-lookup"><span data-stu-id="06d73-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="06d73-145">EventHub</span><span class="sxs-lookup"><span data-stu-id="06d73-145">eventHub</span></span> | <span data-ttu-id="06d73-146">Centrum zdarzeń Pełna nazwa (w tym nazwę przestrzeni nazw).</span><span class="sxs-lookup"><span data-stu-id="06d73-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="06d73-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="06d73-147">partitionId</span></span> | <span data-ttu-id="06d73-148">Zapisywana partycji Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="06d73-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="06d73-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="06d73-149">archiveStep</span></span> | <span data-ttu-id="06d73-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="06d73-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="06d73-151">startTime</span><span class="sxs-lookup"><span data-stu-id="06d73-151">startTime</span></span> | <span data-ttu-id="06d73-152">Godzina rozpoczęcia awarii.</span><span class="sxs-lookup"><span data-stu-id="06d73-152">Failure start time.</span></span>
<span data-ttu-id="06d73-153">błędy</span><span class="sxs-lookup"><span data-stu-id="06d73-153">failures</span></span> | <span data-ttu-id="06d73-154">Liczba wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="06d73-154">Number of times failure occurred.</span></span>
<span data-ttu-id="06d73-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="06d73-155">durationInSeconds</span></span> | <span data-ttu-id="06d73-156">Czas trwania awarii.</span><span class="sxs-lookup"><span data-stu-id="06d73-156">Duration of failure.</span></span>
<span data-ttu-id="06d73-157">Komunikat</span><span class="sxs-lookup"><span data-stu-id="06d73-157">message</span></span> | <span data-ttu-id="06d73-158">Komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="06d73-158">Error message.</span></span>
<span data-ttu-id="06d73-159">category</span><span class="sxs-lookup"><span data-stu-id="06d73-159">category</span></span> | <span data-ttu-id="06d73-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="06d73-160">ArchiveLogs</span></span>

<span data-ttu-id="06d73-161">Następujący kod jest przykładem dziennika archiwum ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="06d73-161">The following code is an example of an archive log JSON string:</span></span>

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
     "message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="06d73-162">Schemat operacyjne dzienniki</span><span class="sxs-lookup"><span data-stu-id="06d73-162">Operational logs schema</span></span>

<span data-ttu-id="06d73-163">Dziennik operacyjny JSON ciągi zawierać elementy wymienione w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="06d73-163">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="06d73-164">Nazwa</span><span class="sxs-lookup"><span data-stu-id="06d73-164">Name</span></span> | <span data-ttu-id="06d73-165">Opis</span><span class="sxs-lookup"><span data-stu-id="06d73-165">Description</span></span>
------- | -------
<span data-ttu-id="06d73-166">Identyfikator działania</span><span class="sxs-lookup"><span data-stu-id="06d73-166">ActivityId</span></span> | <span data-ttu-id="06d73-167">Wewnętrzny identyfikator służący do śledzenia cel.</span><span class="sxs-lookup"><span data-stu-id="06d73-167">Internal ID, used to track purpose.</span></span>
<span data-ttu-id="06d73-168">EventName</span><span class="sxs-lookup"><span data-stu-id="06d73-168">EventName</span></span> | <span data-ttu-id="06d73-169">Nazwa operacji.</span><span class="sxs-lookup"><span data-stu-id="06d73-169">Operation name.</span></span>  
<span data-ttu-id="06d73-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="06d73-170">resourceId</span></span> | <span data-ttu-id="06d73-171">Identyfikator usługi Azure Resource Manager zasobu.</span><span class="sxs-lookup"><span data-stu-id="06d73-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="06d73-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="06d73-172">SubscriptionId</span></span> | <span data-ttu-id="06d73-173">Identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="06d73-173">Subscription ID.</span></span>
<span data-ttu-id="06d73-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="06d73-174">EventTimeString</span></span> | <span data-ttu-id="06d73-175">Czas operacji.</span><span class="sxs-lookup"><span data-stu-id="06d73-175">Operation time.</span></span>
<span data-ttu-id="06d73-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="06d73-176">EventProperties</span></span> | <span data-ttu-id="06d73-177">Właściwości operacji.</span><span class="sxs-lookup"><span data-stu-id="06d73-177">Operation properties.</span></span>
<span data-ttu-id="06d73-178">Stan</span><span class="sxs-lookup"><span data-stu-id="06d73-178">Status</span></span> | <span data-ttu-id="06d73-179">Stan operacji.</span><span class="sxs-lookup"><span data-stu-id="06d73-179">Operation status.</span></span>
<span data-ttu-id="06d73-180">Obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="06d73-180">Caller</span></span> | <span data-ttu-id="06d73-181">Obiekt wywołujący operacji (Azure portalu lub zarządzania klienta).</span><span class="sxs-lookup"><span data-stu-id="06d73-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="06d73-182">category</span><span class="sxs-lookup"><span data-stu-id="06d73-182">category</span></span> | <span data-ttu-id="06d73-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="06d73-183">OperationalLogs</span></span>

<span data-ttu-id="06d73-184">Następujący kod jest przykładem ciągu JSON dziennik operacji:</span><span class="sxs-lookup"><span data-stu-id="06d73-184">The following code is an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="06d73-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06d73-185">Next steps</span></span>
* [<span data-ttu-id="06d73-186">Wprowadzenie do usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="06d73-186">Introduction to Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="06d73-187">Omówienie interfejsu API usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="06d73-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="06d73-188">Rozpoczynanie pracy z usługą Event Hubs</span><span class="sxs-lookup"><span data-stu-id="06d73-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
