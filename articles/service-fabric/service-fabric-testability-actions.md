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
# <a name="testability-actions"></a><span data-ttu-id="c4aab-103">Testowania czynności</span><span class="sxs-lookup"><span data-stu-id="c4aab-103">Testability actions</span></span>
<span data-ttu-id="c4aab-104">W kolejności toosimulate zawodnych infrastruktury sieć szkieletowa usług Azure udostępnia, hello dewelopera, przy użyciu metody toosimulate różnych rzeczywistych błędów i przejścia stanu.</span><span class="sxs-lookup"><span data-stu-id="c4aab-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="c4aab-105">Są one widoczne jako testowania czynności.</span><span class="sxs-lookup"><span data-stu-id="c4aab-105">These are exposed as testability actions.</span></span> <span data-ttu-id="c4aab-106">Akcje Hello są hello niskiego poziomu interfejsów API, które powodują iniekcji określonych błędów, przejście stanu lub sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="c4aab-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="c4aab-107">Łącząc te akcje można zapisywać scenariusze kompleksowego testowania dla usług.</span><span class="sxs-lookup"><span data-stu-id="c4aab-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="c4aab-108">Sieć szkieletowa usług zawiera kilka typowych scenariuszy testu składa się z tych akcji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="c4aab-109">Zdecydowanie zaleca się korzystanie z tych scenariuszy wbudowanych, które dokładnie wybrano tootest wspólnej przejść stanu oraz przypadki niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="c4aab-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="c4aab-110">Jednak akcji może być używane toocreate testu scenariuszy należy tooadd pokrycia w scenariuszach, które nie są objęte scenariusze wbudowanych hello jeszcze lub które są niestandardowe dostosowane do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="c4aab-111">C# implementacje akcje hello znajdują się w hello System.Fabric.dll zestawu.</span><span class="sxs-lookup"><span data-stu-id="c4aab-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="c4aab-112">Moduł PowerShell sieci szkieletowej systemu Hello znajduje się w hello Microsoft.ServiceFabric.Powershell.dll zestawu.</span><span class="sxs-lookup"><span data-stu-id="c4aab-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="c4aab-113">W ramach instalacji środowiska uruchomieniowego hello modułu ServiceFabric programu PowerShell jest zainstalowane tooallow dla łatwość użycia.</span><span class="sxs-lookup"><span data-stu-id="c4aab-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="c4aab-114">Bezpieczne, a błąd nieprawidłowego działania</span><span class="sxs-lookup"><span data-stu-id="c4aab-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="c4aab-115">Testowania czynności dzieli się na dwie główne pakiety:</span><span class="sxs-lookup"><span data-stu-id="c4aab-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="c4aab-116">Błędy nieprawidłowego: te błędy symulacji awarii, takie jak ponowne uruchomienie komputera i awarii procesów.</span><span class="sxs-lookup"><span data-stu-id="c4aab-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="c4aab-117">W takich przypadkach niepowodzenia hello kontekstu wykonywania procesu zatrzymuje nagle.</span><span class="sxs-lookup"><span data-stu-id="c4aab-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="c4aab-118">Oznacza to, że nie oczyszczania stanu hello można uruchomić, zanim aplikacji hello uruchamiany ponownie.</span><span class="sxs-lookup"><span data-stu-id="c4aab-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="c4aab-119">Błędy bezpiecznie: te błędy symulować łagodne akcje jak przenosi repliki i porzucania wyzwalane przez równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c4aab-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="c4aab-120">W takich przypadkach usługi hello pobiera powiadomienie z informacją o hello Zamknij i wyczyścić stanu hello przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="c4aab-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="c4aab-121">Dla lepszej jakości weryfikacji, należy uruchomić usługę hello i firm obciążenie podczas wywołania różnych bezpieczne i nieprawidłowego błędów.</span><span class="sxs-lookup"><span data-stu-id="c4aab-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="c4aab-122">Błędy nieprawidłowego wykonuje scenariuszy, w którym hello usługi proces nagle kończy się w środku hello niektórych przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="c4aab-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="c4aab-123">Testy hello ścieżka odzyskiwania, po przywróceniu repliki usługi hello przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="c4aab-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="c4aab-124">To może pomóc w testowania spójności danych i czy stan usługi hello jest poprawnie utrzymywany po awarii.</span><span class="sxs-lookup"><span data-stu-id="c4aab-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="c4aab-125">Witaj drugi zestaw błędów (hello łagodne awarii) testu czy usługa hello poprawnie reaguje tooreplicas przenoszenie przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="c4aab-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="c4aab-126">Obsługa anulowania to testów w metodzie RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="c4aab-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="c4aab-127">Usługa Hello musi toocheck hello anulowania tokenu jest ustawiona, poprawnie zapisać jej stan, a następnie zamknij hello metodzie RunAsync.</span><span class="sxs-lookup"><span data-stu-id="c4aab-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="c4aab-128">Pola listy Akcje</span><span class="sxs-lookup"><span data-stu-id="c4aab-128">Testability actions list</span></span>
| <span data-ttu-id="c4aab-129">Akcja</span><span class="sxs-lookup"><span data-stu-id="c4aab-129">Action</span></span> | <span data-ttu-id="c4aab-130">Opis</span><span class="sxs-lookup"><span data-stu-id="c4aab-130">Description</span></span> | <span data-ttu-id="c4aab-131">Zarządzanego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="c4aab-131">Managed API</span></span> | <span data-ttu-id="c4aab-132">Polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4aab-132">PowerShell cmdlet</span></span> | <span data-ttu-id="c4aab-133">Bezpieczne/nieprawidłowego błędów</span><span class="sxs-lookup"><span data-stu-id="c4aab-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c4aab-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="c4aab-134">CleanTestState</span></span> |<span data-ttu-id="c4aab-135">Usuwa wszystkie stanu testu hello z klastra hello w przypadku zły zamknięcia hello testu sterownika.</span><span class="sxs-lookup"><span data-stu-id="c4aab-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="c4aab-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-136">CleanTestStateAsync</span></span> |<span data-ttu-id="c4aab-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="c4aab-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="c4aab-138">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c4aab-138">Not applicable</span></span> |
| <span data-ttu-id="c4aab-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="c4aab-139">InvokeDataLoss</span></span> |<span data-ttu-id="c4aab-140">Powoduje utratę danych na partycji usługi.</span><span class="sxs-lookup"><span data-stu-id="c4aab-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="c4aab-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="c4aab-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="c4aab-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="c4aab-143">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="c4aab-143">Graceful</span></span> |
| <span data-ttu-id="c4aab-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="c4aab-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="c4aab-145">Umieszcza partycji danej usługi stanowej, w wyniku utraty kworum.</span><span class="sxs-lookup"><span data-stu-id="c4aab-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="c4aab-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="c4aab-147">Wywołanie ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="c4aab-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="c4aab-148">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="c4aab-148">Graceful</span></span> |
| <span data-ttu-id="c4aab-149">Przenoszenie podstawowej</span><span class="sxs-lookup"><span data-stu-id="c4aab-149">Move Primary</span></span> |<span data-ttu-id="c4aab-150">Przenosi hello określić podstawową replikę usługi stanowej toohello określony węzeł klastra.</span><span class="sxs-lookup"><span data-stu-id="c4aab-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="c4aab-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-151">MovePrimaryAsync</span></span> |<span data-ttu-id="c4aab-152">Przenieś ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="c4aab-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="c4aab-153">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="c4aab-153">Graceful</span></span> |
| <span data-ttu-id="c4aab-154">Przenieś pomocniczej</span><span class="sxs-lookup"><span data-stu-id="c4aab-154">Move Secondary</span></span> |<span data-ttu-id="c4aab-155">Przenosi hello bieżącego pomocniczej replice usługi stanowej tooa inny węzeł klastra.</span><span class="sxs-lookup"><span data-stu-id="c4aab-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="c4aab-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="c4aab-157">Przenieś ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="c4aab-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="c4aab-158">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="c4aab-158">Graceful</span></span> |
| <span data-ttu-id="c4aab-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="c4aab-159">RemoveReplica</span></span> |<span data-ttu-id="c4aab-160">Symuluje awarii repliki poprzez usunięcie repliki z klastra.</span><span class="sxs-lookup"><span data-stu-id="c4aab-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="c4aab-161">To spowoduje zamknięcie hello repliki i przejdą toorole "None", usunięcie wszystkich jego stanu z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="c4aab-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="c4aab-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="c4aab-163">Usuń ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="c4aab-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="c4aab-164">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="c4aab-164">Graceful</span></span> |
| <span data-ttu-id="c4aab-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="c4aab-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="c4aab-166">Symuluje awarii procesu pakietu kodu przez ponowne uruchomienie pakiet kodu wdrożonych na węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c4aab-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="c4aab-167">To przerywa proces pakietu kodu hello, który zostanie uruchomiony ponownie wszystkie repliki hello użytkownika usługi, obsługiwane w tym procesie.</span><span class="sxs-lookup"><span data-stu-id="c4aab-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="c4aab-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="c4aab-169">ServiceFabricDeployedCodePackage ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="c4aab-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="c4aab-170">Nieprawidłowego</span><span class="sxs-lookup"><span data-stu-id="c4aab-170">Ungraceful</span></span> |
| <span data-ttu-id="c4aab-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="c4aab-171">RestartNode</span></span> |<span data-ttu-id="c4aab-172">Symuluje awarii węzła klastra sieci szkieletowej usług przez ponowne uruchomienie węzła.</span><span class="sxs-lookup"><span data-stu-id="c4aab-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="c4aab-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-173">RestartNodeAsync</span></span> |<span data-ttu-id="c4aab-174">ServiceFabricNode ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="c4aab-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="c4aab-175">Nieprawidłowego</span><span class="sxs-lookup"><span data-stu-id="c4aab-175">Ungraceful</span></span> |
| <span data-ttu-id="c4aab-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="c4aab-176">RestartPartition</span></span> |<span data-ttu-id="c4aab-177">Symuluje scenariusza niedostępności klastra lub niedostępności centrum danych przez ponowne uruchomienie niektórych lub wszystkich replik partycji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="c4aab-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-178">RestartPartitionAsync</span></span> |<span data-ttu-id="c4aab-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="c4aab-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="c4aab-180">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="c4aab-180">Graceful</span></span> |
| <span data-ttu-id="c4aab-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="c4aab-181">RestartReplica</span></span> |<span data-ttu-id="c4aab-182">Symuluje awarii repliki ponownego uruchamiania utrwalonych repliki w klastrze, zamykając hello repliki i otworzyć go ponownie.</span><span class="sxs-lookup"><span data-stu-id="c4aab-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="c4aab-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-183">RestartReplicaAsync</span></span> |<span data-ttu-id="c4aab-184">ServiceFabricReplica ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="c4aab-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="c4aab-185">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="c4aab-185">Graceful</span></span> |
| <span data-ttu-id="c4aab-186">Parametr StartNode</span><span class="sxs-lookup"><span data-stu-id="c4aab-186">StartNode</span></span> |<span data-ttu-id="c4aab-187">Rozpoczyna się węzeł w klastrze, który jest już zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="c4aab-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="c4aab-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-188">StartNodeAsync</span></span> |<span data-ttu-id="c4aab-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="c4aab-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="c4aab-190">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c4aab-190">Not applicable</span></span> |
| <span data-ttu-id="c4aab-191">Polecenie StopNode</span><span class="sxs-lookup"><span data-stu-id="c4aab-191">StopNode</span></span> |<span data-ttu-id="c4aab-192">Symuluje awarii węzła przez zatrzymanie węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c4aab-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="c4aab-193">węzeł Hello pozostanie w dół do momentu parametr StartNode jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="c4aab-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="c4aab-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-194">StopNodeAsync</span></span> |<span data-ttu-id="c4aab-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="c4aab-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="c4aab-196">Nieprawidłowego</span><span class="sxs-lookup"><span data-stu-id="c4aab-196">Ungraceful</span></span> |
| <span data-ttu-id="c4aab-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="c4aab-197">ValidateApplication</span></span> |<span data-ttu-id="c4aab-198">Sprawdza dostępność hello i kondycję wszystkich usług sieci szkieletowej usług aplikacji, zwykle po wywołania niektórych błędów w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="c4aab-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="c4aab-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="c4aab-200">ServiceFabricApplication testu</span><span class="sxs-lookup"><span data-stu-id="c4aab-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="c4aab-201">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c4aab-201">Not applicable</span></span> |
| <span data-ttu-id="c4aab-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="c4aab-202">ValidateService</span></span> |<span data-ttu-id="c4aab-203">Sprawdza dostępność hello i kondycji usługi Service Fabric, zwykle po wywołania niektórych błędów w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="c4aab-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="c4aab-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="c4aab-204">ValidateServiceAsync</span></span> |<span data-ttu-id="c4aab-205">ServiceFabricService testu</span><span class="sxs-lookup"><span data-stu-id="c4aab-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="c4aab-206">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c4aab-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="c4aab-207">Uruchomienie akcji testowania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4aab-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="c4aab-208">W tym samouczku przedstawiono sposób toorun akcją testowania przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aab-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="c4aab-209">Dowiesz się jak toorun akcją kontroli względem klastra lokalnego (jeden pole) lub klastrze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aab-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="c4aab-210">Microsoft.Fabric.Powershell.dll — Witaj modułu programu PowerShell dla usługi sieci szkieletowej — jest instalowana automatycznie podczas instalowania hello MSI sieci szkieletowej usług firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c4aab-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="c4aab-211">Moduł Hello jest ładowane automatycznie podczas otwierania wiersza programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aab-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="c4aab-212">Samouczek segmentów:</span><span class="sxs-lookup"><span data-stu-id="c4aab-212">Tutorial segments:</span></span>

* [<span data-ttu-id="c4aab-213">Uruchom akcję w odniesieniu do klastra z jednym polu</span><span class="sxs-lookup"><span data-stu-id="c4aab-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="c4aab-214">Uruchom akcję względem klastra platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c4aab-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="c4aab-215">Uruchom akcję w odniesieniu do klastra z jednym polu</span><span class="sxs-lookup"><span data-stu-id="c4aab-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="c4aab-216">toorun akcję kontroli w odniesieniu do klastra lokalnego, podłącz najpierw toohello klastra i otwórz hello wierszu polecenia PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="c4aab-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="c4aab-217">Daj nam przyjrzeć się hello **ServiceFabricNode ponowne uruchomienie** akcji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="c4aab-218">W tym miejscu hello akcji **ServiceFabricNode ponowne uruchomienie** jest uruchamiana w węźle o nazwie "Node1".</span><span class="sxs-lookup"><span data-stu-id="c4aab-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="c4aab-219">Tryb uzupełniania Hello Określa, że także powinien sprawdza, czy akcja ponownego uruchomienia węzła hello faktycznie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c4aab-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="c4aab-220">Określanie tryb uzupełniania hello jako "Zweryfikuj" spowoduje jego tooverify czy akcja ponownego uruchomienia hello faktycznie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c4aab-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="c4aab-221">Zamiast bezpośrednio określać hello węzła przy użyciu nazwy, możesz je określić za pomocą rodzaj partycji klucza i hello replik, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c4aab-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="c4aab-222">**Ponowne uruchomienie ServiceFabricNode** powinny być używane toorestart węzeł sieci szkieletowej usług w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c4aab-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="c4aab-223">Spowoduje to zatrzymanie proces Fabric.exe hello, który zostanie uruchomiony ponownie wszystkie hello system usługi i użytkowników usługi replik hostowanych w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="c4aab-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="c4aab-224">Użycie tootest tego interfejsu API usługi ułatwia odkrywanie usterki wzdłuż ścieżki odzyskiwania trybu failover hello.</span><span class="sxs-lookup"><span data-stu-id="c4aab-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="c4aab-225">Pomaga symulacji awarii węzła w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c4aab-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="c4aab-226">Witaj Poniższy zrzut ekranu przedstawia hello **ServiceFabricNode ponowne uruchomienie** polecenia kontroli w akcji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="c4aab-227">Witaj dane wyjściowe z hello najpierw **Get-ServiceFabricNode** (polecenia cmdlet z modułu programu PowerShell usługi Service Fabric hello) zawiera klastra lokalne powitania zawiera pięć węzłów: Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="c4aab-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="c4aab-228">Po akcji zmianę hello (polecenia cmdlet) **ServiceFabricNode ponowne uruchomienie** jest wykonywana w węźle hello o nazwie Node.4, przedstawia czas pracy tego węzła hello został zresetowany.</span><span class="sxs-lookup"><span data-stu-id="c4aab-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="c4aab-229">Uruchom akcję względem klastra platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c4aab-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="c4aab-230">Uruchomienie akcji pola (przy użyciu programu PowerShell) względem klastra platformy Azure jest podobne kroki hello toorunning w odniesieniu do klastra lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c4aab-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="c4aab-231">Witaj tylko różnicą jest to, że przed uruchomieniem akcji hello, zamiast łączącego toohello klastra lokalnego, należy tooconnect toohello Azure najpierw klastra.</span><span class="sxs-lookup"><span data-stu-id="c4aab-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="c4aab-232">Uruchomienie akcji testowania w języku C & 35;</span><span class="sxs-lookup"><span data-stu-id="c4aab-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="c4aab-233">toorun akcją testowania przy użyciu języka C#, należy najpierw tooconnect toohello klastra przy użyciu klienta fabricclient z rolą.</span><span class="sxs-lookup"><span data-stu-id="c4aab-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="c4aab-234">Następnie Uzyskaj hello parametry potrzebne toorun hello akcji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="c4aab-235">Można użyć różnych parametrów toorun hello tę samą akcję.</span><span class="sxs-lookup"><span data-stu-id="c4aab-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="c4aab-236">Spojrzenie na powitania RestartServiceFabricNode akcji, jednokierunkowej toorun, jest przy użyciu informacji węzła hello (nazwy węzła i identyfikator wystąpienia węzła) w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c4aab-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="c4aab-237">Objaśnienie parametrów:</span><span class="sxs-lookup"><span data-stu-id="c4aab-237">Parameter explanation:</span></span>

* <span data-ttu-id="c4aab-238">**CompleteMode** Określa, że tryb hello nie sprawdzić, czy akcja ponownego uruchomienia hello faktycznie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c4aab-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="c4aab-239">Określanie tryb uzupełniania hello jako "Zweryfikuj" spowoduje jego tooverify czy akcja ponownego uruchomienia hello faktycznie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c4aab-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="c4aab-240">**OperationTimeout** zestawy hello czas toofinish operacji hello przed jest zgłaszany wyjątek TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="c4aab-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="c4aab-241">**CancellationToken** umożliwia toobe oczekujące wywołanie, anulowane.</span><span class="sxs-lookup"><span data-stu-id="c4aab-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="c4aab-242">Zamiast bezpośrednio określać hello węzła przy użyciu nazwy, możesz je określić za pomocą rodzaj partycji klucza i hello repliki.</span><span class="sxs-lookup"><span data-stu-id="c4aab-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="c4aab-243">Aby uzyskać więcej informacji, zobacz [elementu PartitionSelector i elementu ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="c4aab-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="c4aab-244">Elementu PartitionSelector i elementu ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="c4aab-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="c4aab-245">Elementu PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="c4aab-245">PartitionSelector</span></span>
<span data-ttu-id="c4aab-246">Elementu PartitionSelector jest pomocnika ujawnione podczas testowania i jest używany tooselect określonej partycji na które tooperform hello testowania czynności.</span><span class="sxs-lookup"><span data-stu-id="c4aab-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="c4aab-247">Jeśli identyfikator partycji: hello jest znany wcześniej może być używane tooselect określonej partycji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="c4aab-248">Lub, możesz podać klucz partycji hello i operacji hello rozwiąże identyfikator partycji: hello wewnętrznie.</span><span class="sxs-lookup"><span data-stu-id="c4aab-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="c4aab-249">Istnieje również opcja hello losowe partycji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="c4aab-250">toouse tego pomocnika tworzenia obiektu elementu PartitionSelector hello i wybierz partycję hello przy użyciu jednej z hello Select * metod.</span><span class="sxs-lookup"><span data-stu-id="c4aab-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="c4aab-251">Następnie przekazać hello elementu PartitionSelector obiektu toohello interfejsu API, która go wymaga.</span><span class="sxs-lookup"><span data-stu-id="c4aab-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="c4aab-252">Jeśli wybrano opcję nie, domyślnie tooa losowe partycji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-252">If no option is selected, it defaults tooa random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="c4aab-253">Elementu ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="c4aab-253">ReplicaSelector</span></span>
<span data-ttu-id="c4aab-254">Elementu ReplicaSelector jest pomocnika ujawnione podczas testowania i jest używany toohelp Wybierz replikę, na które tooperform hello testowania czynności.</span><span class="sxs-lookup"><span data-stu-id="c4aab-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="c4aab-255">Identyfikator repliki hello jest znany wcześniej może być używane tooselect określonych repliki.</span><span class="sxs-lookup"><span data-stu-id="c4aab-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="c4aab-256">Ponadto można jeszcze hello opcja repliki podstawowej lub dodatkowej losowych.</span><span class="sxs-lookup"><span data-stu-id="c4aab-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="c4aab-257">Elementu ReplicaSelector pochodzi z elementu PartitionSelector, warto tooselect hello zarówno repliki i hello partycji, na którym chcesz tooperform hello zmianę operacji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="c4aab-258">toouse tego pomocnika, Utwórz obiekt elementu ReplicaSelector i ustaw sposób hello tooselect hello repliki i hello partycji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="c4aab-259">Można następnie przekazać do hello interfejsu API, która go wymaga.</span><span class="sxs-lookup"><span data-stu-id="c4aab-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="c4aab-260">Jeśli wybrano opcję nie, domyślnie tooa losowe repliki i losowe partycji.</span><span class="sxs-lookup"><span data-stu-id="c4aab-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c4aab-261">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4aab-261">Next steps</span></span>
* [<span data-ttu-id="c4aab-262">Scenariusze testowania</span><span class="sxs-lookup"><span data-stu-id="c4aab-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="c4aab-263">Jak tootest usługi</span><span class="sxs-lookup"><span data-stu-id="c4aab-263">How tootest your service</span></span>
  * [<span data-ttu-id="c4aab-264">Symulacji awarii podczas obciążeń usługi</span><span class="sxs-lookup"><span data-stu-id="c4aab-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="c4aab-265">Błędy usługi do komunikacji</span><span class="sxs-lookup"><span data-stu-id="c4aab-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

