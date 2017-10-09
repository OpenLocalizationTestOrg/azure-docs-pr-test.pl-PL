---
title: "Przechwytywanie pakietów aaaManage z obserwatora sieciowego Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak pakietów hello toomanage przechwytywania funkcji obserwatora sieciowego przy użyciu programu PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="ce3e8-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce3e8-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ce3e8-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ce3e8-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="ce3e8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce3e8-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="ce3e8-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="ce3e8-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="ce3e8-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="ce3e8-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="ce3e8-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="ce3e8-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="ce3e8-109">Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="ce3e8-110">Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="ce3e8-111">Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="ce3e8-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="ce3e8-113">Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="ce3e8-114">Ten artykuł przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="ce3e8-115">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="ce3e8-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="ce3e8-116">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="ce3e8-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="ce3e8-117">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="ce3e8-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="ce3e8-118">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="ce3e8-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="ce3e8-119">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ce3e8-119">Before you begin</span></span>

<span data-ttu-id="ce3e8-120">W tym artykule przyjęto założenie, że masz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="ce3e8-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="ce3e8-121">Wystąpienia obserwatora sieciowego w regionie hello ma toocreate przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="ce3e8-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="ce3e8-122">Maszyna wirtualna o pakietów hello przechwytywania rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce3e8-123">Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="ce3e8-124">Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="ce3e8-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="ce3e8-125">Zainstaluj rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ce3e8-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="ce3e8-126">Krok 1</span><span class="sxs-lookup"><span data-stu-id="ce3e8-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="ce3e8-127">Krok 2</span><span class="sxs-lookup"><span data-stu-id="ce3e8-127">Step 2</span></span>

<span data-ttu-id="ce3e8-128">Witaj poniższy przykład pobiera hello informacji o rozszerzeniu potrzebne toorun hello `Set-AzureRmVMExtension` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="ce3e8-129">To polecenie cmdlet instaluje agenta przechwytywania pakietów hello na maszynie wirtualnej typu Gość hello.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="ce3e8-130">Witaj `Set-AzureRmVMExtension` polecenie cmdlet może potrwać kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="ce3e8-131">W przypadku maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="ce3e8-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="ce3e8-132">Dla maszyn wirtualnych systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="ce3e8-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="ce3e8-133">Witaj poniższym przykładzie przedstawiono pomyślnej odpowiedzi po uruchomieniu hello `Set-AzureRmVMExtension` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="ce3e8-134">Krok 3</span><span class="sxs-lookup"><span data-stu-id="ce3e8-134">Step 3</span></span>

<span data-ttu-id="ce3e8-135">tooensure, który hello agent jest zainstalowany, uruchom hello `Get-AzureRmVMExtension` polecenia cmdlet i przekaż go hello nazwę maszyny wirtualnej i hello Nazwa rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="ce3e8-136">następujące przykładowe Hello jest przykładem odpowiedź hello uruchamianie`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="ce3e8-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="ce3e8-137">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="ce3e8-137">Start a packet capture</span></span>

<span data-ttu-id="ce3e8-138">Po hello powyższych kroków są spełnione, agent przechwytywania pakietów hello jest zainstalowany na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="ce3e8-139">Krok 1</span><span class="sxs-lookup"><span data-stu-id="ce3e8-139">Step 1</span></span>

<span data-ttu-id="ce3e8-140">Witaj następnym krokiem jest tooretrieve hello obserwatora sieciowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="ce3e8-141">Ta zmienna jest przekazywana toohello `New-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="ce3e8-142">Krok 2</span><span class="sxs-lookup"><span data-stu-id="ce3e8-142">Step 2</span></span>

<span data-ttu-id="ce3e8-143">Pobierz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-143">Retrieve a storage account.</span></span> <span data-ttu-id="ce3e8-144">To konto magazynu jest plik przechwytywania pakietów hello toostore używane.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="ce3e8-145">Krok 3</span><span class="sxs-lookup"><span data-stu-id="ce3e8-145">Step 3</span></span>

<span data-ttu-id="ce3e8-146">Filtry mogą być używane toolimit hello dane przechowywane przez przechwytywania pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="ce3e8-147">Witaj poniższy przykład przedstawia dwa filtry.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="ce3e8-148">Zbiera jeden filtr wychodzącego TCP ruchu tylko z lokalny adres IP 10.0.0.3 porty toodestination 20, 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="ce3e8-149">drugi filtr Hello zbiera tylko ruch UDP.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="ce3e8-150">Można zdefiniować wiele filtrów dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="ce3e8-151">Krok 4</span><span class="sxs-lookup"><span data-stu-id="ce3e8-151">Step 4</span></span>

<span data-ttu-id="ce3e8-152">Uruchom hello `New-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet toostart hello pakietów proces przechwytywania, przekazanie wartości hello wymagane pobierane w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="ce3e8-153">Witaj poniższym przykładzie jest hello oczekiwane dane wyjściowe systemem hello `New-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="ce3e8-154">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="ce3e8-154">Get a packet capture</span></span>

<span data-ttu-id="ce3e8-155">Uruchomiona hello `Get-AzureRmNetworkWatcherPacketCapture` polecenie cmdlet pobiera stan hello przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="ce3e8-156">Witaj poniższym przykładzie jest hello dane wyjściowe hello `Get-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="ce3e8-157">Witaj poniższym przykładzie jest po zakończeniu hello przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="ce3e8-158">z StopReason TimeExceeded Hello wartość PacketCaptureStatus jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="ce3e8-159">Ta wartość pokazuje, że przechwytywania pakietów hello zakończyła się pomyślnie i jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-159">This value shows that hello packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="ce3e8-160">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="ce3e8-160">Stop a packet capture</span></span>

<span data-ttu-id="ce3e8-161">Uruchamiając hello `Stop-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="ce3e8-162">Witaj polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="ce3e8-163">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="ce3e8-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="ce3e8-164">Usunięcie przechwytywania pakietów nie powoduje usunięcia pliku hello hello koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="ce3e8-165">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="ce3e8-165">Download a packet capture</span></span>

<span data-ttu-id="ce3e8-166">Po zakończeniu sesji przechwytywania pakietów hello pliku przechwytywania może być przekazane tooblob tooa lub magazynu lokalnego pliku na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="ce3e8-167">Lokalizacja przechowywania Hello przechwytywania pakietów hello jest definiowany podczas tworzenia hello sesji.</span><span class="sxs-lookup"><span data-stu-id="ce3e8-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="ce3e8-168">Tooaccess wygodne narzędzie te Przechwytywanie plików, tooa zapisane konto magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="ce3e8-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="ce3e8-169">Jeśli określono konto magazynu, zapisywane są pliki przechwytywania pakietów tooa konta magazynu w następującej lokalizacji hello:</span><span class="sxs-lookup"><span data-stu-id="ce3e8-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="ce3e8-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ce3e8-170">Next steps</span></span>

<span data-ttu-id="ce3e8-171">Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="ce3e8-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="ce3e8-172">Znajdź, jeśli niektórych ruch jest dozwolony w orr poza maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ce3e8-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














