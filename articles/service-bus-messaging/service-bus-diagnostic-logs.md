---
title: "dzienniki diagnostyczne aaaAzure usługi Service Bus | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset zapasowe dzienników diagnostycznych dla usługi Service Bus na platformie Azure."
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
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="177da-103">Dzienniki diagnostyczne usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="177da-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="177da-104">Dla usługi Azure Service Bus, można wyświetlić dwa typy dzienników:</span><span class="sxs-lookup"><span data-stu-id="177da-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="177da-105">**[Dzienniki aktywności](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="177da-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="177da-106">Dzienniki te zawierają informacje o operacji wykonywanych w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="177da-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="177da-107">Dzienniki Hello są zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="177da-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="177da-108">**[Dzienniki diagnostyczne](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="177da-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="177da-109">Można skonfigurować dziennika diagnostycznego bardziej rozbudowane informacje o wszystko, co się stanie w ramach danego zadania.</span><span class="sxs-lookup"><span data-stu-id="177da-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="177da-110">Dzienniki diagnostyczne obejmują działania, od czasu hello, utworzenia zadania hello do momentu usunięcia zadania hello, w tym aktualizacje i działania, które są wykonywane, gdy jest wykonywane zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="177da-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="177da-111">Włączanie dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="177da-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="177da-112">Dzienniki diagnostyczne są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="177da-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="177da-113">tooenable dzienników diagnostycznych, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="177da-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="177da-114">W hello [portalu Azure](https://portal.azure.com)w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="177da-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Dzienniki toodiagnostic nawigacji bloku](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="177da-116">Kliknij zasób hello ma toomonitor.</span><span class="sxs-lookup"><span data-stu-id="177da-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="177da-117">Kliknij przycisk **Włącz diagnostykę**.</span><span class="sxs-lookup"><span data-stu-id="177da-117">Click **Turn on diagnostics**.</span></span>

    ![Włączanie dzienników diagnostycznych](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="177da-119">Aby uzyskać **stan**, kliknij przycisk **na**.</span><span class="sxs-lookup"><span data-stu-id="177da-119">For **Status**, click **On**.</span></span>

    ![Zmień stan dzienników diagnostycznych](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="177da-121">Zestaw docelowy archiwum hello, który ma; na przykład konto magazynu, Centrum zdarzeń lub Analiza dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="177da-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="177da-122">Zapisz hello nowe ustawienia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="177da-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="177da-123">Nowe ustawienia zaczęły obowiązywać w ciągu około 10 minut.</span><span class="sxs-lookup"><span data-stu-id="177da-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="177da-124">Po wykonaniu tej dzienników pojawia się w celu archiwizacji hello skonfigurowane, na powitania **dzienników diagnostycznych** bloku.</span><span class="sxs-lookup"><span data-stu-id="177da-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="177da-125">Aby uzyskać więcej informacji na temat konfigurowania diagnostyki, zobacz hello [omówienie Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="177da-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="177da-126">Dzienniki diagnostyczne schematu</span><span class="sxs-lookup"><span data-stu-id="177da-126">Diagnostic logs schema</span></span>

<span data-ttu-id="177da-127">Wszystkie dzienniki są przechowywane w formacie JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="177da-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="177da-128">Każdy wpis ma pól ciągów, w formacie hello opisane w następujących sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="177da-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="177da-129">Schemat operacyjne dzienniki</span><span class="sxs-lookup"><span data-stu-id="177da-129">Operational logs schema</span></span>

<span data-ttu-id="177da-130">Loguje hello **OperationalLogs** kategorii przechwytywania, co się dzieje podczas operacji usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="177da-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="177da-131">W szczególności te dzienniki przechwytywania hello operacji typu, w tym tworzenie kolejek, zasoby używane i hello stan hello operacji.</span><span class="sxs-lookup"><span data-stu-id="177da-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="177da-132">Dziennik operacyjny JSON ciągi zawierać elementy wymienione w poniższej tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="177da-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="177da-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="177da-133">Name</span></span> | <span data-ttu-id="177da-134">Opis</span><span class="sxs-lookup"><span data-stu-id="177da-134">Description</span></span>
------- | -------
<span data-ttu-id="177da-135">Identyfikator działania</span><span class="sxs-lookup"><span data-stu-id="177da-135">ActivityId</span></span> | <span data-ttu-id="177da-136">Wewnętrzny identyfikator używany do śledzenia</span><span class="sxs-lookup"><span data-stu-id="177da-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="177da-137">EventName</span><span class="sxs-lookup"><span data-stu-id="177da-137">EventName</span></span> | <span data-ttu-id="177da-138">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="177da-138">Operation name</span></span>           
<span data-ttu-id="177da-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="177da-139">resourceId</span></span> | <span data-ttu-id="177da-140">Identyfikator zasobu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="177da-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="177da-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="177da-141">SubscriptionId</span></span> | <span data-ttu-id="177da-142">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="177da-142">Subscription ID</span></span>
<span data-ttu-id="177da-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="177da-143">EventTimeString</span></span> | <span data-ttu-id="177da-144">Czas operacji</span><span class="sxs-lookup"><span data-stu-id="177da-144">Operation time</span></span>
<span data-ttu-id="177da-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="177da-145">EventProperties</span></span> | <span data-ttu-id="177da-146">Właściwości operacji</span><span class="sxs-lookup"><span data-stu-id="177da-146">Operation properties</span></span>
<span data-ttu-id="177da-147">Stan</span><span class="sxs-lookup"><span data-stu-id="177da-147">Status</span></span> | <span data-ttu-id="177da-148">Stan operacji</span><span class="sxs-lookup"><span data-stu-id="177da-148">Operation status</span></span>
<span data-ttu-id="177da-149">Obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="177da-149">Caller</span></span> | <span data-ttu-id="177da-150">Obiekt wywołujący operacji (Azure portalu lub zarządzania klienta)</span><span class="sxs-lookup"><span data-stu-id="177da-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="177da-151">category</span><span class="sxs-lookup"><span data-stu-id="177da-151">category</span></span> | <span data-ttu-id="177da-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="177da-152">OperationalLogs</span></span>

<span data-ttu-id="177da-153">Poniżej przedstawiono przykładowy dziennik operacyjny ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="177da-153">Here's an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="177da-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="177da-154">Next steps</span></span>

<span data-ttu-id="177da-155">Odwiedź powitania po toolearn łącza więcej o magistrali usług:</span><span class="sxs-lookup"><span data-stu-id="177da-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="177da-156">Wprowadzenie tooService magistrali</span><span class="sxs-lookup"><span data-stu-id="177da-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="177da-157">Rozpoczynanie pracy z usługą Service Bus</span><span class="sxs-lookup"><span data-stu-id="177da-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
