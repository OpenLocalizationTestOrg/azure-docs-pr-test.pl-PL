---
title: "aaaEnable diagnostyczne dla partii zdarzeń - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="00d2f-103">Rejestrowanie zdarzeń diagnostycznych oceny i monitorowania rozwiązań partii</span><span class="sxs-lookup"><span data-stu-id="00d2f-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="00d2f-104">Podobnie jak w przypadku wielu usług Azure, hello usługa partia zadań emituje dla niektórych zasobów podczas hello okres istnienia zasobu hello zdarzenia dziennika.</span><span class="sxs-lookup"><span data-stu-id="00d2f-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="00d2f-105">Można Włącz partii zadań Azure dzienników diagnostycznych toorecord zdarzenia dla zasobów, takich jak pule i zadań, a następnie użyj hello dzienników diagnostycznych oceny i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="00d2f-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="00d2f-106">Tworzenie zdarzeń, takich jak puli, Usuń puli, uruchamiania zadań zadanie ukończone i inne są wyświetlane w partii dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="00d2f-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="00d2f-107">W tym artykule omówiono rejestrowania zdarzeń dla samych zasobach konta usługi partia zadań, nie zadania i dane wyjściowe zadań.</span><span class="sxs-lookup"><span data-stu-id="00d2f-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="00d2f-108">Aby uzyskać więcej informacji na temat przechowywania danych wyjściowych hello zadań i zadań, zobacz [danych wyjściowych i zadań utrwalić partii zadań Azure](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="00d2f-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="00d2f-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="00d2f-109">Prerequisites</span></span>
* [<span data-ttu-id="00d2f-110">Konto usługi partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="00d2f-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="00d2f-111">konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="00d2f-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="00d2f-112">dzienniki diagnostyczne partii toopersist, należy utworzyć konta usługi Azure Storage, w którym Azure będą przechowywane dzienniki hello.</span><span class="sxs-lookup"><span data-stu-id="00d2f-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="00d2f-113">To konto magazynu można określić podczas możesz [włączyć rejestrowanie diagnostyczne](#enable-diagnostic-logging) dla Twojego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="00d2f-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="00d2f-114">Witaj konta magazynu, możesz określić, że po włączeniu zbierania dzienników jest hello sam nie jako hello tooin określonego konta magazynu połączone [pakietów aplikacji](batch-application-packages.md) i [trwałości danych wyjściowych zadania](batch-task-output.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="00d2f-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="00d2f-115">Jesteś **obciążona** hello dane przechowywane na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="00d2f-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="00d2f-116">W tym hello dzienników diagnostycznych omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="00d2f-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="00d2f-117">Należy o tym pamiętać podczas projektowania sieci [logowania zasady przechowywania](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="00d2f-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="00d2f-118">Włączanie rejestrowania diagnostycznego</span><span class="sxs-lookup"><span data-stu-id="00d2f-118">Enable diagnostic logging</span></span>
<span data-ttu-id="00d2f-119">Rejestrowanie diagnostyczne nie jest włączone domyślnie dla Twojego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="00d2f-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="00d2f-120">Musisz jawnie włączyć rejestrowanie diagnostyczne dla każdego konta usługi partia zadań, które chcesz toomonitor:</span><span class="sxs-lookup"><span data-stu-id="00d2f-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="00d2f-121">Jak tooenable zbierania dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="00d2f-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="00d2f-122">Zalecamy przeczytanie hello pełne [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain artykułu zrozumienia nie tylko sposób rejestrowania tooenable, ale hello dziennika kategorii obsługiwane przez hello różne usługi platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="00d2f-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="00d2f-123">Na przykład w partii zadań Azure obsługuje obecnie jedną kategorię dziennika: **dzienniki usługi**.</span><span class="sxs-lookup"><span data-stu-id="00d2f-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="00d2f-124">Dzienniki usługi</span><span class="sxs-lookup"><span data-stu-id="00d2f-124">Service Logs</span></span>
<span data-ttu-id="00d2f-125">Dzienniki usługi usługi partia zadań Azure zawiera zdarzenia emitowane przez usługi partia zadań Azure hello okres istnienia hello zasobu partii puli lub zadania.</span><span class="sxs-lookup"><span data-stu-id="00d2f-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="00d2f-126">Każde zdarzenie emitowane przez partię są przechowywane w hello określone konto magazynu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="00d2f-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="00d2f-127">Na przykład to jest treść hello próbki **puli utworzyć zdarzenia**:</span><span class="sxs-lookup"><span data-stu-id="00d2f-127">For example, this is hello body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="00d2f-128">Każda jednostka zdarzenia znajduje się w JSON pliku w hello określono konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="00d2f-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="00d2f-129">Jeśli chcesz tooaccess hello dzienniki bezpośrednio, warto zapoznać się z tooreview hello [schematu dzienników diagnostycznych na koncie magazynu hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="00d2f-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="00d2f-130">Usługa dziennika zdarzeń</span><span class="sxs-lookup"><span data-stu-id="00d2f-130">Service Log events</span></span>
<span data-ttu-id="00d2f-131">Witaj usługa partia zadań emituje obecnie hello następujące zdarzenia logowania do usługi.</span><span class="sxs-lookup"><span data-stu-id="00d2f-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="00d2f-132">Ta lista nie może być pełne, ponieważ dodatkowe zdarzenia mogły zostać dodane od momentu ostatniej aktualizacji w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="00d2f-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="00d2f-133">**Usługa dziennika zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="00d2f-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="00d2f-134">[Tworzenie puli][pool_create]</span><span class="sxs-lookup"><span data-stu-id="00d2f-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="00d2f-135">[Start usuwania puli][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="00d2f-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="00d2f-136">[Usuwanie puli ukończone][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="00d2f-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="00d2f-137">[Początkowy rozmiar puli][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="00d2f-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="00d2f-138">[Zmiana rozmiaru puli ukończone][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="00d2f-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="00d2f-139">[Rozpoczęcia zadania][task_start]</span><span class="sxs-lookup"><span data-stu-id="00d2f-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="00d2f-140">[Zadania ukończone][task_complete]</span><span class="sxs-lookup"><span data-stu-id="00d2f-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="00d2f-141">[Niepowodzenie zadania][task_fail]</span><span class="sxs-lookup"><span data-stu-id="00d2f-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="00d2f-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="00d2f-142">Next steps</span></span>
<span data-ttu-id="00d2f-143">Dodanie toostoring zdarzeń dziennik diagnostyczny na koncie magazynu Azure, możesz również strumienia partii usługi dziennika zdarzeń tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md)i wysyła je za[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00d2f-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="00d2f-144">Strumień dzienników diagnostycznych platformy Azure tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="00d2f-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="00d2f-145">Strumienia partii zdarzeń diagnostycznych toohello wysoce skalowalna Usługa transferu danych, usługa Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="00d2f-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="00d2f-146">Centra zdarzeń może obsługiwać miliony zdarzeń na sekundę, który można przekształcić i magazynu przy użyciu dowolnego dostawcy analiz w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="00d2f-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="00d2f-147">Analizowanie Azure dzienników diagnostycznych przy użyciu analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="00d2f-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="00d2f-148">Wyślij tooLog Twojego dzienniki diagnostyczne analizy, w którym można analizować je w portalu Operations Management Suite (OMS) hello, lub wyeksportować je do analizy w programie Excel lub usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="00d2f-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
