---
title: "Przechwytywanie pakietów aaaManage z obserwatora sieciowego Azure - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toomanage hello funkcja przechwytywania pakietów obserwatora sieciowego używa interfejsu wiersza polecenia platformy Azure w wersji 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a>Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure używa interfejsu wiersza polecenia platformy Azure w wersji 2.0

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Interfejs API Azure REST](network-watcher-packet-capture-manage-rest.md)

Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej. Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu. Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne. Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej. Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.

W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania hello zasobów management, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.

Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

Ten artykuł przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla przechwytywania pakietów.

- [**Uruchom przechwytywania pakietów**](#start-a-packet-capture)
- [**Zatrzymaj przechwytywania pakietów**](#stop-a-packet-capture)
- [**Usuń przechwytywania pakietów**](#delete-a-packet-capture)
- [**Pobierz przechwytywania pakietów**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym artykule przyjęto założenie, że masz hello następujące zasoby:

- Wystąpienia obserwatora sieciowego w regionie hello ma toocreate przechwytywania pakietów
- Maszyna wirtualna o pakietów hello przechwytywania rozszerzenie.

> [!IMPORTANT]
> Przechwytywania pakietów wymaga toobe agent uruchomiony na maszynie wirtualnej hello. Witaj Agent jest instalowany jako rozszerzenie. Aby uzyskać instrukcje dotyczące rozszerzenia maszyny Wirtualnej, odwiedź stronę [rozszerzenia maszyn wirtualnych i funkcji](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a>Zainstaluj rozszerzenia maszyny Wirtualnej

### <a name="step-1"></a>Krok 1

Uruchom hello `az vm extension set` polecenia cmdlet tooinstall hello pakietów przechwytywania agenta na maszynie wirtualnej typu Gość hello.

W przypadku maszyn wirtualnych systemu Windows:

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

Dla maszyn wirtualnych systemu Linux:

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a>Krok 2

tooensure, który hello agent jest zainstalowany, uruchom hello `vm extension get` polecenia cmdlet i przekaż go hello grupy zasobów i nazwy maszyny wirtualnej. Sprawdź, czy hello wynikowej listy tooensure hello agent jest zainstalowany.

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

następujące przykładowe Hello jest przykładem odpowiedź hello uruchamianie`az vm extension show`

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a>Uruchom przechwytywania pakietów

Po hello powyższych kroków są spełnione, agent przechwytywania pakietów hello jest zainstalowany na maszynie wirtualnej hello.

### <a name="step-1"></a>Krok 1

Witaj następnym krokiem jest tooretrieve hello obserwatora sieciowego wystąpienia. Opcjonalna nazwa hello obserwatora sieciowego jest przekazywany toohello `az network watcher show` polecenia cmdlet w kroku 4.

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a>Krok 2

Pobierz konta magazynu. To konto magazynu jest plik przechwytywania pakietów hello toostore używane.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Krok 3

Filtry mogą być używane toolimit hello dane przechowywane przez przechwytywania pakietów hello. Witaj poniższy przykład konfiguruje przechwytywania pakietów z kilka filtrów.  Witaj pierwsze trzy filtry zbierania ruch wychodzący TCP tylko z lokalny adres IP 10.0.0.3 porty toodestination 20, 80 i 443.  Filtr Hello zbiera tylko ruch UDP.

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Witaj poniższym przykładzie jest hello oczekiwane dane wyjściowe systemem hello `az network watcher packet-capture create` polecenia cmdlet.

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a>Pobierz przechwytywania pakietów

Uruchomiona hello `az network watcher packet-capture show` polecenie cmdlet pobiera stan hello przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

Witaj poniższym przykładzie jest hello dane wyjściowe hello `az network watcher packet-capture show` polecenia cmdlet. Witaj poniższym przykładzie jest po zakończeniu hello przechwytywania. z StopReason TimeExceeded Hello wartość PacketCaptureStatus jest zatrzymana. Ta wartość pokazuje, że przechwytywania pakietów hello zakończyła się pomyślnie i jego uruchomienia.

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a>Zatrzymaj przechwytywania pakietów

Uruchamiając hello `az network watcher packet-capture stop` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> Witaj polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.

## <a name="delete-a-packet-capture"></a>Usuń przechwytywania pakietów

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
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

Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
