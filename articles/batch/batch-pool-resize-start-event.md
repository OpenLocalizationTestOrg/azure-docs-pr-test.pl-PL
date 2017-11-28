---
title: "AAA \"zmiany rozmiaru puli partii zadań Azure rozpoczęcia zdarzenia | Dokumentacja firmy Microsoft\""
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="ce3ee-103">Zdarzenie rozpoczęcia zmiany rozmiaru puli</span><span class="sxs-lookup"><span data-stu-id="ce3ee-103">Pool resize start event</span></span>

 <span data-ttu-id="ce3ee-104">To zdarzenie jest emitowany rozpoczęcie rozmiaru puli.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="ce3ee-105">Ponieważ zmiany rozmiaru puli hello jest zdarzenie asynchroniczne, może spodziewać się zakończeniu toobe zdarzenie ukończenia zmiany rozmiaru puli wysyłanego po hello operacja zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="ce3ee-106">Zmień rozmiar Hello poniższy przykład, że pokazuje hello treści zdarzenia rozpoczęcia zmiany rozmiaru puli do zmiany rozmiaru puli z 0 węzłów too2 ręcznego.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="ce3ee-107">Element</span><span class="sxs-lookup"><span data-stu-id="ce3ee-107">Element</span></span>|<span data-ttu-id="ce3ee-108">Typ</span><span class="sxs-lookup"><span data-stu-id="ce3ee-108">Type</span></span>|<span data-ttu-id="ce3ee-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ce3ee-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="ce3ee-110">poolId</span><span class="sxs-lookup"><span data-stu-id="ce3ee-110">poolId</span></span>|<span data-ttu-id="ce3ee-111">Ciąg</span><span class="sxs-lookup"><span data-stu-id="ce3ee-111">String</span></span>|<span data-ttu-id="ce3ee-112">Identyfikator Hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="ce3ee-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="ce3ee-113">nodeDeallocationOption</span></span>|<span data-ttu-id="ce3ee-114">Ciąg</span><span class="sxs-lookup"><span data-stu-id="ce3ee-114">String</span></span>|<span data-ttu-id="ce3ee-115">Określa, kiedy węzły mogą zostać usunięte z puli hello, jeśli hello rozmiar puli będzie zmniejszany.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="ce3ee-116">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="ce3ee-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="ce3ee-117">**requeue** — Przerwij wykonywane zadania i requeue je.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="ce3ee-118">Witaj zadania zostaną ponownie uruchomione, gdy zadanie hello jest włączone.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="ce3ee-119">Usuń węzły zaraz po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="ce3ee-120">**przerwanie** — przerwania uruchomionych zadań.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="ce3ee-121">Witaj zadania nie zostaną ponownie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-121">hello tasks will not run again.</span></span> <span data-ttu-id="ce3ee-122">Usuń węzły zaraz po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="ce3ee-123">**taskcompletion** — Zezwalaj na aktualnie uruchomione zadania toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="ce3ee-124">Nie planuj nowych zadań czasu oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="ce3ee-125">Usuń węzły, po zakończeniu wykonywania wszystkich zadań.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="ce3ee-126">**Retaineddata** — Zezwalaj na aktualnie uruchomione zadania toocomplete, a następnie zaczekaj na zakończenie wszystkich zadań tooexpire okresów przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="ce3ee-127">Nie planuj nowych zadań czasu oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="ce3ee-128">Usuń węzły, gdy wygasły wszystkich okresów przechowywania zadań.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="ce3ee-129">Wartość domyślna Hello jest requeue.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="ce3ee-130">Jeśli rozmiar puli hello jest zwiększenie, hello wartość zbyt**nieprawidłowy**.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="ce3ee-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="ce3ee-131">currentDedicated</span></span>|<span data-ttu-id="ce3ee-132">Int32</span><span class="sxs-lookup"><span data-stu-id="ce3ee-132">Int32</span></span>|<span data-ttu-id="ce3ee-133">Witaj liczba węzłów obliczeniowych aktualnie przypisane toohello puli.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="ce3ee-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="ce3ee-134">targetDedicated</span></span>|<span data-ttu-id="ce3ee-135">Int32</span><span class="sxs-lookup"><span data-stu-id="ce3ee-135">Int32</span></span>|<span data-ttu-id="ce3ee-136">Witaj liczba węzłów obliczeniowych, które są żądane hello puli.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="ce3ee-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="ce3ee-137">enableAutoScale</span></span>|<span data-ttu-id="ce3ee-138">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="ce3ee-138">Bool</span></span>|<span data-ttu-id="ce3ee-139">Określa, czy rozmiar puli hello automatycznie dostosowuje się wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="ce3ee-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="ce3ee-140">isAutoPool</span></span>|<span data-ttu-id="ce3ee-141">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="ce3ee-141">Bool</span></span>|<span data-ttu-id="ce3ee-142">Speficies czy puli hello został utworzony za pomocą mechanizmu AutoPool zadania.</span><span class="sxs-lookup"><span data-stu-id="ce3ee-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
