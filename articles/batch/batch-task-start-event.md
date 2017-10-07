---
title: "AAA \"zdarzenia uruchamiania zadań partii zadań Azure | Dokumentacja firmy Microsoft\""
description: "Odwołanie do zadania wsadowego rozpoczęcia zdarzenia."
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="d2624-103">Zdarzenia uruchamiania zadań</span><span class="sxs-lookup"><span data-stu-id="d2624-103">Task start event</span></span>

 <span data-ttu-id="d2624-104">To zdarzenie jest emitowany po zadania zaplanowane toostart w węźle obliczeń przez hello harmonogram.</span><span class="sxs-lookup"><span data-stu-id="d2624-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="d2624-105">Należy pamiętać, że jeśli zadanie hello jest ponowione lub umieszczony w kolejce to zdarzenie będzie obliczanie ponownie hello tego samego zadania, ale hello liczba ponownych prób i zadań w systemie będą odpowiednio aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="d2624-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="d2624-106">Witaj poniższy przykład przedstawia hello treści zdarzenia uruchamiania zadań.</span><span class="sxs-lookup"><span data-stu-id="d2624-106">hello following example shows hello body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="d2624-107">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="d2624-107">Element name</span></span>|<span data-ttu-id="d2624-108">Typ</span><span class="sxs-lookup"><span data-stu-id="d2624-108">Type</span></span>|<span data-ttu-id="d2624-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d2624-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d2624-110">Identyfikator zadania</span><span class="sxs-lookup"><span data-stu-id="d2624-110">jobId</span></span>|<span data-ttu-id="d2624-111">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d2624-111">String</span></span>|<span data-ttu-id="d2624-112">Identyfikator Hello hello zadania zawierające hello zadań.</span><span class="sxs-lookup"><span data-stu-id="d2624-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="d2624-113">id</span><span class="sxs-lookup"><span data-stu-id="d2624-113">id</span></span>|<span data-ttu-id="d2624-114">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d2624-114">String</span></span>|<span data-ttu-id="d2624-115">Identyfikator Hello hello zadań.</span><span class="sxs-lookup"><span data-stu-id="d2624-115">hello id of hello task.</span></span>|
|<span data-ttu-id="d2624-116">taskType</span><span class="sxs-lookup"><span data-stu-id="d2624-116">taskType</span></span>|<span data-ttu-id="d2624-117">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d2624-117">String</span></span>|<span data-ttu-id="d2624-118">Typ Hello hello zadań.</span><span class="sxs-lookup"><span data-stu-id="d2624-118">hello type of hello task.</span></span> <span data-ttu-id="d2624-119">Może to być "JobManager" i wskazujący, że jest to zadanie Menedżer zadania lub "User" i wskazujący, że nie jest zadanie Menedżer zadania.</span><span class="sxs-lookup"><span data-stu-id="d2624-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="d2624-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="d2624-120">systemTaskVersion</span></span>|<span data-ttu-id="d2624-121">Int32</span><span class="sxs-lookup"><span data-stu-id="d2624-121">Int32</span></span>|<span data-ttu-id="d2624-122">Jest to licznik wewnętrzny ponownych prób hello zadania.</span><span class="sxs-lookup"><span data-stu-id="d2624-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="d2624-123">Wewnętrznie hello usługa partia zadań. Spróbuj ponownie tooaccount zadania, dla przejściowych problemów.</span><span class="sxs-lookup"><span data-stu-id="d2624-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="d2624-124">Te problemy mogą obejmować wewnętrzny planowania toorecover błędy lub prób z węzłami obliczeniowymi w złym stanie.</span><span class="sxs-lookup"><span data-stu-id="d2624-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="d2624-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="d2624-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="d2624-126">Typ złożony</span><span class="sxs-lookup"><span data-stu-id="d2624-126">Complex Type</span></span>|<span data-ttu-id="d2624-127">Zawiera informacje o węźle obliczeń hello, na które hello zadanie zostało wykonane.</span><span class="sxs-lookup"><span data-stu-id="d2624-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="d2624-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="d2624-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="d2624-129">Typ złożony</span><span class="sxs-lookup"><span data-stu-id="d2624-129">Complex Type</span></span>|<span data-ttu-id="d2624-130">Określa, że to zadanie hello jest wiele wystąpień zadań wymagających wielu węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d2624-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="d2624-131">Zobacz [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d2624-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="d2624-132">ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d2624-132">constraints</span></span>](#constraints)|<span data-ttu-id="d2624-133">Typ złożony</span><span class="sxs-lookup"><span data-stu-id="d2624-133">Complex Type</span></span>|<span data-ttu-id="d2624-134">ograniczenia wykonywania Hello stosowane toothis zadań.</span><span class="sxs-lookup"><span data-stu-id="d2624-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="d2624-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="d2624-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="d2624-136">Typ złożony</span><span class="sxs-lookup"><span data-stu-id="d2624-136">Complex Type</span></span>|<span data-ttu-id="d2624-137">Zawiera informacje dotyczące wykonywania hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="d2624-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="d2624-138"><a name="nodeInfo"></a>nodeInfo</span><span class="sxs-lookup"><span data-stu-id="d2624-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="d2624-139">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="d2624-139">Element name</span></span>|<span data-ttu-id="d2624-140">Typ</span><span class="sxs-lookup"><span data-stu-id="d2624-140">Type</span></span>|<span data-ttu-id="d2624-141">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d2624-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d2624-142">poolId</span><span class="sxs-lookup"><span data-stu-id="d2624-142">poolId</span></span>|<span data-ttu-id="d2624-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d2624-143">String</span></span>|<span data-ttu-id="d2624-144">Identyfikator Hello hello puli, na które hello zadanie zostało wykonane.</span><span class="sxs-lookup"><span data-stu-id="d2624-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="d2624-145">ID. węzła</span><span class="sxs-lookup"><span data-stu-id="d2624-145">nodeId</span></span>|<span data-ttu-id="d2624-146">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d2624-146">String</span></span>|<span data-ttu-id="d2624-147">Identyfikator Hello hello węzła, na którym hello zadanie zostało wykonane.</span><span class="sxs-lookup"><span data-stu-id="d2624-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="d2624-148"><a name="multiInstanceSettings"></a>multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="d2624-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="d2624-149">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="d2624-149">Element name</span></span>|<span data-ttu-id="d2624-150">Typ</span><span class="sxs-lookup"><span data-stu-id="d2624-150">Type</span></span>|<span data-ttu-id="d2624-151">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d2624-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d2624-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="d2624-152">numberOfInstances</span></span>|<span data-ttu-id="d2624-153">int</span><span class="sxs-lookup"><span data-stu-id="d2624-153">Int</span></span>|<span data-ttu-id="d2624-154">Liczba Hello wymagane przez zadanie hello węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d2624-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="d2624-155"><a name="constraints"></a>ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d2624-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="d2624-156">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="d2624-156">Element name</span></span>|<span data-ttu-id="d2624-157">Typ</span><span class="sxs-lookup"><span data-stu-id="d2624-157">Type</span></span>|<span data-ttu-id="d2624-158">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d2624-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d2624-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="d2624-159">maxTaskRetryCount</span></span>|<span data-ttu-id="d2624-160">Int32</span><span class="sxs-lookup"><span data-stu-id="d2624-160">Int32</span></span>|<span data-ttu-id="d2624-161">Witaj maksymalną liczbę razy hello zadanie może zostać podjęta ponowna próba wykonania.</span><span class="sxs-lookup"><span data-stu-id="d2624-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="d2624-162">Hello usługa partia zadań ponawia zadanie, jeśli jego kod zakończenia jest różna od zera.</span><span class="sxs-lookup"><span data-stu-id="d2624-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="d2624-163">Należy pamiętać, że ta wartość określa, w szczególności hello liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="d2624-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="d2624-164">Usługa partia zadań Hello ponowi zadania hello raz, a następnie może ponów się toothis limit.</span><span class="sxs-lookup"><span data-stu-id="d2624-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="d2624-165">Na przykład hello maksymalnej liczby ponownych prób to 3, partii próbuje zadanie w górę too4 razy (jedna próba początkowej i 3 ponowne próby).</span><span class="sxs-lookup"><span data-stu-id="d2624-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="d2624-166">Jeśli hello maksymalna liczba ponowień to 0, hello usługa partia zadań nie ponów próbę wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="d2624-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="d2624-167">Jeśli hello maksymalna liczba ponowień to -1, usługa partia zadań hello ponowi próbę zadania bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="d2624-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="d2624-168">Witaj, wartość domyślna to 0 (brak ponownych prób).</span><span class="sxs-lookup"><span data-stu-id="d2624-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="d2624-169"><a name="executionInfo"></a>executionInfo</span><span class="sxs-lookup"><span data-stu-id="d2624-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="d2624-170">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="d2624-170">Element name</span></span>|<span data-ttu-id="d2624-171">Typ</span><span class="sxs-lookup"><span data-stu-id="d2624-171">Type</span></span>|<span data-ttu-id="d2624-172">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d2624-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d2624-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="d2624-173">retryCount</span></span>|<span data-ttu-id="d2624-174">Int32</span><span class="sxs-lookup"><span data-stu-id="d2624-174">Int32</span></span>|<span data-ttu-id="d2624-175">Witaj liczba zadań hello było ponawiane przez hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="d2624-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="d2624-176">zadanie Hello jest podjęta, jeśli kończy działanie z kodem zakończenia różną od zera, zapasowej toohello określony MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="d2624-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
