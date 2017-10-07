---
title: aaaAzure ExpressRoute obwody i domeny routingu | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie obwody usługi ExpressRoute i hello domeny routingu."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>Obwody usługi ExpressRoute i domeny routingu
 Należy zamówić *obwodu ExpressRoute* tooconnect Twojego tooMicrosoft infrastruktury lokalnej za pośrednictwem dostawcy łączności. na poniższej ilustracji Hello zapewnia logiczną reprezentację połączenia między sieci WAN i firmy Microsoft.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>Obwody usługi ExpressRoute
*Obwodu ExpressRoute* reprezentuje połączenie logiczne między lokalną infrastrukturą i usługi w chmurze firmy Microsoft za pośrednictwem dostawcy łączności. Można zamówić wielu obwody usługi ExpressRoute. Każdy obwód może być w hello tych samych lub różnych regionach i może być lokalnym tooyour połączonych za pośrednictwem połączenia różnych dostawców. 

Obwody usługi ExpressRoute nie mapują jednostek fizycznych tooany. Obwód jest unikatowo identyfikowana przez standardowej GUID o nazwie jako klucz usługi (s-key). Klucz usługi Hello jest hello tylko wymieniane między firmą Microsoft, dostawca połączenia hello, a informacje. Witaj s klucz nie jest klucz tajny ze względów bezpieczeństwa. Istnieje mapowanie między obwodu ExpressRoute i hello 1:1 s klucza.

Obwodu usługi ExpressRoute może zawierać maksymalnie niezależne komunikacji równorzędnych toothree: Azure prywatnego publiczne, Azure i firmy Microsoft. Każdy równorzędna to dwa niezależne BGP sesji ich nadmiarowo skonfigurowany pod kątem wysokiej dostępności. Brak 1: n (1 < = N < = 3) mapowanie między obwodu usługi ExpressRoute i domeny routingu. Obwodu usługi ExpressRoute może mieć jeden, dwa lub wszystkich trzech komunikacji równorzędnych włączone dla obwodu usługi expressroute.

Każdy obwód ma stały przepustowości (50 MB/s, 100 MB/s, 200 MB/s, 500 MB/s, 1 GB/s, 10 GB/s) i jest mapowane tooa łączności dostawcy i lokalizacja komunikacji równorzędnej. Hello przepustowości, którą wybierzesz jest współużytkowana przez wszystkie hello komunikacji równorzędnych dla hello obwodu. 

### <a name="quotas-limits-and-limitations"></a>Przydziały, ograniczenia i ograniczenia
Domyślne przydziały i limity mają zastosowanie dla każdego obwodu usługi expressroute. Zobacz toohello [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md) stronę aktualne informacje dotyczące przydziałów.

## <a name="expressroute-routing-domains"></a>Domeny routingu usługi ExpressRoute
Obwodu usługi ExpressRoute ma wiele domen routingu skojarzonych z nim: Azure prywatnego publiczne, Azure i firmy Microsoft. Każdej z domen routingu hello jest skonfigurowane tak samo w parze składającej się z routerów (aktywny aktywny lub udostępniania obciążenia konfiguracji) wysokiej dostępności. Usług platformy Azure są sklasyfikowane jako *Azure publicznego* i *Azure prywatnego* toorepresent hello schematów adresowania IP.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>Prywatna komunikacja równorzędna
Usługi, a mianowicie maszyn wirtualnych (IaaS) rozwiązań usługi obliczenia Azure i usługi w chmurze (PaaS), które są wdrażane w ramach sieci wirtualnej mogą zostać połączone za pośrednictwem hello prywatnej komunikacji równorzędnej domeny. Witaj prywatnej komunikacji równorzędnej domeny jest uważany za toobe rozszerzenie zaufanych sieci podstawowej w Microsoft Azure. Można skonfigurować dwukierunkowej łączności między sieci podstawowej i sieci wirtualnych platformy Azure (sieci wirtualne). Komunikacji równorzędnej umożliwia podłączanie maszyn toovirtual i w chmurze usługi bezpośrednio na swoich prywatnych adresów IP.  

Można połączyć z więcej niż jedną sieć wirtualną toohello prywatnej komunikacji równorzędnej domenę. Przejrzyj hello [z często Zadawanymi pytaniami](expressroute-faqs.md) informacji na temat limity i ograniczenia. Użytkownik może odwiedzić hello [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md) stronę aktualnych informacji o granicach.  Zobacz toohello [Routing](expressroute-routing.md) strony, aby uzyskać szczegółowe informacje o konfiguracji routingu.

### <a name="public-peering"></a>Publiczna komunikacja równorzędna
Usługi, takie jak usługi Azure Storage, baz danych i witryn sieci Web są oferowane na publiczne adresy IP. Możesz połączyć prywatnie tooservices hostowanych na publiczne adresy IP, w tym wirtualne adresy IP usług chmury, za pośrednictwem hello publicznej domeny routingu komunikacji równorzędnej. Możesz łączyć hello publicznej komunikacji równorzędnej domeny tooyour DMZ i połączyć tooall Azure usługi na swoich publicznych adresów IP z sieci WAN, bez konieczności tooconnect za pośrednictwem hello internet. 

Połączenie jest zawsze inicjowane z sieci WAN tooMicrosoft Azure usługi. Usługi Microsoft Azure nie będą mogli tooinitiate połączeń w sieci za pomocą tej domeny routingu. Po włączeniu publicznej komunikacji równorzędnej będą mogli tooconnect tooall Azure usługi. Firma Microsoft nie pozwalają tooselectively pobrania usług, dla których firma Microsoft anonsowanie trasy do. Możesz przejrzeć hello listę prefiksów możemy anonsowanie tooyou za pomocą komunikacji równorzędnej hello [zakresów IP centrum danych Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653) strony. Strona Hello jest aktualizowana co tydzień.

W ramach sieci tooconsume tylko hello trasy potrzebne, można zdefiniować filtry tras niestandardowych. Zobacz toohello [Routing](expressroute-routing.md) strony, aby uzyskać szczegółowe informacje o konfiguracji routingu. 

Zobacz hello [z często Zadawanymi pytaniami](expressroute-faqs.md) uzyskać więcej informacji na temat usługi obsługiwane za pośrednictwem hello publicznej domeny routingu komunikacji równorzędnej. 

### <a name="microsoft-peering"></a>Komunikacja równorzędna firmy Microsoft
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Łączność tooall będzie innych usług online firmy Microsoft (takich jak usługi Office 365) za pomocą komunikacji równorzędnej firmy Microsoft hello. Firma Microsoft Włącz dwukierunkowej łączności między usług w chmurze firmy Microsoft i WAN za pomocą komunikacji równorzędnej domeny routingu hello firmy Microsoft. Usługi w chmurze tooMicrosoft należy połączyć się tylko w przypadku publicznych adresów IP, które należą do firmy przez użytkownika lub dostawcą połączenia i tooall hello zdefiniowane zasady muszą być zgodne. Zobacz hello [wymagania wstępne usługi ExpressRoute](expressroute-prerequisites.md) strony, aby uzyskać więcej informacji.

Zobacz hello [z często Zadawanymi pytaniami](expressroute-faqs.md) Aby uzyskać więcej informacji na temat usługi obsługiwane, kosztów i szczegóły konfiguracji. Zobacz hello [lokalizacje ExpressRoute](expressroute-locations.md) strony, aby uzyskać informacje na liście hello dostawców łączności oferty komunikacji równorzędnej pomocy technicznej firmy Microsoft.

## <a name="routing-domain-comparison"></a>Porównanie domeny routingu
Witaj w poniższej tabeli porównano hello trzy domeny routingu.

|  | **Prywatnej komunikacji równorzędnej** | **Publicznej komunikacji równorzędnej** | **Komunikacji równorzędnej firmy Microsoft** |
| --- | --- | --- | --- |
| **Maks. prefiksy # obsługiwane na komunikacji równorzędnej** |4000 domyślnie 10 000 z ExpressRoute — wersja Premium |200 |200 |
| **Obsługiwane zakresów adresów IP** |Dowolny prawidłowy adres IPv4 w sieci WAN. |Publiczne adresy IPv4 posiadanych przez użytkownika lub dostawcą połączenia. |Publiczne adresy IPv4 posiadanych przez użytkownika lub dostawcą połączenia. |
| **JAKO liczba wymagań** |Prywatne i publiczne jako liczby. Użytkownik musi być właścicielem hello publicznego jako numer po wybraniu toouse jeden. |Prywatne i publiczne jako liczby. Jednak musisz udowodnić własność publicznych adresów IP. |Prywatne i publiczne jako liczby. Jednak musisz udowodnić własność publicznych adresów IP. |
| **Routingu adresów IP interfejsu** |RFC1918 i publiczne adresy IP |Publiczny adres IP adresów tooyou zarejestrowanych w rejestrach routingu. |Publiczny adres IP adresów tooyou zarejestrowanych w rejestrach routingu. |
| **Obsługa wyznaczania wartości skrótu MD5** |Tak |Tak |Tak |

Możesz tooenable jeden lub więcej domen routingu hello w ramach obwodu usługi ExpressRoute. Możesz wybrać toohave wszystkich domen routingu hello zawiesić hello tej samej sieci VPN, jeśli chcesz, aby toocombine je do jednej domeny routingu. Można również wprowadzić je w różnych domenach routingu podobne diagram toohello. Witaj zalecana konfiguracja jest tym prywatnej komunikacji równorzędnej jest połączony bezpośrednio toohello sieci podstawowej i hello publicznego i łączy komunikacji równorzędnej firmy Microsoft są połączone tooyour DMZ.

Jeśli wybierzesz toohave wszystkie trzy sesje komunikacji równorzędnej, musi mieć trzy pary sesje BGP (jedna para dla każdego typu komunikacji równorzędnej). pary sesji BGP Hello podaj łącze wysokiej dostępności. Jeśli łączysz się za pośrednictwem warstwy 2 łączności dostawców, będzie odpowiedzialny za konfigurowanie i Zarządzanie routingiem. Możesz dowiedzieć się więcej, przeglądając hello [przepływy pracy](expressroute-workflows.md) dotyczące konfigurowania usługi ExpressRoute.

## <a name="next-steps"></a>Następne kroki
* Znajdź dostawcę usługi. Zobacz [usługi ExpressRoute dostawców i lokalizacje](expressroute-locations.md).
* Upewnij się, że zostały spełnione wszystkie wymagania wstępne. Zobacz artykuł [ExpressRoute prerequisites](expressroute-prerequisites.md) (Wymagania wstępne usługi ExpressRoute).
* Skonfiguruj połączenie usługi ExpressRoute.
  * [Tworzenie obwodów usługi ExpressRoute i zarządzanie nimi](expressroute-howto-circuit-portal-resource-manager.md)
  * [Konfigurowanie routingu (komunikacji równorzędnej) dla obwodów usługi ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)

