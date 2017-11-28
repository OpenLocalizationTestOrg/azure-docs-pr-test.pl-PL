---
title: "Rozwiązywanie problemów z raportów o kondycji systemu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano raportów kondycji wysyłane przez składniki sieci szkieletowej usług Azure i ich użycia dla klastra rozwiązywaniu problemów lub problemów aplikacji."
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
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="5dfa6-103">Używanie raportów kondycji systemu do rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="5dfa6-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="5dfa6-104">Azure Service Fabric składniki raport poza pole na wszystkich jednostek w klastrze.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="5dfa6-105">[Magazynu kondycji](service-fabric-health-introduction.md#health-store) tworzy i usuwa jednostki na podstawie raportów systemu.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="5dfa6-106">Również organizuje ona je w hierarchii, która przechwytuje interakcje jednostki.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="5dfa6-107">Aby zapoznać się z kondycją pojęcia, Dowiedz się więcej na [model kondycji sieci szkieletowej usług](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="5dfa6-108">Raporty kondycji systemu zapewniają wgląd w klastrze i funkcjonalność aplikacji i flagi błędów za pomocą kondycji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="5dfa6-109">Dla aplikacji i usług systemowych raportów kondycji Sprawdź, czy jednostki są zaimplementowane i są działa prawidłowo z punktu widzenia sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="5dfa6-110">Raporty nie zawierają żadnych monitorowanie kondycji logiki biznesowej usługi lub wykrywania zawieszone procesy.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="5dfa6-111">Usługi użytkownik może uzupełnić dane kondycji z użyciem informacji specyficznych ich logiki.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="5dfa6-112">Watchdogs raportów o kondycji są widoczne tylko *po* składników systemu Tworzenie jednostki.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="5dfa6-113">Po usunięciu jednostki magazynu kondycji automatycznie usuwa wszystkie raporty kondycji skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="5dfa6-114">To samo dotyczy po utworzeniu nowego wystąpienia obiektu (na przykład nowe wystąpienie usługi stanowej utrwalonego repliki jest tworzona).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-114">The same is true when a new instance of the entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="5dfa6-115">Wszystkie raporty skojarzone z wystąpieniem stare usunąć i wyczyścić ze sklepu.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="5dfa6-116">Składnik systemu raporty są identyfikowane przez źródło, w którym rozpoczyna się od "**systemu.**"</span><span class="sxs-lookup"><span data-stu-id="5dfa6-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="5dfa6-117">prefiks.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-117">prefix.</span></span> <span data-ttu-id="5dfa6-118">Watchdogs nie można użyć tego samego prefiksu dla ich źródła, jak raporty z nieprawidłowe parametry są odrzucane.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="5dfa6-119">Oto niektóre raporty systemu, aby zrozumieć wywołujących je i jak skorygować możliwe problemy, które reprezentują.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="5dfa6-120">Sieć szkieletowa usług w dalszym ciągu Dodaj raporty warunków odsetek zwiększających wgląd w działania wykonywane w klastrze i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span> <span data-ttu-id="5dfa6-121">Istniejące raporty mogą być również dołączane więcej szczegółów, aby ułatwić rozwiązanie problemu szybciej.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-121">Existing reports can also be enhanced with more details to help troubleshoot the problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="5dfa6-122">Klaster systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-122">Cluster system health reports</span></span>
<span data-ttu-id="5dfa6-123">Jednostki kondycji klastra jest tworzony automatycznie w magazynie kondycji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-123">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="5dfa6-124">Jeśli wszystko działa prawidłowo, nie ma raportu system.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="5dfa6-125">Utrata otoczenie</span><span class="sxs-lookup"><span data-stu-id="5dfa6-125">Neighborhood loss</span></span>
<span data-ttu-id="5dfa6-126">**System.Federation** zgłasza błąd, jeśli wykryje utraty otoczenia.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="5dfa6-127">Raport jest w poszczególnych węzłach, a identyfikator węzła jest uwzględniony w nazwie właściwości.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-127">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="5dfa6-128">Jeden otoczenie jest zgubiony w kręgu całej sieci szkieletowej usług, zwykle można spodziewać się dwa zdarzenia (obie strony raportu gap).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-128">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="5dfa6-129">W przypadku utraty więcej klubów ma więcej zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="5dfa6-130">Raport określa limit czasu globalnego dzierżawy jako czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-130">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="5dfa6-131">Raport jest ponowne wysłanie co pół czas TTL, jak długo warunek pozostaje aktywna.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-131">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="5dfa6-132">Zdarzenie zostanie automatycznie usunięta po jego wygaśnięciu.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-132">The event is automatically removed when it expires.</span></span> <span data-ttu-id="5dfa6-133">Usuń, gdy wygasłe zachowanie gwarantuje, że raportu są czyszczone z magazynu kondycji poprawnie, nawet, jeśli węzeł raportowania jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-133">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="5dfa6-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="5dfa6-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="5dfa6-135">**Właściwość**: rozpoczyna się od **otoczenie** i zawiera informacje na węzeł</span><span class="sxs-lookup"><span data-stu-id="5dfa6-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="5dfa6-136">**Następne kroki**: Sprawdź, dlaczego otoczenie zostaną utracone (na przykład sprawdzić komunikację między węzłami klastra).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-136">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="5dfa6-137">Węzeł systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-137">Node system health reports</span></span>
<span data-ttu-id="5dfa6-138">**System.FM**, który reprezentuje usługę Menedżer trybu Failover jest urzędu, który zarządza informacjami o węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-138">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="5dfa6-139">Każdy węzeł powinien mieć jeden raport z System.FM przedstawiający jego stanu.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="5dfa6-140">Jednostek node są usuwane po usunięciu stanu węzła (zobacz [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-140">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="5dfa6-141">Węzeł w górę lub w dół</span><span class="sxs-lookup"><span data-stu-id="5dfa6-141">Node up/down</span></span>
<span data-ttu-id="5dfa6-142">System.FM raportów jako OK, gdy węzeł dołączy pierścień (jest uruchomiona).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-142">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="5dfa6-143">Zgłasza błąd, gdy węzeł odjazdem pierścienia (działa, albo do uaktualnienia lub po prostu ponieważ nie powiodła się).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-143">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="5dfa6-144">Hierarchia kondycji utworzony przez magazynu kondycji podejmuje działania na jednostkach wdrożonej w korelacji z System.FM węzła Raporty.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-144">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="5dfa6-145">Traktuje węzła nadrzędnego wirtualnego wszystkich wdrożonych jednostek.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-145">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="5dfa6-146">Jednostek wdrożonych w tym węźle dostępnych za pośrednictwem zapytania, jeśli węzeł został zgłoszony jako czas przez System.FM z tego samego wystąpienia jako wystąpienie skojarzone z jednostkami.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-146">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="5dfa6-147">Gdy System.FM zgłasza, że węzeł nie działa lub ponownego uruchomienia (nowe wystąpienie), magazynu kondycji automatycznie oczyszcza wdrożonej jednostek, które może istnieć tylko na dół węzła lub poprzednie wystąpienie węzła.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-147">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="5dfa6-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5dfa6-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5dfa6-149">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-149">**Property**: State</span></span>
* <span data-ttu-id="5dfa6-150">**Następne kroki**: Jeśli węzeł nie działa w przypadku uaktualnienia, powinna ona przywrócona po został uaktualniony.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-150">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="5dfa6-151">W takim przypadku stan kondycji powinna przejdź do OK.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-151">In this case, the health state should switch back to OK.</span></span> <span data-ttu-id="5dfa6-152">Jeśli węzeł nie wróć lub go nie powiedzie się, problem wymaga więcej dochodzenia.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-152">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="5dfa6-153">W poniższym przykładzie przedstawiono System.FM zdarzenia o stanie kondycji OK dla węzła w:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-153">The following example shows the System.FM event with a health state of OK for node up:</span></span>

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


### <a name="certificate-expiration"></a><span data-ttu-id="5dfa6-154">Wygaśnięcie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="5dfa6-154">Certificate expiration</span></span>
<span data-ttu-id="5dfa6-155">**System.FabricNode** zgłosi ostrzeżenie, gdy zbliża się ważności certyfikatów używanych przez węzeł.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-155">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="5dfa6-156">Występują trzy certyfikaty w każdym węźle: **Certificate_cluster**, **Certificate_server**, i **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="5dfa6-157">Jeśli czas wygaśnięcia jest co najmniej dwa tygodnie, stan kondycji raportu jest OK.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-157">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="5dfa6-158">Jeśli czas wygaśnięcia jest w ciągu dwóch tygodni, jego typ jest ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-158">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="5dfa6-159">TTL te zdarzenia jest nieskończone, i usuwane, gdy węzeł opuści klastra.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-159">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="5dfa6-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="5dfa6-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="5dfa6-161">**Właściwość**: rozpoczyna się od **certyfikatu** i zawiera więcej informacji na temat typ certyfikatu</span><span class="sxs-lookup"><span data-stu-id="5dfa6-161">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="5dfa6-162">**Następne kroki**: zaktualizować certyfikaty, jeśli są one wkrótce wygasną.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-162">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="5dfa6-163">Naruszenie pojemności obciążenia</span><span class="sxs-lookup"><span data-stu-id="5dfa6-163">Load capacity violation</span></span>
<span data-ttu-id="5dfa6-164">Usługa równoważenia obciążenia sieci szkieletowej zgłosi ostrzeżenie po wykryciu naruszenie pojemności węzła.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-164">The Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="5dfa6-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5dfa6-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5dfa6-166">**Właściwość**: rozpoczyna się od **pojemności**</span><span class="sxs-lookup"><span data-stu-id="5dfa6-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="5dfa6-167">**Następne kroki**: Sprawdź podane metryki i wyświetlić w węźle pojemność bieżąca.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-167">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="5dfa6-168">Aplikacja systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-168">Application system health reports</span></span>
<span data-ttu-id="5dfa6-169">**System.CM**, który reprezentuje usługę Menedżer klastra jest urzędu, który zarządza informacjami o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-169">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="5dfa6-170">Stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-170">State</span></span>
<span data-ttu-id="5dfa6-171">System.CM raportów, jako OK gdy aplikacji została utworzona lub zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-171">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="5dfa6-172">Informuje magazynu kondycji po usunięciu aplikacji, dzięki czemu może zostać usunięty z magazynu.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-172">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="5dfa6-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="5dfa6-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="5dfa6-174">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-174">**Property**: State</span></span>
* <span data-ttu-id="5dfa6-175">**Następne kroki**: Jeśli aplikacja została utworzona lub aktualizowane, powinny zawierać raport o kondycji Menedżera klastra.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-175">**Next steps**: If the application has been created or updated, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="5dfa6-176">W przeciwnym razie sprawdź stan aplikacji, wysyłając zapytanie (na przykład polecenia cmdlet programu PowerShell **Get ServiceFabricApplication - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-176">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="5dfa6-177">W poniższym przykładzie przedstawiono zdarzenia stanu na **fabric: / WordCount** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-177">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

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

## <a name="service-system-health-reports"></a><span data-ttu-id="5dfa6-178">Usługa systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-178">Service system health reports</span></span>
<span data-ttu-id="5dfa6-179">**System.FM**, który reprezentuje usługę Menedżer trybu Failover jest urzędu, który zarządza informacjami o usługach.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-179">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="5dfa6-180">Stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-180">State</span></span>
<span data-ttu-id="5dfa6-181">System.FM raporty jako OK po utworzeniu usługi.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-181">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="5dfa6-182">Usuwa obiekt z magazynu kondycji po usunięciu usługi.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-182">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="5dfa6-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5dfa6-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5dfa6-184">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-184">**Property**: State</span></span>

<span data-ttu-id="5dfa6-185">W poniższym przykładzie przedstawiono zdarzenia stanu usługi **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-185">The following example shows the state event on the service **fabric:/WordCount/WordCountWebService**:</span></span>

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

### <a name="service-correlation-error"></a><span data-ttu-id="5dfa6-186">Błąd korelacji usługi</span><span class="sxs-lookup"><span data-stu-id="5dfa6-186">Service correlation error</span></span>
<span data-ttu-id="5dfa6-187">**System.PLB** zgłasza błąd, jeśli wykryje, czy uaktualnianie usługi mają zostać skorelowane z inną usługą tworzy łańcuch koligacji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-187">**System.PLB** reports an error when it detects that updating a service to be correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="5dfa6-188">Raport jest wyczyszczone po pomyślnej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-188">The report is cleared when successful update happens.</span></span>

* <span data-ttu-id="5dfa6-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5dfa6-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5dfa6-190">**Właściwość**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="5dfa6-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="5dfa6-191">**Następne kroki**: Sprawdź opisy skorelowane usług.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-191">**Next steps**: Check the correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="5dfa6-192">Partycja systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-192">Partition system health reports</span></span>
<span data-ttu-id="5dfa6-193">**System.FM**, reprezentuje usługą Failover Manager service jest urzędu, który zarządza informacjami o partycji usługi.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="5dfa6-194">Stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-194">State</span></span>
<span data-ttu-id="5dfa6-195">System.FM raportów, jako OK, gdy partycja został utworzony i działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="5dfa6-196">Usuwa obiekt z magazynu kondycji po usunięciu partycji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="5dfa6-197">W przypadku partycji mniej niż liczba minimalna repliki, zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="5dfa6-198">Jeśli partycja nie jest mniej niż liczba minimalna repliki, ale jest mniejsza od liczby replik docelowej, zgłosi ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="5dfa6-199">W przypadku partycji w wyniku utraty kworum, System.FM zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="5dfa6-200">Innych ważnych wydarzeń, zawierać ostrzeżenie podczas ponownej konfiguracji trwa dłużej, niż oczekiwano, a jeśli Kompilacja trwa dłużej, niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="5dfa6-201">Przewidywany czas dla kompilacji i ponownej konfiguracji są konfigurowane na podstawie scenariuszy usługi.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="5dfa6-202">Na przykład jeśli usługa ma terabajt stanu, takie jak bazy danych SQL, Kompilacja trwa dłużej niż usługi z małej ilości stanu.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="5dfa6-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="5dfa6-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="5dfa6-204">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-204">**Property**: State</span></span>
* <span data-ttu-id="5dfa6-205">**Następne kroki**: Jeśli kondycja nie jest OK, istnieje możliwość, że niektóre repliki nie zostały utworzone, otwarte lub poziom jest podwyższany do podstawowej lub pomocniczej poprawnie.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="5dfa6-206">W wielu przypadkach główną przyczyną jest to błąd usługi w implementacji open lub zmiany roli.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="5dfa6-207">W poniższym przykładzie przedstawiono partycji dobrej kondycji:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-207">The following example shows a healthy partition:</span></span>

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

<span data-ttu-id="5dfa6-208">Poniższy przykład przedstawia kondycję partycji, która znajduje się poniżej docelowej liczby replik.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="5dfa6-209">Następnym krokiem jest, aby uzyskać opis partycji, który przedstawia sposób skonfigurowania: **MinReplicaSetSize** trzy i **TargetReplicaSetSize** wynosi siedem.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="5dfa6-210">Następnie Pobierz liczbę węzłów w klastrze: pięć.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="5dfa6-211">Dlatego w tym przypadku dwóch replik nie można umieścić, ponieważ docelowy liczba replik jest wyższa niż liczba dostępnych węzłów.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-211">So in this case, two replicas can't be placed because the target number of replicas is higher than the number of nodes available.</span></span>

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
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
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

### <a name="replica-constraint-violation"></a><span data-ttu-id="5dfa6-212">Naruszenie ograniczenia repliki</span><span class="sxs-lookup"><span data-stu-id="5dfa6-212">Replica constraint violation</span></span>
<span data-ttu-id="5dfa6-213">**System.PLB** zgłosi ostrzeżenie, jeśli wykryje naruszenie ograniczenia repliki i nie można umieścić wszystkich replik partycji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="5dfa6-214">Szczegóły raportu Pokaż których ograniczeń i właściwości zapobiec umieszczania repliki.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-214">The report details show which constraints and properties prevent the replica placement.</span></span>

* <span data-ttu-id="5dfa6-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="5dfa6-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="5dfa6-216">**Właściwość**: rozpoczyna się od **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="5dfa6-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="5dfa6-217">Repliki systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-217">Replica system health reports</span></span>
<span data-ttu-id="5dfa6-218">**System.RA**, reprezentuje składnika agenta rekonfiguracji, jest serwerem autorytatywnym dla stanu repliki.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-218">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="5dfa6-219">Stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-219">State</span></span>
<span data-ttu-id="5dfa6-220">**System.RA** raporty OK po utworzeniu repliki.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-220">**System.RA** reports OK when the replica has been created.</span></span>

* <span data-ttu-id="5dfa6-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="5dfa6-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="5dfa6-222">**Właściwość**: stan</span><span class="sxs-lookup"><span data-stu-id="5dfa6-222">**Property**: State</span></span>

<span data-ttu-id="5dfa6-223">W poniższym przykładzie przedstawiono repliki dobrej kondycji:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-223">The following example shows a healthy replica:</span></span>

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

### <a name="replica-open-status"></a><span data-ttu-id="5dfa6-224">Otwórz stanu repliki</span><span class="sxs-lookup"><span data-stu-id="5dfa6-224">Replica open status</span></span>
<span data-ttu-id="5dfa6-225">Opis tego raportu o kondycji zawiera czas rozpoczęcia (Coordinated Universal Time), gdy wywołano wywołanie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-225">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="5dfa6-226">**System.RA** zgłosi ostrzeżenie, jeśli replika Otwórz trwa dłużej niż skonfigurowanego okresu (domyślne: 30 minut).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-226">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="5dfa6-227">Jeśli interfejs API ma wpływ na dostępność usługi, raport, zgłaszany jest znacznie szybciej (można skonfigurować interwał, z domyślną 30 sekund).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-227">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="5dfa6-228">Czas obejmuje czas poświęcony na Otwórz replikatora i Otwórz usługę.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-228">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="5dfa6-229">Po zakończeniu Otwórz właściwość zmienia się na OK.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-229">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="5dfa6-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="5dfa6-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="5dfa6-231">**Właściwość**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="5dfa6-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="5dfa6-232">**Następne kroki**: Jeśli stan kondycji nie jest OK, sprawdź, dlaczego Otwórz repliki trwa dłużej, niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-232">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="5dfa6-233">Wywołanie interfejsu API usługi powolne</span><span class="sxs-lookup"><span data-stu-id="5dfa6-233">Slow service API call</span></span>
<span data-ttu-id="5dfa6-234">**System.RAP** i **System.Replicator** raportować ostrzeżenie w przypadku wywołania do kodu użytkownika usługi trwa dłużej niż w skonfigurowanym czasie.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-234">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="5dfa6-235">To ostrzeżenie zostanie wyczyszczona po zakończeniu wywołania.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-235">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="5dfa6-236">**SourceId**: System.RAP lub System.Replicator</span><span class="sxs-lookup"><span data-stu-id="5dfa6-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="5dfa6-237">**Właściwość**: Nazwa powolne interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-237">**Property**: The name of the slow API.</span></span> <span data-ttu-id="5dfa6-238">Opis zawiera więcej informacji na temat interfejsu API został oczekujące czas.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-238">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="5dfa6-239">**Następne kroki**: Sprawdź, dlaczego wywołanie trwa dłużej, niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-239">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="5dfa6-240">Poniższy przykład przedstawia partycji w wyniku utraty kworum i kroki dochodzenia gotowe, aby dowiedzieć się, dlaczego.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-240">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="5dfa6-241">Jednej z replik ma ostrzegawczy stan kondycji, aby uzyskać jego kondycji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-241">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="5dfa6-242">Przedstawia on, że operacja usługi trwa dłużej, niż oczekiwano zdarzenie zgłaszane przez System.RAP.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-242">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="5dfa6-243">Po otrzymaniu tych informacji, następnym krokiem jest przyjrzeć się kodu usługi i badanie istnieje.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-243">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="5dfa6-244">Dla tego przypadku **RunAsync** implementacji usługi stanowej zgłasza nieobsługiwany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-244">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="5dfa6-245">Repliki są odzyskiwanie, więc nie widać żadnych replik w stanie ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-245">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="5dfa6-246">Możesz ponowić próbę pobierania stanu kondycji i wyszukaj różnice w identyfikatorze repliki.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-246">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="5dfa6-247">W niektórych przypadkach ponowne próby pozwoli uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-247">In certain cases, the retries can give you clues.</span></span>

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

<span data-ttu-id="5dfa6-248">Po uruchomieniu błędnej aplikacji w debugerze okna zdarzeń diagnostycznych Pokaż wyjątek z RunAsync:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-248">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Visual Studio 2015 zdarzeń diagnostycznych: niepowodzenie RunAsync w sieci szkieletowej: / HelloWorldStatefulApplication.][1]

<span data-ttu-id="5dfa6-250">Visual Studio 2015 zdarzeń diagnostycznych: niepowodzenie RunAsync w **fabric: / HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="5dfa6-251">Kolejka replikacji jest pełna</span><span class="sxs-lookup"><span data-stu-id="5dfa6-251">Replication queue full</span></span>
<span data-ttu-id="5dfa6-252">**System.Replicator** zgłosi ostrzeżenie, gdy kolejka replikacji jest pełna.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-252">**System.Replicator** reports a warning when the replication queue is full.</span></span> <span data-ttu-id="5dfa6-253">Na serwerze podstawowym kolejki replikacji zazwyczaj zapełni, ponieważ co najmniej jeden replikach pomocniczych są przetwarzane wolno potwierdzić operacji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-253">On the primary, replication queue usually becomes full because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="5dfa6-254">Na serwerze pomocniczym zwykle dzieje się tak, gdy usługa jest powolne zastosować operacji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-254">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="5dfa6-255">To ostrzeżenie zostanie wyczyszczona po kolejki nie jest już pełna.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-255">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="5dfa6-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="5dfa6-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="5dfa6-257">**Właściwość**: **PrimaryReplicationQueueStatus** lub **SecondaryReplicationQueueStatus**w zależności od roli repliki</span><span class="sxs-lookup"><span data-stu-id="5dfa6-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="5dfa6-258">Powolne operacje nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="5dfa6-258">Slow Naming operations</span></span>
<span data-ttu-id="5dfa6-259">**System.NamingService** raportów kondycji na jego repliką podstawową, gdy operacja nazewnictwa trwa dłużej niż dopuszczalne.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="5dfa6-260">Przykłady operacji nazewnictwa [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) lub [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="5dfa6-261">Więcej metod można znaleźć w obszarze klienta fabricclient z rolą, na przykład w obszarze [usługi metod zarządzania](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) lub [metod zarządzania właściwości](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="5dfa6-262">Usługa nazewnictwa rozpoznawania nazw usługi do lokalizacji w klastrze i umożliwia użytkownikom zarządzanie nazwy usługi i właściwości.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-262">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="5dfa6-263">Jest to sieć szkieletowa usług na partycje utrwalone usługi.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="5dfa6-264">Reprezentuje jedną z partycji Authority Owner zawierający metadane dotyczące wszystkich nazw usługi Service Fabric i usług.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-264">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="5dfa6-265">Nazwy sieci szkieletowej usług są mapowane do różnych partycji o nazwie właściciela partycji, dlatego usługa jest rozszerzalny.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-265">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="5dfa6-266">Przeczytaj więcej na temat [Naming service](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="5dfa6-267">Podczas operacji nazewnictwa trwa dłużej, niż oczekiwano, operacja oflagowane z raportem ostrzeżenie na *repliki podstawowej partycji usługi nazewnictwa, która służy operacji*.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-267">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="5dfa6-268">Jeśli operacja zakończy się pomyślnie, ostrzeżenie jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-268">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="5dfa6-269">Po zakończeniu operacji z powodu błędu, raport o kondycji zawiera szczegóły dotyczące błędu.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-269">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="5dfa6-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="5dfa6-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="5dfa6-271">**Właściwość**: rozpoczyna się od prefiksu **Duration_** i identyfikuje wolne działanie i nazwa sieci szkieletowej usług, dla którego jest stosowana operacji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-271">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="5dfa6-272">Na przykład jeśli Tworzenie usługi w sieci szkieletowej name: / MyApp/Moja_usługa trwa zbyt długo, ta właściwość jest Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-272">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="5dfa6-273">AO wskazuje rolą partycji nazewnictwa dla tej nazwy i operację.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-273">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="5dfa6-274">**Następne kroki**: Sprawdź, dlaczego nazewnictwa kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-274">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="5dfa6-275">Każda operacja mogą mieć różnych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-275">Each operation can have different root causes.</span></span> <span data-ttu-id="5dfa6-276">Na przykład usunąć usługi mogą zostać zatrzymane w węźle, ponieważ host aplikacji przechowuje awarii w węźle z powodu błędu użytkownika w kodzie usługi.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-276">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="5dfa6-277">Poniższy przykład przedstawia tworzenie operacji usługi.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-277">The following example shows a create service operation.</span></span> <span data-ttu-id="5dfa6-278">Operacja trwało dłużej niż skonfigurowany czas trwania.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-278">The operation took longer than the configured duration.</span></span> <span data-ttu-id="5dfa6-279">AO ponawia próbę i wysyła pracy na nie.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-279">AO retries and sends work to NO.</span></span> <span data-ttu-id="5dfa6-280">NIE ukończono z limitem czasu ostatniej operacji.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-280">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="5dfa6-281">W takim przypadku samej repliki jest kluczem podstawowym AO i żadnych ról.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-281">In this case, the same replica is primary for both the AO and NO roles.</span></span>

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
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="5dfa6-282">DeployedApplication systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="5dfa6-283">**System.Hosting** urzędu na wdrożonym jednostek.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-283">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="5dfa6-284">aktywacji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-284">Activation</span></span>
<span data-ttu-id="5dfa6-285">System.Hosting raportów, jako OK gdy aplikacji został pomyślnie uaktywniony na węźle.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-285">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="5dfa6-286">W przeciwnym razie go zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="5dfa6-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5dfa6-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5dfa6-288">**Właściwość**: aktywacji, łącznie z wersją wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5dfa6-288">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="5dfa6-289">**Następne kroki**: Jeśli aplikacja jest zła, zbadać, dlaczego aktywacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-289">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="5dfa6-290">W poniższym przykładzie przedstawiono pomyślnej aktywacji:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-290">The following example shows successful activation:</span></span>

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
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="5dfa6-291">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="5dfa6-291">Download</span></span>
<span data-ttu-id="5dfa6-292">**System.Hosting** zgłasza błąd, jeśli pobieranie pakietu aplikacji nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-292">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="5dfa6-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5dfa6-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5dfa6-294">**Właściwość**:  **pobrać:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="5dfa6-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="5dfa6-295">**Następne kroki**: Sprawdź, dlaczego pobieranie nie powiodło się w węźle.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-295">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="5dfa6-296">DeployedServicePackage systemowych raportów kondycji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="5dfa6-297">**System.Hosting** urzędu na wdrożonym jednostek.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-297">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="5dfa6-298">Aktywowanie pakietu usługi</span><span class="sxs-lookup"><span data-stu-id="5dfa6-298">Service package activation</span></span>
<span data-ttu-id="5dfa6-299">System.Hosting raporty jako OK, jeżeli usługa aktywacji pakietu w węźle zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-299">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="5dfa6-300">W przeciwnym razie go zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="5dfa6-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5dfa6-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5dfa6-302">**Właściwość**: aktywacji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-302">**Property**: Activation</span></span>
* <span data-ttu-id="5dfa6-303">**Następne kroki**: Sprawdź, dlaczego aktywacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-303">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="5dfa6-304">Aktywowanie pakietu kodu</span><span class="sxs-lookup"><span data-stu-id="5dfa6-304">Code package activation</span></span>
<span data-ttu-id="5dfa6-305">**System.Hosting** raporty jako OK dla każdego pakietu kodu, jeśli aktywacja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-305">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="5dfa6-306">W przypadku niepowodzenia aktywacji zgłosi ostrzeżenie zgodnie z konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-306">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="5dfa6-307">Jeśli **elementu CodePackage** nie może aktywować lub kończy się z powodu błędu większy niż skonfigurowany **CodePackageHealthErrorThreshold**, hosting zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-307">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="5dfa6-308">Jeśli pakiet usługi zawiera wiele pakietów kodu, aktywacji raport jest generowany dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="5dfa6-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5dfa6-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5dfa6-310">**Właściwość**: używa prefiksu **CodePackageActivation** i zawiera nazwę pakietu kodu i punktu wejścia jako  **CodePackageActivation:*CodePackageName* :*SetupEntryPoint/EntryPoint*** (na przykład **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="5dfa6-310">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="5dfa6-311">Rejestracja typu usługi</span><span class="sxs-lookup"><span data-stu-id="5dfa6-311">Service type registration</span></span>
<span data-ttu-id="5dfa6-312">**System.Hosting** zgłasza jako OK, jeśli typ usługi został pomyślnie zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-312">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="5dfa6-313">Zgłasza błąd, jeśli rejestracja nie została wykonana w czasie (zgodnie z konfiguracją przy użyciu **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-313">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="5dfa6-314">Jeśli środowisko uruchomieniowe jest zamknięty, typ usługi jest zarejestrowany z węzła i hostingu zgłosi ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-314">If the runtime is closed, the service type is unregistered from the node and Hosting reports a warning.</span></span>

* <span data-ttu-id="5dfa6-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5dfa6-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5dfa6-316">**Właściwość**: używa prefiksu **ServiceTypeRegistration** i zawiera nazwę typu usługi (na przykład **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="5dfa6-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="5dfa6-317">W poniższym przykładzie przedstawiono pakietu wdrożonej usługi w dobrej kondycji:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-317">The following example shows a healthy deployed service package:</span></span>

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
                             Description           : The ServicePackage was activated successfully.
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
                             Description           : The CodePackage was activated successfully.
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
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="5dfa6-318">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="5dfa6-318">Download</span></span>
<span data-ttu-id="5dfa6-319">**System.Hosting** zgłasza błąd, jeśli pobieranie pakietu usługi nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="5dfa6-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5dfa6-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5dfa6-321">**Właściwość**:  **pobrać:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="5dfa6-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="5dfa6-322">**Następne kroki**: Sprawdź, dlaczego pobieranie nie powiodło się w węźle.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="5dfa6-323">Weryfikacja uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="5dfa6-323">Upgrade validation</span></span>
<span data-ttu-id="5dfa6-324">**System.Hosting** zgłasza błąd w przypadku niepowodzenia weryfikacji podczas uaktualniania lub Jeśli uaktualnienie nie powiedzie się w węźle.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="5dfa6-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="5dfa6-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="5dfa6-326">**Właściwość**: używa prefiksu **FabricUpgradeValidation** i zawiera uaktualniania wersji</span><span class="sxs-lookup"><span data-stu-id="5dfa6-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="5dfa6-327">**Opis elementu**: wskazuje wystąpił błąd</span><span class="sxs-lookup"><span data-stu-id="5dfa6-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dfa6-328">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5dfa6-328">Next steps</span></span>
[<span data-ttu-id="5dfa6-329">Wyświetl raporty dotyczące kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="5dfa6-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="5dfa6-330">Jak zgłosić i Sprawdź kondycję usług</span><span class="sxs-lookup"><span data-stu-id="5dfa6-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="5dfa6-331">Monitorowanie i diagnozowania usług lokalnie</span><span class="sxs-lookup"><span data-stu-id="5dfa6-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="5dfa6-332">Uaktualnianie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="5dfa6-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

