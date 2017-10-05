---
title: "Azure zmiany rozmiaru puli partii rozpoczęcia zdarzenia | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące zmiany rozmiaru puli partii rozpoczęcia zdarzenia."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="2871b-103">Zdarzenie rozpoczęcia zmiany rozmiaru puli</span><span class="sxs-lookup"><span data-stu-id="2871b-103">Pool resize start event</span></span>

 <span data-ttu-id="2871b-104">To zdarzenie jest emitowany rozpoczęcie rozmiaru puli.</span><span class="sxs-lookup"><span data-stu-id="2871b-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="2871b-105">Ponieważ zmiany rozmiaru puli jest zdarzenie asynchroniczne, można oczekiwać, że zdarzenie ukończenia zmiany rozmiaru puli na obliczanie po zakończeniu operacji zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="2871b-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="2871b-106">W poniższym przykładzie przedstawiono treści zdarzenia rozpoczęcia zmiany rozmiaru puli do puli zmiany rozmiaru z zakresu od 0 do 2 węzłów z ręcznej zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="2871b-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="2871b-107">Element</span><span class="sxs-lookup"><span data-stu-id="2871b-107">Element</span></span>|<span data-ttu-id="2871b-108">Typ</span><span class="sxs-lookup"><span data-stu-id="2871b-108">Type</span></span>|<span data-ttu-id="2871b-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2871b-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="2871b-110">poolId</span><span class="sxs-lookup"><span data-stu-id="2871b-110">poolId</span></span>|<span data-ttu-id="2871b-111">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2871b-111">String</span></span>|<span data-ttu-id="2871b-112">Identyfikator puli.</span><span class="sxs-lookup"><span data-stu-id="2871b-112">The id of the pool.</span></span>|
|<span data-ttu-id="2871b-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="2871b-113">nodeDeallocationOption</span></span>|<span data-ttu-id="2871b-114">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2871b-114">String</span></span>|<span data-ttu-id="2871b-115">Określa, kiedy można usunąć węzłów z puli, jeśli rozmiar puli będzie zmniejszany.</span><span class="sxs-lookup"><span data-stu-id="2871b-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="2871b-116">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="2871b-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="2871b-117">**requeue** — Przerwij wykonywane zadania i requeue je.</span><span class="sxs-lookup"><span data-stu-id="2871b-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="2871b-118">Zadania zostaną ponownie uruchomione, gdy zadanie jest włączone.</span><span class="sxs-lookup"><span data-stu-id="2871b-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="2871b-119">Usuń węzły zaraz po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="2871b-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="2871b-120">**przerwanie** — przerwania uruchomionych zadań.</span><span class="sxs-lookup"><span data-stu-id="2871b-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="2871b-121">Zadania nie zostaną uruchomione ponownie.</span><span class="sxs-lookup"><span data-stu-id="2871b-121">The tasks will not run again.</span></span> <span data-ttu-id="2871b-122">Usuń węzły zaraz po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="2871b-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="2871b-123">**taskcompletion** — Zezwalaj na aktualnie wykonywanych zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="2871b-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="2871b-124">Nie planuj nowych zadań czasu oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="2871b-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="2871b-125">Usuń węzły, po zakończeniu wykonywania wszystkich zadań.</span><span class="sxs-lookup"><span data-stu-id="2871b-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="2871b-126">**Retaineddata** — Zezwalaj na aktualnie wykonywanych zadań do wykonania, a następnie poczekaj na zakończenie wszystkich zadań okresów przechowywania danych wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="2871b-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="2871b-127">Nie planuj nowych zadań czasu oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="2871b-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="2871b-128">Usuń węzły, gdy wygasły wszystkich okresów przechowywania zadań.</span><span class="sxs-lookup"><span data-stu-id="2871b-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="2871b-129">Wartość domyślna to requeue.</span><span class="sxs-lookup"><span data-stu-id="2871b-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="2871b-130">Jeśli jest zwiększenie rozmiaru puli, wartość jest równa **nieprawidłowy**.</span><span class="sxs-lookup"><span data-stu-id="2871b-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="2871b-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="2871b-131">currentDedicated</span></span>|<span data-ttu-id="2871b-132">Int32</span><span class="sxs-lookup"><span data-stu-id="2871b-132">Int32</span></span>|<span data-ttu-id="2871b-133">Liczba węzłów obliczeniowych aktualnie przypisane do puli.</span><span class="sxs-lookup"><span data-stu-id="2871b-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="2871b-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="2871b-134">targetDedicated</span></span>|<span data-ttu-id="2871b-135">Int32</span><span class="sxs-lookup"><span data-stu-id="2871b-135">Int32</span></span>|<span data-ttu-id="2871b-136">Liczba węzłów obliczeniowych, które są wymagane dla puli.</span><span class="sxs-lookup"><span data-stu-id="2871b-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="2871b-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="2871b-137">enableAutoScale</span></span>|<span data-ttu-id="2871b-138">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2871b-138">Bool</span></span>|<span data-ttu-id="2871b-139">Określa, czy rozmiar puli automatycznie dostosowuje się wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="2871b-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="2871b-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="2871b-140">isAutoPool</span></span>|<span data-ttu-id="2871b-141">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2871b-141">Bool</span></span>|<span data-ttu-id="2871b-142">Speficies czy puli został utworzony za pomocą mechanizmu AutoPool zadania.</span><span class="sxs-lookup"><span data-stu-id="2871b-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
