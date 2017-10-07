---
title: "usługi sieci szkieletowej usług aaaPartitioning | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toopartition sieci szkieletowej usług stanowych usług. Partycje umożliwia przechowywanie danych na maszynach lokalne powitania, danych i zasobów obliczeniowych mogą być skalowane razem."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="c141f-104">Niezawodne usługi Service Fabric partycji</span><span class="sxs-lookup"><span data-stu-id="c141f-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="c141f-105">Ten artykuł zawiera toohello wprowadzenie podstawowe pojęcia partycjonowania niezawodne usługi sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="c141f-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="c141f-106">Witaj używane w artykule hello kod źródłowy jest również dostępna w [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="c141f-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="c141f-107">Partycjonowanie</span><span class="sxs-lookup"><span data-stu-id="c141f-107">Partitioning</span></span>
<span data-ttu-id="c141f-108">Partycjonowanie nie jest unikatowy tooService sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="c141f-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="c141f-109">W rzeczywistości jest wzorzec core tworzenie skalowalnych usług.</span><span class="sxs-lookup"><span data-stu-id="c141f-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="c141f-110">W szerszym znaczeniu możemy pomyśleć o partycjonowania jako koncepcji podziału stanu (dane) i obliczeniowe na mniejsze jednostki dostępne tooimprove skalowalność i wydajność.</span><span class="sxs-lookup"><span data-stu-id="c141f-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="c141f-111">Dobrze znane formularz partycjonowania [partycjonowanie danych][wikipartition], znanej również jako dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="c141f-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="c141f-112">Usługi bezstanowej partycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c141f-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="c141f-113">W przypadku usług bezstanowych należy zwrócić uwagę partycji trwa jednostki logicznej, która zawiera co najmniej jedno wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="c141f-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="c141f-114">Rysunek 1 pokazuje usługi bezstanowej wystąpieniami pięć dystrybuowana do klastra przy użyciu jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Usługi bezstanowej](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="c141f-116">Naprawdę są dwa typy rozwiązań usług bezstanowych.</span><span class="sxs-lookup"><span data-stu-id="c141f-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="c141f-117">Witaj najpierw jeden to usługa, która będzie się powtarzał stanu zewnętrznie, na przykład w bazie danych Azure SQL (np. sieci Web, która przechowuje informacje o sesji hello i danych).</span><span class="sxs-lookup"><span data-stu-id="c141f-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="c141f-118">Hello drugim jest tylko do obliczenia usług (takich jak obraz lub Kalkulator tworzenie miniatur) nie zarządzających każdy stan trwały.</span><span class="sxs-lookup"><span data-stu-id="c141f-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="c141f-119">W przypadku partycjonowania usługi bezstanowej jest bardzo rzadko scenariusza — skalowalność i dostępność zwykle są osiągane przez dodanie więcej wystąpień.</span><span class="sxs-lookup"><span data-stu-id="c141f-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="c141f-120">czas tylko Hello ma tooconsider jest wiele partycji dla wystąpień usługi bezstanowej, gdy potrzebne są specjalne routingu toomeet żądań.</span><span class="sxs-lookup"><span data-stu-id="c141f-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="c141f-121">Na przykład należy wziąć pod uwagę przypadek, w którym użytkownicy z identyfikatorami w pewnym powinien być obsługiwany tylko przez wystąpienie określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="c141f-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="c141f-122">Innym przykładem po można partycji usługi bezstanowej jest masz naprawdę partycjonowanej wewnętrznej bazy danych (np. podzielony na niezależne fragmenty bazy danych SQL) i ma toocontrol wystąpieniu usługi, z którym należy zapisać toohello niezależnego fragmentu bazy danych — lub wykonywać inne zadania przygotowywania w Witaj usługi bezstanowej, która wymaga hello takie same informacje o partycjach jest używany w hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c141f-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="c141f-123">Tego typu scenariusze można także rozwiązać na różne sposoby i nie wymagają partycjonowania usługi.</span><span class="sxs-lookup"><span data-stu-id="c141f-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="c141f-124">Witaj pozostałej części tego przewodnika koncentruje się na usług stanowych.</span><span class="sxs-lookup"><span data-stu-id="c141f-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="c141f-125">Usługi stanowej partycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c141f-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="c141f-126">Sieć szkieletowa usług ułatwia skalowalnych usług stanowych łatwe toodevelop oferując najwyższej jakości sposób toopartition stanu (dane).</span><span class="sxs-lookup"><span data-stu-id="c141f-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="c141f-127">Koncepcyjnie, należy zwrócić uwagę partycji usługi stanowej jako jednostkę skalowania, która jest wysoce niezawodne za pośrednictwem [replik](service-fabric-availability-services.md) rozproszonych, się równoważone hello węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c141f-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="c141f-128">Podział na partycje w kontekście hello usługi sieć szkieletowa usług stanowych odwołuje się toohello proces określania, czy partycja określonej usługi jest odpowiedzialny za część hello stan ukończenia hello usługi.</span><span class="sxs-lookup"><span data-stu-id="c141f-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="c141f-129">(Jak wspomniano wcześniej, partycji jest zestawem [replik](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="c141f-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="c141f-130">Największą zaletą sieci szkieletowej usług jest umieszczenie hello partycji, w różnych węzłach.</span><span class="sxs-lookup"><span data-stu-id="c141f-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="c141f-131">Dzięki temu są limit zasobów toogrow tooa węzła.</span><span class="sxs-lookup"><span data-stu-id="c141f-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="c141f-132">Potrzeb danych hello powiększania, partycje wzrostu i sieci szkieletowej usług rebalances partycji w węzłach.</span><span class="sxs-lookup"><span data-stu-id="c141f-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="c141f-133">Dzięki temu hello nadal efektywne wykorzystanie zasobów sprzętowych.</span><span class="sxs-lookup"><span data-stu-id="c141f-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="c141f-134">toogive możesz przykład powiedzieć możesz rozpoczyna się od 5 węzłów klastra i usługi, która jest skonfigurowany toohave 10 partycji i elementem docelowym trzy repliki.</span><span class="sxs-lookup"><span data-stu-id="c141f-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="c141f-135">W takim przypadku sieci szkieletowej usług może równoważyć i rozpowszechniają replik hello klastra hello — i pojawiłyby się dwóch podstawowych [replik](service-fabric-availability-services.md) na węzeł.</span><span class="sxs-lookup"><span data-stu-id="c141f-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="c141f-136">Teraz tooscale limit hello too10 węzłach, należy sieci szkieletowej usług będzie ponowne zrównoważenie podstawowy hello [replik](service-fabric-availability-services.md) we wszystkich węzłach 10.</span><span class="sxs-lookup"><span data-stu-id="c141f-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="c141f-137">Podobnie skalowania wstecz too5 węzłów, sieci szkieletowej usług będzie ponowne zrównoważenie wszystkie repliki hello węzłów hello 5.</span><span class="sxs-lookup"><span data-stu-id="c141f-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="c141f-138">Rysunek 2 przedstawia dystrybucji hello 10 partycji przed i po skalowanie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="c141f-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![Usługi stanowej](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="c141f-140">W związku z tym uzyskuje się hello skalowalnego w poziomie, ponieważ żądania klientów są rozproszone na komputerach, poprawia ogólną wydajność aplikacji hello i zmniejsza się rywalizacji toochunks dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="c141f-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="c141f-141">Planowanie podziału na partycje</span><span class="sxs-lookup"><span data-stu-id="c141f-141">Plan for partitioning</span></span>
<span data-ttu-id="c141f-142">Przed wdrożeniem usługi, zawsze należy rozważyć hello partycjonowania strategii, która jest wymagana tooscale wychodzących. Istnieją różne sposoby, ale ich wszystkich skupić się na jakie aplikacja hello musi tooachieve.</span><span class="sxs-lookup"><span data-stu-id="c141f-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="c141f-143">Dla kontekstu hello w tym artykule zastanówmy się niektóre hello aspekty większe znaczenie.</span><span class="sxs-lookup"><span data-stu-id="c141f-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="c141f-144">Dobrym rozwiązaniem jest toothink informacje o strukturze hello hello stanu, który wymaga toobe podzielona na partycje, jako pierwszy krok hello.</span><span class="sxs-lookup"><span data-stu-id="c141f-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="c141f-145">Spójrzmy prosty przykład.</span><span class="sxs-lookup"><span data-stu-id="c141f-145">Let's take a simple example.</span></span> <span data-ttu-id="c141f-146">Gdyby toobuild usługę countywide sondowania, można utworzyć partycji każdemu miastu w hello województwo.</span><span class="sxs-lookup"><span data-stu-id="c141f-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="c141f-147">Następnie można przechowywać hello głosów dla każdej osoby w mieście hello w hello partycji, która odpowiada toothat miasta.</span><span class="sxs-lookup"><span data-stu-id="c141f-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="c141f-148">Rysunek 3 przedstawia zestaw miasta osoby i hello, w którym znajdują się.</span><span class="sxs-lookup"><span data-stu-id="c141f-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![Proste partycji](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="c141f-150">Jako różni populacji hello miast, może to spowodować niektóre partycje, które zawierają dużą ilość danych (np. Seattle) i innych partycji z bardzo mało stanu (np. Kirkland).</span><span class="sxs-lookup"><span data-stu-id="c141f-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="c141f-151">Co to jest wpływ hello partycji z nierówna ilości stan?</span><span class="sxs-lookup"><span data-stu-id="c141f-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="c141f-152">Jeśli myślisz o przykład Witaj ponownie, można łatwo zobaczyć, czy hello partycji, która przetrzymuje hello głosami Seattle otrzymają więcej ruchu niż Kirkland hello, co.</span><span class="sxs-lookup"><span data-stu-id="c141f-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="c141f-153">Domyślnie usługa sieć szkieletowa sprawia, że upewnić się, że o hello tej samej liczby podstawowych i pomocniczych replik w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="c141f-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="c141f-154">Dlatego użytkownik może pozostać z węzłami zawierających repliki obsługujących więcej ruchu oraz inne osoby, które obsługiwać mniej ruchu.</span><span class="sxs-lookup"><span data-stu-id="c141f-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="c141f-155">Najlepiej warto tooavoid gorących i zimnych miejsc, takich jak to w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c141f-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="c141f-156">W celu tooavoid to, z punktu widzenia partycjonowania należy wykonać dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="c141f-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="c141f-157">Spróbuj toopartition hello stanu, dzięki czemu jest rozmieszczana równomiernie wzdłuż wszystkie partycje.</span><span class="sxs-lookup"><span data-stu-id="c141f-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="c141f-158">Załaduj raport z każdej repliki hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="c141f-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="c141f-159">(Aby uzyskać informacje na temat, zapoznaj się w tym artykule na [metryki i obciążenia](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="c141f-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="c141f-160">Usługi Service Fabric zawiera obciążenia tooreport możliwości hello wykorzystanych w ramach usług, takich jak ilość pamięci lub liczbę rekordów.</span><span class="sxs-lookup"><span data-stu-id="c141f-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="c141f-161">Oparte na powitania metryki zgłoszone, sieci szkieletowej usług wykryje, że niektóre partycje służy obciążeń wyższe niż inne i rebalances hello klastra przez przenoszenie replik toomore odpowiedniego węzły tak, aby ogólna żaden węzeł nie jest przeciążona.</span><span class="sxs-lookup"><span data-stu-id="c141f-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="c141f-162">Czasami nie wiedzieć, jak dużo danych będzie w danej partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="c141f-163">Dzięki ogólne zalecenie jest toodo zarówno — najpierw, przyjmując strategii partycjonowania które rozprzestrzeniają się hello danych równomiernie między hello partycji i sekundę, przez raportowania obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c141f-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="c141f-164">Pierwsza metoda Hello zapobiega sytuacji opisanych w hello głosowania przykład, gdy hello drugi pomaga smooth różnic tymczasowego dostępu lub obciążenia wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="c141f-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="c141f-165">Innym aspektem planowania partycji jest toochoose hello poprawną liczbę partycji toobegin z.</span><span class="sxs-lookup"><span data-stu-id="c141f-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="c141f-166">Z punktu widzenia usługi sieć szkieletowa nie ma nic uniemożliwiający uruchamiania o większej liczby partycji niż zakładano dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c141f-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="c141f-167">W rzeczywistości przy założeniu hello maksymalną liczbę partycji jest prawidłowy podejście.</span><span class="sxs-lookup"><span data-stu-id="c141f-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="c141f-168">W rzadkich przypadkach może to spowodować wymagające partycje więcej niż początkowo wybrana.</span><span class="sxs-lookup"><span data-stu-id="c141f-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="c141f-169">Liczba partycji hello nie można zmienić po hello fakt, będzie potrzebny tooapply podejścia niektórych zaawansowanych partycji, takich jak tworzenie nowego wystąpienia usługi hello sam typ usługi.</span><span class="sxs-lookup"><span data-stu-id="c141f-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="c141f-170">Musisz także tooimplement niektórych logiki po stronie klienta, który przekierowuje hello żądań wystąpienie usługi poprawne toohello, na podstawie wiedzy po stronie klienta, który musi obsługiwać kodu klienta.</span><span class="sxs-lookup"><span data-stu-id="c141f-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="c141f-171">Inną ważną kwestią dotyczącą partycjonowania planowania jest hello komputera dostępne zasoby.</span><span class="sxs-lookup"><span data-stu-id="c141f-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="c141f-172">Stan hello potrzeb toobe dostępne i przechowywane, jest powiązane toofollow:</span><span class="sxs-lookup"><span data-stu-id="c141f-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="c141f-173">Limity przepustowości sieci</span><span class="sxs-lookup"><span data-stu-id="c141f-173">Network bandwidth limits</span></span>
* <span data-ttu-id="c141f-174">Limity pamięci systemu</span><span class="sxs-lookup"><span data-stu-id="c141f-174">System memory limits</span></span>
* <span data-ttu-id="c141f-175">Limity magazynu na dysku</span><span class="sxs-lookup"><span data-stu-id="c141f-175">Disk storage limits</span></span>

<span data-ttu-id="c141f-176">Dlatego co się stanie po uruchomieniu na ograniczenia zasobów w klastrze uruchomione? odpowiedź Hello jest, może po prostu skalowanie w poziomie hello klastra tooaccommodate hello nowe wymagania.</span><span class="sxs-lookup"><span data-stu-id="c141f-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="c141f-177">[Przewodnik planowania pojemności Hello](service-fabric-capacity-planning.md) zawiera wskazówki dotyczące toodetermine liczbę węzłów klastra musi.</span><span class="sxs-lookup"><span data-stu-id="c141f-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="c141f-178">Wprowadzenie do partycjonowania</span><span class="sxs-lookup"><span data-stu-id="c141f-178">Get started with partitioning</span></span>
<span data-ttu-id="c141f-179">W tej sekcji opisano, jak tooget pracę z usługą partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="c141f-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="c141f-180">Sieć szkieletowa usług oferuje możliwość wyboru trzy schemat partycji:</span><span class="sxs-lookup"><span data-stu-id="c141f-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="c141f-181">W granicach partycjonowanie (znany także jako UniformInt64Partition).</span><span class="sxs-lookup"><span data-stu-id="c141f-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="c141f-182">O nazwie partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="c141f-182">Named partitioning.</span></span> <span data-ttu-id="c141f-183">Aplikacje zazwyczaj przy użyciu tego modelu istnieją dane, które można bucketed w ramach ograniczonego zestawu.</span><span class="sxs-lookup"><span data-stu-id="c141f-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="c141f-184">Typowe przykłady pola danych używane jako klucze partycji o nazwie będzie regionów, kodów pocztowych, grupy odbiorców lub granice innych firm.</span><span class="sxs-lookup"><span data-stu-id="c141f-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="c141f-185">Pojedyncze partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="c141f-185">Singleton partitioning.</span></span> <span data-ttu-id="c141f-186">Pojedyncze partycje są zazwyczaj używane do usługi hello nie wymaga żadnych dodatkowych routingu.</span><span class="sxs-lookup"><span data-stu-id="c141f-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="c141f-187">Na przykład usług bezstanowych Użyj ten schemat partycjonowania domyślnie.</span><span class="sxs-lookup"><span data-stu-id="c141f-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="c141f-188">O nazwie i schematy partycjonowania Singleton to specjalne rodzaje ranged partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="c141f-189">Domyślnie hello szablony Visual Studio do użytku w sieci szkieletowej usług w granicach partycje, ponieważ jest on hello najczęstszych i najbardziej przydatnych jeden.</span><span class="sxs-lookup"><span data-stu-id="c141f-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="c141f-190">Witaj dalszej części tego artykułu koncentruje się na powitania ranged schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="c141f-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="c141f-191">Schemat partycjonowania w granicach</span><span class="sxs-lookup"><span data-stu-id="c141f-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="c141f-192">Jest to używane toospecify całkowitą zakresu (określone przez niska wartość klucza i wysoka wartość klucza) i liczba partycji (n).</span><span class="sxs-lookup"><span data-stu-id="c141f-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="c141f-193">Tworzy partycje n, każdy odpowiedzialny za nienakładający tekst Podzakres hello zakresem kluczy partycji: Ogólne.</span><span class="sxs-lookup"><span data-stu-id="c141f-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="c141f-194">Na przykład ranged schemat partycjonowania kluczem niski 0, wysoka wartość klucza 99 oraz liczbę 4 utworzyć cztery partycje, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c141f-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Zakres partycji](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="c141f-196">Typowym podejściem jest toocreate skrót oparte na zestawie danych hello Unikatowy klucz.</span><span class="sxs-lookup"><span data-stu-id="c141f-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="c141f-197">Typowe przykłady klucze będą numer identyfikacyjny (VIN), identyfikator pracownika i unikatowym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="c141f-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="c141f-198">Za pomocą tego Unikatowy klucz, czy następnie wygenerować skrótu, modulo hello klucza zakresu, toouse jako klucz.</span><span class="sxs-lookup"><span data-stu-id="c141f-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="c141f-199">Można określić hello górne i dolne granice hello dopuszczalny zakres klucza.</span><span class="sxs-lookup"><span data-stu-id="c141f-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="c141f-200">Wybierz algorytm wyznaczania wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="c141f-200">Select a hash algorithm</span></span>
<span data-ttu-id="c141f-201">Ważnym elementem wyznaczania wartości skrótu jest wybranie sieci algorytmu wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="c141f-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="c141f-202">Wchodzi w grę jest czy hello celem jest podobnych kluczy toogroup obok siebie (miejscowości poufnych wyznaczania wartości skrótu)--lub jeśli działanie powinien zostać przekazany szeroko wszystkich partycji (dystrybucji mieszania), która jest najczęściej.</span><span class="sxs-lookup"><span data-stu-id="c141f-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="c141f-203">właściwości Hello dobrej algorytmu wyznaczania wartości skrótu są jest łatwe toocompute, składa się z kilku kolizji i rozpowszechnia klucze hello równomiernie.</span><span class="sxs-lookup"><span data-stu-id="c141f-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="c141f-204">Dobrym przykładem algorytmu wyznaczania wartości skrótu wydajne jest hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algorytmu wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="c141f-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="c141f-205">Hello jest dobrym zasobu dla skrótu ogólne kod algorytmu opcji [Wikipedia strony na funkcje skrótu](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="c141f-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="c141f-206">Tworzenie usługi stanowej z wieloma partycjami</span><span class="sxs-lookup"><span data-stu-id="c141f-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="c141f-207">Utwórz pierwszy niezawodnej usługi stanowej z wieloma partycjami.</span><span class="sxs-lookup"><span data-stu-id="c141f-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="c141f-208">W tym przykładzie utworzysz bardzo prostej aplikacji, w którym ma być toostore wszystkich ostatnich o nazwach zaczynających hello sam list w hello tej samej partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="c141f-209">Przed przystąpieniem do napisania kodu, należy toothink dotyczące hello partycji i kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="c141f-210">Potrzebne są 26 partycje, (po jednej dla każdej litery alfabetu hello), ale co o hello niski i wysoki klucz?</span><span class="sxs-lookup"><span data-stu-id="c141f-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="c141f-211">Ponieważ chcemy dosłownie toohave jedną partycję na literę, możemy użyć 0 jako hello niska wartość klucza i 25 jako hello wysoka wartość klucza, jak litera każdego jest własnego klucza.</span><span class="sxs-lookup"><span data-stu-id="c141f-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="c141f-212">To jest uproszczone scenariusz, w rzeczywistości byłoby nierówna dystrybucja hello.</span><span class="sxs-lookup"><span data-stu-id="c141f-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="c141f-213">Nazwisk, począwszy od litery hello "S" lub "M" są częściej niż hello te począwszy "X" lub "Y".</span><span class="sxs-lookup"><span data-stu-id="c141f-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="c141f-214">Otwórz **programu Visual Studio** > **pliku** > **nowe** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="c141f-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="c141f-215">W hello **nowy projekt** oknie dialogowym Wybierz hello sieci szkieletowej usług aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c141f-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="c141f-216">Wywołanie "AlphabetPartitions" hello projektu.</span><span class="sxs-lookup"><span data-stu-id="c141f-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="c141f-217">W hello **Tworzenie usługi** oknie dialogowym wybierz **Stateful** usługi i wywołać go "Alphabet.Processing", jak pokazano w poniższym obrazie hello.</span><span class="sxs-lookup"><span data-stu-id="c141f-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="c141f-218">![Okno dialogowe nowej usługi w programie Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="c141f-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="c141f-219">Ustaw numer hello partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-219">Set hello number of partitions.</span></span> <span data-ttu-id="c141f-220">Otwórz hello pliku Applicationmanifest.xml się w hello folderu ApplicationPackageRoot hello AlphabetPartitions projektu i zaktualizuj hello parametru too26 Processing_PartitionCount, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c141f-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="c141f-221">Należy również tooupdate hello LowKey i właściwości HighKey elementu klasy StatefulService hello w hello ApplicationManifest.xml, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c141f-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="c141f-222">Dla toobe usługi hello jest dostępny otwarcie punktu końcowego na porcie przez dodanie elementu punktu końcowego hello ServiceManifest.xml (znajdujący się w folderze elementu PackageRoot hello) dla hello Alphabet.Processing usługi, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c141f-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="c141f-223">Obecnie usługa hello jest skonfigurowany toolisten tooan wewnętrzny punkt końcowy z partycjami 26.</span><span class="sxs-lookup"><span data-stu-id="c141f-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="c141f-224">Następnie należy toooverride hello `CreateServiceReplicaListeners()` metody klasy hello przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c141f-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c141f-225">Dla tego przykładu przyjęto założenie, używasz HttpCommunicationListener proste.</span><span class="sxs-lookup"><span data-stu-id="c141f-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="c141f-226">Aby uzyskać więcej informacji dotyczących komunikacji niezawodnej usługi, zobacz [model komunikacji niezawodnej usługi hello](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="c141f-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="c141f-227">Zalecane wzorzec hello adresu URL, który nasłuchuje repliki jest zgodny z formatem hello: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="c141f-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="c141f-228">Dlatego ma tooconfigure toolisten odbiornik komunikacji na powitania poprawne punktów końcowych i z tego wzorca.</span><span class="sxs-lookup"><span data-stu-id="c141f-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="c141f-229">Wiele replik tej usługi może być hostowana na powitania tym samym komputerze, więc ten adres musi toobe unikatowy toohello repliki.</span><span class="sxs-lookup"><span data-stu-id="c141f-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="c141f-230">Jest to, dlaczego identyfikator partycji: + identyfikator repliki są w adresie URL hello.</span><span class="sxs-lookup"><span data-stu-id="c141f-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="c141f-231">HttpListener może nasłuchiwać na wielu adresów w powitalne portu takie same jak prefiksu adresu URL hello jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="c141f-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="c141f-232">Witaj, dodatkowe identyfikator GUID jest przeznaczony dla zaawansowanych case, gdzie również nasłuchiwanie żądań tylko do odczytu replikach pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="c141f-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="c141f-233">W takim przypadku hello ma toomake się, że nowy unikatowy adres jest używany podczas przejścia z podstawowego toosecondary tooforce klientów toore rozwiązanie hello adresu.</span><span class="sxs-lookup"><span data-stu-id="c141f-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="c141f-234">jest używany jako adres hello tutaj, aby hello funkcja replica nasłuchuje na wszystkich dostępnych hostów (IP, FQDM, localhost itp.) hello kod poniżej przedstawiono przykład ' +'.</span><span class="sxs-lookup"><span data-stu-id="c141f-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="c141f-235">Warto również zauważyć tego hello opublikowane adres URL jest nieco inne niż hello nasłuchiwania prefiksu adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c141f-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="c141f-236">adres URL nasłuchiwania Hello otrzymuje tooHttpListener.</span><span class="sxs-lookup"><span data-stu-id="c141f-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="c141f-237">Witaj, opublikowanego adresu URL jest hello adresu URL opublikowanego toohello Usługa nazewnictwa sieci szkieletowej usług, który służy do odnajdywania usługi.</span><span class="sxs-lookup"><span data-stu-id="c141f-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="c141f-238">Ten adres za pomocą usługi odnajdywania poprosi klientów.</span><span class="sxs-lookup"><span data-stu-id="c141f-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="c141f-239">adres Hello, że klienci otrzymują potrzeb toohave hello rzeczywisty adres IP lub nazwa FQDN węzła hello tooconnect kolejności.</span><span class="sxs-lookup"><span data-stu-id="c141f-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="c141f-240">Dlatego należy tooreplace "+" z hello węzła IP lub nazwa FQDN jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="c141f-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="c141f-241">ostatni krok Hello jest hello tooadd przetwarzania logiki toohello usługi jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c141f-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="c141f-242">`ProcessInternalRequest`Odczyty hello wartości hello zapytania ciąg używany parametr toocall hello partycji i wywołania `AddUserAsync` tooadd hello nazwisko toohello niezawodnej słownika `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="c141f-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="c141f-243">Dodajmy toosee projektu toohello usługi bezstanowej sposób może wywołać określonej partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="c141f-244">Ta usługa służy jako prosty interfejs sieci web akceptuje nazwisko hello jako parametr ciągu zapytania, określa hello klucz partycji i wysyła je toohello Alphabet.Processing usługi do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c141f-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="c141f-245">W hello **Tworzenie usługi** oknie dialogowym wybierz **Stateless** usługi i nadaj mu "Alphabet.Web", jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c141f-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Zrzut ekranu usługi bezstanowej](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="c141f-247">.</span><span class="sxs-lookup"><span data-stu-id="c141f-247">.</span></span>
12. <span data-ttu-id="c141f-248">Zaktualizuj informacje o punkcie końcowym hello w hello ServiceManifest.xml hello Alphabet.WebApi usługi tooopen zapasowej portu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c141f-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="c141f-249">Należy tooreturn kolekcję ServiceInstanceListeners w klasie hello sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c141f-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="c141f-250">Ponownie możesz wybrać tooimplement HttpCommunicationListener proste.</span><span class="sxs-lookup"><span data-stu-id="c141f-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="c141f-251">Teraz należy tooimplement hello przetwarzania logiki.</span><span class="sxs-lookup"><span data-stu-id="c141f-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="c141f-252">Witaj wywołania HttpCommunicationListener `ProcessInputRequest` gdy nadejdzie żądanie.</span><span class="sxs-lookup"><span data-stu-id="c141f-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="c141f-253">Dlatego spróbuj teraz i Dodaj poniższy kod hello.</span><span class="sxs-lookup"><span data-stu-id="c141f-253">So let's go ahead and add hello code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="c141f-254">Przejdźmy krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="c141f-254">Let's walk through it step by step.</span></span> <span data-ttu-id="c141f-255">Kod Hello odczytuje hello pierwszą literę parametru ciągu zapytania hello `lastname` na wartość typu char.</span><span class="sxs-lookup"><span data-stu-id="c141f-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="c141f-256">Następnie określa klucz partycji hello na list przez odjęcie wartości szesnastkowej hello `A` z wartości szesnastkowej hello hello nazwisk pierwszą literę.</span><span class="sxs-lookup"><span data-stu-id="c141f-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="c141f-257">Pamiętaj, że w tym przykładzie używamy 26 partycje z jedną partycję kluczem dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="c141f-258">Następnie możemy uzyskać partycji usługi hello `partition` dla tego klucza przy użyciu hello `ResolveAsync` metody na powitania `servicePartitionResolver` obiektu.</span><span class="sxs-lookup"><span data-stu-id="c141f-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="c141f-259">`servicePartitionResolver`nie zdefiniowano jako</span><span class="sxs-lookup"><span data-stu-id="c141f-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="c141f-260">Witaj `ResolveAsync` identyfikator URI usługi hello ma metodę, hello klucz partycji i token anulowania jako parametry.</span><span class="sxs-lookup"><span data-stu-id="c141f-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="c141f-261">Witaj identyfikator URI usługi hello usługę przetwarzania jest `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="c141f-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="c141f-262">Następnie Pobierz punktu końcowego hello hello partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="c141f-263">Na koniec możemy utworzyć adres URL punktu końcowego hello plus hello querystring i Wywołaj hello usługę przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c141f-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="c141f-264">Po zakończeniu przetwarzania hello możemy zapisywać dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="c141f-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="c141f-265">ostatni krok Hello jest tootest hello usługi.</span><span class="sxs-lookup"><span data-stu-id="c141f-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="c141f-266">Visual Studio korzysta parametry aplikacji dla lokalnych i chmurze wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c141f-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="c141f-267">Usługa hello tootest z partycjami 26 lokalnie, należy tooupdate hello `Local.xml` plików w folderze ApplicationParameters hello hello AlphabetPartitions projektu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c141f-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="c141f-268">Po zakończeniu wdrażania możesz sprawdzić hello usługi i wszystkie jego partycji w hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="c141f-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Zrzut ekranu Eksploratora usługi sieć szkieletowa](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="c141f-270">W przeglądarce, należy przetestować hello partycjonowania logiki wprowadzając `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="c141f-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="c141f-271">Zobaczysz, że każdy nazwisko zaczynającym się znakiem hello tej samej litery są przechowywane w hello tej samej partycji.</span><span class="sxs-lookup"><span data-stu-id="c141f-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![Zrzut ekranu przeglądarki](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="c141f-273">Kod źródłowy całego Hello próbki hello jest dostępne na [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="c141f-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c141f-274">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c141f-274">Next steps</span></span>
<span data-ttu-id="c141f-275">Dla informacji na temat pojęć sieci szkieletowej usług zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c141f-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="c141f-276">Dostępność usług sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c141f-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="c141f-277">Skalowalność usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c141f-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="c141f-278">Planowanie wydajności dla aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c141f-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png