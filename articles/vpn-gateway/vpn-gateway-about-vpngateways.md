---
title: "Usługa VPN Gateway — omówienie: Tworzenie połączeń VPN obejmujących wiele lokalizacji z sieciami wirtualnymi platformy Azure | Microsoft Docs"
description: "W omówieniu usługi VPN Gateway wyjaśniono sposoby nawiązywania połączenia z sieciami wirtualnymi platformy Azure przez Internet przy użyciu połączenia VPN. Omówienie zawiera diagramy podstawowych konfiguracji połączeń."
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
ms.date: 12/04/2017
ms.author: cherylmc
ms.openlocfilehash: ae8de17c6b2ca8e1b9888612221c7f39b629c1b1
ms.sourcegitcommit: 7136d06474dd20bb8ef6a821c8d7e31edf3a2820
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2017
---
# <a name="about-vpn-gateway"></a>VPN Gateway — informacje

Brama sieci VPN jest typem bramy sieci wirtualnej, który wysyła zaszyfrowany ruch sieciowy przez połączenie publiczne do lokalizacji lokalnej. Za pomocą bram sieci VPN można także wysyłać zaszyfrowany ruch sieciowy między sieciami wirtualnymi platformy Azure przez sieć firmy Microsoft. Aby wysyłać zaszyfrowany ruch sieciowy między siecią wirtualną platformy Azure i lokacją lokalną, musisz utworzyć bramę sieci VPN dla sieci wirtualnej.

Każda sieć wirtualna może mieć tylko jedną bramę sieci VPN, jednak można tworzyć wiele połączeń z tą samą bramą sieci VPN. Przykładem może być konfiguracja połączenia obejmującego wiele lokacji. W przypadku utworzenia wielu połączeń z tą samą bramą sieci VPN wszystkie tunele VPN, łącznie z sieciami VPN typu punkt-lokacja, współużytkują przepustowość dostępną dla bramy.

### <a name="whatis"></a>Co to jest brama sieci wirtualnej?

Brama sieci wirtualnej składa się z co najmniej dwóch maszyn wirtualnych, które są wdrażane w określonej podsieci o nazwie GatewaySubnet. Maszyny wirtualne, które znajdują się w podsieci GatewaySubnet, są tworzone podczas tworzenia bramy sieci wirtualnej. Maszyny wirtualne bramy sieci wirtualnej są skonfigurowane w taki sposób, aby zawierały tabele routingu oraz specyficzne dla siebie usługi bramy. Nie można bezpośrednio skonfigurować maszyn wirtualnych, które są częścią bramy sieci wirtualnej, i nie należy nigdy wdrażać dodatkowych zasobów w podsieci GatewaySubnet.

Podczas tworzenia bramy sieci wirtualnej przy użyciu typu bramy „Vpn” tworzy on określony typ bramy sieci wirtualnej, która szyfruje ruch; jest to brama sieci VPN. Tworzenie bramy sieci VPN może potrwać do 45 minut. Dzieje się tak dlatego, że maszyny wirtualne dla bramy sieci VPN są wdrażane w podsieci GatewaySubnet i konfigurowane przy użyciu określonych przez użytkownika ustawień. Wybrana jednostka SKU bramy określa, jak wydajne są maszyny wirtualne.

## <a name="gwsku"></a>Jednostki SKU bramy

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>Konfigurowanie bramy VPN Gateway

Połączenie bramy sieci VPN bazuje na wielu zasobach konfigurowanych przy użyciu konkretnych ustawień. Większość zasobów można skonfigurować osobno, choć w niektórych przypadkach muszą być one konfigurowane w określonej kolejności.

### <a name="settings"></a>Ustawienia

Ustawienia wybrane dla każdego zasobu mają kluczowe znaczenie dla utworzenia prawidłowego połączenia. Aby uzyskać informacje na temat poszczególnych zasobów i ustawień dla bramy sieci VPN, zobacz [Ustawienia bramy sieci VPN — informacje](vpn-gateway-about-vpn-gateway-settings.md). Ten artykuł zawiera informacje ułatwiające poznanie typów bram, typów sieci VPN, typów połączeń, podsieci bram, bram sieci lokalnych i innych ustawień zasobów, które warto wziąć pod uwagę.

### <a name="tools"></a>Narzędzia wdrażania

Możesz rozpocząć tworzenie i konfigurowanie zasobów za pomocą jednego narzędzia konfiguracji, takiego jak witryna Azure Portal. Później możesz zdecydować się zmienić narzędzie na inne, np. program PowerShell, w celu skonfigurowania dodatkowych zasobów lub zmodyfikowania istniejących zasobów, jeśli jest to wymagane. Obecnie nie wszystkie zasoby i ustawienia zasobów można skonfigurować w witrynie Azure Portal. Instrukcje w artykułach dotyczących poszczególnych topologii połączeń określają, kiedy potrzebne jest konkretne narzędzie konfiguracji. 

### <a name="models"></a>Model wdrażania

Czynności wykonywane podczas konfigurowania bramy sieci VPN zależą od modelu wdrażania użytego w celu utworzenia sieci wirtualnej. Jeśli na przykład sieć wirtualna została utworzona przy użyciu klasycznego modelu wdrożenia, do tworzenia i konfigurowania ustawień bramy sieci VPN należy użyć wskazówek i instrukcji dotyczących klasycznego modelu wdrażania. Aby uzyskać więcej informacji na temat modeli wdrażania, zobacz [Omówienie modelu wdrażania przy użyciu usługi Resource Manager oraz wdrażania klasycznego](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="diagrams"></a>Diagramy topologii połączeń

Dostępne są różne konfiguracje połączeń bramy sieci VPN. Należy określić, która konfiguracja najlepiej odpowiada Twoim wymaganiom. Poniższe sekcje zawierają informacje i diagramy topologii dotyczące następujących połączeń bramy sieci VPN: Poniższe sekcje zawierają tabele z informacjami o następujących elementach:

* Dostępny model wdrażania
* Dostępne narzędzia konfiguracji
* Linki prowadzące bezpośrednio do artykułu, jeśli jest dostępny

Przedstawione diagramy i opisy mogą ułatwić wybór topologii połączenia dostosowanej do potrzeb użytkownika. Choć te diagramy przedstawiają podstawowe topologie, możliwe jest utworzenie bardziej złożonych konfiguracji z użyciem tych diagramów jako wskazówek.

## <a name="s2smulti"></a>Połączenia typu lokacja-lokacja i połączenia obejmujące wiele lokacji (tunel VPN protokołu IPsec/IKE)

### <a name="S2S"></a>Lokacja-lokacja

Połączenie bramy sieci VPN typu lokacja-lokacja to połączenie nawiązywane za pośrednictwem tunelu sieci VPN wykorzystującego protokół IPsec/IKE (IKEv1 lub IKEv2). Połączenie typu lokacja-lokacja wymaga, aby urządzenie sieci VPN znajdowało się w środowisku lokalnym, miało przypisany publiczny adres IP i nie znajdowało się za translatorem adresów sieciowych. Z połączeń typu lokacja-lokacja (S2S) można korzystać w ramach konfiguracji hybrydowych i obejmujących wiele lokalizacji.   

![Przykład połączenia typu lokacja-lokacja w usłudze Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Wiele witryn

Ten typ połączenia jest odmianą połączenia typu lokacja-lokacja. W tym przypadku tworzysz więcej niż jedno połączenie VPN z bramy sieci wirtualnej — zwykle do nawiązywania połączenia z wieloma lokacjami lokalnymi. Podczas pracy z wieloma połączeniami musisz użyć sieci VPN typu RouteBased (nazywanego dynamiczną bramą w przypadku pracy z klasycznymi sieciami wirtualnymi). Ze względu na to, że każda sieć wirtualna może mieć tylko jedną bramę sieci VPN, wszystkie połączenia za pośrednictwem bramy współużytkują dostępną przepustowość. Ten typ konfiguracji jest często określany mianem połączenia „obejmującego wiele lokacji”.

![Przykład połączenia obejmującego wiele lokacji w usłudze Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Modele wdrażania i metody nawiązywania połączeń typu lokacja-lokacja i połączeń obejmujących wiele lokacji

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Punkt-lokacja (sieć VPN przez protokół IKEv2 lub SSTP)

Połączenie bramy VPN Gateway typu punkt-lokacja pozwala utworzyć bezpieczne połączenie z siecią wirtualną z indywidualnego komputera klienckiego. Połączenie typu punkt-lokacja jest ustanawiane przez uruchomienie z komputera klienckiego. To rozwiązanie jest przydatne dla osób pracujących zdalnie, które chcą łączyć się z sieciami wirtualnymi platformy Azure z lokalizacji zdalnej, na przykład z domu lub sali konferencyjnej. Połączenie sieci VPN typu punkt-lokacja jest również przydatne zamiast połączenia sieci VPN typu lokacja-lokacja w przypadku niewielkiej liczby klientów, którzy muszą się łączyć z siecią wirtualną.

W przeciwieństwie do połączeń S2S połączenia P2S nie wymagają lokalnego, publicznego adresu IP ani urządzenia sieci VPN. Połączenia typu punkt-lokacja mogą być używane z połączeniami typu lokacja-lokacja z użyciem tej samej bramy sieci VPN, pod warunkiem że wszystkie wymagania dotyczące konfiguracji dla obu połączeń są zgodne. Aby uzyskać więcej informacji na temat połączeń punkt-lokacja, zobacz [About Point-to-Site VPN](point-to-site-about.md) (Informacje o sieci VPN typu punkt-lokacja).


![Przykład połączenia typu punkt-lokacja w usłudze Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/point-to-site.png)

### <a name="deployment-models-and-methods-for-p2s"></a>Modele wdrażania i metody nawiązywania połączeń typu punkt-lokacja

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>Połączenia między sieciami wirtualnymi (tunel VPN protokołu IPsec/IKE)

Proces nawiązywania połączenia między dwiema sieciami wirtualnymi przebiega podobnie do procesu łączenia sieci wirtualnej z lokacją lokalną. Oba typy połączeń wykorzystują bramę sieci VPN, aby zapewnić bezpieczny tunel z użyciem protokołu IPsec/IKE. Można także łączyć połączenia między sieciami wirtualnymi z konfiguracjami połączeń obejmujących wiele lokacji. Pozwala to tworzyć topologie sieci, które łączą wdrożenia obejmujące wiele lokalizacji z połączeniami między sieciami wirtualnymi.

Sieci wirtualne, między którymi tworzone jest połączenie, mogą:

* znajdować się w tym samym lub różnych regionach,
* należeć do tej samej lub różnych subskrypcji, 
* korzystać z tego samego lub różnych modeli wdrażania.

![Przykład połączenia między sieciami wirtualnymi w usłudze Azure VPN Gateway](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>Połączenia między modelami wdrażania

Platforma Azure ma obecnie dwa modele wdrażania: klasyczny model wdrażania oraz model wdrażania przy użyciu usługi Resource Manager. Jeśli korzystasz z platformy Azure od pewnego czasu, prawdopodobnie masz maszyny wirtualne i wystąpienia roli platformy Azure działające w klasycznej sieci wirtualnej. Nowsze maszyny wirtualne i wystąpienia roli mogą działać w sieci wirtualnej utworzonej w usłudze Resource Manager. Możesz utworzyć połączenie między tymi sieciami wirtualnymi, aby umożliwić zasobom w jednej sieci wirtualnej bezpośrednie komunikowanie się z zasobami w innej sieci.

### <a name="vnet-peering"></a>Komunikacja równorzędna sieci wirtualnych

Można utworzyć połączenie przy użyciu komunikacji równorzędnej sieci wirtualnych pod warunkiem, że sieć wirtualna spełnia określone wymagania. W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci wirtualnej. Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Modele wdrażania i metody nawiązywania połączeń między sieciami wirtualnymi

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (połączenie prywatne)

Usługa Microsoft Azure ExpressRoute umożliwia rozszerzanie sieci lokalnych na chmurę Microsoft za pośrednictwem połączenia prywatnego obsługiwanego przez dostawcę połączenia. Dzięki usłudze ExpressRoute można ustanowić połączenia z usługami Microsoft w chmurze, np. Microsoft Azure, Office 365 i CRM Online. Połączenie może być z sieci typu dowolna-dowolna (IP VPN), sieci Ethernet typu punkt-punkt lub przy użyciu łączności obejmującej wiele połączeń wirtualnych przez dostawcę połączenia w ramach infrastruktury współlokacji.

Połączenia ExpressRoute nie odbywają się za pośrednictwem publicznego Internetu. Dzięki temu oferują one większą niezawodność i szybkość oraz mniejsze opóźnienia i lepsze zabezpieczenia niż typowe połączenia przez Internet.

Połączenie usługi ExpressRoute nie używa bramy sieci VPN, mimo że używa bramy sieci wirtualnej w ramach wymaganej konfiguracji. W przypadku połączenia usługi ExpressRoute brama sieci wirtualnej jest konfigurowana z typem bramy „ExpressRoute” zamiast „Vpn”. Więcej informacji na temat usługi ExpressRoute zawiera artykuł [ExpressRoute technical overview](../expressroute/expressroute-introduction.md) (Opis techniczny usługi ExpressRoute).

## <a name="coexisting"></a>Współistniejące połączenia typu lokacja-lokacja i ExpressRoute

ExpressRoute to bezpośrednie, prywatne połączenie z usługami firmy Microsoft, w tym z platformą Azure, nawiązane z poziomu sieci WAN użytkownika, a nie z publicznego Internetu. Zaszyfrowany ruch połączenia sieci VPN typu lokacja-lokacja jest przesyłany za pośrednictwem publicznej sieci Internet. Możliwość konfiguracji połączenia sieci VPN typu lokacja-lokacja oraz połączenia ExpressRoute dla tej samej sieci wirtualnej niesie ze sobą pewne korzyści.

Sieć VPN typu lokacja-lokacja może zostać skonfigurowana jako bezpieczna ścieżka trybu failover dla połączenia ExpressRoute. Połączenia sieci VPN typu lokacja-lokacja mogą także zostać użyte w celu połączenia się z lokacjami, które nie są częścią sieci, ale które są połączone metodą ExpressRoute. Ta konfiguracja wymaga dwóch bram sieci wirtualnej dla tej samej sieci wirtualnej, z których jedna używa bramy typu „Vpn”, a druga — bramy typu „ExpressRoute”.

![Przykład współistniejących połączeń usług ExpressRoute i VPN Gateway](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute-coexist"></a>Modele wdrażania i metody nawiązywania połączeń typu lokacja-lokacja i połączeń usługi ExpressRoute współistnieją

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Cennik

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

Więcej informacji o jednostkach SKU bramy dla usługi VPN Gateway zawiera artykuł [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy).

## <a name="faq"></a>Często zadawane pytania

Aby zapoznać się z często zadawanymi pytaniami dotyczącymi bramy sieci VPN, zobacz [Brama VPN Gateway — często zadawane pytania](vpn-gateway-vpn-faq.md).

## <a name="next-steps"></a>Następne kroki

- Planowanie konfiguracji bramy sieci VPN. Zobacz [Planowanie i projektowanie usługi VPN Gateway](vpn-gateway-plan-design.md).
- Więcej informacji można znaleźć w temacie [Brama VPN Gateway — często zadawane pytania](vpn-gateway-vpn-faq.md).
- Wyświetl [limity usług i subskrypcji](../azure-subscription-service-limits.md#networking-limits).
- Poznaj inne kluczowe [możliwości sieciowe](../networking/networking-overview.md) platformy Azure.
