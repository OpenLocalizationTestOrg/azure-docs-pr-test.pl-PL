---
title: "błędy aaaSimulate w Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje o akcji zmianę hello w usługi sieć szkieletowa usług Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Testowania czynności
W kolejności toosimulate zawodnych infrastruktury sieć szkieletowa usług Azure udostępnia, hello dewelopera, przy użyciu metody toosimulate różnych rzeczywistych błędów i przejścia stanu. Są one widoczne jako testowania czynności. Akcje Hello są hello niskiego poziomu interfejsów API, które powodują iniekcji określonych błędów, przejście stanu lub sprawdzania poprawności. Łącząc te akcje można zapisywać scenariusze kompleksowego testowania dla usług.

Sieć szkieletowa usług zawiera kilka typowych scenariuszy testu składa się z tych akcji. Zdecydowanie zaleca się korzystanie z tych scenariuszy wbudowanych, które dokładnie wybrano tootest wspólnej przejść stanu oraz przypadki niepowodzenia. Jednak akcji może być używane toocreate testu scenariuszy należy tooadd pokrycia w scenariuszach, które nie są objęte scenariusze wbudowanych hello jeszcze lub które są niestandardowe dostosowane do aplikacji.

C# implementacje akcje hello znajdują się w hello System.Fabric.dll zestawu. Moduł PowerShell sieci szkieletowej systemu Hello znajduje się w hello Microsoft.ServiceFabric.Powershell.dll zestawu. W ramach instalacji środowiska uruchomieniowego hello modułu ServiceFabric programu PowerShell jest zainstalowane tooallow dla łatwość użycia.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Bezpieczne, a błąd nieprawidłowego działania
Testowania czynności dzieli się na dwie główne pakiety:

* Błędy nieprawidłowego: te błędy symulacji awarii, takie jak ponowne uruchomienie komputera i awarii procesów. W takich przypadkach niepowodzenia hello kontekstu wykonywania procesu zatrzymuje nagle. Oznacza to, że nie oczyszczania stanu hello można uruchomić, zanim aplikacji hello uruchamiany ponownie.
* Błędy bezpiecznie: te błędy symulować łagodne akcje jak przenosi repliki i porzucania wyzwalane przez równoważenia obciążenia. W takich przypadkach usługi hello pobiera powiadomienie z informacją o hello Zamknij i wyczyścić stanu hello przed zakończeniem.

Dla lepszej jakości weryfikacji, należy uruchomić usługę hello i firm obciążenie podczas wywołania różnych bezpieczne i nieprawidłowego błędów. Błędy nieprawidłowego wykonuje scenariuszy, w którym hello usługi proces nagle kończy się w środku hello niektórych przepływu pracy. Testy hello ścieżka odzyskiwania, po przywróceniu repliki usługi hello przez sieć szkieletowa usług. To może pomóc w testowania spójności danych i czy stan usługi hello jest poprawnie utrzymywany po awarii. Witaj drugi zestaw błędów (hello łagodne awarii) testu czy usługa hello poprawnie reaguje tooreplicas przenoszenie przez sieć szkieletowa usług. Obsługa anulowania to testów w metodzie RunAsync hello. Usługa Hello musi toocheck hello anulowania tokenu jest ustawiona, poprawnie zapisać jej stan, a następnie zamknij hello metodzie RunAsync.

## <a name="testability-actions-list"></a>Pola listy Akcje
| Akcja | Opis | Zarządzanego interfejsu API | Polecenia cmdlet programu PowerShell | Bezpieczne/nieprawidłowego błędów |
| --- | --- | --- | --- | --- |
| CleanTestState |Usuwa wszystkie stanu testu hello z klastra hello w przypadku zły zamknięcia hello testu sterownika. |CleanTestStateAsync |Remove-ServiceFabricTestState |Nie dotyczy |
| InvokeDataLoss |Powoduje utratę danych na partycji usługi. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Bezpieczne |
| InvokeQuorumLoss |Umieszcza partycji danej usługi stanowej, w wyniku utraty kworum. |InvokeQuorumLossAsync |Wywołanie ServiceFabricQuorumLoss |Bezpieczne |
| Przenoszenie podstawowej |Przenosi hello określić podstawową replikę usługi stanowej toohello określony węzeł klastra. |MovePrimaryAsync |Przenieś ServiceFabricPrimaryReplica |Bezpieczne |
| Przenieś pomocniczej |Przenosi hello bieżącego pomocniczej replice usługi stanowej tooa inny węzeł klastra. |MoveSecondaryAsync |Przenieś ServiceFabricSecondaryReplica |Bezpieczne |
| RemoveReplica |Symuluje awarii repliki poprzez usunięcie repliki z klastra. To spowoduje zamknięcie hello repliki i przejdą toorole "None", usunięcie wszystkich jego stanu z hello klastra. |RemoveReplicaAsync |Usuń ServiceFabricReplica |Bezpieczne |
| RestartDeployedCodePackage |Symuluje awarii procesu pakietu kodu przez ponowne uruchomienie pakiet kodu wdrożonych na węzłach w klastrze. To przerywa proces pakietu kodu hello, który zostanie uruchomiony ponownie wszystkie repliki hello użytkownika usługi, obsługiwane w tym procesie. |RestartDeployedCodePackageAsync |ServiceFabricDeployedCodePackage ponownego uruchomienia |Nieprawidłowego |
| RestartNode |Symuluje awarii węzła klastra sieci szkieletowej usług przez ponowne uruchomienie węzła. |RestartNodeAsync |ServiceFabricNode ponownego uruchomienia |Nieprawidłowego |
| RestartPartition |Symuluje scenariusza niedostępności klastra lub niedostępności centrum danych przez ponowne uruchomienie niektórych lub wszystkich replik partycji. |RestartPartitionAsync |Restart-ServiceFabricPartition |Bezpieczne |
| RestartReplica |Symuluje awarii repliki ponownego uruchamiania utrwalonych repliki w klastrze, zamykając hello repliki i otworzyć go ponownie. |RestartReplicaAsync |ServiceFabricReplica ponownego uruchomienia |Bezpieczne |
| Parametr StartNode |Rozpoczyna się węzeł w klastrze, który jest już zatrzymana. |StartNodeAsync |Start-ServiceFabricNode |Nie dotyczy |
| Polecenie StopNode |Symuluje awarii węzła przez zatrzymanie węzła w klastrze. węzeł Hello pozostanie w dół do momentu parametr StartNode jest wywoływana. |StopNodeAsync |Stop-ServiceFabricNode |Nieprawidłowego |
| ValidateApplication |Sprawdza dostępność hello i kondycję wszystkich usług sieci szkieletowej usług aplikacji, zwykle po wywołania niektórych błędów w systemie hello. |ValidateApplicationAsync |ServiceFabricApplication testu |Nie dotyczy |
| ValidateService |Sprawdza dostępność hello i kondycji usługi Service Fabric, zwykle po wywołania niektórych błędów w systemie hello. |ValidateServiceAsync |ServiceFabricService testu |Nie dotyczy |

## <a name="running-a-testability-action-using-powershell"></a>Uruchomienie akcji testowania przy użyciu programu PowerShell
W tym samouczku przedstawiono sposób toorun akcją testowania przy użyciu programu PowerShell. Dowiesz się jak toorun akcją kontroli względem klastra lokalnego (jeden pole) lub klastrze platformy Azure. Microsoft.Fabric.Powershell.dll — Witaj modułu programu PowerShell dla usługi sieci szkieletowej — jest instalowana automatycznie podczas instalowania hello MSI sieci szkieletowej usług firmy Microsoft. Moduł Hello jest ładowane automatycznie podczas otwierania wiersza programu PowerShell.

Samouczek segmentów:

* [Uruchom akcję w odniesieniu do klastra z jednym polu](#run-an-action-against-a-one-box-cluster)
* [Uruchom akcję względem klastra platformy Azure](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Uruchom akcję w odniesieniu do klastra z jednym polu
toorun akcję kontroli w odniesieniu do klastra lokalnego, podłącz najpierw toohello klastra i otwórz hello wierszu polecenia PowerShell w trybie administratora. Daj nam przyjrzeć się hello **ServiceFabricNode ponowne uruchomienie** akcji.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

W tym miejscu hello akcji **ServiceFabricNode ponowne uruchomienie** jest uruchamiana w węźle o nazwie "Node1". Tryb uzupełniania Hello Określa, że także powinien sprawdza, czy akcja ponownego uruchomienia węzła hello faktycznie zakończyło się pomyślnie. Określanie tryb uzupełniania hello jako "Zweryfikuj" spowoduje jego tooverify czy akcja ponownego uruchomienia hello faktycznie zakończyło się pomyślnie. Zamiast bezpośrednio określać hello węzła przy użyciu nazwy, możesz je określić za pomocą rodzaj partycji klucza i hello replik, w następujący sposób:

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Ponowne uruchomienie ServiceFabricNode** powinny być używane toorestart węzeł sieci szkieletowej usług w klastrze. Spowoduje to zatrzymanie proces Fabric.exe hello, który zostanie uruchomiony ponownie wszystkie hello system usługi i użytkowników usługi replik hostowanych w tym węźle. Użycie tootest tego interfejsu API usługi ułatwia odkrywanie usterki wzdłuż ścieżki odzyskiwania trybu failover hello. Pomaga symulacji awarii węzła w klastrze hello.

Witaj Poniższy zrzut ekranu przedstawia hello **ServiceFabricNode ponowne uruchomienie** polecenia kontroli w akcji.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

Witaj dane wyjściowe z hello najpierw **Get-ServiceFabricNode** (polecenia cmdlet z modułu programu PowerShell usługi Service Fabric hello) zawiera klastra lokalne powitania zawiera pięć węzłów: Node.1 tooNode.5. Po akcji zmianę hello (polecenia cmdlet) **ServiceFabricNode ponowne uruchomienie** jest wykonywana w węźle hello o nazwie Node.4, przedstawia czas pracy tego węzła hello został zresetowany.

### <a name="run-an-action-against-an-azure-cluster"></a>Uruchom akcję względem klastra platformy Azure
Uruchomienie akcji pola (przy użyciu programu PowerShell) względem klastra platformy Azure jest podobne kroki hello toorunning w odniesieniu do klastra lokalnego. Witaj tylko różnicą jest to, że przed uruchomieniem akcji hello, zamiast łączącego toohello klastra lokalnego, należy tooconnect toohello Azure najpierw klastra.

## <a name="running-a-testability-action-using-c35"></a>Uruchomienie akcji testowania w języku C & 35;
toorun akcją testowania przy użyciu języka C#, należy najpierw tooconnect toohello klastra przy użyciu klienta fabricclient z rolą. Następnie Uzyskaj hello parametry potrzebne toorun hello akcji. Można użyć różnych parametrów toorun hello tę samą akcję.
Spojrzenie na powitania RestartServiceFabricNode akcji, jednokierunkowej toorun, jest przy użyciu informacji węzła hello (nazwy węzła i identyfikator wystąpienia węzła) w klastrze hello.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Objaśnienie parametrów:

* **CompleteMode** Określa, że tryb hello nie sprawdzić, czy akcja ponownego uruchomienia hello faktycznie zakończyło się pomyślnie. Określanie tryb uzupełniania hello jako "Zweryfikuj" spowoduje jego tooverify czy akcja ponownego uruchomienia hello faktycznie zakończyło się pomyślnie.  
* **OperationTimeout** zestawy hello czas toofinish operacji hello przed jest zgłaszany wyjątek TimeoutException.
* **CancellationToken** umożliwia toobe oczekujące wywołanie, anulowane.

Zamiast bezpośrednio określać hello węzła przy użyciu nazwy, możesz je określić za pomocą rodzaj partycji klucza i hello repliki.

Aby uzyskać więcej informacji, zobacz [elementu PartitionSelector i elementu ReplicaSelector](#partition_replica_selector).

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>Elementu PartitionSelector i elementu ReplicaSelector
### <a name="partitionselector"></a>Elementu PartitionSelector
Elementu PartitionSelector jest pomocnika ujawnione podczas testowania i jest używany tooselect określonej partycji na które tooperform hello testowania czynności. Jeśli identyfikator partycji: hello jest znany wcześniej może być używane tooselect określonej partycji. Lub, możesz podać klucz partycji hello i operacji hello rozwiąże identyfikator partycji: hello wewnętrznie. Istnieje również opcja hello losowe partycji.

toouse tego pomocnika tworzenia obiektu elementu PartitionSelector hello i wybierz partycję hello przy użyciu jednej z hello Select * metod. Następnie przekazać hello elementu PartitionSelector obiektu toohello interfejsu API, która go wymaga. Jeśli wybrano opcję nie, domyślnie tooa losowe partycji.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>Elementu ReplicaSelector
Elementu ReplicaSelector jest pomocnika ujawnione podczas testowania i jest używany toohelp Wybierz replikę, na które tooperform hello testowania czynności. Identyfikator repliki hello jest znany wcześniej może być używane tooselect określonych repliki. Ponadto można jeszcze hello opcja repliki podstawowej lub dodatkowej losowych. Elementu ReplicaSelector pochodzi z elementu PartitionSelector, warto tooselect hello zarówno repliki i hello partycji, na którym chcesz tooperform hello zmianę operacji.

toouse tego pomocnika, Utwórz obiekt elementu ReplicaSelector i ustaw sposób hello tooselect hello repliki i hello partycji. Można następnie przekazać do hello interfejsu API, która go wymaga. Jeśli wybrano opcję nie, domyślnie tooa losowe repliki i losowe partycji.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>Następne kroki
* [Scenariusze testowania](service-fabric-testability-scenarios.md)
* Jak tootest usługi
  * [Symulacji awarii podczas obciążeń usługi](service-fabric-testability-workload-tests.md)
  * [Błędy usługi do komunikacji](service-fabric-testability-scenarios-service-communication.md)

