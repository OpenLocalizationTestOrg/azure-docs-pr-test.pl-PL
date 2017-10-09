---
title: "aaaTroubleshoot z raportów o kondycji systemu | Dokumentacja firmy Microsoft"
description: "Opis raportów o kondycji hello wysyłane przez składniki sieci szkieletowej usług Azure i ich użycia dla klastra rozwiązywaniu problemów lub problemów aplikacji."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="35766-103">Użyj tootroubleshoot Raporty kondycji systemu</span><span class="sxs-lookup"><span data-stu-id="35766-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="35766-104">Azure Service Fabric raportu składników fabrycznej hello na wszystkich jednostek w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="35766-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="35766-105">Witaj [magazynu kondycji](service-fabric-health-introduction.md#health-store) tworzy i usuwa jednostki na podstawie hello systemu raportów.</span><span class="sxs-lookup"><span data-stu-id="35766-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="35766-106">Również organizuje ona je w hierarchii, która przechwytuje interakcje jednostki.</span><span class="sxs-lookup"><span data-stu-id="35766-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="35766-107">Pojęcia dotyczące kondycji toounderstand Dowiedz się więcej o [model kondycji sieci szkieletowej usług](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="35766-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="35766-108">Raporty kondycji systemu zapewniają wgląd w klastrze i funkcjonalność aplikacji i flagi błędów za pomocą kondycji.</span><span class="sxs-lookup"><span data-stu-id="35766-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="35766-109">Dla aplikacji i usług systemowych raportów kondycji Sprawdź, czy jednostki są zaimplementowane i są działa prawidłowo z hello perspektywy sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="35766-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="35766-110">Raporty Hello nie zawierają żadnych monitorowanie kondycji hello logiki biznesowej usługi hello lub wykrywania zawieszone procesy.</span><span class="sxs-lookup"><span data-stu-id="35766-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="35766-111">Usługi użytkownik może uzupełnić hello dane kondycji z logiką tootheir określonych informacji.</span><span class="sxs-lookup"><span data-stu-id="35766-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="35766-112">Watchdogs raportów o kondycji są widoczne tylko *po* składników systemu hello Tworzenie jednostki.</span><span class="sxs-lookup"><span data-stu-id="35766-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="35766-113">Po usunięciu jednostki magazynu kondycji hello automatycznie usuwa wszystkie raporty kondycji skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="35766-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="35766-114">Witaj dotyczy po utworzeniu nowego wystąpienia obiektu hello (na przykład nowe wystąpienie usługi stanowej utrwalonego repliki jest tworzona).</span><span class="sxs-lookup"><span data-stu-id="35766-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="35766-115">Wszystkie raporty skojarzone z wystąpieniem starego hello usunąć i wyczyścić sklepie hello.</span><span class="sxs-lookup"><span data-stu-id="35766-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="35766-116">Witaj raporty składnik systemu są identyfikowane przez źródło hello, w którym rozpoczyna się od hello "**systemu.**"</span><span class="sxs-lookup"><span data-stu-id="35766-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="35766-117">prefiks.</span><span class="sxs-lookup"><span data-stu-id="35766-117">prefix.</span></span> <span data-ttu-id="35766-118">Watchdogs nie można użyć hello sam prefiks dla ich źródła, jak raporty z nieprawidłowe parametry są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="35766-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="35766-119">Załóżmy przyjrzeć się niektóre systemu raporty toounderstand wywołujących je i jak toocorrect hello możliwe problemy reprezentują.</span><span class="sxs-lookup"><span data-stu-id="35766-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="35766-120">Sieć szkieletowa usług nadal tooadd raporty dotyczące warunków odsetek zwiększających wgląd w działania wykonywane w klastrze hello i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35766-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="35766-121">Może również zostać poprawione istniejących raportów z bardziej szczegółowymi informacjami toohelp hello Rozwiązywanie problemów z szybciej.</span><span class="sxs-lookup"><span data-stu-id="35766-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="35766-122">Klaster systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-122">Cluster system health reports</span></span>
<span data-ttu-id="35766-123">jednostki kondycji klastra Hello jest tworzony automatycznie w magazynie kondycji hello.</span><span class="sxs-lookup"><span data-stu-id="35766-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="35766-124">Jeśli wszystko działa prawidłowo, nie ma raportu system.</span><span class="sxs-lookup"><span data-stu-id="35766-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="35766-125">Utrata otoczenie</span><span class="sxs-lookup"><span data-stu-id="35766-125">Neighborhood loss</span></span>
<span data-ttu-id="35766-126">**System.Federation** zgłasza błąd, jeśli wykryje utraty otoczenia.</span><span class="sxs-lookup"><span data-stu-id="35766-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="35766-127">Raport Hello jest w poszczególnych węzłach, a identyfikator węzła hello jest uwzględniony w nazwie właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="35766-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="35766-128">Jeden otoczenie jest zgubiony hello całej sieci szkieletowej usług pierścienia, zwykle można spodziewać się dwa zdarzenia (obie strony raportu przerwę hello).</span><span class="sxs-lookup"><span data-stu-id="35766-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="35766-129">W przypadku utraty więcej klubów ma więcej zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="35766-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="35766-130">Raport Hello określa limit czasu operacji hello globalnego dzierżawy jako czas hello toolive.</span><span class="sxs-lookup"><span data-stu-id="35766-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="35766-131">Raport Hello jest ponowne wysłanie co pół czas TTL hello tak długo, jak warunek hello pozostaje aktywna.</span><span class="sxs-lookup"><span data-stu-id="35766-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="35766-132">Zdarzenie Hello zostanie automatycznie usunięta po jego wygaśnięciu.</span><span class="sxs-lookup"><span data-stu-id="35766-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="35766-133">Usuń, gdy wygasłe zachowanie gwarantuje, że raport hello są czyszczone z magazynu kondycji hello poprawnie, nawet, jeśli węzeł raportowania hello jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="35766-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="35766-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="35766-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="35766-135">**Właściwość**: rozpoczyna się od **otoczenie** i zawiera informacje na węzeł</span><span class="sxs-lookup"><span data-stu-id="35766-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="35766-136">**Następne kroki**: Sprawdź, dlaczego otoczenie hello jest utracone (na przykład wyboru hello komunikacji między węzłami klastra).</span><span class="sxs-lookup"><span data-stu-id="35766-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="35766-137">Węzeł systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-137">Node system health reports</span></span>
<span data-ttu-id="35766-138">**System.FM**, który reprezentuje hello usługi Menedżera trybu Failover, jest urzędu hello, który zarządza informacjami o węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="35766-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="35766-139">Każdy węzeł powinien mieć jeden raport z System.FM przedstawiający jego stanu.</span><span class="sxs-lookup"><span data-stu-id="35766-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="35766-140">jednostek node Hello są usuwane po usunięciu stan węzła hello (zobacz [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="35766-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="35766-141">Węzeł w górę lub w dół</span><span class="sxs-lookup"><span data-stu-id="35766-141">Node up/down</span></span>
<span data-ttu-id="35766-142">System.FM raportów jako OK, gdy węzeł hello dołącza pierścień hello (jest uruchomiona).</span><span class="sxs-lookup"><span data-stu-id="35766-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="35766-143">Zgłasza błąd, gdy węzeł hello odjazdem pierścień hello (działa, albo do uaktualnienia lub po prostu ponieważ nie powiodła się).</span><span class="sxs-lookup"><span data-stu-id="35766-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="35766-144">utworzony przez magazynu kondycji hello hierarchii kondycji Hello podejmuje działania na jednostkach wdrożonej w korelacji z raportów węzłów System.FM.</span><span class="sxs-lookup"><span data-stu-id="35766-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="35766-145">Traktuje hello węzła nadrzędnego wirtualnego wszystkich wdrożonych jednostek.</span><span class="sxs-lookup"><span data-stu-id="35766-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="35766-146">jednostek Hello wdrożone w tym węźle dostępnych za pośrednictwem zapytania, jeśli węzeł hello jest zgłaszana jako się przez System.FM, z hello takie same wystąpienia jako wystąpienie hello skojarzone z jednostek hello.</span><span class="sxs-lookup"><span data-stu-id="35766-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="35766-147">Gdy System.FM zgłasza tego węzła hello jest wyłączony lub ponownego uruchomienia (nowe wystąpienie), magazynu kondycji hello automatycznie oczyszcza hello wdrożone jednostek, które może istnieć tylko na powitania węzeł w dół lub poprzednie wystąpienie hello hello węzła.</span><span class="sxs-lookup"><span data-stu-id="35766-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="35766-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="35766-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="35766-149">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="35766-149">**Property**: State</span></span>
* <span data-ttu-id="35766-150">**Następne kroki**: Jeśli hello węzeł w dół do uaktualnienia, powinna ona przywrócona po został uaktualniony.</span><span class="sxs-lookup"><span data-stu-id="35766-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="35766-151">W takim przypadku stan kondycji hello powinien przełącznika tooOK Wstecz.</span><span class="sxs-lookup"><span data-stu-id="35766-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="35766-152">Jeśli węzeł hello nie wróć lub go nie powiedzie się, hello problem musi więcej dochodzenia.</span><span class="sxs-lookup"><span data-stu-id="35766-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="35766-153">Witaj poniższy przykład przedstawia hello System.FM zdarzeń o stanie kondycji OK dla węzła:</span><span class="sxs-lookup"><span data-stu-id="35766-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="35766-154">Wygaśnięcie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="35766-154">Certificate expiration</span></span>
<span data-ttu-id="35766-155">**System.FabricNode** zgłosi ostrzeżenie, gdy zbliża się ważności certyfikatów używanych przez węzeł hello.</span><span class="sxs-lookup"><span data-stu-id="35766-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="35766-156">Występują trzy certyfikaty w każdym węźle: **Certificate_cluster**, **Certificate_server**, i **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="35766-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="35766-157">Po wygaśnięciu hello jest co najmniej dwa tygodnie, stan kondycji raportów hello jest OK.</span><span class="sxs-lookup"><span data-stu-id="35766-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="35766-158">W przypadku wygaśnięcia hello w ciągu dwóch tygodni, typ raportu hello jest ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="35766-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="35766-159">TTL te zdarzenia jest nieskończone, i usuwane, gdy węzeł opuści hello klastra.</span><span class="sxs-lookup"><span data-stu-id="35766-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="35766-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="35766-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="35766-161">**Właściwość**: rozpoczyna się od **certyfikatu** i zawiera więcej informacji na temat hello typ certyfikatu</span><span class="sxs-lookup"><span data-stu-id="35766-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="35766-162">**Następne kroki**: Aktualizuj certyfikaty, hello, jeśli są one wkrótce wygasną.</span><span class="sxs-lookup"><span data-stu-id="35766-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="35766-163">Naruszenie pojemności obciążenia</span><span class="sxs-lookup"><span data-stu-id="35766-163">Load capacity violation</span></span>
<span data-ttu-id="35766-164">Witaj modułu równoważenia obciążenia sieci szkieletowej usług zgłosi ostrzeżenie po wykryciu naruszenie pojemności węzła.</span><span class="sxs-lookup"><span data-stu-id="35766-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="35766-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="35766-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="35766-166">**Właściwość**: rozpoczyna się od **pojemności**</span><span class="sxs-lookup"><span data-stu-id="35766-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="35766-167">**Następne kroki**: Sprawdź podany obecna pojemność hello metryki i widoku w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="35766-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="35766-168">Aplikacja systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-168">Application system health reports</span></span>
<span data-ttu-id="35766-169">**System.CM**, który reprezentuje hello Menedżera klastra usługi, jest urzędu hello, który zarządza informacjami o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35766-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="35766-170">Stan</span><span class="sxs-lookup"><span data-stu-id="35766-170">State</span></span>
<span data-ttu-id="35766-171">System.CM raporty jako OK aplikacji hello został utworzony lub zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="35766-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="35766-172">Informuje magazynu kondycji powitania po usunięciu aplikacji hello, dzięki czemu może zostać usunięty z magazynu.</span><span class="sxs-lookup"><span data-stu-id="35766-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="35766-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="35766-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="35766-174">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="35766-174">**Property**: State</span></span>
* <span data-ttu-id="35766-175">**Następne kroki**: Jeśli aplikacji hello została utworzona lub zaktualizowana, powinny zawierać hello raport o kondycji Menedżera klastra.</span><span class="sxs-lookup"><span data-stu-id="35766-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="35766-176">W przeciwnym razie sprawdź stan hello aplikacji hello wysyłając kwerendy (na przykład Witaj polecenia cmdlet programu PowerShell **Get ServiceFabricApplication - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="35766-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="35766-177">Witaj poniższy przykład przedstawia zdarzenia stanu hello na powitania **fabric: / WordCount** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="35766-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="35766-178">Usługa systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-178">Service system health reports</span></span>
<span data-ttu-id="35766-179">**System.FM**, który reprezentuje hello usługi Menedżera trybu Failover, jest urzędu hello, który zarządza informacjami o usługach.</span><span class="sxs-lookup"><span data-stu-id="35766-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="35766-180">Stan</span><span class="sxs-lookup"><span data-stu-id="35766-180">State</span></span>
<span data-ttu-id="35766-181">System.FM raporty jako OK po utworzeniu hello usługi.</span><span class="sxs-lookup"><span data-stu-id="35766-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="35766-182">Usuwa hello jednostki z magazynu kondycji powitania po usunięciu hello usługi.</span><span class="sxs-lookup"><span data-stu-id="35766-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="35766-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="35766-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="35766-184">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="35766-184">**Property**: State</span></span>

<span data-ttu-id="35766-185">Witaj poniższy przykład przedstawia zdarzenia stanu hello w usłudze hello **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="35766-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="35766-186">Błąd korelacji usługi</span><span class="sxs-lookup"><span data-stu-id="35766-186">Service correlation error</span></span>
<span data-ttu-id="35766-187">**System.PLB** zgłasza błąd, jeśli wykryje, że aktualizacja toobe usługi, skorelowane z innej usługi tworzy łańcuch koligacji.</span><span class="sxs-lookup"><span data-stu-id="35766-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="35766-188">Raport Hello jest wyczyszczone po pomyślnej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="35766-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="35766-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="35766-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="35766-190">**Właściwość**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="35766-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="35766-191">**Następne kroki**: hello wyboru skorelowane opisy usług.</span><span class="sxs-lookup"><span data-stu-id="35766-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="35766-192">Partycja systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-192">Partition system health reports</span></span>
<span data-ttu-id="35766-193">**System.FM**, który reprezentuje hello usługi Menedżera trybu Failover, jest urzędu hello, który zarządza informacjami o partycji usługi.</span><span class="sxs-lookup"><span data-stu-id="35766-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="35766-194">Stan</span><span class="sxs-lookup"><span data-stu-id="35766-194">State</span></span>
<span data-ttu-id="35766-195">System.FM raportów, jako OK gdy partycji hello został utworzony i działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="35766-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="35766-196">Usuwa hello jednostki z magazynu kondycji powitania po usunięciu hello partycji.</span><span class="sxs-lookup"><span data-stu-id="35766-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="35766-197">W przypadku partycji hello poniżej hello repliki minimalna liczba, zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="35766-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="35766-198">Jeśli hello partycja nie jest mniej hello repliki minimalna liczba, ale jest on poniżej hello docelowa liczba replik, zgłosi ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="35766-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="35766-199">W przypadku partycji hello w wyniku utraty kworum, System.FM zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="35766-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="35766-200">Innych ważnych wydarzeń, zawierać ostrzeżenie podczas ponownej konfiguracji hello trwa dłużej, niż oczekiwano i podczas kompilacji hello trwa dłużej, niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="35766-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="35766-201">czasy Hello oczekiwano hello kompilacji i ponownej konfiguracji są konfigurowane w oparciu o scenariuszach usługi.</span><span class="sxs-lookup"><span data-stu-id="35766-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="35766-202">Na przykład jeśli usługa ma terabajt stanu, takie jak bazy danych SQL, kompilacji hello trwa dłużej niż usługi z małej ilości stanu.</span><span class="sxs-lookup"><span data-stu-id="35766-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="35766-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="35766-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="35766-204">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="35766-204">**Property**: State</span></span>
* <span data-ttu-id="35766-205">**Następne kroki**: Jeśli stan kondycji hello nie jest OK, jest to możliwe, że niektóre repliki nie zostały utworzone, otwarty lub awansowana tooprimary lub pomocniczej poprawnie.</span><span class="sxs-lookup"><span data-stu-id="35766-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="35766-206">W wielu przypadkach hello główną przyczyną jest to błąd usługi w hello open lub implementacji zmiany roli.</span><span class="sxs-lookup"><span data-stu-id="35766-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="35766-207">Witaj poniższy przykład przedstawia partycji dobrej kondycji:</span><span class="sxs-lookup"><span data-stu-id="35766-207">hello following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="35766-208">Witaj poniższy przykład przedstawia kondycję hello partycji, która znajduje się poniżej docelowej liczby replik.</span><span class="sxs-lookup"><span data-stu-id="35766-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="35766-209">Witaj następnym krokiem jest tooget hello partycji opis, który pokazuje, jak skonfigurowano: **MinReplicaSetSize** trzy i **TargetReplicaSetSize** wynosi siedem.</span><span class="sxs-lookup"><span data-stu-id="35766-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="35766-210">Następnie Uzyskaj hello liczby węzłów w klastrze hello: pięć.</span><span class="sxs-lookup"><span data-stu-id="35766-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="35766-211">Dlatego w tym przypadku dwóch replik nie można umieścić, ponieważ liczba replik w docelowym hello jest wyższy niż hello liczby dostępnych węzłów.</span><span class="sxs-lookup"><span data-stu-id="35766-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="35766-212">Naruszenie ograniczenia repliki</span><span class="sxs-lookup"><span data-stu-id="35766-212">Replica constraint violation</span></span>
<span data-ttu-id="35766-213">**System.PLB** zgłosi ostrzeżenie, jeśli wykryje naruszenie ograniczenia repliki i nie można umieścić wszystkich replik partycji.</span><span class="sxs-lookup"><span data-stu-id="35766-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="35766-214">wyświetlone szczegóły raportu Hello których ograniczeń i właściwości zapobiec hello repliki umieszczania.</span><span class="sxs-lookup"><span data-stu-id="35766-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="35766-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="35766-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="35766-216">**Właściwość**: rozpoczyna się od **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="35766-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="35766-217">Repliki systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-217">Replica system health reports</span></span>
<span data-ttu-id="35766-218">**System.RA**, reprezentuje składnika agenta rekonfiguracji hello, jest źródłem hello hello stanu repliki.</span><span class="sxs-lookup"><span data-stu-id="35766-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="35766-219">Stan</span><span class="sxs-lookup"><span data-stu-id="35766-219">State</span></span>
<span data-ttu-id="35766-220">**System.RA** raporty OK po utworzeniu repliki hello.</span><span class="sxs-lookup"><span data-stu-id="35766-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="35766-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="35766-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="35766-222">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="35766-222">**Property**: State</span></span>

<span data-ttu-id="35766-223">Witaj poniższy przykład przedstawia repliki dobrej kondycji:</span><span class="sxs-lookup"><span data-stu-id="35766-223">hello following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="35766-224">Otwórz stanu repliki</span><span class="sxs-lookup"><span data-stu-id="35766-224">Replica open status</span></span>
<span data-ttu-id="35766-225">Opis Hello raport o kondycji zawiera czas rozpoczęcia hello (Coordinated Universal Time) podczas wywołania hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="35766-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="35766-226">**System.RA** zgłosi ostrzeżenie, jeśli repliki hello Otwórz trwa dłużej niż okres hello skonfigurowane (domyślne: 30 minut).</span><span class="sxs-lookup"><span data-stu-id="35766-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="35766-227">Jeśli hello interfejsu API ma wpływ na dostępność usługi, raport hello zgłaszany jest znacznie szybciej (można skonfigurować interwał, z domyślną 30 sekund).</span><span class="sxs-lookup"><span data-stu-id="35766-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="35766-228">czas Hello obejmuje czas hello replikatora hello Otwórz i Otwórz usługę hello.</span><span class="sxs-lookup"><span data-stu-id="35766-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="35766-229">kończy Hello tooOK zmiany właściwości hello otwarcia.</span><span class="sxs-lookup"><span data-stu-id="35766-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="35766-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="35766-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="35766-231">**Właściwość**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="35766-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="35766-232">**Następne kroki**: Jeśli stan kondycji hello nie jest OK, sprawdź, dlaczego repliki hello Otwórz trwa dłużej, niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="35766-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="35766-233">Wywołanie interfejsu API usługi powolne</span><span class="sxs-lookup"><span data-stu-id="35766-233">Slow service API call</span></span>
<span data-ttu-id="35766-234">**System.RAP** i **System.Replicator** raport ostrzeżenie, jeśli kod wywołania toohello użytkownika usługi trwa dłużej niż hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="35766-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="35766-235">Ostrzeżenie Hello są czyszczone po zakończeniu wywołania hello.</span><span class="sxs-lookup"><span data-stu-id="35766-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="35766-236">**SourceId**: System.RAP lub System.Replicator</span><span class="sxs-lookup"><span data-stu-id="35766-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="35766-237">**Właściwość**: Nazwa hello hello powolne interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="35766-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="35766-238">Opis Hello zawiera szczegółowe informacje o hello czasu hello interfejsu API został oczekujące.</span><span class="sxs-lookup"><span data-stu-id="35766-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="35766-239">**Następne kroki**: Sprawdź, dlaczego wywołania hello trwa dłużej, niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="35766-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="35766-240">Hello poniższy przykład przedstawia partycja utraciła kworum i hello dochodzenia czynności wykonywane toofigure się, dlaczego.</span><span class="sxs-lookup"><span data-stu-id="35766-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="35766-241">Jeden z replik hello ma ostrzegawczy stan kondycji, aby uzyskać jego kondycji.</span><span class="sxs-lookup"><span data-stu-id="35766-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="35766-242">Pokazuje, że operacja usługi hello trwa dłużej, niż oczekiwano zdarzenie zgłaszane przez System.RAP.</span><span class="sxs-lookup"><span data-stu-id="35766-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="35766-243">Po otrzymaniu tych informacji hello następnym krokiem jest toolook na powitania kodu usługi i zbadaj istnieje.</span><span class="sxs-lookup"><span data-stu-id="35766-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="35766-244">Dla tego przypadku hello **RunAsync** implementacji usługi stanowej hello zgłasza nieobsługiwany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="35766-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="35766-245">repliki Hello są odzyskiwanie, więc nie widać żadnych replik w stanie ostrzeżenia hello.</span><span class="sxs-lookup"><span data-stu-id="35766-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="35766-246">Można ponowić próbę pobierania stanu kondycji hello i wyszukaj różnice w identyfikatorze hello repliki.</span><span class="sxs-lookup"><span data-stu-id="35766-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="35766-247">W niektórych przypadkach prób hello pozwalają uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="35766-247">In certain cases, hello retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="35766-248">Po uruchomieniu hello błędnej aplikacji w debugerze hello windows zdarzeń diagnostycznych hello Pokaż hello wyjątek z RunAsync:</span><span class="sxs-lookup"><span data-stu-id="35766-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![Visual Studio 2015 zdarzeń diagnostycznych: niepowodzenie RunAsync w sieci szkieletowej: / HelloWorldStatefulApplication.][1]

<span data-ttu-id="35766-250">Visual Studio 2015 zdarzeń diagnostycznych: niepowodzenie RunAsync w **fabric: / HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="35766-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="35766-251">Kolejka replikacji jest pełna</span><span class="sxs-lookup"><span data-stu-id="35766-251">Replication queue full</span></span>
<span data-ttu-id="35766-252">**System.Replicator** zgłosi ostrzeżenie, gdy kolejka replikacji hello jest pełna.</span><span class="sxs-lookup"><span data-stu-id="35766-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="35766-253">Na głównej hello kolejki replikacji zazwyczaj zapełni ponieważ co najmniej jeden replikach pomocniczych operacji tooacknowledge powolne.</span><span class="sxs-lookup"><span data-stu-id="35766-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="35766-254">Na powitania dodatkowej to zazwyczaj miejsce, gdy usługa hello jest powolne tooapply hello operacji.</span><span class="sxs-lookup"><span data-stu-id="35766-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="35766-255">Ostrzeżenie Hello są czyszczone po hello kolejki nie jest już pełna.</span><span class="sxs-lookup"><span data-stu-id="35766-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="35766-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="35766-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="35766-257">**Właściwość**: **PrimaryReplicationQueueStatus** lub **SecondaryReplicationQueueStatus**w zależności od roli repliki hello</span><span class="sxs-lookup"><span data-stu-id="35766-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="35766-258">Powolne operacje nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="35766-258">Slow Naming operations</span></span>
<span data-ttu-id="35766-259">**System.NamingService** raportów kondycji na jego repliką podstawową, gdy operacja nazewnictwa trwa dłużej niż dopuszczalne.</span><span class="sxs-lookup"><span data-stu-id="35766-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="35766-260">Przykłady operacji nazewnictwa [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) lub [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="35766-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="35766-261">Więcej metod można znaleźć w obszarze klienta fabricclient z rolą, na przykład w obszarze [usługi metod zarządzania](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) lub [metod zarządzania właściwości](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="35766-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="35766-262">Hello Naming service jest rozpoznawany jako lokalizacja tooa nazwy usługi w klastrze hello i umożliwia użytkownikom toomanage usługi nazwy i właściwości.</span><span class="sxs-lookup"><span data-stu-id="35766-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="35766-263">Jest to sieć szkieletowa usług na partycje utrwalone usługi.</span><span class="sxs-lookup"><span data-stu-id="35766-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="35766-264">Reprezentuje jedną z partycji hello hello Authority Owner zawierający metadane dotyczące wszystkich nazw usługi Service Fabric i usług.</span><span class="sxs-lookup"><span data-stu-id="35766-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="35766-265">nazwy sieci szkieletowej usług Hello są mapowane toodifferent partycji, o nazwie właściciela partycji, dlatego usługa hello jest rozszerzony.</span><span class="sxs-lookup"><span data-stu-id="35766-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="35766-266">Przeczytaj więcej na temat [Naming service](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="35766-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="35766-267">Podczas operacji nazewnictwa trwa dłużej, niż oczekiwano, operacja hello oflagowane z raportem ostrzeżenie na powitania *replikę podstawową hello partycji usługi nazw, która służy operacji hello*.</span><span class="sxs-lookup"><span data-stu-id="35766-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="35766-268">Jeśli operacja hello zakończy się pomyślnie, hello ostrzeżenie jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="35766-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="35766-269">Jeśli hello zakończeniu operacji z powodu błędu hello raport o kondycji zawiera szczegółowe informacje o błędzie hello.</span><span class="sxs-lookup"><span data-stu-id="35766-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="35766-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="35766-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="35766-271">**Właściwość**: rozpoczyna się od prefiksu **Duration_** i identyfikuje hello wolne działanie i nazwę sieci szkieletowej usług hello, w których hello operacji są stosowane.</span><span class="sxs-lookup"><span data-stu-id="35766-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="35766-272">Na przykład jeśli Tworzenie usługi w sieci szkieletowej name: / MyApp/Moja_usługa trwa zbyt długo, właściwość hello jest Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="35766-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="35766-273">AO rola toohello punktów hello nazw partycji dla tej nazwy i operację.</span><span class="sxs-lookup"><span data-stu-id="35766-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="35766-274">**Następne kroki**: niepowodzenia hello nazewnictwa operacji wyboru.</span><span class="sxs-lookup"><span data-stu-id="35766-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="35766-275">Każda operacja mogą mieć różnych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="35766-275">Each operation can have different root causes.</span></span> <span data-ttu-id="35766-276">Na przykład usunąć usługi mogą zostać zatrzymane w węźle, ponieważ host aplikacji hello śledzi awarii w węźle powodu usterki użytkownika tooa hello kodem usługi.</span><span class="sxs-lookup"><span data-stu-id="35766-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="35766-277">Witaj poniższy przykład przedstawia operację tworzenia usługi.</span><span class="sxs-lookup"><span data-stu-id="35766-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="35766-278">Operacja Hello trwało dłużej niż czas trwania hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="35766-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="35766-279">AO ponawia próbę i wysyła tooNO pracy.</span><span class="sxs-lookup"><span data-stu-id="35766-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="35766-280">NIE ukończono hello ostatniej operacji limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="35766-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="35766-281">W takim przypadku hello tej samej repliki jest kluczem podstawowym hello AO i żadnych ról.</span><span class="sxs-lookup"><span data-stu-id="35766-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="35766-282">DeployedApplication systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="35766-283">**System.Hosting** urzędu hello na wdrożonym jednostek.</span><span class="sxs-lookup"><span data-stu-id="35766-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="35766-284">aktywacji</span><span class="sxs-lookup"><span data-stu-id="35766-284">Activation</span></span>
<span data-ttu-id="35766-285">System.Hosting raportów, jako OK gdy aplikacji został pomyślnie uaktywniony na powitania węzła.</span><span class="sxs-lookup"><span data-stu-id="35766-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="35766-286">W przeciwnym razie go zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="35766-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="35766-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="35766-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="35766-288">**Właściwość**: aktywacji wersji wdrożenia hello</span><span class="sxs-lookup"><span data-stu-id="35766-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="35766-289">**Następne kroki**: Jeśli aplikacja hello jest zła, sprawdź, dlaczego hello aktywacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="35766-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="35766-290">Witaj poniższy przykład przedstawia pomyślnej aktywacji:</span><span class="sxs-lookup"><span data-stu-id="35766-290">hello following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="35766-291">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="35766-291">Download</span></span>
<span data-ttu-id="35766-292">**System.Hosting** zgłasza błąd, jeśli pobieranie pakietu aplikacji hello nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="35766-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="35766-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="35766-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="35766-294">**Właściwość**:  **pobrać:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="35766-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="35766-295">**Następne kroki**: Sprawdź, dlaczego hello pobieranie nie powiodło się w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="35766-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="35766-296">DeployedServicePackage systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="35766-297">**System.Hosting** urzędu hello na wdrożonym jednostek.</span><span class="sxs-lookup"><span data-stu-id="35766-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="35766-298">Aktywowanie pakietu usługi</span><span class="sxs-lookup"><span data-stu-id="35766-298">Service package activation</span></span>
<span data-ttu-id="35766-299">Jako OK System.Hosting raporty, jeśli aktywowanie pakietu usługi hello w węźle hello zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="35766-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="35766-300">W przeciwnym razie go zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="35766-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="35766-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="35766-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="35766-302">**Właściwość**: aktywacji</span><span class="sxs-lookup"><span data-stu-id="35766-302">**Property**: Activation</span></span>
* <span data-ttu-id="35766-303">**Następne kroki**: Sprawdź, dlaczego hello aktywacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="35766-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="35766-304">Aktywowanie pakietu kodu</span><span class="sxs-lookup"><span data-stu-id="35766-304">Code package activation</span></span>
<span data-ttu-id="35766-305">**System.Hosting** raporty jako OK dla każdego pakietu kodu, jeśli aktywacja hello zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="35766-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="35766-306">W przypadku niepowodzenia aktywacji hello zgłosi ostrzeżenie zgodnie z konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="35766-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="35766-307">Jeśli **elementu CodePackage** nie powiedzie się tooactivate lub kończy się z powodu błędu większy niż skonfigurowany hello **CodePackageHealthErrorThreshold**, hosting zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="35766-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="35766-308">Jeśli pakiet usługi zawiera wiele pakietów kodu, aktywacji raport jest generowany dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="35766-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="35766-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="35766-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="35766-310">**Właściwość**: prefiks hello używa **CodePackageActivation** i zawiera nazwę hello hello pakietu kodu i punktu wejścia hello jako  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint*** (na przykład **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="35766-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="35766-311">Rejestracja typu usługi</span><span class="sxs-lookup"><span data-stu-id="35766-311">Service type registration</span></span>
<span data-ttu-id="35766-312">**System.Hosting** zgłasza jako OK, jeśli typ usługi hello został pomyślnie zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="35766-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="35766-313">Zgłasza błąd, jeśli hello rejestracja nie została wykonana w czasie (zgodnie z konfiguracją przy użyciu **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="35766-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="35766-314">Jeśli środowisko uruchomieniowe hello są zamknięte, typ usługi hello jest zarejestrowany z węzła hello i hostingu zgłosi ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="35766-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="35766-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="35766-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="35766-316">**Właściwość**: prefiks hello używa **ServiceTypeRegistration** i zawiera nazwę typu usługi hello (na przykład **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="35766-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="35766-317">Witaj poniższy przykład przedstawia pakietu dobrej kondycji wdrożonej usługi:</span><span class="sxs-lookup"><span data-stu-id="35766-317">hello following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="35766-318">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="35766-318">Download</span></span>
<span data-ttu-id="35766-319">**System.Hosting** zgłasza błąd, jeśli pobieranie pakietu hello usługi nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="35766-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="35766-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="35766-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="35766-321">**Właściwość**:  **pobrać:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="35766-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="35766-322">**Następne kroki**: Sprawdź, dlaczego hello pobieranie nie powiodło się w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="35766-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="35766-323">Weryfikacja uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="35766-323">Upgrade validation</span></span>
<span data-ttu-id="35766-324">**System.Hosting** zgłasza błąd w przypadku niepowodzenia weryfikacji podczas uaktualniania hello lub hello uaktualnienie nie powiedzie się w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="35766-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="35766-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="35766-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="35766-326">**Właściwość**: prefiks hello używa **FabricUpgradeValidation** i zawiera hello uaktualniania wersji</span><span class="sxs-lookup"><span data-stu-id="35766-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="35766-327">**Opis elementu**: Napotkano błąd toohello punktów</span><span class="sxs-lookup"><span data-stu-id="35766-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="35766-328">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35766-328">Next steps</span></span>
[<span data-ttu-id="35766-329">Wyświetl raporty dotyczące kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="35766-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="35766-330">Jak tooreport i zaznacz pole wyboru usługi kondycji</span><span class="sxs-lookup"><span data-stu-id="35766-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="35766-331">Monitorowanie i diagnozowania usług lokalnie</span><span class="sxs-lookup"><span data-stu-id="35766-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="35766-332">Uaktualnianie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="35766-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

