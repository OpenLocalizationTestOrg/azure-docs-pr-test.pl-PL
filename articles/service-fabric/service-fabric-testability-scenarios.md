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
# <a name="testability-scenarios"></a>Scenariusze testowania
Dużych systemach rozproszonych jak infrastruktury chmury jest z założenia gwarantowane. Azure sieci szkieletowej usług oferuje deweloperom hello możliwości toowrite usługi toorun na szczycie infrastruktury zawodne. W kolejności toowrite wysokiej jakości usług deweloperzy muszą tooinduce stanie toobe takie zawodnych infrastruktury tootest hello stabilność swoich usług.

Hello błędów Analysis Services zapewnia deweloperom hello możliwości tooinduce błędów akcje tootest usług w hello występowania błędów. Jednak docelowe błędów symulowane programy tylko do tej pory. Ponadto testowanie hello tootake hello scenariuszy testowania można używać w sieci szkieletowej usług: chaos test i test pracy awaryjnej. Te scenariusze symulować ciągłego przeplotem błędów, zarówno bezpieczne i nieprawidłowego w całym klastrze hello przez dłuższy czas. Po skonfigurowaniu testu z hello szybkość i rodzaju błędów można było go uruchomić za pomocą interfejsów API języka C# lub programu PowerShell, toogenerate błędów w klastrze hello i usługi.

> [!WARNING]
> ChaosTestScenario jest zastępowany przez Chaos bardziej elastyczne, oparta na usłudze. Zobacz nowy artykuł toohello [kontrolowane Chaos](service-fabric-controlled-chaos.md) więcej szczegółów.
> 
> 

## <a name="chaos-test"></a>Chaos testu
Scenariusz chaos Hello generuje błędy między hello całego klastra sieci szkieletowej usług. Scenariusz Hello kompresuje błędów zwykle widoczny w miesiącach lub latach tooa kilka godzin. Kombinacja Hello przeplotem błędów ze stawką wysoką odporność hello znajduje sytuacjach wyjątkowych, które w przeciwnym razie zostaną pominięte. Prowadzi to tooa znaczne ulepszenia w jakości kodu hello hello usługi.

### <a name="faults-simulated-in-hello-chaos-test"></a>Błędy w hello chaos testu
* Uruchom ponownie węzeł
* Ponowne uruchomienie wdrożonego pakietu kodu
* Usuwanie repliki
* Uruchom ponownie repliki
* Przenieś repliki podstawowej (opcjonalnie)
* Przenieś repliki pomocniczej (opcjonalnie)

uruchomienia testów chaos Hello przejść przez wiele iteracji błędów i sprawdzanie poprawności klastra na powitania określony czas. konfiguruje się czas Hello hello toostabilize klastra i toosucceed sprawdzania poprawności. Scenariusz Hello nie powiedzie się, gdy naciśniesz pojedynczego uszkodzenia w weryfikacji klastra.

Rozważmy na przykład zestawu testu toorun przez godzinę z maksymalnie trzech równoczesnych błędów. Hello test wywołać trzy usterek i sprawdzania poprawności kondycji klastra hello. Hello testu będzie iterację hello w poprzednim kroku, dopóki hello klastra staje się nieprawidłowy, lub przekazuje jedną godzinę. Jeśli klaster hello staje się nieprawidłowy, w dowolnym iteracji, tj. nie ustabilizowania w skonfigurowanym czasie, hello test zakończy się niepowodzeniem z powodu wyjątku. Ten wyjątek wskazuje, że coś niepowodzenia i wymaga dalszego badania.

W postaci bieżącego aparatu generowania błędów hello w teście chaos hello wywołuje tylko bezpiecznych błędów. Oznacza to, że hello braku błędów zewnętrznych, utrata kworum lub dane nigdy nie wystąpi.

### <a name="important-configuration-options"></a>Opcje konfiguracji ważne
* **TimeToRun**: całkowity czas hello test zostanie uruchomiony przed zakończeniem pomyślnie. Hello test zakończyć wcześniej zamiast niepowodzenia weryfikacji.
* **MaxClusterStabilizationTimeout**: maksymalna ilość czasu toowait dla toobecome klastra hello dobrej kondycji przed niepowodzeniem testu hello. Hello sprawdzenia wykonywane są czy klastra kondycja jest dobra, usługa kondycji jest OK hello rozmiar docelowego zestawu replik uzyskuje się hello usługi partycji i replik w stanie InBuild nie istnieje.
* **MaxConcurrentFaults**: Maksymalna liczba jednoczesnych błędów powstaniu w każdej iteracji. Witaj większą liczbę hello, hello bardziej aktywnego testu hello, dlatego co zapewnia bardziej złożonych przechodzenia w tryb failover i kombinacje przejścia. Hello test gwarantuje, że w przypadku braku błędów zewnętrznych nie będzie kworum lub utraty danych, niezależnie od tego, jak wysoka jest w tej konfiguracji.
* **EnableMoveReplicaFaults**: Włącza lub wyłącza hello błędów, które powodują przeniesienie hello hello repliki podstawowej lub dodatkowej. Te błędy są domyślnie wyłączone.
* **WaitTimeBetweenIterations**: ilość toowait czas między poszczególnymi iteracjami po round usterek i odpowiednie sprawdzania poprawności.

### <a name="how-toorun-hello-chaos-test"></a>Jak przetestować toorun hello chaos
Przykład w języku C#

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

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>Test pracy awaryjnej
Scenariusz test pracy awaryjnej Hello jest wersja hello chaos testu scenariusza, przeznaczonego dla partycji określonej usługi. Sprawdzenie hello wpływ trybu failover na partycji określonej usługi, pozostawiając hello inne usługi nie ma wpływu. Po skonfigurowaniu o innych parametrach i informacji o partycji docelowej hello jest uruchamiany jako narzędzie po stronie klienta, które używa interfejsów API języka C# lub środowiska PowerShell błędów toogenerate dla partycji usługi. Scenariusz Hello iterację sekwencji symulowane usterek i weryfikacja usług logiki biznesowej działać na powitania po stronie tooprovide obciążenia. Błąd podczas weryfikowania usługi wskazuje problem, który wymaga dalszego badania.

### <a name="faults-simulated-in-hello-failover-test"></a>Błędy w hello test pracy awaryjnej
* Ponowne uruchomienie wdrożonego pakietu kodu gdzie jest hostowana hello partycji
* Usuń podstawowe i pomocnicze repliki lub bezstanowych wystąpienia
* Uruchom ponownie podstawowej repliki pomocniczej (Jeśli usługa utrwalonego)
* Przenieś repliki podstawowej
* Przenieś replikę pomocniczą
* Uruchom ponownie hello partycji

test pracy awaryjnej Hello powoduje odporność wybrany, a następnie uruchomi sprawdzania poprawności na powitania usługi tooensure jej stabilności. test pracy awaryjnej Hello wywołuje tylko jedną fault w czasie, nazwą toopossible wiele usterek hello chaos testu. Partycji usługi hello nie stabilizacji przed upływem limitu czasu hello skonfigurowany po każdej błędów hello testów kończy się niepowodzeniem. Hello test wywołuje tylko bezpiecznych błędów. Oznacza to, że w przypadku braku błędów zewnętrznych, utrata danych lub kworum nie nastąpi.

### <a name="important-configuration-options"></a>Opcje konfiguracji ważne
* **Elementu PartitionSelector**: selektora obiekt, który określa hello partycji, która wymaga toobe docelowe.
* **TimeToRun**: całkowity czas hello test zostanie uruchomiony przed zakończeniem.
* **MaxServiceStabilizationTimeout**: maksymalna ilość czasu toowait dla toobecome klastra hello dobrej kondycji przed niepowodzeniem testu hello. Hello sprawdzenia wykonywane są Określa, czy usługa kondycji jest OK hello rozmiar docelowego zestawu replik odbywa się dla wszystkich partycji i replik w stanie InBuild nie istnieje.
* **WaitTimeBetweenFaults**: ilość czasu toowait między każdym cyklu usterek i sprawdzania poprawności.

### <a name="how-toorun-hello-failover-test"></a>Jak przetestować tryb failover hello toorun
**C#**

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


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
