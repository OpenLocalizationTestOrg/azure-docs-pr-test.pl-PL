---
title: "aaaCreate wystąpienia obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera toocreate kroki hello wystąpienia obserwatora sieciowego przy użyciu portalu hello i interfejsu API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Utwórz wystąpienie obserwatora sieciowego Azure

Obserwatora sieciowego jest usługą regionalnych, która umożliwia toomonitor możesz i diagnozowanie warunki na poziomie sieci scenariusz w, do i z platformy Azure. Scenariusz poziomu monitorowania umożliwia problemów toodiagnose na końcu tooend poziomu widok sieci. Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i uzyskać informacje na temat technologii sieci tooyour na platformie Azure.

> [!NOTE]
> Obserwatora sieciowego aktualnie obsługuje tylko 1.0 interfejsu wiersza polecenia, toocreate instrukcje hello nowego wystąpienia obserwatora sieciowego jest dostępna dla interfejsu wiersza polecenia 1.0.

## <a name="create-a-network-watcher-in-hello-portal"></a>Utwórz w portalu hello obserwatora sieciowego

Przejdź za**więcej usług** > **sieci** > **obserwatora sieciowego**. Możesz wybrać wszystkie subskrypcje hello ma tooenable obserwatora sieciowego dla. Ta akcja tworzy obserwatora sieciowego w każdym regionie dostępnej.

![Utwórz obserwatora sieciowego][1]

Po włączeniu obserwatora sieciowego przy użyciu portalu hello hello nazwę wystąpienia obserwatora sieciowego hello zostanie automatycznie ustawiona tooNetworkWatcher_region_name gdzie region_name odpowiada toohello regionu Azure, gdy włączono hello wystąpienia.  Na przykład będzie nazwę obserwatora sieciowego, włączona w regionie Zachód środkowe stany NetworkWatcher_westcentralus

Ponadto wystąpienia obserwatora sieciowego hello automatycznie zostanie dodany do grupy zasobów o nazwie NetworkWatcherRG.  Ta grupa zasobów zostanie utworzony, jeśli jeszcze nie istnieje.

Jeśli chcesz, aby nazwa hello toocustomize wystąpienia obserwatora sieciowego i hello grupy zasobów została umieszczona w, możesz użyć programu Powershell, interfejsu API REST hello lub ARMClient metod opisanych poniżej.  W przypadku każdej opcji hello grupy zasobów musi istnieć przed umieszczeniem hello obserwatora sieciowego do niego.  

## <a name="create-a-network-watcher-with-powershell"></a>Utwórz obserwatora sieciowego przy użyciu programu PowerShell

toocreate wystąpienia obserwatora sieciowego, uruchom poniższy przykład hello:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>Utwórz obserwatora sieciowego z hello interfejsu API REST

ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell. ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)

### <a name="log-in-with-armclient"></a>Zaloguj się za pomocą ARMClient

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>Utwórz hello obserwatora sieciowego

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>Następne kroki

Teraz, gdy masz wystąpienie obserwatora sieciowego Dowiedz się więcej o funkcji hello:

* [Topologia](network-watcher-topology-overview.md)
* [Przechwytywania pakietów](network-watcher-packet-capture-overview.md)
* [Weryfikowanie przepływu adresów IP](network-watcher-ip-flow-verify-overview.md)
* [Następny przeskok](network-watcher-next-hop-overview.md)
* [Widok grupy zabezpieczeń](network-watcher-security-group-view-overview.md)
* [Rejestrowanie przepływu NSG](network-watcher-nsg-flow-logging-overview.md)
* [Rozwiązywanie problemów bramy sieci wirtualnej](network-watcher-troubleshoot-overview.md)

Po utworzeniu wystąpienia obserwatora sieciowego przechwytywania pakietu można skonfigurować w następującym artykule hello: [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











