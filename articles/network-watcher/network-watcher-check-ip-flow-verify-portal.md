---
title: "Sprawdź aaaVerify ruchu z przepływem IP obserwatora sieci platformy Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocheck Jeśli tooor ruch z maszyny wirtualnej jest dozwolony lub niedozwolony"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
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


Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który umożliwia tooverify Jeśli ruch jest dozwolony tooor z maszyny wirtualnej. Sprawdzanie poprawności Hello mogą być uruchamiane dla ruchu przychodzącego lub wychodzącego. Ten scenariusz jest przydatne tooget bieżący stan czy maszynę wirtualną można rozmawiać zasobu zewnętrznego tooan lub innego zasobu. Sprawdź przepływ IP można tooverify używane w regułach grupy zabezpieczeń sieci (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG. Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź tooensure ruchu, które mają zablokowany jest prawidłowo blokowane przez hello NSG.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego lub istniejącego wystąpienia obserwatora sieciowego. Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.

## <a name="scenario"></a>Scenariusz

W tym scenariuszu tooverify IP przepływu Sprawdź, czy maszynę wirtualną można rozmawiać tooanother komputera za pośrednictwem portu 443. Ruch hello jest niedozwolone, zwraca hello reguły zabezpieczeń, która odrzuciła ten ruch. toolearn więcej informacji na temat przepływu Sprawdź IP, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>Sprawdź uruchomienia przepływu IP

Przejdź tooyour obserwatora sieciowego i kliknij **Sprawdź przepływ IP**. Wybierz maszynę wirtualną hello i interfejsu sieciowego interesujące tooverify ruch z. Wprowadź wszelkie dodatkowe informacje filtrowania, a następnie kliknij przycisk **Sprawdź**.

Po kliknięciu **Sprawdź**, hello przepływem na podstawie podanych kryteriów hello jest zaznaczony. wynik Hello jest **dozwolony dostęp do** lub **odmowa dostępu**. W przypadku odmowy dostępu hello grupy zabezpieczeń sieci (NSG) i podano reguły zabezpieczeń, która blokowania ruchu. Jeśli odmowa hello ruchu jest oczekiwane zachowanie, reguła hello zakończyło się pomyślnie.

> [!NOTE]
> Sprawdź przepływ IP wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona.

Jak widać na powitania po obrazu, ruch wychodzący protokołu HTTPS hello jest dozwolone.

![Przepływ IP Sprawdź — omówienie][1]

Jak pokazano w powitania po obrazu, ruch zostanie zmieniona tooinbound i hello ruchu przychodzącego too123 zmienić port. Teraz odmówiono ruchu, wiadomości powitania "Odmowa dostępu" jest dostarczany wraz z hello reguły zabezpieczeń sieci grupy i zabezpieczeń które Odmów hello ruchu.

![wyniki przepływu IP][2]

## <a name="next-steps"></a>Następne kroki

Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które są zdefiniowane w dół.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













