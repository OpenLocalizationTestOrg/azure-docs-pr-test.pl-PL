---
title: "aaaPrerequisites do przyjęcia Azure ExpressRoute | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera listę wymagań toobe spełnione, aby zamówić obwodu usługi Azure ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>Wymagania wstępne usługi ExpressRoute i lista kontrolna
Chmura tooMicrosoft tooconnect usług za pomocą usługi ExpressRoute, należy tooverify hello, że następujące wymagania wymienione w hello następujące sekcje zostały spełnione.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Konto platformy Azure
* Prawidłowe i aktywne konto platformy Microsoft Azure. To konto jest wymagane tooset się hello obwodu usługi expressroute. Obwody usługi ExpressRoute to zasoby w ramach subskrypcji platformy Azure. Subskrypcja platformy Azure jest wymagane, nawet jeśli łączność jest ograniczona usług chmurowych firmy Microsoft toonon Azure, takie jak usługi Office 365 i Dynamics 365.
* Aktywna subskrypcja usługi Office 365 (w przypadku korzystania z usług Office 365). Aby uzyskać więcej informacji, zobacz hello [specyficznych wymagań usługi Office 365](#office-365-specific-requirements) sekcji tego artykułu.

## <a name="connectivity-provider"></a>Dostawca połączenia

* Możesz pracować z [partnera połączenie ExpressRoute](expressroute-locations.md#partners) toohello tooconnect firmy Microsoft w chmurze. Połączenie między siecią lokalną a firmą Microsoft można skonfigurować na [trzy sposoby](expressroute-introduction.md).
* Jeśli dostawca nie jest partnera połączenia ExpressRoute, nadal można połączyć toohello firmy Microsoft w chmurze za pośrednictwem [dostawcy usług w chmurze programu exchange](expressroute-locations.md#connectivity-through-exchange-providers).

## <a name="network-requirements"></a>Wymagania dotyczące sieci
* **Łączność nadmiarowa**: nie ma wymagania nadmiarowości względem fizycznej łączności między użytkownikiem a dostawcą. Microsoft wymagają nadmiarowe toobe sesje BGP Konfigurowanie między routerami firmy Microsoft i hello routery komunikacji równorzędnej, nawet wtedy, gdy masz tylko [jednego fizycznego połączenia tooa chmury exchange](expressroute-faqs.md#onep2plink).
* **Routing**: w zależności od tego, jak można łączyć toohello Microsoft Cloud, możesz lub dostawcy muszą tooset się i zarządzanie hello sesje BGP dla [domen routingu](expressroute-circuit-peerings.md). Niektórzy dostawcy połączenia Ethernet lub dostawcy usług serwera Exchange w chmurze mogą oferować zarządzanie przy użyciu protokołu BGP w ramach usługi dodatkowej.
* **Translator adresów sieciowych**: firma Microsoft akceptuje tylko publiczne adresy IP za pośrednictwem komunikacji równorzędnej firmy Microsoft. Korzystania z prywatnych adresów IP w sieci lokalnej można lub sieci dostawcy potrzeby tootranslate hello prywatne adresy IP toohello publiczne adresy IP [przy użyciu hello NAT](expressroute-nat.md).
* **Technologia QoS**: program Skype dla firm oferuje różne usługi (np. połączenia głosowe, wideo, usługi tekstowe), które wymagają zróżnicowanej obsługi w technologii QoS. Twój dostawca loadmetrics hello [wymagania QoS](expressroute-qos.md).
* **Zabezpieczenia sieci**: należy wziąć pod uwagę [zabezpieczenia sieci](../best-practices-network-security.md) podczas łączenia toohello Microsoft Cloud za pośrednictwem usługi ExpressRoute.

## <a name="office-365"></a>Office 365
Jeśli planujesz tooenable usługi Office 365 na ExpressRoute, przejrzyj powitania po dokumentów, aby uzyskać więcej informacji o wymaganiach dotyczących usługi Office 365.

* [Omówienie usługi ExpressRoute dla usługi Office 365](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Routing za pomocą usługi ExpressRoute dla usługi Office 365](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [Zakresy adresów URL i IP dla usługi Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Planowanie sieci i dostrajanie wydajności dla usługi Office 365](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [Narzędzia i kalkulatory przepustowości sieci](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [Integracja usługi Office 365 ze środowiskiem lokalnym](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Usługa ExpressRoute w usłudze Office 365 — szkoleniowe filmy wideo dla zaawansowanych](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
Jeśli planujesz tooenable Dynamics 365 ExpressRoute, przejrzyj następujące dokumentów, aby uzyskać więcej informacji na temat Dynamics 365 hello

* [Dynamics 365 and ExpressRoute whitepaper](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf) (Usługi Dynamics 365 i ExpressRoute — oficjalny dokument)
* [Dynamics 365 URLs](https://support.microsoft.com/kb/2655102) and [IP address ranges](https://support.microsoft.com/kb/2728473) (Zakresy adresów URL i IP dla usługi Dynamics 365)

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).
* Znajdź dostawcę połączenia usługi ExpressRoute. Zobacz artykuł [ExpressRoute partners and peering locations](expressroute-locations.md) (Partnerzy i lokalizacje komunikacji równorzędnej usługi ExpressRoute).
* Zobacz toorequirements dla [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), i [QoS](expressroute-qos.md).
* Skonfiguruj połączenie usługi ExpressRoute.
  * [Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)](expressroute-howto-circuit-classic.md)
  * [Configure routing (Konfigurowanie routingu)](expressroute-howto-routing-classic.md)
  * [Link sieci wirtualnej tooan obwodu usługi expressroute](expressroute-howto-linkvnet-classic.md)
