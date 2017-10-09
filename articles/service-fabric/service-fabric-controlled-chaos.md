---
title: "klastry Chaos w sieci szkieletowej usług aaaInduce | Dokumentacja firmy Microsoft"
description: "Przy użyciu iniekcji błędów i interfejsów API usługi analizy klastra toomanage Chaos hello klastra."
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
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="94cee-103">Wywołać kontrolowane Chaos w klastrach sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="94cee-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="94cee-104">Dużych systemów rozproszonych jak infrastruktury chmury jest z założenia gwarantowane.</span><span class="sxs-lookup"><span data-stu-id="94cee-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="94cee-105">Sieć szkieletowa usług Azure umożliwia toowrite deweloperzy niezawodnej usługi rozproszone zawodnych infrastrukturze.</span><span class="sxs-lookup"><span data-stu-id="94cee-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="94cee-106">toowrite niezawodne usługi rozproszone zawodnych infrastrukturze, deweloperzy muszą toobe tootest stanie hello stabilności ich usług podczas hello podstawowej infrastruktury zawodnych przechodzi przez przejść stanu skomplikowane toofaults ukończenia.</span><span class="sxs-lookup"><span data-stu-id="94cee-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="94cee-107">Witaj [iniekcji błędów i usługi klastrowania analizy](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (znanej także jako hello błędów Analysis Service) umożliwia deweloperom hello tooinduce błędów tootest swoich usług.</span><span class="sxs-lookup"><span data-stu-id="94cee-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="94cee-108">Tak samo, jak te docelowe symulowane błędów, [ponowne uruchomienie partycji](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), ułatwiają wykonywanie hello najczęściej przejścia stanu.</span><span class="sxs-lookup"><span data-stu-id="94cee-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="94cee-109">Jednak docelowe symulowane błędów są ukierunkowane zgodnie z definicją i w związku z tym może nie usterek przedstawiające się tylko w twardych prognozowania, długich i skomplikowane sekwencji przejścia stanu.</span><span class="sxs-lookup"><span data-stu-id="94cee-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="94cee-110">Nieobciążonej testowania, możesz użyć Chaos.</span><span class="sxs-lookup"><span data-stu-id="94cee-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="94cee-111">Chaos symuluje błędów okresowych, przeplotem (bezpieczne i nieprawidłowego) w całym klastrze hello przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="94cee-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="94cee-112">Po skonfigurowaniu Chaos hello szybkość i hello rodzaju błędów, można uruchomić Chaos za pomocą języka C# lub interfejs API środowiska Powershell toostart generowanie błędów w klastrze hello i w usługach.</span><span class="sxs-lookup"><span data-stu-id="94cee-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="94cee-113">Można skonfigurować Chaos toorun w określonym przedziale czasu (na przykład na godzinę), po którym Chaos automatycznie zatrzymywana, lub toostop API StopChaos (C# lub programu Powershell) można wywołać go w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="94cee-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="94cee-114">W postaci bieżącego Chaos wywołuje tylko bezpiecznych błędy, co oznacza, że w przypadku braku błędów zewnętrznych hello utrata kworum, lub utraty danych nigdy nie występuje.</span><span class="sxs-lookup"><span data-stu-id="94cee-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="94cee-115">Po uruchomieniu Chaos tworzy różne zdarzenia, które przechwytywania stanu hello hello Uruchom w chwili hello.</span><span class="sxs-lookup"><span data-stu-id="94cee-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="94cee-116">Na przykład ExecutingFaultsEvent zawiera wszystkie błędy hello Chaos decyzję tooexecute w tym iteracji.</span><span class="sxs-lookup"><span data-stu-id="94cee-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="94cee-117">ValidationFailedEvent zawiera szczegóły hello awarii sprawdzania poprawności (problemów kondycji lub stabilności), który został znaleziony podczas sprawdzania poprawności hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="94cee-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="94cee-118">Można wywołać hello API GetChaosReport (C# lub programu Powershell) tooget hello raportu Chaos przebiegów.</span><span class="sxs-lookup"><span data-stu-id="94cee-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="94cee-119">Te zdarzenia uzyskać utrwalone w [niezawodnej słownika](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), której obowiązują zasady obcięcie ustawieniem dwie konfiguracje: **MaxStoredChaosEventCount** (wartość domyślna to 25000) i **StoredActionCleanupIntervalInSeconds** (wartość domyślna to 3600).</span><span class="sxs-lookup"><span data-stu-id="94cee-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="94cee-120">Każdy *StoredActionCleanupIntervalInSeconds* Chaos kontroli i wszystkie ale hello najnowszych *MaxStoredChaosEventCount* zdarzenia, zostaną usunięte ze słownika niezawodnej hello.</span><span class="sxs-lookup"><span data-stu-id="94cee-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="94cee-121">Błędy powstaniu w Chaos</span><span class="sxs-lookup"><span data-stu-id="94cee-121">Faults induced in Chaos</span></span>
<span data-ttu-id="94cee-122">Chaos generuje błędy między hello całego klastra sieci szkieletowej usług i kompresuje błędów, które są widoczne w miesięcy lub lat do kilku godzin.</span><span class="sxs-lookup"><span data-stu-id="94cee-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="94cee-123">Kombinacja Hello przeplotem błędów ze stawką wysoką odporność hello znajduje sytuacjach wyjątkowych, które w przeciwnym razie mogą zostać pominięci.</span><span class="sxs-lookup"><span data-stu-id="94cee-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="94cee-124">Tego ćwiczenia Chaos prowadzi tooa znaczne ulepszenia w jakości kodu hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="94cee-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="94cee-125">Chaos wywołuje usterek z hello następujące kategorie:</span><span class="sxs-lookup"><span data-stu-id="94cee-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="94cee-126">Uruchom ponownie węzeł</span><span class="sxs-lookup"><span data-stu-id="94cee-126">Restart a node</span></span>
* <span data-ttu-id="94cee-127">Ponowne uruchomienie wdrożonego pakietu kodu</span><span class="sxs-lookup"><span data-stu-id="94cee-127">Restart a deployed code package</span></span>
* <span data-ttu-id="94cee-128">Usuwanie repliki</span><span class="sxs-lookup"><span data-stu-id="94cee-128">Remove a replica</span></span>
* <span data-ttu-id="94cee-129">Uruchom ponownie repliki</span><span class="sxs-lookup"><span data-stu-id="94cee-129">Restart a replica</span></span>
* <span data-ttu-id="94cee-130">Przenieś repliki podstawowej (można konfigurować)</span><span class="sxs-lookup"><span data-stu-id="94cee-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="94cee-131">Przenieś repliki pomocniczej (można konfigurować)</span><span class="sxs-lookup"><span data-stu-id="94cee-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="94cee-132">Chaos działa w przejść przez wiele iteracji.</span><span class="sxs-lookup"><span data-stu-id="94cee-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="94cee-133">Każdej iteracji składa się z usterek i sprawdzania poprawności klastra hello określonym okresie.</span><span class="sxs-lookup"><span data-stu-id="94cee-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="94cee-134">Możesz skonfigurować czas hello hello toostabilize klastra i toosucceed sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="94cee-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="94cee-135">Jeśli błąd zostanie znaleziony w weryfikacji klastra, Chaos generuje i będzie się powtarzał ValidationFailedEvent sygnatury czasowej UTC hello oraz szczegóły dotyczące błędu hello.</span><span class="sxs-lookup"><span data-stu-id="94cee-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="94cee-136">Rozważmy na przykład wystąpienie Chaos ustawionej toorun godzinę z maksymalnie trzech równoczesnych błędów.</span><span class="sxs-lookup"><span data-stu-id="94cee-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="94cee-137">Chaos wywołuje trzy błędów, a następnie weryfikuje hello kondycji klastra.</span><span class="sxs-lookup"><span data-stu-id="94cee-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="94cee-138">Go iterację hello poprzedniego kroku, dopóki nie zostanie jawnie zatrzymana za pośrednictwem interfejsu API StopChaosAsync hello lub jednogodzinnym przekazuje.</span><span class="sxs-lookup"><span data-stu-id="94cee-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="94cee-139">Jeśli klaster hello staje się zła w dowolnym iteracji (to znaczy go nie stabilizacji w hello przekazany w MaxClusterStabilizationTimeout) Chaos generuje ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="94cee-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="94cee-140">To zdarzenie wskazuje, że coś niepowodzenia i może być konieczne dalsze badania.</span><span class="sxs-lookup"><span data-stu-id="94cee-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="94cee-141">tooget, który błędów Chaos powstaniu, możesz użyć GetChaosReport API (programu powershell lub C#).</span><span class="sxs-lookup"><span data-stu-id="94cee-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="94cee-142">Witaj interfejsu API pobiera hello następny segment hello Chaos raportu na podstawie tokenu przekazanego kontynuacji hello lub hello przekazany w czasie range.</span><span class="sxs-lookup"><span data-stu-id="94cee-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="94cee-143">Można określić hello ContinuationToken tooget hello następny segment hello Chaos raportu lub można określić zakres czasu hello za pośrednictwem StartTimeUtc i EndTimeUtc, ale nie można określić zarówno hello ContinuationToken, jak i zakres czasu hello w hello samo wywołanie.</span><span class="sxs-lookup"><span data-stu-id="94cee-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="94cee-144">W przypadku więcej niż 100 zdarzeń Chaos hello Chaos raportu jest zwracana w segmentach gdy segment zawiera nie więcej niż 100 zdarzeń Chaos.</span><span class="sxs-lookup"><span data-stu-id="94cee-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="94cee-145">Opcje konfiguracji ważne</span><span class="sxs-lookup"><span data-stu-id="94cee-145">Important configuration options</span></span>
* <span data-ttu-id="94cee-146">**TimeToRun**: suma czasu uruchomionym programem Chaos przed zakończeniem pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="94cee-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="94cee-147">Można zatrzymać Chaos ma uruchomić hello TimeToRun okres za pośrednictwem hello StopChaos interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="94cee-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="94cee-148">**MaxClusterStabilizationTimeout**: hello maksymalną ilość czasu toowait dla toobecome klastra hello dobrej kondycji przed utworzeniem ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="94cee-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="94cee-149">Ten oczekiwania jest tooreduce hello obciążenie klastra hello podczas, gdy trwa jej odzyskiwanie.</span><span class="sxs-lookup"><span data-stu-id="94cee-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="94cee-150">testy Hello wykonać to polecenie:</span><span class="sxs-lookup"><span data-stu-id="94cee-150">hello checks performed are:</span></span>
  * <span data-ttu-id="94cee-151">Jeśli kondycja klastra hello jest OK</span><span class="sxs-lookup"><span data-stu-id="94cee-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="94cee-152">Jeśli kondycja usługi hello jest OK</span><span class="sxs-lookup"><span data-stu-id="94cee-152">If hello service health is OK</span></span>
  * <span data-ttu-id="94cee-153">Jeśli rozmiar zestawu replik docelowy hello uzyskuje się hello partycji usługi</span><span class="sxs-lookup"><span data-stu-id="94cee-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="94cee-154">Czy istnieją nie replik w stanie InBuild</span><span class="sxs-lookup"><span data-stu-id="94cee-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="94cee-155">**MaxConcurrentFaults**: hello maksymalną liczbę równoczesnych usterek, które są wywołane w każdej iteracji.</span><span class="sxs-lookup"><span data-stu-id="94cee-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="94cee-156">większa liczba hello Hello, hello skuteczniejsze jest Chaos i hello operacji Failover i hello stan przejścia kombinacje, które hello klastra przesyłany przez także są bardziej złożone.</span><span class="sxs-lookup"><span data-stu-id="94cee-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="94cee-157">Niezależnie od tego jak wysoka wartość *MaxConcurrentFaults* ma Chaos gwarantuje — w przypadku braku hello zewnętrznych usterek — nie utraty kworum lub utraty danych.</span><span class="sxs-lookup"><span data-stu-id="94cee-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="94cee-158">**EnableMoveReplicaFaults**: Włącza lub wyłącza hello błędów, które powodują hello toomove repliki podstawowej lub dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="94cee-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="94cee-159">Te błędy są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="94cee-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="94cee-160">**WaitTimeBetweenIterations**: hello ilość toowait czas między poszczególnymi iteracjami.</span><span class="sxs-lookup"><span data-stu-id="94cee-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="94cee-161">Oznacza to, że hello czas Chaos zatrzyma się po wykonaniu round usterek i o zakończeniu hello odpowiedniego sprawdzania poprawności kondycji hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="94cee-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="94cee-162">Witaj wyższa wartość hello, niższe hello jest wskaźnikiem iniekcji średnią usterek hello.</span><span class="sxs-lookup"><span data-stu-id="94cee-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="94cee-163">**WaitTimeBetweenFaults**: hello ilość czasu toowait między dwa kolejne błędy w jednym iteracji.</span><span class="sxs-lookup"><span data-stu-id="94cee-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="94cee-164">Witaj wyższa wartość hello, hello niższe hello współbieżności (lub hello nakładania się) błędów.</span><span class="sxs-lookup"><span data-stu-id="94cee-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="94cee-165">**ClusterHealthPolicy**: zasady dotyczące kondycji klastra jest używane toovalidate hello kondycji klastra hello Between Chaos iteracji.</span><span class="sxs-lookup"><span data-stu-id="94cee-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="94cee-166">Jeśli stan klastra hello jest wynikiem błędu lub sytuacji wystąpił nieoczekiwany wyjątek podczas wykonywania błąd Chaos będzie czekać przez 30 minut przed hello dalej — sprawdzenie kondycji - tooprovide hello klaster z niektórych toorecuperate czasu.</span><span class="sxs-lookup"><span data-stu-id="94cee-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="94cee-167">**Kontekst**: pary klucz wartość typu kolekcji (ciąg).</span><span class="sxs-lookup"><span data-stu-id="94cee-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="94cee-168">Mapa Hello mogą być używane toorecord informacje o hello Chaos Uruchom.</span><span class="sxs-lookup"><span data-stu-id="94cee-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="94cee-169">Nie może być więcej niż 100 takie pary, a każdy ciąg (klucz lub wartość) może mieć maksymalnie 4095 znaków.</span><span class="sxs-lookup"><span data-stu-id="94cee-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="94cee-170">Ta mapa jest ustawiana przez starter hello hello Chaos Uruchom toooptionally magazynu hello kontekstu o określonych hello Uruchom.</span><span class="sxs-lookup"><span data-stu-id="94cee-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="94cee-171">Jak toorun Chaos</span><span class="sxs-lookup"><span data-stu-id="94cee-171">How toorun Chaos</span></span>

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
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
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
                // If a StoppedEvent is found, exit hello loop.
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
