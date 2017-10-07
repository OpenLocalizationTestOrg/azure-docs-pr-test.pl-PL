---
title: "aaaRun partii zadań Azure obciążenie ekonomicznego niskiego priorytetu maszyny wirtualne (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprovision niskiego priorytetu maszyny wirtualne tooreduce hello koszt obciążeń partii zadań Azure."
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
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="f01a9-103">Niskiego priorytetu maszyn wirtualnych za pomocą partii (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="f01a9-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="f01a9-104">Partia zadań Azure oferuje małej priorty maszynach wirtualnych (VM) tooreduce hello koszt obciążeń partii.</span><span class="sxs-lookup"><span data-stu-id="f01a9-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="f01a9-105">Maszyny wirtualne o niskim priorytecie umożliwiają nowe typy obciążeń partii, zapewniając dużo mocy obliczeniowej, który jest również ekonomiczny.</span><span class="sxs-lookup"><span data-stu-id="f01a9-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="f01a9-106">Maszyny wirtualne niskiego priorytetu korzystać z nadwyżki zdolności produkcyjnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f01a9-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="f01a9-107">Po określeniu niskiego priorytetu maszyny wirtualne w Twojej puli partii zadań Azure automatycznie można użyć tego nadwyżka, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="f01a9-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="f01a9-108">Hello rozwiązanie dla przy użyciu maszyn wirtualnych o niskim priorytecie jest, że tych maszyn wirtualnych może być wywłaszczony gdy nie zdolności nadwyżki nie jest dostępny w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="f01a9-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="f01a9-109">Z tego powodu niskiego priorytetu maszyny wirtualne są najbardziej odpowiednie dla pewnych typów obciążeń.</span><span class="sxs-lookup"><span data-stu-id="f01a9-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="f01a9-110">Użyj maszyn wirtualnych niskiego priorytetu partii i przetwarzania asynchronicznego obciążeń, których czas ukończenia zadania hello jest elastyczny i pracy hello jest rozmieszczona na wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="f01a9-111">Maszyny wirtualne o niskim priorytecie są znacznie tańszy niż dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="f01a9-112">Aby uzyskać szczegółowe informacje o cenach, zobacz [cennik partii](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="f01a9-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="f01a9-113">Dodatkowe omówienie niskiego priorytetu maszyn wirtualnych, można znaleźć w sekcji anons blogu hello: [partii obliczeniowych w ułamku cen hello](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="f01a9-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f01a9-114">Maszyny wirtualne o niskim priorytecie są obecnie w wersji zapoznawczej i są dostępne tylko dla obciążeń działających w partii.</span><span class="sxs-lookup"><span data-stu-id="f01a9-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="f01a9-115">Przypadki użycia dla maszyn wirtualnych o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="f01a9-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="f01a9-116">Biorąc pod uwagę charakterystykę hello niskiego priorytetu maszyn wirtualnych, jakie obciążenia może i nie można ich używać?</span><span class="sxs-lookup"><span data-stu-id="f01a9-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="f01a9-117">Ogólnie rzecz biorąc obciążeń przetwarzania wsadowego są świetnie sprawdza się, ponieważ zadania są podzielone na wiele zadań równoległych lub ma wiele zadań, które skalowana w poziomie i rozproszone na wielu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="f01a9-118">Użycie toomaximize nadwyżki zdolności produkcyjnych Azure, odpowiednich zadań można skalować w poziomie.</span><span class="sxs-lookup"><span data-stu-id="f01a9-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="f01a9-119">Czasami maszyny wirtualne mogą być niedostępne lub będzie być wywłaszczony, co spowoduje zmniejszenie wydajności dla zadań i może spowodować przerwanie tootask i powtórki.</span><span class="sxs-lookup"><span data-stu-id="f01a9-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="f01a9-120">Zadania w związku z tym muszą być elastyczne w czasie hello, które podejmują toorun.</span><span class="sxs-lookup"><span data-stu-id="f01a9-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="f01a9-121">Zadania z zadaniami dłużej może to mieć wpływ na więcej przerwania.</span><span class="sxs-lookup"><span data-stu-id="f01a9-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="f01a9-122">Jeśli długotrwałych zadań implementować postępu toosave punkty kontrolne, ponieważ są one wykonywane, następnie wpływ przerwania byłby znacznie mniej.</span><span class="sxs-lookup"><span data-stu-id="f01a9-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="f01a9-123">Zadania związane z krótszy czas wykonywania zwykle toowork najlepiej z maszynami wirtualnymi niskiego priorytetu wpływ hello przerwania jest znacznie mniej.</span><span class="sxs-lookup"><span data-stu-id="f01a9-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="f01a9-124">Długotrwałych zadań MPI, które korzystają z wieloma maszynami wirtualnymi nie są dobrze nadają się toouse maszyn wirtualnych niskiego priorytetu jako jedna maszyna wirtualna, które są zastępowane będzie prawdopodobnie realizacji toohello całą pracę o toobe, uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="f01a9-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="f01a9-125">Przykłady przetwarzania wsadowego Użyj przypadków toouse dobrze nadają się niskiego priorytetu maszyny wirtualne są:</span><span class="sxs-lookup"><span data-stu-id="f01a9-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="f01a9-126">**Projektowanie i testowanie**: W szczególności, jeśli są opracowywane na dużą skalę rozwiązania znaczne oszczędności może istnieć.</span><span class="sxs-lookup"><span data-stu-id="f01a9-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="f01a9-127">Wszystkie typy testowania można korzystać, ale testów obciążenia na dużą skalę i testowania regresji są doskonałe używa.</span><span class="sxs-lookup"><span data-stu-id="f01a9-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="f01a9-128">**Uzupełniające pojemności na żądanie**: niskiego priorytetu maszyn wirtualnych może służyć do uzupełnienia regular dedykowanych maszyn wirtualnych — Jeśli jest dostępny, zadania można skalować i z tego powodu ukończyć przyspieszają obniżenia kosztów; nie jest dostępny, hello linii bazowej dedykowanych maszyn wirtualnych są dostępne.</span><span class="sxs-lookup"><span data-stu-id="f01a9-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="f01a9-129">**Czas wykonania zadania elastyczne**: Jeśli elastyczność w zadaniach czasu hello mieć toocomplete, a następnie potencjalnych porzucania pojemności może następować; jednak z hello dodawania zadań maszyn wirtualnych niskiego priorytetu będzie często działają szybciej i obniżenia kosztów.</span><span class="sxs-lookup"><span data-stu-id="f01a9-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="f01a9-130">Pule partii można toouse skonfigurowany czas wykonania zadania maszyn wirtualnych niskiego priorytetu na kilka sposobów, w zależności od elastyczność hello:</span><span class="sxs-lookup"><span data-stu-id="f01a9-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="f01a9-131">Maszyny wirtualne niskiego priorytetu może służyć wyłącznie w puli i partii zostanie odzyskana po prostu żadnych preempted pojemności, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="f01a9-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="f01a9-132">Jest to hello najtańszej sposób tooexecute zadania, ponieważ są używane tylko niskiego priorytetu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="f01a9-133">Maszyny wirtualne niskiego priorytetu może służyć w połączeniu z linii bazowej stałym dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="f01a9-134">Witaj stała liczba dedykowanych maszyn wirtualnych zapewnia, że istnieje zawsze niektórych tookeep pojemności postęp zadania.</span><span class="sxs-lookup"><span data-stu-id="f01a9-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="f01a9-135">Może istnieć dynamiczne mieszanego dedykowanej i niskiego priorytetu maszyn wirtualnych, dzięki czemu tańsze VMs niskiego priorytetu wyłącznie są używane, jeśli jest dostępny, ale hello cenach pełnej dedykowanych maszyn wirtualnych są skalowane w górę na żądanie, tookeep minimalna ilość zadania hello tookeep dostępna pojemność postęp.</span><span class="sxs-lookup"><span data-stu-id="f01a9-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="f01a9-136">Obsługa partii dla maszyn wirtualnych o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="f01a9-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="f01a9-137">Partia zadań Azure oferuje kilka możliwości była tooconsume łatwe, które korzystają z maszyn wirtualnych o niskim priorytecie:</span><span class="sxs-lookup"><span data-stu-id="f01a9-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="f01a9-138">Pule partii może zawierać zarówno dedykowanych maszyn wirtualnych, jak i niskiego priorytetu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="f01a9-139">Liczba Hello każdego typu maszyny Wirtualnej można określić podczas tworzenia puli lub zmienić w dowolnym momencie dla istniejącej puli, przy użyciu operacji zmiany rozmiaru jawne hello lub automatyczne skalowanie.</span><span class="sxs-lookup"><span data-stu-id="f01a9-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="f01a9-140">Przesyłanie zadań i zadań może pozostać bez zmian i nie trzeba zajmować się hello typach maszyn wirtualnych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="f01a9-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="f01a9-141">Możliwe jest również możliwe toohave puli całkowicie Użyj niskiego priorytetu maszyny wirtualne toorun zadania jako tanio, jak to możliwe, ale pokrętła zapasowej dedykowanych maszyn wirtualnych Jeśli pojemność hello spadnie poniżej minimalnej, aby zachować zadania uruchomione.</span><span class="sxs-lookup"><span data-stu-id="f01a9-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="f01a9-142">Pule partii automatycznie wyszukiwać toohello docelowej liczby maszyn wirtualnych o niskim priorytecie.</span><span class="sxs-lookup"><span data-stu-id="f01a9-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="f01a9-143">Jeśli maszyny wirtualne są zastępowane, partii podejmie hello tooreplace utraty pojemności i zwracany toohello docelowej.</span><span class="sxs-lookup"><span data-stu-id="f01a9-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="f01a9-144">W przypadku hello zadania zostanie przerwane partii wykryje i automatycznie requeue toobe zadania, uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="f01a9-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="f01a9-145">Maszyny wirtualne niskiego priorytetu ma limit przydziału rdzeni, która różni się od dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="f01a9-146">Hello cudzysłowu dla maszyn wirtualnych niskiego priorytetu jest wyższy niż dedykowanych maszyn wirtualnych, ponieważ koszt niskiego priorytetu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="f01a9-147">Zobacz [partii usługi przydziały i limity](batch-quota-limit.md#resource-quotas) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f01a9-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="f01a9-148">Niskiego priorytetu maszyny wirtualne nie są obsługiwane dla konta usługi partia zadań, w którym tryb alokacji puli hello ustawiono zbyt[subskrypcji użytkownika](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="f01a9-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="f01a9-149">Tworzenie i aktualizowanie pul</span><span class="sxs-lookup"><span data-stu-id="f01a9-149">Create and update pools</span></span>

<span data-ttu-id="f01a9-150">Pula usługi partia zadań może zawierać dedykowanych i niskiego priorytetu maszyny wirtualne (również określonego tooas węzły obliczeniowe).</span><span class="sxs-lookup"><span data-stu-id="f01a9-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="f01a9-151">Można ustawić hello docelowej liczby węzłów obliczeniowych dedykowanych i niskiego priorytetu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="f01a9-152">Hello docelowej liczby węzłów Określa numer hello maszyn wirtualnych ma toohave hello puli.</span><span class="sxs-lookup"><span data-stu-id="f01a9-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="f01a9-153">Na przykład toocreate puli przy użyciu usługi w chmurze Azure maszyn wirtualnych z elementem docelowym 5 dedykowanych maszyn wirtualnych i 20 niskiego priorytetu maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="f01a9-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="f01a9-154">maszyny wirtualne i 20 niskiego priorytetu maszyny wirtualne w wersji dedykowanej toocreate puli przy użyciu maszyn wirtualnych platformy Azure (w tym przypadku maszyn wirtualnych systemu Linux) z docelowym 5:</span><span class="sxs-lookup"><span data-stu-id="f01a9-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="f01a9-155">Możesz też uzyskać hello bieżąca liczba węzłów dedykowanych i niskiego priorytetu maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="f01a9-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="f01a9-156">Węzły puli mają tooindicate właściwości, jeśli węzeł hello jest dedykowanej lub niskiego priorytetu maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f01a9-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="f01a9-157">Co najmniej jeden węzeł w puli są zastępowane, operację listy węzłów w puli nadal będzie zwracać tych węzłów hello bieżąca liczba węzłów niskiego priorytetu pozostaną niezmienione, ale te węzły będą mieć ich stan wartość toothe **przeniesione**stanu.</span><span class="sxs-lookup"><span data-stu-id="f01a9-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="f01a9-158">Wsadowe podejmie zastępczy toofind maszyn wirtualnych, a w przypadku powodzenia hello węzłów będzie przejście przez **tworzenie** , a następnie **uruchamianie** stanów, zanim staną się dostępne do wykonania zadania, podobnie jak nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="f01a9-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="f01a9-159">Skalowanie pulę zawierającą maszyn wirtualnych o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="f01a9-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="f01a9-160">Podobnie jak w przypadku pul wyłącznie składające się z dedykowanych maszyn wirtualnych, jest maszyn wirtualnych możliwe tooscale puli zawierającej niskim priorytecie przez wywołanie metody zmiany rozmiaru hello lub przy użyciu automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="f01a9-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="f01a9-161">Witaj operacji zmiany rozmiaru puli przyjmuje opcjonalny drugi parametr, który aktualizuje wartość **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="f01a9-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="f01a9-162">Formuła automatycznego skalowania puli Hello obsługuje niskiego priorytetu maszyn wirtualnych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f01a9-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="f01a9-163">Można pobrać lub ustawić hello wartość zmiennej hello zdefiniowane przez usługi **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="f01a9-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="f01a9-164">Można pobrać wartości hello hello zmiennej zdefiniowanej przez usługę **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="f01a9-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="f01a9-165">Można pobrać wartości hello hello zmiennej zdefiniowanej przez usługę **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="f01a9-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="f01a9-166">Ta zmienna zwraca hello liczby węzłów w hello wywłaszczone stanu i umożliwia skalowanie w górę lub w dół hello Liczba dedykowanych węzłów, w zależności od hello liczba węzłów wywłaszczone, które są niedostępne.</span><span class="sxs-lookup"><span data-stu-id="f01a9-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="f01a9-167">Zadań i zadań</span><span class="sxs-lookup"><span data-stu-id="f01a9-167">Jobs and tasks</span></span>

<span data-ttu-id="f01a9-168">Zadań i zadań wymaga bardzo małego obsługi węzłów niskiego priorytetu; obsługiwane jest tylko Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="f01a9-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="f01a9-169">Witaj JobManagerTask właściwości zadania ma nową właściwość **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="f01a9-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="f01a9-170">Jeśli ta właściwość ma wartość true, można zaplanować zadanie Menedżer zadania hello w węźle dedykowanej lub niskim priorytecie.</span><span class="sxs-lookup"><span data-stu-id="f01a9-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="f01a9-171">Jeśli ta właściwość ma wartość false, hello zadania Menedżera zadań będzie zaplanowane tooa tylko dedykowane węzła.</span><span class="sxs-lookup"><span data-stu-id="f01a9-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="f01a9-172">[Zmiennej środowiskowej](batch-compute-node-environment-variables.md) jest tooa dostępne zadania aplikacji, dzięki czemu można określić, czy jest uruchomiona w węźle niskiego priorytetu lub dedykowanych.</span><span class="sxs-lookup"><span data-stu-id="f01a9-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="f01a9-173">Zmienna środowiskowa Hello jest AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="f01a9-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="f01a9-174">Obsługa wywłaszczania</span><span class="sxs-lookup"><span data-stu-id="f01a9-174">Handling preemption</span></span>

<span data-ttu-id="f01a9-175">Maszyny wirtualne od czasu do czasu może być wywłaszczony; w takim przypadku partii hello następujące:</span><span class="sxs-lookup"><span data-stu-id="f01a9-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="f01a9-176">Witaj wywłaszczone maszyny wirtualne mają ich stan zaktualizowane**przeniesione**.</span><span class="sxs-lookup"><span data-stu-id="f01a9-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="f01a9-177">Jeśli zadania zostały uruchomione na hello przeniesiona węzła maszyn wirtualnych, te zadania są umieszczony w kolejce i uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="f01a9-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="f01a9-178">Hello wirtualna skutecznie zostanie usunięty, początkowe tooany dane przechowywane lokalnie na powitania utratę maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f01a9-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="f01a9-179">Pula Hello podejmuje stale tooreach hello docelowej liczby węzłów niskiego priorytetu dostępne.</span><span class="sxs-lookup"><span data-stu-id="f01a9-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="f01a9-180">Po znalezieniu pojemności zastępczy Zachowaj ich identyfikatory węzłów, ale są ponownie inicjowane, pośrednictwa **tworzenie** i **uruchamianie** stwierdza, zanim staną się dostępne do planowania zadań.</span><span class="sxs-lookup"><span data-stu-id="f01a9-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="f01a9-181">Wywłaszczanie liczniki są dostępne jako metrykę w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f01a9-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="f01a9-182">Metryki</span><span class="sxs-lookup"><span data-stu-id="f01a9-182">Metrics</span></span>

<span data-ttu-id="f01a9-183">Nowe metryki są dostępne w hello [portalu Azure](https://portal.azure.com) dla węzłów o niskim priorytecie.</span><span class="sxs-lookup"><span data-stu-id="f01a9-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="f01a9-184">Te metryki są:</span><span class="sxs-lookup"><span data-stu-id="f01a9-184">These metrics are:</span></span>

- <span data-ttu-id="f01a9-185">Liczba węzłów o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="f01a9-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="f01a9-186">Liczby rdzeni o niskim priorytecie</span><span class="sxs-lookup"><span data-stu-id="f01a9-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="f01a9-187">Wywłaszczone liczba węzłów</span><span class="sxs-lookup"><span data-stu-id="f01a9-187">Preempted Node Count</span></span>

<span data-ttu-id="f01a9-188">metryki tooview w hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="f01a9-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="f01a9-189">Przejdź tooyour konta usługi partia zadań w portalu hello i wyświetlić hello ustawień konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="f01a9-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="f01a9-190">Wybierz **metryki** z hello **monitorowanie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="f01a9-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="f01a9-191">Wybierz metryki hello chcesz z hello **dostępne metryki** listy.</span><span class="sxs-lookup"><span data-stu-id="f01a9-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![Metryki dla węzłów o niskim priorytecie](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="f01a9-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f01a9-193">Next steps</span></span>

* <span data-ttu-id="f01a9-194">Witaj odczytu [Przegląd funkcji partii dla deweloperów](batch-api-basics.md), ważne informacje dla każdego przygotowywanie toouse partii.</span><span class="sxs-lookup"><span data-stu-id="f01a9-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="f01a9-195">Witaj artykuł zawiera bardziej szczegółowe informacje o partii usługi zasobów, takich jak pule, węzłów, zadań i zadań i hello wiele funkcji interfejsu API, które można używać podczas tworzenia aplikacji partii.</span><span class="sxs-lookup"><span data-stu-id="f01a9-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="f01a9-196">Dowiedz się więcej o hello [narzędzia i interfejsy API partii](batch-apis-tools.md) dostępne do tworzenia rozwiązań partii.</span><span class="sxs-lookup"><span data-stu-id="f01a9-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
