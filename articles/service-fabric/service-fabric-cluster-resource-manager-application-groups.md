---
title: "aaaService Menedżer zasobów klastra sieci szkieletowej — grup aplikacji | Dokumentacja firmy Microsoft"
description: "Omówienie hello funkcji grupy aplikacji hello zasobu klastra sieci szkieletowej programu Service Manager"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="6c927-103">Wprowadzenie tooApplication grup</span><span class="sxs-lookup"><span data-stu-id="6c927-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="6c927-104">Menedżer zasobów klastra usługi sieć szkieletowa zwykle zarządza zasobami klastra przez rozłożenie obciążenia hello (reprezentowane przez [metryki](service-fabric-cluster-resource-manager-metrics.md)) równomiernie w całej hello klastra.</span><span class="sxs-lookup"><span data-stu-id="6c927-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="6c927-105">Usługa Service Fabric zarządza pojemności hello węzłów hello hello i klastrze hello jako całość przy użyciu [pojemności](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="6c927-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="6c927-106">Metryki i wydajność pracy wygodne w przypadku wielu obciążeń, ale wzorców, które w znacznym stopniu wykorzystywane różnych wystąpień aplikacji sieci szkieletowej usług czasami przenieść dodatkowe wymagania.</span><span class="sxs-lookup"><span data-stu-id="6c927-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="6c927-107">Na przykład można:</span><span class="sxs-lookup"><span data-stu-id="6c927-107">For example you may want to:</span></span>

- <span data-ttu-id="6c927-108">Niektóre wydajność hello węzłach klastra hello hello usług w ramach wystąpienia niektórych aplikacji o nazwie rezerwowa</span><span class="sxs-lookup"><span data-stu-id="6c927-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="6c927-109">Ogranicz hello całkowitą liczbę węzłów, które usługi hello w wystąpieniu o nazwie aplikacji są uruchomione na (zamiast rozkładanie je za pośrednictwem hello całego klastra)</span><span class="sxs-lookup"><span data-stu-id="6c927-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="6c927-110">Definiowanie pojemności na powitania aplikacji nazwane wystąpienie toolimit hello liczbę usług lub Suma zużycie zasobów usług hello w nim</span><span class="sxs-lookup"><span data-stu-id="6c927-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="6c927-111">toomeet tych wymagań, hello zasobu klastra sieci szkieletowej programu Service Manager obsługuje funkcję grupy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="6c927-112">Ograniczanie hello maksymalna liczba węzłów</span><span class="sxs-lookup"><span data-stu-id="6c927-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="6c927-113">Witaj najprostszym przypadek użycia pojemności aplikacji jest gdy wystąpienie aplikacji musi toobe ograniczone tooa niektórych maksymalną liczbę węzłów.</span><span class="sxs-lookup"><span data-stu-id="6c927-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="6c927-114">Zakłada skonsolidowanie obsługi wszystkich usług w ramach danego wystąpienia aplikacji na zestaw liczby maszyn.</span><span class="sxs-lookup"><span data-stu-id="6c927-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="6c927-115">Konsolidacja jest przydatne, gdy próbujesz toopredict lub cap użycia zasobów fizycznych przez usługi hello w ramach tego wystąpienia nazwanego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="6c927-116">Witaj poniższy obraz przedstawia wystąpienie aplikacji z włączonymi i wyłączonymi maksymalną liczbę węzłów zdefiniowane:</span><span class="sxs-lookup"><span data-stu-id="6c927-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="6c927-117"><center>
![Maksymalna liczba węzłów Definiowanie wystąpienia aplikacji][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="6c927-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="6c927-118">W przykładzie po lewej stronie powitania aplikacji hello nie ma maksymalną liczbę węzłów zdefiniowane, i ma trzy usługi.</span><span class="sxs-lookup"><span data-stu-id="6c927-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="6c927-119">Witaj Menedżera zasobów klastra ma rozszerzane wszystkie repliki na sześciu dostępne węzły tooachieve hello równowagę w klastrze hello (hello domyślne zachowanie).</span><span class="sxs-lookup"><span data-stu-id="6c927-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="6c927-120">W przykładzie prawo hello widzimy hello węzłów toothree ograniczone tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="6c927-121">Parametr Hello, który kontroluje to zachowanie jest nazywany wartość MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="6c927-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="6c927-122">Ten parametr można ustawić podczas tworzenia aplikacji lub aktualizacji dla wystąpienia aplikacji, która została już uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6c927-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="6c927-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c927-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="6c927-124">C#</span><span class="sxs-lookup"><span data-stu-id="6c927-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="6c927-125">W ramach hello zestawu węzłów hello Menedżera zasobów klastra nie gwarantuje obiekty, które usługa uzyskać umieszczone razem lub pobrać używane węzły, które.</span><span class="sxs-lookup"><span data-stu-id="6c927-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="6c927-126">Metryki aplikacji, obciążenia i pojemności</span><span class="sxs-lookup"><span data-stu-id="6c927-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="6c927-127">Grupy aplikacji pozwalają również metryki toodefine skojarzonych z wystąpienia danej aplikacji o nazwie i wydajności danego wystąpienia aplikacji dla tych metryki.</span><span class="sxs-lookup"><span data-stu-id="6c927-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="6c927-128">Metryki aplikacji pozwalają tootrack, rezerwy oraz zużycie zasobów hello limit usług hello wewnątrz tego wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="6c927-129">Dla każdej aplikacji metryki istnieją dwie wartości, które można ustawić:</span><span class="sxs-lookup"><span data-stu-id="6c927-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="6c927-130">**Całkowita liczba aplikacji, zdolność** — to ustawienie reprezentuje hello całkowita pojemność aplikacji hello dla określonej metryki.</span><span class="sxs-lookup"><span data-stu-id="6c927-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="6c927-131">Hello Menedżera zasobów klastra nie zezwala na powitania tworzenia nowych usług, w ramach tego wystąpienia aplikacji, spowodowałoby tooexceed całkowite obciążenie tej wartości.</span><span class="sxs-lookup"><span data-stu-id="6c927-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="6c927-132">Na przykład załóżmy, że wystąpienie aplikacji hello pojemności 10 ma już obciążenia pięć.</span><span class="sxs-lookup"><span data-stu-id="6c927-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="6c927-133">Hello tworzenia usługi z obciążeniem całkowita domyślne 10 będzie niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="6c927-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="6c927-134">**Maksymalna pojemność węzła** — to ustawienie określa maksymalne obciążenie całkowita hello aplikacji hello w jednym węźle.</span><span class="sxs-lookup"><span data-stu-id="6c927-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="6c927-135">Jeśli obciążenie odbywa się za pośrednictwem tej pojemności, hello Menedżera zasobów klastra przenosi węzłów tooother repliki tak, aby hello obciążenia zmniejsza.</span><span class="sxs-lookup"><span data-stu-id="6c927-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="6c927-136">Środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6c927-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="6c927-137">C#:</span><span class="sxs-lookup"><span data-stu-id="6c927-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="6c927-138">Rezerwacji pojemności</span><span class="sxs-lookup"><span data-stu-id="6c927-138">Reserving Capacity</span></span>
<span data-ttu-id="6c927-139">Inne typowe zastosowanie dla grup aplikacji jest tooensure, że zasoby w hello klastra są zastrzeżone dla wystąpienia danej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="6c927-140">Po utworzeniu wystąpienia aplikacji hello, zawsze jest zarezerwowane miejsce Hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="6c927-141">Rezerwacji miejsca w klastrze powitania dla aplikacji hello się natychmiast stanie nawet wtedy, gdy:</span><span class="sxs-lookup"><span data-stu-id="6c927-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="6c927-142">wystąpienie aplikacji Hello jest tworzony, ale nie ma jeszcze żadnych usług w niej</span><span class="sxs-lookup"><span data-stu-id="6c927-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="6c927-143">Witaj liczba usług w ramach zmian wystąpienia aplikacji hello zawsze</span><span class="sxs-lookup"><span data-stu-id="6c927-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="6c927-144">Witaj usługi istnieje, ale nie korzysta z zasobów hello</span><span class="sxs-lookup"><span data-stu-id="6c927-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="6c927-145">Rezerwacji zasobów dla wystąpienia aplikacji wymaga określenia dwóch dodatkowych parametrów: *MinimumNodes* i *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="6c927-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="6c927-146">**Wartość MinimumNodes** — definiuje hello minimalna liczba węzłów, które aplikacji hello wystąpienia nie powinna działać.</span><span class="sxs-lookup"><span data-stu-id="6c927-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="6c927-147">**NodeReservationCapacity** — jest to ustawienie na metrykę dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="6c927-148">wartość Hello jest hello ilość tego Metryka zastrzeżone dla aplikacji hello w każdym węźle, w przypadku, gdy hello usług w tej aplikacji, uruchom.</span><span class="sxs-lookup"><span data-stu-id="6c927-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="6c927-149">Łączenie **MinimumNodes** i **NodeReservationCapacity** gwarancje rezerwacji minimalna obciążenia dla aplikacji hello w ramach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="6c927-150">W przypadku pozostałych mniej pojemności w hello klastra niż wymagana Rezerwacja całkowita hello, tworzenie aplikacji hello zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="6c927-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="6c927-151">Oto przykład rezerwacji pojemności:</span><span class="sxs-lookup"><span data-stu-id="6c927-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="6c927-152"><center>
![Definiowanie pojemności zastrzeżone wystąpień aplikacji][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="6c927-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="6c927-153">W przykładzie po lewej stronie powitania aplikacji nie mają żadnych zdefiniowano zdolności produkcyjnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="6c927-154">Witaj Menedżera zasobów klastra równoważy wszystko zgodnie z zasadami toonormal.</span><span class="sxs-lookup"><span data-stu-id="6c927-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="6c927-155">W przykładzie hello na powitania prawo Załóżmy, że czy Application1 został utworzony z hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="6c927-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="6c927-156">Wartość MinimumNodes tootwo zestawu</span><span class="sxs-lookup"><span data-stu-id="6c927-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="6c927-157">Metryka zdefiniowana z aplikacji</span><span class="sxs-lookup"><span data-stu-id="6c927-157">An application Metric defined with</span></span>
  - <span data-ttu-id="6c927-158">NodeReservationCapacity 20</span><span class="sxs-lookup"><span data-stu-id="6c927-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="6c927-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c927-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="6c927-160">C#</span><span class="sxs-lookup"><span data-stu-id="6c927-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="6c927-161">Sieć szkieletowa usług rezerw pojemności na dwóch węzłów w Application1 i nie można używać usług z tooconsume Aplikacja2 wydajność nawet jeśli istnieją takie obciążenia jest są używane przez usługi hello wewnątrz Application1 w czasie hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="6c927-162">Pojemność ten zastrzeżony aplikacji jest uznawany za używane i hello pozostająca w tym węźle, a w ramach klastra hello jest za mała.</span><span class="sxs-lookup"><span data-stu-id="6c927-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="6c927-163">zastrzeżenie Hello jest odejmowany od hello pozostająca klastra natychmiast, jednak zastrzeżone hello zużycie jest odejmowany od pojemności hello określonego węzła tylko wtedy, gdy co najmniej jedną usługę obiekt znajduje się na nim.</span><span class="sxs-lookup"><span data-stu-id="6c927-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="6c927-164">Tego zastrzeżenia nowsze umożliwia elastyczność i lepsze wykorzystanie zasobów, ponieważ zasoby są tylko zarezerwowane na węzłach w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="6c927-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="6c927-165">Uzyskiwanie informacji o obciążenia aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6c927-165">Obtaining hello application load information</span></span>
<span data-ttu-id="6c927-166">Dla każdej aplikacji, który posiada zdefiniowane dla co najmniej jedną metrykę zdolność aplikacji można uzyskać hello informacji na temat hello obciążenia agregacji zgłoszone przez repliki z jego usług.</span><span class="sxs-lookup"><span data-stu-id="6c927-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="6c927-167">Środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6c927-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="6c927-168">C#</span><span class="sxs-lookup"><span data-stu-id="6c927-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="6c927-169">Witaj ApplicationLoad zapytanie zwraca hello podstawowe informacje o wydajności aplikacji, który został określony dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="6c927-170">Informacje te obejmują informacje o węzłach minimalna i maksymalna liczba węzłów hello i hello liczba, która obecnie zajmuje aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="6c927-171">Zawiera także informacje o każdym Metryka obciążenia aplikacji, w tym:</span><span class="sxs-lookup"><span data-stu-id="6c927-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="6c927-172">Nazwa metryki: Nazwa metryki hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="6c927-173">Reservationcapacity: Pojemności klastra w klastrze hello zarezerwowane dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="6c927-174">Obciążenia aplikacji: Całkowita liczba obciążenia replik podrzędnych tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="6c927-175">Pojemność aplikacji: Maksymalna dopuszczalna wartość obciążenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="6c927-176">Usuwanie aplikacji, zdolność</span><span class="sxs-lookup"><span data-stu-id="6c927-176">Removing Application Capacity</span></span>
<span data-ttu-id="6c927-177">Po ustawieniu parametrów aplikacji, zdolność powitania dla aplikacji, można je usunąć za pomocą poleceń cmdlet interfejsów API aplikacji aktualizacji lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c927-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="6c927-178">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6c927-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="6c927-179">To polecenie usuwa wszystkie parametry zarządzania wydajności aplikacji z wystąpienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="6c927-180">W tym MinimumNodes, wartość MaximumNodes i metryki aplikacji hello, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="6c927-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="6c927-181">Witaj hello polecenie powoduje natychmiastowe.</span><span class="sxs-lookup"><span data-stu-id="6c927-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="6c927-182">Po wykonaniu tego polecenia, hello Menedżera zasobów klastra używa hello domyślne zachowanie związanych z zarządzaniem aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="6c927-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="6c927-183">Parametry pojemność aplikacji można określić ponownie za pomocą `Update-ServiceFabricApplication` / `System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="6c927-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="6c927-184">Ograniczenia dotyczące wydajności aplikacji</span><span class="sxs-lookup"><span data-stu-id="6c927-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="6c927-185">Istnieje kilka ograniczeń w parametrach wydajność aplikacji, które muszą zostać zachowane.</span><span class="sxs-lookup"><span data-stu-id="6c927-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="6c927-186">Jeśli występują błędy sprawdzania poprawności żadne zmiany nie została wykonana.</span><span class="sxs-lookup"><span data-stu-id="6c927-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="6c927-187">Wszystkie parametry liczba całkowita musi być liczby nieujemnej.</span><span class="sxs-lookup"><span data-stu-id="6c927-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="6c927-188">Wartość MinimumNodes nigdy nie może być większa niż wartość MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="6c927-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="6c927-189">Jeśli zdefiniowano wydajności dla metryki obciążenia, są one musi wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6c927-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="6c927-190">Węzeł rezerwacji pojemność nie może być większa niż maksymalna pojemność węzła.</span><span class="sxs-lookup"><span data-stu-id="6c927-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="6c927-191">Nie można na przykład ograniczyć hello pojemność hello metryki "CPU" hello węzła tootwo jednostki i spróbuj tooreserve trzy jednostki w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="6c927-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="6c927-192">Jeśli określono wartość MaximumNodes, następnie produktu hello MaximumNodes i maksymalna pojemność węzła nie może być większa niż całkowita pojemność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="6c927-193">Na przykład załóżmy, że hello maksymalna pojemność węzła metryki obciążenia, ustawione tooeight "CPU".</span><span class="sxs-lookup"><span data-stu-id="6c927-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="6c927-194">Również Załóżmy, że ustawisz hello too10 maksymalna liczba węzłów.</span><span class="sxs-lookup"><span data-stu-id="6c927-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="6c927-195">W takim przypadku całkowita pojemność aplikacji musi być większa niż 80 dla ta metryka obciążenia.</span><span class="sxs-lookup"><span data-stu-id="6c927-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="6c927-196">ograniczenia dotyczące Hello są wymuszane, zarówno podczas tworzenia aplikacji i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="6c927-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="6c927-197">W jaki sposób toouse wydajności aplikacji</span><span class="sxs-lookup"><span data-stu-id="6c927-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="6c927-198">Nie próbuj grupy aplikacji hello toouse funkcji tooa aplikacji hello tooconstrain _określonych_ podzbioru węzłów.</span><span class="sxs-lookup"><span data-stu-id="6c927-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="6c927-199">Innymi słowy, można określić, że aplikacja hello działa na maksymalnie pięć węzłów, ale nie których określonych pięć węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="6c927-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="6c927-200">Ograniczający toospecific aplikacji węzłów można osiągnąć za pomocą ograniczenia umieszczania usług.</span><span class="sxs-lookup"><span data-stu-id="6c927-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="6c927-201">Nie próbuj tooensure pojemność aplikacji hello toouse czy dwie usługi z tej samej aplikacji są umieszczane na powitania hello samych węzłów.</span><span class="sxs-lookup"><span data-stu-id="6c927-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="6c927-202">Zamiast tego użyj [koligacji](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) lub [ograniczenia umieszczania](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="6c927-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c927-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c927-203">Next steps</span></span>
- <span data-ttu-id="6c927-204">Aby uzyskać więcej informacji na temat konfigurowania usługi [Dowiedz się więcej o konfigurowaniu usługi](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="6c927-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="6c927-205">toofind limit o jak hello Menedżera zasobów klastra zarządza i równoważy obciążenie klastra hello wyewidencjonować hello artykułu na [równoważenia obciążenia](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="6c927-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="6c927-206">Rozpocznij od początku hello i [uzyskać toohello wprowadzenie zasobu klastra sieci szkieletowej programu Service Manager](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6c927-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="6c927-207">Aby uzyskać więcej informacji na temat działania metryki ogólnie rzecz biorąc, przeczytaj na [metryki obciążenia sieci szkieletowej usług](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="6c927-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="6c927-208">Witaj Menedżera zasobów klastra ma wiele opcji opisujące hello klastra.</span><span class="sxs-lookup"><span data-stu-id="6c927-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="6c927-209">toofind się więcej na ich temat, zapoznaj się w tym artykule na [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="6c927-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
