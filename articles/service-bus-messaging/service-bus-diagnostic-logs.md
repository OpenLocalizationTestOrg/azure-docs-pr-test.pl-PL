---
title: "Azure Service Bus dzienników diagnostycznych | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania dzienników diagnostycznych dla usługi Service Bus na platformie Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: 72e18444c83b84c5191a0aab3dc6983517167dd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="6e24e-103">Dzienniki diagnostyczne usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="6e24e-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="6e24e-104">Dla usługi Azure Service Bus, można wyświetlić dwa typy dzienników:</span><span class="sxs-lookup"><span data-stu-id="6e24e-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="6e24e-105">**[Dzienniki aktywności](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="6e24e-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="6e24e-106">Dzienniki te zawierają informacje o operacji wykonywanych w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="6e24e-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="6e24e-107">Dzienniki są zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="6e24e-107">The logs are always enabled.</span></span>
* <span data-ttu-id="6e24e-108">**[Dzienniki diagnostyczne](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="6e24e-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="6e24e-109">Można skonfigurować dziennika diagnostycznego bardziej rozbudowane informacje o wszystko, co się stanie w ramach danego zadania.</span><span class="sxs-lookup"><span data-stu-id="6e24e-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="6e24e-110">Dzienniki diagnostyczne obejmują działania, od czasu utworzenia zadania do momentu usunięcia zadania, w tym aktualizacje i działania, które są wykonywane, gdy zadanie jest uruchomione.</span><span class="sxs-lookup"><span data-stu-id="6e24e-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="6e24e-111">Włączanie dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="6e24e-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="6e24e-112">Dzienniki diagnostyczne są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6e24e-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="6e24e-113">Aby włączyć dzienniki diagnostyczne, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6e24e-113">To enable diagnostic logs, perform the following steps:</span></span>

1.  <span data-ttu-id="6e24e-114">W [portalu Azure](https://portal.azure.com)w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="6e24e-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Nawigacja bloku do dzienników diagnostycznych](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="6e24e-116">Kliknij zasób, który chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="6e24e-116">Click the resource you want to monitor.</span></span>  

3.  <span data-ttu-id="6e24e-117">Kliknij przycisk **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="6e24e-117">Click **Turn on diagnostics**.</span></span>

    ![Włączanie dzienników diagnostycznych](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="6e24e-119">Aby uzyskać **stan**, kliknij przycisk **na**.</span><span class="sxs-lookup"><span data-stu-id="6e24e-119">For **Status**, click **On**.</span></span>

    ![Zmień stan dzienników diagnostycznych](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="6e24e-121">Ustaw element docelowy archiwum, które mają; na przykład konto magazynu, Centrum zdarzeń lub Analiza dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="6e24e-121">Set the archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="6e24e-122">Zapisz nowe ustawienia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="6e24e-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="6e24e-123">Nowe ustawienia zaczęły obowiązywać w ciągu około 10 minut.</span><span class="sxs-lookup"><span data-stu-id="6e24e-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="6e24e-124">Po wykonaniu tej dzienników pojawia się w celu archiwizacji skonfigurowane, na **dzienników diagnostycznych** bloku.</span><span class="sxs-lookup"><span data-stu-id="6e24e-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="6e24e-125">Aby uzyskać więcej informacji na temat konfigurowania diagnostyki, zobacz [omówienie Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6e24e-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="6e24e-126">Dzienniki diagnostyczne schematu</span><span class="sxs-lookup"><span data-stu-id="6e24e-126">Diagnostic logs schema</span></span>

<span data-ttu-id="6e24e-127">Wszystkie dzienniki są przechowywane w formacie JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="6e24e-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="6e24e-128">Każdy wpis ma pól ciągów, które używają formatu opisane w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="6e24e-128">Each entry has string fields that use the format described in the following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="6e24e-129">Schemat operacyjne dzienniki</span><span class="sxs-lookup"><span data-stu-id="6e24e-129">Operational logs schema</span></span>

<span data-ttu-id="6e24e-130">Loguje **OperationalLogs** kategorii przechwytywania, co się dzieje podczas operacji usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6e24e-130">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="6e24e-131">W szczególności te dzienniki przechwytywania typ operacji, łącznie z tworzeniem kolejki, zasoby używane i stan operacji.</span><span class="sxs-lookup"><span data-stu-id="6e24e-131">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span></span>

<span data-ttu-id="6e24e-132">Dziennik operacyjny JSON ciągi zawierać elementy wymienione w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="6e24e-132">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="6e24e-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6e24e-133">Name</span></span> | <span data-ttu-id="6e24e-134">Opis</span><span class="sxs-lookup"><span data-stu-id="6e24e-134">Description</span></span>
------- | -------
<span data-ttu-id="6e24e-135">Identyfikator działania</span><span class="sxs-lookup"><span data-stu-id="6e24e-135">ActivityId</span></span> | <span data-ttu-id="6e24e-136">Wewnętrzny identyfikator używany do śledzenia</span><span class="sxs-lookup"><span data-stu-id="6e24e-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="6e24e-137">EventName</span><span class="sxs-lookup"><span data-stu-id="6e24e-137">EventName</span></span> | <span data-ttu-id="6e24e-138">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="6e24e-138">Operation name</span></span>           
<span data-ttu-id="6e24e-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="6e24e-139">resourceId</span></span> | <span data-ttu-id="6e24e-140">Identyfikator zasobu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6e24e-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="6e24e-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="6e24e-141">SubscriptionId</span></span> | <span data-ttu-id="6e24e-142">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6e24e-142">Subscription ID</span></span>
<span data-ttu-id="6e24e-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="6e24e-143">EventTimeString</span></span> | <span data-ttu-id="6e24e-144">Czas operacji</span><span class="sxs-lookup"><span data-stu-id="6e24e-144">Operation time</span></span>
<span data-ttu-id="6e24e-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="6e24e-145">EventProperties</span></span> | <span data-ttu-id="6e24e-146">Właściwości operacji</span><span class="sxs-lookup"><span data-stu-id="6e24e-146">Operation properties</span></span>
<span data-ttu-id="6e24e-147">Stan</span><span class="sxs-lookup"><span data-stu-id="6e24e-147">Status</span></span> | <span data-ttu-id="6e24e-148">Stan operacji</span><span class="sxs-lookup"><span data-stu-id="6e24e-148">Operation status</span></span>
<span data-ttu-id="6e24e-149">Obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="6e24e-149">Caller</span></span> | <span data-ttu-id="6e24e-150">Obiekt wywołujący operacji (Azure portalu lub zarządzania klienta)</span><span class="sxs-lookup"><span data-stu-id="6e24e-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="6e24e-151">category</span><span class="sxs-lookup"><span data-stu-id="6e24e-151">category</span></span> | <span data-ttu-id="6e24e-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="6e24e-152">OperationalLogs</span></span>

<span data-ttu-id="6e24e-153">Poniżej przedstawiono przykładowy dziennik operacyjny ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="6e24e-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="6e24e-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6e24e-154">Next steps</span></span>

<span data-ttu-id="6e24e-155">Odwiedź poniższe łącza, aby dowiedzieć się więcej na temat magistrali usług:</span><span class="sxs-lookup"><span data-stu-id="6e24e-155">Visit the following links to learn more about Service Bus:</span></span>

* [<span data-ttu-id="6e24e-156">Wprowadzenie do usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="6e24e-156">Introduction to Service Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="6e24e-157">Rozpoczynanie pracy z usługą Service Bus</span><span class="sxs-lookup"><span data-stu-id="6e24e-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
