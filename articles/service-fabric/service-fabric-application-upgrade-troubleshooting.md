---
title: Uaktualnianie aplikacji aaaTroubleshooting | Dokumentacja firmy Microsoft
description: "W tym artykule opisano kilka typowych problemów wokół uaktualniania aplikacji usługi Service Fabric i w jaki sposób tooresolve je."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="296ca-103">Rozwiązywanie problemów z uaktualnieniami aplikacji</span><span class="sxs-lookup"><span data-stu-id="296ca-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="296ca-104">W tym artykule omówiono niektóre typowe problemy hello wokół uaktualniania aplikacji sieci szkieletowej usług Azure i w jaki sposób tooresolve je.</span><span class="sxs-lookup"><span data-stu-id="296ca-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="296ca-105">Rozwiązywanie problemów z uaktualniania aplikacji nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="296ca-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="296ca-106">Jeśli uaktualnienie nie powiedzie się, dane wyjściowe hello hello **Get-ServiceFabricApplicationUpgrade** polecenia zawiera dodatkowe informacje dotyczące debugowania błędu hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="296ca-107">Witaj poniżej określa używania hello dodatkowe informacje:</span><span class="sxs-lookup"><span data-stu-id="296ca-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="296ca-108">Określ typ awarii hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="296ca-109">Zidentyfikuj hello Przyczyna niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="296ca-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="296ca-110">Określ co najmniej jednego składnika Niepowodzenie w celu dokładniejszego zbadania.</span><span class="sxs-lookup"><span data-stu-id="296ca-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="296ca-111">Te informacje są dostępne, gdy sieci szkieletowej usług wykryje błąd hello niezależnie od tego, czy hello **FailureAction** jest tooroll wstecz lub wstrzymać hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="296ca-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="296ca-112">Określ typ awarii hello</span><span class="sxs-lookup"><span data-stu-id="296ca-112">Identify hello failure type</span></span>
<span data-ttu-id="296ca-113">W danych wyjściowych hello **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identyfikuje hello sygnatury (UTC) jaką błąd uaktualnienia został wykryty przez sieć szkieletowa usług i  **FailureAction** zostało wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="296ca-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="296ca-114">**Przyczyna błędu** identyfikuje jeden z trzech potencjalnych przyczyn wysokiego poziomu przez hello:</span><span class="sxs-lookup"><span data-stu-id="296ca-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="296ca-115">UpgradeDomainTimeout — wskazuje, że konkretnej domeny uaktualnienia trwało zbyt długo toocomplete i **UpgradeDomainTimeout** wygasł.</span><span class="sxs-lookup"><span data-stu-id="296ca-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="296ca-116">OverallUpgradeTimeout - wskazuje tego hello ogólne uaktualnienia trwało zbyt długo toocomplete i **UpgradeTimeout** wygasł.</span><span class="sxs-lookup"><span data-stu-id="296ca-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="296ca-117">Test kondycji — wskazuje, że po uaktualnieniu domeny aktualizacji aplikacji hello pozostała zła zgodnie z toohello określone zasady dotyczące kondycji i **HealthCheckRetryTimeout** wygasł.</span><span class="sxs-lookup"><span data-stu-id="296ca-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="296ca-118">Te wpisy tylko widoczne w danych wyjściowych hello podczas hello uaktualnienie nie powiedzie się i uruchamia wycofywanie.</span><span class="sxs-lookup"><span data-stu-id="296ca-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="296ca-119">Dalsze informacje są wyświetlane w zależności od typu hello hello błędu.</span><span class="sxs-lookup"><span data-stu-id="296ca-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="296ca-120">Zbadaj uaktualnienia limitów czasu</span><span class="sxs-lookup"><span data-stu-id="296ca-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="296ca-121">Uaktualnij limit błędów są najczęściej spowodowane problemów dotyczących dostępności usługi.</span><span class="sxs-lookup"><span data-stu-id="296ca-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="296ca-122">dane wyjściowe Hello dalej w tym temacie jest typowe dla uaktualnienia gdzie repliki usługi lub wystąpienia awarii toostart w nowej wersji kodu hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="296ca-123">Witaj **UpgradeDomainProgressAtFailure** pola przechwytuje migawkę oczekującego uaktualnienia pracę w czasie hello awarii.</span><span class="sxs-lookup"><span data-stu-id="296ca-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

<span data-ttu-id="296ca-124">W tym przykładzie hello uaktualnienie nie powiodło się w domenie uaktualnienia *MYUD1* i dwóch partycji (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* i *4b43f4d8-b26b-424e-9307-7a7a62e79750*) zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="296ca-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="296ca-125">partycje Hello zostały zatrzymane powodu środowiska uruchomieniowego hello replik podstawowych tooplace (*WaitForPrimaryPlacement*) na węzłach docelowych *Node1* i *Węzeł4*.</span><span class="sxs-lookup"><span data-stu-id="296ca-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="296ca-126">Witaj **Get-ServiceFabricNode** polecenie może być używane tooverify, że te dwa węzły znajdują się w domenie uaktualnienia *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="296ca-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="296ca-127">Witaj *UpgradePhase* mówi *PostUpgradeSafetyCheck*, co oznacza, że występuje kontrole bezpieczeństwa po we wszystkich węzłach w domenie uaktualnienia hello zakończeniu uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="296ca-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="296ca-128">Te informacje punktów tooa potencjalny problem z nową wersję kodu aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="296ca-129">najbardziej typowe problemy Hello są błędy usługi hello open lub ścieżki kodu tooprimary podwyższania poziomu.</span><span class="sxs-lookup"><span data-stu-id="296ca-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="296ca-130">*UpgradePhase* z *PreUpgradeSafetyCheck* oznacza, że wystąpiły problemy przygotowanie domeny uaktualnienia hello, przed jego została wykonana.</span><span class="sxs-lookup"><span data-stu-id="296ca-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="296ca-131">w takim przypadku Hello najczęściej występujących problemów są błędy usługi Zamknij hello lub obniżania poziomu od ścieżki głównej kodu.</span><span class="sxs-lookup"><span data-stu-id="296ca-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="296ca-132">Bieżący Hello **UpgradeState** jest *RollingBackCompleted*, więc hello oryginalnego uaktualniania należy wykonać o wycofaniu **FailureAction**, która automatycznie wycofane hello uaktualnienia w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="296ca-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="296ca-133">W przypadku uaktualniania oryginalnego hello ręcznego **FailureAction**, a następnie Uaktualnianie hello zamiast tego będzie w stanie wstrzymanym tooallow na żywo, debugowania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="296ca-134">Zbadaj błędy sprawdzania kondycji</span><span class="sxs-lookup"><span data-stu-id="296ca-134">Investigate health check failures</span></span>
<span data-ttu-id="296ca-135">Błędy sprawdzania kondycji mogą być wyzwalane przez różne problemy, które mogą wystąpić po zakończeniu wszystkich węzłów w domenie uaktualnienia, uaktualniania i przekazywania wszystkich kontroli bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="296ca-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="296ca-136">dane wyjściowe Hello dalej w tym temacie jest typowe dla niepowodzenia uaktualnienia powodu toofailed kontroli kondycji.</span><span class="sxs-lookup"><span data-stu-id="296ca-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="296ca-137">Witaj **UnhealthyEvaluations** pola przechwytuje migawki kontroli kondycji, których nie powiodła się w czasie hello uaktualnienia hello zgodnie z toohello określony [zasad dotyczących kondycji](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="296ca-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

<span data-ttu-id="296ca-138">Najpierw niepowodzeń sprawdzenia kondycji do badania wymaga zrozumienia model kondycji sieci szkieletowej usług hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="296ca-139">Ale nawet bez takich dobrej znajomości, możemy stwierdzić, czy dwie usługi są w złej kondycji: *sieci szkieletowej: / DemoApp/Svc3* i *fabric: / DemoApp/Svc2*, wraz z raportów o kondycji błąd hello ("InjectedFault "w tym przypadku).</span><span class="sxs-lookup"><span data-stu-id="296ca-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="296ca-140">W tym przykładzie dwóch spośród czterech usługi jest w złej kondycji, która jest poniżej wartości docelowej domyślne hello 0% złej kondycji (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="296ca-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="296ca-141">Witaj uaktualnienie zostało zawieszone po niepowodzeniu określając **FailureAction** w przypadku ręcznego uruchamiania hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="296ca-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="296ca-142">Ten tryb umożliwia tooinvestigate hello systemu na żywo w stanie hello nie powiodło się przed podjęciem dalszych działań.</span><span class="sxs-lookup"><span data-stu-id="296ca-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="296ca-143">Odzyskiwanie z wstrzymane uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="296ca-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="296ca-144">O wycofaniu **FailureAction**, jest odzyskanie nie jest wymagane, ponieważ uaktualnienie hello automatycznie przywraca po niepowodzeniu.</span><span class="sxs-lookup"><span data-stu-id="296ca-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="296ca-145">Ręcznego **FailureAction**, dostępnych jest kilka opcji odzyskiwania:</span><span class="sxs-lookup"><span data-stu-id="296ca-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="296ca-146">wyzwalacz wycofywania</span><span class="sxs-lookup"><span data-stu-id="296ca-146">trigger a rollback</span></span>
2. <span data-ttu-id="296ca-147">Postępuj zgodnie z instrukcjami hello pozostałej części uaktualnienia hello ręcznie</span><span class="sxs-lookup"><span data-stu-id="296ca-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="296ca-148">Wznów hello monitorowane uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="296ca-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="296ca-149">Witaj **Start ServiceFabricApplicationRollback** polecenie może być używany w żadnych toostart czasu wycofywanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="296ca-150">Po polecenie hello zwraca pomyślnie, żądanie wycofania hello został zarejestrowany w systemie hello i rozpoczyna się w krótkim czasie.</span><span class="sxs-lookup"><span data-stu-id="296ca-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="296ca-151">Witaj **polecenie Resume-ServiceFabricApplicationUpgrade** , można użyć polecenia tooproceed za pośrednictwem hello pozostałej części hello ręcznie uaktualnić domeny uaktualnienia pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="296ca-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="296ca-152">W tym trybie bezpieczeństwa tylko testy są wykonywane przez hello system.</span><span class="sxs-lookup"><span data-stu-id="296ca-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="296ca-153">Brak kondycji są sprawdzane.</span><span class="sxs-lookup"><span data-stu-id="296ca-153">No more health checks are performed.</span></span> <span data-ttu-id="296ca-154">To polecenie można użyć tylko, gdy hello *UpgradeState* pokazuje *RollingForwardPending*, co oznacza, że bieżąca domena uaktualnienia hello zakończył uaktualnianie, ale hello obok jedną nie została uruchomiona (oczekiwanie).</span><span class="sxs-lookup"><span data-stu-id="296ca-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="296ca-155">Witaj **ServiceFabricApplicationUpgrade aktualizacji** polecenia mogą być używane tooresume hello monitorowane uaktualnienia z kontroli zdrowia i bezpieczeństwa są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="296ca-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

<span data-ttu-id="296ca-156">uaktualnienie Hello kontynuuje działanie od hello domeny uaktualnień, których ostatnio został wstrzymany i hello Użyj takie same parametry i zasady dotyczące kondycji jako przed uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="296ca-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="296ca-157">W razie potrzeby, parametry uaktualniania hello i zasady dotyczące kondycji pokazano hello poprzedzający dane wyjściowe można zmienić w hello same polecenia po wznowieniu pracy uaktualniania hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="296ca-158">W tym przykładzie hello uaktualnienie zostało wznowione w trybie monitorowanej hello parametrów i zasady dotyczące kondycji hello bez zmian.</span><span class="sxs-lookup"><span data-stu-id="296ca-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="296ca-159">Dodatkowe informacje o rozwiązywaniu</span><span class="sxs-lookup"><span data-stu-id="296ca-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="296ca-160">Sieć szkieletowa usług nie jest po hello określone zasady dotyczące kondycji</span><span class="sxs-lookup"><span data-stu-id="296ca-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="296ca-161">Możliwa przyczyna 1:</span><span class="sxs-lookup"><span data-stu-id="296ca-161">Possible Cause 1:</span></span>

<span data-ttu-id="296ca-162">Sieć szkieletowa usług tłumaczy wszystkie wartości procentowe na rzeczywistą liczbę jednostek (na przykład replik, partycji i usług) do oceny kondycji i zawsze zaokrągla liczbę w górę toowhole jednostek.</span><span class="sxs-lookup"><span data-stu-id="296ca-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="296ca-163">Na przykład, jeśli hello maksymalna *MaxPercentUnhealthyReplicasPerPartition* % 21 i istnieją pięciu replik, a następnie umożliwia sieci szkieletowej usług zapasową replik zła tootwo (czyli`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="296ca-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="296ca-164">W związku z tym zasady dotyczące kondycji powinien być odpowiednio ustawiony.</span><span class="sxs-lookup"><span data-stu-id="296ca-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="296ca-165">Możliwe przyczyny 2:</span><span class="sxs-lookup"><span data-stu-id="296ca-165">Possible Cause 2:</span></span>

<span data-ttu-id="296ca-166">Zasady dotyczące kondycji są określane w przeliczeniu na wartości procentowe całkowita usługi i wystąpień nie określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="296ca-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="296ca-167">Na przykład przed uaktualnieniem, jeśli aplikacja ma cztery usługi wystąpień A "," B "," C "i" D, w przypadku, gdy usługa D jest zła, ale mały wpływ toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="296ca-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="296ca-168">Chcemy hello tooignore znane usługi w złej kondycji D podczas hello uaktualnienia i ustawić parametr *MaxPercentUnhealthyServices* toobe 25%, przy założeniu, A, B i C muszą toobe dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="296ca-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="296ca-169">Jednak podczas uaktualniania hello D mogą stać się dobra podczas C staje się nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="296ca-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="296ca-170">uaktualnienie Hello może nadal się powieść, ponieważ tylko 25% hello usługi jest w złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="296ca-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="296ca-171">Jednak może to spowodować nieprzewidziane błędy powodu tooC jest nieoczekiwanie zła zamiast D. W takiej sytuacji należy należy modelować D jako typ innej usługi, a, B i C. Ponieważ zasady dotyczące kondycji są określone dla typów usług, progi różnych Zła wartość procentowa może być zastosowane toodifferent usług.</span><span class="sxs-lookup"><span data-stu-id="296ca-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="296ca-172">Nie określono zasadę dla aplikacji, ale uaktualnienia hello nadal nie powiedzie się niektóre błędy przekroczenia limitu czasu, które nigdy nie została określona</span><span class="sxs-lookup"><span data-stu-id="296ca-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="296ca-173">Zasady dotyczące kondycji nie są udostępniane toohello żądanie uaktualnienia, będą pobierane z hello *ApplicationManifest.xml* hello bieżącej wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="296ca-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="296ca-174">Na przykład jeśli w przypadku uaktualniania z wersji 1.0 tooversion 2.0 X aplikacji, są używane zasady dotyczące kondycji aplikacji określone dla w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="296ca-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="296ca-175">Jeśli zasadę różnych powinny być używane do uaktualnienia hello hello zasad musi toobe określony jako część aplikacji hello uaktualnienia wywołanie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="296ca-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="296ca-176">Witaj zasady określony jako część wywołania interfejsu API hello miały zastosowanie tylko podczas uaktualniania hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="296ca-177">Po ukończeniu uaktualniania hello hello zasad określonych w hello *ApplicationManifest.xml* są używane.</span><span class="sxs-lookup"><span data-stu-id="296ca-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="296ca-178">Podano niepoprawny limity czasu</span><span class="sxs-lookup"><span data-stu-id="296ca-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="296ca-179">Może mieć zastanawiasz się o co się dzieje, gdy niespójnie przekroczeń limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="296ca-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="296ca-180">Na przykład może być *UpgradeTimeout* jest mniejsza niż hello *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="296ca-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="296ca-181">Witaj odpowiedzi jest zwracany jest błąd.</span><span class="sxs-lookup"><span data-stu-id="296ca-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="296ca-182">Błędy są zwracane, jeśli hello *UpgradeDomainTimeout* jest mniejsza niż suma hello *HealthCheckWaitDuration* i *HealthCheckRetryTimeout*, lub jeśli  *UpgradeDomainTimeout* jest mniejsza niż suma hello *HealthCheckWaitDuration* i *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="296ca-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="296ca-183">Moje uaktualnień trwa zbyt długo</span><span class="sxs-lookup"><span data-stu-id="296ca-183">My upgrades are taking too long</span></span>
<span data-ttu-id="296ca-184">Hello czas uaktualniania toocomplete zależy od hello kontroli kondycji i określić limity czasu.</span><span class="sxs-lookup"><span data-stu-id="296ca-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="296ca-185">Sprawdzanie kondycji i limity czasu są zależne od czasu wykonywania toocopy, wdrażanie i ustabilizowania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="296ca-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="296ca-186">Trwa zbyt agresywnie z limitów czasu może to oznaczać więcej uaktualnienia nie powiodło się, dlatego zalecamy konserwatywnie począwszy od dłuższego limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="296ca-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="296ca-187">Oto szybkie odświeżacz na interakcję hello przekroczeń limitu czasu z hello uaktualnienia razy:</span><span class="sxs-lookup"><span data-stu-id="296ca-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="296ca-188">Uaktualnia dla domeny uaktualnienia nie można ukończyć szybciej niż *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="296ca-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="296ca-189">Niepowodzenie uaktualniania nie może być szybsza niż *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="296ca-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="296ca-190">Witaj czas uaktualniania dla domeny uaktualnienia jest ograniczona przez *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="296ca-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="296ca-191">Jeśli *HealthCheckRetryTimeout* i *HealthCheckStableDuration* są zarówno niezerowy i hello kondycji aplikacji hello śledzi przełączania i z powrotem, następnie uaktualnienie hello ostatecznie upłynie limit czasu na  *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="296ca-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="296ca-192">*UpgradeDomainTimeout* rozpoczyna zliczanie raz hello uaktualnienia dla rozpoczyna hello bieżąca domena uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="296ca-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="296ca-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="296ca-193">Next steps</span></span>
<span data-ttu-id="296ca-194">[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="296ca-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="296ca-195">[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="296ca-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="296ca-196">Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="296ca-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="296ca-197">Uzyskania uaktualnień aplikacji zgodnych przez uczenia jak toouse [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="296ca-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="296ca-198">Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="296ca-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
