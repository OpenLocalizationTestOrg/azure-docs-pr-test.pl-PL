---
title: "Uruchom partii zadań Azure obciążeń na ekonomicznego niskiego priorytetu maszyny wirtualne (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie obsługi administracyjnej maszyn wirtualnych niskiego priorytetu będzie zmniejszenie kosztów obciążeń partii zadań Azure."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="b8d1e-103">Niskiego priorytetu maszyn wirtualnych za pomocą partii (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="b8d1e-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="b8d1e-104">Partia zadań Azure oferuje małej priorty maszyn wirtualnych (VM) będzie zmniejszenie kosztów obciążeń partii.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-104">Azure Batch offers low-priorty virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="b8d1e-105">Maszyny wirtualne o niskim priorytecie umożliwiają nowe typy obciążeń partii, zapewniając dużo mocy obliczeniowej, który jest również ekonomiczny.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="b8d1e-106">Maszyny wirtualne niskiego priorytetu korzystać z nadwyżki zdolności produkcyjnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="b8d1e-107">Po określeniu niskiego priorytetu maszyny wirtualne w Twojej puli partii zadań Azure automatycznie można użyć tego nadwyżka, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="b8d1e-108">Rozwiązanie dla przy użyciu maszyn wirtualnych o niskim priorytecie jest, że tych maszyn wirtualnych może być wywłaszczony gdy nie zdolności nadwyżki nie jest dostępny w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-108">The tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="b8d1e-109">Z tego powodu niskiego priorytetu maszyny wirtualne są najbardziej odpowiednie dla pewnych typów obciążeń.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="b8d1e-110">Użyj maszyn wirtualnych niskiego priorytetu partii i przetwarzania asynchronicznego obciążeń, których czas ukończenia zadania są elastyczne i praca będzie rozmieszczona na wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>

<span data-ttu-id="b8d1e-111">Maszyny wirtualne o niskim priorytecie są znacznie tańszy niż dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="b8d1e-112">Aby uzyskać szczegółowe informacje o cenach, zobacz [cennik partii](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="b8d1e-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="b8d1e-113">Dodatkowe omówienie niskiego priorytetu maszyn wirtualnych, można znaleźć w sekcji powiadomienia post blogu: [partii obliczeniowych w ułamku ceny](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="b8d1e-113">For an additional discussion of low-priority VMs, see the blog post announcement: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8d1e-114">Maszyny wirtualne o niskim priorytecie są obecnie w wersji zapoznawczej i są dostępne tylko dla obciążeń działających w partii.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="b8d1e-115">Przypadki użycia dla maszyn wirtualnych o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="b8d1e-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="b8d1e-116">Podane właściwości niskiego priorytetu maszyny wirtualne, jakie obciążenia może i nie można ich używać?</span><span class="sxs-lookup"><span data-stu-id="b8d1e-116">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="b8d1e-117">Ogólnie rzecz biorąc obciążeń przetwarzania wsadowego są świetnie sprawdza się, ponieważ zadania są podzielone na wiele zadań równoległych lub ma wiele zadań, które skalowana w poziomie i rozproszone na wielu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="b8d1e-118">Aby zapewnić maksymalne użycie nadwyżki pojemności na platformie Azure, odpowiedniego zadania można skalować w poziomie.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-118">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="b8d1e-119">Czasami maszyny wirtualne mogą być niedostępne lub będzie być wywłaszczony, co spowoduje zmniejszenie wydajności dla zadań i może prowadzić do przerwania zadań i powtórki.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="b8d1e-120">W związku z tym należy elastycznych w czasie, które można wykonać, aby uruchomić zadania.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-120">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="b8d1e-121">Zadania z zadaniami dłużej może to mieć wpływ na więcej przerwania.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="b8d1e-122">Jeśli długotrwałych zadań implementować tworzenie punktów kontrolnych do zapisania postępu, ponieważ są one wykonywane, następnie wpływ przerwania byłby znacznie mniej.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-122">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="b8d1e-123">Zadania związane z krótszy czas wykonywania zazwyczaj najlepiej z maszynami wirtualnymi niskiego priorytetu wpływ przerwania jest znacznie mniej.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-123">Tasks with shorter execution times tend to work best with low-priority VMs as the impact of interruption is far less.</span></span>

-   <span data-ttu-id="b8d1e-124">Długotrwałych zadań MPI, które korzystają z wieloma maszynami wirtualnymi nie są dobrze nadają się do użycia niskiego priorytetu maszyny wirtualne zgodnie z jedną wywłaszczone maszyny Wirtualnej prawdopodobnie spowoduje całą pracę o ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-124">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs as one preempted VM will likely lead to the whole job having to be run again.</span></span>

<span data-ttu-id="b8d1e-125">Przykładowe przypadki użycia przetwarzania wsadowego dobrze nadaje się do użycia niskiego priorytetu maszyny wirtualne to:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-125">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="b8d1e-126">**Projektowanie i testowanie**: W szczególności, jeśli są opracowywane na dużą skalę rozwiązania znaczne oszczędności może istnieć.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="b8d1e-127">Wszystkie typy testowania można korzystać, ale testów obciążenia na dużą skalę i testowania regresji są doskonałe używa.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="b8d1e-128">**Uzupełniające pojemności na żądanie**: niskiego priorytetu maszyn wirtualnych może służyć do uzupełnienia regular dedykowanych maszyn wirtualnych — Jeśli jest dostępny, zadania można skalować i z tego powodu ukończyć przyspieszają obniżenia kosztów; nie jest dostępny, używana jest linia bazowa dedykowanych maszyn wirtualnych są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="b8d1e-129">**Czas wykonania zadania elastyczne**: w przypadku elastyczność w zadaniach czasu trzeba wykonać, a następnie potencjalnych porzucania pojemności może następować; z uwzględnieniem niskiego priorytetu maszyny wirtualne zadania będą często wykonywane szybsze i tańsze.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-129">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="b8d1e-130">Pule partii może być skonfigurowana do używania niskiego priorytetu maszyny wirtualne na kilka sposobów, w zależności od elastyczność w czasie wykonywania zadania:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-130">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="b8d1e-131">Maszyny wirtualne niskiego priorytetu może służyć wyłącznie w puli i partii zostanie odzyskana po prostu żadnych preempted pojemności, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="b8d1e-132">Jest to sposób najtańszej można uruchomić zadania, które są używane tylko niskiego priorytetu maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-132">This is the cheapest way to execute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="b8d1e-133">Maszyny wirtualne niskiego priorytetu może służyć w połączeniu z linii bazowej stałym dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="b8d1e-134">Stała liczba dedykowanych maszyn wirtualnych zapewnia, że jest zawsze niektórych wydajności, aby zachować postęp zadania.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-134">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="b8d1e-135">Może istnieć dynamiczne mieszanego dedykowanej i niskiego priorytetu maszyn wirtualnych, tak, aby tańsze niskiego priorytetu maszyny wirtualnej wyłącznie są używane, jeśli jest dostępny, ale dedykowanych maszyn wirtualnych cenach full są skalowane w górę na żądanie, aby zachować minimalną ilość zdolności do prowadzenia postęp zadania.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required, to keep a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="b8d1e-136">Obsługa partii dla maszyn wirtualnych o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="b8d1e-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="b8d1e-137">Partia zadań Azure oferuje kilka możliwości, które ułatwiają korzystanie i korzystają z maszyn wirtualnych o niskim priorytecie:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="b8d1e-138">Pule partii może zawierać zarówno dedykowanych maszyn wirtualnych, jak i niskiego priorytetu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="b8d1e-139">Podczas tworzenia puli lub zmienić w dowolnym momencie dla istniejącej puli, przy użyciu operacji zmiany rozmiaru jawne lub automatyczne skalowanie można określić liczbę każdego typu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="b8d1e-140">Przesyłanie zadań i zadań może pozostać bez zmian i nie trzeba zajmować się typy maszyn wirtualnych w puli.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-140">Job and task submission can remain unchanged and do not need to be concerned with the VM types in the pool.</span></span> <span data-ttu-id="b8d1e-141">Istnieje również możliwość dostępna pula całkowicie używają maszyn wirtualnych niskiego priorytetu uruchomienie zadania jako tanio, jak to możliwe, ale pokrętła zapasowej dedykowanych maszyn wirtualnych, jeśli pojemność spadnie poniżej minimalnej, aby zachować zadania uruchomione.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-141">It is also possible to have a pool completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="b8d1e-142">Pule partii automatycznie przejść do docelowej liczby maszyn wirtualnych o niskim priorytecie.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-142">Batch pools automatically seek to the target number of low-priority VMs.</span></span> <span data-ttu-id="b8d1e-143">Jeśli maszyny wirtualne są zastępowane, partii będzie podejmować próby Zastąp utracone pojemności i zwracany do obiektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-143">If VMs are preempted, then Batch will attempt to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="b8d1e-144">W przypadku zadania zostanie przerwane wykryje partii i automatycznie requeue zadań, aby ponownie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-144">In the case of tasks being interrupted, Batch will detect and automatically requeue tasks to be run again.</span></span>

-   <span data-ttu-id="b8d1e-145">Maszyny wirtualne niskiego priorytetu ma limit przydziału rdzeni, która różni się od dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="b8d1e-146">Oferta dla maszyn wirtualnych niskiego priorytetu jest wyższy niż dedykowanych maszyn wirtualnych, ponieważ koszt niskiego priorytetu maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-146">The quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="b8d1e-147">Zobacz [partii usługi przydziały i limity](batch-quota-limit.md#resource-quotas) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="b8d1e-148">Niskiego priorytetu maszyny wirtualne nie są obsługiwane dla konta usługi partia zadań, w których ustawiono tryb alokacji puli [subskrypcji użytkownika](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="b8d1e-148">Low-priority VMs are not currently supported for Batch accounts where the pool allocation mode is set to [User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="b8d1e-149">Tworzenie i aktualizowanie pul</span><span class="sxs-lookup"><span data-stu-id="b8d1e-149">Create and update pools</span></span>

<span data-ttu-id="b8d1e-150">Pula usługi partia zadań może zawierać dedykowanych i niskiego priorytetu maszyny wirtualne (zwaną także jako węzły obliczeniowe).</span><span class="sxs-lookup"><span data-stu-id="b8d1e-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="b8d1e-151">Można ustawić docelowy liczba węzłów obliczeniowych dla dedykowanych i niskiego priorytetu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="b8d1e-152">Docelowy liczba węzłów określa liczbę maszyn wirtualnych mają w puli.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="b8d1e-153">Na przykład aby utworzyć pulę przy użyciu usługi w chmurze Azure maszyn wirtualnych z elementem docelowym 5 dedykowanych maszyn wirtualnych i 20 niskiego priorytetu maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="b8d1e-154">Aby utworzyć pulę przy użyciu maszyn wirtualnych platformy Azure (w tym przypadku maszyn wirtualnych systemu Linux) z docelowym 5 dedykowanych maszyn wirtualnych i 20 niskiego priorytetu maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="b8d1e-155">Bieżąca liczba węzłów można uzyskać dedykowane i niskiego priorytetu maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="b8d1e-156">Węzły puli mają właściwości, aby wskazać, czy węzeł jest dedykowanej lub niskiego priorytetu maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="b8d1e-157">Co najmniej jeden węzeł w puli są zastępowane, operację listy węzłów w puli nadal będzie zwracać tych węzłów, bieżąca liczba węzłów niskiego priorytetu pozostaną niezmienione, ale te węzły będą mieć stanu ustawioną **przeniesione** Stan.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, the current number of low-priority nodes will remain unchanged, but those nodes will have their state set to the **Preempted** state.</span></span> <span data-ttu-id="b8d1e-158">Partii spróbuje znaleźć zastąpienia maszyn wirtualnych, a w razie powodzenia węzłów będzie przejście przez **tworzenie** , a następnie **uruchamianie** stanów, zanim staną się dostępne do wykonania zadania, podobnie jak nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-158">Batch will attempt to find replacement VMs and, if successful, the nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="b8d1e-159">Skalowanie pulę zawierającą maszyn wirtualnych o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="b8d1e-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="b8d1e-160">Podobnie jak w przypadku pul wyłącznie składające się z dedykowanych maszyn wirtualnych, jest możliwość skalowania zawierających maszyny wirtualne o niskim priorytecie przez wywołanie metody zmiany rozmiaru lub przy użyciu automatycznego skalowania puli.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-160">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using auto-scale.</span></span>

<span data-ttu-id="b8d1e-161">Drugi parametr opcjonalny, który aktualizuje wartość przyjmuje operacji zmiany rozmiaru puli **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-161">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="b8d1e-162">Formuła automatycznego skalowania puli obsługuje niskiego priorytetu maszyn wirtualnych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-162">The pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="b8d1e-163">Można pobrać lub ustawić wartość zmiennej zdefiniowanej przez usługę **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-163">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="b8d1e-164">Można uzyskać wartości zmiennej zdefiniowanej przez usługę **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-164">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="b8d1e-165">Można uzyskać wartości zmiennej zdefiniowanej przez usługę **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-165">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="b8d1e-166">Ta zmienna zwraca liczbę węzłów w stanie preempted i umożliwia skalowanie w górę lub w dół Liczba dedykowanych węzłów, w zależności od liczby węzłów wywłaszczone, które są niedostępne.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-166">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="b8d1e-167">Zadań i zadań</span><span class="sxs-lookup"><span data-stu-id="b8d1e-167">Jobs and tasks</span></span>

<span data-ttu-id="b8d1e-168">Zadań i zadań wymaga bardzo małego obsługi węzłów niskiego priorytetu; obsługiwane jest tylko wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-168">Jobs and tasks require very little support for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="b8d1e-169">Właściwość JobManagerTask zadania ma nową właściwość **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-169">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="b8d1e-170">Jeśli ta właściwość ma wartość true, można zaplanować zadanie Menedżer zadania w węźle dedykowanej lub niskim priorytecie.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-170">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="b8d1e-171">Jeśli ta właściwość ma wartość false, do dedykowanych węzła tylko zostanie zaplanowane zadanie Menedżer zadania.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-171">If this property is false, the job manager task will be scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="b8d1e-172">[Zmiennej środowiskowej](batch-compute-node-environment-variables.md) jest dostępna w aplikacji zadań, dzięki czemu można określić, czy jest uruchomiona w węźle niskiego priorytetu lub dedykowanych.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-172">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="b8d1e-173">Zmienna środowiskowa jest AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-173">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="b8d1e-174">Obsługa wywłaszczania</span><span class="sxs-lookup"><span data-stu-id="b8d1e-174">Handling preemption</span></span>

<span data-ttu-id="b8d1e-175">Maszyny wirtualne od czasu do czasu może być wywłaszczony; w takim przypadku partii wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-175">VMs may occasionally be preempted; when this happens, Batch does the following:</span></span>

-   <span data-ttu-id="b8d1e-176">Preempted maszyny wirtualne mają ich stan aktualizacji do **przeniesione**.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-176">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="b8d1e-177">Jeśli zadania zostały uruchomione na maszynach wirtualnych węzła wywłaszczone, te zadania są umieszczony w kolejce i uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-177">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="b8d1e-178">Maszyna wirtualna skutecznie zostanie usunięty, co może prowadzić do wszystkich danych przechowywanych lokalnie na utratę maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-178">The VM is effectively deleted, leading to any data stored locally on the VM being lost.</span></span>
-   <span data-ttu-id="b8d1e-179">Pula stale próbuje nawiązać połączenie docelowej liczba dostępnych węzłów niskiego priorytetu.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-179">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="b8d1e-180">Po znalezieniu pojemności zastępczy Zachowaj ich identyfikatory węzłów, ale są ponownie inicjowane, pośrednictwa **tworzenie** i **uruchamianie** stwierdza, zanim staną się dostępne do planowania zadań.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="b8d1e-181">Wywłaszczanie liczniki są dostępne jako metrykę w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-181">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="b8d1e-182">Metryki</span><span class="sxs-lookup"><span data-stu-id="b8d1e-182">Metrics</span></span>

<span data-ttu-id="b8d1e-183">Dostępne są nowe metryki [portalu Azure](https://portal.azure.com) dla węzłów o niskim priorytecie.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-183">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="b8d1e-184">Te metryki są:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-184">These metrics are:</span></span>

- <span data-ttu-id="b8d1e-185">Liczba węzłów o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="b8d1e-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="b8d1e-186">Liczby rdzeni o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="b8d1e-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="b8d1e-187">Wywłaszczone liczba węzłów</span><span class="sxs-lookup"><span data-stu-id="b8d1e-187">Preempted Node Count</span></span>

<span data-ttu-id="b8d1e-188">Aby wyświetlić metryki w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="b8d1e-188">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="b8d1e-189">Przejdź do konta partii zadań w portalu i wyświetlenia ustawień konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-189">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="b8d1e-190">Wybierz **metryki** z **monitorowanie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-190">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="b8d1e-191">Wybrać metryki chcesz z **dostępne metryki** listy.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-191">Select the metrics you desire from the **Available Metrics** list.</span></span>

![Metryki dla węzłów o niskim priorytecie](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="b8d1e-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8d1e-193">Next steps</span></span>

* <span data-ttu-id="b8d1e-194">Przeczytaj artykuł [Batch feature overview for developers](batch-api-basics.md) (Omówienie funkcji usługi Batch dla deweloperów) zawierający informacje kluczowe dla wszystkich osób przygotowujących się do korzystania z usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-194">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="b8d1e-195">Ten artykuł zawiera bardziej szczegółowe informacje o zasobach usługi Batch, takich jak pule, węzły i zadania oraz wielu funkcjach API, których można używać podczas kompilowania aplikacji usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-195">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="b8d1e-196">Dowiedz się więcej o [interfejsach API i narzędziach usługi Batch](batch-apis-tools.md) umożliwiających tworzenie rozwiązań usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="b8d1e-196">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
