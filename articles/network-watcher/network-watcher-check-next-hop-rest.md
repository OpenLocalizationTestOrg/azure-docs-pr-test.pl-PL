---
title: "aaaFind następnego przeskoku z Azure sieci obserwatora następnego przeskoku - REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak i można znaleźć jakie hello następnego przeskoku typu jest adres ip przy użyciu następnego przeskoku hello interfejsu API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure przy użyciu interfejsu API REST Azure

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-check-next-hop-cli.md)
> - [Interfejs API Azure REST](network-watcher-check-next-hop-rest.md)

Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej. Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.

## <a name="before-you-begin"></a>Przed rozpoczęciem

ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell. ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku hello i adres IP dla każdego zasobu. odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).

W tym scenariuszu obejmują:

* Pobrać hello następnego skoku dla maszyny wirtualnej.

## <a name="log-in-with-armclient"></a>Zaloguj się za pomocą ARMClient

Zaloguj się za tooarmclient przy użyciu poświadczeń platformy Azure.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Pobieranie maszyny wirtualnej

Uruchom maszynę wirtualną powitania po tooreturn skryptu. Te informacje są potrzebne do uruchomienia następnego przeskoku.

Hello następującego kodu wymaga wartości dla hello następujące zmienne:

- **Identyfikator subskrypcji** — Witaj toouse identyfikator subskrypcji.
- **resourceGroupName** — Witaj Nazwa grupy zasobów, która zawiera maszyny wirtualne.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Z danych wyjściowych poniżej hello, identyfikator hello maszyny wirtualnej hello jest używany w hello poniższy przykład:

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>Pobierz następnego skoku

Po utworzeniu nagłówek autoryzacji hello hello następnego przeskoku z maszyny wirtualnej może zostać pobrany. Witaj następujące wartości należy zastąpić dla toowork przykładowy kod hello.

> [!Important]
> Dla interfejsu API REST obserwatora sieciowego wywołania hello Nazwa grupy zasobów w żądaniu hello się, że identyfikator URI jest hello grupę zasobów, która zawiera hello obserwatora sieciowego nie zasoby hello czynności diagnostyczne hello są wykonywane na.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Następnego przeskoku wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.

## <a name="results"></a>Wyniki

Witaj poniższy fragment kodu jest przykład danych wyjściowych hello odebrane. Witaj wyniki zawierają hello następujące wartości:

* **Typ następnego przeskoku** — ta wartość jest jednym z hello następujące wartości: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway lub None.
* **adres IP następnego przeskoku** — Witaj adres IP następnego przeskoku hello.
* **routeTableId** — wartość hello jest albo identyfikatorem uri dla tabeli tras hello skojarzone z trasą hello, lub zdefiniowanej przez użytkownika nie trasy jest wartość zdefiniowanych hello *trasa systemowa* jest zwracany.

Oto Hello hello wyniki w formacie json.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>Następne kroki

Po toofind stanie się hello następnego skoku dla maszyny wirtualnej można wyświetlić hello bezpieczeństwa zasobów sieciowych, odwiedzając [widok zabezpieczeń — omówienie](network-watcher-security-group-view-overview.md)














