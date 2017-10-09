---
title: "Modele połączenie ExpressRoute: łączenie się tooMicrosoft Azure za pośrednictwem dostawcy usług sieciowych, wymiany i dostawców Ethernet | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano różne tryby hello łączności między sieci i usługi Microsoft Azure i usługi Office 365, Dynamics 365 powitania klienta. Klienci mogą korzystać z dostawców MPLS, wymian w chmurze i dostawców sieci Ethernet."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>Modele połączeń usługi ExpressRoute
Można utworzyć połączenie między siecią lokalną a hello firmy Microsoft w chmurze na trzy różne sposoby, [CloudExchange wspólnej lokalizacji](#CloudExchange), [Ethernet połączeniem](#Ethernet)i [Połączenia dowolny z każdym (IPVPN)](#IPVPN). Dostawcy połączenia oferują po jednym modelu łączności lub większą ich liczbę. Możesz pracować z modelu hello toopick dostawcy łączności, które najlepiej odpowiada użytkownik.
<br><br>

![Diagram modelu połączeń usługi ExpressRoute](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>Kolokowanie w ramach wymiany w chmurze
Jeśli są umieszczone znajduje się w miejscu z programu exchange w chmurze, można zamówić toohello połączeń między wirtualnych firmy Microsoft w chmurze za pośrednictwem programu exchange Ethernet hello wspólnej lokalizacji dostawcy. Warstwy 2 cross połączenia lub zarządzanych warstwy 3 cross połączeń między infrastruktury w zakładzie wspólnej lokalizacji hello i w chmurze firmy Microsoft hello zaoferować wspólnej lokalizacji dostawcy.

## <a name="Ethernet"></a>Połączenia Ethernet typu punkt-punkt
Możesz połączyć z lokalnymi toohello centrów danych/oddziałów firmy Microsoft w chmurze za pośrednictwem łącza Ethernet point-to-point. Point-to-Point Ethernet dostawców można zaoferować połączeń warstwy 2 lub zarządzanych warstwy 3 połączenia między lokacją i hello firmy Microsoft w chmurze.

## <a name="IPVPN"></a>Sieci typu dowolna-dowolna (IPVPN)
Sieci WAN można zintegrować z hello firmy Microsoft w chmurze. Dostawcy sieci IPVPN (zwykle MPLS VPN) oferują łączność typu dowolna-dowolna między biurami oddziałów i centrami danych. Hello Microsoft chmury mogą być połączonych tooyour toomake WAN wygląda podobnie jak inne biura oddziału. Dostawcy sieci WAN oferują zazwyczaj łączność zarządzaną w warstwie 3. Funkcje i możliwości usługi ExpressRoute są wszystkie identyczne we wszystkich hello powyżej modeli łączności. 

## <a name="next-steps"></a>Następne kroki
* Więcej informacji na temat połączeń ExpressRoute i domen routingu. Zobacz artykuł [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (Obwody i domeny routingu usługi ExpressRoute).
* Dowiedz się więcej na temat funkcji usługi ExpressRoute. Zobacz hello [opis techniczny ExpressRoute](expressroute-introduction.md)
* Znajdź dostawcę usługi. Zobacz artykuł [ExpressRoute partners and peering locations](expressroute-locations.md) (Partnerzy i lokalizacje komunikacji równorzędnej usługi ExpressRoute).
* Upewnij się, że zostały spełnione wszystkie wymagania wstępne. Zobacz artykuł [ExpressRoute prerequisites](expressroute-prerequisites.md) (Wymagania wstępne usługi ExpressRoute).
* Zobacz wymagania toohello [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), i [QoS](expressroute-qos.md).
* Skonfiguruj połączenie usługi ExpressRoute.
  * [Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configure routing (Konfigurowanie routingu)](expressroute-howto-routing-portal-resource-manager.md)
  * [Link sieci wirtualnej tooan obwodu usługi expressroute](expressroute-howto-linkvnet-portal-resource-manager.md)
