---
title: "Tworzenie testów chaos i pracy awaryjnej dla usługi Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Przy użyciu usługi Service Fabric chaos testu i pracy awaryjnej przetestować scenariusze wywołać błędów i sprawdź niezawodności usług."
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
ms.openlocfilehash: d06026c750e01ad5825338a78d9af331265f434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="604bc-103">Scenariusze testowania</span><span class="sxs-lookup"><span data-stu-id="604bc-103">Testability scenarios</span></span>
<span data-ttu-id="604bc-104">Dużych systemach rozproszonych jak infrastruktury chmury jest z założenia gwarantowane.</span><span class="sxs-lookup"><span data-stu-id="604bc-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="604bc-105">Sieć szkieletowa usług Azure zapewnia deweloperom możliwość zapisu do uruchamiania na szczycie infrastruktury niepewna.</span><span class="sxs-lookup"><span data-stu-id="604bc-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="604bc-106">Aby można było zapisać wysokiej jakości usług, deweloperzy muszą móc wywoływać takie zawodnych infrastruktury do testowania stabilność swoich usług.</span><span class="sxs-lookup"><span data-stu-id="604bc-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="604bc-107">Usługi analizy błędów zapewnia deweloperom możliwość wywołać błędów działań do przetestowania usługi w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="604bc-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="604bc-108">Jednak docelowe błędów symulowane programy tylko do tej pory.</span><span class="sxs-lookup"><span data-stu-id="604bc-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="604bc-109">Podejmowanie testowania, możesz skorzystać ze scenariuszy testu w sieci szkieletowej usług: chaos test i test pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="604bc-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="604bc-110">Te scenariusze symulować ciągłego przeplotem błędów, zarówno bezpieczne i nieprawidłowego w całym klastrze przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="604bc-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="604bc-111">Po skonfigurowaniu testu z szybkość i rodzaju błędów można było go uruchomić za pomocą interfejsów API języka C# lub programu PowerShell w celu generowania błędów w klastrze i usługi.</span><span class="sxs-lookup"><span data-stu-id="604bc-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="604bc-112">ChaosTestScenario jest zastępowany przez Chaos bardziej elastyczne, oparta na usłudze.</span><span class="sxs-lookup"><span data-stu-id="604bc-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="604bc-113">Zapoznaj się z nowego artykułu [kontrolowane Chaos](service-fabric-controlled-chaos.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="604bc-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="604bc-114">Chaos testu</span><span class="sxs-lookup"><span data-stu-id="604bc-114">Chaos test</span></span>
<span data-ttu-id="604bc-115">Scenariusz chaos generuje błędy w ramach całego klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="604bc-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="604bc-116">Scenariusz kompresuje błędów zwykle widoczny w miesięcy lub lat do kilku godzin.</span><span class="sxs-lookup"><span data-stu-id="604bc-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="604bc-117">Kombinacja przeplotem błędów ze wskaźnikiem wysoką odporność znajduje sytuacjach wyjątkowych, które w przeciwnym razie zostaną pominięte.</span><span class="sxs-lookup"><span data-stu-id="604bc-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="604bc-118">Prowadzi to do znacznej poprawy jakości kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="604bc-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="604bc-119">Błędy w teście chaos</span><span class="sxs-lookup"><span data-stu-id="604bc-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="604bc-120">Uruchom ponownie węzeł</span><span class="sxs-lookup"><span data-stu-id="604bc-120">Restart a node</span></span>
* <span data-ttu-id="604bc-121">Ponowne uruchomienie wdrożonego pakietu kodu</span><span class="sxs-lookup"><span data-stu-id="604bc-121">Restart a deployed code package</span></span>
* <span data-ttu-id="604bc-122">Usuwanie repliki</span><span class="sxs-lookup"><span data-stu-id="604bc-122">Remove a replica</span></span>
* <span data-ttu-id="604bc-123">Uruchom ponownie repliki</span><span class="sxs-lookup"><span data-stu-id="604bc-123">Restart a replica</span></span>
* <span data-ttu-id="604bc-124">Przenieś repliki podstawowej (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="604bc-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="604bc-125">Przenieś repliki pomocniczej (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="604bc-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="604bc-126">Chaos test uruchamia przejść przez wiele iteracji usterek i sprawdzanie poprawności klastra w określonym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="604bc-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="604bc-127">Konfiguruje się czas dla klastra do utrwalania i Weryfikacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="604bc-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="604bc-128">Scenariusz nie powiedzie się, gdy naciśniesz pojedynczego uszkodzenia w weryfikacji klastra.</span><span class="sxs-lookup"><span data-stu-id="604bc-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="604bc-129">Rozważmy na przykład uruchamiana przez godzinę z maksymalnie trzech równoczesnych błędów testu.</span><span class="sxs-lookup"><span data-stu-id="604bc-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="604bc-130">Testu wywoływać błędy trzy, a następnie sprawdź stan klastra.</span><span class="sxs-lookup"><span data-stu-id="604bc-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="604bc-131">Test zostanie iterację poprzedniego kroku, dopóki klastra staje się nieprawidłowy, lub przekazuje jedną godzinę.</span><span class="sxs-lookup"><span data-stu-id="604bc-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="604bc-132">Jeśli klaster staje się nieprawidłowy, w dowolnym iteracji, tj. nie ustabilizowania w skonfigurowanym czasie, test zakończy się niepowodzeniem z powodu wyjątku.</span><span class="sxs-lookup"><span data-stu-id="604bc-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="604bc-133">Ten wyjątek wskazuje, że coś niepowodzenia i wymaga dalszego badania.</span><span class="sxs-lookup"><span data-stu-id="604bc-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="604bc-134">W postaci bieżącego aparatu generowania błędów w teście chaos wywołuje tylko bezpiecznych błędów.</span><span class="sxs-lookup"><span data-stu-id="604bc-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="604bc-135">Oznacza to, że w przypadku braku błędów zewnętrznych utraty kworum lub dane nigdy nie wystąpi.</span><span class="sxs-lookup"><span data-stu-id="604bc-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="604bc-136">Opcje konfiguracji ważne</span><span class="sxs-lookup"><span data-stu-id="604bc-136">Important configuration options</span></span>
* <span data-ttu-id="604bc-137">**TimeToRun**: całkowity czas uruchomienia testu przed zakończeniem pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="604bc-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="604bc-138">Test zakończenia wcześniej zamiast niepowodzenia weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="604bc-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="604bc-139">**MaxClusterStabilizationTimeout**: maksymalna ilość czasu oczekiwania na klaster, aby stała się dobra przed niepowodzeniem testu.</span><span class="sxs-lookup"><span data-stu-id="604bc-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="604bc-140">Testy wykonywane są czy klastra kondycja jest dobra, usługa kondycji jest OK uzyskuje się rozmiar docelowego zestawu replik partycji usługi i replik w stanie InBuild nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="604bc-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="604bc-141">**MaxConcurrentFaults**: Maksymalna liczba jednoczesnych błędów powstaniu w każdej iteracji.</span><span class="sxs-lookup"><span data-stu-id="604bc-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="604bc-142">Wyższa wartość, bardziej aktywnego testu, dlatego co zapewnia bardziej złożonych przechodzenia w tryb failover i kombinacje przejścia.</span><span class="sxs-lookup"><span data-stu-id="604bc-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="604bc-143">Test gwarantuje, że w przypadku braku błędów zewnętrznych nie będzie kworum lub utraty danych, niezależnie od tego, jak wysoka jest w tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="604bc-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="604bc-144">**EnableMoveReplicaFaults**: Włącza lub wyłącza usterek, które powodują przeniesienie repliki podstawowej lub dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="604bc-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="604bc-145">Te błędy są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="604bc-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="604bc-146">**WaitTimeBetweenIterations**: czas oczekiwania pomiędzy iteracjami po round usterek i odpowiednie sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="604bc-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="604bc-147">Jak uruchomić chaos test</span><span class="sxs-lookup"><span data-stu-id="604bc-147">How to run the chaos test</span></span>
<span data-ttu-id="604bc-148">Przykład w języku C#</span><span class="sxs-lookup"><span data-stu-id="604bc-148">C# sample</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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

<span data-ttu-id="604bc-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="604bc-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="604bc-150">Test pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="604bc-150">Failover test</span></span>
<span data-ttu-id="604bc-151">Scenariusz test pracy awaryjnej jest wersja chaos scenariusza testowego przeznaczonego dla partycji określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="604bc-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="604bc-152">Sprawdzenie wpływ trybu failover na partycji określonej usługi, pozostawiając nie dotyczy innych usług.</span><span class="sxs-lookup"><span data-stu-id="604bc-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="604bc-153">Po skonfigurowaniu o innych parametrach i informacji o partycji docelowej jest uruchamiany jako narzędzie po stronie klienta, które korzysta z interfejsów API języka C# lub programu PowerShell do generowania błędów dla partycji usługi.</span><span class="sxs-lookup"><span data-stu-id="604bc-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="604bc-154">Scenariusz iterację sekwencji symulowane usterek i weryfikacji usługi podczas wykonywania logiki biznesowej po stronie, zapewnienie obciążenia.</span><span class="sxs-lookup"><span data-stu-id="604bc-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="604bc-155">Błąd podczas weryfikowania usługi wskazuje problem, który wymaga dalszego badania.</span><span class="sxs-lookup"><span data-stu-id="604bc-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="604bc-156">Błędy w test pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="604bc-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="604bc-157">Ponowne uruchomienie wdrożonego pakietu kodu gdzie jest hostowana partycji</span><span class="sxs-lookup"><span data-stu-id="604bc-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="604bc-158">Usuń podstawowe i pomocnicze repliki lub bezstanowych wystąpienia</span><span class="sxs-lookup"><span data-stu-id="604bc-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="604bc-159">Uruchom ponownie podstawowej repliki pomocniczej (Jeśli usługa utrwalonego)</span><span class="sxs-lookup"><span data-stu-id="604bc-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="604bc-160">Przenieś repliki podstawowej</span><span class="sxs-lookup"><span data-stu-id="604bc-160">Move a primary replica</span></span>
* <span data-ttu-id="604bc-161">Przenieś replikę pomocniczą</span><span class="sxs-lookup"><span data-stu-id="604bc-161">Move a secondary replica</span></span>
* <span data-ttu-id="604bc-162">Uruchom ponownie partycji</span><span class="sxs-lookup"><span data-stu-id="604bc-162">Restart the partition</span></span>

<span data-ttu-id="604bc-163">Test pracy awaryjnej powoduje odporność wybrany, a następnie uruchomi sprawdzanie poprawności w usłudze, aby zapewnić jego stabilność.</span><span class="sxs-lookup"><span data-stu-id="604bc-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="604bc-164">Test pracy awaryjnej wywołuje tylko jeden błąd w czasie, w przeciwieństwie do możliwości wiele błędów w teście chaos.</span><span class="sxs-lookup"><span data-stu-id="604bc-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="604bc-165">Partycji usługi nie stabilizacji w ciągu skonfigurowanego limitu czasu po awarii każdego testu nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="604bc-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="604bc-166">Test wywołuje tylko bezpiecznych błędów.</span><span class="sxs-lookup"><span data-stu-id="604bc-166">The test induces only safe faults.</span></span> <span data-ttu-id="604bc-167">Oznacza to, że w przypadku braku błędów zewnętrznych, utrata danych lub kworum nie nastąpi.</span><span class="sxs-lookup"><span data-stu-id="604bc-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="604bc-168">Opcje konfiguracji ważne</span><span class="sxs-lookup"><span data-stu-id="604bc-168">Important configuration options</span></span>
* <span data-ttu-id="604bc-169">**Elementu PartitionSelector**: selektora obiekt, który określa partycji, który ma być celem.</span><span class="sxs-lookup"><span data-stu-id="604bc-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="604bc-170">**TimeToRun**: całkowity czas uruchomienia testu przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="604bc-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="604bc-171">**MaxServiceStabilizationTimeout**: maksymalna ilość czasu oczekiwania na klaster, aby stała się dobra przed niepowodzeniem testu.</span><span class="sxs-lookup"><span data-stu-id="604bc-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="604bc-172">Testy wykonywane są Określa, czy usługa kondycji jest OK rozmiar docelowego zestawu replik odbywa się dla wszystkich partycji i replik w stanie InBuild nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="604bc-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="604bc-173">**WaitTimeBetweenFaults**: ilość czasu między każdym cyklu usterek i sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="604bc-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="604bc-174">Jak uruchomić test trybu failover</span><span class="sxs-lookup"><span data-stu-id="604bc-174">How to run the failover test</span></span>
<span data-ttu-id="604bc-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="604bc-175">**C#**</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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


<span data-ttu-id="604bc-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="604bc-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
