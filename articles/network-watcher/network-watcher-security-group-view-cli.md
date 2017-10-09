---
title: "zabezpieczenia sieci aaaAnalyze z widokiem grupy obserwatorów zabezpieczeń Azure sieci - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooanalyze toouse 2.0 interfejsu wiersza polecenia Azure, a wirtualnych maszyn zabezpieczeń z widokiem grupy zabezpieczeń."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a>Analizowanie zabezpieczeń maszyny wirtualnej z widokiem grupy zabezpieczeń używa interfejsu wiersza polecenia platformy Azure w wersji 2.0

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-security-group-view-cli.md)
> - [Interfejs API REST](network-watcher-security-group-view-rest.md)

Widok grupy zabezpieczeń zwraca reguły zabezpieczeń sieci skonfigurowane i skuteczne, które są stosowane tooa maszyny wirtualnej. Ta funkcja jest przydatna tooaudit i diagnozowanie grup zabezpieczeń sieci i reguł, które są skonfigurowane na ruch tooensure maszyn wirtualnych są poprawnie dozwolony lub niedozwolony. W tym artykule możemy wyświetlić konfiguracji tooretrieve hello i efektywnym elementem systemu zabezpieczeń reguły tooa maszyny wirtualnej za pomocą wiersza polecenia platformy Azure


W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania hello zasobów management, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.

Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule pobiera hello skonfigurowane i reguły efektywnym elementem systemu zabezpieczeń dla podanej maszyny wirtualnej.

## <a name="get-a-vm"></a>Uzyskiwanie maszyny Wirtualnej

Maszyna wirtualna jest wymagana toorun hello `vm list` polecenia cmdlet. Witaj następujące polecenie wyświetla listę hello maszyny wirtualne w grupie zasobów:

```azurecli
az vm list -resource-group resourceGroupName
```

Jeśli znasz już hello maszyny wirtualnej, można użyć hello `vm show` tooget polecenia cmdlet jego identyfikator zasobu:

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a>Pobierz widok grupy zabezpieczeń

Witaj następnym krokiem jest wynik widoku tooretrieve hello zabezpieczeń grupy.

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a>Wyświetlanie wyników hello

Witaj poniższy przykład jest skróconą odpowiedzi hello wyniki zwrócone. Witaj w wynikach wszystkich reguł zabezpieczeń skuteczne i zastosowane hello na maszynie wirtualnej hello podziale grupy **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, i  **EffectiveSecurityRules**.

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a>Następne kroki

Odwiedź stronę [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md) toolearn sposób weryfikacji tooautomate grup zabezpieczeń sieci.

Dowiedz się więcej o hello reguły zabezpieczeń, które są stosowane tooyour zasobów sieciowych, odwiedzając [Omówienie widoku grupy zabezpieczeń](network-watcher-security-group-view-overview.md)
