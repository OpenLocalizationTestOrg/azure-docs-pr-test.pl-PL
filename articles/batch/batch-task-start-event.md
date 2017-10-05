---
title: "Usługi Azure event rozpoczęcia zadania wsadowego | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="31a3f-103">Zdarzenia uruchamiania zadań</span><span class="sxs-lookup"><span data-stu-id="31a3f-103">Task start event</span></span>

 <span data-ttu-id="31a3f-104">To zdarzenie jest emitowany, gdy zadanie zostało zaplanowane do uruchomienia w węźle obliczeń przez harmonogram.</span><span class="sxs-lookup"><span data-stu-id="31a3f-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="31a3f-105">Należy pamiętać, że jeśli zadanie zostanie ponowiona lub umieszczony w kolejce to zdarzenie będzie obliczanie ponownie do tego samego zadania, ale liczby ponownych prób i zadań w systemie zostanie odpowiednio aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="31a3f-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="31a3f-106">W poniższym przykładzie przedstawiono treść zadania rozpoczęcia zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="31a3f-106">The following example shows the body of a task start event.</span></span>

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

|<span data-ttu-id="31a3f-107">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="31a3f-107">Element name</span></span>|<span data-ttu-id="31a3f-108">Typ</span><span class="sxs-lookup"><span data-stu-id="31a3f-108">Type</span></span>|<span data-ttu-id="31a3f-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="31a3f-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="31a3f-110">Identyfikator zadania</span><span class="sxs-lookup"><span data-stu-id="31a3f-110">jobId</span></span>|<span data-ttu-id="31a3f-111">Ciąg</span><span class="sxs-lookup"><span data-stu-id="31a3f-111">String</span></span>|<span data-ttu-id="31a3f-112">Identyfikator zadania zawierającego zadanie.</span><span class="sxs-lookup"><span data-stu-id="31a3f-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="31a3f-113">id</span><span class="sxs-lookup"><span data-stu-id="31a3f-113">id</span></span>|<span data-ttu-id="31a3f-114">Ciąg</span><span class="sxs-lookup"><span data-stu-id="31a3f-114">String</span></span>|<span data-ttu-id="31a3f-115">Identyfikator zadania.</span><span class="sxs-lookup"><span data-stu-id="31a3f-115">The id of the task.</span></span>|
|<span data-ttu-id="31a3f-116">taskType</span><span class="sxs-lookup"><span data-stu-id="31a3f-116">taskType</span></span>|<span data-ttu-id="31a3f-117">Ciąg</span><span class="sxs-lookup"><span data-stu-id="31a3f-117">String</span></span>|<span data-ttu-id="31a3f-118">Typ zadania.</span><span class="sxs-lookup"><span data-stu-id="31a3f-118">The type of the task.</span></span> <span data-ttu-id="31a3f-119">Może to być "JobManager" i wskazujący, że jest to zadanie Menedżer zadania lub "User" i wskazujący, że nie jest zadanie Menedżer zadania.</span><span class="sxs-lookup"><span data-stu-id="31a3f-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="31a3f-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="31a3f-120">systemTaskVersion</span></span>|<span data-ttu-id="31a3f-121">Int32</span><span class="sxs-lookup"><span data-stu-id="31a3f-121">Int32</span></span>|<span data-ttu-id="31a3f-122">Jest to licznik ponownych prób wewnętrzny dla zadania.</span><span class="sxs-lookup"><span data-stu-id="31a3f-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="31a3f-123">Wewnętrznie usługa partia zadań. Spróbuj ponownie zadania konta dla przejściowych problemów.</span><span class="sxs-lookup"><span data-stu-id="31a3f-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="31a3f-124">Te problemy mogą zawierać błędy wewnętrzne planowania lub próbuje odzyskać z węzłami w złym stanie przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="31a3f-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="31a3f-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="31a3f-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="31a3f-126">Typ złożony</span><span class="sxs-lookup"><span data-stu-id="31a3f-126">Complex Type</span></span>|<span data-ttu-id="31a3f-127">Zawiera informacje o węźle obliczeń, na którym uruchomiono zadanie.</span><span class="sxs-lookup"><span data-stu-id="31a3f-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="31a3f-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="31a3f-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="31a3f-129">Typ złożony</span><span class="sxs-lookup"><span data-stu-id="31a3f-129">Complex Type</span></span>|<span data-ttu-id="31a3f-130">Określa, że zadanie jest wiele wystąpień zadań wymagających wielu węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="31a3f-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="31a3f-131">Zobacz [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="31a3f-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="31a3f-132">ograniczenia</span><span class="sxs-lookup"><span data-stu-id="31a3f-132">constraints</span></span>](#constraints)|<span data-ttu-id="31a3f-133">Typ złożony</span><span class="sxs-lookup"><span data-stu-id="31a3f-133">Complex Type</span></span>|<span data-ttu-id="31a3f-134">Ograniczenia wykonanie, które są stosowane do tego zadania.</span><span class="sxs-lookup"><span data-stu-id="31a3f-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="31a3f-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="31a3f-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="31a3f-136">Typ złożony</span><span class="sxs-lookup"><span data-stu-id="31a3f-136">Complex Type</span></span>|<span data-ttu-id="31a3f-137">Zawiera informacje dotyczące wykonywania tego zadania.</span><span class="sxs-lookup"><span data-stu-id="31a3f-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="31a3f-138"><a name="nodeInfo"></a>nodeInfo</span><span class="sxs-lookup"><span data-stu-id="31a3f-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="31a3f-139">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="31a3f-139">Element name</span></span>|<span data-ttu-id="31a3f-140">Typ</span><span class="sxs-lookup"><span data-stu-id="31a3f-140">Type</span></span>|<span data-ttu-id="31a3f-141">Uwagi</span><span class="sxs-lookup"><span data-stu-id="31a3f-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="31a3f-142">poolId</span><span class="sxs-lookup"><span data-stu-id="31a3f-142">poolId</span></span>|<span data-ttu-id="31a3f-143">Ciąg</span><span class="sxs-lookup"><span data-stu-id="31a3f-143">String</span></span>|<span data-ttu-id="31a3f-144">Identyfikator puli, na którym uruchomiono zadanie.</span><span class="sxs-lookup"><span data-stu-id="31a3f-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="31a3f-145">ID. węzła</span><span class="sxs-lookup"><span data-stu-id="31a3f-145">nodeId</span></span>|<span data-ttu-id="31a3f-146">Ciąg</span><span class="sxs-lookup"><span data-stu-id="31a3f-146">String</span></span>|<span data-ttu-id="31a3f-147">Identyfikator węzła, na którym uruchomiono zadanie.</span><span class="sxs-lookup"><span data-stu-id="31a3f-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="31a3f-148"><a name="multiInstanceSettings"></a>multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="31a3f-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="31a3f-149">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="31a3f-149">Element name</span></span>|<span data-ttu-id="31a3f-150">Typ</span><span class="sxs-lookup"><span data-stu-id="31a3f-150">Type</span></span>|<span data-ttu-id="31a3f-151">Uwagi</span><span class="sxs-lookup"><span data-stu-id="31a3f-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="31a3f-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="31a3f-152">numberOfInstances</span></span>|<span data-ttu-id="31a3f-153">int</span><span class="sxs-lookup"><span data-stu-id="31a3f-153">Int</span></span>|<span data-ttu-id="31a3f-154">Liczba węzłów obliczeń wymagana przez zadanie.</span><span class="sxs-lookup"><span data-stu-id="31a3f-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="31a3f-155"><a name="constraints"></a>ograniczenia</span><span class="sxs-lookup"><span data-stu-id="31a3f-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="31a3f-156">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="31a3f-156">Element name</span></span>|<span data-ttu-id="31a3f-157">Typ</span><span class="sxs-lookup"><span data-stu-id="31a3f-157">Type</span></span>|<span data-ttu-id="31a3f-158">Uwagi</span><span class="sxs-lookup"><span data-stu-id="31a3f-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="31a3f-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="31a3f-159">maxTaskRetryCount</span></span>|<span data-ttu-id="31a3f-160">Int32</span><span class="sxs-lookup"><span data-stu-id="31a3f-160">Int32</span></span>|<span data-ttu-id="31a3f-161">Maksymalna liczba powtórzeń zadania mogą być ponowiona.</span><span class="sxs-lookup"><span data-stu-id="31a3f-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="31a3f-162">Usługa partia zadań ponawia zadanie, jeśli jego kod zakończenia jest różna od zera.</span><span class="sxs-lookup"><span data-stu-id="31a3f-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="31a3f-163">Należy pamiętać, że ta wartość określa, w szczególności liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="31a3f-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="31a3f-164">Usługa partia zadań ponowi zadania raz i może następnie ponów próbę wykonania tego limitu.</span><span class="sxs-lookup"><span data-stu-id="31a3f-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="31a3f-165">Na przykład jeśli maksymalna liczba ponowień prób partii zadanie 3 do 4 godziny (jedna próba początkowej i 3 ponowne próby).</span><span class="sxs-lookup"><span data-stu-id="31a3f-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="31a3f-166">Jeśli maksymalna liczba ponowień to 0, usługa partia zadań nie ponów próbę wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="31a3f-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="31a3f-167">Jeśli maksymalna liczba ponowień to -1, usługa partia zadań ponawia próbę zadania bez ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="31a3f-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="31a3f-168">Wartość domyślna to 0 (brak ponownych prób).</span><span class="sxs-lookup"><span data-stu-id="31a3f-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="31a3f-169"><a name="executionInfo"></a>executionInfo</span><span class="sxs-lookup"><span data-stu-id="31a3f-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="31a3f-170">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="31a3f-170">Element name</span></span>|<span data-ttu-id="31a3f-171">Typ</span><span class="sxs-lookup"><span data-stu-id="31a3f-171">Type</span></span>|<span data-ttu-id="31a3f-172">Uwagi</span><span class="sxs-lookup"><span data-stu-id="31a3f-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="31a3f-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="31a3f-173">retryCount</span></span>|<span data-ttu-id="31a3f-174">Int32</span><span class="sxs-lookup"><span data-stu-id="31a3f-174">Int32</span></span>|<span data-ttu-id="31a3f-175">Ile razy zadanie było ponawiane przez usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="31a3f-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="31a3f-176">Zadanie jest podjęta, jeśli kończy działanie z kodem zakończenia różną od zera, do określonego MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="31a3f-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
