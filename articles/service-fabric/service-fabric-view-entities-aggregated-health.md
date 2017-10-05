---
title: "Jak wyświetlić jednostki sieci szkieletowej usług Azure zagregowane kondycji | Dokumentacja firmy Microsoft"
description: "Opisuje sposób zapytania, widoków i oceniania kondycji zagregowane jednostki sieci szkieletowej usług Azure, za pomocą zapytań o kondycję i ogólne zapytania."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: b97972b1bdc28a17fb9c3a0e997738f5bd0b5d15
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="4dfb6-103">Wyświetl raporty dotyczące kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="4dfb6-103">View Service Fabric health reports</span></span>
<span data-ttu-id="4dfb6-104">Sieć szkieletowa usług Azure wprowadza [model kondycji](service-fabric-health-introduction.md) z jednostek kondycji, na którym składników systemu i watchdogs można raportu lokalnego warunki, które są monitorowania.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="4dfb6-105">[Magazynu kondycji](service-fabric-health-introduction.md#health-store) agreguje wszystkie dane kondycji, aby określić, czy jednostki są w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="4dfb6-106">Klaster jest automatycznie wypełniana raportów o kondycji wysyłane przez składniki systemu.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-106">The cluster is automatically populated with health reports sent by the system components.</span></span> <span data-ttu-id="4dfb6-107">Dowiedz się więcej o [użyć raportów o kondycji systemu w celu rozwiązania](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="4dfb6-108">Sieć szkieletowa usług zawiera wiele sposobów uzyskania zagregowane kondycji jednostek:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="4dfb6-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) lub innych narzędzi wizualizacji</span><span class="sxs-lookup"><span data-stu-id="4dfb6-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="4dfb6-110">Zapytań o kondycję (za pośrednictwem programu PowerShell, interfejsu API lub REST)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="4dfb6-111">Ogólne zapytania to zwracany listę obiektów, które mają kondycji jako jedna z właściwości (przy użyciu programu PowerShell, interfejsu API lub REST)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="4dfb6-112">Aby zademonstrować tych opcji, Użyjmy lokalny klaster z pięcioma węzłami i [fabric: / WordCount aplikacji](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="4dfb6-113">**Fabric: / WordCount** aplikacji zawiera dwie domyślne usługi, usługi stanowej typu `WordCountServiceType`i usługi bezstanowej typu `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="4dfb6-114">Po zmianie `ApplicationManifest.xml` wymagające siedem target replik dla usługi stanowej i jedną partycję.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span></span> <span data-ttu-id="4dfb6-115">Ponieważ istnieje tylko pięć węzłów w klastrze, składniki systemu raport ostrzeżenie na partycji usługi, ponieważ jest on poniżej docelowa liczba.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="4dfb6-116">Kondycji w narzędziu Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="4dfb6-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="4dfb6-117">Service Fabric Explorer oferuje czytelny klastra.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-117">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="4dfb6-118">Na poniższej ilustracji można stwierdzić, że:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-118">In the image below, you can see that:</span></span>

* <span data-ttu-id="4dfb6-119">Aplikacja **fabric: / WordCount** jest czerwony (w wyniku błędu), ponieważ ma ona zdarzenie błędu zgłoszony przez **MyWatchdog** dla właściwości **dostępności**.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="4dfb6-120">Jedna z jego usług **fabric: / WordCount/usługi WordCountService** jest żółty (w ostrzeżenie).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="4dfb6-121">Usługa jest skonfigurowana z replikami siedem i klastra ma pięć węzłów, więc nie może zostać umieszczona repicas dwa.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="4dfb6-122">Wprawdzie nie pokazano poniżej, partycji usługi jest żółty, ze względu na raport dotyczący systemu z `System.FM` informacją, że `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="4dfb6-123">Żółty partycji wyzwala żółty usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-123">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="4dfb6-124">Z powodu red aplikacji jest czerwony klastra.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-124">The cluster is red because of the red application.</span></span>

<span data-ttu-id="4dfb6-125">Obliczanie korzysta z domyślnych zasad z manifestu klastra i manifest aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-125">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="4dfb6-126">Są ścisłe zasady i nieodpowiednie jakiekolwiek niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="4dfb6-127">Widok klastra Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-127">View of the cluster with Service Fabric Explorer:</span></span>

![Widok klastra z Eksploratora usługi sieć szkieletowa.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="4dfb6-129">Przeczytaj więcej na temat [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="4dfb6-130">Zapytań o kondycję</span><span class="sxs-lookup"><span data-stu-id="4dfb6-130">Health queries</span></span>
<span data-ttu-id="4dfb6-131">Usługa sieci szkieletowej udostępnia zapytań o kondycję dla każdej z obsługiwanych [typów jednostek](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="4dfb6-132">Są one dostępne za pośrednictwem interfejsu API, przy użyciu metod na [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), poleceń cmdlet programu PowerShell i REST.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="4dfb6-133">Te zapytania zwraca pełną kondycję informacje o jednostce: stan kondycji zagregowane, zdarzenia kondycji jednostki, stanów kondycji podrzędnych (jeśli jest to wymagane), zła ocen (jeśli jednostki nie jest w dobrej kondycji) i statystyki kondycji elementy podrzędne (gdy ma zastosowanie).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="4dfb6-134">Jednostki kondycji jest zwracany, gdy pełni znajduje się w magazynie kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-134">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="4dfb6-135">Obiekt musi być aktywne (nie usunięte) i ma raportu system.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-135">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="4dfb6-136">Jej nadrzędnej jednostki w łańcuchu hierarchii musi mieć również raporty systemu.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-136">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="4dfb6-137">Jeśli te warunki nie są spełnione, kondycję kwerendy powrotu [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) z [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` który pokazuje, dlaczego nie są zwracane jednostki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="4dfb6-138">Zapytań o kondycję musi upłynąć w identyfikator jednostki, który jest zależny od typu jednostki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-138">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="4dfb6-139">Zapytania zaakceptować kondycji opcjonalne parametry zasad.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-139">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="4dfb6-140">Jeśli nie określono żadnych zasad dotyczących kondycji, [zasady dotyczące kondycji](service-fabric-health-introduction.md#health-policies) w manifeście klastra lub aplikacji są używane do oceny.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="4dfb6-141">Jeśli manifesty nie zawiera definicji dla zasad dotyczących kondycji, domyślne zasady dotyczące kondycji służą do oceny.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span></span> <span data-ttu-id="4dfb6-142">Domyślne zasady dotyczące kondycji nieodpowiednie zakończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-142">The default health policies do not tolerate any failures.</span></span> <span data-ttu-id="4dfb6-143">Zapytania także zaakceptować filtry dla zwracania tylko częściowe elementy podrzędne lub zdarzenia — te, które przestrzegać określonych filtrów.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span> <span data-ttu-id="4dfb6-144">Inny filtr zezwala, z wyłączeniem statystyki elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-144">Another filter allows excluding the children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="4dfb6-145">Filtry wyjściowe są stosowane po stronie serwera, zmniejsza rozmiar komunikatu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-145">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="4dfb6-146">Zaleca się, że możesz użyć filtrów danych wyjściowych, aby ograniczyć dane zwrócone, zamiast zastosować filtry po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="4dfb6-147">Prawidłowość jednostki zawiera:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-147">An entity's health contains:</span></span>

* <span data-ttu-id="4dfb6-148">Stan kondycji zagregowane jednostki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-148">The aggregated health state of the entity.</span></span> <span data-ttu-id="4dfb6-149">Obliczone przez magazynu kondycji na podstawie raportów o kondycji jednostki, stanów kondycji podrzędnych (jeśli jest to wymagane) i zasad dotyczących kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="4dfb6-150">Przeczytaj więcej na temat [oceny kondycji jednostki](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="4dfb6-151">Zdarzenia kondycji jednostki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-151">The health events on the entity.</span></span>
* <span data-ttu-id="4dfb6-152">Kolekcja stanów kondycji wszystkich elementów podrzędnych dla jednostek, które mogą mieć elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-152">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="4dfb6-153">Stany kondycji zawiera identyfikatorów jednostki i stan kondycji zagregowanych.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-153">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="4dfb6-154">Aby uzyskać pełną kondycję dziecka, wywołaj kondycji zapytania dla typu obiektu podrzędnego i podaj identyfikator podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="4dfb6-155">Zła oceny wskazujące do raportu, która wyzwoliła stanu jednostki, jeśli obiekt nie jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span> <span data-ttu-id="4dfb6-156">Oceny są cykliczne zawierające oceny kondycji elementy podrzędne, które wywołały bieżącego stanu kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span></span> <span data-ttu-id="4dfb6-157">Na przykład programu alarmowego zgłosił błąd przed repliki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="4dfb6-158">Kondycja aplikacji zawiera ocenę niezdrowy z powodu złej kondycji usługi; Usługa jest niezdrowe, ponieważ partycja w błąd; partycja jest niezdrowe, ponieważ replika błąd; Replika jest niezdrowe, ponieważ raport o kondycji programu alarmowego błędu.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span></span>
* <span data-ttu-id="4dfb6-159">Statystyki kondycji dla wszystkich elementów podrzędnych typów obiektów, które mają elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-159">The health statistics for all children types of the entities that have children.</span></span> <span data-ttu-id="4dfb6-160">Na przykład stan klastra jest wyświetlana łączna liczba aplikacji, usług, partycji i replik i wdrażane jednostek w klastrze.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span></span> <span data-ttu-id="4dfb6-161">Kondycja usługi zawiera całkowitą liczbę partycji i replik w obszarze określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-161">Service health shows the total number of partitions and replicas under the specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="4dfb6-162">Pobierz stan klastra</span><span class="sxs-lookup"><span data-stu-id="4dfb6-162">Get cluster health</span></span>
<span data-ttu-id="4dfb6-163">Zwraca kondycji jednostki klastra i zawiera stanów kondycji aplikacji i węzły (elementy podrzędne klastra).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="4dfb6-164">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-164">Input:</span></span>

* <span data-ttu-id="4dfb6-165">[Opcjonalnie] Zasad dotyczących kondycji klastra używane do analizowania węzły i zdarzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="4dfb6-166">[Opcjonalnie] Aplikacja kondycji zasad mapy, zasady dotyczące kondycji służy do zastępowania zasad manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="4dfb6-167">[Opcjonalnie] Filtry dla zdarzeń, węzły i aplikacje, które określają zapisy, które są interesujące i powinny być zwracane w wynikach (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4dfb6-168">Wszystkie zdarzenia, węzły i aplikacje są używane do oceny kondycji jednostki zagregowane, niezależnie od tego filtru.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="4dfb6-169">[Opcjonalnie] Filtr, aby wykluczyć statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-169">[Optional] Filter to exclude health statistics.</span></span>
* <span data-ttu-id="4dfb6-170">[Opcjonalnie] Filtr w celu uwzględnienia fabric: / statystyki kondycji systemu w statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span></span> <span data-ttu-id="4dfb6-171">Dotyczy tylko gdy statystyki kondycji nie są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-171">Only applicable when the health statistics are not excluded.</span></span> <span data-ttu-id="4dfb6-172">Domyślnie statystyki kondycji zawierają tylko statystyki dla użytkownika aplikacji i nie aplikacji systemowej.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-172">By default, the health statistics include only statistics for user applications and not the System application.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-173">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-173">API</span></span>
<span data-ttu-id="4dfb6-174">Aby uzyskać stan klastra, Utwórz `FabricClient` i Wywołaj [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) metody na jego **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="4dfb6-175">Następujące wywołanie pobiera stan klastra:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-175">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="4dfb6-176">Poniższy kod pobiera stan klastra przy użyciu zasad kondycji niestandardowych klastra i filtry dla węzłów i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="4dfb6-177">Określa, że statystyki kondycji obejmuje sieci szkieletowej: / statystyk systemu.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-177">It specifies that the health statistics include the fabric:/System statistics.</span></span> <span data-ttu-id="4dfb6-178">Tworzy [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), który zawiera informacje wejściowe.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-179">PowerShell</span></span>
<span data-ttu-id="4dfb6-180">Polecenie cmdlet, aby pobrać stan klastra jest [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="4dfb6-181">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="4dfb6-182">Stan klastra jest pięć węzłów, aplikacja systemu i sieci szkieletowej: / WordCount skonfigurowane zgodnie z opisem.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="4dfb6-183">Następujące polecenie cmdlet pobiera stan klastra za pomocą domyślnych zasad kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-183">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="4dfb6-184">Ostrzeżenie zagregowane kondycji, ponieważ sieci szkieletowej: / WordCount aplikacja jest ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="4dfb6-185">Należy zwrócić uwagę, jak zła oceny zawierają szczegółowe informacje dotyczące warunków, które wywołały zagregowane kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="4dfb6-186">Następujące polecenie cmdlet programu PowerShell pobiera kondycji klastra za pomocą zasad niestandardowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="4dfb6-187">Filtruje wyniki można uzyskać tylko aplikacji i węzły w błąd lub ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-187">It filters results to get only applications and nodes in error or warning.</span></span> <span data-ttu-id="4dfb6-188">W związku z tym żadnych węzłów są zwracane, ponieważ są one wszystkich dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="4dfb6-189">Tylko fabric: / aplikacji WordCount szanuje filtru aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-189">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="4dfb6-190">Ponieważ zasady niestandardowe określa wziąć pod uwagę ostrzeżenia jako błędy sieci szkieletowej: / aplikacji WordCount, aplikacja jest oceniany, tak jak błąd, a więc klastra.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="4dfb6-191">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-191">REST</span></span>
<span data-ttu-id="4dfb6-192">Możesz uzyskać kondycji klastra z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="4dfb6-193">Pobierz węzeł kondycji</span><span class="sxs-lookup"><span data-stu-id="4dfb6-193">Get node health</span></span>
<span data-ttu-id="4dfb6-194">Zwraca kondycji jednostek node i zawiera zdarzenia kondycji zgłoszone w węźle.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-194">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="4dfb6-195">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-195">Input:</span></span>

* <span data-ttu-id="4dfb6-196">[Wymagane] Nazwa węzła, który identyfikuje węzeł.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-196">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="4dfb6-197">[Opcjonalnie] Ustawienia zasad kondycji klastra używane do oceny kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-197">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="4dfb6-198">[Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwracane w wynikach (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4dfb6-199">Wszystkie zdarzenia są używane do oceny kondycji jednostki zagregowane, niezależnie od tego filtru.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-200">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-200">API</span></span>
<span data-ttu-id="4dfb6-201">Aby uzyskać węzła kondycji za pomocą interfejsu API, Utwórz `FabricClient` i Wywołaj [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="4dfb6-202">Poniższy kod pobiera kondycji węzła nazwę określonego węzła:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-202">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="4dfb6-203">Poniższy kod pobiera kondycji węzła nazwę określonego węzła i przekazuje filtr zdarzeń i niestandardowych zasad za pośrednictwem [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="4dfb6-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-204">PowerShell</span></span>
<span data-ttu-id="4dfb6-205">To polecenie cmdlet, aby pobrać kondycji węzła [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="4dfb6-206">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="4dfb6-207">Następujące polecenie cmdlet pobiera kondycji węzłów za pomocą domyślnych zasad kondycji:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-207">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="4dfb6-208">Następujące polecenie cmdlet pobiera kondycję wszystkich węzłów w klastrze:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-208">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="4dfb6-209">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-209">REST</span></span>
<span data-ttu-id="4dfb6-210">Możesz uzyskać kondycji węzła z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="4dfb6-211">Pobierz kondycji aplikacji</span><span class="sxs-lookup"><span data-stu-id="4dfb6-211">Get application health</span></span>
<span data-ttu-id="4dfb6-212">Zwraca kondycji jednostki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-212">Returns the health of an application entity.</span></span> <span data-ttu-id="4dfb6-213">Zawiera ona stanów kondycji wdrożonej aplikacji i usług dzieci.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-213">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="4dfb6-214">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-214">Input:</span></span>

* <span data-ttu-id="4dfb6-215">[Wymagane] Nazwa aplikacji (URI), który identyfikuje aplikację.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-215">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="4dfb6-216">[Opcjonalnie] Zasady kondycji aplikacji służy do zastępowania zasad manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-216">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="4dfb6-217">[Opcjonalnie] Filtry dla zdarzeń, usług i wdrożone aplikacje, które określają zapisy, które są interesujące i powinny być zwracane w wynikach (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4dfb6-218">Wszystkie zdarzenia, usługi i wdrożone aplikacje są używane do oceny kondycji jednostki zagregowane, niezależnie od tego filtru.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="4dfb6-219">[Opcjonalnie] Filtr, aby wykluczyć statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-219">[Optional] Filter to exclude the health statistics.</span></span> <span data-ttu-id="4dfb6-220">Jeśli nie zostanie określony, statystyki kondycji obejmują ok, ostrzeżenia i liczby błędów dla wszystkich aplikacji elementów podrzędnych: usług, partycji, repliki, wdrożonych aplikacji i wdrożonych pakietów usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-221">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-221">API</span></span>
<span data-ttu-id="4dfb6-222">Aby uzyskać kondycji aplikacji, należy utworzyć `FabricClient` i Wywołaj [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="4dfb6-223">Poniższy kod pobiera kondycji aplikacji dla nazwy określonej aplikacji (URI):</span><span class="sxs-lookup"><span data-stu-id="4dfb6-223">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="4dfb6-224">Poniższy kod pobiera kondycji aplikacji dla nazwy określonej aplikacji (URI) z filtrami i niestandardowych zasad określona za pomocą [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-225">PowerShell</span></span>
<span data-ttu-id="4dfb6-226">To polecenie cmdlet, aby pobrać kondycji aplikacji [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="4dfb6-227">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="4dfb6-228">Następujące polecenie cmdlet zwraca kondycji **fabric: / WordCount** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="4dfb6-229">Przekazuje następującego polecenia cmdlet programu PowerShell w niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-229">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="4dfb6-230">Filtruje także elementów podrzędnych i zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="4dfb6-231">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-231">REST</span></span>
<span data-ttu-id="4dfb6-232">Możesz uzyskać kondycji aplikacji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="4dfb6-233">Pobierz usługi kondycji</span><span class="sxs-lookup"><span data-stu-id="4dfb6-233">Get service health</span></span>
<span data-ttu-id="4dfb6-234">Zwraca kondycji jednostki usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-234">Returns the health of a service entity.</span></span> <span data-ttu-id="4dfb6-235">Zawiera ona stanów kondycji partycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-235">It contains the partition health states.</span></span> <span data-ttu-id="4dfb6-236">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-236">Input:</span></span>

* <span data-ttu-id="4dfb6-237">[Wymagane] Nazwa usługi (URI), który identyfikuje usługę.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-237">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="4dfb6-238">[Opcjonalnie] Zasady kondycji aplikacji służy do zastępowania zasad manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-238">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="4dfb6-239">[Opcjonalnie] Filtry dla zdarzeń i partycje, które określają zapisy, które są interesujące i powinny być zwracane w wynikach (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4dfb6-240">Wszystkie zdarzenia i partycji są używane do oceny kondycji jednostki zagregowane, niezależnie od tego filtru.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="4dfb6-241">[Opcjonalnie] Filtr, aby wykluczyć statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-241">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="4dfb6-242">Jeśli nie jest określony, statystyki kondycji Pokaż ok, ostrzeżenie, i liczby błędów dla wszystkich partycji i replik usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-243">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-243">API</span></span>
<span data-ttu-id="4dfb6-244">Aby uzyskać kondycja usługi za pomocą interfejsu API, Utwórz `FabricClient` i Wywołaj [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="4dfb6-245">Poniższy przykład pobiera kondycji usługi o nazwie określonej usługi (URI):</span><span class="sxs-lookup"><span data-stu-id="4dfb6-245">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="4dfb6-246">Poniższy kod pobiera kondycja usługi dla określonej nazwy usługi (URI), filtrów i zasad niestandardowych za pomocą [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="4dfb6-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-247">PowerShell</span></span>
<span data-ttu-id="4dfb6-248">To polecenie cmdlet, aby pobrać kondycja usługi [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="4dfb6-249">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="4dfb6-250">Następujące polecenie cmdlet pobiera kondycja usługi za pomocą domyślnych zasad kondycji:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-250">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="4dfb6-251">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-251">REST</span></span>
<span data-ttu-id="4dfb6-252">Można pobrać usługi kondycji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="4dfb6-253">Pobierz kondycji partycji</span><span class="sxs-lookup"><span data-stu-id="4dfb6-253">Get partition health</span></span>
<span data-ttu-id="4dfb6-254">Zwraca kondycji jednostki partycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-254">Returns the health of a partition entity.</span></span> <span data-ttu-id="4dfb6-255">Zawiera ona stanów kondycji repliki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-255">It contains the replica health states.</span></span> <span data-ttu-id="4dfb6-256">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-256">Input:</span></span>

* <span data-ttu-id="4dfb6-257">[Wymagane] Partycja identyfikator (GUID), który identyfikuje partycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-257">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="4dfb6-258">[Opcjonalnie] Zasady kondycji aplikacji służy do zastępowania zasad manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-258">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="4dfb6-259">[Opcjonalnie] Filtry dla zdarzeń i replik, które określają zapisy, które są interesujące i powinny być zwracane w wynikach (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4dfb6-260">Wszystkie zdarzenia i repliki są używane do oceny kondycji jednostki zagregowane, niezależnie od tego filtru.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="4dfb6-261">[Opcjonalnie] Filtr, aby wykluczyć statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-261">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="4dfb6-262">Jeśli nie zostanie określony, statystyki kondycji pokazują, jak wiele repliki są w ok, ostrzeżenia i błędu stanów.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-263">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-263">API</span></span>
<span data-ttu-id="4dfb6-264">Aby uzyskać partycji kondycji za pomocą interfejsu API, Utwórz `FabricClient` i Wywołaj [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="4dfb6-265">Aby określić następujące parametry opcjonalne, utworzyć [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-266">PowerShell</span></span>
<span data-ttu-id="4dfb6-267">To polecenie cmdlet, aby pobrać kondycji partycji [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="4dfb6-268">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="4dfb6-269">Następujące polecenie cmdlet pobiera kondycji dla wszystkich partycji **fabric: / WordCount/usługi WordCountService** usługi i odfiltrowuje repliki stanów kondycji:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
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
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="4dfb6-270">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-270">REST</span></span>
<span data-ttu-id="4dfb6-271">Możesz uzyskać kondycji partycji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="4dfb6-272">Pobierz kondycji repliki</span><span class="sxs-lookup"><span data-stu-id="4dfb6-272">Get replica health</span></span>
<span data-ttu-id="4dfb6-273">Zwraca kondycji repliki usługi stanowej lub wystąpienie usługi bezstanowej.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-273">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="4dfb6-274">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-274">Input:</span></span>

* <span data-ttu-id="4dfb6-275">[Wymagane] Identyfikator (GUID) i repliki Identyfikatora partycji identyfikujący repliki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="4dfb6-276">[Opcjonalnie] Parametry zasady kondycji aplikacji służy do zastępowania zasad manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-276">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="4dfb6-277">[Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwracane w wynikach (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4dfb6-278">Wszystkie zdarzenia są używane do oceny kondycji jednostki zagregowane, niezależnie od tego filtru.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-279">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-279">API</span></span>
<span data-ttu-id="4dfb6-280">Aby uzyskać kondycji repliki za pomocą interfejsu API, Utwórz `FabricClient` i Wywołaj [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="4dfb6-281">Aby określić parametry zaawansowane, użyj [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-282">PowerShell</span></span>
<span data-ttu-id="4dfb6-283">To polecenie cmdlet, aby pobrać kondycji repliki [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="4dfb6-284">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="4dfb6-285">Następujące polecenie cmdlet pobiera kondycji repliką podstawową dla wszystkich partycji usługi:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="4dfb6-286">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-286">REST</span></span>
<span data-ttu-id="4dfb6-287">Możesz uzyskać kondycji repliki z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="4dfb6-288">Pobierz kondycji wdrożonej aplikacji</span><span class="sxs-lookup"><span data-stu-id="4dfb6-288">Get deployed application health</span></span>
<span data-ttu-id="4dfb6-289">Zwraca kondycji aplikacji wdrożone w ramach jednostki węzła.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-289">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="4dfb6-290">Zawiera ona stanów kondycji pakietu wdrożonej usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-290">It contains the deployed service package health states.</span></span> <span data-ttu-id="4dfb6-291">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-291">Input:</span></span>

* <span data-ttu-id="4dfb6-292">[Wymagane] Nazwa aplikacji (URI) i nazwę węzła (ciąg) identyfikujących wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="4dfb6-293">[Opcjonalnie] Zasady kondycji aplikacji służy do zastępowania zasad manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-293">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="4dfb6-294">[Opcjonalnie] Filtry dla zdarzeń i wdrożone pakiety usługi określające zapisy, które są interesujące i powinny być zwracane w wynikach (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4dfb6-295">Wszystkie zdarzenia i wdrożone pakiety usługi są używane do oceny kondycji jednostki zagregowane, niezależnie od tego filtru.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="4dfb6-296">[Opcjonalnie] Filtr, aby wykluczyć statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-296">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="4dfb6-297">Jeśli nie zostanie określony, statystyki kondycji Pokaż liczbę wdrożone pakiety usługi ok, ostrzeżenia i błędu stany kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-298">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-298">API</span></span>
<span data-ttu-id="4dfb6-299">Aby uzyskać kondycję aplikacji wdrożonych na węźle, za pośrednictwem interfejsu API, Utwórz `FabricClient` i Wywołaj [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="4dfb6-300">Aby określić następujące parametry opcjonalne, użyj [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-301">PowerShell</span></span>
<span data-ttu-id="4dfb6-302">To polecenie cmdlet, aby pobrać kondycji wdrożonej aplikacji [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="4dfb6-303">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="4dfb6-304">Aby dowiedzieć się, gdy aplikacja jest wdrażana, uruchom [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) i przyjrzyj się dzieci wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span></span>

<span data-ttu-id="4dfb6-305">Następujące polecenie cmdlet pobiera kondycji **fabric: / WordCount** aplikacji wdrożonych na **to węzeł _Node_2**.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="4dfb6-306">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-306">REST</span></span>
<span data-ttu-id="4dfb6-307">Możesz uzyskać kondycji wdrożonej aplikacji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="4dfb6-308">Pobierz kondycji pakietu wdrożonej usługi</span><span class="sxs-lookup"><span data-stu-id="4dfb6-308">Get deployed service package health</span></span>
<span data-ttu-id="4dfb6-309">Zwraca kondycji jednostki pakietu wdrożonej usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-309">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="4dfb6-310">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-310">Input:</span></span>

* <span data-ttu-id="4dfb6-311">[Wymagane] Nazwa aplikacji (URI), nazwę węzła (ciąg) i nazwa manifestu usługi (ciąg) identyfikujących pakietu wdrożonej usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="4dfb6-312">[Opcjonalnie] Zasady kondycji aplikacji służy do zastępowania zasad manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-312">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="4dfb6-313">[Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwracane w wynikach (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="4dfb6-314">Wszystkie zdarzenia są używane do oceny kondycji jednostki zagregowane, niezależnie od tego filtru.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-315">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-315">API</span></span>
<span data-ttu-id="4dfb6-316">Aby uzyskać kondycji pakietu wdrożonej usługi za pomocą interfejsu API, Utwórz `FabricClient` i Wywołaj [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="4dfb6-317">Aby określić następujące parametry opcjonalne, użyj [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-318">PowerShell</span></span>
<span data-ttu-id="4dfb6-319">Polecenie cmdlet, aby pobrać pakiet wdrożonej usługi kondycji jest [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="4dfb6-320">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="4dfb6-321">Aby sprawdzić, gdy aplikacja jest wdrażana, uruchom [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) i przyjrzyj się wdrożone aplikacje.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span></span> <span data-ttu-id="4dfb6-322">Aby wyświetlić usługi, które pakiety znajdują się w aplikacji, obejrzyj dzieci pakietu wdrożonej usługi w [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="4dfb6-323">Następujące polecenie cmdlet pobiera kondycji **WordCountServicePkg** pakiet usługi **fabric: / WordCount** aplikacji wdrożonych na **to węzeł _Node_2**.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="4dfb6-324">Jednostka ma **System.Hosting** raporty dla pomyślnej aktywacji w pakiecie usługi i punktu wejścia i pomyślną rejestrację typu usługi.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="4dfb6-325">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-325">REST</span></span>
<span data-ttu-id="4dfb6-326">Możesz uzyskać wdrożonej usługi kondycji pakietu z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="4dfb6-327">Fragmentu zapytań o kondycję</span><span class="sxs-lookup"><span data-stu-id="4dfb6-327">Health chunk queries</span></span>
<span data-ttu-id="4dfb6-328">Zapytania fragmentu kondycji mogą zwracać elementy podrzędne (rekursywnie), wielopoziomowe klastra na filtry.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="4dfb6-329">Obsługuje ona filtrów zaawansowanych, które umożliwiają dużą elastyczność w wyborze dzieci, który ma zostać zwrócona.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span></span> <span data-ttu-id="4dfb6-330">Filtry można określić elementy podrzędne, za pomocą unikatowego identyfikatora lub przez inne grupy identyfikatorów i/lub stanów kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="4dfb6-331">Domyślnie bez żadnych elementów podrzędnych są uwzględnione, zamiast polecenia kondycji, które zawsze należy uwzględniać pierwszego poziomu elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-331">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="4dfb6-332">[Zapytań o kondycję](service-fabric-view-entities-aggregated-health.md#health-queries) zwracać tylko pierwszy poziom dzieci określonej jednostki na wymagane filtrów.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="4dfb6-333">Można uzyskać elementów podrzędnych elementu podrzędnego, należy wywołać kondycji dodatkowe interfejsy API dla każdej jednostki zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="4dfb6-334">Podobnie Aby uzyskać kondycji konkretnych obiektów, należy wywołać kondycji jednego interfejsu API dla każdej żądanej jednostki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="4dfb6-335">Zapytanie fragmentu zaawansowane filtrowanie umożliwia zażądanie wielu elementy w jednym zapytaniu, minimalizując rozmiaru wiadomości i liczby wiadomości.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="4dfb6-336">Wartość zapytania fragmentu jest, że wyświetlić stan kondycji dla kolejnych jednostek klastra (potencjalnie wszystkich klastra jednostek zaczynając od wymaganego głównego) w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="4dfb6-337">Można wyrazić zapytania kondycji złożonych takich jak:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="4dfb6-338">Zwracany aplikacji tylko w błąd, a w przypadku aplikacji obejmują wszystkie usługi w ostrzeżenia lub błędu.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="4dfb6-339">W przypadku zwróconych usług zawiera wszystkie partycje.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="4dfb6-340">Zwróć tylko kondycję cztery aplikacji, określonych przez ich nazwy.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-340">Return only the health of four applications, specified by their names.</span></span>
* <span data-ttu-id="4dfb6-341">Zwróć tylko kondycję aplikacji typu żądanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-341">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="4dfb6-342">Zwraca wszystkie wdrożone jednostek w węźle.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="4dfb6-343">Zwraca wszystkie aplikacje, wszystkie wdrażane aplikacje na określony węzeł i wszystkie pakiety wdrożonej usługi na tym węźle.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="4dfb6-344">Zwróć wszystkie repliki na błąd.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-344">Return all replicas in error.</span></span> <span data-ttu-id="4dfb6-345">Zwraca wszystkich aplikacji, usług, partycji i replik tylko z błędami.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="4dfb6-346">Zwróć wszystkie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-346">Return all applications.</span></span> <span data-ttu-id="4dfb6-347">Dla określonej usługi należy wprowadzić wszystkie partycje.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="4dfb6-348">Obecnie fragmentu zapytania kondycji jest widoczne tylko dla obiektu klastra.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-348">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="4dfb6-349">Zwraca fragmentu kondycji klastra, który zawiera:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="4dfb6-350">Stan kondycji jest agregowana w klastrze.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-350">The cluster aggregated health state.</span></span>
* <span data-ttu-id="4dfb6-351">Lista fragmentu stanu kondycji węzłów, które przestrzegać filtry.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-351">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="4dfb6-352">Lista fragmentu stan kondycji aplikacji, których przestrzeganie filtry.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-352">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="4dfb6-353">Każdego fragmentu stan kondycji aplikacji znajduje się lista fragmentu ze wszystkich usług, których przestrzeganie filtry i listy fragmentu z wszystkich wdrożonych aplikacji, które przestrzegać filtrów.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="4dfb6-354">Wartość taka sama dla dzieci, usług i wdrożone aplikacje.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-354">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="4dfb6-355">Dzięki temu wszystkie jednostki w klastrze może być potencjalnie zwracany żądanie w hierarchiczny sposób.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="4dfb6-356">Klaster kondycji fragmentu zapytania</span><span class="sxs-lookup"><span data-stu-id="4dfb6-356">Cluster health chunk query</span></span>
<span data-ttu-id="4dfb6-357">Zwraca kondycji jednostki klastra i zawiera fragmenty stan kondycji hierarchiczna wymagane elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="4dfb6-358">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-358">Input:</span></span>

* <span data-ttu-id="4dfb6-359">[Opcjonalnie] Zasad dotyczących kondycji klastra używane do analizowania węzły i zdarzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="4dfb6-360">[Opcjonalnie] Aplikacja kondycji zasad mapy, zasady dotyczące kondycji służy do zastępowania zasad manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="4dfb6-361">[Opcjonalnie] Filtry dla węzłów i aplikacje, które określają zapisy, które są interesujące i powinny być zwracane w wynikach.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="4dfb6-362">Filtry są specyficzne dla jednostki/grupy jednostek lub mają zastosowanie do wszystkich jednostek na tym poziomie.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="4dfb6-363">Lista filtrów może zawierać jeden filtr ogólne i/lub filtrów dla określonych identyfikatorów dla jednostek szczegółowe dzielenie zwróconych przez kwerendę.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="4dfb6-364">W przypadku braku domyślnie nie są zwracane elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-364">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="4dfb6-365">Przeczytaj więcej na temat filtrów w [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) i [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="4dfb6-366">Rekursywnie może filtrów aplikacji określ filtry zaawansowane podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-366">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="4dfb6-367">Wynik fragmentu zawiera elementy podrzędne, które przestrzegać filtrów.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-367">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="4dfb6-368">Obecnie zapytania fragmentu nie zwraca zła ocen lub zdarzeń jednostki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="4dfb6-369">Dodatkowe informacje można uzyskać przy użyciu istniejącego zapytania kondycji klastra.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-369">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="4dfb6-370">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="4dfb6-370">API</span></span>
<span data-ttu-id="4dfb6-371">Aby uzyskać fragmentu kondycji klastra, Utwórz `FabricClient` i Wywołaj [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) metody na jego **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="4dfb6-372">Można przekazać [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) do opisu zasady dotyczące kondycji i filtry zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="4dfb6-373">Poniższy kod pobiera fragmentu kondycji klastra z filtry zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-373">The following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except the ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="4dfb6-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfb6-374">PowerShell</span></span>
<span data-ttu-id="4dfb6-375">Polecenie cmdlet, aby pobrać stan klastra jest [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="4dfb6-376">Po pierwsze, połącz się z klastrem przy użyciu [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="4dfb6-377">Poniższy kod pobiera węzły tylko wtedy, gdy są one błąd z wyjątkiem określonego węzła zawsze ma zostać zwrócony.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="4dfb6-378">Następujące polecenie cmdlet pobiera fragmentu klastra z filtrami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-378">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="4dfb6-379">Następujące polecenie cmdlet zwraca wszystkie jednostki wdrożonej w węźle.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-379">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="4dfb6-380">REST</span><span class="sxs-lookup"><span data-stu-id="4dfb6-380">REST</span></span>
<span data-ttu-id="4dfb6-381">Możesz uzyskać fragment kondycji klastra z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) zawierającej zasady dotyczące kondycji i filtry zaawansowane opisanego w treści.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="4dfb6-382">Ogólne zapytań</span><span class="sxs-lookup"><span data-stu-id="4dfb6-382">General queries</span></span>
<span data-ttu-id="4dfb6-383">Ogólne kwerendy zwracają listę jednostki sieci szkieletowej usług określonego typu.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="4dfb6-384">Są one dostępne za pośrednictwem interfejsu API (za pomocą metod na **FabricClient.QueryManager**), polecenia cmdlet programu PowerShell i REST.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="4dfb6-385">Te zapytania agregować podzapytania z wielu składników.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="4dfb6-386">Jeden z nich jest [magazynu kondycji](service-fabric-health-introduction.md#health-store), który wypełnia stan kondycji zagregowane dla każdego wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="4dfb6-387">Ogólne zapytania zwracać zagregowane kondycja jednostki i nie zawierają danych sformatowanego kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="4dfb6-388">Jeśli jednostka nie jest w dobrej kondycji, można odpowiednio zareagować z zapytania kondycji, aby uzyskać wszystkie jego informacje kondycji, w tym zdarzenia, stanów kondycji podrzędnych i oceny złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="4dfb6-389">Jeśli ogólne kwerend zwraca nieznany kondycja jednostki, jest to możliwe, że magazynu kondycji nie ma pełnych danych o tej jednostce.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="4dfb6-390">Istnieje również możliwość, że podzapytania w magazynie kondycji nie powiodło się (na przykład wystąpił błąd komunikacji lub został ograniczony magazynu kondycji).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="4dfb6-391">Dostosuj się zapytania kondycji dla jednostki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-391">Follow up with a health query for the entity.</span></span> <span data-ttu-id="4dfb6-392">Jeśli podzapytanie napotkała błąd przejściowy, takie jak problemy z siecią, to zapytanie kolejnych może się powieść.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="4dfb6-393">Go może także zapewniają więcej szczegółowych informacji z magazynu kondycji o Dlaczego jednostki nie jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-393">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="4dfb6-394">Zapytania, które zawierają **HealthState** dla jednostki to:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-394">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="4dfb6-395">Listy węzłów: zwraca listy węzłów w klastrze (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-395">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="4dfb6-396">Interfejs API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="4dfb6-397">Środowiska PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="4dfb6-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="4dfb6-398">Lista aplikacji: zwraca listę aplikacji w klastrze (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-398">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="4dfb6-399">Interfejs API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="4dfb6-400">Środowiska PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="4dfb6-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="4dfb6-401">Lista usług: zwraca listę usług w aplikacji (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-401">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="4dfb6-402">Interfejs API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="4dfb6-403">Środowiska PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="4dfb6-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="4dfb6-404">Lista partycji: zwraca listę partycji w usłudze (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-404">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="4dfb6-405">Interfejs API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="4dfb6-406">Środowiska PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="4dfb6-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="4dfb6-407">Listy replik: zwraca listę replik partycji (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-407">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="4dfb6-408">Interfejs API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="4dfb6-409">Środowiska PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="4dfb6-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="4dfb6-410">Wdrożone listy aplikacji: zwraca listę wdrożonych aplikacji w węźle.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-410">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="4dfb6-411">Interfejs API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="4dfb6-412">Środowiska PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="4dfb6-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="4dfb6-413">Wdrożone usługi listy pakietów: zwraca listę pakietów usług we wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-413">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="4dfb6-414">Interfejs API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="4dfb6-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="4dfb6-415">Środowiska PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="4dfb6-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="4dfb6-416">Niektóre z zapytań Zwróć wyników stronicowania.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-416">Some of the queries return paged results.</span></span> <span data-ttu-id="4dfb6-417">Powrót z tych kwerend znajduje się lista pochodzące z [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="4dfb6-418">Jeśli wyniki nie pasują do wiadomości, jest zwracana tylko stronę i ContinuationToken śledzi gdzie wyliczenie zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="4dfb6-419">Nadal wywołanie tej samej kwerendy i przekaż token kontynuacji z poprzedniej kwerendy, aby uzyskać wyniki dalej.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="4dfb6-420">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4dfb6-420">Examples</span></span>
<span data-ttu-id="4dfb6-421">Poniższy kod pobiera złej kondycji aplikacji w klastrze:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-421">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="4dfb6-422">Następujące polecenie cmdlet pobiera szczegółów aplikacji w sieci szkieletowej: / WordCount aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="4dfb6-423">Należy zauważyć, że stan kondycji jest ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="4dfb6-424">Następujące polecenie cmdlet pobiera usług o stanie kondycji błędu:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-424">The following cmdlet gets the services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="4dfb6-425">Uaktualnienia klastra i aplikacji</span><span class="sxs-lookup"><span data-stu-id="4dfb6-425">Cluster and application upgrades</span></span>
<span data-ttu-id="4dfb6-426">Podczas uaktualniania monitorowanych klastra i aplikacji sieci szkieletowej usług umożliwia sprawdzenie kondycji, aby zapewnić wszystko działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="4dfb6-427">Jeśli jednostki jest nieprawidłowy, ponieważ oceniane przy użyciu zasad dotyczących kondycji skonfigurowanego, uaktualnienie ma zastosowanie zasad dla konkretnych uaktualnienia ustalenie następnej akcji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="4dfb6-428">Uaktualnienia może być wstrzymane. Aby zezwolić na interakcję użytkownika (na przykład poprawki błędów lub zmiany zasad) lub może automatycznie przywracać stanu sprzed dobrej poprzedniej wersji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="4dfb6-429">Podczas *klastra* uaktualnienia, możesz uzyskać stan uaktualnienia klastra.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="4dfb6-430">Stan uaktualnienia obejmuje ocen złej kondycji, które wskaż co to jest w złej kondycji w klastrze.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="4dfb6-431">Jeśli uaktualnianie zostanie wycofana z powodu problemów kondycji, stan uaktualnienia pamięta ostatniego przyczyny złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="4dfb6-432">Te informacje mogą pomóc Administratorzy zbadać, co poszło źle po uaktualnieniu z powrotem obniżyć lub zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="4dfb6-433">Podobnie podczas *aplikacji* uaktualnienia, wszelkie nieprawidłowości oceny są zawarte w stan uaktualnienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="4dfb6-434">Poniżej pokazano stanu uaktualniania aplikacji dla zmodyfikowanych sieci szkieletowej: / WordCount aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="4dfb6-435">Programu alarmowego zgłosił błąd na jednym z jego repliki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="4dfb6-436">Uaktualnianie jest stopniowych, ponieważ kontroli kondycji nie są przestrzegane.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-436">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="4dfb6-437">Przeczytaj więcej na temat [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="4dfb6-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="4dfb6-438">Rozwiązywanie problemów przy użyciu oceny kondycji</span><span class="sxs-lookup"><span data-stu-id="4dfb6-438">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="4dfb6-439">Zawsze, gdy występuje problem z klastra lub aplikacji, obejrzyj kondycji klastra lub aplikacji w celu określenia, co jest nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="4dfb6-440">Zła oceny zawierają szczegółowe informacje o co wyzwoliło bieżący stan złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="4dfb6-441">Jeśli zajdzie potrzeba, użytkownik może przejść do jednostek podrzędne o złej kondycji, aby zidentyfikować przyczynę.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

<span data-ttu-id="4dfb6-442">Rozważmy na przykład aplikacji nieprawidłowy, ponieważ raport o błędach na jednym z jego repliki.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="4dfb6-443">Następujące polecenie cmdlet programu Powershell pokazuje ocen złej kondycji:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-443">The following Powershell cmdlet shows the unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="4dfb6-444">Można przyjrzeć się replikę tak, aby uzyskać więcej informacji:</span><span class="sxs-lookup"><span data-stu-id="4dfb6-444">You can look at the replica to get more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="4dfb6-445">Zła ocen Pokaż pierwsze urząd jednostki jest obliczane do bieżącego stanu kondycji.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="4dfb6-446">Może istnieć wiele zdarzeń wyzwalających ten stan, ale są one nie zostać zawarte w oceny.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="4dfb6-447">Aby uzyskać więcej informacji, przejdź do szczegółów jednostki kondycji, aby poznać wszystkie raporty złej kondycji w klastrze.</span><span class="sxs-lookup"><span data-stu-id="4dfb6-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4dfb6-448">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4dfb6-448">Next steps</span></span>
[<span data-ttu-id="4dfb6-449">Używanie raportów kondycji systemu do rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="4dfb6-449">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="4dfb6-450">Dodawanie niestandardowych raportów kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="4dfb6-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="4dfb6-451">Jak zgłosić i Sprawdź kondycję usług</span><span class="sxs-lookup"><span data-stu-id="4dfb6-451">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="4dfb6-452">Monitorowanie i diagnozowania usług lokalnie</span><span class="sxs-lookup"><span data-stu-id="4dfb6-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="4dfb6-453">Uaktualnianie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="4dfb6-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
