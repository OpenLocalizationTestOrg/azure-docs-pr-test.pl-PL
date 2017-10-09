---
title: "aaaMultiple adresów VIP usługi równoważenia obciążenia Azure | Dokumentacja firmy Microsoft"
description: "Omówienie wielu adresów VIP modułu równoważenia obciążenia Azure"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Obsługa wielu adresów VIP dla usługi Azure Load Balancer

Moduł równoważenia obciążenia Azure umożliwia tooload zrównoważyć usług w wielu portów i/lub wiele adresów IP. Możesz użyć obciążenia publicznych oraz wewnętrznych równoważenia definicje tooload saldo przepływów zestawu maszyn wirtualnych.

W tym artykule opisano podstawy hello tej możliwości, ważne pojęcia i ograniczeń. Jeśli planujesz usług tooexpose tylko na jeden adres IP, można znaleźć uproszczony instrukcje dotyczące [publicznego](load-balancer-get-started-internet-portal.md) lub [wewnętrzny](load-balancer-get-started-ilb-arm-portal.md) konfiguracji usługi równoważenia obciążenia. Dodawanie wielu adresów VIP jest przyrostowe tooa pojedynczą konfiguracją adresu VIP. Przy użyciu pojęcia hello w tym artykule, możesz rozszerzyć uproszczona konfiguracja w dowolnym momencie.

Podczas definiowania modułu równoważenia obciążenia Azure frontonu i wewnętrznej bazy danych konfiguracji są połączone z zasadami. Hello sondy kondycji przywoływany przez regułę hello jest używany toodetermine nowych przepływów są wysyłane tooa węzła w puli zaplecza hello. frontonu Hello jest zdefiniowany przez wirtualnego adresu IP (VIP), czyli krotka 3 składającej się z adresu IP (wewnętrzny lub publiczny), protokół transportu (UDP lub TCP) i numer portu. Adres IP na Azure wirtualnej karty Sieciowej podłączony tooa maszyn wirtualnych w puli zaplecza hello jest DIP.

w poniższej tabeli Hello zawiera niektóre przykładowe konfiguracje serwera sieci Web:

| VIP | Adres IP | Protokół | port |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

Witaj tabeli przedstawiono cztery różne frontends. Frontends #1, #2 i #3 są pojedynczego wirtualnego adresu IP z wielu reguł. Witaj tego samego adresu IP jest używana, ale hello portu lub protokół jest różne dla każdego serwera sieci Web. Frontends #1 i #4 są przykładem wieloma wirtualnymi adresami IP, gdzie hello tego samego serwera sieci Web protokół i port są ponownie między wieloma wirtualnymi adresami IP.

Moduł równoważenia obciążenia Azure zapewnia elastyczność podczas definiowania reguł równoważenia obciążenia hello. Reguła deklaruje, jak adres i port na powitania serwera sieci Web jest mapowanych toohello docelowy adres i port hello wewnętrznej bazy danych. Określa, czy porty wewnętrznej bazy danych są ponownie przez zasady, zależy od typu hello hello reguły. Każdy typ reguły ma szczególne wymagania, które mogą mieć wpływ na projekt konfiguracji i badania hosta. Istnieją dwa typy zasad:

1. ponowne użycie Hello domyślną regułę z portem nie wewnętrznej bazy danych
2. Hello pływający adres IP reguły, gdzie są ponownie używane porty wewnętrznej bazy danych

Moduł równoważenia obciążenia Azure umożliwia toomix reguły oba typy hello tej samej konfiguracji usługi równoważenia obciążenia. Moduł równoważenia obciążenia Hello można używać ich równocześnie dla danej maszyny Wirtualnej lub dowolnej kombinacji pod warunkiem przestrzegania ograniczeń hello hello reguły. Typ reguły, który można wybrać, zależy od hello wymagań Twojej aplikacji i hello złożoności obsługi tej konfiguracji. Należy ocenić, jakie typy reguł są najlepsze w przypadku danego scenariusza.

Firma Microsoft Poznaj te dodatkowe scenariusze, zaczynając od hello domyślne zachowanie.

## <a name="rule-type-1-no-backend-port-reuse"></a>Typ #1 reguły: nie ponownemu portu zaplecza

![Ilustracja z wieloma wirtualnymi adresami IP](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

W tym scenariuszu frontonu hello wirtualne adresy IP są konfigurowane w następujący sposób:

| VIP | Adres IP | Protokół | port |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Witaj DIP jest hello docelowym hello ruchu przychodzącego przepływu. W puli zaplecza hello każda maszyna wirtualna przedstawia usługę hello żądanego na unikatowy portu na DIP. Ta usługa jest skojarzony z frontonu hello za pośrednictwem definicji reguły.

Definiujemy dwie reguły:

| Reguła | Mapa frontonu | toobackend puli |
| --- | --- | --- |
| 1 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![wewnętrznej bazy danych](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![wewnętrznej bazy danych](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![wewnętrznej bazy danych](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![wewnętrznej bazy danych](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

Mapowanie pełną Hello w usłudze równoważenia obciążenia Azure jest teraz w następujący sposób:

| Reguła | Adres VIP IP | Protokół | port | Element docelowy | port |
| --- | --- | --- | --- | --- | --- |
| ![Reguły](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |Adres IP DIP |80 |
| ![Reguły](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |Adres IP DIP |81 |

Każda reguła musi mieć przepływ z unikatowych kombinacji adresu IP i port docelowy. Przez zróżnicowanie port docelowy hello hello przepływu wiele reguł można dostarczać toohello przepływów tego samego DIP na różnych portów.

Sondy kondycji są zawsze ukierunkowanej toohello DIP maszyny wirtualnej. Należy zapewnić, że czy Twoje sondowania odzwierciedla hello kondycję hello maszyny Wirtualnej.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>Typ #2 reguły: ponowne użycie portu zaplecza przy użyciu pływającego adresu IP

Moduł równoważenia obciążenia Azure zapewnia elastyczność hello portu frontonu hello tooreuse między wieloma wirtualnymi adresami IP, niezależnie od typu reguły hello używane. Ponadto niektóre scenariusze aplikacji preferowane lub wymagają hello sam port używany przez wiele wystąpień aplikacji na jednej maszynie Wirtualnej w puli zaplecza hello toobe. Typowe przykłady ponownemu portu obejmują klastrowanie wysokiej dostępności, sieci wirtualnych urządzeń i udostępnia wiele TLS punktów końcowych bez ponownego szyfrowania.

Jeśli chcesz portu zaplecza hello tooreuse przez wiele reguł, należy włączyć pływającego adresu IP w definicji reguły hello.

Zmienny adres IP jest częścią co to jest znany jako bezpośrednie serwer zwraca DSR (). DSR składa się z dwóch części: Topologia przepływu i adresów IP schematu mapowania. Na poziomie platformy usługi równoważenia obciążenia Azure zawsze działa w topologii przepływu DSR niezależnie od tego, czy pływający adres IP jest włączone. Oznacza to, że hello część ruchu wychodzącego przepływu zawsze ma tooflow poprawnie ponownie zapisane bezpośrednio wstecz toohello pochodzenia.

Z typem reguły domyślne hello Azure udostępnia tradycyjne schemat mapowania adresów IP dla łatwość użycia z równoważeniem obciążenia. Włączanie pływający adres IP zmienia tooallow schemat mapowania adresów IP hello dodatkowe elastyczność jak wyjaśniono poniżej.

powitania po diagram przedstawia tej konfiguracji:

![Ilustracja z wieloma wirtualnymi adresami IP](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

W tym scenariuszu dla każdej maszyny Wirtualnej w puli zaplecza hello ma trzy interfejsów sieciowych:

* DIP: wirtualnej karty Sieciowej skojarzonych z hello maszyny Wirtualnej (Konfiguracja IP zasobów kart platformy Azure)
* Adres VIP1: interfejsu sprzężenia zwrotnego gościu systemu operacyjnego, który jest skonfigurowany z adresem IP adresu VIP1
* VIP2: interfejsu sprzężenia zwrotnego gościu systemu operacyjnego, który jest skonfigurowany z adresem IP VIP2

> [!IMPORTANT]
> Konfiguracja Hello interfejsów logicznej hello jest wykonywana w ramach system operacyjny gościa hello. Ta konfiguracja nie jest wykonywane lub zarządzane przez usługę Azure. Bez tej konfiguracji reguły hello nie będzie działać. Definicje sondy kondycji Użyj hello DIP hello maszyny Wirtualnej, a nie hello logicznych adresu VIP. W związku z tym usługi podać sondowania odpowiedzi na port DIP odzwierciedlenia stanu hello hello usług oferowanych w systemie hello logicznych adresu VIP.

Załóżmy, że hello tej samej konfiguracji serwera sieci Web, jak w poprzednim scenariuszu hello:

| VIP | Adres IP | Protokół | port |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Definiujemy dwie reguły:

| Reguła | Mapa frontonu | toobackend puli |
| --- | --- | --- |
| 1 |![Reguły](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![wewnętrznej bazy danych](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (w VM1 i maszyny VM2) |
| 2 |![Reguły](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![wewnętrznej bazy danych](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (w VM1 i maszyny VM2) |

Hello w poniższej tabeli przedstawiono pełną mapowania hello w hello usługi równoważenia obciążenia:

| Reguła | Adres VIP IP | Protokół | port | Element docelowy | port |
| --- | --- | --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |identyczny VIP (65.52.0.1) |identyczny VIP (80) |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |identyczny VIP (65.52.0.2) |identyczny VIP (80) |

docelowy Hello hello przepływu ruchu przychodzącego jest adresu hello VIP w interfejsie sprzężenia zwrotnego hello w hello maszyny Wirtualnej. Każda reguła musi mieć przepływ z unikatowych kombinacji adresu IP i port docelowy. Zróżnicowanie hello docelowy adres IP przepływu hello jest możliwe w ponownemu portu hello tej samej maszyny Wirtualnej. Usługa jest narażonych toohello modułu równoważenia obciążenia przez powiązanie jego adres IP i port interfejsu sprzężenia zwrotnego odpowiednich hello toohello VIP w.

Zwróć uwagę, w tym przykładzie nie zmienia hello port docelowy. Mimo że jest to scenariusz pływającego adresu IP, usługi równoważenia obciążenia Azure obsługuje również definiowanie port docelowy reguły toorewrite hello wewnętrznej bazy danych i toomake on inny niż port docelowy hello frontonu.

Hello typ reguły pływający adres IP jest foundation hello kilka wzorców konfiguracji usługi równoważenia obciążenia. Przykładem, która jest obecnie dostępna jest hello [funkcji SQL AlwaysOn z wiele odbiorników](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) konfiguracji. Wraz z upływem czasu firma Microsoft będzie dokumentu jeden z tych scenariuszy.

## <a name="limitations"></a>Ograniczenia

* Wielu konfiguracji adresów VIP są obsługiwane tylko z maszyn wirtualnych IaaS.
* Witaj pływający adres IP reguły aplikacji musi być hello DIP przepływów wychodzących. Aplikacji wiąże adres VIP toohello skonfigurowane dla interfejsu sprzężenia zwrotnego hello w system operacyjny gościa hello, następnie SNAT nie jest dostępne toorewrite hello wychodzącego przepływu i hello przepływu nie powiodło się.
* Publiczne adresy IP mają wpływ na rozliczenia. Aby uzyskać więcej informacji, zobacz [cennik adresu IP](https://azure.microsoft.com/pricing/details/ip-addresses/)
* Zastosuj limity subskrypcji. Aby uzyskać więcej informacji, zobacz [usługi limity](../azure-subscription-service-limits.md#networking-limits) szczegółowe informacje.
