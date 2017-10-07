---
title: "aaaFind następnego przeskoku z Azure sieci obserwatora następnego przeskoku - PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak i można znaleźć jakie hello następnego przeskoku typu jest przy użyciu adresu ip następnego przeskoku przy użyciu programu PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure przy użyciu programu PowerShell

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-check-next-hop-cli.md)
> - [Interfejs API Azure REST](network-watcher-check-next-hop-rest.md)

Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej. Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu użyje hello Typ następnego przeskoku hello toofind portalu Azure i adres IP.

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego. Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku hello i adres IP dla każdego zasobu. odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).

## <a name="retrieve-network-watcher"></a>Pobrać obserwatora sieciowego

pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia. Witaj `$networkWatcher` zmienna jest przekazywana toohello następnego przeskoku Sprawdź polecenia cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>Uzyskiwanie maszyny wirtualnej

Następny przeskok zwraca hello następnego przeskoku i adres IP następnego przeskoku hello hello z maszyny wirtualnej. Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet hello. Jeśli znasz już identyfikator hello hello toouse maszyny wirtualnej, można pominąć ten krok.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Następnego przeskoku wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.

## <a name="get-hello-network-interfaces"></a>Pobierz interfejsy sieciowe hello

adres IP karty Sieciowej na maszynie wirtualnej hello Hello jest potrzebne w tym przykładzie Pobieramy hello karty interfejsu sieciowego na maszynie wirtualnej. Jeśli znasz już IP hello adresu, który ma tootest na maszynie wirtualnej hello, możesz pominąć ten krok.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>Pobierz następnego skoku

Teraz nazywamy hello `Get-AzureRmNetworkWatcherNextHop` polecenia cmdlet. Możemy przekazać hello polecenia cmdlet hello obserwatora sieciowego maszyny wirtualnej identyfikator, źródłowy adres IP i docelowego adresu IP. W tym przykładzie hello docelowy adres IP jest tooa maszyny Wirtualnej w innej sieci wirtualnej. Między dwiema sieciami wirtualnymi hello jest bramy sieci wirtualnej.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>Przejrzyj wyniki

Po zakończeniu hello wyniki są dostarczane. oraz hello typ zasobu, który jest zwracany jest adres IP następnego przeskoku Hello. W tym scenariuszu jest hello publicznego adresu IP bramy sieci wirtualnej hello.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

Witaj Poniższa lista zawiera aktualnie dostępne wartości Typ następnego przeskoku hello:

**Typ następnego przeskoku**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Brak

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooreview ustawieniami grupy zabezpieczeń sieci programowo, odwiedzając [NSG inspekcji z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md)

















