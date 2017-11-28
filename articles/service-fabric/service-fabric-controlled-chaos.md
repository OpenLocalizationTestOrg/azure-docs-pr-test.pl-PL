---
title: "Wywołać Chaos w klastrach usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
description: "Zarządzanie za pomocą iniekcji błędów i interfejsów API usługi analizy klastra Chaos w klastrze."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 3b3b93bc9ec5ecdcfc289e5b62e84de6aa4172ed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="8e358-103">Wywołać kontrolowane Chaos w klastrach sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="8e358-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="8e358-104">Dużych systemów rozproszonych jak infrastruktury chmury jest z założenia gwarantowane.</span><span class="sxs-lookup"><span data-stu-id="8e358-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="8e358-105">Sieć szkieletowa usług Azure umożliwia deweloperom zapisu niezawodnej usługi rozproszone zawodnych infrastrukturze.</span><span class="sxs-lookup"><span data-stu-id="8e358-105">Azure Service Fabric enables developers to write reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="8e358-106">Można zapisać niezawodne usługi rozproszone zawodnych infrastrukturze, deweloperzy muszą być możliwe przetestowanie stabilność swoich usług, podczas gdy podstawowej infrastruktury zawodnych przechodzi przez przejść skomplikowane stanu z powodu błędów.</span><span class="sxs-lookup"><span data-stu-id="8e358-106">To write robust distributed services on top of an unreliable infrastructure, developers need to be able to test the stability of their services while the underlying unreliable infrastructure is going through complicated state transitions due to faults.</span></span>

<span data-ttu-id="8e358-107">[Iniekcji błędów i usługi klastrowania analizy](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (znaną również jako usługa analiza błędów) umożliwia deweloperom powodować błędy, aby przetestować swoich usług.</span><span class="sxs-lookup"><span data-stu-id="8e358-107">The [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as the Fault Analysis Service) gives developers the ability to induce faults to test their services.</span></span> <span data-ttu-id="8e358-108">Tak samo, jak te docelowe symulowane błędów, [ponowne uruchomienie partycji](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), ułatwiają wykonywanie typowych przejścia stanu.</span><span class="sxs-lookup"><span data-stu-id="8e358-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise the most common state transitions.</span></span> <span data-ttu-id="8e358-109">Jednak docelowe symulowane błędów są ukierunkowane zgodnie z definicją i w związku z tym może nie usterek przedstawiające się tylko w twardych prognozowania, długich i skomplikowane sekwencji przejścia stanu.</span><span class="sxs-lookup"><span data-stu-id="8e358-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="8e358-110">Nieobciążonej testowania, możesz użyć Chaos.</span><span class="sxs-lookup"><span data-stu-id="8e358-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="8e358-111">Chaos symuluje błędów okresowych, przeplotem (bezpieczne i nieprawidłowego) w całym klastrze przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="8e358-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="8e358-112">Po skonfigurowaniu Chaos częstotliwość i rodzaju błędów, można uruchomić Chaos za pomocą języka C# lub interfejs API środowiska Powershell w celu rozpoczęcia generowania błędów w klastrze i w usługach.</span><span class="sxs-lookup"><span data-stu-id="8e358-112">Once you have configured Chaos with the rate and the kind of faults, you can start Chaos through C# or Powershell API to start generating faults in the cluster and in your services.</span></span> <span data-ttu-id="8e358-113">Chaos do uruchomienia w określonym przedziale czasu (na przykład na godzinę), po którym zatrzymuje Chaos można skonfigurować automatycznie lub można wywołać interfejsu API StopChaos, (C# lub programu Powershell) można zatrzymać w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="8e358-113">You can configure Chaos to run for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) to stop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="8e358-114">W postaci bieżącego Chaos wywołuje tylko bezpiecznych błędy, co oznacza, że w przypadku braku błędów zewnętrznych utrata kworum, lub utraty danych nigdy nie występuje.</span><span class="sxs-lookup"><span data-stu-id="8e358-114">In its current form, Chaos induces only safe faults, which implies that in the absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="8e358-115">Po uruchomieniu Chaos tworzy różnych zdarzeń, których przechwycony stan w momencie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="8e358-115">While Chaos is running, it produces different events that capture the state of the run at the moment.</span></span> <span data-ttu-id="8e358-116">Na przykład ExecutingFaultsEvent zawiera wszystkie błędy, które Chaos podjęto decyzję o wykonanie w tym iteracji.</span><span class="sxs-lookup"><span data-stu-id="8e358-116">For example, an ExecutingFaultsEvent contains all the faults that Chaos has decided to execute in that iteration.</span></span> <span data-ttu-id="8e358-117">ValidationFailedEvent zawiera szczegóły niepowodzenia weryfikacji (problemów kondycji lub stabilności) został znaleziony podczas sprawdzania poprawności klastra.</span><span class="sxs-lookup"><span data-stu-id="8e358-117">A ValidationFailedEvent contains the details of a validation failure (health or stability issues) that was found during the validation of the cluster.</span></span> <span data-ttu-id="8e358-118">Można wywołać GetChaosReport interfejsu API (C# lub programu Powershell) w celu uzyskania raportu Chaos działa.</span><span class="sxs-lookup"><span data-stu-id="8e358-118">You can invoke the GetChaosReport API (C# or Powershell) to get the report of Chaos runs.</span></span> <span data-ttu-id="8e358-119">Te zdarzenia uzyskać utrwalone w [niezawodnej słownika](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), której obowiązują zasady obcięcie ustawieniem dwie konfiguracje: **MaxStoredChaosEventCount** (wartość domyślna to 25000) i **StoredActionCleanupIntervalInSeconds** (wartość domyślna to 3600).</span><span class="sxs-lookup"><span data-stu-id="8e358-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="8e358-120">Co *StoredActionCleanupIntervalInSeconds* Chaos kontroli i wszystkie, ale najnowszej *MaxStoredChaosEventCount* zdarzenia, zostaną usunięte ze słownika wiarygodne.</span><span class="sxs-lookup"><span data-stu-id="8e358-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but the most recent *MaxStoredChaosEventCount* events, are purged from the reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="8e358-121">Błędy powstaniu w Chaos</span><span class="sxs-lookup"><span data-stu-id="8e358-121">Faults induced in Chaos</span></span>
<span data-ttu-id="8e358-122">Chaos generuje błędy w ramach całego klastra sieci szkieletowej usług i kompresuje błędów, które są widoczne w miesięcy lub lat do kilku godzin.</span><span class="sxs-lookup"><span data-stu-id="8e358-122">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="8e358-123">Kombinacja przeplotem błędów ze wskaźnikiem wysoką odporność znajduje sytuacjach wyjątkowych, które w przeciwnym razie mogą zostać pominięci.</span><span class="sxs-lookup"><span data-stu-id="8e358-123">The combination of interleaved faults with the high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="8e358-124">Tego ćwiczenia Chaos prowadzi do znacznej poprawy jakości kodu usługi.</span><span class="sxs-lookup"><span data-stu-id="8e358-124">This exercise of Chaos leads to a significant improvement in the code quality of the service.</span></span>

<span data-ttu-id="8e358-125">Chaos wywołuje usterek z następujących kategorii:</span><span class="sxs-lookup"><span data-stu-id="8e358-125">Chaos induces faults from the following categories:</span></span>

* <span data-ttu-id="8e358-126">Uruchom ponownie węzeł</span><span class="sxs-lookup"><span data-stu-id="8e358-126">Restart a node</span></span>
* <span data-ttu-id="8e358-127">Ponowne uruchomienie wdrożonego pakietu kodu</span><span class="sxs-lookup"><span data-stu-id="8e358-127">Restart a deployed code package</span></span>
* <span data-ttu-id="8e358-128">Usuwanie repliki</span><span class="sxs-lookup"><span data-stu-id="8e358-128">Remove a replica</span></span>
* <span data-ttu-id="8e358-129">Uruchom ponownie repliki</span><span class="sxs-lookup"><span data-stu-id="8e358-129">Restart a replica</span></span>
* <span data-ttu-id="8e358-130">Przenieś repliki podstawowej (można konfigurować)</span><span class="sxs-lookup"><span data-stu-id="8e358-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="8e358-131">Przenieś repliki pomocniczej (można konfigurować)</span><span class="sxs-lookup"><span data-stu-id="8e358-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="8e358-132">Chaos działa w przejść przez wiele iteracji.</span><span class="sxs-lookup"><span data-stu-id="8e358-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="8e358-133">Każdej iteracji składa się z usterek i weryfikacji klastra w określonym okresie.</span><span class="sxs-lookup"><span data-stu-id="8e358-133">Each iteration consists of faults and cluster validation for the specified period.</span></span> <span data-ttu-id="8e358-134">Można skonfigurować czas dla klastra do utrwalania i Weryfikacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="8e358-134">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span></span> <span data-ttu-id="8e358-135">Jeśli błąd zostanie znaleziony w weryfikacji klastra, Chaos generuje i będzie się powtarzał ValidationFailedEvent sygnatury czasowej UTC oraz szczegóły dotyczące błędu.</span><span class="sxs-lookup"><span data-stu-id="8e358-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span></span> <span data-ttu-id="8e358-136">Rozważmy na przykład wystąpienie Chaos, który jest ustawiony na uruchomienie przez godzinę z maksymalnie trzech równoczesnych błędów.</span><span class="sxs-lookup"><span data-stu-id="8e358-136">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="8e358-137">Chaos wywołuje trzy błędów, a następnie sprawdza stan klastra.</span><span class="sxs-lookup"><span data-stu-id="8e358-137">Chaos induces three faults, and then validates the cluster health.</span></span> <span data-ttu-id="8e358-138">Jego iterację poprzedniego kroku, dopóki nie zostanie jawnie zatrzymana za pośrednictwem interfejsu API StopChaosAsync lub jednogodzinnym przekazuje.</span><span class="sxs-lookup"><span data-stu-id="8e358-138">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="8e358-139">Jeśli klaster staje się zła w dowolnym iteracji (to znaczy go nie stabilizacji w MaxClusterStabilizationTimeout przekazany w) Chaos generuje ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="8e358-139">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize within the passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="8e358-140">To zdarzenie wskazuje, że coś niepowodzenia i może być konieczne dalsze badania.</span><span class="sxs-lookup"><span data-stu-id="8e358-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="8e358-141">Można pobrać błędów, które powstaniu Chaos, można użyć API GetChaosReport (programu powershell lub C#).</span><span class="sxs-lookup"><span data-stu-id="8e358-141">To get which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="8e358-142">Interfejs API pobiera następny segment Chaos raportu na podstawie token kontynuacji przekazany lub przekazany w czasie zakresie.</span><span class="sxs-lookup"><span data-stu-id="8e358-142">The API gets the next segment of the Chaos report based on the passed-in continuation token or the passed-in time-range.</span></span> <span data-ttu-id="8e358-143">Można określić ContinuationToken uzyskać następny segment raportu Chaos lub można określić zakres czasu za pośrednictwem StartTimeUtc i EndTimeUtc, ale nie można określić zarówno ContinuationToken, jak i zakres czasu, w tym samym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="8e358-143">You can either specify the ContinuationToken to get the next segment of the Chaos report or you can specify the time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both the ContinuationToken and the time-range in the same call.</span></span> <span data-ttu-id="8e358-144">W przypadku więcej niż 100 zdarzeń Chaos raportu Chaos jest zwracany w segmentów gdy segment zawiera nie więcej niż 100 Chaos zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8e358-144">When there are more than 100 Chaos events, the Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="8e358-145">Opcje konfiguracji ważne</span><span class="sxs-lookup"><span data-stu-id="8e358-145">Important configuration options</span></span>
* <span data-ttu-id="8e358-146">**TimeToRun**: suma czasu uruchomionym programem Chaos przed zakończeniem pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="8e358-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="8e358-147">Można zatrzymać Chaos ma uruchomić w okresie TimeToRun za pośrednictwem interfejsu API StopChaos.</span><span class="sxs-lookup"><span data-stu-id="8e358-147">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span></span>

* <span data-ttu-id="8e358-148">**MaxClusterStabilizationTimeout**: maksymalną ilość czasu oczekiwania na klaster, aby stała się dobra przed utworzeniem ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="8e358-148">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="8e358-149">Jest to oczekiwania Aby zmniejszyć obciążenie klastra, gdy jest on odzyskiwanie.</span><span class="sxs-lookup"><span data-stu-id="8e358-149">This wait is to reduce the load on the cluster while it is recovering.</span></span> <span data-ttu-id="8e358-150">Testy wykonywane przez to:</span><span class="sxs-lookup"><span data-stu-id="8e358-150">The checks performed are:</span></span>
  * <span data-ttu-id="8e358-151">Jeśli kondycja klastra jest OK</span><span class="sxs-lookup"><span data-stu-id="8e358-151">If the cluster health is OK</span></span>
  * <span data-ttu-id="8e358-152">Jeśli kondycja usługi jest OK</span><span class="sxs-lookup"><span data-stu-id="8e358-152">If the service health is OK</span></span>
  * <span data-ttu-id="8e358-153">Jeśli rozmiar zestawu replik docelowej uzyskuje się partycji usługi</span><span class="sxs-lookup"><span data-stu-id="8e358-153">If the target replica set size is achieved for the service partition</span></span>
  * <span data-ttu-id="8e358-154">Czy istnieją nie replik w stanie InBuild</span><span class="sxs-lookup"><span data-stu-id="8e358-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="8e358-155">**MaxConcurrentFaults**: Maksymalna liczba jednoczesnych usterek, które są wywołane w każdej iteracji.</span><span class="sxs-lookup"><span data-stu-id="8e358-155">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="8e358-156">Jest wyższy Chaos liczba, tym bardziej agresywną i tryb failover i kombinacji przejścia stanu, które przechodzą klastra są również bardziej złożone.</span><span class="sxs-lookup"><span data-stu-id="8e358-156">The higher the number, the more aggressive Chaos is and the failovers and the state transition combinations that the cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="8e358-157">Niezależnie od tego jak wysoka wartość *MaxConcurrentFaults* ma Chaos gwarantuje — w przypadku braku błędów zewnętrznych — nie utraty kworum lub utraty danych.</span><span class="sxs-lookup"><span data-stu-id="8e358-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in the absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="8e358-158">**EnableMoveReplicaFaults**: Włącza lub wyłącza błędów, które powodują repliki podstawowej lub pomocniczej, aby przenieść.</span><span class="sxs-lookup"><span data-stu-id="8e358-158">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span></span> <span data-ttu-id="8e358-159">Te błędy są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="8e358-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="8e358-160">**WaitTimeBetweenIterations**: ilość czasu między iteracji.</span><span class="sxs-lookup"><span data-stu-id="8e358-160">**WaitTimeBetweenIterations**: The amount of time to wait between iterations.</span></span> <span data-ttu-id="8e358-161">Oznacza to, że czas Chaos zatrzyma się po wykonaniu round usterek i o zakończeniu odpowiednich sprawdzania poprawności kondycji klastra.</span><span class="sxs-lookup"><span data-stu-id="8e358-161">That is, the amount of time Chaos will pause after having executed a round of faults and having finished the corresponding validation of the health of the cluster.</span></span> <span data-ttu-id="8e358-162">Im wyższa wartość dolnej jest wskaźnikiem iniekcji średnią usterek.</span><span class="sxs-lookup"><span data-stu-id="8e358-162">The higher the value, the lower is the average fault injection rate.</span></span>
* <span data-ttu-id="8e358-163">**WaitTimeBetweenFaults**: ilość czasu między dwa kolejne błędy w jednym iteracji.</span><span class="sxs-lookup"><span data-stu-id="8e358-163">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="8e358-164">Im większa wartość, tym mniejszy współbieżności (lub nakładanie się między) błędów.</span><span class="sxs-lookup"><span data-stu-id="8e358-164">The higher the value, the lower the concurrency of (or the overlap between) faults.</span></span>
* <span data-ttu-id="8e358-165">**ClusterHealthPolicy**: zasad dotyczących kondycji klastra jest używany do sprawdzania poprawności kondycji klastra Between Chaos iteracji.</span><span class="sxs-lookup"><span data-stu-id="8e358-165">**ClusterHealthPolicy**: Cluster health policy is used to validate the health of the cluster in between Chaos iterations.</span></span> <span data-ttu-id="8e358-166">Jeśli stan klastra jest wynikiem błędu lub sytuacji wystąpił nieoczekiwany wyjątek podczas wykonywania błąd Chaos będzie czekać przez 30 minut przed dalej — sprawdzenie kondycji - zapewnienie klastra recuperate trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="8e358-166">If the cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before the next health-check - to provide the cluster with some time to recuperate.</span></span>
* <span data-ttu-id="8e358-167">**Kontekst**: pary klucz wartość typu kolekcji (ciąg).</span><span class="sxs-lookup"><span data-stu-id="8e358-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="8e358-168">Mapy może służyć do rejestrowania informacji o przebiegu Chaos.</span><span class="sxs-lookup"><span data-stu-id="8e358-168">The map can be used to record information about the Chaos run.</span></span> <span data-ttu-id="8e358-169">Nie może być więcej niż 100 takie pary, a każdy ciąg (klucz lub wartość) może mieć maksymalnie 4095 znaków.</span><span class="sxs-lookup"><span data-stu-id="8e358-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="8e358-170">Ta mapa jest ustawiana przez starter milczenia Uruchom na przechowywanie w kontekście o określonym przebiegu.</span><span class="sxs-lookup"><span data-stu-id="8e358-170">This map is set by the starter of the Chaos run to optionally store the context about the specific run.</span></span>

## <a name="how-to-run-chaos"></a><span data-ttu-id="8e358-171">Jak uruchomić Chaos</span><span class="sxs-lookup"><span data-stu-id="8e358-171">How to run Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in the cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit the loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
