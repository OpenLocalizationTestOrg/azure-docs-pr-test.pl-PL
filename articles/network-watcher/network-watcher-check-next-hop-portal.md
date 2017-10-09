---
title: "Następny przeskok aaaFind z Azure sieci obserwatora następnego przeskoku - portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak i można znaleźć jakie hello następnego przeskoku typu jest adres ip przy użyciu następnego przeskoku hello portalu Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure za pomocą portalu hello

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-check-next-hop-cli.md)
> - [Interfejs API Azure REST](network-watcher-check-next-hop-rest.md)

Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej. Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego. Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule używa następnego przeskoku toofind Typ następnego przeskoku hello i adres IP dla każdego zasobu. odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).

W tym scenariuszu obejmują:

* Pobrać hello następnego przeskoku z maszyny wirtualnej.

## <a name="get-next-hop"></a>Pobierz następnego skoku

### <a name="step-1"></a>Krok 1

Przejdź tooyour obserwatora sieciowego zasobu w hello portalu Azure.

### <a name="step-2"></a>Krok 2

Kliknij przycisk **następnego przeskoku** w hello okienka nawigacji, wybierz hello maszyny wirtualnej i interfejsu sieciowego, wypełnij hello źródłowego i docelowego adresu IP, a następnie kliknij przycisk hello **następnego przeskoku** przycisku.

> [!NOTE]
> Następnego przeskoku wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona toorun.

![Pobierz następnego przeskoku — omówienie][1]

### <a name="step-3"></a>Krok 3

Po zakończeniu zadania hello hello wyniki są dostarczane. Witaj, adres IP i typ następnego przeskoku hello urządzenia jest, zostanie wyświetlony. Witaj poniższej tabeli przedstawiono dostępne wartości zwracane hello w portalu hello.

**Typ następnego przeskoku**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Brak

Jeśli niestandardowa trasa został użyty tooroute ten ruch trasy zdefiniowane przez użytkownika hello (przez) wyświetlany jest również z wynikami hello.

![Następny przeskok wyniki][2]

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooreview ustawieniami grupy zabezpieczeń sieci programowo, odwiedzając [NSG inspekcji z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














