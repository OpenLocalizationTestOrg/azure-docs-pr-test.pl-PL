---
title: "Włączanie rejestrowania diagnostycznego partii zdarzeń - Azure | Dokumentacja firmy Microsoft"
description: "Rejestruj i analizowanie dzienników diagnostycznych zdarzeń dla zasobów konta partii zadań Azure, takich jak pule i zadania."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7bc6fd9921ab0f2374ace33ea5c1ab93a78f860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="55dce-103">Rejestrowanie zdarzeń diagnostycznych oceny i monitorowania rozwiązań partii</span><span class="sxs-lookup"><span data-stu-id="55dce-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="55dce-104">Podobnie jak w przypadku wielu usług Azure, usługa partia zadań emituje dziennika zdarzeń dla niektórych zasobów przez cały okres istnienia zasobu.</span><span class="sxs-lookup"><span data-stu-id="55dce-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="55dce-105">Można Włączanie dzienników diagnostycznych partii zadań Azure rejestrowanie zdarzeń dla zasobów, takich jak pule i zadań, a następnie za pomocą dzienników diagnostycznych oceny i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="55dce-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="55dce-106">Tworzenie zdarzeń, takich jak puli, Usuń puli, uruchamiania zadań zadanie ukończone i inne są wyświetlane w partii dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="55dce-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="55dce-107">W tym artykule omówiono rejestrowania zdarzeń dla samych zasobach konta usługi partia zadań, nie zadania i dane wyjściowe zadań.</span><span class="sxs-lookup"><span data-stu-id="55dce-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="55dce-108">Aby uzyskać więcej informacji na temat przechowywania danych wyjściowych zadań i zadań, zobacz [danych wyjściowych i zadań utrwalić partii zadań Azure](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="55dce-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="55dce-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55dce-109">Prerequisites</span></span>
* [<span data-ttu-id="55dce-110">Konto usługi partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="55dce-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="55dce-111">konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="55dce-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="55dce-112">Aby utrwalić dzienników diagnostycznych partii, należy utworzyć konta usługi Azure Storage, w którym Azure będą przechowywane dzienniki.</span><span class="sxs-lookup"><span data-stu-id="55dce-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="55dce-113">To konto magazynu można określić podczas możesz [włączyć rejestrowanie diagnostyczne](#enable-diagnostic-logging) dla Twojego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="55dce-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="55dce-114">Konto magazynu, możesz określić, że po włączeniu zbierania dzienników nie jest taka sama jak połączonym koncie magazynu określonym w [pakietów aplikacji](batch-application-packages.md) i [trwałości danych wyjściowych zadania](batch-task-output.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="55dce-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="55dce-115">Jesteś **obciążona** dane przechowywane na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="55dce-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="55dce-116">W tym dzienniki diagnostyczne omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="55dce-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="55dce-117">Należy o tym pamiętać podczas projektowania sieci [logowania zasady przechowywania](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="55dce-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="55dce-118">Włączanie rejestrowania diagnostycznego</span><span class="sxs-lookup"><span data-stu-id="55dce-118">Enable diagnostic logging</span></span>
<span data-ttu-id="55dce-119">Rejestrowanie diagnostyczne nie jest włączone domyślnie dla Twojego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="55dce-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="55dce-120">Musisz jawnie włączyć rejestrowanie diagnostyczne dla każdego konta usługi partia zadań, które chcesz monitorować:</span><span class="sxs-lookup"><span data-stu-id="55dce-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="55dce-121">Jak włączyć kolekcję dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="55dce-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="55dce-122">Zalecamy przeczytanie pełnego [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykuł, aby poznać nie tylko sposób włączania rejestrowania, ale kategorie dziennika obsługiwanych przez różne usługi platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="55dce-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="55dce-123">Na przykład w partii zadań Azure obsługuje obecnie jedną kategorię dziennika: **dzienniki usługi**.</span><span class="sxs-lookup"><span data-stu-id="55dce-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="55dce-124">Dzienniki usługi</span><span class="sxs-lookup"><span data-stu-id="55dce-124">Service Logs</span></span>
<span data-ttu-id="55dce-125">Dzienniki usługi usługi partia zadań Azure zawiera zdarzenia emitowane przez usługi partia zadań Azure przez cały okres istnienia zasobu partii puli lub zadania.</span><span class="sxs-lookup"><span data-stu-id="55dce-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="55dce-126">Każdego zdarzenia emitowane przez partię znajduje się na określonym koncie magazynu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="55dce-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="55dce-127">Na przykład to jest treść próbki **puli utworzyć zdarzenia**:</span><span class="sxs-lookup"><span data-stu-id="55dce-127">For example, this is the body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="55dce-128">Każda jednostka zdarzenia znajduje się w pliku JSON w określonym koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="55dce-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="55dce-129">Jeśli chcesz uzyskać bezpośredni dostęp dzienniki, możesz przejrzeć [schematu dzienników diagnostycznych na koncie magazynu](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="55dce-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="55dce-130">Usługa dziennika zdarzeń</span><span class="sxs-lookup"><span data-stu-id="55dce-130">Service Log events</span></span>
<span data-ttu-id="55dce-131">Usługa partia zadań emituje obecnie następujące zdarzenia logowania do usługi.</span><span class="sxs-lookup"><span data-stu-id="55dce-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="55dce-132">Ta lista nie może być pełne, ponieważ dodatkowe zdarzenia mogły zostać dodane od momentu ostatniej aktualizacji w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="55dce-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="55dce-133">**Usługa dziennika zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="55dce-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="55dce-134">[Tworzenie puli][pool_create]</span><span class="sxs-lookup"><span data-stu-id="55dce-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="55dce-135">[Start usuwania puli][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="55dce-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="55dce-136">[Usuwanie puli ukończone][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="55dce-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="55dce-137">[Początkowy rozmiar puli][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="55dce-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="55dce-138">[Zmiana rozmiaru puli ukończone][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="55dce-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="55dce-139">[Rozpoczęcia zadania][task_start]</span><span class="sxs-lookup"><span data-stu-id="55dce-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="55dce-140">[Zadania ukończone][task_complete]</span><span class="sxs-lookup"><span data-stu-id="55dce-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="55dce-141">[Niepowodzenie zadania][task_fail]</span><span class="sxs-lookup"><span data-stu-id="55dce-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="55dce-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55dce-142">Next steps</span></span>
<span data-ttu-id="55dce-143">Oprócz zdarzeń diagnostycznych dziennika są przechowywane na koncie magazynu Azure, możesz również strumienia zdarzeń logowania do usługi partii [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md)i wyślij je do [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55dce-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="55dce-144">Strumienia Azure dzienników diagnostycznych do usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="55dce-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="55dce-145">Strumienia zdarzeń diagnostycznych partii do wysoce skalowalna Usługa transferu danych, usługa Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="55dce-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="55dce-146">Centra zdarzeń może obsługiwać miliony zdarzeń na sekundę, który można przekształcić i magazynu przy użyciu dowolnego dostawcy analiz w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="55dce-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="55dce-147">Analizowanie Azure dzienników diagnostycznych przy użyciu analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="55dce-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="55dce-148">Wysyłanie dzienników diagnostycznych do analizy dzienników, w którym można analizować je w portalu Operations Management Suite (OMS), lub wyeksportować je do analizy w programie Excel lub usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="55dce-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
