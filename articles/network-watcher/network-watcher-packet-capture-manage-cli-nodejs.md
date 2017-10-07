---
title: "Przechwytywanie pakietów aaaManage z obserwatora sieciowego Azure - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toomanage hello funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0"
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
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a>Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Interfejs API Azure REST](network-watcher-packet-capture-manage-rest.md)

Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej. Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu. Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne. Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej. Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.

W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.

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

Uruchom hello `azure vm extension set` polecenia cmdlet tooinstall hello pakietów przechwytywania agenta na maszynie wirtualnej typu Gość hello.

W przypadku maszyn wirtualnych systemu Windows:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

Dla maszyn wirtualnych systemu Linux:

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a>Krok 2

tooensure, który hello agent jest zainstalowany, uruchom hello `vm extension get` polecenia cmdlet i przekaż go hello grupy zasobów i nazwy maszyny wirtualnej. Sprawdź, czy hello wynikowej listy tooensure hello agent jest zainstalowany.

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

następujące przykładowe Hello jest przykładem odpowiedź hello uruchamianie`azure vm extension get`

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a>Uruchom przechwytywania pakietów

Po hello powyższych kroków są spełnione, agent przechwytywania pakietów hello jest zainstalowany na maszynie wirtualnej hello.

### <a name="step-1"></a>Krok 1

Witaj następnym krokiem jest tooretrieve hello obserwatora sieciowego wystąpienia. Ta zmienna jest przekazywana toohello `network watcher show` polecenia cmdlet w kroku 4.

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a>Krok 2

Pobierz konta magazynu. To konto magazynu jest plik przechwytywania pakietów hello toostore używane.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Krok 3

Filtry mogą być używane toolimit hello dane przechowywane przez przechwytywania pakietów hello. Witaj poniższy przykład konfiguruje przechwytywania pakietów z kilka filtrów.  Witaj pierwsze trzy filtry zbierania ruch wychodzący TCP tylko z lokalny adres IP 10.0.0.3 porty toodestination 20, 80 i 443.  Filtr Hello zbiera tylko ruch UDP.

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Można zdefiniować wiele filtrów dla przechwytywania pakietów. Jeśli używasz struktury złożonych filtru jest lepsze filtry toouse jako błędy składniowe tooavoid pliku json. Na przykład użyć hello flagi "-r" (zamiast "-f") i przekaż hello lokalizację pliku json zawierający hello następujące filtry:

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


Witaj poniższym przykładzie jest hello oczekiwane dane wyjściowe systemem hello `network watcher packet-capture create` polecenia cmdlet.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a>Pobierz przechwytywania pakietów

Uruchomiona hello `network watcher packet-capture show` polecenie cmdlet pobiera stan hello przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

Witaj poniższym przykładzie jest hello dane wyjściowe hello `network watcher packet-capture show` polecenia cmdlet. Witaj poniższym przykładzie jest po zakończeniu hello przechwytywania. z StopReason TimeExceeded Hello wartość PacketCaptureStatus jest zatrzymana. Ta wartość pokazuje, że przechwytywania pakietów hello zakończyła się pomyślnie i jego uruchomienia.

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a>Zatrzymaj przechwytywania pakietów

Uruchamiając hello `network watcher packet-capture stop` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Witaj polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.

## <a name="delete-a-packet-capture"></a>Usuń przechwytywania pakietów

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
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
