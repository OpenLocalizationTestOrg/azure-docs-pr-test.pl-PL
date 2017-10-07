---
title: "wymagania aaaNAT obwody usługi ExpressRoute | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera szczegółowe wymagania dotyczące konfigurowania translatora adresów sieciowych oraz zarządzania nim na potrzeby obwodów usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>Wymagania dotyczące translatora adresów sieciowych w usłudze ExpressRoute
tooconnect tooMicrosoft usługi w chmurze przy użyciu usługi ExpressRoute, będzie konieczne tooset się i zarządzaj nimi translatory adresów sieciowych. Niektórzy dostawcy połączenia oferują konfigurowanie translatora adresów sieciowych oraz zarządzanie nim jako usługę zarządzaną. Skontaktuj się z Twojego toosee dostawcy łączności, jeśli oferują takiej usługi. Jeśli nie, muszą spełniać wymagania toohello opisane poniżej. 

Przejrzyj hello [ExpressRoute obwody i domeny routingu](expressroute-circuit-peerings.md) strony tooget omówienie hello różnych domen routingu. toomeet hello publicznego wymagania dotyczące adresów IP dla publicznej Azure i komunikacji równorzędnej firmy Microsoft, zaleca się skonfigurowanie translatora adresów Sieciowych między siecią a firmy Microsoft. Ta sekcja zawiera szczegółowy opis hello infrastruktury NAT, należy tooset się.

## <a name="nat-requirements-for-azure-public-peering"></a>Wymagania dotyczące translatora adresów sieciowych dla publicznej komunikacji równorzędnej Azure
Hello Azure publicznej komunikacji równorzędnej ścieżki włącza możesz tooconnect tooall usługi hostowanej na platformie Azure za pośrednictwem swoich publicznych adresów IP. Obejmują one usług wymienionych w hello [ExpessRoute — często zadawane pytania](expressroute-faqs.md) i usług hostowanych przez niezależnych dostawców oprogramowania w systemie Microsoft Azure. 

> [!IMPORTANT]
> W publicznej usług łączności tooMicrosoft Azure komunikacji równorzędnej jest zawsze inicjowane z sieci do sieci firmy Microsoft hello. W związku z tym sesji nie można zainicjować z sieci tooyour usług Microsoft Azure za pośrednictwem usługi ExpressRoute. Podjęto, pakiety wysyłane toothese anonsowana adresów IP będzie używać hello internet zamiast ExpressRoute.
> 

Ruch kierowany tooMicrosoft Azure w ramach publicznej komunikacji równorzędnej musi być toovalid SNATed, adresy IPv4 publicznego przed ich wejściem hello sieci firmy Microsoft. na poniższej ilustracji Hello zawiera ogólny obraz hello NAT może być konfiguracji hello toomeet powyżej wymagań.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>Anonse puli adresów IP translatora adresów sieciowych oraz tras
Należy się upewnić, że ruch jest wprowadzane hello Azure publicznej komunikacji równorzędnej ścieżki prawidłowy publiczny adres IPv4. Microsoft musi być możliwe toovalidate własność hello hello puli adresów IPv4 NAT względem regionalny Rejestr internetowy routingu (RIR) lub rejestru routingu internetowego (IRR). Sprawdzanie zostanie wykonane oparte na powitania jako numer jest połączyć za pomocą z i hello adresy IP używane dla hello translatora adresów sieciowych. Zobacz toohello [wymagania dotyczące routingu usługi ExpressRoute](expressroute-routing.md) strony, aby uzyskać informacje dotyczące routingu rejestrów.

Nie ma żadnych ograniczeń na powitania długość prefiksu IP translatora adresów Sieciowych hello anonsowane za pomocą komunikacji równorzędnej. Należy monitorować pulę translacji NAT hello i upewnij się, że użytkownik nie zginą sesji translatora adresów Sieciowych.

> [!IMPORTANT]
> Witaj puli adresów IP translatora adresów Sieciowych anonsowany tooMicrosoft nie może być anonsowany toohello Internet. Spowoduje to przerwanie usług Microsoft tooother łączności.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Wymagania dotyczące translatora adresów sieciowych dla komunikacji równorzędnej firmy Microsoft
ścieżki komunikacji równorzędnej firmy Microsoft Hello umożliwia nawiązanie połączenia usługi tooMicrosoft w chmurze, które nie są obsługiwane za pośrednictwem hello Azure publicznej komunikacji równorzędnej ścieżki. Lista Hello usług zawiera usługi Office 365, takie jak Exchange Online, SharePoint Online i Skype dla firm i Dynamics 365. Microsoft oczekuje toosupport dwukierunkową łączność na powitania komunikacji równorzędnej firmy Microsoft. Usługi w chmurze tooMicrosoft ruch kierowany musi być toovalid SNATed, adresy IPv4 publicznego przed ich wejściem hello sieci firmy Microsoft. Ruch kierowany tooyour sieci z usługi w chmurze firmy Microsoft musi być SNATed w sieci Internet krawędzi tooprevent [asymetrycznego routingu](expressroute-asymmetric-routing.md). na poniższej ilustracji Hello zawiera ogólny obraz jak hello translatora adresów Sieciowych powinny być skonfigurowane do komunikacji równorzędnej firmy Microsoft.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>Ruch pochodzący z sieci tooMicrosoft sieci przeznaczonych
* Należy się upewnić, że ruch jest wprowadzane hello ścieżki komunikacji równorzędnej firmy Microsoft z publiczny adres IPv4. Microsoft musi być właścicielem hello stanie toovalidate hello translatora adresów Sieciowych IPv4 puli adresów przed hello regionalnych routingu Rejestr internetowy (RIR) lub rejestru routingu internetowego (IRR). Sprawdzanie zostanie wykonane oparte na powitania jako numer jest połączyć za pomocą z i hello adresy IP używane dla hello translatora adresów sieciowych. Zobacz toohello [wymagania dotyczące routingu usługi ExpressRoute](expressroute-routing.md) strony, aby uzyskać informacje dotyczące routingu rejestrów.
* Adresy IP używane dla hello Azure publicznej komunikacji równorzędnej Instalatora i innych obwody usługi ExpressRoute nie może być anonsowany tooMicrosoft za pomocą sesji protokołu BGP hello. Nie podlega ograniczeniom na powitania długość prefiksu IP translatora adresów Sieciowych hello anonsowane za pomocą komunikacji równorzędnej.
  
  > [!IMPORTANT]
  > Witaj puli adresów IP translatora adresów Sieciowych anonsowany tooMicrosoft nie może być anonsowany toohello Internet. Spowoduje to przerwanie usług Microsoft tooother łączności.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>Ruch pochodzący z sieci firmy Microsoft przeznaczone tooyour
* Niektóre scenariusze wymagają Microsoft tooinitiate łączności tooservice końcowych hostowanych w sieci. Typowym przykładem scenariusza hello byłoby łączności tooADFS serwerów hostowanych w sieci z poziomu usługi Office 365. W takich przypadkach możesz wyciek prefiksów odpowiednich z sieci do komunikacji równorzędnej firmy Microsoft hello. 
* Musi SNAT Microsoft ruchu na powitania Internet krawędzią w przypadku punktów końcowych usług w Twojej sieci tooprevent [asymetrycznego routingu](expressroute-asymmetric-routing.md). Żądania **i odpowiedzi** z docelowym adresem IP zgodne z trasą odebraną za pomocą usługi ExpressRoute będą zawsze wysyłane przy użyciu usługi ExpressRoute. Routing asymetrycznego istnieje, jeśli zostanie odebrane żądanie hello za pośrednictwem hello Internet z hello odpowiedź wysłana przez usługi ExpressRoute. SNATing hello Microsoft ruchu przychodzącego na powitania krawędzi Internet wymusza toohello wstecz odpowiedzi ruchu internetowego krawędzi, rozwiązywania problemu hello.

![Routing asymetryczny przy użyciu usługi ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>Następne kroki
* Zobacz wymagania toohello [Routing](expressroute-routing.md) i [QoS](expressroute-qos.md).
* Informacje o przepływach pracy można znaleźć w artykule [ExpressRoute circuit provisioning workflows and circuit states](expressroute-workflows.md) (Przepływy pracy inicjowania obsługi obwodu i stany obwodu usługi ExpressRoute).
* Skonfiguruj połączenie usługi ExpressRoute.
  
  * [Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)](expressroute-howto-circuit-classic.md)
  * [Configure routing (Konfigurowanie routingu)](expressroute-howto-routing-classic.md)
  * [Link sieci wirtualnej tooan obwodu usługi expressroute](expressroute-howto-linkvnet-classic.md)

