---
title: aaaAzure sieci infrastruktury wytyczne - systemu Linux | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello klucza projekt i implementację wskazówki dotyczące wdrażania sieci wirtualne w usług infrastruktury platformy Azure."
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
ms.openlocfilehash: f3f49b135b1f9bca3fd463e9ff27299fb97908c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a>Azure networking wskazówki dotyczące infrastruktury dla maszyn wirtualnych systemu Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Ten artykuł skupia się na powitania opis wymaganych czynności dla sieci wirtualnych w obrębie platformy Azure i łączności między istniejących środowiskach lokalnych związane z planowaniem.

## <a name="implementation-guidelines-for-virtual-networks"></a>Implementacja — wskazówki dla sieci wirtualnych
Decyzje:

* Jaki typ sieci wirtualnej potrzebujesz toohost infrastruktury i obciążenia IT (tylko w chmurze lub między lokalizacjami)?
* Dla sieci wirtualnych między lokalizacjami, ile adresów miejsca potrzebujesz toohost hello podsieci i maszyn wirtualnych teraz i uzasadnione rozszerzenia w hello przyszłych?
* Czy mimo to toocreate scentralizowane sieci wirtualnych i utworzyć poszczególnymi sieciami wirtualnymi dla każdej grupy zasobów?

Zadania:

* Zdefiniuj przestrzeń adresowa hello hello toobe sieci wirtualne utworzone.
* Definiowanie hello zestawów podsieci i przestrzeń adresową powitania dla każdego.
* Dla sieci wirtualnej między lokalizacjami należy zdefiniować zestaw hello obszarów adresów sieci lokalnej dla lokalizacji lokalne powitania, które hello maszyn wirtualnych w tooreach potrzeby sieci wirtualnej hello.
* Praca z lokalnej sieci zespołu tooensure hello odpowiedniego routingu skonfigurowano podczas tworzenia między lokalizacjami sieci wirtualnych.
* Tworzenie sieci wirtualnych hello przy użyciu Konwencja nazewnictwa.

## <a name="virtual-networks"></a>Sieci wirtualne
Sieci wirtualne są niezbędne toosupport komunikacji między maszynach wirtualnych (VM). Można zdefiniować podsieci, Niestandardowy adres IP, ustawienia DNS, filtrowania zabezpieczeń i równoważenie obciążenia, tak jak w przypadku sieci fizycznej. Za pomocą [bramy sieci VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) lub [obwodzie usługi Express Route](../../expressroute/expressroute-introduction.md), istnieje możliwość połączenia sieci lokalnej tooyour sieci wirtualnych platformy Azure. Możesz przeczytać dodatkowe informacje [sieci wirtualnych i ich elementy](../../virtual-network/virtual-networks-overview.md).

Za pomocą grup zasobów, masz elastyczność w sposób projektowania składniki wirtualnej sieci. Maszyny wirtualne można połączyć sieci toovirtual poza własne grupy zasobów. Typowym podejściem projekt będzie toocreate scentralizowane grupy zasobów, które zawierają infrastruktury sieci podstawowej mogą być zarządzane przez zespół wspólnej. Maszyny wirtualne i ich aplikacje wdrażane tooseparate grup zasobów. Takie podejście umożliwia właściciele aplikacji dostępu toohello grupę zasobów, która zawiera ich maszyn wirtualnych bez konieczności otwierania konfigurację toohello dostępu hello szerszej wirtualnych sieci zasobów.

## <a name="site-connectivity"></a>Połączenie lokacji
### <a name="cloud-only-virtual-networks"></a>Sieci wirtualne tylko w chmurze
Jeśli lokalnych użytkowników i komputerów nie wymagają tooVMs trwającą łączność w sieci wirtualnej platformy Azure, projekt sieci wirtualnej jest wprost do przodu:

![Diagram podstawowego tylko w chmurze sieci wirtualnej](./media/infrastructure-networking-guidelines/vnet01.png)

Ta metoda jest zwykle dla obciążeń skierowane do Internetu, na przykład internetowy serwer sieci web. Możesz zarządzać tych maszyn wirtualnych przy użyciu protokołu SSH i połączeń sieci VPN punkt lokacja.

Ponieważ nie podłączaj tooyour sieci lokalnej, tylko Azure sieci wirtualne mogą używać jakiejkolwiek jego części hello prywatnych przestrzeni adresów IP. przestrzeń adresowa Hello może być hello tą samą przestrzenią prywatny, który znajduje się w pomocą lokalnymi.

### <a name="cross-premises-virtual-networks"></a>Między różnymi lokalizacjami, sieci wirtualnych
Jeśli lokalnych użytkowników i komputery wymagają tooVMs trwającą łączność w sieci wirtualnej platformy Azure, należy utworzyć sieć wirtualną między lokalizacjami. Uzyskuj dostęp do sieci lokalnej tooyour sieci wirtualnej hello ExpressRoute lub połączeń sieci VPN lokacja lokacja.

![Diagram sieci wirtualnej między lokalizacjami](./media/infrastructure-networking-guidelines/vnet02.png)

W tej konfiguracji hello sieci wirtualnej platformy Azure to zasadniczo oparte na chmurze rozszerzenie sieci lokalnej.

Ponieważ łączą tooyour lokalnej sieci, między różnymi lokalizacjami, sieci wirtualnych należy użyć część przestrzeni adresowej hello używane przez Twoją organizację, która jest unikatowa. W hello sam sposób tego różnych lokalizacjach w firmie są przypisane określonej podsieci IP, Azure staje się inną lokalizację, jak rozszerzyć limit sieci.

tooallow tootravel pakietów z sieci lokalnej tooyour sieci wirtualnej między lokalizacjami, należy skonfigurować zestaw hello prefiksy adresów lokalnych odpowiednich jako część definicji sieci lokalnej hello hello sieci wirtualnej. W zależności od adresu hello miejsca hello wirtualnych sieci i hello zestaw odpowiednich lokalnej lokalizacji, może istnieć wiele prefiksów adresów w sieci lokalnej hello.

Możesz przekształcić sieci wirtualnej między lokalizacjami tooa tylko w chmurze sieci wirtualnej, ale najprawdopodobniej wymaga toore IP przestrzeń adresową sieci wirtualnej, a zasobów platformy Azure. W związku z tym należy rozważyć, czy wymaga sieci wirtualnej sieci lokalnej podłączonej tooyour toobe podczas przypisywania podsieci IP.

## <a name="subnets"></a>Podsieci
Podsieci pozwalają tooorganize zasobów, które są powiązane, albo logicznie (na przykład podsieci dla maszyn wirtualnych skojarzone toohello tej samej aplikacji), lub fizycznie (na przykład w jednej podsieci dla grupy zasobów). Możesz również użyć techniki izolacji podsieci, aby zwiększyć bezpieczeństwo.

Dla sieci wirtualnej między lokalizacjami, zalecane jest zaprojektowanie podsieci z hello tej samej Konwencji, których używasz do zasobów lokalnych. **Azure zawsze używa hello pierwszych trzech adresów IP hello przestrzeni adresowej dla każdej podsieci**. numer hello toodetermine adresów potrzebne dla podsieci hello, Rozpocznij od zliczania hello liczbę maszyn wirtualnych, które należy teraz. Szacowanie przyszły wzrost, a następnie użyj powitania od rozmiaru hello toodetermine tabeli hello podsieci.

| Liczba maszyn wirtualnych potrzebnych | Liczba bitów hosta potrzebne | Rozmiar podsieci hello |
| --- | --- | --- |
| 1–3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> Dla podsieci lokalnej normalne hello maksymalną liczbę adresów hosta dla podsieci z bitami n hosta jest 2<sup> n </sup> — 2. Dla podsieci platformy Azure, hello maksymalna liczba adresów hosta dla podsieci z bitami n hosta wynosi 2<sup> n </sup> – 5 (2 i 3 adresów hello Azure używa w każdej podsieci).
> 
> 

Jeśli wybierzesz podsieci o rozmiarze, który jest za mały, mają toore IP i ponownie wdrożyć maszyn wirtualnych hello w podsieci hello.

## <a name="network-security-groups"></a>Grupy zabezpieczeń sieci
Można zastosować filtrowanie ruchu toohello reguły przepływającego za pośrednictwem sieci wirtualne przy użyciu grup zabezpieczeń sieci. Można utworzyć szczegółowego toosecure reguły filtrowania wirtualnego środowiska sieciowego, kontrolowanie ruchu przychodzącego i wychodzącego ruchu sieciowego, źródłowy i docelowy zakresy IP, dozwolone portów itp. Grupy zabezpieczeń sieci może być toosubnets zastosowane w ramach sieci wirtualnej lub bezpośrednio tooa danego interfejsu sieci wirtualnej. Jest zalecana toohave pewnego poziomu sieciowej grupy zabezpieczeń, filtrowanie ruchu w sieci wirtualnej. Możesz przeczytać dodatkowe informacje [grup zabezpieczeń sieci](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Dodatkowe składniki sieciowe
Podobnie jak w przypadku fizycznej infrastruktury sieci lokalnej, sieci wirtualne platformy Azure może zawierać więcej niż tylko podsieci i adresów IP. Podczas projektowania infrastruktury aplikacji, może być tooincorporate niektóre z tych dodatkowych składników:

* [Bramy sieci VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) -połączyć sieci wirtualnych platformy Azure tooother wirtualnej Azure sieci lub połączyć sieci lokalnej tooon za pośrednictwem połączenia sieci VPN typu lokacja-lokacja. Implementowanie połączeń Expressroute w wersji dedykowanej, bezpiecznych połączeń. Może także udostępnić użytkownikom bezpośredni dostęp do połączeń sieci VPN typu punkt-lokacja.
* [Moduł równoważenia obciążenia](../../load-balancer/load-balancer-overview.md) — udostępnia równoważenie obciążenia ruchu dla wewnętrznych i zewnętrznych ruchu zgodnie z potrzebami.
* [Brama aplikacji w](../../application-gateway/application-gateway-introduction.md) — HTTP równoważenia obciążenia w warstwie aplikacji hello, zapewniając niektóre dodatkowe korzyści dla aplikacji sieci web zamiast wdrażania usługi równoważenia obciążenia Azure hello.
* [Menedżer ruchu](../../traffic-manager/traffic-manager-overview.md) — oparte na DNS ruchu dystrybucji toodirect użytkownicy końcowi toohello najbliższy dostępny punkt końcowy aplikacji, dzięki czemu możesz toohost aplikacji poza centrach danych platformy Azure w różnych regionach.

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

