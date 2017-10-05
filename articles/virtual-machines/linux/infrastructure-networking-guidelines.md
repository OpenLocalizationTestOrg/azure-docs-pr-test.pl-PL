---
title: Azure networking wytyczne infrastruktury - systemu Linux | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat klucza projekt i implementację wskazówki dotyczące wdrażania sieci wirtualne w usług infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7ebd5da-3c62-45e8-ad90-6c73a37ebeb1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 13e041956c05bec522c83587f8a7f99ac1ceb510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a>Azure networking wskazówki dotyczące infrastruktury dla maszyn wirtualnych systemu Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na wymagane kroki planowania dla sieci wirtualnych w obrębie platformy Azure i łączności między istniejącego środowiska lokalnego.

## <a name="implementation-guidelines-for-virtual-networks"></a>Implementacja — wskazówki dla sieci wirtualnych
Decyzje:

* Jakiego rodzaju sieci wirtualnej jest potrzebne do obsługi infrastruktury i obciążenia IT (tylko w chmurze lub między lokalizacjami)?
* Dla sieci wirtualnej między lokalizacjami ile przestrzeni adresowej potrzebujesz do hostowania podsieci i maszyn wirtualnych, teraz i w przyszłości uzasadnione rozszerzenia?
* Zamierzasz utworzyć scentralizowane sieci wirtualnych lub poszczególnymi sieciami wirtualnymi dla każdej grupy zasobów?

Zadania:

* Zdefiniuj przestrzeni adresowej dla sieci wirtualnych, które ma zostać utworzony.
* Zdefiniuj zbiór dla każdej podsieci oraz przestrzenie adresów.
* Dla sieci wirtualnej między lokalizacjami Zdefiniuj zestaw obszarów adresów sieci lokalnej dla lokalizacji lokalnej, które maszyn wirtualnych w sieci wirtualnej muszą nawiązać połączenie.
* Praca z lokalnej sieci zespołu w celu zapewnienia odpowiedniego routingu jest konfigurowany podczas tworzenia między lokalizacjami sieci wirtualnych.
* Tworzenie sieci wirtualnej, zgodnie z konwencją nazewnictwa.

## <a name="virtual-networks"></a>Sieci wirtualne
Sieci wirtualne są niezbędne do obsługi komunikacji między maszynach wirtualnych (VM). Można zdefiniować podsieci, Niestandardowy adres IP, ustawienia DNS, filtrowania zabezpieczeń i równoważenie obciążenia, tak jak w przypadku sieci fizycznej. Za pomocą [bramy sieci VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) lub [obwodzie usługi Express Route](../../expressroute/expressroute-introduction.md), możesz nawiązać połączenie sieci wirtualnych platformy Azure w sieci lokalnej. Możesz przeczytać dodatkowe informacje [sieci wirtualnych i ich elementy](../../virtual-network/virtual-networks-overview.md).

Za pomocą grup zasobów, masz elastyczność w sposób projektowania składniki wirtualnej sieci. Maszyny wirtualne mogą łączyć się sieci wirtualnych poza własne grupy zasobów. Typowym podejściem projekt będzie można utworzyć grupy zasobów scentralizowane, które zawierają infrastruktury sieci podstawowej mogą być zarządzane przez zespół wspólnej. Maszyny wirtualne i ich aplikacje wdrożone na oddzielnych grup zasobów. Takie podejście umożliwia dostęp do właścicieli aplikacji do grupy zasobów, zawierającą ich maszyn wirtualnych bez konieczności otwierania dostępu do konfiguracji szerszej wirtualnego zasobów sieciowych.

## <a name="site-connectivity"></a>Połączenie lokacji
### <a name="cloud-only-virtual-networks"></a>Sieci wirtualne tylko w chmurze
Jeśli lokalnych użytkowników i komputerów nie wymagają trwającą łączności maszyn wirtualnych w sieci wirtualnej platformy Azure, projekt sieci wirtualnej jest wprost do przodu:

![Diagram podstawowego tylko w chmurze sieci wirtualnej](./media/infrastructure-networking-guidelines/vnet01.png)

Ta metoda jest zwykle dla obciążeń skierowane do Internetu, na przykład internetowy serwer sieci web. Możesz zarządzać tych maszyn wirtualnych przy użyciu protokołu SSH i połączeń sieci VPN punkt lokacja.

Ponieważ należy nawiązywać połączenia z siecią lokalną, tylko Azure sieci wirtualne mogą używać jakiejkolwiek części w prywatnej przestrzeni adresów IP. Przestrzeń adresowa może być tą samą przestrzenią prywatny, który jest używany w lokalnym programie.

### <a name="cross-premises-virtual-networks"></a>Między różnymi lokalizacjami, sieci wirtualnych
Jeśli lokalnych użytkowników i komputery wymagają trwającą łączności maszyn wirtualnych w sieci wirtualnej platformy Azure, należy utworzyć sieć wirtualną między lokalizacjami. Połączyć sieć wirtualną do sieci lokalnej za pomocą programu ExpressRoute lub połączeń sieci VPN lokacja lokacja.

![Diagram sieci wirtualnej między lokalizacjami](./media/infrastructure-networking-guidelines/vnet02.png)

W tej konfiguracji sieci wirtualnej platformy Azure to zasadniczo oparte na chmurze rozszerzenie sieci lokalnej.

Ponieważ łączą się z sieci lokalnej, między różnymi lokalizacjami, sieci wirtualnych należy użyć część przestrzeni adresowej używane przez Twoją organizację, która jest unikatowa. W taki sam sposób jak różnych lokalizacjach w firmie są przypisane do określonej podsieci IP Azure staje się innej lokalizacji poszerzają limit sieci.

Aby zezwalać na pakiety na komunikację z sieci wirtualnej między lokalizacjami do sieci lokalnej, należy skonfigurować zestaw prefiksy adresów lokalnych odpowiednich jako część definicji sieci lokalnej dla sieci wirtualnej. W zależności od przestrzeni adresowej sieci wirtualnej i zestaw lokalizacji lokalnej istotne może istnieć wiele prefiksów adresów w sieci lokalnej.

Tylko w chmurze sieci wirtualnej można przekonwertować na sieć wirtualną między lokalizacjami, ale prawdopodobnie wymaga adresowi IP ponowna przestrzeń adresową sieci wirtualnej, a zasobów platformy Azure. W związku z tym należy rozważyć, jeśli sieć wirtualna musi być podłączony do sieci lokalnej, podczas przypisywania podsieci IP.

## <a name="subnets"></a>Podsieci
Podsieci umożliwiają organizowania zasobów, które są powiązane, albo logicznie (na przykład podsieci dla maszyn wirtualnych skojarzonego z tej samej aplikacji), lub fizycznie (na przykład w jednej podsieci dla grupy zasobów). Możesz również użyć techniki izolacji podsieci, aby zwiększyć bezpieczeństwo.

Dla sieci wirtualnej między lokalizacjami zalecane jest zaprojektowanie podsieci z tej samej Konwencji, których używasz do zasobów lokalnych. **Azure zawsze używa pierwszych trzech adresów IP w przestrzeni adresowej dla każdej podsieci**. Aby określić liczbę potrzebnych dla podsieci adresów, Rozpocznij od liczby maszyn wirtualnych, które należy teraz. Szacowana rozwój w przyszłości, a następnie skorzystaj z poniższej tabeli, aby określić rozmiar podsieci.

| Liczba maszyn wirtualnych potrzebnych | Liczba bitów hosta potrzebne | Rozmiar podsieci |
| --- | --- | --- |
| 1–3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> Dla podsieci lokalnej normalne, maksymalna liczba adresów hosta dla podsieci z bitami n hosta jest 2<sup> n </sup> — 2. Dla podsieci platformy Azure, maksymalna liczba adresów hosta dla podsieci z bitami n hosta wynosi 2<sup> n </sup> – 5 (2 i 3 dla adresów używanych w każdej podsieci platformy Azure).
> 
> 

Jeśli wybierzesz podsieci o rozmiarze, który jest za mały, trzeba ponownie IP i ponownie wdrożyć maszyn wirtualnych w podsieci.

## <a name="network-security-groups"></a>Grupy zabezpieczeń sieci
Reguły filtrowania można stosować do ruchu przepływającego za pośrednictwem sieci wirtualne przy użyciu grup zabezpieczeń sieci. Szczegółowe reguły filtrowania zabezpieczające wirtualnego środowiska sieciowego, można tworzyć kontrolowanie ruchu przychodzącego i wychodzącego ruchu sieciowego, źródłowy i docelowy zakresy IP, dozwolone portów itp. Grupy zabezpieczeń sieci może odnosić się do podsieci sieci wirtualnej lub bezpośrednio do interfejsu danej sieci wirtualnej. Zalecane jest ma pewnego poziomu sieciowej grupy zabezpieczeń, filtrowanie ruchu w sieci wirtualnej. Możesz przeczytać dodatkowe informacje [grup zabezpieczeń sieci](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Dodatkowe składniki sieciowe
Podobnie jak w przypadku fizycznej infrastruktury sieci lokalnej, sieci wirtualne platformy Azure może zawierać więcej niż tylko podsieci i adresów IP. Podczas projektowania infrastruktury aplikacji, może zajść potrzeba niektóre z tych dodatkowych składników:

* [Bramy sieci VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) — łączenie sieci wirtualnych platformy Azure innych sieci wirtualnych platformy Azure lub łączenie się z sieciami lokalnymi za pośrednictwem połączenia sieci VPN typu lokacja-lokacja. Implementowanie połączeń Expressroute w wersji dedykowanej, bezpiecznych połączeń. Może także udostępnić użytkownikom bezpośredni dostęp do połączeń sieci VPN typu punkt-lokacja.
* [Moduł równoważenia obciążenia](../../load-balancer/load-balancer-overview.md) — udostępnia równoważenie obciążenia ruchu dla wewnętrznych i zewnętrznych ruchu zgodnie z potrzebami.
* [Brama aplikacji w](../../application-gateway/application-gateway-introduction.md) — HTTP równoważenia obciążenia w warstwie aplikacji, zapewniając niektóre dodatkowe korzyści dla aplikacji sieci web zamiast wdrażania usługi równoważenia obciążenia Azure.
* [Menedżer ruchu](../../traffic-manager/traffic-manager-overview.md) — oparte na DNS ruchu dystrybucji użytkownikom bezpośrednie do najbliższego punktu końcowego dostępnych aplikacji, co pozwoli na potrzeby hostowania aplikacji poza centrach danych platformy Azure w różnych regionach.

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

