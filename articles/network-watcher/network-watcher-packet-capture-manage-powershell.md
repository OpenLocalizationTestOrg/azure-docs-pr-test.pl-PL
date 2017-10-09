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
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a>Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Interfejs API Azure REST](network-watcher-packet-capture-manage-rest.md)

Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej. Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu. Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne. Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej. Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.

Ten artykuł przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla przechwytywania pakietów.

- [**Uruchom przechwytywania pakietów**](#start-a-packet-capture)
- [**Zatrzymaj przechwytywania pakietów**](#stop-a-packet-capture)
- [**Usuń przechwytywania pakietów**](#delete-a-packet-capture)
- [**Pobierz przechwytywania pakietów**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym artykule przyjęto założenie, że masz hello następujące zasoby:

* Wystąpienia obserwatora sieciowego w regionie hello ma toocreate przechwytywania pakietów

* Maszyna wirtualna o pakietów hello przechwytywania rozszerzenie.

> [!IMPORTANT]
> Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`. Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a>Zainstaluj rozszerzenia maszyny Wirtualnej

### <a name="step-1"></a>Krok 1

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a>Krok 2

Witaj poniższy przykład pobiera hello informacji o rozszerzeniu potrzebne toorun hello `Set-AzureRmVMExtension` polecenia cmdlet. To polecenie cmdlet instaluje agenta przechwytywania pakietów hello na maszynie wirtualnej typu Gość hello.

> [!NOTE]
> Witaj `Set-AzureRmVMExtension` polecenie cmdlet może potrwać kilka minut toocomplete.

W przypadku maszyn wirtualnych systemu Windows:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

Dla maszyn wirtualnych systemu Linux:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

Witaj poniższym przykładzie przedstawiono pomyślnej odpowiedzi po uruchomieniu hello `Set-AzureRmVMExtension` polecenia cmdlet.

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a>Krok 3

tooensure, który hello agent jest zainstalowany, uruchom hello `Get-AzureRmVMExtension` polecenia cmdlet i przekaż go hello nazwę maszyny wirtualnej i hello Nazwa rozszerzenia.

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

następujące przykładowe Hello jest przykładem odpowiedź hello uruchamianie`Get-AzureRmVMExtension`

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

## <a name="start-a-packet-capture"></a>Uruchom przechwytywania pakietów

Po hello powyższych kroków są spełnione, agent przechwytywania pakietów hello jest zainstalowany na maszynie wirtualnej hello.

### <a name="step-1"></a>Krok 1

Witaj następnym krokiem jest tooretrieve hello obserwatora sieciowego wystąpienia. Ta zmienna jest przekazywana toohello `New-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet w kroku 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a>Krok 2

Pobierz konta magazynu. To konto magazynu jest plik przechwytywania pakietów hello toostore używane.

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a>Krok 3

Filtry mogą być używane toolimit hello dane przechowywane przez przechwytywania pakietów hello. Witaj poniższy przykład przedstawia dwa filtry.  Zbiera jeden filtr wychodzącego TCP ruchu tylko z lokalny adres IP 10.0.0.3 porty toodestination 20, 80 i 443.  drugi filtr Hello zbiera tylko ruch UDP.

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> Można zdefiniować wiele filtrów dla przechwytywania pakietów.

### <a name="step-4"></a>Krok 4

Uruchom hello `New-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet toostart hello pakietów proces przechwytywania, przekazanie wartości hello wymagane pobierane w poprzednich krokach hello.
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

Witaj poniższym przykładzie jest hello oczekiwane dane wyjściowe systemem hello `New-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet.

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

## <a name="get-a-packet-capture"></a>Pobierz przechwytywania pakietów

Uruchomiona hello `Get-AzureRmNetworkWatcherPacketCapture` polecenie cmdlet pobiera stan hello przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

Witaj poniższym przykładzie jest hello dane wyjściowe hello `Get-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet. Witaj poniższym przykładzie jest po zakończeniu hello przechwytywania. z StopReason TimeExceeded Hello wartość PacketCaptureStatus jest zatrzymana. Ta wartość pokazuje, że przechwytywania pakietów hello zakończyła się pomyślnie i jego uruchomienia.
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

## <a name="stop-a-packet-capture"></a>Zatrzymaj przechwytywania pakietów

Uruchamiając hello `Stop-AzureRmNetworkWatcherPacketCapture` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Witaj polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.

## <a name="delete-a-packet-capture"></a>Usuń przechwytywania pakietów

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> Usunięcie przechwytywania pakietów nie powoduje usunięcia pliku hello hello koncie magazynu.

## <a name="download-a-packet-capture"></a>Pobierz przechwytywania pakietów

Po zakończeniu sesji przechwytywania pakietów hello pliku przechwytywania może być przekazane tooblob tooa lub magazynu lokalnego pliku na powitania maszyny Wirtualnej. Lokalizacja przechowywania Hello przechwytywania pakietów hello jest definiowany podczas tworzenia hello sesji. Tooaccess wygodne narzędzie te Przechwytywanie plików, tooa zapisane konto magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/

Jeśli określono konto magazynu, zapisywane są pliki przechwytywania pakietów tooa konta magazynu w następującej lokalizacji hello:

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)

Znajdź, jeśli niektórych ruch jest dozwolony w orr poza maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->














