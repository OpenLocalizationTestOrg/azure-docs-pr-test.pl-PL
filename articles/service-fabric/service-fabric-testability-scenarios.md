---
title: "aaaCreate chaos i pracy awaryjnej testów Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Za pomocą testu chaos sieci szkieletowej usług hello i pracy awaryjnej testowania scenariuszy tooinduce błędów i sprawdź niezawodności hello usług."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="48463-103">Scenariusze testowania</span><span class="sxs-lookup"><span data-stu-id="48463-103">Testability scenarios</span></span>
<span data-ttu-id="48463-104">Dużych systemach rozproszonych jak infrastruktury chmury jest z założenia gwarantowane.</span><span class="sxs-lookup"><span data-stu-id="48463-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="48463-105">Azure sieci szkieletowej usług oferuje deweloperom hello możliwości toowrite usługi toorun na szczycie infrastruktury zawodne.</span><span class="sxs-lookup"><span data-stu-id="48463-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="48463-106">W kolejności toowrite wysokiej jakości usług deweloperzy muszą tooinduce stanie toobe takie zawodnych infrastruktury tootest hello stabilność swoich usług.</span><span class="sxs-lookup"><span data-stu-id="48463-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="48463-107">Hello błędów Analysis Services zapewnia deweloperom hello możliwości tooinduce błędów akcje tootest usług w hello występowania błędów.</span><span class="sxs-lookup"><span data-stu-id="48463-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="48463-108">Jednak docelowe błędów symulowane programy tylko do tej pory.</span><span class="sxs-lookup"><span data-stu-id="48463-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="48463-109">Ponadto testowanie hello tootake hello scenariuszy testowania można używać w sieci szkieletowej usług: chaos test i test pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="48463-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="48463-110">Te scenariusze symulować ciągłego przeplotem błędów, zarówno bezpieczne i nieprawidłowego w całym klastrze hello przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="48463-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="48463-111">Po skonfigurowaniu testu z hello szybkość i rodzaju błędów można było go uruchomić za pomocą interfejsów API języka C# lub programu PowerShell, toogenerate błędów w klastrze hello i usługi.</span><span class="sxs-lookup"><span data-stu-id="48463-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="48463-112">ChaosTestScenario jest zastępowany przez Chaos bardziej elastyczne, oparta na usłudze.</span><span class="sxs-lookup"><span data-stu-id="48463-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="48463-113">Zobacz nowy artykuł toohello [kontrolowane Chaos](service-fabric-controlled-chaos.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="48463-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="48463-114">Chaos testu</span><span class="sxs-lookup"><span data-stu-id="48463-114">Chaos test</span></span>
<span data-ttu-id="48463-115">Scenariusz chaos Hello generuje błędy między hello całego klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="48463-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="48463-116">Scenariusz Hello kompresuje błędów zwykle widoczny w miesiącach lub latach tooa kilka godzin.</span><span class="sxs-lookup"><span data-stu-id="48463-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="48463-117">Kombinacja Hello przeplotem błędów ze stawką wysoką odporność hello znajduje sytuacjach wyjątkowych, które w przeciwnym razie zostaną pominięte.</span><span class="sxs-lookup"><span data-stu-id="48463-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="48463-118">Prowadzi to tooa znaczne ulepszenia w jakości kodu hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="48463-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="48463-119">Błędy w hello chaos testu</span><span class="sxs-lookup"><span data-stu-id="48463-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="48463-120">Uruchom ponownie węzeł</span><span class="sxs-lookup"><span data-stu-id="48463-120">Restart a node</span></span>
* <span data-ttu-id="48463-121">Ponowne uruchomienie wdrożonego pakietu kodu</span><span class="sxs-lookup"><span data-stu-id="48463-121">Restart a deployed code package</span></span>
* <span data-ttu-id="48463-122">Usuwanie repliki</span><span class="sxs-lookup"><span data-stu-id="48463-122">Remove a replica</span></span>
* <span data-ttu-id="48463-123">Uruchom ponownie repliki</span><span class="sxs-lookup"><span data-stu-id="48463-123">Restart a replica</span></span>
* <span data-ttu-id="48463-124">Przenieś repliki podstawowej (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="48463-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="48463-125">Przenieś repliki pomocniczej (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="48463-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="48463-126">uruchomienia testów chaos Hello przejść przez wiele iteracji błędów i sprawdzanie poprawności klastra na powitania określony czas.</span><span class="sxs-lookup"><span data-stu-id="48463-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="48463-127">konfiguruje się czas Hello hello toostabilize klastra i toosucceed sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="48463-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="48463-128">Scenariusz Hello nie powiedzie się, gdy naciśniesz pojedynczego uszkodzenia w weryfikacji klastra.</span><span class="sxs-lookup"><span data-stu-id="48463-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="48463-129">Rozważmy na przykład zestawu testu toorun przez godzinę z maksymalnie trzech równoczesnych błędów.</span><span class="sxs-lookup"><span data-stu-id="48463-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="48463-130">Hello test wywołać trzy usterek i sprawdzania poprawności kondycji klastra hello.</span><span class="sxs-lookup"><span data-stu-id="48463-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="48463-131">Hello testu będzie iterację hello w poprzednim kroku, dopóki hello klastra staje się nieprawidłowy, lub przekazuje jedną godzinę.</span><span class="sxs-lookup"><span data-stu-id="48463-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="48463-132">Jeśli klaster hello staje się nieprawidłowy, w dowolnym iteracji, tj. nie ustabilizowania w skonfigurowanym czasie, hello test zakończy się niepowodzeniem z powodu wyjątku.</span><span class="sxs-lookup"><span data-stu-id="48463-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="48463-133">Ten wyjątek wskazuje, że coś niepowodzenia i wymaga dalszego badania.</span><span class="sxs-lookup"><span data-stu-id="48463-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="48463-134">W postaci bieżącego aparatu generowania błędów hello w teście chaos hello wywołuje tylko bezpiecznych błędów.</span><span class="sxs-lookup"><span data-stu-id="48463-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="48463-135">Oznacza to, że hello braku błędów zewnętrznych, utrata kworum lub dane nigdy nie wystąpi.</span><span class="sxs-lookup"><span data-stu-id="48463-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="48463-136">Opcje konfiguracji ważne</span><span class="sxs-lookup"><span data-stu-id="48463-136">Important configuration options</span></span>
* <span data-ttu-id="48463-137">**TimeToRun**: całkowity czas hello test zostanie uruchomiony przed zakończeniem pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="48463-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="48463-138">Hello test zakończyć wcześniej zamiast niepowodzenia weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="48463-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="48463-139">**MaxClusterStabilizationTimeout**: maksymalna ilość czasu toowait dla toobecome klastra hello dobrej kondycji przed niepowodzeniem testu hello.</span><span class="sxs-lookup"><span data-stu-id="48463-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="48463-140">Hello sprawdzenia wykonywane są czy klastra kondycja jest dobra, usługa kondycji jest OK hello rozmiar docelowego zestawu replik uzyskuje się hello usługi partycji i replik w stanie InBuild nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="48463-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="48463-141">**MaxConcurrentFaults**: Maksymalna liczba jednoczesnych błędów powstaniu w każdej iteracji.</span><span class="sxs-lookup"><span data-stu-id="48463-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="48463-142">Witaj większą liczbę hello, hello bardziej aktywnego testu hello, dlatego co zapewnia bardziej złożonych przechodzenia w tryb failover i kombinacje przejścia.</span><span class="sxs-lookup"><span data-stu-id="48463-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="48463-143">Hello test gwarantuje, że w przypadku braku błędów zewnętrznych nie będzie kworum lub utraty danych, niezależnie od tego, jak wysoka jest w tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="48463-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="48463-144">**EnableMoveReplicaFaults**: Włącza lub wyłącza hello błędów, które powodują przeniesienie hello hello repliki podstawowej lub dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="48463-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="48463-145">Te błędy są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="48463-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="48463-146">**WaitTimeBetweenIterations**: ilość toowait czas między poszczególnymi iteracjami po round usterek i odpowiednie sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="48463-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="48463-147">Jak przetestować toorun hello chaos</span><span class="sxs-lookup"><span data-stu-id="48463-147">How toorun hello chaos test</span></span>
<span data-ttu-id="48463-148">Przykład w języku C#</span><span class="sxs-lookup"><span data-stu-id="48463-148">C# sample</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

<span data-ttu-id="48463-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48463-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="48463-150">Test pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="48463-150">Failover test</span></span>
<span data-ttu-id="48463-151">Scenariusz test pracy awaryjnej Hello jest wersja hello chaos testu scenariusza, przeznaczonego dla partycji określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="48463-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="48463-152">Sprawdzenie hello wpływ trybu failover na partycji określonej usługi, pozostawiając hello inne usługi nie ma wpływu.</span><span class="sxs-lookup"><span data-stu-id="48463-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="48463-153">Po skonfigurowaniu o innych parametrach i informacji o partycji docelowej hello jest uruchamiany jako narzędzie po stronie klienta, które używa interfejsów API języka C# lub środowiska PowerShell błędów toogenerate dla partycji usługi.</span><span class="sxs-lookup"><span data-stu-id="48463-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="48463-154">Scenariusz Hello iterację sekwencji symulowane usterek i weryfikacja usług logiki biznesowej działać na powitania po stronie tooprovide obciążenia.</span><span class="sxs-lookup"><span data-stu-id="48463-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="48463-155">Błąd podczas weryfikowania usługi wskazuje problem, który wymaga dalszego badania.</span><span class="sxs-lookup"><span data-stu-id="48463-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="48463-156">Błędy w hello test pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="48463-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="48463-157">Ponowne uruchomienie wdrożonego pakietu kodu gdzie jest hostowana hello partycji</span><span class="sxs-lookup"><span data-stu-id="48463-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="48463-158">Usuń podstawowe i pomocnicze repliki lub bezstanowych wystąpienia</span><span class="sxs-lookup"><span data-stu-id="48463-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="48463-159">Uruchom ponownie podstawowej repliki pomocniczej (Jeśli usługa utrwalonego)</span><span class="sxs-lookup"><span data-stu-id="48463-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="48463-160">Przenieś repliki podstawowej</span><span class="sxs-lookup"><span data-stu-id="48463-160">Move a primary replica</span></span>
* <span data-ttu-id="48463-161">Przenieś replikę pomocniczą</span><span class="sxs-lookup"><span data-stu-id="48463-161">Move a secondary replica</span></span>
* <span data-ttu-id="48463-162">Uruchom ponownie hello partycji</span><span class="sxs-lookup"><span data-stu-id="48463-162">Restart hello partition</span></span>

<span data-ttu-id="48463-163">test pracy awaryjnej Hello powoduje odporność wybrany, a następnie uruchomi sprawdzania poprawności na powitania usługi tooensure jej stabilności.</span><span class="sxs-lookup"><span data-stu-id="48463-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="48463-164">test pracy awaryjnej Hello wywołuje tylko jedną fault w czasie, nazwą toopossible wiele usterek hello chaos testu.</span><span class="sxs-lookup"><span data-stu-id="48463-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="48463-165">Partycji usługi hello nie stabilizacji przed upływem limitu czasu hello skonfigurowany po każdej błędów hello testów kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="48463-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="48463-166">Hello test wywołuje tylko bezpiecznych błędów.</span><span class="sxs-lookup"><span data-stu-id="48463-166">hello test induces only safe faults.</span></span> <span data-ttu-id="48463-167">Oznacza to, że w przypadku braku błędów zewnętrznych, utrata danych lub kworum nie nastąpi.</span><span class="sxs-lookup"><span data-stu-id="48463-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="48463-168">Opcje konfiguracji ważne</span><span class="sxs-lookup"><span data-stu-id="48463-168">Important configuration options</span></span>
* <span data-ttu-id="48463-169">**Elementu PartitionSelector**: selektora obiekt, który określa hello partycji, która wymaga toobe docelowe.</span><span class="sxs-lookup"><span data-stu-id="48463-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="48463-170">**TimeToRun**: całkowity czas hello test zostanie uruchomiony przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="48463-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="48463-171">**MaxServiceStabilizationTimeout**: maksymalna ilość czasu toowait dla toobecome klastra hello dobrej kondycji przed niepowodzeniem testu hello.</span><span class="sxs-lookup"><span data-stu-id="48463-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="48463-172">Hello sprawdzenia wykonywane są Określa, czy usługa kondycji jest OK hello rozmiar docelowego zestawu replik odbywa się dla wszystkich partycji i replik w stanie InBuild nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="48463-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="48463-173">**WaitTimeBetweenFaults**: ilość czasu toowait między każdym cyklu usterek i sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="48463-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="48463-174">Jak przetestować tryb failover hello toorun</span><span class="sxs-lookup"><span data-stu-id="48463-174">How toorun hello failover test</span></span>
<span data-ttu-id="48463-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="48463-175">**C#**</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


<span data-ttu-id="48463-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="48463-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
