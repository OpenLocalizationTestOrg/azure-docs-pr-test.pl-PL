---
title: "zabezpieczenia sieci aaaAnalyze z widokiem grupy obserwatorów zabezpieczeń Azure sieci — interfejs API REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse tooanalyze programu PowerShell, a wirtualnych maszyn zabezpieczeń z widokiem grupy zabezpieczeń."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a>Analizowanie zabezpieczeń maszyny wirtualnej z widoku grupy zabezpieczeń przy użyciu interfejsu API REST

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-security-group-view-cli.md)
> - [Interfejs API REST](network-watcher-security-group-view-rest.md)

Widok grupy zabezpieczeń zwraca reguły zabezpieczeń sieci skonfigurowane i skuteczne, które są stosowane tooa maszyny wirtualnej. Ta funkcja jest przydatna tooaudit i diagnozowanie grup zabezpieczeń sieci i reguł, które są skonfigurowane na ruch tooensure maszyn wirtualnych są poprawnie dozwolony lub niedozwolony. W tym artykule zostanie przedstawiony zostanie sposób tooretrieve hello skuteczne i zastosowane reguł tooa maszyny wirtualnej za pomocą interfejsu API REST

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu należy wywołać widok grupy zabezpieczeń tooget hello hello interfejsu API Rest obserwatorów sieci dla maszyny wirtualnej. ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell. ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego. Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule pobiera hello reguły zabezpieczeń skuteczne i zastosowane dla podanej maszyny wirtualnej.

## <a name="log-in-with-armclient"></a>Zaloguj się za pomocą ARMClient

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Pobieranie maszyny wirtualnej

Uruchom hello następującego skryptu tooreturn wirtualnego machineThe następującego kodu wymaga zmiennych:

- **Identyfikator subskrypcji** -hello identyfikator subskrypcji można również pobrać z hello **Get-AzureRMSubscription** polecenia cmdlet.
- **resourceGroupName** — Witaj Nazwa grupy zasobów, która zawiera maszyny wirtualne.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Witaj potrzebna jest hello **identyfikator** typu hello `Microsoft.Compute/virtualMachines` w odpowiedzi, jak pokazano w hello poniższy przykład:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a>Pobierz widok grupy zabezpieczeń dla maszyny wirtualnej

Poniższy przykład Hello żądań widok grupy zabezpieczeń hello docelowej maszyny wirtualnej. wyniki Hello w tym przykładzie może być używane toocompare toohello reguł i zdefiniowanych przez hello utworzenia toolook dla odejście konfiguracji zabezpieczeń.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a>Wyświetl hello odpowiedź

następujące przykładowe Hello jest hello odpowiedź zwrócona z hello poprzedzających polecenia. Witaj w wynikach wszystkich reguł zabezpieczeń skuteczne i zastosowane hello na maszynie wirtualnej hello podziale grupy **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, i  **EffectiveSecurityRules**.

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a>Następne kroki

Odwiedź stronę [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-security-group-view-powershell.md) toolearn sposób weryfikacji tooautomate grup zabezpieczeń sieci.


