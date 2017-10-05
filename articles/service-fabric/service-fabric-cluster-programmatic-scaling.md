---
title: "Azure Usługa sieci szkieletowej programowe skalowanie | Dokumentacja firmy Microsoft"
description: "Skalowanie klastra usługi sieć szkieletowa usług Azure lub programistycznie, zgodnie z wyzwalaczy niestandardowych"
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
ms.openlocfilehash: 46b0b62f92abbac57bc27bbcdd5821eafedf5519
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="7ce4b-103">Programowo skalowanie klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="7ce4b-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="7ce4b-104">Podstawowe informacje na temat skalowania klastra sieci szkieletowej usług na platformie Azure opisano w dokumentacji na [skalowanie klastra](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="7ce4b-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="7ce4b-105">Tym artykule opisano sposób klastrów sieci szkieletowej usług są zbudowane na podstawie zestawy skalowania maszyny wirtualnej i mogą być skalowane ręcznie lub przy użyciu reguł automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="7ce4b-106">Ten dokument analizuje metod programistycznych koordynujący Azure operacji skalowania dla bardziej zaawansowanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="7ce4b-107">Przyczyny skalowanie programowe</span><span class="sxs-lookup"><span data-stu-id="7ce4b-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="7ce4b-108">W wielu scenariuszach skalowanie ręcznie lub za pomocą reguł automatycznego skalowania są dobrym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="7ce4b-109">W innych sytuacjach jednak mogą nie być rozwiązanie właściwe.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="7ce4b-110">Wady do tych metod uwzględnić:</span><span class="sxs-lookup"><span data-stu-id="7ce4b-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="7ce4b-111">Ręcznie skalowanie należy zalogować się i jawne żądanie operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="7ce4b-112">Operacje skalowania wymagane są często lub w czasie nieprzewidywalne, ta metoda nie może być dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="7ce4b-113">Usunięcie reguły automatycznego skalowania wystąpienia z zestawu skalowania maszyn wirtualnych, ich nie automatycznie usuwaj wiedzę na temat tego węzła z klastra usługi sieć szkieletowa skojarzone chyba, że typ węzła ma poziom trwałości Silver lub Gold.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="7ce4b-114">Ponieważ reguły automatycznego skalowania działają na dużą skalę, Ustaw poziom (a nie na poziomie sieci szkieletowej usług), reguły automatycznego skalowania można usunąć węzłów sieci szkieletowej usług bez zamykania bezpiecznie zamknąć.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="7ce4b-115">Usunięcie węzła niegrzeczny pozostawi "widma" stan węzła sieci szkieletowej usług po operacji w skali.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="7ce4b-116">Osoby (lub usługą) należy okresowo Wyczyść stan usuniętym węźle w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="7ce4b-117">Należy pamiętać, że typ węzła z poziomu trwałości Gold lub Silver automatycznie spowoduje oczyszczenie usunięte węzłów.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="7ce4b-118">Mimo że istnieją [wiele metryk](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) obsługiwane przez reguły automatycznego skalowania, nadal jest ograniczony zestaw.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="7ce4b-119">Jeśli scenariusz wymaga skalowanie oparte na niektóre metryki nieuwzględnionego w tym zestawie, następnie reguły automatycznego skalowania nie może być dobrym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="7ce4b-120">W oparciu o te ograniczenia, można zaimplementować więcej dostosowane automatycznego skalowania modeli.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="7ce4b-121">Skalowanie interfejsów API</span><span class="sxs-lookup"><span data-stu-id="7ce4b-121">Scaling APIs</span></span>
<span data-ttu-id="7ce4b-122">Interfejsy API Azure istnieje, co umożliwia aplikacjom programowo pracować z maszyną wirtualną skalowanie zestawów i klastrów sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="7ce4b-123">Jeśli istniejących opcji automatycznego skalowania nie działa dla danego scenariusza, te interfejsy API umożliwiają wdrożenie niestandardowej logiki skalowania.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="7ce4b-124">Jednym z podejść do wykonania tej "wprowadzone głównej" funkcji skalowania automatycznego jest dodania nowej usługi bezstanowej do aplikacji sieci szkieletowej usług do zarządzania operacjami skalowania.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="7ce4b-125">W ramach usługi `RunAsync` metody, zestawu wyzwalaczy można określić, czy skalowanie jest wymagana (w tym sprawdzanie parametry, takie jak maksymalna wielkość klastra i skalowanie cooldowns).</span><span class="sxs-lookup"><span data-stu-id="7ce4b-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="7ce4b-126">Interfejs API, używany do interakcji zestaw skali maszyny wirtualnej, (zarówno do sprawdzenia bieżąca liczba wystąpień maszyn wirtualnych, a następnie zmodyfikować go) jest [fluent biblioteki Azure zarządzania obliczeniowe](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="7ce4b-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="7ce4b-127">Biblioteka fluent obliczeń zapewnia łatwy w użyciu interfejsu API do interakcji z zestawy skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="7ce4b-128">Aby pracować interaktywnie z klastra usługi sieć szkieletowa, użyj [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="7ce4b-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="7ce4b-129">Oczywiście skalowania kodu nie trzeba uruchamiać jako usługi w klastrze, który ma być skalowana w.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="7ce4b-130">Zarówno `IAzure` i `FabricClient` mogą łączyć się z zasobami platformy Azure skojarzone zdalnie, więc skalowania usługi można łatwo aplikacji konsoli lub usługa systemu Windows uruchomiony za pośrednictwem poza aplikacją sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="7ce4b-131">Zarządzanie poświadczeniami</span><span class="sxs-lookup"><span data-stu-id="7ce4b-131">Credential management</span></span>
<span data-ttu-id="7ce4b-132">Jednym z wyzwań zapisywania usługi do obsługi skalowania jest, że usługi musi być możliwy dostęp do zasobów zestawu skali maszyny wirtualnej bez logowania interakcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="7ce4b-133">Uzyskiwanie dostępu do klastra usługi sieć szkieletowa jest proste, jeśli skalowania usługi modyfikuje własnej aplikacji usługi Service Fabric, ale poświadczenia są wymagane do zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="7ce4b-134">Aby zalogować się, można użyć [nazwy głównej usługi](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) utworzone za pomocą [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7ce4b-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="7ce4b-135">Nazwy głównej usługi mogą być tworzone z następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="7ce4b-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="7ce4b-136">Zaloguj się do wiersza polecenia platformy Azure (`az login`) jako użytkownik z dostępem do skalowania maszyny wirtualnej ustawić</span><span class="sxs-lookup"><span data-stu-id="7ce4b-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="7ce4b-137">Tworzenie nazwy głównej z usługi`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="7ce4b-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="7ce4b-138">Zanotuj identyfikator aplikacji (nazywane "identyfikator klienta" w innym miejscu), nazwa, hasło i dzierżawy w celu późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="7ce4b-139">Należy również identyfikator subskrypcji można wyświetlić w programie`az account list`</span><span class="sxs-lookup"><span data-stu-id="7ce4b-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="7ce4b-140">Biblioteka fluent obliczeń zalogować się przy użyciu tych poświadczeń w następujący sposób (należy pamiętać, że fluent Azure typów podstawowych, takich jak `IAzure` w [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pakietu):</span><span class="sxs-lookup"><span data-stu-id="7ce4b-140">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="7ce4b-141">Po zalogowaniu, liczba wystąpień zestawu skali można tworzyć zapytania za pomocą `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="7ce4b-142">Skalowanie w poziomie</span><span class="sxs-lookup"><span data-stu-id="7ce4b-142">Scaling out</span></span>
<span data-ttu-id="7ce4b-143">Przy użyciu fluent Azure obliczeniowe zestawu SDK, wystąpień, mogą być dodawane do zestaw z kilku wywołania - skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7ce4b-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="7ce4b-144">Alternatywnie rozmiaru zestawu skali maszyny wirtualnej, można też zarządzać za pomocą poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="7ce4b-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)można pobrać obiektu zestawu skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="7ce4b-146">Obecna pojemność będzie przechowywany w `.sku.capacity` właściwości.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-146">The current capacity will be stored in the `.sku.capacity` property.</span></span> <span data-ttu-id="7ce4b-147">Po zmianie pojemność na żądaną wartość, skalowania maszyny wirtualnej w usłudze Azure można zaktualizować za pomocą [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-147">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="7ce4b-148">Podczas dodawania węzła ręcznie, dodając wystąpienia zestawu skalowania powinny być wszystkie punkty, które ma potrzebne do uruchomienia nowego węzła sieci szkieletowej usług, ponieważ szablon zestawu skalowania obejmują rozszerzenia automatycznie dołączy do klastra usługi sieć szkieletowa nowych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="7ce4b-149">Skalowanie w</span><span class="sxs-lookup"><span data-stu-id="7ce4b-149">Scaling in</span></span>

<span data-ttu-id="7ce4b-150">Skalowanie w jest podobny do skalowania.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-150">Scaling in is similar to scaling out.</span></span> <span data-ttu-id="7ce4b-151">Rzeczywiste zestawu skalowania maszyn wirtualnych zmiany praktycznie są takie same.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-151">The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="7ce4b-152">Jednak jak został już wcześniej, usługa sieć szkieletowa tylko automatycznie oczyszcza usuniętych węzłów trwałości Gold lub Silver.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-152">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="7ce4b-153">Tak, w tym trwałości brązowa skalowania w przypadku należy interakcje z klastrem usługi sieć szkieletowa można zamknąć węzeł ma zostać usunięty, a następnie usunąć jego stanu.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-153">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="7ce4b-154">Przygotowanie węzła dla zamknięcia polega na znajdowaniu się, że węzeł, który ma być usunięty (węzeł ostatnio dodane) i dezaktywowanie go.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-154">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="7ce4b-155">Dla węzłów z systemem innym niż inicjatora nowszej węzły znajdują się na podstawie porównania ilości `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-155">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="7ce4b-156">Należy pamiętać, że *inicjatora* węzłów nie wydają się zawsze wykonać Konwencji najpierw usunąć większa identyfikatorów wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-156">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="7ce4b-157">Po znalezieniu węzeł ma zostać usunięty, można dezaktywować i usunąć korzystającej z tego samego `FabricClient` wystąpienia i `IAzure` wystąpienie z wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-157">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
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

<span data-ttu-id="7ce4b-158">Jako ze skalowania poleceń cmdlet programu PowerShell modyfikowania skalowania maszyny wirtualnej zestawu pojemności można także tutaj Jeśli skryptów podejście jest bardziej pożądane.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-158">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="7ce4b-159">Po usunięciu wystąpienie maszyny wirtualnej, można usunąć stan węzła sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-159">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="7ce4b-160">Wady</span><span class="sxs-lookup"><span data-stu-id="7ce4b-160">Potential drawbacks</span></span>

<span data-ttu-id="7ce4b-161">Jak pokazano w poprzedzających fragmentów kodu, tworzenia własnego skalowania usługi zapewnia najwyższy stopień kontroli i dostosowywalności za pośrednictwem aplikacji na skalowanie.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-161">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="7ce4b-162">Może to być przydatne w scenariuszach wymagających precyzyjną kontrolę, kiedy i jak aplikacja skaluje przychodzący lub wychodzący.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-162">This can be useful for scenarios requiring precise control over when or how an application scales in or out.</span></span> <span data-ttu-id="7ce4b-163">Jednak ten formant pochodzi z zależnościami złożoności kodu.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-163">However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="7ce4b-164">Przy użyciu tej metody oznacza, że konieczne do własnych skalowania kod, który jest nieuproszczony.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-164">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="7ce4b-165">Jak powinna wynosić skalowania usługi Service Fabric, zależy od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-165">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="7ce4b-166">W przypadku skalowania rzadko, możliwość dodawania lub usuwania węzłów ręcznie jest prawdopodobnie wystarczający.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-166">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="7ce4b-167">Dla bardziej złożonymi scenariuszami reguły automatyczne skalowanie i zestawy SDK udostępnia możliwość skalowania programowo oferują zaawansowane alternatyw.</span><span class="sxs-lookup"><span data-stu-id="7ce4b-167">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ce4b-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ce4b-168">Next steps</span></span>

<span data-ttu-id="7ce4b-169">Aby rozpocząć wdrażanie własną logikę automatyczne skalowanie, należy zapoznać się z przydatne interfejsów API i następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="7ce4b-169">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="7ce4b-170">Skalowanie ręcznie lub przy użyciu reguł automatycznego skalowania</span><span class="sxs-lookup"><span data-stu-id="7ce4b-170">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="7ce4b-171">[Fluent biblioteki zarządzania platformy Azure dla platformy .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (przydatne w przypadku interakcji z podstawowej zestawy skalowania maszyny wirtualnej w klastrze usługi sieć szkieletowa)</span><span class="sxs-lookup"><span data-stu-id="7ce4b-171">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="7ce4b-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (przydatne w przypadku interakcji z klastra sieci szkieletowej usług i jego węzły)</span><span class="sxs-lookup"><span data-stu-id="7ce4b-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
