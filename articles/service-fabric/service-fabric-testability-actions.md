---
title: "Symulacji awarii w Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje o akcji zmianę w usługi sieć szkieletowa usług Microsoft Azure."
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
ms.openlocfilehash: c8ddc7732999ae555323bebaef60aa34c8f2ec17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="testability-actions"></a><span data-ttu-id="eefb1-103">Testowania czynności</span><span class="sxs-lookup"><span data-stu-id="eefb1-103">Testability actions</span></span>
<span data-ttu-id="eefb1-104">Aby symulować zawodnych infrastruktury, sieć szkieletowa usług Azure udostępnia Tobie, deweloperze, ze sposobów, aby symulować różne błędy rzeczywistych i przejścia stanu.</span><span class="sxs-lookup"><span data-stu-id="eefb1-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span></span> <span data-ttu-id="eefb1-105">Są one widoczne jako testowania czynności.</span><span class="sxs-lookup"><span data-stu-id="eefb1-105">These are exposed as testability actions.</span></span> <span data-ttu-id="eefb1-106">Akcje są niskiego poziomu interfejsów API, które powodują iniekcji określonych błędów, przejście stanu lub sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="eefb1-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="eefb1-107">Łącząc te akcje można zapisywać scenariusze kompleksowego testowania dla usług.</span><span class="sxs-lookup"><span data-stu-id="eefb1-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="eefb1-108">Sieć szkieletowa usług zawiera kilka typowych scenariuszy testu składa się z tych akcji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="eefb1-109">Zdecydowanie zaleca się korzystanie z tych wbudowanych scenariuszy, które dokładnie chcą wspólnej przejść stanu i przypadków awarii.</span><span class="sxs-lookup"><span data-stu-id="eefb1-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span></span> <span data-ttu-id="eefb1-110">Jednak akcje może służyć do tworzenia scenariuszy testowania niestandardowych, jeśli chcesz dodać pokrycia w scenariuszach, które nie są objęte wbudowanych scenariusze jeszcze lub które są niestandardowe dostosowane do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="eefb1-111">C# implementacje akcje znajdują się w zestawie System.Fabric.dll.</span><span class="sxs-lookup"><span data-stu-id="eefb1-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span></span> <span data-ttu-id="eefb1-112">Moduł PowerShell sieci szkieletowej systemu znajduje się w zestawie Microsoft.ServiceFabric.Powershell.dll.</span><span class="sxs-lookup"><span data-stu-id="eefb1-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="eefb1-113">W ramach instalacji środowiska uruchomieniowego zainstalowano modułu ServiceFabric programu PowerShell umożliwiające łatwość użycia.</span><span class="sxs-lookup"><span data-stu-id="eefb1-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="eefb1-114">Bezpieczne, a błąd nieprawidłowego działania</span><span class="sxs-lookup"><span data-stu-id="eefb1-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="eefb1-115">Testowania czynności dzieli się na dwie główne pakiety:</span><span class="sxs-lookup"><span data-stu-id="eefb1-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="eefb1-116">Błędy nieprawidłowego: te błędy symulacji awarii, takie jak ponowne uruchomienie komputera i awarii procesów.</span><span class="sxs-lookup"><span data-stu-id="eefb1-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="eefb1-117">W takich przypadkach niepowodzenia kontekstu wykonywania procesu zatrzymuje nagle.</span><span class="sxs-lookup"><span data-stu-id="eefb1-117">In such cases of failures, the execution context of process stops abruptly.</span></span> <span data-ttu-id="eefb1-118">Oznacza to, że nie oczyszczania stanu można uruchomić, zanim uruchamiania aplikacji ponownie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-118">This means no cleanup of the state can run before the application starts up again.</span></span>
* <span data-ttu-id="eefb1-119">Błędy bezpiecznie: te błędy symulować łagodne akcje jak przenosi repliki i porzucania wyzwalane przez równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="eefb1-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="eefb1-120">W takiej sytuacji usługa pobiera powiadomienie po zamknięciu i wyczyścić stanu przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="eefb1-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span></span>

<span data-ttu-id="eefb1-121">Podczas wywołania różnych błędów bezpieczne i nieprawidłowego lepszą jakość sprawdzania poprawności, uruchamiać obciążenie usługi i biznesowych.</span><span class="sxs-lookup"><span data-stu-id="eefb1-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="eefb1-122">Błędy nieprawidłowego wykonuje scenariuszy, w którym proces usługi nagle kończy środku niektórych przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="eefb1-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span></span> <span data-ttu-id="eefb1-123">Testy ścieżka odzyskiwania, po przywróceniu repliki usługi przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="eefb1-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span></span> <span data-ttu-id="eefb1-124">To może pomóc w testowania spójności danych i określa, czy stan usługi jest prawidłowo utrzymywany po awarii.</span><span class="sxs-lookup"><span data-stu-id="eefb1-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span></span> <span data-ttu-id="eefb1-125">Zestaw błędów (awarii bezpieczne) przetestować, czy usługa poprawnie reaguje na replik przenoszenie przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="eefb1-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span></span> <span data-ttu-id="eefb1-126">Obsługa anulowania to testów w metodzie RunAsync.</span><span class="sxs-lookup"><span data-stu-id="eefb1-126">This tests handling of cancellation in the RunAsync method.</span></span> <span data-ttu-id="eefb1-127">Usługa musi Sprawdź, czy token anulowania jest ustawiona, poprawnie zapisać jej stan, a następnie zamknij metodzie RunAsync.</span><span class="sxs-lookup"><span data-stu-id="eefb1-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="eefb1-128">Pola listy Akcje</span><span class="sxs-lookup"><span data-stu-id="eefb1-128">Testability actions list</span></span>
| <span data-ttu-id="eefb1-129">Akcja</span><span class="sxs-lookup"><span data-stu-id="eefb1-129">Action</span></span> | <span data-ttu-id="eefb1-130">Opis</span><span class="sxs-lookup"><span data-stu-id="eefb1-130">Description</span></span> | <span data-ttu-id="eefb1-131">Zarządzanego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="eefb1-131">Managed API</span></span> | <span data-ttu-id="eefb1-132">Polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eefb1-132">PowerShell cmdlet</span></span> | <span data-ttu-id="eefb1-133">Bezpieczne/nieprawidłowego błędów</span><span class="sxs-lookup"><span data-stu-id="eefb1-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="eefb1-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="eefb1-134">CleanTestState</span></span> |<span data-ttu-id="eefb1-135">Usuwa wszystkie stanu testu z klastra w przypadku zły wyłączania sterownika testu.</span><span class="sxs-lookup"><span data-stu-id="eefb1-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span></span> |<span data-ttu-id="eefb1-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-136">CleanTestStateAsync</span></span> |<span data-ttu-id="eefb1-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="eefb1-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="eefb1-138">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="eefb1-138">Not applicable</span></span> |
| <span data-ttu-id="eefb1-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="eefb1-139">InvokeDataLoss</span></span> |<span data-ttu-id="eefb1-140">Powoduje utratę danych na partycji usługi.</span><span class="sxs-lookup"><span data-stu-id="eefb1-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="eefb1-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="eefb1-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="eefb1-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="eefb1-143">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="eefb1-143">Graceful</span></span> |
| <span data-ttu-id="eefb1-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="eefb1-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="eefb1-145">Umieszcza partycji danej usługi stanowej, w wyniku utraty kworum.</span><span class="sxs-lookup"><span data-stu-id="eefb1-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="eefb1-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="eefb1-147">Wywołanie ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="eefb1-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="eefb1-148">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="eefb1-148">Graceful</span></span> |
| <span data-ttu-id="eefb1-149">Przenoszenie podstawowej</span><span class="sxs-lookup"><span data-stu-id="eefb1-149">Move Primary</span></span> |<span data-ttu-id="eefb1-150">Przenosi określony repliką podstawową usługi stanowej określony węzeł klastra.</span><span class="sxs-lookup"><span data-stu-id="eefb1-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span></span> |<span data-ttu-id="eefb1-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-151">MovePrimaryAsync</span></span> |<span data-ttu-id="eefb1-152">Przenieś ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="eefb1-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="eefb1-153">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="eefb1-153">Graceful</span></span> |
| <span data-ttu-id="eefb1-154">Przenieś pomocniczej</span><span class="sxs-lookup"><span data-stu-id="eefb1-154">Move Secondary</span></span> |<span data-ttu-id="eefb1-155">Przenosi bieżący pomocniczej replice usługi stanowej na inny węzeł klastra.</span><span class="sxs-lookup"><span data-stu-id="eefb1-155">Moves the current secondary replica of a stateful service to a different cluster node.</span></span> |<span data-ttu-id="eefb1-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="eefb1-157">Przenieś ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="eefb1-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="eefb1-158">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="eefb1-158">Graceful</span></span> |
| <span data-ttu-id="eefb1-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="eefb1-159">RemoveReplica</span></span> |<span data-ttu-id="eefb1-160">Symuluje awarii repliki poprzez usunięcie repliki z klastra.</span><span class="sxs-lookup"><span data-stu-id="eefb1-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="eefb1-161">To spowoduje zamknięcie repliki i przenieść ją do roli "None", usunięcie wszystkich jego stanu z klastra.</span><span class="sxs-lookup"><span data-stu-id="eefb1-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span></span> |<span data-ttu-id="eefb1-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="eefb1-163">Usuń ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="eefb1-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="eefb1-164">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="eefb1-164">Graceful</span></span> |
| <span data-ttu-id="eefb1-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="eefb1-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="eefb1-166">Symuluje awarii procesu pakietu kodu przez ponowne uruchomienie pakiet kodu wdrożonych na węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="eefb1-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="eefb1-167">Przerywa ten proces pakietu kodu, który zostanie uruchomiony ponownie wszystkie użytkownika repliki usługi hostowanej w tym procesie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span></span> |<span data-ttu-id="eefb1-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="eefb1-169">ServiceFabricDeployedCodePackage ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="eefb1-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="eefb1-170">Nieprawidłowego</span><span class="sxs-lookup"><span data-stu-id="eefb1-170">Ungraceful</span></span> |
| <span data-ttu-id="eefb1-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="eefb1-171">RestartNode</span></span> |<span data-ttu-id="eefb1-172">Symuluje awarii węzła klastra sieci szkieletowej usług przez ponowne uruchomienie węzła.</span><span class="sxs-lookup"><span data-stu-id="eefb1-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="eefb1-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-173">RestartNodeAsync</span></span> |<span data-ttu-id="eefb1-174">ServiceFabricNode ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="eefb1-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="eefb1-175">Nieprawidłowego</span><span class="sxs-lookup"><span data-stu-id="eefb1-175">Ungraceful</span></span> |
| <span data-ttu-id="eefb1-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="eefb1-176">RestartPartition</span></span> |<span data-ttu-id="eefb1-177">Symuluje scenariusza niedostępności klastra lub niedostępności centrum danych przez ponowne uruchomienie niektórych lub wszystkich replik partycji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="eefb1-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-178">RestartPartitionAsync</span></span> |<span data-ttu-id="eefb1-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="eefb1-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="eefb1-180">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="eefb1-180">Graceful</span></span> |
| <span data-ttu-id="eefb1-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="eefb1-181">RestartReplica</span></span> |<span data-ttu-id="eefb1-182">Symuluje awarii repliki ponownego uruchamiania utrwalonych repliki w klastrze, zamykając repliki i otworzyć go ponownie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span></span> |<span data-ttu-id="eefb1-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-183">RestartReplicaAsync</span></span> |<span data-ttu-id="eefb1-184">ServiceFabricReplica ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="eefb1-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="eefb1-185">Bezpieczne</span><span class="sxs-lookup"><span data-stu-id="eefb1-185">Graceful</span></span> |
| <span data-ttu-id="eefb1-186">Parametr StartNode</span><span class="sxs-lookup"><span data-stu-id="eefb1-186">StartNode</span></span> |<span data-ttu-id="eefb1-187">Rozpoczyna się węzeł w klastrze, który jest już zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="eefb1-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="eefb1-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-188">StartNodeAsync</span></span> |<span data-ttu-id="eefb1-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="eefb1-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="eefb1-190">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="eefb1-190">Not applicable</span></span> |
| <span data-ttu-id="eefb1-191">Polecenie StopNode</span><span class="sxs-lookup"><span data-stu-id="eefb1-191">StopNode</span></span> |<span data-ttu-id="eefb1-192">Symuluje awarii węzła przez zatrzymanie węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="eefb1-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="eefb1-193">Węzeł pozostanie w dół do momentu parametr StartNode jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="eefb1-193">The node will stay down until StartNode is called.</span></span> |<span data-ttu-id="eefb1-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-194">StopNodeAsync</span></span> |<span data-ttu-id="eefb1-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="eefb1-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="eefb1-196">Nieprawidłowego</span><span class="sxs-lookup"><span data-stu-id="eefb1-196">Ungraceful</span></span> |
| <span data-ttu-id="eefb1-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="eefb1-197">ValidateApplication</span></span> |<span data-ttu-id="eefb1-198">Sprawdza dostępność i kondycję wszystkich usług sieci szkieletowej usług aplikacji, zwykle po wywołania niektórych błędów w systemie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="eefb1-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="eefb1-200">ServiceFabricApplication testu</span><span class="sxs-lookup"><span data-stu-id="eefb1-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="eefb1-201">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="eefb1-201">Not applicable</span></span> |
| <span data-ttu-id="eefb1-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="eefb1-202">ValidateService</span></span> |<span data-ttu-id="eefb1-203">Sprawdza dostępność i kondycji usługi Service Fabric, zwykle po wywołania niektórych błędów w systemie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="eefb1-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="eefb1-204">ValidateServiceAsync</span></span> |<span data-ttu-id="eefb1-205">ServiceFabricService testu</span><span class="sxs-lookup"><span data-stu-id="eefb1-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="eefb1-206">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="eefb1-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="eefb1-207">Uruchomienie akcji testowania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eefb1-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="eefb1-208">Ten samouczek przedstawia sposób uruchamiania działania testowania przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eefb1-208">This tutorial shows you how to run a testability action by using PowerShell.</span></span> <span data-ttu-id="eefb1-209">Dowiesz się sposób uruchamiania działania kontroli względem klastra lokalnego (jeden pole) lub klastrze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eefb1-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="eefb1-210">Microsoft.Fabric.Powershell.dll — moduł programu PowerShell usługi Service Fabric — jest instalowana automatycznie podczas instalowania MSI sieci szkieletowej usług firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eefb1-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="eefb1-211">Moduł jest ładowane automatycznie podczas otwierania wiersza programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eefb1-211">The module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="eefb1-212">Samouczek segmentów:</span><span class="sxs-lookup"><span data-stu-id="eefb1-212">Tutorial segments:</span></span>

* [<span data-ttu-id="eefb1-213">Uruchom akcję w odniesieniu do klastra z jednym polu</span><span class="sxs-lookup"><span data-stu-id="eefb1-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="eefb1-214">Uruchom akcję względem klastra platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eefb1-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="eefb1-215">Uruchom akcję w odniesieniu do klastra z jednym polu</span><span class="sxs-lookup"><span data-stu-id="eefb1-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="eefb1-216">W celu uruchomienia działania kontroli klastra lokalnego, połącz się z klastrem i otwórz wiersz polecenia programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="eefb1-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="eefb1-217">Daj nam przyjrzeć się **ServiceFabricNode ponowne uruchomienie** akcji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-217">Let us look at the **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="eefb1-218">Tutaj akcji **ServiceFabricNode ponowne uruchomienie** jest uruchamiana w węźle o nazwie "Node1".</span><span class="sxs-lookup"><span data-stu-id="eefb1-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="eefb1-219">Tryb uzupełniania Określa, że także powinien sprawdza, czy ponowne uruchomienie węzła akcji faktycznie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span></span> <span data-ttu-id="eefb1-220">Określanie tryb uzupełniania jako "Weryfikuj" spowoduje, że należy sprawdzić, czy akcja ponownego uruchomienia faktycznie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="eefb1-221">Zamiast bezpośrednio określać węzła przy użyciu nazwy, możesz je określić za pomocą klucza partycji i rodzaj repliki, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eefb1-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="eefb1-222">**Ponowne uruchomienie ServiceFabricNode** należy ponownie uruchomić węzeł sieci szkieletowej usług w klastrze.</span><span class="sxs-lookup"><span data-stu-id="eefb1-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="eefb1-223">Spowoduje to zatrzymanie proces Fabric.exe, który zostanie uruchomiony ponownie wszystkie system usługi i użytkowników usługi repliki obsługiwane w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="eefb1-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="eefb1-224">Przy użyciu tego interfejsu API, aby przetestować usługi pomaga odkrywanie usterki wzdłuż ścieżki odzyskiwania trybu failover.</span><span class="sxs-lookup"><span data-stu-id="eefb1-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span></span> <span data-ttu-id="eefb1-225">Pomaga symulacji awarii węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="eefb1-225">It helps simulate node failures in the cluster.</span></span>

<span data-ttu-id="eefb1-226">Poniższy zrzut ekranu przedstawia **ServiceFabricNode ponowne uruchomienie** polecenia kontroli w akcji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="eefb1-227">Dane wyjściowe pierwszego **Get-ServiceFabricNode** (polecenia cmdlet z modułu programu PowerShell usługi Service Fabric) pokazuje, że klaster lokalny zawiera pięć węzłów: Node.1 do Node.5.</span><span class="sxs-lookup"><span data-stu-id="eefb1-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span></span> <span data-ttu-id="eefb1-228">Po testowania czynności (polecenia cmdlet) **ServiceFabricNode ponowne uruchomienie** jest wykonywana w węźle o nazwie Node.4, widzimy zresetowano węzła przestojów.</span><span class="sxs-lookup"><span data-stu-id="eefb1-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="eefb1-229">Uruchom akcję względem klastra platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eefb1-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="eefb1-230">Uruchomienie akcji pola (przy użyciu programu PowerShell) względem klastra platformy Azure jest podobny do uruchamiania działania klastra lokalnego.</span><span class="sxs-lookup"><span data-stu-id="eefb1-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span></span> <span data-ttu-id="eefb1-231">Jedyna różnica polega na tym, że przed uruchomieniem tej akcji, zamiast nawiązywania połączenia z lokalnym klastrem, należy połączyć się z klastrem Azure najpierw.</span><span class="sxs-lookup"><span data-stu-id="eefb1-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="eefb1-232">Uruchomienie akcji testowania w języku C & 35;</span><span class="sxs-lookup"><span data-stu-id="eefb1-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="eefb1-233">Aby uruchomić akcję testowania przy użyciu języka C#, musisz najpierw Połącz się z klastrem przy użyciu klienta fabricclient z rolą.</span><span class="sxs-lookup"><span data-stu-id="eefb1-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span></span> <span data-ttu-id="eefb1-234">Następnie Uzyskaj parametrów wymaganych do uruchomienia akcji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-234">Then obtain the parameters needed to run the action.</span></span> <span data-ttu-id="eefb1-235">Można użyć różnych parametrów do uruchomienia tego samego działania.</span><span class="sxs-lookup"><span data-stu-id="eefb1-235">Different parameters can be used to run the same action.</span></span>
<span data-ttu-id="eefb1-236">Jednym ze sposobów uruchamiania patrzeć akcji RestartServiceFabricNode, jest przy użyciu informacji węzła (nazwy węzła i identyfikator wystąpienia węzła) w klastrze.</span><span class="sxs-lookup"><span data-stu-id="eefb1-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="eefb1-237">Objaśnienie parametrów:</span><span class="sxs-lookup"><span data-stu-id="eefb1-237">Parameter explanation:</span></span>

* <span data-ttu-id="eefb1-238">**CompleteMode** Określa, czy tryb nie należy sprawdzić, czy akcja ponownego uruchomienia faktycznie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="eefb1-239">Określanie tryb uzupełniania jako "Weryfikuj" spowoduje, że należy sprawdzić, czy akcja ponownego uruchomienia faktycznie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="eefb1-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span>  
* <span data-ttu-id="eefb1-240">**OperationTimeout** ustawia czas operacji przed jest zgłaszany wyjątek TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="eefb1-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="eefb1-241">**CancellationToken** umożliwia oczekujące wywołanie do anulowania.</span><span class="sxs-lookup"><span data-stu-id="eefb1-241">**CancellationToken** enables a pending call to be canceled.</span></span>

<span data-ttu-id="eefb1-242">Zamiast bezpośrednio określać węzła przy użyciu nazwy, możesz je określić za pomocą klucza partycji i rodzaj repliki.</span><span class="sxs-lookup"><span data-stu-id="eefb1-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span></span>

<span data-ttu-id="eefb1-243">Aby uzyskać więcej informacji, zobacz [elementu PartitionSelector i elementu ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="eefb1-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll
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
            //Restart the node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way to restart node is by using nodeName and nodeInstanceId
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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="eefb1-244">Elementu PartitionSelector i elementu ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="eefb1-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="eefb1-245">Elementu PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="eefb1-245">PartitionSelector</span></span>
<span data-ttu-id="eefb1-246">Elementu PartitionSelector jest pomocnika ujawnione podczas testowania i jest używany do wybierania określonej partycji, na którym należy wykonać czynności kontroli.</span><span class="sxs-lookup"><span data-stu-id="eefb1-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span></span> <span data-ttu-id="eefb1-247">Można ją wybrać określonej partycji, jeśli identyfikator partycji jest znany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="eefb1-247">It can be used to select a specific partition if the partition ID is known beforehand.</span></span> <span data-ttu-id="eefb1-248">Lub, możesz podać klucz partycji i operacji wewnętrznie rozwiąże Identyfikatora partycji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span></span> <span data-ttu-id="eefb1-249">Masz również wybrać losowe partycji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-249">You also have the option of selecting a random partition.</span></span>

<span data-ttu-id="eefb1-250">Aby użyć tego pomocnika, Utwórz obiekt elementu PartitionSelector i wybierz partycję za pomocą jednej z metod Select *.</span><span class="sxs-lookup"><span data-stu-id="eefb1-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select* methods.</span></span> <span data-ttu-id="eefb1-251">Następnie przekaż obiekt elementu PartitionSelector do interfejsu API, która go wymaga.</span><span class="sxs-lookup"><span data-stu-id="eefb1-251">Then pass in the PartitionSelector object to the API that requires it.</span></span> <span data-ttu-id="eefb1-252">Jeśli wybrano opcję nie, domyślnie losowe partycji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-252">If no option is selected, it defaults to a random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="eefb1-253">Elementu ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="eefb1-253">ReplicaSelector</span></span>
<span data-ttu-id="eefb1-254">Elementu ReplicaSelector jest pomocnika ujawnione podczas testowania i służą do wybierz replikę, na którym należy wykonać czynności kontroli.</span><span class="sxs-lookup"><span data-stu-id="eefb1-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span></span> <span data-ttu-id="eefb1-255">Można ją wybrać określonych repliki, jeśli identyfikator repliki jest znany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="eefb1-255">It can be used to select a specific replica if the replica ID is known beforehand.</span></span> <span data-ttu-id="eefb1-256">Ponadto istnieje możliwość wybrania repliki podstawowej lub pomocniczej losowe.</span><span class="sxs-lookup"><span data-stu-id="eefb1-256">In addition, you have the option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="eefb1-257">Elementu ReplicaSelector pochodzi z elementu PartitionSelector, dlatego należy wybrać zarówno repliki i partycji, na którym chcesz wykonać operacji kontroli.</span><span class="sxs-lookup"><span data-stu-id="eefb1-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span></span>

<span data-ttu-id="eefb1-258">Aby użyć tego pomocnika, Utwórz obiekt elementu ReplicaSelector i skonfigurowane w sposób, aby wybrać repliki i partycji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span></span> <span data-ttu-id="eefb1-259">Można następnie przekazać do interfejsu API, która go wymaga.</span><span class="sxs-lookup"><span data-stu-id="eefb1-259">You can then pass it into the API that requires it.</span></span> <span data-ttu-id="eefb1-260">Jeśli wybrano opcję nie, domyślnie losowe repliki i losowe partycji.</span><span class="sxs-lookup"><span data-stu-id="eefb1-260">If no option is selected, it defaults to a random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select the primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select the replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="eefb1-261">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eefb1-261">Next steps</span></span>
* [<span data-ttu-id="eefb1-262">Scenariusze testowania</span><span class="sxs-lookup"><span data-stu-id="eefb1-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="eefb1-263">Jak przetestować usługi</span><span class="sxs-lookup"><span data-stu-id="eefb1-263">How to test your service</span></span>
  * [<span data-ttu-id="eefb1-264">Symulacji awarii podczas obciążeń usługi</span><span class="sxs-lookup"><span data-stu-id="eefb1-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="eefb1-265">Błędy usługi do komunikacji</span><span class="sxs-lookup"><span data-stu-id="eefb1-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

