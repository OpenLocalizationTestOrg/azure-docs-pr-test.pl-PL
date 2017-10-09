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
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="dc6a2-103">Jak tooInvoke utraty danych w usługach</span><span class="sxs-lookup"><span data-stu-id="dc6a2-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="dc6a2-104">Tym dokumencie opisano sposób toocause utraty danych w usługach i powinna być używana z rozwagą.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="dc6a2-105">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="dc6a2-105">Introduction</span></span>
<span data-ttu-id="dc6a2-106">Utrata danych na partycji usługi sieć szkieletowa usług przez wywołanie StartPartitionDataLossAsync() można wywołać.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="dc6a2-107">Ten interfejs api korzysta hello iniekcji błędów i Analysis Service tooperform hello pracy toocause danych utraty warunków.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="dc6a2-108">Przy użyciu hello iniekcji błędów i usługi analizy</span><span class="sxs-lookup"><span data-stu-id="dc6a2-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="dc6a2-109">Hello iniekcji błędów i Analysis Service obecnie obsługuje następujące interfejsy API w poniższej tabeli hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="dc6a2-110">powitania po prawej stronie wykresu hello pokazuje hello odpowiednie polecenie cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="dc6a2-111">Aby uzyskać więcej informacji na temat każdej z nich można znaleźć w dokumentacji msdn toohello w każdym interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="dc6a2-112">INTERFEJS API JĘZYKA C#</span><span class="sxs-lookup"><span data-stu-id="dc6a2-112">C# API</span></span> | <span data-ttu-id="dc6a2-113">Polecenia Cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc6a2-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="dc6a2-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="dc6a2-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="dc6a2-115">[Start ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="dc6a2-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="dc6a2-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="dc6a2-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="dc6a2-117">[Start ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="dc6a2-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="dc6a2-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="dc6a2-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="dc6a2-119">[Start ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="dc6a2-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="dc6a2-120">Omówienie pojęć dotyczących uruchomiono polecenie</span><span class="sxs-lookup"><span data-stu-id="dc6a2-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="dc6a2-121">Witaj iniekcji błędów i Analysis Services używa modelu asynchroniczne, gdzie rozpoczęciem powitalne polecenie z jednego interfejsu API, określonego interfejsu API "Start" hello tooas tego dokumentu, a następnie postęp hello kontroli tego polecenia przy użyciu interfejsu API "GetProgress", dopóki osiągnie terminal Stan, lub do czasu można anulować.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="dc6a2-122">toostart polecenia, wywołania interfejsu API hello "Start" hello odpowiedniego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="dc6a2-123">Ten interfejs API zwraca podczas hello iniekcji błędów i Analysis Service zaakceptował Żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="dc6a2-124">Jednak nie oznacza jakim zostało uruchomione polecenie, lub nawet jeśli została ona jeszcze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="dc6a2-125">Trwa kolejności toocheck polecenia należy wywołać hello "GetProgress" interfejsu API, który odpowiada toohello "Start" interfejsu API wcześniej nazywane.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="dc6a2-126">Witaj "GetProgress" interfejsu API będzie zwracać wskazująca bieżący stan hello polecenia hello wewnątrz jego właściwość stanu obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="dc6a2-127">Polecenie działa przez czas nieokreślony do:</span><span class="sxs-lookup"><span data-stu-id="dc6a2-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="dc6a2-128">Pomyślnie zakończy działanie.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-128">It completes successfully.</span></span>  <span data-ttu-id="dc6a2-129">Jeśli w tym przypadku wywołać "GetProgress" na nim, stan obiektu postępu hello zostanie ukończona.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="dc6a2-130">Napotkania błędu krytycznego.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-130">It encounters a fatal error.</span></span>  <span data-ttu-id="dc6a2-131">Jeśli w tym przypadku wywołać "GetProgress" na nim, stan obiektu postępu hello wystąpi błąd</span><span class="sxs-lookup"><span data-stu-id="dc6a2-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="dc6a2-132">Możesz anulować za pośrednictwem hello [CancelTestCommandAsync] [ cancel] interfejsu API, lub [Stop-ServiceFabricTestCommand] [ cancelps] polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="dc6a2-133">Jeśli w tym przypadku wywołać "GetProgress" na nim, hello stan obiektu postęp będzie odwołania lub ForceCancelled, w zależności od argumentu toothat interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="dc6a2-134">Zapoznaj się dokumentacją hello [CancelTestCommandAsync] [ cancel] więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="dc6a2-135">Szczegółowe informacje o uruchamianiu polecenia</span><span class="sxs-lookup"><span data-stu-id="dc6a2-135">Details of Running a Command</span></span>
<span data-ttu-id="dc6a2-136">W kolejności toostart polecenia należy wywołać hello Start interfejsu API z argumentami hello oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="dc6a2-137">Wszystkie interfejsy API Start użyć argumentu Guid o nazwie operationId.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="dc6a2-138">Użytkownik powinien zachować informacje o hello operationId argument, ponieważ jest on używany postępu tootrack tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="dc6a2-139">Musi być przekazany hello "GetProgress" interfejsu API w toku tootrack kolejności hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="dc6a2-140">Witaj operationId musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-140">hello operationId must be unique.</span></span>

<span data-ttu-id="dc6a2-141">Po wywołaniu metody pomyślnie hello Start interfejsu API powitalne GetProgress API powinna być wywoływana w pętli, dopóki hello zwrócił postępu właściwości stan obiektu jest ukończone.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="dc6a2-142">Wszystkie [w FabricTransientException] [ fte] i jego operationcanceledexception — należy wykonać ponownie.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="dc6a2-143">Po osiągnięciu terminali stanu (ukończone, Faulted lub odwołania) polecenia hello hello zwrócił Właściwość Result obiekt postępu ma dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="dc6a2-144">Jeśli stan hello jest ukończona, Result.SelectedPartition.PartitionId będzie zawierać identyfikator partycji hello, który został wybrany.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="dc6a2-145">Result.Exception będzie równy null.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-145">Result.Exception will be null.</span></span>  <span data-ttu-id="dc6a2-146">Jeśli stan hello jest uszkodzona, Result.Exception będzie mieć hello Przyczyna hello iniekcji błędów i polecenia hello usługi analizy wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="dc6a2-147">Result.SelectedPartition.PartitionId będzie miał hello identyfikator partycji, który został wybrany.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="dc6a2-148">W niektórych sytuacjach hello polecenia może nie mieć prowadzi wystarczający toochoose partycji.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="dc6a2-149">W takim przypadku hello PartitionId będzie równa 0.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="dc6a2-150">Jeśli stan hello zostało anulowane, Result.Exception będzie równy null.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="dc6a2-151">Podobnie jak hello przypadku Faulted Result.SelectedPartition.PartitionId ma identyfikator partycji hello, która została wybrana, ale jeśli polecenie hello nie prowadzi wystarczający toodo tak, będzie równa 0.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="dc6a2-152">Można również znaleźć poniższy przykład toohello.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="dc6a2-153">Hello Poniższy przykładowy kod przedstawia sposób toostart następnie sprawdzić postęp na utratę danych toocause polecenia na określonej partycji.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

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

<span data-ttu-id="dc6a2-154">Poniższy przykład Hello pokazuje, jak toouse hello toochoose elementu PartitionSelector losowe partycji określonej usługi:</span><span class="sxs-lookup"><span data-stu-id="dc6a2-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

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

## <a name="history-and-truncation"></a><span data-ttu-id="dc6a2-155">Historia i obcięcie</span><span class="sxs-lookup"><span data-stu-id="dc6a2-155">History and Truncation</span></span>
<span data-ttu-id="dc6a2-156">Po osiągnięciu terminali stanu polecenia metadanych pozostanie w hello iniekcji błędów i usunąć usługi analizy przez pewien czas, zanim będzie on toosave miejsca.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="dc6a2-157">"GetProgress" jest wywoływana przy użyciu operationId hello polecenia, po jego usunięciu, zwróci FabricException z ErrorCode KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="dc6a2-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
