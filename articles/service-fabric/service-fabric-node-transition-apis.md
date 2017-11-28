---
title: "aaaStart i Zatrzymaj tootest węzłów klastra Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse fault tootest iniekcji aplikacji usługi Service Fabric przez uruchamianie i zatrzymywanie węzłów klastra."
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="d1ff1-103">Zastępowanie hello API Przejście węzła hello uruchomić węzeł i zatrzymanie węzła interfejsów API</span><span class="sxs-lookup"><span data-stu-id="d1ff1-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="d1ff1-104">Co hello zatrzymanie węzła i uruchomić interfejsy API węzeł?</span><span class="sxs-lookup"><span data-stu-id="d1ff1-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="d1ff1-105">Hello zatrzymanie węzła API (zarządzany: [StopNodeAsync()][stopnode], programu PowerShell: [Stop-ServiceFabricNode][stopnodeps]) zatrzymuje węzła sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="d1ff1-106">Węzeł sieci szkieletowej usług to proces, nie maszyny Wirtualnej lub maszyny — hello maszyny Wirtualnej lub maszyny będą nadal działać.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="d1ff1-107">Witaj pozostałej części dokumentu hello "węzła" oznacza węzła sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="d1ff1-108">Zatrzymanie węzła umieszcza je w *zatrzymana* stanu, gdy nie jest członkiem klastra hello i nie może obsługiwać usługi, w związku z tym symulując *dół* węzła.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="d1ff1-109">Jest to przydatne wstrzykiwania błędów do tootest systemu hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="d1ff1-110">Hello Start API węzła (zarządzane: [StartNodeAsync()][startnode], programu PowerShell: [Start ServiceFabricNode][startnodeps]]) odwrócona hello zatrzymać API węzła  które łączy hello węzła tooa tyłu normalnym stanie.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="d1ff1-111">Dlaczego możemy je zastąpić?</span><span class="sxs-lookup"><span data-stu-id="d1ff1-111">Why are we replacing these?</span></span>

<span data-ttu-id="d1ff1-112">Jak opisano wcześniej, *zatrzymana* sieci szkieletowej usług węzeł jest węzłem, który został celowo docelowych przy użyciu hello API zatrzymanie węzła.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="d1ff1-113">A *dół* węzeł jest węzłem, który nie działa z jakiegokolwiek powodu (np. hello maszyny Wirtualnej lub maszyny jest wyłączone).</span><span class="sxs-lookup"><span data-stu-id="d1ff1-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="d1ff1-114">Z hello zatrzymanie węzła API hello systemu nie ujawnia toodifferentiate informacji między *zatrzymana* węzłów i *dół* węzłów.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="d1ff1-115">Ponadto niektóre błędy zwrócone przez te interfejsy API nie są jako opisową stać się.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="d1ff1-116">Na przykład wywoływania hello API zatrzymanie węzła na moduł już *zatrzymana* węzła zwróci błąd hello *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="d1ff1-117">To środowisko można lepiej.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-117">This experience could be improved.</span></span>

<span data-ttu-id="d1ff1-118">Ponadto węzła jest zatrzymana na czas trwania hello jest "nieskończone" do powitalne Start interfejs API węzeł zostanie wywołany.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="d1ff1-119">Znaleźliśmy to może spowodować problemy i mogą być podatne na błędy.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="d1ff1-120">Na przykład firma Microsoft w tym samouczku problemów gdzie użytkownika wywoływane hello zatrzymać API węzeł w węźle i następnie zapomniano o nim.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="d1ff1-121">Później, został jasne, czy węzeł hello miał *dół* lub *zatrzymana*.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="d1ff1-122">Wprowadzenie hello interfejsów API Przejście węzła</span><span class="sxs-lookup"><span data-stu-id="d1ff1-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="d1ff1-123">Uwzględniono te problemy powyżej w nowy zestaw interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="d1ff1-124">Hello nowy interfejs API Przejście węzła (zarządzany: [StartNodeTransitionAsync()][snt]) mogą być używane tootransition tooa węzła sieci szkieletowej usług *zatrzymana* stanu lub tootransition go z *zatrzymana* tooa stanu normalnego stanu.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="d1ff1-125">Należy pamiętać, że ten hello "Start" w nazwie hello hello interfejsu API nie odwołuje się toostarting węzła.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="d1ff1-126">Odnosi się operacja asynchroniczna, czy hello system wykona tootransition hello węzła tooeither toobeginning *zatrzymana* lub został rozpoczęty stanu.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="d1ff1-127">**Użycie**</span><span class="sxs-lookup"><span data-stu-id="d1ff1-127">**Usage**</span></span>

<span data-ttu-id="d1ff1-128">Jeśli hello API Przejście węzła zgłosiła wyjątek przy wywołaniu, następnie hello systemu zaakceptowane przez operację asynchroniczną hello i wykonaj go.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="d1ff1-129">Pomyślne wywołanie nie oznacza, że operacja hello jest jeszcze zakończone.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="d1ff1-130">tooget informacji na temat hello bieżący stan działania hello hello wywołania interfejsu API postępu Przejście węzła (zarządzany: [GetNodeTransitionProgressAsync()][gntp]) o identyfikatorze guid hello używany podczas wywoływania węzła Interfejs API przejścia dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="d1ff1-131">Witaj API postępu Przejście węzła zwraca obiekt NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="d1ff1-132">Właściwość stanu tego obiektu określa bieżący stan hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="d1ff1-133">Jeśli stan hello "działa" hello operacja jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="d1ff1-134">Jeśli jest zakończone, operacja hello zakończyło się bez błędów.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="d1ff1-135">Jeśli jest ona uszkodzona, wystąpił problem podczas wykonywania operacji hello.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="d1ff1-136">Właściwość Result Hello właściwości wskaże, jakie hello wystawiać wyjątek.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="d1ff1-137">Zobacz https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate Aby uzyskać więcej informacji na temat hello stanu właściwości i sekcję "Przykładowe zastosowanie" hello poniżej przykłady kodu.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="d1ff1-138">**Rozróżnianie między węzłem zatrzymana i dół węzła** Jeśli węzeł ma *zatrzymana* przy użyciu hello API Przejście węzła, hello wyników kwerendy węzła (zarządzany: [GetNodeListAsync()] [ nodequery], Programu PowerShell: [Get-ServiceFabricNode][nodequeryps]) wyświetli ten węzeł zawiera *IsStopped* właściwości wartość true.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="d1ff1-139">Należy pamiętać, jest inna niż wartość hello hello *NodeStatus* właściwość, która będzie napisane *dół*.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="d1ff1-140">Jeśli hello *NodeStatus* właściwość ma wartość *dół*, ale *IsStopped* jest false, a następnie hello węzeł nie został zatrzymany, przy użyciu hello API Przejście węzła, a * Dół* powodu innego powodu.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="d1ff1-141">Jeśli hello *IsStopped* właściwość ma wartość true, a hello *NodeStatus* właściwość jest *dół*, a następnie została zatrzymana, przy użyciu hello API Przejście węzła.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="d1ff1-142">Uruchamianie *zatrzymana* węzła przy użyciu hello API Przejście węzła zwróci on toofunction normalne członkiem klastra hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="d1ff1-143">Hello wyników kwerendy węzła hello interfejsu API wyświetli *IsStopped* jako FAŁSZ i *NodeStatus* jako element, który nie jest w dół (np. w górę).</span><span class="sxs-lookup"><span data-stu-id="d1ff1-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="d1ff1-144">**Ograniczony czas trwania** używając hello toostop API Przejście węzła węzeł, jeden hello wymagane parametry, *stopNodeDurationInSeconds*, czas w sekundach tookeep hello węzła hello reprezentuje * Zatrzymano*.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="d1ff1-145">Ta wartość musi być w hello dopuszczalny zakres, który ma co najmniej 600 i maksymalnie 14400.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="d1ff1-146">Po upływie tego czasu, hello węzeł zostanie automatycznie uruchomiony ponownie się do stanu.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="d1ff1-147">Przykład użycia można znaleźć tooSample 1 poniżej.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="d1ff1-148">Należy unikać mieszanie interfejsów API Przejście węzła oraz hello API węzła uruchomić i zatrzymać węzła.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="d1ff1-149">zalecenie Hello jest zbyt Użyj tylko hello API Przejście węzła.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="d1ff1-150">> Jeśli już zostało węzła zatrzymana, przy użyciu hello API zatrzymanie węzła, go powinny być uruchamiane przy użyciu hello Start API węzła najpierw przed użyciem hello > interfejsów API Przejście węzła.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="d1ff1-151">Wiele API Przejście węzła wywołania nie można wprowadzać na hello tym samym węźle równolegle.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="d1ff1-152">W takiej sytuacji zostanie hello API Przejście węzła > throw FabricException o wartości właściwości ErrorCode NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="d1ff1-153">Przejście węzła w określonym węźle ma > została uruchomiona, należy poczekać aż operacja hello osiągnie stan terminali (ukończone, Faulted lub ForceCancelled) przed rozpoczęciem > nowe przejście na powitania sam węzeł.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="d1ff1-154">Równoległe węzła wywołania przejścia w różnych węzłach są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="d1ff1-155">Przykładowe zastosowanie</span><span class="sxs-lookup"><span data-stu-id="d1ff1-155">Sample Usage</span></span>


<span data-ttu-id="d1ff1-156">**Przykład 1** -hello następujące przykładowe używa hello toostop API Przejście węzła węzeł.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="d1ff1-157">**Przykład 2** — Witaj po uruchomieniu próbki *zatrzymana* węzła.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="d1ff1-158">Niektóre metody pomocnika z pierwszego przykładu hello go używa.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-158">It uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="d1ff1-159">**Przykład 3** — Witaj poniższy przykład zawiera niepoprawne użycie.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="d1ff1-160">To użycie jest nieprawidłowy ponieważ hello *stopDurationInSeconds* zapewnia jest większa niż hello dozwolony zakres.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="d1ff1-161">Ponieważ StartNodeTransitionAsync() zakończy się niepowodzeniem z powodu błędu krytycznego, operacji hello nie został zaakceptowany, i nie należy wywoływać interfejs API postępu hello.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="d1ff1-162">W przykładzie użyto metody pomocnicze, niektóre z pierwszego przykładu hello.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-162">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="d1ff1-163">**Przykład 4** — Witaj poniższy przykład przedstawia hello informacje o błędzie, który zostanie zwrócony z hello węzła przejścia postępu API operacji hello inicjowane przez hello API przejścia węzeł zostanie przyjęte, ale nie powiedzie się później, podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="d1ff1-164">W przypadku hello go nie działa, ponieważ hello API Przejście węzła prób toostart węzła, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="d1ff1-165">W przykładzie użyto metody pomocnicze, niektóre z pierwszego przykładu hello.</span><span class="sxs-lookup"><span data-stu-id="d1ff1-165">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
