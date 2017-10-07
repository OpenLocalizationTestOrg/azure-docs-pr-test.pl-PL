---
title: "Topologia obserwatora sieciowego Azure aaaView — wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooquery interfejsu wiersza polecenia Azure toouse topologii sieci."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a>Wyświetl topologia obserwatora sieciowego z wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-topology-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-topology-cli.md)
> - [Interfejs API REST](network-watcher-topology-rest.md)

Funkcja topologii Hello obserwatora sieciowego zapewnia wizualną reprezentację hello zasobów sieciowych w ramach subskrypcji. W portalu hello tej wizualizacji przedstawiono tooyou automatycznie. informacje Hello za hello widoku topologii w portalu hello mogą zostać pobrane za pomocą programu PowerShell.
Dzięki temu informacji dotyczących topologii hello bardziej elastyczne, hello danych mogą być używane przez inne narzędzia toobuild limit hello wizualizacji.

W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux. Obserwatora sieciowego aktualnie używa interfejsu wiersza polecenia platformy Azure w wersji 1.0 do obsługi interfejsu wiersza polecenia.

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

W tym scenariuszu, należy użyć hello `network watcher topology` informacje topologii hello tooretrieve polecenia cmdlet. Istnieje również artykuł na temat zbyt[pobrać topologii sieci z interfejsu API REST](network-watcher-topology-rest.md).

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule pobiera odpowiedź hello topologii dla określonej grupy zasobów.

## <a name="retrieve-topology"></a>Pobrać topologii

Witaj `network watcher topology` polecenie cmdlet pobiera hello topologii dla określonej grupy zasobów. Dodaj hello argument "--json" tooview oput hello w formacie json

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>Wyniki

Witaj wyników zwróconych ma właściwości name "zasoby", które zawiera treść odpowiedzi json hello hello `network watcher topology` polecenia cmdlet.  odpowiedź Hello zawiera zasoby hello w hello sieciowej grupy zabezpieczeń i ich powiązania (to znaczy zawiera, skojarzone).

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o hello reguły zabezpieczeń, które są stosowane tooyour zasobów sieciowych, odwiedzając [Omówienie widoku grupy zabezpieczeń](network-watcher-security-group-view-overview.md)
