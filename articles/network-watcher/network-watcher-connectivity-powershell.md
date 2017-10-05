---
title: "Sprawdź łączność z obserwatora sieciowego Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak przetestowanie łączności z obserwatora sieciowego przy użyciu programu PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: a8f936cd23838759dc30b04688d3c6544e4895cc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="5776c-103">Sprawdź łączność z obserwatora sieciowego Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5776c-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5776c-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5776c-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="5776c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5776c-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="5776c-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="5776c-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="5776c-107">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="5776c-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="5776c-108">Dowiedz się, jak używać łączności, aby sprawdzić, czy można nawiązać bezpośrednie połączenie TCP z maszyny wirtualnej do danego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5776c-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5776c-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="5776c-109">Before you begin</span></span>

<span data-ttu-id="5776c-110">W tym artykule przyjęto założenie, że masz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="5776c-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="5776c-111">Wystąpienie obserwatora sieciowego w regionie, aby sprawdzić łączność.</span><span class="sxs-lookup"><span data-stu-id="5776c-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="5776c-112">Sprawdź łączność z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5776c-112">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="5776c-113">Sprawdź łączność wymaga rozszerzenia maszyny wirtualnej `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="5776c-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="5776c-114">Instalowanie rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="5776c-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="5776c-115">Zarejestruj możliwości wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="5776c-115">Register the preview capability</span></span>

<span data-ttu-id="5776c-116">Połączenie jest aktualnie w publicznej wersji zapoznawczej, aby użyć tej funkcji, który musi być zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="5776c-116">Connectivity is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="5776c-117">Aby to zrobić, uruchom w poniższym przykładzie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5776c-117">To do this, run the following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="5776c-118">Aby sprawdzić, czy rejestracja zakończyła się pomyślnie, należy uruchomić w poniższym przykładzie programu Powershell:</span><span class="sxs-lookup"><span data-stu-id="5776c-118">To verify the registration was successful, run the following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="5776c-119">Jeśli funkcja został prawidłowo zarejestrowany, dane wyjściowe powinny odpowiadać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5776c-119">If the feature was properly registered, the output should match the following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="5776c-120">Sprawdź połączenie z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="5776c-120">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="5776c-121">W tym przykładzie służy do sprawdzania łączności do docelowej maszyny wirtualnej za pośrednictwem portu 80.</span><span class="sxs-lookup"><span data-stu-id="5776c-121">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="5776c-122">Przykład</span><span class="sxs-lookup"><span data-stu-id="5776c-122">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="5776c-123">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="5776c-123">Response</span></span>

<span data-ttu-id="5776c-124">Następujące odpowiedzi jest z poprzedniego przykładu.</span><span class="sxs-lookup"><span data-stu-id="5776c-124">The following response is from the previous example.</span></span>  <span data-ttu-id="5776c-125">W tej odpowiedzi `ConnectionStatus` jest **informujący**.</span><span class="sxs-lookup"><span data-stu-id="5776c-125">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="5776c-126">Widać, że wszystkie sond wysyłane nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="5776c-126">You can see that all the probes sent failed.</span></span> <span data-ttu-id="5776c-127">Połączenie nie powiodło się na urządzenie wirtualne z powodu użytkownik skonfigurował `NetworkSecurityRule` o nazwie **UserRule_Port80**, jest skonfigurowany do blokowania ruchu przychodzącego na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="5776c-127">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="5776c-128">Te informacje mogą służyć do badania problemów z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="5776c-128">This information can be used to research connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="5776c-129">Sprawdź poprawność routingu problemów</span><span class="sxs-lookup"><span data-stu-id="5776c-129">Validate routing issues</span></span>

<span data-ttu-id="5776c-130">Przykład służy do sprawdzania łączności między maszyną wirtualną i zdalny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="5776c-130">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="5776c-131">Przykład</span><span class="sxs-lookup"><span data-stu-id="5776c-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="5776c-132">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="5776c-132">Response</span></span>

<span data-ttu-id="5776c-133">W poniższym przykładzie `ConnectionStatus` jest wyświetlany jako **informujący**.</span><span class="sxs-lookup"><span data-stu-id="5776c-133">In the following example, the `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="5776c-134">W `Hops` uzyskać szczegółowe informacje, widoczny w obszarze `Issues` ruch został zablokowany ze względu na `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="5776c-134">In the `Hops` details, you can see under `Issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="5776c-135">Sprawdź czas oczekiwania witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="5776c-135">Check website latency</span></span>

<span data-ttu-id="5776c-136">Poniższy przykład służy do sprawdzania łączności z witryną sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5776c-136">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="5776c-137">Przykład</span><span class="sxs-lookup"><span data-stu-id="5776c-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="5776c-138">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="5776c-138">Response</span></span>

<span data-ttu-id="5776c-139">W poniższych odpowiedzi, zobacz `ConnectionStatus` jest pokazywana jako **osiągalne**.</span><span class="sxs-lookup"><span data-stu-id="5776c-139">In the following response, you can see the `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="5776c-140">Gdy połączenie zostanie nawiązane, znajdują się wartości opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="5776c-140">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="5776c-141">Sprawdź łączność z punktu końcowego magazynu</span><span class="sxs-lookup"><span data-stu-id="5776c-141">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="5776c-142">Poniższy przykład sprawdza łączność z maszyny wirtualnej na blogu konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="5776c-142">The following example tests the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="5776c-143">Przykład</span><span class="sxs-lookup"><span data-stu-id="5776c-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="5776c-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="5776c-144">Response</span></span>

<span data-ttu-id="5776c-145">Następujący kod json jest przykład odpowiedzi z uruchomienie poprzedniego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5776c-145">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="5776c-146">Jako miejsce docelowe jest osiągalny, `ConnectionStatus` właściwość pokazuje, jak **osiągalne**.</span><span class="sxs-lookup"><span data-stu-id="5776c-146">As the destination is reachable, the `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="5776c-147">Podano szczegółowe informacje dotyczące liczby przeskoków niezbędnych do magazynu obiektów blob i opóźnień.</span><span class="sxs-lookup"><span data-stu-id="5776c-147">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="5776c-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5776c-148">Next steps</span></span>

<span data-ttu-id="5776c-149">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5776c-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="5776c-150">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) śledzić reguły zabezpieczeń sieciowych grupy i zabezpieczeń zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="5776c-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<!-- Image references -->














