---
title: "Sprawdź aaaVerify ruchu z przepływem IP obserwatora sieci platformy Azure - REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocheck Jeśli tooor ruch z maszyny wirtualnej jest dozwolony lub niedozwolony"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Sprawdź, czy ruch jest dozwolony lub odrzucany z przepływem IP Sprawdź składnik Azure obserwatora sieciowego

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Interfejs API Azure REST](network-watcher-check-ip-flow-verify-rest.md)


Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który umożliwia tooverify Jeśli ruch jest dozwolony tooor z maszyny wirtualnej. Sprawdzanie poprawności Hello mogą być uruchamiane dla ruchu przychodzącego lub wychodzącego. Ten scenariusz jest przydatne tooget bieżący stan czy maszynę wirtualną można rozmawiać tooan zasobu zewnętrznego i wewnętrznej bazy danych. Sprawdź przepływ IP można tooverify używane w regułach grupy zabezpieczeń sieci (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG. Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź tooensure ruchu, które mają zablokowany jest prawidłowo blokowane przez hello NSG.

## <a name="before-you-begin"></a>Przed rozpoczęciem

ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell. ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

## <a name="scenario"></a>Scenariusz

W tym scenariuszu tooverify Sprawdź przepływ IP Jeśli maszynę wirtualną można rozmawiać tooanother komputera za pośrednictwem portu 443. Ruch hello jest niedozwolone, zwraca hello reguły zabezpieczeń, która odrzuciła ten ruch. toolearn więcej informacji na temat przepływu IP upewnij się, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)

W tym scenariuszu należy:

* Pobieranie maszyny wirtualnej
* Sprawdź połączenie IP przepływu
* Sprawdź wyniki

## <a name="log-in-with-armclient"></a>Zaloguj się za pomocą ARMClient

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Pobieranie maszyny wirtualnej

Uruchom maszynę wirtualną powitania po tooreturn skryptu. Witaj następujący kod wymaga wartości zmiennych hello:

* **Identyfikator subskrypcji** — Witaj toouse identyfikator subskrypcji.
* **resourceGroupName** — Witaj Nazwa grupy zasobów, która zawiera maszyny wirtualne.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Witaj informacje potrzebne jest hello identyfikator typu hello `Microsoft.Compute/virtualMachines`. Hello wyniki powinny być podobne toohello po przykładowym kodzie:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a>Wywołanie IP przepływu Sprawdź

Witaj poniższy przykład tworzy żądanie tooverify hello ruchu dla określonej maszyny wirtualnej. odpowiedź Hello zwraca czy hello ruch jest dozwolony, czy ruch hello jest zabroniony. Jeśli ruch odmówiono ona również zwraca jakie bloków reguł hello ruchu.

> [!NOTE]
> Sprawdź przepływ IP wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona.

skrypt Hello wymaga zasobów hello identyfikator maszyny wirtualnej i karty interfejsu sieciowego na maszynie wirtualnej hello. Wartości te są dostarczane przez hello poprzedzających danych wyjściowych.

> [!Important]
> Dla wszystkich pozostałych obserwatora sieciowego wywołania hello Nazwa grupy zasobów w żądaniu hello hello taką, która zawiera nie zasoby hello czynności diagnostyczne hello są wykonywane na powitania wystąpienia obserwatora sieciowego, to identyfikator URI.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a>Opis wyników hello

odpowiedź Hello, wracając informuje, czy ruch hello jest dozwolony lub niedozwolony. odpowiedź Hello wygląda jedną hello następujące przykłady:

**Dozwolone**

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

**Odmowa dostępu**

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a>Następne kroki

Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn więcej informacji na temat grup zabezpieczeń sieci.












