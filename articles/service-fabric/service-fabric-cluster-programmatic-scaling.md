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
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Programowo skalowanie klastra sieci szkieletowej usług 

Podstawowe informacje na temat skalowania klastra sieci szkieletowej usług na platformie Azure opisano w dokumentacji na [skalowanie klastra](./service-fabric-cluster-scale-up-down.md). Tym artykule opisano sposób klastrów sieci szkieletowej usług są zbudowane na podstawie zestawy skalowania maszyny wirtualnej i mogą być skalowane ręcznie lub przy użyciu reguł automatycznego skalowania. Ten dokument analizuje metod programistycznych koordynujący Azure operacji skalowania dla bardziej zaawansowanych scenariuszy. 

## <a name="reasons-for-programmatic-scaling"></a>Przyczyny skalowanie programowe
W wielu scenariuszach skalowanie ręcznie lub za pomocą reguł automatycznego skalowania są dobrym rozwiązania. W innych sytuacjach, mogą nie być hello mieści się po prawej. Potencjalne wady toothese podejścia obejmują:

- Ręcznie skalowanie wymaga toolog w i jawnie żądania operacji skalowania. Operacje skalowania wymagane są często lub w czasie nieprzewidywalne, ta metoda nie może być dobrym rozwiązaniem.
- Usunięcie reguły automatycznego skalowania wystąpienia z zestawu skalowania maszyn wirtualnych, ich nie automatycznie usuwaj wiedzę na temat tego węzła z klastra usługi sieć szkieletowa hello skojarzone chyba, że typ węzła hello ma poziom trwałości Silver lub Gold. Ponieważ reguły automatycznego skalowania działają na dużą skalę hello Ustaw poziom (a nie na powitania poziom usługi sieć szkieletowa), reguły automatycznego skalowania można usunąć węzłów sieci szkieletowej usług bez zamykania bezpiecznie zamknąć. Usunięcie węzła niegrzeczny pozostawi "widma" stan węzła sieci szkieletowej usług po operacji w skali. Potrzebny tooperiodically czyszczenie stanu usuniętym węźle w klastrze usługi sieć szkieletowa hello osoby (lub usługi).
  - Należy pamiętać, że typ węzła z poziomu trwałości Gold lub Silver automatycznie spowoduje oczyszczenie usunięte węzłów.  
- Mimo że istnieją [wiele metryk](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) obsługiwane przez reguły automatycznego skalowania, nadal jest ograniczony zestaw. Jeśli scenariusz wymaga skalowanie oparte na niektóre metryki nieuwzględnionego w tym zestawie, następnie reguły automatycznego skalowania nie może być dobrym rozwiązaniem.

W oparciu o te ograniczenia, warto zapoznać się z tooimplement bardziej dostosowanego automatycznego skalowania modeli. 

## <a name="scaling-apis"></a>Skalowanie interfejsów API
Interfejsy API usługi Azure istnieje, co pozwala aplikacji tooprogrammatically współpracują z zestawy skalowania maszyn wirtualnych i klastrów sieci szkieletowej usług. Jeśli istniejących opcji automatycznego skalowania nie działa dla danego scenariusza, te interfejsy API była możliwa tooimplement niestandardowej logiki skalowania. 

Jednym z podejść tooimplementing to "głównej wytworzone" automatyczne skalowanie funkcji jest tooadd nowej usługi bezstanowej toohello sieci szkieletowej usług aplikacji toomanage operacji skalowania. W ramach usługi hello `RunAsync` metody, zestawu wyzwalaczy można określić, czy skalowanie jest wymagana (w tym sprawdzanie parametry, takie jak maksymalna wielkość klastra i skalowanie cooldowns).   

Hello API używany interakcji zestaw skali maszyny wirtualnej (zarówno toocheck hello bieżąca liczba wystąpień maszyn wirtualnych i toomodify go) jest hello [fluent biblioteki Azure zarządzania obliczeniowe](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). Biblioteka fluent obliczeń Hello zapewnia łatwy w użyciu interfejsu API do interakcji z zestawy skalowania maszyny wirtualnej.

Użyj toointeract z klastra sieci szkieletowej usług hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Oczywiście hello skalowanie kodu nie wymaga toorun jako usługa w toobe klastra hello skalowania. Zarówno `IAzure` i `FabricClient` możesz połączyć tootheir skojarzonych zasobów Azure zdalnie, więc hello skalowania usługi można łatwo aplikacji konsoli lub uruchomiony za pośrednictwem aplikacji usługi Service Fabric poza hello usługi systemu Windows. 

## <a name="credential-management"></a>Zarządzanie poświadczeniami
Jednym z wyzwań zapisu, skalowanie toohandle usługi jest, że usługa hello musi być tooaccess stanie zasobów zestawu skali maszyny wirtualnej bez interakcyjnego logowania. Uzyskiwanie dostępu do sieci szkieletowej usług hello klastra jest łatwe hello skalowania usługi modyfikuje własnej aplikacji usługi Service Fabric, ale tooaccess wymagane są poświadczenia hello zestaw skali. toolog w, można użyć [nazwy głównej usługi](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) utworzone za pomocą hello [Azure CLI 2.0](https://github.com/azure/azure-cli).

Nazwy głównej usługi można tworzyć za pomocą hello następujące kroki:

1. Zaloguj się za toohello wiersza polecenia platformy Azure (`az login`) jako użytkownik z skalowania maszyny wirtualnej toohello dostępu należy ustawić
2. Tworzenie nazwy głównej z hello usługi`az ad sp create-for-rbac`
    1. Zanotuj identyfikator aplikacji hello (nazywanych "identyfikator klienta" w innym miejscu), nazwa, hasło i dzierżawy w celu późniejszego użycia.
    2. Należy również identyfikator subskrypcji można wyświetlić w programie`az account list`

Hello biblioteki fluent obliczeń zalogować się przy użyciu tych poświadczeń w następujący sposób (należy pamiętać, że fluent Azure typów podstawowych, takich jak `IAzure` w hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pakietu):

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

Po zalogowaniu, liczba wystąpień zestawu skali można tworzyć zapytania za pomocą `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Skalowanie w poziomie
Przy użyciu hello fluent SDK rozwiązań usługi obliczenia Azure, można dodać wystąpienia skalowania maszyny wirtualnej toohello ustawiony za pomocą kilku wywołania-

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

Alternatywnie rozmiaru zestawu skali maszyny wirtualnej, można też zarządzać za pomocą poleceń cmdlet programu PowerShell. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)można pobrać obiektu zestawu skali maszyny wirtualnej hello. obecna pojemność Hello będą przechowywane w hello `.sku.capacity` właściwości. Po zmiana hello pojemności toohello Żądana wartość, hello skalowania maszyny wirtualnej w usłudze Azure może zostać zaktualizowana przy użyciu hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) polecenia.

Podczas dodawania węzła ręcznie, dodając wystąpienia zestawu skalowania powinny być wszystkie to jest wymagana toostart obejmuje nowy węzeł sieci szkieletowej usług, ponieważ zestaw skalowania hello szablonu tooautomatically rozszerzenia Dołącz do nowego klastra usługi sieć szkieletowa toohello wystąpień. 

## <a name="scaling-in"></a>Skalowanie w

Skalowanie w jest podobne tooscaling wychodzących. zestaw skali Hello rzeczywiste maszyny wirtualnej, zmiany są praktycznie hello takie same. Jednak jak został już wcześniej, usługa sieć szkieletowa tylko automatycznie oczyszcza usuniętych węzłów trwałości Gold lub Silver. W hello trwałości brązowa skalowania w przypadku jest konieczne toointeract z hello sieci szkieletowej usług klastra tooshut dół toobe węzła hello usunięte, a następnie tooremove jego stanu.

Przygotowywanie węzła hello zamknięcia obejmuje znajdowanie toobe węzła hello usunięte (ostatnio dodane węzeł hello) i dezaktywowanie go. Dla węzłów z systemem innym niż inicjatora nowszej węzły znajdują się na podstawie porównania ilości `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

Należy pamiętać, że *inicjatora* węzłów nie wydają się tooalways wykonaj Konwencji hello najpierw usunąć większa identyfikatorów wystąpienia.

Po znalezieniu toobe węzła hello usunięte można dezaktywować i usunięty przy użyciu hello sam `FabricClient` wystąpienia i hello `IAzure` wystąpienie z wcześniej.

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

Jako ze skalowania poleceń cmdlet programu PowerShell modyfikowania skalowania maszyny wirtualnej zestawu pojemności można także tutaj Jeśli skryptów podejście jest bardziej pożądane. Po usunięciu hello wystąpienie maszyny wirtualnej, można usunąć stan węzła sieci szkieletowej usług.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Wady

Jak pokazano w hello poprzedzających fragmentów kodu, tworzenie własnych skalowania usługi zapewnia najwyższy stopień kontroli i dostosowywalności za pośrednictwem aplikacji hello na skalowanie. Może to być przydatne w scenariuszach wymagających precyzyjną kontrolę, kiedy i jak aplikacja skaluje przychodzący lub wychodzący. Jednak ten formant pochodzi z zależnościami złożoności kodu. Przy użyciu tej metody oznacza, że konieczne tooown kod, który jest nieuproszczony skalowania.

Jak powinna wynosić skalowania usługi Service Fabric, zależy od danego scenariusza. W przypadku skalowania rzadko, hello możliwości tooadd lub usuń węzłami ręcznie jest prawdopodobnie wystarczający. Dla bardziej złożonymi scenariuszami reguły automatycznego skalowania i zestawy SDK programowo udostępnianie tooscale możliwości hello oferują zaawansowanych rozwiązań alternatywnych.

## <a name="next-steps"></a>Następne kroki

rozpoczęto wdrażanie własną logikę automatyczne skalowanie tooget zapoznania się z hello następujące pojęcia i przydatne interfejsów API:

- [Skalowanie ręcznie lub przy użyciu reguł automatycznego skalowania](./service-fabric-cluster-scale-up-down.md)
- [Fluent biblioteki zarządzania platformy Azure dla platformy .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (przydatne w przypadku interakcji z podstawowej zestawy skalowania maszyny wirtualnej w klastrze usługi sieć szkieletowa)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (przydatne w przypadku interakcji z klastra sieci szkieletowej usług i jego węzły)
