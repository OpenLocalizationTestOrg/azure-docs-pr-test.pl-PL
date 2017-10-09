---
title: "aaaAzure programowe skalowania usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
description: "Skalowanie klastra usługi sieć szkieletowa usług Azure lub programistycznie, zgodnie z wyzwalaczy toocustom"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="21333-103">Programowo skalowanie klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="21333-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="21333-104">Podstawowe informacje na temat skalowania klastra sieci szkieletowej usług na platformie Azure opisano w dokumentacji na [skalowanie klastra](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="21333-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="21333-105">Tym artykule opisano sposób klastrów sieci szkieletowej usług są zbudowane na podstawie zestawy skalowania maszyny wirtualnej i mogą być skalowane ręcznie lub przy użyciu reguł automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="21333-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="21333-106">Ten dokument analizuje metod programistycznych koordynujący Azure operacji skalowania dla bardziej zaawansowanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="21333-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="21333-107">Przyczyny skalowanie programowe</span><span class="sxs-lookup"><span data-stu-id="21333-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="21333-108">W wielu scenariuszach skalowanie ręcznie lub za pomocą reguł automatycznego skalowania są dobrym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="21333-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="21333-109">W innych sytuacjach, mogą nie być hello mieści się po prawej.</span><span class="sxs-lookup"><span data-stu-id="21333-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="21333-110">Potencjalne wady toothese podejścia obejmują:</span><span class="sxs-lookup"><span data-stu-id="21333-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="21333-111">Ręcznie skalowanie wymaga toolog w i jawnie żądania operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="21333-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="21333-112">Operacje skalowania wymagane są często lub w czasie nieprzewidywalne, ta metoda nie może być dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="21333-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="21333-113">Usunięcie reguły automatycznego skalowania wystąpienia z zestawu skalowania maszyn wirtualnych, ich nie automatycznie usuwaj wiedzę na temat tego węzła z klastra usługi sieć szkieletowa hello skojarzone chyba, że typ węzła hello ma poziom trwałości Silver lub Gold.</span><span class="sxs-lookup"><span data-stu-id="21333-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="21333-114">Ponieważ reguły automatycznego skalowania działają na dużą skalę hello Ustaw poziom (a nie na powitania poziom usługi sieć szkieletowa), reguły automatycznego skalowania można usunąć węzłów sieci szkieletowej usług bez zamykania bezpiecznie zamknąć.</span><span class="sxs-lookup"><span data-stu-id="21333-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="21333-115">Usunięcie węzła niegrzeczny pozostawi "widma" stan węzła sieci szkieletowej usług po operacji w skali.</span><span class="sxs-lookup"><span data-stu-id="21333-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="21333-116">Potrzebny tooperiodically czyszczenie stanu usuniętym węźle w klastrze usługi sieć szkieletowa hello osoby (lub usługi).</span><span class="sxs-lookup"><span data-stu-id="21333-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="21333-117">Należy pamiętać, że typ węzła z poziomu trwałości Gold lub Silver automatycznie spowoduje oczyszczenie usunięte węzłów.</span><span class="sxs-lookup"><span data-stu-id="21333-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="21333-118">Mimo że istnieją [wiele metryk](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) obsługiwane przez reguły automatycznego skalowania, nadal jest ograniczony zestaw.</span><span class="sxs-lookup"><span data-stu-id="21333-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="21333-119">Jeśli scenariusz wymaga skalowanie oparte na niektóre metryki nieuwzględnionego w tym zestawie, następnie reguły automatycznego skalowania nie może być dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="21333-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="21333-120">W oparciu o te ograniczenia, warto zapoznać się z tooimplement bardziej dostosowanego automatycznego skalowania modeli.</span><span class="sxs-lookup"><span data-stu-id="21333-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="21333-121">Skalowanie interfejsów API</span><span class="sxs-lookup"><span data-stu-id="21333-121">Scaling APIs</span></span>
<span data-ttu-id="21333-122">Interfejsy API usługi Azure istnieje, co pozwala aplikacji tooprogrammatically współpracują z zestawy skalowania maszyn wirtualnych i klastrów sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="21333-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="21333-123">Jeśli istniejących opcji automatycznego skalowania nie działa dla danego scenariusza, te interfejsy API była możliwa tooimplement niestandardowej logiki skalowania.</span><span class="sxs-lookup"><span data-stu-id="21333-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="21333-124">Jednym z podejść tooimplementing to "głównej wytworzone" automatyczne skalowanie funkcji jest tooadd nowej usługi bezstanowej toohello sieci szkieletowej usług aplikacji toomanage operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="21333-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="21333-125">W ramach usługi hello `RunAsync` metody, zestawu wyzwalaczy można określić, czy skalowanie jest wymagana (w tym sprawdzanie parametry, takie jak maksymalna wielkość klastra i skalowanie cooldowns).</span><span class="sxs-lookup"><span data-stu-id="21333-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="21333-126">Hello API używany interakcji zestaw skali maszyny wirtualnej (zarówno toocheck hello bieżąca liczba wystąpień maszyn wirtualnych i toomodify go) jest hello [fluent biblioteki Azure zarządzania obliczeniowe](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="21333-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="21333-127">Biblioteka fluent obliczeń Hello zapewnia łatwy w użyciu interfejsu API do interakcji z zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="21333-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="21333-128">Użyj toointeract z klastra sieci szkieletowej usług hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="21333-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="21333-129">Oczywiście hello skalowanie kodu nie wymaga toorun jako usługa w toobe klastra hello skalowania.</span><span class="sxs-lookup"><span data-stu-id="21333-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="21333-130">Zarówno `IAzure` i `FabricClient` możesz połączyć tootheir skojarzonych zasobów Azure zdalnie, więc hello skalowania usługi można łatwo aplikacji konsoli lub uruchomiony za pośrednictwem aplikacji usługi Service Fabric poza hello usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="21333-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="21333-131">Zarządzanie poświadczeniami</span><span class="sxs-lookup"><span data-stu-id="21333-131">Credential management</span></span>
<span data-ttu-id="21333-132">Jednym z wyzwań zapisu, skalowanie toohandle usługi jest, że usługa hello musi być tooaccess stanie zasobów zestawu skali maszyny wirtualnej bez interakcyjnego logowania.</span><span class="sxs-lookup"><span data-stu-id="21333-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="21333-133">Uzyskiwanie dostępu do sieci szkieletowej usług hello klastra jest łatwe hello skalowania usługi modyfikuje własnej aplikacji usługi Service Fabric, ale tooaccess wymagane są poświadczenia hello zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="21333-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="21333-134">toolog w, można użyć [nazwy głównej usługi](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) utworzone za pomocą hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="21333-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="21333-135">Nazwy głównej usługi można tworzyć za pomocą hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="21333-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="21333-136">Zaloguj się za toohello wiersza polecenia platformy Azure (`az login`) jako użytkownik z skalowania maszyny wirtualnej toohello dostępu należy ustawić</span><span class="sxs-lookup"><span data-stu-id="21333-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="21333-137">Tworzenie nazwy głównej z hello usługi`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="21333-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="21333-138">Zanotuj identyfikator aplikacji hello (nazywanych "identyfikator klienta" w innym miejscu), nazwa, hasło i dzierżawy w celu późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="21333-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="21333-139">Należy również identyfikator subskrypcji można wyświetlić w programie`az account list`</span><span class="sxs-lookup"><span data-stu-id="21333-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="21333-140">Hello biblioteki fluent obliczeń zalogować się przy użyciu tych poświadczeń w następujący sposób (należy pamiętać, że fluent Azure typów podstawowych, takich jak `IAzure` w hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pakietu):</span><span class="sxs-lookup"><span data-stu-id="21333-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="21333-141">Po zalogowaniu, liczba wystąpień zestawu skali można tworzyć zapytania za pomocą `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="21333-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="21333-142">Skalowanie w poziomie</span><span class="sxs-lookup"><span data-stu-id="21333-142">Scaling out</span></span>
<span data-ttu-id="21333-143">Przy użyciu hello fluent SDK rozwiązań usługi obliczenia Azure, można dodać wystąpienia skalowania maszyny wirtualnej toohello ustawiony za pomocą kilku wywołania-</span><span class="sxs-lookup"><span data-stu-id="21333-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="21333-144">Alternatywnie rozmiaru zestawu skali maszyny wirtualnej, można też zarządzać za pomocą poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21333-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="21333-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)można pobrać obiektu zestawu skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="21333-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="21333-146">obecna pojemność Hello będą przechowywane w hello `.sku.capacity` właściwości.</span><span class="sxs-lookup"><span data-stu-id="21333-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="21333-147">Po zmiana hello pojemności toohello Żądana wartość, hello skalowania maszyny wirtualnej w usłudze Azure może zostać zaktualizowana przy użyciu hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) polecenia.</span><span class="sxs-lookup"><span data-stu-id="21333-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="21333-148">Podczas dodawania węzła ręcznie, dodając wystąpienia zestawu skalowania powinny być wszystkie to jest wymagana toostart obejmuje nowy węzeł sieci szkieletowej usług, ponieważ zestaw skalowania hello szablonu tooautomatically rozszerzenia Dołącz do nowego klastra usługi sieć szkieletowa toohello wystąpień.</span><span class="sxs-lookup"><span data-stu-id="21333-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="21333-149">Skalowanie w</span><span class="sxs-lookup"><span data-stu-id="21333-149">Scaling in</span></span>

<span data-ttu-id="21333-150">Skalowanie w jest podobne tooscaling wychodzących. zestaw skali Hello rzeczywiste maszyny wirtualnej, zmiany są praktycznie hello takie same.</span><span class="sxs-lookup"><span data-stu-id="21333-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="21333-151">Jednak jak został już wcześniej, usługa sieć szkieletowa tylko automatycznie oczyszcza usuniętych węzłów trwałości Gold lub Silver.</span><span class="sxs-lookup"><span data-stu-id="21333-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="21333-152">W hello trwałości brązowa skalowania w przypadku jest konieczne toointeract z hello sieci szkieletowej usług klastra tooshut dół toobe węzła hello usunięte, a następnie tooremove jego stanu.</span><span class="sxs-lookup"><span data-stu-id="21333-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="21333-153">Przygotowywanie węzła hello zamknięcia obejmuje znajdowanie toobe węzła hello usunięte (ostatnio dodane węzeł hello) i dezaktywowanie go.</span><span class="sxs-lookup"><span data-stu-id="21333-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="21333-154">Dla węzłów z systemem innym niż inicjatora nowszej węzły znajdują się na podstawie porównania ilości `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="21333-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="21333-155">Należy pamiętać, że *inicjatora* węzłów nie wydają się tooalways wykonaj Konwencji hello najpierw usunąć większa identyfikatorów wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="21333-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="21333-156">Po znalezieniu toobe węzła hello usunięte można dezaktywować i usunięty przy użyciu hello sam `FabricClient` wystąpienia i hello `IAzure` wystąpienie z wcześniej.</span><span class="sxs-lookup"><span data-stu-id="21333-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="21333-157">Jako ze skalowania poleceń cmdlet programu PowerShell modyfikowania skalowania maszyny wirtualnej zestawu pojemności można także tutaj Jeśli skryptów podejście jest bardziej pożądane.</span><span class="sxs-lookup"><span data-stu-id="21333-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="21333-158">Po usunięciu hello wystąpienie maszyny wirtualnej, można usunąć stan węzła sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="21333-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="21333-159">Wady</span><span class="sxs-lookup"><span data-stu-id="21333-159">Potential drawbacks</span></span>

<span data-ttu-id="21333-160">Jak pokazano w hello poprzedzających fragmentów kodu, tworzenie własnych skalowania usługi zapewnia najwyższy stopień kontroli i dostosowywalności za pośrednictwem aplikacji hello na skalowanie.</span><span class="sxs-lookup"><span data-stu-id="21333-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="21333-161">Może to być przydatne w scenariuszach wymagających precyzyjną kontrolę, kiedy i jak aplikacja skaluje przychodzący lub wychodzący. Jednak ten formant pochodzi z zależnościami złożoności kodu.</span><span class="sxs-lookup"><span data-stu-id="21333-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="21333-162">Przy użyciu tej metody oznacza, że konieczne tooown kod, który jest nieuproszczony skalowania.</span><span class="sxs-lookup"><span data-stu-id="21333-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="21333-163">Jak powinna wynosić skalowania usługi Service Fabric, zależy od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="21333-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="21333-164">W przypadku skalowania rzadko, hello możliwości tooadd lub usuń węzłami ręcznie jest prawdopodobnie wystarczający.</span><span class="sxs-lookup"><span data-stu-id="21333-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="21333-165">Dla bardziej złożonymi scenariuszami reguły automatycznego skalowania i zestawy SDK programowo udostępnianie tooscale możliwości hello oferują zaawansowanych rozwiązań alternatywnych.</span><span class="sxs-lookup"><span data-stu-id="21333-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21333-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="21333-166">Next steps</span></span>

<span data-ttu-id="21333-167">rozpoczęto wdrażanie własną logikę automatyczne skalowanie tooget zapoznania się z hello następujące pojęcia i przydatne interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="21333-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="21333-168">Skalowanie ręcznie lub przy użyciu reguł automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="21333-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="21333-169">[Fluent biblioteki zarządzania platformy Azure dla platformy .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (przydatne w przypadku interakcji z podstawowej zestawy skalowania maszyny wirtualnej w klastrze usługi sieć szkieletowa)</span><span class="sxs-lookup"><span data-stu-id="21333-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="21333-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (przydatne w przypadku interakcji z klastra sieci szkieletowej usług i jego węzły)</span><span class="sxs-lookup"><span data-stu-id="21333-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
