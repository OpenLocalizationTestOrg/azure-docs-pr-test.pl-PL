---
title: "Sprawdź aaaverify ruchu z przepływem IP obserwatora sieci platformy Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocheck Jeśli tooor ruch z maszyny wirtualnej jest dozwolony lub odrzucany, przy użyciu programu PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Sprawdź, czy ruch jest dozwolony lub odrzucany tooor z maszyny Wirtualnej z przepływem IP Sprawdź składnik Azure obserwatora sieciowego

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Interfejs API Azure REST](network-watcher-check-ip-flow-verify-rest.md)


Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który umożliwia tooverify Jeśli ruch jest dozwolony tooor z maszyny wirtualnej. Ten scenariusz jest przydatne tooget bieżący stan czy maszynę wirtualną można rozmawiać tooan zasobu zewnętrznego i wewnętrznej bazy danych. Sprawdź przepływ IP można tooverify używane w regułach grupy zabezpieczeń sieci (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG. Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź tooensure ruchu, które mają zablokowany jest prawidłowo blokowane przez hello NSG.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego lub istniejącego wystąpienia obserwatora sieciowego. Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.

## <a name="scenario"></a>Scenariusz

Ten scenariusz używa IP przepływ Sprawdź tooverify maszynę wirtualną można, rozmawiać tooa będzie znane adresu IP usługi Bing. Ruch hello jest niedozwolone, zwraca hello reguły zabezpieczeń, która odrzuciła ten ruch. więcej informacji na temat przepływu IP sprawdzić, odwiedź stronę toolearn [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)

## <a name="retrieve-network-watcher"></a>Pobrać obserwatora sieciowego

pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia. Witaj `$networkWatcher` zmienna jest przekazywana toohello IP przepływu Sprawdź polecenia cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Uzyskiwanie maszyny Wirtualnej

Przepływ IP Sprawdź testy tooor ruch z adresu IP na tooor maszyny wirtualnej, z zdalnego miejsca docelowego. Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet hello. Jeśli znasz już identyfikator hello hello toouse maszyny wirtualnej, można pominąć ten krok.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a>Pobierz hello kart Sieciowych

adres IP karty Sieciowej na maszynie wirtualnej hello Hello jest potrzebne w tym przykładzie Pobieramy hello karty interfejsu sieciowego na maszynie wirtualnej. Jeśli znasz już IP hello adresu, który ma tootest na maszynie wirtualnej hello, możesz pominąć ten krok.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a>Sprawdź uruchomienia przepływu IP

Teraz, gdy mamy informacji hello potrzebne toorun hello polecenia cmdlet, przeprowadzana hello `Test-AzureRmNetworkWatcherIPFlow` ruchu hello tootest polecenia cmdlet. W tym przykładzie używamy hello pierwszego adresu IP na powitania pierwszej karty sieciowej.

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> Sprawdź przepływ IP wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.

## <a name="review-results"></a>Przejrzyj wyniki

Po uruchomieniu `Test-AzureRmNetworkWatcherIPFlow` hello wyniki są zwracane, hello poniższym przykładzie jest hello wyniki zwrócone z hello poprzedzających krok.

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a>Następne kroki

Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które są zdefiniowane w dół.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













