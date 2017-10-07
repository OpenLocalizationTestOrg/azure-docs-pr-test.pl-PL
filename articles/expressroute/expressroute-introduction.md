---
title: "Omówienie usługi ExpressRoute: Rozszerzenie Twojej lokalnej sieci tooAzure za pośrednictwem połączenia prywatnego | Dokumentacja firmy Microsoft"
description: "Ten opis techniczny ExpressRoute wyjaśniono sposób połączenia ExpressRoute działania tooextend Twojego tooAzure sieci lokalnej za pośrednictwem połączenia prywatnego."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>Omówienie usługi ExpressRoute
Microsoft Azure ExpressRoute pozwala rozszerzyć sieci lokalnej na powitania firmy Microsoft w chmurze za pośrednictwem połączenia prywatne w ramach dostawcy łączności. Z usługi ExpressRoute można ustanowić połączenia usług chmury tooMicrosoft, takich jak Microsoft Azure i usługi Office 365, Dynamics 365.

Połączenie może być z sieci typu dowolna-dowolna (IP VPN), sieci Ethernet typu punkt-punkt lub przy użyciu łączności obejmującej wiele połączeń wirtualnych przez dostawcę połączenia w ramach infrastruktury współlokacji. Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet. Dzięki toooffer połączeń ExpressRoute więcej niezawodności, szybkości szybsze niższe opóźnienia i lepsze zabezpieczenia niż typowe połączenia za pośrednictwem Internetu hello. Aby uzyskać informacje na temat tooconnect Twojego tooMicrosoft sieci przy użyciu usługi ExpressRoute, zobacz [modeli połączenie ExpressRoute](expressroute-connectivity-models.md).

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>Najważniejsze korzyści

* Warstwy 3 łączności między siecią lokalną a hello Microsoft Cloud za pośrednictwem dostawcy łączności. Połączenie może być z sieci typu dowolna-dowolna (IP VPN), sieci Ethernet typu punkt-punkt lub przy użyciu łączności obejmującej wiele połączeń wirtualnych za pośrednictwem wymiany sieci Ethernet.
* Łączność tooMicrosoft usługi w chmurze we wszystkich regionach w regionie geograficznymi hello.
* Globalne łączności usługi tooMicrosoft we wszystkich regionach z dodatkiem premium usługi ExpressRoute.
* Routing dynamiczny między siecią użytkownika i firmą Microsoft za pośrednictwem standardowych protokołów (BGP).
* Wbudowana nadmiarowość w każdej lokalizacji komunikacji równorzędnej w celu uzyskania większej niezawodności.
* Czas sprawnego działania połączenia zgodnie z umową [SLA](https://azure.microsoft.com/support/legal/sla/).
* Obsługa QoS dla programu Skype dla firm.

Aby uzyskać więcej informacji, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).

## <a name="features"></a>Funkcje

### <a name="layer-3-connectivity"></a>Łączność w warstwie 3
Microsoft używa branżowy standard dynamiczne routingu protocol (BGP) tooexchange tras między siecią lokalną, swoich wystąpień na platformie Azure i Microsoft publicznych adresów.  Ustanawiamy wiele sesji BGP z siecią dla różnych profilów ruchu. Więcej informacji można znaleźć w hello [ExpressRoute obwodu i domeny routingu](expressroute-circuit-peerings.md) artykułu.

### <a name="redundancy"></a>Nadmiarowość
Każdy obwód usługi ExpressRoute składa się z dwóch połączeń tootwo Microsoft Enterprise krawędzi routery (MSEEs) od dostawcy łączności hello / Twojej sieci krawędzi. Firma Microsoft wymaga dwóch połączenia BGP od dostawcy łączności hello / po stronie — jeden tooeach MSEE. Można wybrać nie toodeploy nadmiarowe urządzenia / obwody Ethernet z końcem. Jednak łączności dostawcy używają tooensure nadmiarowe urządzeń, które przekazuje połączenia tooMicrosoft w sposób nadmiarowe. Nadmiarowe konfiguracji łączności warstwy 3 jest wymagany przez naszych [SLA](https://azure.microsoft.com/support/legal/sla/) toobe prawidłowe.

### <a name="connectivity-toomicrosoft-cloud-services"></a>Usługi w chmurze tooMicrosoft łączności
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Połączenia ExpressRoute Włącz dostęp toohello następujące usługi:

* Usługi Microsoft Azure
* Usługi Microsoft Office 365
* Microsoft Dynamics 365

Użytkownik może odwiedzić hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) strony, aby uzyskać szczegółową listę usług obsługiwanych przez usługi ExpressRoute.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>Regiony tooall łączność w obrębie regionu geograficznymi
Możesz połączyć tooMicrosoft w jednym z naszych [komunikacji równorzędnej lokalizacje](expressroute-locations.md) i regiony tooall dostępu w obrębie regionu geograficznymi hello. 

Na przykład jeśli tooMicrosoft w Amsterdamie są połączone za pośrednictwem usługi ExpressRoute, masz dostęp tooall usług chmurowych firmy Microsoft w Europa Północna i Europa Zachodnia. Zobacz hello [ExpressRoute partnerów i lokalizacje komunikacji równorzędnej](expressroute-locations.md) artykuł Omówienie hello geograficznymi regionów, skojarzone regionów chmury firmy Microsoft i odpowiedniej lokalizacji komunikacji równorzędnej ExpressRoute.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>Globalna łączność dzięki dodatkowi ExpressRoute Premium
Można włączyć hello ExpressRoute premium dodatek funkcji tooextend łączności między granicami geograficznymi. Na przykład, jeśli są połączone tooMicrosoft w Amsterdamie za pośrednictwem usługi ExpressRoute, konieczne będzie dostępu tooall usług chmurowych firmy Microsoft obsługiwanych we wszystkich regionach w hello world (national chmury są wyłączone). Można uzyskać dostępu do usług wdrożone w Azji lub Australii hello tak samo dostęp hello północ i regiony Europa Zachodnia.

### <a name="rich-connectivity-partner-ecosystem"></a>Bogaty ekosystem partnerów łączności
Usługa ExpressRoute ma rosnący ekosystem dostawców połączenia i partnerów SI. Może się odwoływać toohello [ExpressRoute dostawców i lokalizacje](expressroute-locations.md) artykuł, aby hello najnowsze informacje.

### <a name="connectivity-toonational-clouds"></a>Łączność toonational chmur
Firma Microsoft obsługuje izolowane środowiska w chmurze dla określonych regionów geopolitycznych i segmentów klientów. Zobacz toohello [ExpressRoute dostawców i lokalizacje](expressroute-locations.md) strony listę national chmur i dostawców.

### <a name="bandwidth-options"></a>Opcje przepustowości
Możesz zakupić obwody usługi ExpressRoute do szerokiego zakresu przepustowości. Lista obsługiwanych przepustowości znajduje się poniżej. Należy się toocheck z łączności dostawcy toodetermine hello listę obsługiwanych wartości przepustowości, które zapewniają.

* 50 Mb/s
* 100 Mb/s
* 200 Mb/s
* 500 Mb/s
* 1 Gb/s
* 2 Gb/s
* 5 Gb/s
* 10 Gb/s

### <a name="dynamic-scaling-of-bandwidth"></a>Dynamiczne skalowanie przepustowości
Przepustowości obwodu ExpressRoute hello (na podstawie bieżącej sytuacji) można zwiększyć, bez konieczności tootear dół połączenia. 

### <a name="flexible-billing-models"></a>Elastyczne modele rozliczeń
Możesz wybrać najlepszy dla siebie model rozliczeń. Wybierz między modelami rozliczeń hello wymienionych poniżej. Aby uzyskać więcej informacji, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).

* **Nieograniczona ilość danych**. rozliczany w oparciu o miesięcznej opłaty za Hello obwodu usługi expressroute, a cały transfer danych przychodzących i wychodzących jest dołączany bez dodatkowych opłat. 
* **Mierzone dane**. Hello obwodu ExpressRoute jest pobierana w oparciu o miesięcznej opłaty za. Cały transfer danych przychodzących jest bezpłatny. Transfer danych wychodzących jest obciążany opłatą za GB transferu danych. Stawki transferu danych różnią się zależnie od regionu.
* **Dodatek ExpressRoute Premium**. Hello ExpressRoute premium jest dodatek hello obwodu usługi expressroute. Dodatek premium ExpressRoute Hello zapewnia hello następujące możliwości: 
  * Limity zwiększona trasy dla publicznych i Azure prywatnej komunikacji równorzędnej platformy Azure z 4000 too10 tras, 000 trasy.
  * Globalna łączność dla usług. Obwodu usługi ExpressRoute utworzone w dowolnym regionie (z wyjątkiem national chmur) będzie miał tooresources dostępu przez innego regionu hello world. Na przykład dostęp do sieci wirtualnej utworzonej w Europie Zachodniej można uzyskać za pośrednictwem obwodu usługi ExpressRoute zainicjowanego w Dolinie Krzemowej.
  * Zwiększonej liczby łącza sieci wirtualnej dla obwodu usługi expressroute z 10 limitu większych tooa, w zależności od przepustowości hello hello obwodu.

## <a name="faq"></a>Często zadawane pytania

Często zadawane pytania na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [modelach połączeń usługi ExpressRoute](expressroute-connectivity-models.md).
* Więcej informacji na temat połączeń ExpressRoute i domen routingu. Zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).
* Znajdź dostawcę usługi. Zobacz artykuł [ExpressRoute partners and peering locations](expressroute-locations.md) (Partnerzy i lokalizacje komunikacji równorzędnej usługi ExpressRoute).
* Upewnij się, że zostały spełnione wszystkie wymagania wstępne. Zobacz artykuł [ExpressRoute prerequisites](expressroute-prerequisites.md) (Wymagania wstępne usługi ExpressRoute).
* Zobacz wymagania toohello [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), i [QoS](expressroute-qos.md).
* Skonfiguruj połączenie usługi ExpressRoute.
  * [Tworzenie obwodu usługi ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Konfigurowanie komunikacji równorzędnej na potrzeby obwodu usługi ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
  * [Połączenie wirtualnej sieci tooan obwodu usługi expressroute](expressroute-howto-linkvnet-portal-resource-manager.md)
* Dowiedz się więcej o niektórych hello innego klucza [możliwości w zakresie obsługi](../networking/networking-overview.md) platformy Azure.
