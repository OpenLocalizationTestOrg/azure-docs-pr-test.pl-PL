---
title: "Zarządzanie przechwytywania pakietów z obserwatora sieciowego Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśnia sposób zarządzania funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu programu PowerShell"
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
ms.openlocfilehash: abd3b3641da80ee835fac85b4bde68594449e451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="61020-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="61020-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="61020-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="61020-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="61020-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="61020-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="61020-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="61020-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="61020-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="61020-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="61020-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="61020-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="61020-109">Przechwytywania pakietów obserwatora sieciowego umożliwia tworzenie sesji przechwytywania, aby śledzić ruch do i z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61020-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="61020-110">Filtry są dostępne dla sesji przechwytywania, aby upewnić się, że przechwytywać ruch, który ma.</span><span class="sxs-lookup"><span data-stu-id="61020-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="61020-111">Przechwytywania pakietów ułatwia diagnozowanie anomalii sieci rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="61020-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="61020-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat wtargnięcia sieci, aby debugować komunikacja klient serwer i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="61020-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="61020-113">Dzięki możliwości zdalnie wywołać przechwytywania pakietów, ta funkcja ułatwia obciążeń uruchomionych przechwytywania pakietów, ręcznie i tylko na odpowiednią maszynę, która zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="61020-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="61020-114">Ten artykuł przedstawia za pomocą zadań zarządzania różnych, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="61020-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="61020-115">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="61020-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="61020-116">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="61020-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="61020-117">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="61020-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="61020-118">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="61020-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="61020-119">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="61020-119">Before you begin</span></span>

<span data-ttu-id="61020-120">W tym artykule przyjęto założenie, że masz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="61020-120">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="61020-121">Wystąpienia obserwatora sieciowego w regionie, w którym chcesz utworzyć przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="61020-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>

* <span data-ttu-id="61020-122">Maszyna wirtualna z rozszerzeniem przechwytywania pakietów włączone.</span><span class="sxs-lookup"><span data-stu-id="61020-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61020-123">Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="61020-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="61020-124">Instalowanie rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="61020-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="61020-125">Zainstaluj rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="61020-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="61020-126">Krok 1</span><span class="sxs-lookup"><span data-stu-id="61020-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="61020-127">Krok 2</span><span class="sxs-lookup"><span data-stu-id="61020-127">Step 2</span></span>

<span data-ttu-id="61020-128">Poniższy przykład pobiera rozszerzenie informacje potrzebne do uruchomienia `Set-AzureRmVMExtension` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="61020-128">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="61020-129">To polecenie cmdlet instaluje agenta przechwytywania pakietów na maszynie wirtualnej gościa.</span><span class="sxs-lookup"><span data-stu-id="61020-129">This cmdlet installs the packet capture agent on the guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="61020-130">`Set-AzureRmVMExtension` Polecenie cmdlet może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="61020-130">The `Set-AzureRmVMExtension` cmdlet may take several minutes to complete.</span></span>

<span data-ttu-id="61020-131">W przypadku maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="61020-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="61020-132">Dla maszyn wirtualnych systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="61020-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="61020-133">Poniższy przykład jest odpowiedź oznaczająca Powodzenie po uruchomieniu `Set-AzureRmVMExtension` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="61020-133">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="61020-134">Krok 3</span><span class="sxs-lookup"><span data-stu-id="61020-134">Step 3</span></span>

<span data-ttu-id="61020-135">Aby upewnić się, że agent jest zainstalowany, należy uruchomić `Get-AzureRmVMExtension` polecenia cmdlet i przekaż go nazwę maszyny wirtualnej i nazwa rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="61020-135">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="61020-136">Poniższy przykład jest przykładem uruchamianie odpowiedzi`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="61020-136">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="61020-137">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="61020-137">Start a packet capture</span></span>

<span data-ttu-id="61020-138">Po zakończeniu powyższych kroków agent przechwytywania pakietów jest zainstalowany na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61020-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="61020-139">Krok 1</span><span class="sxs-lookup"><span data-stu-id="61020-139">Step 1</span></span>

<span data-ttu-id="61020-140">Następnym krokiem jest w celu pobrania wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="61020-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="61020-141">Ta zmienna jest przekazywana do `New-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="61020-141">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="61020-142">Krok 2</span><span class="sxs-lookup"><span data-stu-id="61020-142">Step 2</span></span>

<span data-ttu-id="61020-143">Pobierz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="61020-143">Retrieve a storage account.</span></span> <span data-ttu-id="61020-144">To konto magazynu jest używany do przechowywania pliku przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="61020-144">This storage account is used to store the packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="61020-145">Krok 3</span><span class="sxs-lookup"><span data-stu-id="61020-145">Step 3</span></span>

<span data-ttu-id="61020-146">Można używać filtrów w celu ograniczenia danych, który jest przechowywany przez przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="61020-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="61020-147">Poniższy przykład przedstawia dwa filtry.</span><span class="sxs-lookup"><span data-stu-id="61020-147">The following example sets up two filters.</span></span>  <span data-ttu-id="61020-148">Jeden filtr zbiera ruch wychodzący TCP tylko lokalny adres IP 10.0.0.3 do porty docelowe 20, 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="61020-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="61020-149">Drugi filtr zbiera tylko ruch UDP.</span><span class="sxs-lookup"><span data-stu-id="61020-149">The second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="61020-150">Można zdefiniować wiele filtrów dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="61020-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="61020-151">Krok 4</span><span class="sxs-lookup"><span data-stu-id="61020-151">Step 4</span></span>

<span data-ttu-id="61020-152">Uruchom `New-AzureRmNetworkWatcherPacketCapture` pobrać polecenia cmdlet, aby rozpocząć proces przechwytywania pakietów, przekazywanie wymagane wartości w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="61020-152">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="61020-153">Poniższy przykład jest oczekiwane dane wyjściowe uruchamianie `New-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="61020-153">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="61020-154">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="61020-154">Get a packet capture</span></span>

<span data-ttu-id="61020-155">Uruchomiona `Get-AzureRmNetworkWatcherPacketCapture` polecenie cmdlet pobiera stan przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="61020-155">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="61020-156">Poniższy przykład jest wynikiem `Get-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="61020-156">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="61020-157">Poniższy przykład jest po zakończeniu przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="61020-157">The following example is after the capture is complete.</span></span> <span data-ttu-id="61020-158">Wartość PacketCaptureStatus została zatrzymana z StopReason TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="61020-158">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="61020-159">Ta wartość pokazuje, że przechwytywania pakietów zakończyła się pomyślnie i jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="61020-159">This value shows that the packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="61020-160">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="61020-160">Stop a packet capture</span></span>

<span data-ttu-id="61020-161">Uruchamiając `Stop-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="61020-161">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="61020-162">Polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="61020-162">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="61020-163">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="61020-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="61020-164">Usunięcie przechwytywania pakietów nie powoduje usunięcia plików na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="61020-164">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="61020-165">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="61020-165">Download a packet capture</span></span>

<span data-ttu-id="61020-166">Po zakończeniu sesji przechwytywania pakietów, plik przechwytywania można przekazać do magazynu obiektów blob lub do pliku lokalnego na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="61020-166">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="61020-167">Lokalizacja magazynu przechwytywania pakietów jest definiowany podczas tworzenia sesji.</span><span class="sxs-lookup"><span data-stu-id="61020-167">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="61020-168">Wygodne narzędzie one dostęp do plików przechwytywania na koncie magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="61020-168">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="61020-169">Jeśli określono konto magazynu, pliki przechwytywania pakietów są zapisywane na koncie magazynu w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="61020-169">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="61020-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61020-170">Next steps</span></span>

<span data-ttu-id="61020-171">Dowiedz się, jak można zautomatyzować przechwytywania pakietów z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="61020-171">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="61020-172">Znajdź, jeśli niektórych ruch jest dozwolony w orr poza maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="61020-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














