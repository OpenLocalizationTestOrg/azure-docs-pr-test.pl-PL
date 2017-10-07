---
title: "aaaTroubleshoot połączenia - Azure CLI 2.0 i Brama sieci wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toouse hello Azure obserwatora sieciowego Rozwiązywanie problemów z 2.0 interfejsu wiersza polecenia platformy Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a>Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu usługi Azure sieci obserwatora Azure CLI 2.0

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [Interfejs API REST](network-watcher-troubleshoot-manage-rest.md)

Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure. Jeden z tych funkcji jest zasobem rozwiązywania problemów. Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST. Po wywołaniu, obserwatora sieciowego sprawdza kondycję hello Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.

W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania hello zasobów management, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.

Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Omówienie

Rozwiązywanie problemów z zasobów umożliwia określenie hello rozwiązywania problemów, które wynikają z bramy sieci wirtualnej i połączenia. Po wysłaniu żądania jest rozwiązywanie problemów z tooresource, dzienniki są proszeni i inspekcji. Po zakończeniu kontroli hello są zwracane. Zasób, którego rozwiązywania problemów z żądania to długo działające żądania, może to potrwać kilka minut tooreturn wynik. Dzienniki Hello z Rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Pobieranie połączenia bramy sieci wirtualnej

W tym przykładzie Rozwiązywanie problemów z zasobów jest są uruchomione na połączenie. Można również przekazać go Brama sieci wirtualnej. Witaj następujące polecenie cmdlet wyświetla listę hello połączeń sieci vpn w grupie zasobów.

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

Po utworzeniu hello nazwę połączenia hello, można uruchomić tego polecenia tooget jego identyfikator zasobu:

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji hello hello zasobu, zapisuje dzienniki tooa magazynu konta toobe sprawdzone. W tym kroku utworzymy konta magazynu, jeśli istnieje już konto magazynu można go.

1. Tworzenie konta magazynu hello

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. Uzyskaj klucze konta magazynu hello

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. Tworzenie kontenera hello

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Uruchom Rozwiązywanie problemów z zasobów obserwatora sieciowego

Rozwiązywanie problemów z zasobami za pomocą hello `az network watcher troubleshooting` polecenia cmdlet. Grupy zasobów hello polecenia cmdlet hello jest przekazywana, hello nazwa hello obserwatora sieciowego, hello identyfikator połączenia hello hello identyfikator hello konta magazynu i hello ścieżki toohello obiektu blob toostore hello Rozwiązywanie problemów z wynikiem.

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

Po uruchomieniu polecenia cmdlet hello obserwatora sieciowego przegląda hello zasobów tooverify hello kondycji. Zwraca wyniki hello toohello powłoki, a są przechowywane dzienniki hello wyników na koncie magazynu hello określony.

## <a name="understanding-hello-results"></a>Opis wyników hello

tekst akcji Hello zawiera ogólne wskazówki dotyczące sposobu tooresolve hello problem. Jeśli hello problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek. W przypadku hello w przypadku, gdy nie ma żadnych dodatkowych wskazówek, odpowiedź hello zapewnia tooopen adres url hello sprawy pomocy technicznej.  Aby uzyskać więcej informacji o właściwościach hello hello odpowiedzi i dostępnych, odwiedź stronę [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)

Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage. Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)

## <a name="next-steps"></a>Następne kroki

Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.
