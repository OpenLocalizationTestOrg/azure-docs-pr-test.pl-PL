---
title: Temat bramy sieci VPN Azure stosu | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o i konfigurowanie bramy sieci VPN, używanych w usłudze Azure stosu."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 0e30522f-20d6-4da7-87d3-28ca3567a890
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/01/2017
ms.author: brenduns
ms.openlocfilehash: ba9642d8c51f57623aded44b84d7127334806bc1
ms.sourcegitcommit: 80eb8523913fc7c5f876ab9afde506f39d17b5a1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2017
---
# <a name="about-vpn-gateway-for-azure-stack"></a>Brama sieci VPN Azure stosu — informacje
*Dotyczy: Azure stosu zintegrowanych systemów i Azure stosu Development Kit*


Przed wysłaniem ruch sieciowy między sieci wirtualnej platformy Azure i witryny lokalnej, należy utworzyć bramę sieci wirtualnej dla sieci wirtualnej.

Brama sieci VPN jest typem bramy sieci wirtualnej, który wysyła zaszyfrowany ruch sieciowy przez połączenie publiczne. Bramy sieci VPN można użyć do wysyłania ruchu bezpiecznie między sieci wirtualnej Azure stosu i sieć wirtualna na platformie Azure lub między sieci wirtualnej, a inna sieć podłączoną do urządzenia sieci VPN.

Podczas tworzenia bramy sieci wirtualnej musisz wybrać typ bramy do utworzenia. Stos Azure obsługuje jeden typ bramy sieci wirtualnej: typ "Vpn".

Każda sieć wirtualna może mieć tylko dwie bramy sieci wirtualnych, ale może istnieć tylko jedna brama danego typu. W zależności od wybranych ustawień można utworzyć wiele połączeń z jedną bramą sieci VPN. Przykładem może być konfiguracja połączenia obejmującego wiele lokacji.

> [!NOTE]
> Na platformie Azure przepływności przepustowości zostanie wybrana jednostka SKU bramy sieci VPN musi być podzielone między wszystkich połączeń, które są połączone.  W stosie Azure wartość przepustowości dla jednostki SKU bramy sieci VPN jest stosowany do każdego zasobu połączenia, który jest połączony.     

> Na przykład w usłudze Azure podstawowa jednostka SKU bramy sieci VPN może obsłużyć około 100 MB/s przepustowości agregacji.  Jeśli utworzysz dwa połączenia tej bramy VPN, a jedno połączenie używa 50 MB/s przepustowości, następnie 50 MB/s jest dostępne inne połączenie.   

> W stosie Azure *każdego* połączenie podstawowa jednostka SKU bramy sieci VPN pobiera przydzielone 100 MB/s przepustowości.

## <a name="configuring-a-vpn-gateway"></a>Konfigurowanie bramy sieci VPN
Połączenie bramy sieci VPN bazuje na wielu zasobach konfigurowanych przy użyciu konkretnych ustawień. Większość zasobów można skonfigurować osobno, choć w niektórych przypadkach muszą być one konfigurowane w określonej kolejności.

### <a name="settings"></a>Ustawienia
Ustawienia wybrane dla każdego zasobu mają kluczowe znaczenie dla utworzenia prawidłowego połączenia. Aby uzyskać informacje dotyczące poszczególnych zasobów i ustawień dla bramy sieci VPN, zobacz [ustawienia bramy sieci VPN o stosu Azure](azure-stack-vpn-gateway-settings.md). Informacje pomagające zrozumieć typy bramy, typy sieci VPN, typów połączeń, podsieci bramy, bramy sieci lokalnej i różne ustawienia zasobów, w których warto rozważyć można znaleźć.

### <a name="deployment-tools"></a>Narzędzia wdrażania
Możesz rozpocząć tworzenie i konfigurowanie zasobów za pomocą jednego narzędzia konfiguracji, takiego jak witryna Azure Portal. Później możesz zdecydować się przełączyć do innego narzędzia, takiego jak program PowerShell, w celu skonfigurowania dodatkowych zasobów lub zmodyfikowania istniejących zasobów, jeśli jest to wymagane. Obecnie nie wszystkie zasoby i ustawienia zasobów można skonfigurować w witrynie Azure Portal. Instrukcje w artykułach dotyczących poszczególnych topologii połączeń określają, kiedy potrzebne jest konkretne narzędzie konfiguracji.

## <a name="connection-topology-diagrams"></a>Diagram topologii połączenia
Dostępne są różne konfiguracje połączeń bramy sieci VPN. Należy określić, która konfiguracja najlepiej odpowiada Twoim wymaganiom. Poniższe sekcje zawierają informacje i diagramy topologii dotyczące następujących połączeń bramy sieci VPN: Poniższe sekcje zawierają tabele z informacjami o następujących elementach:

- Dostępny model wdrażania
- Dostępne narzędzia konfiguracji
- Linki prowadzące bezpośrednio do artykułu, jeśli jest dostępny

Diagramy i opisy w poniższych sekcjach ułatwią topologii połączenia dostosować do swoich potrzeb. Choć te diagramy przedstawiają podstawowe topologie, możliwe jest utworzenie bardziej złożonych konfiguracji z użyciem tych diagramów jako wskazówek.

## <a name="site-to-site-and-multi-site-ipsecike-vpn-tunnel"></a>Połączenia typu lokacja-lokacja i połączenia obejmujące wiele lokacji (tunel VPN protokołu IPsec/IKE)
### <a name="site-to-site"></a>Lokacja-lokacja
Połączenie bramy sieci VPN typu lokacja-lokacja to połączenie nawiązywane za pośrednictwem tunelu sieci VPN wykorzystującego protokół IPsec/IKE (IKEv1 lub IKEv2). Ten typ połączenia wymaga, aby urządzenie sieci VPN znajdowało się lokalnie, miało przypisany publiczny adres IP i nie znajdowało się za translatorem adresów sieciowych. Z połączeń typu lokacja-lokacja (S2S) można korzystać w ramach konfiguracji hybrydowych i obejmujących wiele lokalizacji.    
![Przykład konfiguracji połączenia sieci VPN typu lokacja lokacja](media/azure-stack-vpn-gateway-about-vpn-gateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="multi-site"></a>Obejmujące wiele lokacji
Ten typ połączenia jest odmianą połączenia typu lokacja-lokacja. W tym przypadku tworzysz więcej niż jedno połączenie VPN z bramy sieci wirtualnej — zwykle do nawiązywania połączenia z wieloma lokacjami lokalnymi. Podczas pracy z wieloma połączeniami musisz użyć sieci VPN typu RouteBased (nazywanego dynamiczną bramą w przypadku pracy z klasycznymi sieciami wirtualnymi). Ze względu na to, że każda sieć wirtualna może mieć tylko jedną bramę sieci VPN, wszystkie połączenia za pośrednictwem bramy współużytkują dostępną przepustowość. Ten typ konfiguracji jest często określany mianem połączenia „obejmującego wiele lokacji”.   
![Przykład połączenia obejmującego wiele lokacji w usłudze Azure VPN Gateway](media/azure-stack-vpn-gateway-about-vpn-gateways/vpngateway-multisite-connection-diagram.png)



## <a name="gateway-skus"></a>Jednostki SKU bramy
Po utworzeniu bramy sieci wirtualnej Azure stosu, możesz określić bramy jednostka SKU, którego chcesz używać. Obsługiwane są następujące jednostki SKU bramy sieci VPN:
- Podstawowa
- Standardowa (Standard)
- Wysoka wydajność (HighPerformance)

Po wybraniu wyższej bramy jednostka SKU, takich jak standardowy za pośrednictwem Basic lub wysokowydajnej za pośrednictwem Standard lub Basic więcej procesorów i przepustowość sieci są przydzielone do bramy. W związku z tym bramy może obsługiwać wyższej przepustowości sieci do sieci wirtualnej.

Stos Azure nie obsługuje bramy UltraPerformance jednostka SKU, które jest używane wyłącznie w przypadku Express Route.

Podczas wybierania jednostki SKU należy wziąć pod uwagę następujące zagadnienia:
- Stos Azure nie obsługuje bramy oparte na zasadach.
- Protokół BGP (Border Gateway) nie jest obsługiwana na podstawowy SKU.
- Brama sieci VPN ExpressRoute współistnieją konfiguracje nie są obsługiwane w stosie Azure
- Połączenia usługi VPN Gateway typu lokacja do lokacji (S2S) aktywne-aktywne można skonfigurować tylko w ramach jednostki SKU o wysokiej wydajności.

## <a name="estimated-aggregate-throughput-by-sku"></a>Szacowana agregowana przepływność według jednostki SKU
W poniższej tabeli przedstawiono typy bram i szacowaną agregowaną przepływność według jednostek SKU bramy.

|   | Przepływność bramy sieci VPN *(1)* |Max tuneli protokołu IPsec bramy sieci VPN |
|-------|-------|-------|
|**Podstawowy SKU** ***(2)***    | 100 Mb/s  | 10    |
|**Standardowy SKU**       | 100 Mb/s  | 10    |
|**SKU wysokiej wydajności** | 200 Mb/s    | 30    |
***(1)***  Przepływność sieci VPN nie jest gwarantowanej przepustowości dla połączeń między lokalizacjami w Internecie. Jest to maksymalna możliwa przepustowość.  
***(2)***  BGP nie jest obsługiwana dla podstawowej jednostki SKU.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [ustawienia dla bram sieci VPN](azure-stack-vpn-gateway-settings.md) stosu Azure.
