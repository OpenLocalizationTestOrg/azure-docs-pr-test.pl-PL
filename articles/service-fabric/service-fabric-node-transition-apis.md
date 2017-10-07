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
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Zastępowanie hello API Przejście węzła hello uruchomić węzeł i zatrzymanie węzła interfejsów API

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>Co hello zatrzymanie węzła i uruchomić interfejsy API węzeł?

Hello zatrzymanie węzła API (zarządzany: [StopNodeAsync()][stopnode], programu PowerShell: [Stop-ServiceFabricNode][stopnodeps]) zatrzymuje węzła sieci szkieletowej usług.  Węzeł sieci szkieletowej usług to proces, nie maszyny Wirtualnej lub maszyny — hello maszyny Wirtualnej lub maszyny będą nadal działać.  Witaj pozostałej części dokumentu hello "węzła" oznacza węzła sieci szkieletowej usług.  Zatrzymanie węzła umieszcza je w *zatrzymana* stanu, gdy nie jest członkiem klastra hello i nie może obsługiwać usługi, w związku z tym symulując *dół* węzła.  Jest to przydatne wstrzykiwania błędów do tootest systemu hello aplikacji.  Hello Start API węzła (zarządzane: [StartNodeAsync()][startnode], programu PowerShell: [Start ServiceFabricNode][startnodeps]]) odwrócona hello zatrzymać API węzła  które łączy hello węzła tooa tyłu normalnym stanie.

## <a name="why-are-we-replacing-these"></a>Dlaczego możemy je zastąpić?

Jak opisano wcześniej, *zatrzymana* sieci szkieletowej usług węzeł jest węzłem, który został celowo docelowych przy użyciu hello API zatrzymanie węzła.  A *dół* węzeł jest węzłem, który nie działa z jakiegokolwiek powodu (np. hello maszyny Wirtualnej lub maszyny jest wyłączone).  Z hello zatrzymanie węzła API hello systemu nie ujawnia toodifferentiate informacji między *zatrzymana* węzłów i *dół* węzłów.

Ponadto niektóre błędy zwrócone przez te interfejsy API nie są jako opisową stać się.  Na przykład wywoływania hello API zatrzymanie węzła na moduł już *zatrzymana* węzła zwróci błąd hello *InvalidAddress*.  To środowisko można lepiej.

Ponadto węzła jest zatrzymana na czas trwania hello jest "nieskończone" do powitalne Start interfejs API węzeł zostanie wywołany.  Znaleźliśmy to może spowodować problemy i mogą być podatne na błędy.  Na przykład firma Microsoft w tym samouczku problemów gdzie użytkownika wywoływane hello zatrzymać API węzeł w węźle i następnie zapomniano o nim.  Później, został jasne, czy węzeł hello miał *dół* lub *zatrzymana*.


## <a name="introducing-hello-node-transition-apis"></a>Wprowadzenie hello interfejsów API Przejście węzła

Uwzględniono te problemy powyżej w nowy zestaw interfejsów API.  Hello nowy interfejs API Przejście węzła (zarządzany: [StartNodeTransitionAsync()][snt]) mogą być używane tootransition tooa węzła sieci szkieletowej usług *zatrzymana* stanu lub tootransition go z *zatrzymana* tooa stanu normalnego stanu.  Należy pamiętać, że ten hello "Start" w nazwie hello hello interfejsu API nie odwołuje się toostarting węzła.  Odnosi się operacja asynchroniczna, czy hello system wykona tootransition hello węzła tooeither toobeginning *zatrzymana* lub został rozpoczęty stanu.

**Użycie**

Jeśli hello API Przejście węzła zgłosiła wyjątek przy wywołaniu, następnie hello systemu zaakceptowane przez operację asynchroniczną hello i wykonaj go.  Pomyślne wywołanie nie oznacza, że operacja hello jest jeszcze zakończone.  tooget informacji na temat hello bieżący stan działania hello hello wywołania interfejsu API postępu Przejście węzła (zarządzany: [GetNodeTransitionProgressAsync()][gntp]) o identyfikatorze guid hello używany podczas wywoływania węzła Interfejs API przejścia dla tej operacji.  Witaj API postępu Przejście węzła zwraca obiekt NodeTransitionProgress.  Właściwość stanu tego obiektu określa bieżący stan hello hello operacji.  Jeśli stan hello "działa" hello operacja jest wykonywana.  Jeśli jest zakończone, operacja hello zakończyło się bez błędów.  Jeśli jest ona uszkodzona, wystąpił problem podczas wykonywania operacji hello.  Właściwość Result Hello właściwości wskaże, jakie hello wystawiać wyjątek.  Zobacz https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate Aby uzyskać więcej informacji na temat hello stanu właściwości i sekcję "Przykładowe zastosowanie" hello poniżej przykłady kodu.


**Rozróżnianie między węzłem zatrzymana i dół węzła** Jeśli węzeł ma *zatrzymana* przy użyciu hello API Przejście węzła, hello wyników kwerendy węzła (zarządzany: [GetNodeListAsync()] [ nodequery], Programu PowerShell: [Get-ServiceFabricNode][nodequeryps]) wyświetli ten węzeł zawiera *IsStopped* właściwości wartość true.  Należy pamiętać, jest inna niż wartość hello hello *NodeStatus* właściwość, która będzie napisane *dół*.  Jeśli hello *NodeStatus* właściwość ma wartość *dół*, ale *IsStopped* jest false, a następnie hello węzeł nie został zatrzymany, przy użyciu hello API Przejście węzła, a * Dół* powodu innego powodu.  Jeśli hello *IsStopped* właściwość ma wartość true, a hello *NodeStatus* właściwość jest *dół*, a następnie została zatrzymana, przy użyciu hello API Przejście węzła.

Uruchamianie *zatrzymana* węzła przy użyciu hello API Przejście węzła zwróci on toofunction normalne członkiem klastra hello ponownie.  Hello wyników kwerendy węzła hello interfejsu API wyświetli *IsStopped* jako FAŁSZ i *NodeStatus* jako element, który nie jest w dół (np. w górę).


**Ograniczony czas trwania** używając hello toostop API Przejście węzła węzeł, jeden hello wymagane parametry, *stopNodeDurationInSeconds*, czas w sekundach tookeep hello węzła hello reprezentuje * Zatrzymano*.  Ta wartość musi być w hello dopuszczalny zakres, który ma co najmniej 600 i maksymalnie 14400.  Po upływie tego czasu, hello węzeł zostanie automatycznie uruchomiony ponownie się do stanu.  Przykład użycia można znaleźć tooSample 1 poniżej.

> [!WARNING]
> Należy unikać mieszanie interfejsów API Przejście węzła oraz hello API węzła uruchomić i zatrzymać węzła.  zalecenie Hello jest zbyt Użyj tylko hello API Przejście węzła.  > Jeśli już zostało węzła zatrzymana, przy użyciu hello API zatrzymanie węzła, go powinny być uruchamiane przy użyciu hello Start API węzła najpierw przed użyciem hello > interfejsów API Przejście węzła.

> [!WARNING]
> Wiele API Przejście węzła wywołania nie można wprowadzać na hello tym samym węźle równolegle.  W takiej sytuacji zostanie hello API Przejście węzła > throw FabricException o wartości właściwości ErrorCode NodeTransitionInProgress.  Przejście węzła w określonym węźle ma > została uruchomiona, należy poczekać aż operacja hello osiągnie stan terminali (ukończone, Faulted lub ForceCancelled) przed rozpoczęciem > nowe przejście na powitania sam węzeł.  Równoległe węzła wywołania przejścia w różnych węzłach są dozwolone.


#### <a name="sample-usage"></a>Przykładowe zastosowanie


**Przykład 1** -hello następujące przykładowe używa hello toostop API Przejście węzła węzeł.

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

**Przykład 2** — Witaj po uruchomieniu próbki *zatrzymana* węzła.  Niektóre metody pomocnika z pierwszego przykładu hello go używa.

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

**Przykład 3** — Witaj poniższy przykład zawiera niepoprawne użycie.  To użycie jest nieprawidłowy ponieważ hello *stopDurationInSeconds* zapewnia jest większa niż hello dozwolony zakres.  Ponieważ StartNodeTransitionAsync() zakończy się niepowodzeniem z powodu błędu krytycznego, operacji hello nie został zaakceptowany, i nie należy wywoływać interfejs API postępu hello.  W przykładzie użyto metody pomocnicze, niektóre z pierwszego przykładu hello.

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

**Przykład 4** — Witaj poniższy przykład przedstawia hello informacje o błędzie, który zostanie zwrócony z hello węzła przejścia postępu API operacji hello inicjowane przez hello API przejścia węzeł zostanie przyjęte, ale nie powiedzie się później, podczas wykonywania.  W przypadku hello go nie działa, ponieważ hello API Przejście węzła prób toostart węzła, który nie istnieje.  W przykładzie użyto metody pomocnicze, niektóre z pierwszego przykładu hello.

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
