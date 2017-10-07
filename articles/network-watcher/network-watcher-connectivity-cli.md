---
title: "aaaCheck łączność z obserwatora sieciowego Azure - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak łączność toouse skontaktuj się z obserwatora sieciowego używa interfejsu wiersza polecenia platformy Azure w wersji 2.0"
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
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a>Sprawdź łączność z obserwatora sieciowego Azure używa interfejsu wiersza polecenia platformy Azure w wersji 2.0

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-connectivity-cli.md)
> - [Interfejs API Azure REST](network-watcher-connectivity-rest.md)

Dowiedz się, jak można ustalić toouse łączności tooverify Jeśli bezpośrednie połączenie TCP z tooa maszyny wirtualnej, danego punktu końcowego.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym artykule przyjęto założenie, że masz hello następujące zasoby:

* Wystąpienia obserwatora sieciowego w regionie hello ma toocheck łączności.

* Maszyny wirtualne toocheck łączność z.

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> Sprawdź łączność wymaga rozszerzenia maszyny wirtualnej `AzureNetworkWatcherExtension`. Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="register-hello-preview-capability"></a>Zarejestruj hello możliwości wersji zapoznawczej 

Sprawdź łączność jest obecnie w wersji zapoznawczej toouse ta funkcja wymaga toobe zarejestrowany. toodo, uruchom hello następujące przykładowe interfejsu wiersza polecenia

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

Rejestracja hello tooverify zakończyło się powodzeniem, uruchom następujące polecenia interfejsu wiersza polecenia hello:

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

Jeśli funkcja hello zostało prawidłowo zarejestrowane hello dane wyjściowe powinny odpowiadać hello następujące czynności: 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-tooa-virtual-machine"></a>Sprawdź maszyny wirtualnej tooa łączności

W tym przykładzie sprawdza łączność tooa docelowej maszyny wirtualnej za pośrednictwem portu 80.

### <a name="example"></a>Przykład

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a>Odpowiedź

powitania po odpowiedzi pochodzi z poprzedniego przykładu hello.  W tej odpowiedzi hello `ConnectionStatus` jest **informujący**. Widać, że wszystkie hello sond wysyłane nie powiodło się. łączność Hello na urządzenie wirtualne hello nie powiodła się z powodu tooa konfigurowane przez użytkownika `NetworkSecurityRule` o nazwie **UserRule_Port80**, skonfigurowany tooblock ruch przychodzący na porcie 80. Te informacje mogą być używane tooresearch problemy z połączeniem.

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a>Sprawdź poprawność routingu problemów

przykład Witaj służy do sprawdzania łączności między maszyną wirtualną i zdalny punkt końcowy.

### <a name="example"></a>Przykład

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a>Odpowiedź

W hello poniższy przykład, hello `connectionStatus` jest wyświetlany jako **informujący**. W hello `hops` uzyskać szczegółowe informacje, widoczny w obszarze `issues` czy ruch hello zostało zablokowane z powodu tooa `UserDefinedRoute`.

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a>Sprawdź czas oczekiwania witryny sieci Web

Witaj poniższy przykład sprawdza hello łączności tooa witryny sieci Web.

### <a name="example"></a>Przykład

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a>Odpowiedź

Hello po odpowiedzi, zawiera hello `connectionStatus` jest pokazywana jako **osiągalne**. Gdy połączenie zostanie nawiązane, znajdują się wartości opóźnienia.

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a>Sprawdź łączność tooa pamięci masowej w punkcie końcowym

Witaj poniższy przykład służy do sprawdzania hello łączności z konta magazynu blogu tooa maszyny wirtualnej.

### <a name="example"></a>Przykład

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a>Odpowiedź

Witaj następujące json jest hello przykład odpowiedzi z polecenia cmdlet poprzedniej hello. Jak wyboru hello zakończy się pomyślnie, hello `connectionStatus` właściwość pokazuje, jak **osiągalne**.  Podano hello szczegóły dotyczące hello liczba przeskoków wymagane tooreach hello — obiekt blob magazynu i opóźnień.

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)

Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)
