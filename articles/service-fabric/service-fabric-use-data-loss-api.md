---
title: "tooInvoke aaaHow utratą danych w sieci szkieletowej usługi | Dokumentacja firmy Microsoft"
description: W tym artykule opisano, jak toouse hello utraty danych interfejsu api
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
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a>Jak tooInvoke utraty danych w usługach
> [!WARNING]
> Tym dokumencie opisano sposób toocause utraty danych w usługach i powinna być używana z rozwagą.
> 
> 

## <a name="introduction"></a>Wprowadzenie
Utrata danych na partycji usługi sieć szkieletowa usług przez wywołanie StartPartitionDataLossAsync() można wywołać.  Ten interfejs api korzysta hello iniekcji błędów i Analysis Service tooperform hello pracy toocause danych utraty warunków.

## <a name="using-hello-fault-injection-and-analysis-service"></a>Przy użyciu hello iniekcji błędów i usługi analizy
Hello iniekcji błędów i Analysis Service obecnie obsługuje następujące interfejsy API w poniższej tabeli hello hello.  powitania po prawej stronie wykresu hello pokazuje hello odpowiednie polecenie cmdlet programu PowerShell.  Aby uzyskać więcej informacji na temat każdej z nich można znaleźć w dokumentacji msdn toohello w każdym interfejsu API.

| INTERFEJS API JĘZYKA C# | Polecenia Cmdlet programu PowerShell |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Omówienie pojęć dotyczących uruchomiono polecenie
Witaj iniekcji błędów i Analysis Services używa modelu asynchroniczne, gdzie rozpoczęciem powitalne polecenie z jednego interfejsu API, określonego interfejsu API "Start" hello tooas tego dokumentu, a następnie postęp hello kontroli tego polecenia przy użyciu interfejsu API "GetProgress", dopóki osiągnie terminal Stan, lub do czasu można anulować.
toostart polecenia, wywołania interfejsu API hello "Start" hello odpowiedniego interfejsu API.  Ten interfejs API zwraca podczas hello iniekcji błędów i Analysis Service zaakceptował Żądanie hello.  Jednak nie oznacza jakim zostało uruchomione polecenie, lub nawet jeśli została ona jeszcze uruchomiona.  Trwa kolejności toocheck polecenia należy wywołać hello "GetProgress" interfejsu API, który odpowiada toohello "Start" interfejsu API wcześniej nazywane.  Witaj "GetProgress" interfejsu API będzie zwracać wskazująca bieżący stan hello polecenia hello wewnątrz jego właściwość stanu obiektu.  Polecenie działa przez czas nieokreślony do:

1. Pomyślnie zakończy działanie.  Jeśli w tym przypadku wywołać "GetProgress" na nim, stan obiektu postępu hello zostanie ukończona.
2. Napotkania błędu krytycznego.  Jeśli w tym przypadku wywołać "GetProgress" na nim, stan obiektu postępu hello wystąpi błąd
3. Możesz anulować za pośrednictwem hello [CancelTestCommandAsync] [ cancel] interfejsu API, lub [Stop-ServiceFabricTestCommand] [ cancelps] polecenia cmdlet programu PowerShell.  Jeśli w tym przypadku wywołać "GetProgress" na nim, hello stan obiektu postęp będzie odwołania lub ForceCancelled, w zależności od argumentu toothat interfejsu API.  Zapoznaj się dokumentacją hello [CancelTestCommandAsync] [ cancel] więcej szczegółów.

## <a name="details-of-running-a-command"></a>Szczegółowe informacje o uruchamianiu polecenia
W kolejności toostart polecenia należy wywołać hello Start interfejsu API z argumentami hello oczekiwano.  Wszystkie interfejsy API Start użyć argumentu Guid o nazwie operationId.  Użytkownik powinien zachować informacje o hello operationId argument, ponieważ jest on używany postępu tootrack tego polecenia.  Musi być przekazany hello "GetProgress" interfejsu API w toku tootrack kolejności hello polecenia.  Witaj operationId musi być unikatowa.

Po wywołaniu metody pomyślnie hello Start interfejsu API powitalne GetProgress API powinna być wywoływana w pętli, dopóki hello zwrócił postępu właściwości stan obiektu jest ukończone.  Wszystkie [w FabricTransientException] [ fte] i jego operationcanceledexception — należy wykonać ponownie.
Po osiągnięciu terminali stanu (ukończone, Faulted lub odwołania) polecenia hello hello zwrócił Właściwość Result obiekt postępu ma dodatkowe informacje.  Jeśli stan hello jest ukończona, Result.SelectedPartition.PartitionId będzie zawierać identyfikator partycji hello, który został wybrany.  Result.Exception będzie równy null.  Jeśli stan hello jest uszkodzona, Result.Exception będzie mieć hello Przyczyna hello iniekcji błędów i polecenia hello usługi analizy wystąpił błąd.  Result.SelectedPartition.PartitionId będzie miał hello identyfikator partycji, który został wybrany.  W niektórych sytuacjach hello polecenia może nie mieć prowadzi wystarczający toochoose partycji.  W takim przypadku hello PartitionId będzie równa 0.  Jeśli stan hello zostało anulowane, Result.Exception będzie równy null.  Podobnie jak hello przypadku Faulted Result.SelectedPartition.PartitionId ma identyfikator partycji hello, która została wybrana, ale jeśli polecenie hello nie prowadzi wystarczający toodo tak, będzie równa 0.  Można również znaleźć poniższy przykład toohello.

Hello Poniższy przykładowy kod przedstawia sposób toostart następnie sprawdzić postęp na utratę danych toocause polecenia na określonej partycji.

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

Poniższy przykład Hello pokazuje, jak toouse hello toochoose elementu PartitionSelector losowe partycji określonej usługi:

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a>Historia i obcięcie
Po osiągnięciu terminali stanu polecenia metadanych pozostanie w hello iniekcji błędów i usunąć usługi analizy przez pewien czas, zanim będzie on toosave miejsca.  "GetProgress" jest wywoływana przy użyciu operationId hello polecenia, po jego usunięciu, zwróci FabricException z ErrorCode KeyNotFound.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
