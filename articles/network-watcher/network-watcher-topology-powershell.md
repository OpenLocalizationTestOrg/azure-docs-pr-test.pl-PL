---
title: "Topologia obserwatora sieciowego Azure aaaView — PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toouse PowerShell tooquery topologii sieci."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a>Wyświetl topologii obserwatora sieciowego przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-topology-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-topology-cli.md)
> - [Interfejs API REST](network-watcher-topology-rest.md)

Funkcja topologii Hello obserwatora sieciowego zapewnia wizualną reprezentację hello zasobów sieciowych w ramach subskrypcji. W portalu hello tej wizualizacji przedstawiono tooyou automatycznie. informacje Hello za hello widoku topologii w portalu hello mogą zostać pobrane za pomocą programu PowerShell.
Dzięki temu informacji dotyczących topologii hello bardziej elastyczne, hello danych mogą być używane przez inne narzędzia toobuild limit hello wizualizacji.

w obszarze dwie relacje w modelu Hello połączenia.

- **Zawieranie** — przykład: sieć wirtualna zawiera podsieć zawiera karty Sieciowej
- **Skojarzone** — przykład: karta sieciowa jest skojarzona z maszyną Wirtualną

Witaj poniżej znajduje się właściwości, które są zwracane, gdy zapytanie hello interfejsu API REST topologii.

* **Nazwa** — Witaj Nazwa zasobu hello
* **Identyfikator** — Witaj identyfikatora uri zasobu hello.
* **Lokalizacja** — Witaj lokalizacji, w której istnieje zasób hello.
* **skojarzenia** — lista toohello skojarzenia odwołuje się do obiektu.
    * **Nazwa** — nazwa hello hello odwołuje się do zasobu.
    * **resourceId** -hello resourceId jest identyfikatorem uri hello hello zasobu, do którego odwołuje się powiązanie hello.
    * **Obiekt associationType** -hello relacja między hello obiektu podrzędnego i nadrzędnego hello odwołuje się do tej wartości. Prawidłowe wartości to **zawiera** lub **skojarzone**.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu, należy użyć hello `Get-AzureRmNetworkWatcherTopology` informacje topologii hello tooretrieve polecenia cmdlet. Istnieje również artykuł na temat zbyt[pobrać topologii sieci z interfejsu API REST](network-watcher-topology-rest.md).

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule pobiera odpowiedź hello topologii dla określonej grupy zasobów.

## <a name="retrieve-network-watcher"></a>Pobrać obserwatora sieciowego

pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia. Witaj `$networkWatcher` zmienna jest przekazywana toohello `Get-AzureRmNetworkWatcherTopology` polecenia cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a>Pobrać topologii

Witaj `Get-AzureRmNetworkWatcherTopology` polecenie cmdlet pobiera hello topologii dla określonej grupy zasobów.

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a>Wyniki

Witaj wyników zwróconych ma właściwości name "zasoby", które zawiera treść odpowiedzi json hello hello `Get-AzureRmNetworkWatcherTopology` polecenia cmdlet.  odpowiedź Hello zawiera zasoby hello w hello sieciowej grupy zabezpieczeń i ich powiązania (to znaczy zawiera, skojarzone).

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


