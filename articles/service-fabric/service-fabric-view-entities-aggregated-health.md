---
title: "jednostek aaaHow tooview sieć szkieletowa usług Azure zagregowane kondycji | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooquery, wyświetlać i oceniania kondycji zagregowane jednostki sieci szkieletowej usług Azure, za pomocą zapytań o kondycję i ogólne zapytania."
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
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="32612-103">Wyświetl raporty dotyczące kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="32612-103">View Service Fabric health reports</span></span>
<span data-ttu-id="32612-104">Sieć szkieletowa usług Azure wprowadza [model kondycji](service-fabric-health-introduction.md) z jednostek kondycji, na którym składników systemu i watchdogs można raportu lokalnego warunki, które są monitorowania.</span><span class="sxs-lookup"><span data-stu-id="32612-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="32612-105">Witaj [magazynu kondycji](service-fabric-health-introduction.md#health-store) agreguje wszystkich toodetermine danych kondycji, czy jednostki są w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="32612-106">Witaj klastra jest automatycznie wypełniana wysyłane przez składniki systemu hello raportów o kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="32612-107">Dowiedz się więcej o [tootroubleshoot raportów kondycji systemu używany](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="32612-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="32612-108">Sieć szkieletowa usług zawiera wiele sposobów tooget hello zagregowane kondycji jednostek hello:</span><span class="sxs-lookup"><span data-stu-id="32612-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="32612-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) lub innych narzędzi wizualizacji</span><span class="sxs-lookup"><span data-stu-id="32612-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="32612-110">Zapytań o kondycję (za pośrednictwem programu PowerShell, interfejsu API lub REST)</span><span class="sxs-lookup"><span data-stu-id="32612-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="32612-111">Ogólne zapytania to zwracany listę obiektów, które mają kondycji jako jedna z właściwości hello (za pośrednictwem programu PowerShell, interfejsu API lub REST)</span><span class="sxs-lookup"><span data-stu-id="32612-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="32612-112">toodemonstrate korzystać z tych opcji, umożliwia używanie lokalnego klastra z pięciu węzłów i hello [sieci szkieletowej: / WordCount aplikacji](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="32612-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="32612-113">Hello **fabric: / WordCount** aplikacji zawiera dwie domyślne usługi, usługi stanowej typu `WordCountServiceType`i usługi bezstanowej typu `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="32612-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="32612-114">Po zmianie hello `ApplicationManifest.xml` toorequire siedmiu docelowej repliki usługi stanowej hello i jedną partycję.</span><span class="sxs-lookup"><span data-stu-id="32612-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="32612-115">Ponieważ istnieje tylko pięć węzłów w klastrze hello, hello składników systemu raport ostrzeżenie na hello partycji usługi, ponieważ jest on poniżej hello docelowa liczba.</span><span class="sxs-lookup"><span data-stu-id="32612-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

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

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="32612-116">Kondycji w narzędziu Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="32612-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="32612-117">Service Fabric Explorer zawiera czytelny hello klastra.</span><span class="sxs-lookup"><span data-stu-id="32612-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="32612-118">Obraz powitania poniżej można stwierdzić, że:</span><span class="sxs-lookup"><span data-stu-id="32612-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="32612-119">Aplikacja Hello **sieci szkieletowej: / WordCount** jest czerwony (w wyniku błędu), ponieważ ma ona zdarzenie błędu zgłoszony przez **MyWatchdog** dla właściwości hello **dostępności**.</span><span class="sxs-lookup"><span data-stu-id="32612-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="32612-120">Jedna z jego usług **fabric: / WordCount/usługi WordCountService** jest żółty (w ostrzeżenie).</span><span class="sxs-lookup"><span data-stu-id="32612-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="32612-121">Usługa Hello jest skonfigurowana z replikami siedem i hello klastra ma pięć węzłów, więc nie może zostać umieszczona repicas dwa.</span><span class="sxs-lookup"><span data-stu-id="32612-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="32612-122">Wprawdzie nie pokazano poniżej, partycji usługi hello jest żółty, ze względu na raport dotyczący systemu z `System.FM` informacją, że `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="32612-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="32612-123">Wyzwalacze żółty partycji Hello hello żółty usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="32612-124">z powodu aplikacji hello red klastra Hello jest czerwony.</span><span class="sxs-lookup"><span data-stu-id="32612-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="32612-125">Ocena Hello korzysta z domyślnych zasad z manifestu klastra hello i manifest aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="32612-126">Są ścisłe zasady i nieodpowiednie jakiekolwiek niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="32612-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="32612-127">Widok Eksploratora usługi sieć szkieletowa hello klastra:</span><span class="sxs-lookup"><span data-stu-id="32612-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Widok klastra hello z Eksploratora usługi sieć szkieletowa.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="32612-129">Przeczytaj więcej na temat [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="32612-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="32612-130">Zapytań o kondycję</span><span class="sxs-lookup"><span data-stu-id="32612-130">Health queries</span></span>
<span data-ttu-id="32612-131">Usługa sieci szkieletowej udostępnia zapytań o kondycję dla każdej z obsługiwanych hello [typów jednostek](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="32612-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="32612-132">Są one dostępne za pośrednictwem hello interfejsu API, przy użyciu metody na [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), poleceń cmdlet programu PowerShell i REST.</span><span class="sxs-lookup"><span data-stu-id="32612-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="32612-133">Te zapytania zwraca pełną kondycję informacje dotyczące jednostki hello: hello zagregowane stan kondycji, zdarzenia kondycji jednostki stanów kondycji podrzędnych (jeśli jest to wymagane), zła ocen (jeśli jednostki hello nie jest w dobrej kondycji) i statystyki kondycji elementy podrzędne (gdy ma zastosowanie).</span><span class="sxs-lookup"><span data-stu-id="32612-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="32612-134">Jednostki kondycji jest zwracany, gdy pełni znajduje się w magazynie kondycji hello.</span><span class="sxs-lookup"><span data-stu-id="32612-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="32612-135">Hello jednostki musi być aktywne (nie usunięto) i ma raportu system.</span><span class="sxs-lookup"><span data-stu-id="32612-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="32612-136">Jej podmioty nadrzędnego w łańcuchu hierarchii hello musi mieć również raporty systemu.</span><span class="sxs-lookup"><span data-stu-id="32612-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="32612-137">Jeśli te warunki nie są spełnione, kondycji hello kwerendy powrotu [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) z [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` który pokazuje, dlaczego nie są zwracane jednostki hello.</span><span class="sxs-lookup"><span data-stu-id="32612-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="32612-138">zapytań o kondycję Hello musi upłynąć w hello identyfikator jednostki, który jest zależny od typu jednostki hello.</span><span class="sxs-lookup"><span data-stu-id="32612-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="32612-139">zapytania Hello zaakceptować kondycji opcjonalne parametry zasad.</span><span class="sxs-lookup"><span data-stu-id="32612-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="32612-140">Jeśli nie określono żadnych zasad dotyczących kondycji, hello [zasady dotyczące kondycji](service-fabric-health-introduction.md#health-policies) z manifestu klastra lub aplikacji hello są używane do oceny.</span><span class="sxs-lookup"><span data-stu-id="32612-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="32612-141">Jeśli hello manifestów nie zawiera definicji dla zasad dotyczących kondycji, zasady dotyczące kondycji domyślne hello są używane do oceny.</span><span class="sxs-lookup"><span data-stu-id="32612-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="32612-142">zasady dotyczące kondycji domyślne Hello nieodpowiednie zakończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="32612-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="32612-143">zapytania Hello również Zaakceptuj filtry dla zwracania tylko częściowe elementów podrzędnych lub zdarzenia — Witaj te, które przestrzegać hello określonych filtrów.</span><span class="sxs-lookup"><span data-stu-id="32612-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="32612-144">Inny filtr zezwala, z wyłączeniem hello statystyki elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="32612-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="32612-145">filtrów danych wyjściowych Hello są stosowane na powitania po stronie serwera, więc zmniejsza rozmiar odpowiedzi wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="32612-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="32612-146">Zaleca się, że używasz filtrów danych wyjściowych hello toolimit hello danych zwrócił, zamiast zastosować filtry na powitania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="32612-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="32612-147">Prawidłowość jednostki zawiera:</span><span class="sxs-lookup"><span data-stu-id="32612-147">An entity's health contains:</span></span>

* <span data-ttu-id="32612-148">stan kondycji Hello zagregowane hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="32612-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="32612-149">Obliczone przez hello magazynu kondycji na podstawie raportów o kondycji jednostki, stanów kondycji podrzędnych (jeśli jest to wymagane) i zasad dotyczących kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="32612-150">Przeczytaj więcej na temat [oceny kondycji jednostki](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="32612-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="32612-151">zdarzenia kondycji Hello na powitania jednostki.</span><span class="sxs-lookup"><span data-stu-id="32612-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="32612-152">Kolekcja Hello stanów kondycji wszystkich elementów podrzędnych dla hello jednostek, które mogą mieć elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="32612-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="32612-153">stany kondycji Hello zawierają identyfikatory jednostek i hello zagregowane kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="32612-154">pełną kondycję tooget dziecka, wywołanie dla typów jednostek podrzędnych hello hello zapytania kondycji i podaj identyfikator podrzędnych hello.</span><span class="sxs-lookup"><span data-stu-id="32612-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="32612-155">Hello ocen zła raport toohello tego punktu, który wyzwalane hello stanu jednostki hello, jeżeli hello jednostki jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="32612-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="32612-156">Obliczanie Hello są cykliczne zawierające hello dzieci kondycji oceny, które wywołały bieżącego stanu kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="32612-157">Na przykład programu alarmowego zgłosił błąd przed repliki.</span><span class="sxs-lookup"><span data-stu-id="32612-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="32612-158">Kondycja aplikacji Hello pokazuje ocenę zła powodu usługi w złej kondycji tooan; Usługa Hello jest zła powodu tooa partycji w błąd; partycja Hello jest zła powodu repliki tooa błąd; Replika Hello jest nieprawidłowy, ponieważ raport o kondycji błąd programu alarmowego toohello.</span><span class="sxs-lookup"><span data-stu-id="32612-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="32612-159">Witaj statystyki kondycji dla wszystkich typów elementów podrzędnych hello jednostek, które mają elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="32612-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="32612-160">Na przykład stan klastra jest wyświetlana liczba całkowita hello aplikacji, usług, partycji i replik i wdrażane jednostek w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="32612-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="32612-161">Kondycja usługi pokazuje hello łączna liczba partycji i replik w obszarze hello określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="32612-162">Pobierz stan klastra</span><span class="sxs-lookup"><span data-stu-id="32612-162">Get cluster health</span></span>
<span data-ttu-id="32612-163">Zwraca hello kondycji jednostki klastra hello i zawiera hello stanów kondycji aplikacji i węzły (dzieci hello klastra).</span><span class="sxs-lookup"><span data-stu-id="32612-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="32612-164">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-164">Input:</span></span>

* <span data-ttu-id="32612-165">[Opcjonalnie] hello zasad dotyczących kondycji klastra używane tooevaluate hello węzły i hello zdarzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="32612-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="32612-166">Mapowanie zasady kondycji aplikacji hello [opcjonalnie], z zasad dotyczących kondycji hello używane zasady manifestu aplikacji hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="32612-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="32612-167">[Opcjonalnie] Filtry dla zdarzeń, węzły i aplikacje, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="32612-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="32612-168">Wszystkie zdarzenia, węzły i aplikacji są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.</span><span class="sxs-lookup"><span data-stu-id="32612-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="32612-169">[Opcjonalnie] Filtr tooexclude statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="32612-170">[Opcjonalnie] Filtrować tooinclude fabric: / statystyki kondycji systemu w hello statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="32612-171">Dotyczy tylko gdy hello statystyki kondycji nie są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="32612-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="32612-172">Domyślnie statystyki kondycji hello zawierają tylko statystyki dla użytkownika aplikacji i nie hello aplikacji systemowej.</span><span class="sxs-lookup"><span data-stu-id="32612-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="32612-173">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-173">API</span></span>
<span data-ttu-id="32612-174">tooget klastra kondycji, należy utworzyć `FabricClient` i wywołanie hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) metody na jego **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="32612-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="32612-175">Witaj następujące wywołanie pobiera stan klastra hello:</span><span class="sxs-lookup"><span data-stu-id="32612-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="32612-176">Witaj poniższy kod pobiera stan klastra hello za pomocą zasad niestandardowych klastra kondycji i filtrów dla węzłów i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="32612-177">Określa, że statystyki kondycji hello obejmuje hello sieci szkieletowej: / statystyk systemu.</span><span class="sxs-lookup"><span data-stu-id="32612-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="32612-178">Tworzy [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), który zawiera informacje wejściowe hello.</span><span class="sxs-lookup"><span data-stu-id="32612-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="32612-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-179">PowerShell</span></span>
<span data-ttu-id="32612-180">Stan klastra hello tooget polecenia cmdlet Hello jest [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="32612-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="32612-181">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="32612-182">Witaj stan klastra hello jest pięć węzłów, aplikacji systemowej hello i sieci szkieletowej: / WordCount skonfigurowane zgodnie z opisem.</span><span class="sxs-lookup"><span data-stu-id="32612-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="32612-183">Hello następujące polecenie cmdlet pobiera stan klastra za pomocą domyślnych zasad kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="32612-184">Witaj zagregowane kondycji jest w stanie ostrzegawczym, ponieważ hello fabric: / aplikacja WordCount jest ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="32612-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="32612-185">Należy zwrócić uwagę, jak hello zła oceny zawierają szczegółowe informacje dotyczące hello warunki, które wyzwalane kondycji hello agregowane.</span><span class="sxs-lookup"><span data-stu-id="32612-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

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

<span data-ttu-id="32612-186">Witaj następujące polecenia cmdlet programu PowerShell pobiera kondycji hello hello klastra za pomocą zasad niestandardowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="32612-187">Filtruje wyniki tooget tylko aplikacji i węzły w błąd lub ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="32612-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="32612-188">W związku z tym żadnych węzłów są zwracane, ponieważ są one wszystkich dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="32612-189">Tylko hello fabric: / WordCount aplikacji szanuje filtru aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="32612-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="32612-190">Ponieważ zasady niestandardowe hello określa tooconsider ostrzeżenia jako błędy sieci szkieletowej hello: / WordCount aplikacji, aplikacji hello jest oceniany, tak jak błąd, i dlatego jest hello klastra.</span><span class="sxs-lookup"><span data-stu-id="32612-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

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

### <a name="rest"></a><span data-ttu-id="32612-191">REST</span><span class="sxs-lookup"><span data-stu-id="32612-191">REST</span></span>
<span data-ttu-id="32612-192">Możesz uzyskać kondycji klastra z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.</span><span class="sxs-lookup"><span data-stu-id="32612-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="32612-193">Pobierz węzeł kondycji</span><span class="sxs-lookup"><span data-stu-id="32612-193">Get node health</span></span>
<span data-ttu-id="32612-194">Zwraca hello kondycji jednostek node i zawiera zdarzenia kondycji hello zgłoszone w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="32612-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="32612-195">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-195">Input:</span></span>

* <span data-ttu-id="32612-196">Nazwa węzła hello [wymagane], która identyfikuje hello węzła.</span><span class="sxs-lookup"><span data-stu-id="32612-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="32612-197">Ustawienia zasad kondycji klastra [opcjonalnie] hello używane tooevaluate kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="32612-198">[Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="32612-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="32612-199">Wszystkie zdarzenia są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.</span><span class="sxs-lookup"><span data-stu-id="32612-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="32612-200">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-200">API</span></span>
<span data-ttu-id="32612-201">Tworzenie tooget węzła kondycji za pomocą interfejsu API, hello `FabricClient` i hello wywołania [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="32612-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="32612-202">Witaj poniższy kod pobiera kondycji węzła hello nazwę określonego węzła hello:</span><span class="sxs-lookup"><span data-stu-id="32612-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="32612-203">Witaj poniższy kod umożliwia pobranie kondycji węzła hello hello określić nazwy węzła i przekazuje filtr zdarzeń i niestandardowych zasad za pośrednictwem [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="32612-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="32612-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-204">PowerShell</span></span>
<span data-ttu-id="32612-205">Witaj polecenia cmdlet tooget hello węzła kondycja jest [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="32612-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="32612-206">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="32612-207">Hello następujące polecenie cmdlet pobiera hello węzła kondycji za pomocą domyślnych zasad kondycji:</span><span class="sxs-lookup"><span data-stu-id="32612-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

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

<span data-ttu-id="32612-208">Witaj następujące polecenie cmdlet pobiera hello kondycję wszystkich węzłów w klastrze hello:</span><span class="sxs-lookup"><span data-stu-id="32612-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

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

### <a name="rest"></a><span data-ttu-id="32612-209">REST</span><span class="sxs-lookup"><span data-stu-id="32612-209">REST</span></span>
<span data-ttu-id="32612-210">Możesz uzyskać kondycji węzła z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.</span><span class="sxs-lookup"><span data-stu-id="32612-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="32612-211">Pobierz kondycji aplikacji</span><span class="sxs-lookup"><span data-stu-id="32612-211">Get application health</span></span>
<span data-ttu-id="32612-212">Zwraca hello kondycję obiektu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="32612-213">Zawiera ona hello stanów kondycji aplikacji hello wdrożony i usługa dzieci.</span><span class="sxs-lookup"><span data-stu-id="32612-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="32612-214">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-214">Input:</span></span>

* <span data-ttu-id="32612-215">[Wymagane] hello Nazwa aplikacji (URI) określający aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="32612-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="32612-216">Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="32612-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="32612-217">[Opcjonalnie] Filtry dla zdarzeń, usług i wdrożone aplikacje, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="32612-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="32612-218">Zdarzeń, usług i wdrożone aplikacje są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.</span><span class="sxs-lookup"><span data-stu-id="32612-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="32612-219">[Opcjonalnie] Filtrowanie statystyki kondycji hello tooexclude.</span><span class="sxs-lookup"><span data-stu-id="32612-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="32612-220">Jeśli nie zostanie określony, statystyki kondycji hello obejmują hello ok, ostrzeżenie i liczby błędów dla wszystkich aplikacji elementów podrzędnych: usług, partycji, repliki, wdrożonych aplikacji i wdrożonych pakietów usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="32612-221">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-221">API</span></span>
<span data-ttu-id="32612-222">tooget kondycji aplikacji, Utwórz `FabricClient` i wywołanie hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="32612-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="32612-223">Witaj poniższy kod pobiera kondycji aplikacji hello nazwy określonej aplikacji hello (URI):</span><span class="sxs-lookup"><span data-stu-id="32612-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="32612-224">Witaj poniższy kod pobiera kondycji aplikacji hello nazwy określonej aplikacji hello (URI), z filtrami i niestandardowych zasad określona za pomocą [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="32612-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

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

### <a name="powershell"></a><span data-ttu-id="32612-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-225">PowerShell</span></span>
<span data-ttu-id="32612-226">Kondycja aplikacji hello tooget polecenia cmdlet Hello jest [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="32612-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="32612-227">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="32612-228">Witaj następujące polecenie cmdlet zwraca hello kondycję hello **fabric: / WordCount** aplikacji:</span><span class="sxs-lookup"><span data-stu-id="32612-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

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

<span data-ttu-id="32612-229">Witaj, po przekazuje polecenia cmdlet programu PowerShell w ramach zasad niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="32612-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="32612-230">Filtruje także elementów podrzędnych i zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="32612-230">It also filters children and events.</span></span>

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

### <a name="rest"></a><span data-ttu-id="32612-231">REST</span><span class="sxs-lookup"><span data-stu-id="32612-231">REST</span></span>
<span data-ttu-id="32612-232">Możesz uzyskać kondycji aplikacji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.</span><span class="sxs-lookup"><span data-stu-id="32612-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="32612-233">Pobierz usługi kondycji</span><span class="sxs-lookup"><span data-stu-id="32612-233">Get service health</span></span>
<span data-ttu-id="32612-234">Zwraca hello kondycji jednostki usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="32612-235">Zawiera ona stanów kondycji hello partycji.</span><span class="sxs-lookup"><span data-stu-id="32612-235">It contains hello partition health states.</span></span> <span data-ttu-id="32612-236">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-236">Input:</span></span>

* <span data-ttu-id="32612-237">[Wymagane] hello nazwa usługi (URI) określający hello usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="32612-238">Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="32612-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="32612-239">[Opcjonalnie] Filtry dla zdarzeń i partycje, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="32612-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="32612-240">Wszystkie zdarzenia i partycji są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.</span><span class="sxs-lookup"><span data-stu-id="32612-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="32612-241">[Opcjonalnie] Filtr tooexclude statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="32612-242">Jeśli nie zostanie określony, ok hello hello Pokaż statystyki kondycji, ostrzeżenia i błędu liczba dla wszystkich partycji i replik hello usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="32612-243">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-243">API</span></span>
<span data-ttu-id="32612-244">Kondycja usługi tooget za pośrednictwem hello interfejsu API, Utwórz `FabricClient` i wywołanie hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="32612-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="32612-245">Witaj poniższy przykład pobiera hello kondycji usługi o nazwie określonej usługi (URI):</span><span class="sxs-lookup"><span data-stu-id="32612-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="32612-246">Witaj poniższy kod pobiera hello usługi kondycji dla nazwy usługi określony hello (URI), filtrów i zasad niestandardowych za pomocą [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="32612-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="32612-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-247">PowerShell</span></span>
<span data-ttu-id="32612-248">Kondycja usługi hello tooget polecenia cmdlet Hello jest [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="32612-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="32612-249">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="32612-250">Hello następujące polecenie cmdlet pobiera hello usługi kondycji za pomocą domyślnych zasad kondycji:</span><span class="sxs-lookup"><span data-stu-id="32612-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

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

### <a name="rest"></a><span data-ttu-id="32612-251">REST</span><span class="sxs-lookup"><span data-stu-id="32612-251">REST</span></span>
<span data-ttu-id="32612-252">Można pobrać usługi kondycji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.</span><span class="sxs-lookup"><span data-stu-id="32612-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="32612-253">Pobierz kondycji partycji</span><span class="sxs-lookup"><span data-stu-id="32612-253">Get partition health</span></span>
<span data-ttu-id="32612-254">Zwraca hello kondycji jednostki partycji.</span><span class="sxs-lookup"><span data-stu-id="32612-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="32612-255">Zawiera ona stanów kondycji hello repliki.</span><span class="sxs-lookup"><span data-stu-id="32612-255">It contains hello replica health states.</span></span> <span data-ttu-id="32612-256">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-256">Input:</span></span>

* <span data-ttu-id="32612-257">[Wymagane] hello partycji identyfikator (GUID), który identyfikuje hello partycji.</span><span class="sxs-lookup"><span data-stu-id="32612-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="32612-258">Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="32612-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="32612-259">[Opcjonalnie] Filtry dla zdarzeń i replik, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="32612-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="32612-260">Wszystkie zdarzenia i repliki są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.</span><span class="sxs-lookup"><span data-stu-id="32612-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="32612-261">[Opcjonalnie] Filtr tooexclude statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="32612-262">Jeśli nie zostanie określony, statystyki kondycji hello pokazują, jak wiele repliki są w ok, ostrzeżenia i błędu stanów.</span><span class="sxs-lookup"><span data-stu-id="32612-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="32612-263">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-263">API</span></span>
<span data-ttu-id="32612-264">Utwórz tooget partycji kondycji za pomocą interfejsu API, hello `FabricClient` i wywołanie hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="32612-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="32612-265">Utwórz następujące parametry opcjonalne toospecify, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="32612-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="32612-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-266">PowerShell</span></span>
<span data-ttu-id="32612-267">Witaj polecenia cmdlet tooget hello partycji kondycja jest [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="32612-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="32612-268">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="32612-269">Hello następujące polecenie cmdlet pobiera hello kondycji dla wszystkich partycji hello **fabric: / WordCount/usługi WordCountService** usługi i odfiltrowuje repliki stanów kondycji:</span><span class="sxs-lookup"><span data-stu-id="32612-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

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

### <a name="rest"></a><span data-ttu-id="32612-270">REST</span><span class="sxs-lookup"><span data-stu-id="32612-270">REST</span></span>
<span data-ttu-id="32612-271">Możesz uzyskać kondycji partycji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.</span><span class="sxs-lookup"><span data-stu-id="32612-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="32612-272">Pobierz kondycji repliki</span><span class="sxs-lookup"><span data-stu-id="32612-272">Get replica health</span></span>
<span data-ttu-id="32612-273">Zwraca kondycji hello repliki usługi stanowej lub wystąpienia usługi bezstanowej.</span><span class="sxs-lookup"><span data-stu-id="32612-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="32612-274">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-274">Input:</span></span>

* <span data-ttu-id="32612-275">[Wymagane] hello identyfikator partycji: Identyfikatora (GUID) i repliki identyfikujący hello repliki.</span><span class="sxs-lookup"><span data-stu-id="32612-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="32612-276">Parametry zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="32612-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="32612-277">[Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="32612-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="32612-278">Wszystkie zdarzenia są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.</span><span class="sxs-lookup"><span data-stu-id="32612-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="32612-279">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-279">API</span></span>
<span data-ttu-id="32612-280">Utwórz tooget hello repliki kondycji za pomocą interfejsu API, hello `FabricClient` i wywołanie hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="32612-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="32612-281">Zaawansowane parametry, użyj toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="32612-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="32612-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-282">PowerShell</span></span>
<span data-ttu-id="32612-283">Witaj polecenia cmdlet tooget hello repliki kondycja jest [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="32612-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="32612-284">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="32612-285">Witaj następujące polecenie cmdlet pobiera hello kondycję hello repliki podstawowej dla wszystkich partycji usługi hello:</span><span class="sxs-lookup"><span data-stu-id="32612-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

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

### <a name="rest"></a><span data-ttu-id="32612-286">REST</span><span class="sxs-lookup"><span data-stu-id="32612-286">REST</span></span>
<span data-ttu-id="32612-287">Możesz uzyskać kondycji repliki z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.</span><span class="sxs-lookup"><span data-stu-id="32612-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="32612-288">Pobierz kondycji wdrożonej aplikacji</span><span class="sxs-lookup"><span data-stu-id="32612-288">Get deployed application health</span></span>
<span data-ttu-id="32612-289">Zwraca hello kondycji aplikacji wdrożone w ramach jednostki węzła.</span><span class="sxs-lookup"><span data-stu-id="32612-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="32612-290">Zawiera ona stanów kondycji pakietu usługi hello wdrożone.</span><span class="sxs-lookup"><span data-stu-id="32612-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="32612-291">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-291">Input:</span></span>

* <span data-ttu-id="32612-292">Nazwa aplikacji hello [wymagane] (URI) i nazwa węzła (ciąg) identyfikujących hello wdrożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="32612-293">Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="32612-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="32612-294">[Opcjonalnie] Filtry dla zdarzeń i wdrożone pakiety usługi określające zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="32612-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="32612-295">Wszystkie zdarzenia i wdrożone pakiety usługi są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.</span><span class="sxs-lookup"><span data-stu-id="32612-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="32612-296">[Opcjonalnie] Filtr tooexclude statystyki kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="32612-297">Jeśli nie zostanie określony, statystyki kondycji hello zawierają hello liczbę pakietów wdrożonej usługi w ok, ostrzeżenia i błędu stanów kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="32612-298">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-298">API</span></span>
<span data-ttu-id="32612-299">Utwórz tooget hello kondycji aplikacji wdrożonych na węźle, za pośrednictwem interfejsu API, hello `FabricClient` i wywołanie hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="32612-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="32612-300">Parametry opcjonalne toospecify, użyj [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="32612-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="32612-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-301">PowerShell</span></span>
<span data-ttu-id="32612-302">Witaj kondycji aplikacji hello wdrożone tooget polecenia cmdlet jest [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="32612-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="32612-303">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="32612-304">Uruchom toofind się, gdy aplikacja jest wdrażana, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) i przyjrzeć hello wdrożonych aplikacji elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="32612-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="32612-305">Hello następujące polecenie cmdlet pobiera hello kondycję hello **fabric: / WordCount** aplikacji wdrożonych na **to węzeł _Node_2**.</span><span class="sxs-lookup"><span data-stu-id="32612-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="32612-306">REST</span><span class="sxs-lookup"><span data-stu-id="32612-306">REST</span></span>
<span data-ttu-id="32612-307">Możesz uzyskać kondycji wdrożonej aplikacji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.</span><span class="sxs-lookup"><span data-stu-id="32612-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="32612-308">Pobierz kondycji pakietu wdrożonej usługi</span><span class="sxs-lookup"><span data-stu-id="32612-308">Get deployed service package health</span></span>
<span data-ttu-id="32612-309">Zwraca hello kondycji jednostki pakietu wdrożonej usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="32612-310">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-310">Input:</span></span>

* <span data-ttu-id="32612-311">Nazwa aplikacji hello [wymagane] (URI), nazwę węzła (ciąg) i nazwa manifestu usługi (ciąg) identyfikujących hello wdrożony pakiet usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="32612-312">Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="32612-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="32612-313">[Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy).</span><span class="sxs-lookup"><span data-stu-id="32612-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="32612-314">Wszystkie zdarzenia są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.</span><span class="sxs-lookup"><span data-stu-id="32612-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="32612-315">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-315">API</span></span>
<span data-ttu-id="32612-316">Utwórz tooget hello kondycji pakietu wdrożonej usługi za pośrednictwem hello interfejsu API, `FabricClient` i wywołanie hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) metody na jego HealthManager.</span><span class="sxs-lookup"><span data-stu-id="32612-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="32612-317">Parametry opcjonalne toospecify, użyj [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="32612-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="32612-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-318">PowerShell</span></span>
<span data-ttu-id="32612-319">Witaj polecenia cmdlet tooget hello wdrożone usługi pakietu kondycja jest [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="32612-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="32612-320">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="32612-321">Uruchom toosee, w którym aplikacja jest wdrażana, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) i przyjrzyj się hello wdrożone aplikacje.</span><span class="sxs-lookup"><span data-stu-id="32612-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="32612-322">toosee, które pakiety usługi są w aplikacji, poszukać w hello wdrożone usługi pakietu dzieci w hello [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="32612-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="32612-323">Witaj następujące polecenie cmdlet pobiera hello kondycję hello **WordCountServicePkg** pakiet usługi hello **sieci szkieletowej: / WordCount** aplikacji wdrożonych na **to węzeł _Node_2**.</span><span class="sxs-lookup"><span data-stu-id="32612-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="32612-324">Jednostka Hello ma **System.Hosting** raporty dla pomyślnej aktywacji w pakiecie usługi i punktu wejścia i pomyślną rejestrację typu usługi.</span><span class="sxs-lookup"><span data-stu-id="32612-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="32612-325">REST</span><span class="sxs-lookup"><span data-stu-id="32612-325">REST</span></span>
<span data-ttu-id="32612-326">Możesz uzyskać wdrożonej usługi kondycji pakietu z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.</span><span class="sxs-lookup"><span data-stu-id="32612-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="32612-327">Fragmentu zapytań o kondycję</span><span class="sxs-lookup"><span data-stu-id="32612-327">Health chunk queries</span></span>
<span data-ttu-id="32612-328">Witaj kondycji fragmentu zapytania mogą zwracać elementy podrzędne (rekursywnie), wielopoziomowe klastra na filtry.</span><span class="sxs-lookup"><span data-stu-id="32612-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="32612-329">Obsługuje ona filtrów zaawansowanych, zezwalających na dużą elastyczność w wyborze dzieci hello toobe zwracane.</span><span class="sxs-lookup"><span data-stu-id="32612-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="32612-330">filtry Hello określić elementy podrzędne Unikatowy identyfikator hello lub przez inne grupy identyfikatorów i/lub stanów kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="32612-331">Domyślnie bez żadnych elementów podrzędnych zostaną uzupełnione, w przeciwieństwie toohealth poleceń, które zawsze zawierają elementy podrzędne pierwszego stopnia.</span><span class="sxs-lookup"><span data-stu-id="32612-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="32612-332">Witaj [zapytań o kondycję](service-fabric-view-entities-aggregated-health.md#health-queries) zwracane elementy podrzędne tylko pierwszy poziom hello określone jednostki na wymagane filtrów.</span><span class="sxs-lookup"><span data-stu-id="32612-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="32612-333">tooget hello podrzędnych elementów podrzędnych hello, należy wywołać kondycji dodatkowe interfejsy API dla każdej jednostki zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="32612-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="32612-334">Podobnie kondycję hello tooget konkretnych obiektów, należy wywołać kondycji jednego interfejsu API dla każdego żądanego obiektu.</span><span class="sxs-lookup"><span data-stu-id="32612-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="32612-335">Witaj fragmentu zapytania zaawansowane filtrowanie pozwala toorequest wielu elementy w jednym zapytaniu, minimalizując rozmiaru wiadomości powitania i hello liczbę komunikatów.</span><span class="sxs-lookup"><span data-stu-id="32612-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="32612-336">wartość Hello hello fragmentu zapytania jest, że możesz też uzyskać stan kondycji kolejnych jednostek klastra (potencjalnie wszystkich klastra jednostek zaczynając od wymaganego głównego) w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="32612-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="32612-337">Można wyrazić zapytania kondycji złożonych takich jak:</span><span class="sxs-lookup"><span data-stu-id="32612-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="32612-338">Zwracany aplikacji tylko w błąd, a w przypadku aplikacji obejmują wszystkie usługi w ostrzeżenia lub błędu.</span><span class="sxs-lookup"><span data-stu-id="32612-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="32612-339">W przypadku zwróconych usług zawiera wszystkie partycje.</span><span class="sxs-lookup"><span data-stu-id="32612-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="32612-340">Zwróć tylko hello kondycji cztery aplikacje, określonych przez ich nazwy.</span><span class="sxs-lookup"><span data-stu-id="32612-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="32612-341">Zwróć tylko hello kondycję aplikacji typu żądanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="32612-342">Zwraca wszystkie wdrożone jednostek w węźle.</span><span class="sxs-lookup"><span data-stu-id="32612-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="32612-343">Zwraca wszystkie aplikacje, wszystkich aplikacji wdrożonych na powitania określony węzeł i wszystkie pakiety service hello wdrożone w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="32612-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="32612-344">Zwróć wszystkie repliki na błąd.</span><span class="sxs-lookup"><span data-stu-id="32612-344">Return all replicas in error.</span></span> <span data-ttu-id="32612-345">Zwraca wszystkich aplikacji, usług, partycji i replik tylko z błędami.</span><span class="sxs-lookup"><span data-stu-id="32612-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="32612-346">Zwróć wszystkie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="32612-346">Return all applications.</span></span> <span data-ttu-id="32612-347">Dla określonej usługi należy wprowadzić wszystkie partycje.</span><span class="sxs-lookup"><span data-stu-id="32612-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="32612-348">Obecnie hello kondycji fragmentu zapytania jest widoczne tylko dla obiektu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="32612-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="32612-349">Zwraca fragmentu kondycji klastra, który zawiera:</span><span class="sxs-lookup"><span data-stu-id="32612-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="32612-350">klaster Hello agregowana stan kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="32612-351">Hello kondycji stanu fragmentu listy węzłów, które przestrzegać filtry.</span><span class="sxs-lookup"><span data-stu-id="32612-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="32612-352">Hello kondycji stanu fragmentu lista aplikacji, których przestrzeganie filtry.</span><span class="sxs-lookup"><span data-stu-id="32612-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="32612-353">Każdego fragmentu stan kondycji aplikacji znajduje się lista fragmentu ze wszystkich usług, których przestrzeganie filtry i listy fragmentu z wszystkich wdrożonych aplikacji, które przestrzegać hello filtrów.</span><span class="sxs-lookup"><span data-stu-id="32612-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="32612-354">Wartość taka sama dla dzieci hello usług i wdrożone aplikacje.</span><span class="sxs-lookup"><span data-stu-id="32612-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="32612-355">Dzięki temu wszystkie jednostki w klastrze hello może być potencjalnie zwracany żądanie w hierarchiczny sposób.</span><span class="sxs-lookup"><span data-stu-id="32612-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="32612-356">Klaster kondycji fragmentu zapytania</span><span class="sxs-lookup"><span data-stu-id="32612-356">Cluster health chunk query</span></span>
<span data-ttu-id="32612-357">Zwraca hello kondycji jednostki klastra hello i zawiera fragmenty stan kondycji hierarchiczna hello wymagane elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="32612-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="32612-358">Dane wejściowe:</span><span class="sxs-lookup"><span data-stu-id="32612-358">Input:</span></span>

* <span data-ttu-id="32612-359">[Opcjonalnie] hello zasad dotyczących kondycji klastra używane tooevaluate hello węzły i hello zdarzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="32612-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="32612-360">Mapowanie zasady kondycji aplikacji hello [opcjonalnie], z zasad dotyczących kondycji hello używane zasady manifestu aplikacji hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="32612-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="32612-361">[Opcjonalnie] Filtry dla węzłów i aplikacje, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello.</span><span class="sxs-lookup"><span data-stu-id="32612-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="32612-362">filtry Hello są tooan określonej jednostki/grupy jednostek lub tooall odpowiednich jednostek na tym poziomie.</span><span class="sxs-lookup"><span data-stu-id="32612-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="32612-363">Witaj lista filtrów może zawierać jeden filtr ogólne i/lub filtrów dla określonych identyfikatorów toofine ziarna jednostek zwróconych przez zapytanie hello.</span><span class="sxs-lookup"><span data-stu-id="32612-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="32612-364">W przypadku braku hello elementy podrzędne nie są zwracane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="32612-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="32612-365">Przeczytaj więcej na temat filtrów hello w [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) i [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="32612-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="32612-366">rekursywnie może filtrów aplikacji Hello określ filtry zaawansowane podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="32612-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="32612-367">Wynik fragmentu Hello zawiera elementy podrzędne hello przestrzegać hello filtrów.</span><span class="sxs-lookup"><span data-stu-id="32612-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="32612-368">Obecnie hello fragmentu zapytania nie zwraca zła ocen lub zdarzeń jednostki.</span><span class="sxs-lookup"><span data-stu-id="32612-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="32612-369">Dodatkowe informacje można uzyskać za pomocą hello istniejące zapytanie kondycji klastra.</span><span class="sxs-lookup"><span data-stu-id="32612-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="32612-370">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="32612-370">API</span></span>
<span data-ttu-id="32612-371">Stan klastra tooget bryłkach, Utwórz `FabricClient` i wywołanie hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) metody na jego **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="32612-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="32612-372">Można przekazać [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe zasady dotyczące kondycji i filtry zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="32612-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="32612-373">Witaj poniższy kod pobiera fragmentu kondycji klastra z filtry zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="32612-373">hello following code gets cluster health chunk with advanced filters.</span></span>

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

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="32612-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32612-374">PowerShell</span></span>
<span data-ttu-id="32612-375">Stan klastra hello tooget polecenia cmdlet Hello jest [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="32612-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="32612-376">Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="32612-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="32612-377">Witaj poniższy kod pobiera węzły tylko wtedy, gdy są one błąd z wyjątkiem określonego węzła zawsze ma zostać zwrócony.</span><span class="sxs-lookup"><span data-stu-id="32612-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
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

<span data-ttu-id="32612-378">Witaj następujące polecenie cmdlet pobiera fragmentu klastra z filtrami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

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

<span data-ttu-id="32612-379">Witaj następujące polecenie cmdlet zwraca wszystkie wdrożone jednostki w węźle.</span><span class="sxs-lookup"><span data-stu-id="32612-379">hello following cmdlet returns all deployed entities on a node.</span></span>

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

### <a name="rest"></a><span data-ttu-id="32612-380">REST</span><span class="sxs-lookup"><span data-stu-id="32612-380">REST</span></span>
<span data-ttu-id="32612-381">Możesz uzyskać fragment kondycji klastra z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) zawierającej zasady dotyczące kondycji i opisane w treści hello filtry zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="32612-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="32612-382">Ogólne zapytań</span><span class="sxs-lookup"><span data-stu-id="32612-382">General queries</span></span>
<span data-ttu-id="32612-383">Ogólne kwerendy zwracają listę jednostki sieci szkieletowej usług określonego typu.</span><span class="sxs-lookup"><span data-stu-id="32612-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="32612-384">Są one dostępne za pośrednictwem hello interfejsu API (za pomocą metod hello na **FabricClient.QueryManager**), polecenia cmdlet programu PowerShell i REST.</span><span class="sxs-lookup"><span data-stu-id="32612-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="32612-385">Te zapytania agregować podzapytania z wielu składników.</span><span class="sxs-lookup"><span data-stu-id="32612-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="32612-386">Jeden z nich jest hello [magazynu kondycji](service-fabric-health-introduction.md#health-store), który wypełnia hello zagregowane stan kondycji dla każdego wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="32612-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="32612-387">Ogólne zapytania zwracać hello zagregowane stanu kondycji jednostki hello i nie zawierają danych sformatowanego kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="32612-388">Jeśli jednostka nie jest w dobrej kondycji, można odpowiednio zareagować z tooget zapytania kondycji wszystkich jego kondycji informacji, w tym zdarzenia, stanów kondycji podrzędnych i oceny złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="32612-389">Jeśli ogólne kwerend zwraca nieznany kondycja jednostki, istnieje możliwość tego magazynu kondycji hello nie ma pełnych danych o hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="32612-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="32612-390">Istnieje również możliwość, że sklep kondycji toohello podzapytania nie powiodło się (na przykład wystąpił błąd komunikacji lub magazynu kondycji hello został ograniczony).</span><span class="sxs-lookup"><span data-stu-id="32612-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="32612-391">Wykonaj przy użyciu zapytania kondycji hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="32612-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="32612-392">Jeśli podzapytanie hello napotkała przejściowe błędy, takie jak problemy z siecią, to zapytanie kolejnych może się powieść.</span><span class="sxs-lookup"><span data-stu-id="32612-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="32612-393">Go może także zapewniają więcej szczegółowych informacji z magazynu kondycji hello o Dlaczego hello jednostki nie jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="32612-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="32612-394">Witaj zapytania, które zawierają **HealthState** dla jednostki to:</span><span class="sxs-lookup"><span data-stu-id="32612-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="32612-395">Listy węzłów: zwraca hello listy węzłów w klastrze hello (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="32612-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="32612-396">Interfejs API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="32612-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="32612-397">Środowiska PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="32612-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="32612-398">Lista aplikacji: hello zwraca listę aplikacji w klastrze hello (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="32612-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="32612-399">Interfejs API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="32612-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="32612-400">Środowiska PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="32612-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="32612-401">Lista usług: hello zwraca listę usług w aplikacji (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="32612-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="32612-402">Interfejs API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="32612-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="32612-403">Środowiska PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="32612-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="32612-404">Lista partycji: zwraca listę hello partycji w usłudze (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="32612-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="32612-405">Interfejs API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="32612-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="32612-406">Środowiska PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="32612-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="32612-407">Listy replik: zwraca hello listę replik w partycji (stronicowanej).</span><span class="sxs-lookup"><span data-stu-id="32612-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="32612-408">Interfejs API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="32612-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="32612-409">Środowiska PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="32612-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="32612-410">Wdrożone listy aplikacji: hello zwraca listę wdrożonych aplikacji w węźle.</span><span class="sxs-lookup"><span data-stu-id="32612-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="32612-411">Interfejs API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="32612-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="32612-412">Środowiska PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="32612-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="32612-413">Wdrożone usługi listy pakietów: hello zwraca listę pakietów usług we wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="32612-414">Interfejs API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="32612-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="32612-415">Środowiska PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="32612-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="32612-416">Niektóre z zapytań hello zwracać wyników stronicowania.</span><span class="sxs-lookup"><span data-stu-id="32612-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="32612-417">Witaj zwrotu z tych kwerend znajduje się lista pochodzące z [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="32612-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="32612-418">Jeśli wyniki hello nie pasują do wiadomości, jest zwracana tylko stronę i ContinuationToken śledzi gdzie wyliczenie zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="32612-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="32612-419">Nadal hello toocall sam zapytań i przekaż token kontynuacji hello z hello poprzednich zapytań tooget dalej wyników.</span><span class="sxs-lookup"><span data-stu-id="32612-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="32612-420">Przykłady</span><span class="sxs-lookup"><span data-stu-id="32612-420">Examples</span></span>
<span data-ttu-id="32612-421">Witaj poniższy kod pobiera złej kondycji aplikacji hello w klastrze hello:</span><span class="sxs-lookup"><span data-stu-id="32612-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="32612-422">Witaj następujące polecenie cmdlet pobiera szczegóły aplikacji hello hello sieci szkieletowej: / WordCount aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="32612-423">Należy zauważyć, że stan kondycji jest ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="32612-423">Notice that health state is at warning.</span></span>

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

<span data-ttu-id="32612-424">Witaj następujące polecenie cmdlet pobiera hello usług o stanie kondycji błędu:</span><span class="sxs-lookup"><span data-stu-id="32612-424">hello following cmdlet gets hello services with a health state of error:</span></span>

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

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="32612-425">Uaktualnienia klastra i aplikacji</span><span class="sxs-lookup"><span data-stu-id="32612-425">Cluster and application upgrades</span></span>
<span data-ttu-id="32612-426">Podczas uaktualniania monitorowanych hello klastra i aplikacji sieci szkieletowej usług sprawdza tooensure kondycji wszystkich pozostaje dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="32612-427">Jeśli jednostka jest nieprawidłowy, ponieważ oceniane przy użyciu zasad dotyczących kondycji skonfigurowanego, uaktualnienie hello ma zastosowanie zasad dla konkretnych uaktualnienia toodetermine hello następnej akcji.</span><span class="sxs-lookup"><span data-stu-id="32612-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="32612-428">uaktualnienie Hello może być wstrzymana tooallow interakcji z użytkownikiem (na przykład poprawki błędów lub zmiany zasad) lub go może automatycznie przywrócić poprzedniej wersji dobrej toohello.</span><span class="sxs-lookup"><span data-stu-id="32612-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="32612-429">Podczas *klastra* uaktualnienia, możesz uzyskać stan uaktualnienia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="32612-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="32612-430">Stan uaktualnienia Hello obejmuje oceny złej kondycji, które toowhat punkt jest zła hello klastra.</span><span class="sxs-lookup"><span data-stu-id="32612-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="32612-431">Jeśli uaktualnienie hello jest przywracana powodu toohealth problemy, stan uaktualnienia hello pamięta hello ostatniego przyczyny złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="32612-432">Te informacje mogą pomóc Administratorzy zbadać, co poszło źle po uaktualnieniu hello wycofana lub zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="32612-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="32612-433">Podobnie podczas *aplikacji* uaktualnienia, wszelkie nieprawidłowości oceny są zawarte w stan uaktualnienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="32612-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="32612-434">Hello poniżej przedstawia stan uaktualnienia aplikacji hello zmodyfikowane sieci szkieletowej: / WordCount aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32612-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="32612-435">Programu alarmowego zgłosił błąd na jednym z jego repliki.</span><span class="sxs-lookup"><span data-stu-id="32612-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="32612-436">uaktualnienie Hello wykonuje procedurę wycofywania, ponieważ hello kontroli kondycji nie są przestrzegane.</span><span class="sxs-lookup"><span data-stu-id="32612-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

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

<span data-ttu-id="32612-437">Dowiedz się więcej o hello [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="32612-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="32612-438">Użyj tootroubleshoot oceny kondycji</span><span class="sxs-lookup"><span data-stu-id="32612-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="32612-439">Zawsze, gdy występuje problem z klastra hello lub aplikacji, obejrzyj toopinpoint kondycji klastra lub aplikacji hello co to jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="32612-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="32612-440">Zła ocen Hello zawierają szczegółowe informacje o jakie wyzwalanych hello bieżący stan złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="32612-441">Jeśli zajdzie potrzeba, użytkownik może przejść do podrzędne o złej kondycji jednostek tooidentify hello główną przyczynę.</span><span class="sxs-lookup"><span data-stu-id="32612-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="32612-442">Rozważmy na przykład aplikacji nieprawidłowy, ponieważ raport o błędach na jednym z jego repliki.</span><span class="sxs-lookup"><span data-stu-id="32612-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="32612-443">Hello następujące polecenia cmdlet programu Powershell pokazuje hello ocen złej kondycji:</span><span class="sxs-lookup"><span data-stu-id="32612-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

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

<span data-ttu-id="32612-444">Można przyjrzeć się tooget repliki hello więcej informacji:</span><span class="sxs-lookup"><span data-stu-id="32612-444">You can look at hello replica tooget more information:</span></span>

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
> <span data-ttu-id="32612-445">Hello zła ocen Pokaż hello pierwszy przyczyny jednostka hello jest oceniane toocurrent stan kondycji.</span><span class="sxs-lookup"><span data-stu-id="32612-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="32612-446">Może istnieć wiele zdarzeń wyzwalających ten stan, ale są one nie zostać zawarte w hello oceny.</span><span class="sxs-lookup"><span data-stu-id="32612-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="32612-447">tooget więcej informacji, przechodzenie do toofigure jednostek kondycji hello limit wszystkich raportów zła hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="32612-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="32612-448">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32612-448">Next steps</span></span>
[<span data-ttu-id="32612-449">Użyj tootroubleshoot Raporty kondycji systemu</span><span class="sxs-lookup"><span data-stu-id="32612-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="32612-450">Dodawanie niestandardowych raportów kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="32612-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="32612-451">Jak tooreport i zaznacz pole wyboru usługi kondycji</span><span class="sxs-lookup"><span data-stu-id="32612-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="32612-452">Monitorowanie i diagnozowania usług lokalnie</span><span class="sxs-lookup"><span data-stu-id="32612-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="32612-453">Uaktualnianie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="32612-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
