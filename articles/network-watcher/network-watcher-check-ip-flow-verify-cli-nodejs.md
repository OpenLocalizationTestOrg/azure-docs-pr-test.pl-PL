---
title: "ruch aaaVerify Azure sieci obserwatora IP przepływ weryfikacji - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocheck Jeśli tooor ruch z maszyny wirtualnej jest dozwolony lub odrzucany, przy użyciu wiersza polecenia platformy Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Sprawdź, czy ruch jest dozwolony lub z maszyny Wirtualnej z przepływem Sprawdź IP zabronione tooor a składnik Azure obserwatora sieciowego

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Interfejs API Azure REST](network-watcher-check-ip-flow-verify-rest.md)


Przepływ IP Sprawdź jest funkcją obserwatora sieciowego, który umożliwia tooverify Jeśli ruch jest dozwolony tooor z maszyny wirtualnej. Ten scenariusz jest przydatne tooget bieżący stan czy maszynę wirtualną można rozmawiać tooan zasobu zewnętrznego i wewnętrznej bazy danych. Sprawdź przepływ IP można tooverify używane w regułach grupy zabezpieczeń sieci (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG. Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź tooensure ruchu, które mają zablokowany jest prawidłowo blokowane przez hello NSG.

W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego lub istniejącego wystąpienia obserwatora sieciowego. Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.

## <a name="scenario"></a>Scenariusz

W tym scenariuszu Sprawdź przepływ IP tooverify Jeśli maszynę wirtualną można, komunikować tooa będzie znany adres IP usługi Bing. Ruch hello jest niedozwolone, zwraca hello reguły zabezpieczeń, która odrzuciła ten ruch. toolearn więcej informacji na temat przepływu Sprawdź IP, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)


## <a name="get-a-vm"></a>Uzyskiwanie maszyny Wirtualnej

Przepływ IP Sprawdź testy tooor ruch z adresu IP na tooor maszyny wirtualnej, z zdalnego miejsca docelowego. Identyfikator maszyny wirtualnej jest wymagany dla polecenia cmdlet hello. Jeśli znasz już identyfikator hello hello toouse maszyny wirtualnej, można pominąć ten krok.

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a>Pobierz hello kart Sieciowych

adres IP karty Sieciowej na maszynie wirtualnej hello Hello jest potrzebne w tym przykładzie Pobieramy hello karty interfejsu sieciowego na maszynie wirtualnej. Jeśli znasz już IP hello adresu, który ma tootest na maszynie wirtualnej hello, możesz pominąć ten krok.

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>Sprawdź uruchomienia przepływu IP

Teraz, gdy mamy informacji hello potrzebne toorun hello polecenia cmdlet, przeprowadzana hello `network watcher ip-flow-verify` ruchu hello tootest polecenia cmdlet. W tym przykładzie używamy hello pierwszego adresu IP na powitania pierwszej karty sieciowej.

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> Przepływ IP Sprawdź wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.

## <a name="review-results"></a>Przejrzyj wyniki

Po uruchomieniu `network watcher ip-flow-verify` hello wyniki są zwracane, hello poniższym przykładzie jest hello wyniki zwrócone z hello poprzedzających krok.

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>Następne kroki

Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które są zdefiniowane w dół.

Dowiedz się tooaudit ustawienia grupy NSG, odwiedzając [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
