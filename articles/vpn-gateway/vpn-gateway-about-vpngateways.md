---
title: "Omówienie bramy sieci VPN: Tworzenie połączeń sieci VPN między lokalizacjami, sieci wirtualnych tooAzure | Dokumentacja firmy Microsoft"
description: "To omówienie bramy sieci VPN wyjaśniono hello sposoby tooconnect tooAzure sieci wirtualnych za pośrednictwem Internetu hello połączenie sieci VPN. Omówienie zawiera diagramy podstawowych konfiguracji połączeń."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>VPN Gateway — informacje

Brama sieci VPN jest typu bramy sieci wirtualnej, która wysyła szyfrowanego ruchu sieciowego między tooan publicznego połączenia lokalizacji lokalnej. Umożliwia także ruchu toosend szyfrowane bram sieci VPN między sieciami wirtualnymi platformy Azure w sieci Microsoft hello. toosend zaszyfrowany ruch sieciowy między sieci wirtualnej platformy Azure i witryny lokalnej, należy utworzyć bramę sieci VPN dla sieci wirtualnej.

Każdej sieci wirtualnej może mieć tylko jedną bramę sieci VPN, jednak można utworzyć wiele połączeń toohello tej samej bramy sieci VPN. Przykładem może być konfiguracja połączenia obejmującego wiele lokacji. Podczas tworzenia wielu połączeń toohello tej samej bramy sieci VPN, wszystkie tuneli VPN, w tym sieci VPN typu punkt-lokacja, udziału hello przepustowość dostępną dla hello bramy.

### <a name="whatis"></a>Co to jest brama sieci wirtualnej?

Brama sieci wirtualnej składa się z dwóch lub więcej maszyn wirtualnych, które są wdrożone tooa określonej podsieci o nazwie hello GatewaySubnet. maszyny wirtualne, które znajdują się w hello GatewaySubnet są tworzone po utworzeniu bramy sieci wirtualnej hello Hello. Bramy sieci wirtualnej maszyny wirtualne są skonfigurowane toocontain tabele routingu i bramy toohello określonych usług bramy. Nie można bezpośrednio skonfigurować hello maszyn wirtualnych, które są częścią hello bramy sieci wirtualnej i nigdy nie należy wdrożyć dodatkowe zasoby toohello GatewaySubnet.

Po utworzeniu bramy sieci wirtualnej przy użyciu typu bramy hello "Vpn" tworzy dla określonego typu bramy sieci wirtualnej, który szyfruje ruch; Brama sieci VPN. Brama sieci VPN może potrwać too45 toocreate minut. Ponieważ hello maszyn wirtualnych dla bramy sieci VPN hello są wdrożone toohello GatewaySubnet i skonfigurowano ustawienia hello, określone przez użytkownika. Hello jednostka SKU bramy, który można wybrać Określa, jak zaawansowanych hello są maszyny wirtualne.

## <a name="gwsku"></a>Jednostki SKU bramy

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>Konfigurowanie bramy VPN Gateway

Połączenie bramy sieci VPN bazuje na wielu zasobach konfigurowanych przy użyciu konkretnych ustawień. Większość hello zasobów można skonfigurować osobno, mimo że musi być skonfigurowany w określonej kolejności w niektórych przypadkach.

### <a name="settings"></a>Ustawienia

wybrane dla każdego zasobu ustawienia Hello są krytyczne toocreating udane połączenie. Aby uzyskać informacje na temat poszczególnych zasobów i ustawień dla bramy sieci VPN, zobacz [Ustawienia bramy sieci VPN — informacje](vpn-gateway-about-vpn-gateway-settings.md). Artykuł Hello zawiera zrozumieć typy bramy, typy sieci VPN, typów połączeń, podsieci bramy, bramy sieci lokalnej i różnych innych ustawień zasobu można tooconsider toohelp informacji.

### <a name="tools"></a>Narzędzia wdrażania

Możesz rozpocząć tworzenie i konfigurowanie zasobów za pomocą jednego narzędzia konfiguracji, takich jak hello portalu Azure. Później można zdecydować, tooswitch tooanother narzędzia, takie jak środowiska PowerShell, tooconfigure dodatkowe zasoby, lub modyfikowania istniejących zasobów, w razie potrzeby. Obecnie nie można skonfigurować dla każdego zasobu i ustawienie zasobów w hello portalu Azure. instrukcje Hello w artykułach hello topologia każdego połączenia określać, gdy potrzebny jest narzędziem do określonej konfiguracji. 

### <a name="models"></a>Model wdrażania

Podczas konfigurowania bramy sieci VPN, hello czynności, które możesz wykonać zależą od modelu wdrażania hello używane toocreate sieci wirtualnej. Na przykład jeśli utworzono sieci wirtualnej przy użyciu hello klasycznego modelu wdrażania, użyj wytycznych hello i instrukcje dotyczące wdrażania klasycznego hello modelu toocreate i skonfigurować ustawienia bramy sieci VPN. Aby uzyskać więcej informacji na temat modeli wdrażania, zobacz [Omówienie modelu wdrażania przy użyciu usługi Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="diagrams"></a>Diagramy topologii połączeń

Jest ważne tooknow dostępne dla połączenia bramy sieci VPN są różne konfiguracje. Należy toodetermine konfigurację, która najlepiej odpowiada potrzebom użytkownika. W poniższych sekcjach hello, można wyświetlić diagramy topologii i informacje o hello następujące połączenia bramy sieci VPN: hello następujące sekcje zawierają tabel, których listy:

* Dostępny model wdrażania
* Dostępne narzędzia konfiguracji
* Linki prowadzące bezpośrednio tooan artykułu, jeśli jest dostępna

Użyj hello diagramy i opisy toohelp wybierz hello połączenia topologii toomatch wymagań. Witaj diagramach hello topologie głównych linii bazowej, ale jest możliwe toobuild bardziej złożonych konfiguracji przy użyciu diagramów hello jako wskazówki.

## <a name="s2smulti"></a>Połączenia typu lokacja-lokacja i połączenia obejmujące wiele lokacji (tunel VPN protokołu IPsec/IKE)

### <a name="S2S"></a>Lokacja-lokacja

Połączenie bramy sieci VPN typu lokacja-lokacja to połączenie nawiązywane za pośrednictwem tunelu sieci VPN wykorzystującego protokół IPsec/IKE (IKEv1 lub IKEv2). Połączenia S2S wymaga sieci VPN urządzeń znajdujących się lokalnie ma publiczny tooit przypisany adres IP, które nie znajduje się za urządzeniem NAT Z połączeń typu lokacja-lokacja (S2S) można korzystać w ramach konfiguracji hybrydowych i obejmujących wiele lokalizacji.   

![Przykład połączenia typu lokacja-lokacja w usłudze Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Wiele witryn

Ten typ połączenia jest odmianą hello połączenie lokacja-lokacja. Tworzenie więcej niż jednego połączenia sieci VPN z bramy sieci wirtualnej, zwykle połączenie toomultiple lokacjami lokalnymi. Podczas pracy z wieloma połączeniami musisz użyć sieci VPN typu RouteBased (nazywanego dynamiczną bramą w przypadku pracy z klasycznymi sieciami wirtualnymi). Ponieważ każdej sieci wirtualnej może mieć tylko jedną bramę sieci VPN, wszystkie połączenia za pośrednictwem bramy hello udostępnianie hello dostępną przepustowość. Ten typ konfiguracji jest często określany mianem połączenia „obejmującego wiele lokacji”.

![Przykład połączenia obejmującego wiele lokacji w usłudze Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Modele wdrażania i metody nawiązywania połączeń typu lokacja-lokacja i połączeń obejmujących wiele lokacji

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Punkt-lokacja (sieć VPN za pośrednictwem protokołu SSTP)

Brama sieci VPN typu punkt-lokacja (P2S) umożliwia tworzenie sieci wirtualnej tooyour bezpiecznego połączenia z pojedynczym komputerem klienckim. Połączenia sieci VPN punkt-lokacja są przydatne, gdy chcesz tooyour tooconnect sieci wirtualnej z lokalizacji zdalnej, takie, gdy są Niezale¿nie z domu lub konferencji. P2S sieci VPN jest również toouse przydatne rozwiązanie, zamiast VPN lokacja-lokacja, jeśli istnieje tylko kilka klientów, którzy potrzebują tooa tooconnect sieci wirtualnej. 

W przeciwieństwie do połączeń S2S połączenia P2S nie wymagają lokalnego, publicznego adresu IP ani urządzenia sieci VPN. Połączeń P2S może być używany z połączeń S2S za pośrednictwem hello tej samej bramy sieci VPN, dopóki wszystkie wymagania dotyczące konfiguracji Witaj dla obu połączenia są niezgodne.

Używa P2S hello gniazda Tunelowanie protokołu SSTP (Secure), która jest oparta na protokole SSL protokołu sieci VPN. Uruchamiając go z komputera klienckiego hello jest nawiązywane połączenie sieci VPN P2S.

![Przykład połączenia typu punkt-lokacja w usłudze Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>Modele wdrażania i metody nawiązywania połączeń typu punkt-lokacja

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>Połączenia między sieciami wirtualnymi (tunel VPN protokołu IPsec/IKE)

Połączenie wirtualnej sieci tooanother sieć wirtualną (VNet-VNet) jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji. Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu. Można także łączyć połączenia między sieciami wirtualnymi z konfiguracjami połączeń obejmujących wiele lokacji. Pozwala to tworzyć topologie sieci, które łączą wdrożenia obejmujące wiele lokalizacji z połączeniami między sieciami wirtualnymi.

można Hello łączenia sieci wirtualnych:

* w hello tych samych lub różnych regionów
* w hello tych samych lub różnych subskrypcji. 
* w hello modele wdrażania tego samego lub innego

![Przykład połączenia tooVNet w usłudze Azure bramy sieci VPN w sieci wirtualnej](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>Połączenia między modelami wdrażania

Platforma Azure ma obecnie dwa modele wdrażania: klasyczny model wdrażania oraz model wdrażania przy użyciu usługi Resource Manager. Jeśli korzystasz z platformy Azure od pewnego czasu, prawdopodobnie masz maszyny wirtualne i wystąpienia roli platformy Azure działające w klasycznej sieci wirtualnej. Nowsze maszyny wirtualne i wystąpienia roli mogą działać w sieci wirtualnej utworzonej w usłudze Resource Manager. Połączenie między hello tooallow sieci wirtualnych można utworzyć zasoby hello w jednej sieci wirtualnej toocommunicate bezpośrednio z zasobami w innym.

### <a name="vnet-peering"></a>Komunikacja równorzędna sieci wirtualnych

Możliwe toouse wirtualne sieci równorzędne — toocreate połączenie, może być tak długo, jak sieci wirtualnej spełnia określone wymagania. W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci wirtualnej. Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Modele wdrażania i metody nawiązywania połączeń między sieciami wirtualnymi

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (dedykowane połączenie prywatne)

Microsoft Azure ExpressRoute pozwala rozszerzyć sieci lokalnej na powitania firmy Microsoft w chmurze za pośrednictwem dedykowanego połączenia prywatne w ramach dostawcy łączności. Z usługi ExpressRoute można ustanowić połączenia usług chmury tooMicrosoft, takich jak Microsoft Azure, Office 365 i CRM Online. Połączenie może być z sieci typu dowolna-dowolna (IP VPN), sieci Ethernet typu punkt-punkt lub przy użyciu łączności obejmującej wiele połączeń wirtualnych przez dostawcę połączenia w ramach infrastruktury współlokacji.

Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet. Dzięki toooffer połączeń ExpressRoute więcej niezawodności, szybkości szybsze niższe opóźnienia i lepsze zabezpieczenia niż typowe połączenia za pośrednictwem Internetu hello.

Połączenie usługi ExpressRoute nie używa bramy sieci VPN, mimo że używa bramy sieci wirtualnej w ramach wymaganej konfiguracji. Połączenia ExpressRoute Brama sieci wirtualnej hello skonfigurowano typu bramy hello "ExpressRoute" zamiast "Vpn". Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [opis techniczny ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="coexisting"></a>Współistniejące połączenia typu lokacja-lokacja i ExpressRoute

ExpressRoute jest bezpośrednie, dedykowane połączenie z sieci WAN (nie w hello publicznego Internetu) tooMicrosoft usług, w tym na platformie Azure. Lokacja-lokacja sieci VPN ruchu przemieszcza się zaszyfrowana za pośrednictwem hello publicznej sieci Internet. Trwa tooconfigure stanie połączeń VPN lokacja-lokacja i ExpressRoute hello tej samej sieci wirtualnej ma kilka zalet.

Można skonfigurować sieci VPN lokacja-lokacja jako ścieżka bezpiecznego pracy awaryjnej dla usługi ExpressRoute, lub użyj toosites tooconnect sieci VPN typu lokacja-lokacja, które nie są częścią sieci, ale które są połączone za pośrednictwem usługi ExpressRoute. Należy zauważyć, że ta konfiguracja wymaga dwóch bram sieci wirtualnej dla hello tej samej sieci wirtualnej, przy użyciu typu bramy sieci VPN "typu" hello i innych przy użyciu typu bramy hello "ExpressRoute" hello.

![Przykład współistniejących połączeń usług ExpressRoute i VPN Gateway](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>Modele wdrażania i metody nawiązywania połączeń typu lokacja-lokacja i połączeń usługi ExpressRoute

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Cennik

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

Więcej informacji o jednostkach SKU bramy dla usługi VPN Gateway zawiera artykuł [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy).

## <a name="faq"></a>Często zadawane pytania

Często zadawane pytania na temat bramy sieci VPN, zobacz hello [bramy sieci VPN — często zadawane pytania](vpn-gateway-vpn-faq.md).

## <a name="next-steps"></a>Następne kroki

- Planowanie konfiguracji bramy sieci VPN. Zobacz [Planowanie i projektowanie usługi VPN Gateway](vpn-gateway-plan-design.md).
- Widok hello [bramy sieci VPN — często zadawane pytania](vpn-gateway-vpn-faq.md) Aby uzyskać dodatkowe informacje.
- Widok hello [subskrypcji i ograniczenia usługi](../azure-subscription-service-limits.md#networking-limits).
- Dowiedz się więcej o niektórych hello innego klucza [możliwości w zakresie obsługi](../networking/networking-overview.md) platformy Azure.
