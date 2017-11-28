---
title: "aaaCheck łączność z obserwatora sieciowego Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono sposób tootest łączność z obserwatora sieciowego przy użyciu programu PowerShell"
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
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="140eb-103">Sprawdź łączność z obserwatora sieciowego Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="140eb-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="140eb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="140eb-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="140eb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="140eb-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="140eb-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="140eb-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="140eb-107">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="140eb-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="140eb-108">Dowiedz się, jak można ustalić toouse łączności tooverify Jeśli bezpośrednie połączenie TCP z tooa maszyny wirtualnej, danego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="140eb-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="140eb-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="140eb-109">Before you begin</span></span>

<span data-ttu-id="140eb-110">W tym artykule przyjęto założenie, że masz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="140eb-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="140eb-111">Wystąpienia obserwatora sieciowego w regionie hello ma toocheck łączności.</span><span class="sxs-lookup"><span data-stu-id="140eb-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="140eb-112">Maszyny wirtualne toocheck łączność z.</span><span class="sxs-lookup"><span data-stu-id="140eb-112">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="140eb-113">Sprawdź łączność wymaga rozszerzenia maszyny wirtualnej `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="140eb-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="140eb-114">Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="140eb-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="140eb-115">Zarejestruj hello możliwości wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="140eb-115">Register hello preview capability</span></span>

<span data-ttu-id="140eb-116">Połączenie jest obecnie w publicznej wersji zapoznawczej, toouse ta funkcja wymaga toobe zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="140eb-116">Connectivity is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="140eb-117">toodo tego, hello uruchomienia następującego programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="140eb-117">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="140eb-118">Rejestracja hello tooverify zakończyło się powodzeniem, uruchom następujące przykładowe Powershell hello:</span><span class="sxs-lookup"><span data-stu-id="140eb-118">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="140eb-119">Jeśli funkcja hello zostało prawidłowo zarejestrowane hello dane wyjściowe powinny odpowiadać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="140eb-119">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="140eb-120">Sprawdź maszyny wirtualnej tooa łączności</span><span class="sxs-lookup"><span data-stu-id="140eb-120">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="140eb-121">W tym przykładzie sprawdza łączność tooa docelowej maszyny wirtualnej za pośrednictwem portu 80.</span><span class="sxs-lookup"><span data-stu-id="140eb-121">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="140eb-122">Przykład</span><span class="sxs-lookup"><span data-stu-id="140eb-122">Example</span></span>

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

### <a name="response"></a><span data-ttu-id="140eb-123">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="140eb-123">Response</span></span>

<span data-ttu-id="140eb-124">powitania po odpowiedzi pochodzi z poprzedniego przykładu hello.</span><span class="sxs-lookup"><span data-stu-id="140eb-124">hello following response is from hello previous example.</span></span>  <span data-ttu-id="140eb-125">W tej odpowiedzi hello `ConnectionStatus` jest **informujący**.</span><span class="sxs-lookup"><span data-stu-id="140eb-125">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="140eb-126">Widać, że wszystkie hello sond wysyłane nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="140eb-126">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="140eb-127">łączność Hello na urządzenie wirtualne hello nie powiodła się z powodu tooa konfigurowane przez użytkownika `NetworkSecurityRule` o nazwie **UserRule_Port80**, skonfigurowany tooblock ruch przychodzący na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="140eb-127">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="140eb-128">Te informacje mogą być używane tooresearch problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="140eb-128">This information can be used tooresearch connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="140eb-129">Sprawdź poprawność routingu problemów</span><span class="sxs-lookup"><span data-stu-id="140eb-129">Validate routing issues</span></span>

<span data-ttu-id="140eb-130">przykład Witaj służy do sprawdzania łączności między maszyną wirtualną i zdalny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="140eb-130">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="140eb-131">Przykład</span><span class="sxs-lookup"><span data-stu-id="140eb-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="140eb-132">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="140eb-132">Response</span></span>

<span data-ttu-id="140eb-133">W hello poniższy przykład, hello `ConnectionStatus` jest wyświetlany jako **informujący**.</span><span class="sxs-lookup"><span data-stu-id="140eb-133">In hello following example, hello `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="140eb-134">W hello `Hops` uzyskać szczegółowe informacje, widoczny w obszarze `Issues` czy ruch hello zostało zablokowane z powodu tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="140eb-134">In hello `Hops` details, you can see under `Issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span> 

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

## <a name="check-website-latency"></a><span data-ttu-id="140eb-135">Sprawdź czas oczekiwania witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="140eb-135">Check website latency</span></span>

<span data-ttu-id="140eb-136">Witaj poniższy przykład sprawdza hello łączności tooa witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="140eb-136">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="140eb-137">Przykład</span><span class="sxs-lookup"><span data-stu-id="140eb-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="140eb-138">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="140eb-138">Response</span></span>

<span data-ttu-id="140eb-139">Hello po odpowiedzi, zawiera hello `ConnectionStatus` jest pokazywana jako **osiągalne**.</span><span class="sxs-lookup"><span data-stu-id="140eb-139">In hello following response, you can see hello `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="140eb-140">Gdy połączenie zostanie nawiązane, znajdują się wartości opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="140eb-140">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="140eb-141">Sprawdź łączność tooa pamięci masowej w punkcie końcowym</span><span class="sxs-lookup"><span data-stu-id="140eb-141">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="140eb-142">Poniższy przykład Hello sprawdza łączność hello z konta magazynu blogu tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="140eb-142">hello following example tests hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="140eb-143">Przykład</span><span class="sxs-lookup"><span data-stu-id="140eb-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="140eb-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="140eb-144">Response</span></span>

<span data-ttu-id="140eb-145">Witaj następujące json jest hello przykład odpowiedzi z polecenia cmdlet poprzedniej hello.</span><span class="sxs-lookup"><span data-stu-id="140eb-145">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="140eb-146">Witaj hello docelowy jest dostępny, `ConnectionStatus` właściwość pokazuje, jak **osiągalne**.</span><span class="sxs-lookup"><span data-stu-id="140eb-146">As hello destination is reachable, hello `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="140eb-147">Podano hello szczegóły dotyczące hello liczba przeskoków wymagane tooreach hello — obiekt blob magazynu i opóźnień.</span><span class="sxs-lookup"><span data-stu-id="140eb-147">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="140eb-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="140eb-148">Next steps</span></span>

<span data-ttu-id="140eb-149">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="140eb-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="140eb-150">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które są zdefiniowane w dół.</span><span class="sxs-lookup"><span data-stu-id="140eb-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<!-- Image references -->














