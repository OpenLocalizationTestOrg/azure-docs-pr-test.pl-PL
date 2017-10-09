---
title: "Topologia obserwatora sieciowego Azure aaaView — interfejs API REST | Dokumentacja firmy Microsoft"
description: W tym artykule opisano, jak toouse REST API tooquery topologii sieci.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>Wyświetl topologią obserwatora sieciowego za pomocą interfejsu API REST

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

W tym scenariuszu można pobrać informacji o topologii hello. ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell. ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule pobiera odpowiedź hello topologii dla określonej grupy zasobów.

## <a name="log-in-with-armclient"></a>Zaloguj się za pomocą ARMClient

Zaloguj się za tooarmclient przy użyciu poświadczeń platformy Azure.

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>Pobrać topologii

Poniższy przykład Hello żądanie topologii hello hello interfejsu API REST.  przykład Witaj jest sparametryzowane tooallow elastyczność tworzenia przykładem.  Zamień wszystkie wartości z \< \> między nimi.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

powitania po odpowiedzi jest przykładem skróconą odpowiedzi, który jest zwracany, gdy pobrać topologii grupa zasobów:

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

