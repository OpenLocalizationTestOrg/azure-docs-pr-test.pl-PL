---
title: "Translator adresów sieciowych dla usługi Azure ExpressRoute | Microsoft Docs"
description: "Ta strona zawiera szczegółowe wymagania dotyczące konfigurowania routingu oraz zarządzania nim na potrzeby obwodów usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>Translator adresów sieciowych dla usługi ExpressRoute

tooconnect tooMicrosoft usługi w chmurze przy użyciu usługi ExpressRoute, będzie konieczne tooset się i zarządzaj nimi routingu. Niektórzy dostawcy połączenia oferują konfigurowanie routingu oraz zarządzanie nim jako usługą zarządzaną. Skontaktuj się z Twojego toosee dostawcy łączności, jeśli oferują tej usługi. Jeśli nie, toohello następujące wymagania muszą być zgodne. 

Zobacz toohello [obwody i domeny routingu](expressroute-circuit-peerings.md) artykułu Opis routingu hello sesje, które wymagają toobe Konfigurowanie w toofacilitate łączności.

> [!NOTE]
> Firma Microsoft nie obsługuje protokołów nadmiarowości routerów (np. HSRP, VRRP) w konfiguracjach wysokiej dostępności. Polegamy na nadmiarowej parze sesji protokołu BGP na komunikację równorzędną w celu zapewnienia wysokiej dostępności.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>Adresy IP używane do komunikacji równorzędnej

Należy tooreserve kilka bloków IP adresów tooconfigure routingu między siecią a routery brzegowe (MSEEs) przedsiębiorstwa firmy Microsoft. Ta sekcja zawiera listę wymagań i opisuje hello zasady dotyczące sposób musi uzyskać i używać tych adresów IP.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Adresy IP używane do prywatnej komunikacji równorzędnej Azure

Można użyć prywatnych adresów IP lub publicznego adresu IP adresów tooconfigure hello komunikacji równorzędnych. zakres adresów Hello używane do konfigurowania tras nie mogą się pokrywać z sieciami wirtualnymi toocreate używane zakresy adresów w usłudze Azure. 

* Należy zarezerwować podsieć /29 lub dwie podsieci /30 dla interfejsów routingu.
* używane do przesyłania podsieci Hello można prywatnych adresów IP lub publicznych adresów IP.
* Witaj podsieci nie może powodować konfliktu z zakresem hello zastrzeżone przez powitania klienta do użycia w chmurze firmy Microsoft hello.
* Jeśli zostanie użyta podsieć /29, zostanie ona podzielona na dwie podsieci /30. 
  * najpierw Hello/30 podsieci będą używane dla linku podstawowego hello i hello /30 drugiej podsieci będą używane dla linku dodatkowego hello.
  * Dla każdej podsieci hello /30 należy użyć hello pierwszy adres IP podsieci hello /30 na routerze. Firma Microsoft będzie używać hello drugiego adresu IP tooset podsieci hello /30 sesji BGP.
  * Należy skonfigurować zarówno sesje BGP dla naszych [dostępność](https://azure.microsoft.com/support/legal/sla/) toobe jest nieprawidłowy.  

#### <a name="example-for-private-peering"></a>Przykład prywatnej komunikacji równorzędnej

Jeśli wybierzesz tooset a.b.c.d/29 toouse się hello komunikacji równorzędnej, zostaną podzielone na dwa /30 podsieci. W poniższym przykładzie hello przedstawiono, jak podsieć a.b.c.d/29 hello jest używany. 

a.b.c.d/29 będzie tooa.b.c.d/30 podziału i a.b.c.d+4/30 i przekazywane w dół tooMicrosoft za pośrednictwem hello inicjowania obsługi administracyjnej interfejsów API. A.b.c.d+1 będzie używany jako hello VRF IP hello PE podstawowego i Microsoft zużyje a.b.c.d+2 jako hello VRF IP dla hello MSEE podstawowego. A.b.c.d+5 będzie używany jako hello VRF IP hello dodatkowej PE i Microsoft użyje a.b.c.d+6 jako hello VRF IP dla hello MSEE dodatkowej.

Należy wziąć pod uwagę przypadek, w którym należy wybrać tooset 192.168.100.128/29 się prywatnej komunikacji równorzędnej. 192.168.100.128/29 zawiera adresy z 192.168.100.128 too192.168.100.135, do których:

* 192.168.100.128/30 zostanie przypisany toolink1, przy użyciu 192.168.100.129 i firmy Microsoft przy użyciu 192.168.100.130 dostawcy.
* 192.168.100.132/30 zostanie przypisany toolink2, przy użyciu 192.168.100.133 i firmy Microsoft przy użyciu 192.168.100.134 dostawcy.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Adresy IP używane do publicznej komunikacji równorzędnej Azure i komunikacji równorzędnej firmy Microsoft

Publiczne adresy IP, które masz korzystać do konfigurowania hello sesje BGP. Microsoft musi być możliwe tooverify hello własność hello adresów IP przy użyciu routingu rejestrów internetowych i rejestrów routingu internetowego. 

* Należy użyć unikatowego/29 podsieci lub tooset /30 dwie podsieci zapasowej hello BGP komunikacji równorzędnej dla każdego komunikacji równorzędnej dla obwodu usługi expressroute (Jeśli masz więcej niż jeden). 
* Jeśli zostanie użyta podsieć /29, zostanie ona podzielona na dwie podsieci /30. 
  * najpierw Hello/30 podsieci będą używane dla linku podstawowego hello i hello /30 drugiej podsieci będą używane dla linku dodatkowego hello.
  * Dla każdej podsieci hello /30 należy użyć hello pierwszy adres IP podsieci hello /30 na routerze. Firma Microsoft będzie używać hello drugiego adresu IP tooset podsieci hello /30 sesji BGP.
  * Należy skonfigurować zarówno sesje BGP dla naszych [dostępność](https://azure.microsoft.com/support/legal/sla/) toobe jest nieprawidłowy.

## <a name="public-ip-address-requirement"></a>Wymagania dotyczące publicznego adresu IP

### <a name="private-peering"></a>Prywatna komunikacja równorzędna

Możesz wybrać toouse publicznych lub prywatnych adresów IPv4 dla prywatnej komunikacji równorzędnej. Firma Microsoft zapewnia kompleksową izolację ruchu, w związku z czym w warunkach prywatnej komunikacji równorzędnej nie ma możliwości, aby adresy się nakładały. Tych adresów nie są anonsowany tooInternet. 

### <a name="public-peering"></a>Publiczna komunikacja równorzędna

Hello Azure publicznej komunikacji równorzędnej ścieżki włącza możesz tooconnect tooall usługi hostowanej na platformie Azure za pośrednictwem swoich publicznych adresów IP. Obejmują one usług wymienionych w hello [ExpessRoute — często zadawane pytania](expressroute-faqs.md) i usług hostowanych przez niezależnych dostawców oprogramowania w systemie Microsoft Azure. W publicznej usług łączności tooMicrosoft Azure komunikacji równorzędnej jest zawsze inicjowane z sieci do sieci firmy Microsoft hello. Publiczny adres IP musi używać hello ruchu kierowana tooMicrosoft sieci.

### <a name="microsoft-peering"></a>Komunikacja równorzędna firmy Microsoft

ścieżki komunikacji równorzędnej firmy Microsoft Hello umożliwia nawiązanie połączenia usługi tooMicrosoft w chmurze, które nie są obsługiwane za pośrednictwem hello Azure publicznej komunikacji równorzędnej ścieżki. Lista Hello usług zawiera usługi Office 365, takie jak Exchange Online, SharePoint Online i Skype dla firm i Dynamics 365. Firma Microsoft obsługuje dwukierunkową łączność na powitania komunikacji równorzędnej firmy Microsoft. Usługi w chmurze tooMicrosoft ruch kierowany musi używać prawidłowych publicznych adresów IPv4, przed ich wejściem hello sieci firmy Microsoft.

Upewnij się, że liczba swój adres IP i jak są tooyou zarejestrowanych w jednym z rejestrów hello wymienionych poniżej.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> Publiczny adres IP na adresy anonsowane tooMicrosoft za pośrednictwem usługi ExpressRoute nie może być anonsowany toohello Internet. Może to spowodować uszkodzenie usług Microsoft tooother łączności. Używane przez serwery w sieci użytkownika publiczne adresy IP, które komunikują się z punktami końcowymi usługi O365 w środowisku firmy Microsoft, mogą być jednak anonsowane za pośrednictwem usługi ExpressRoute. 
> 
> 

## <a name="dynamic-route-exchange"></a>Wymiana tras dynamicznych

Wymiana routingu będzie odbywać się za pośrednictwem protokołu eBGP. Sesje EBGP są wyznaczane między hello MSEEs i routery. Uwierzytelnianie sesji BGP nie jest wymagane. W razie potrzeby można skonfigurować skrót MD5. Zobacz hello [Konfigurowanie routingu](expressroute-howto-routing-classic.md) i [obwodu inicjowania obsługi administracyjnej przepływów pracy i stanów obwodów](expressroute-workflows.md) informacji o konfigurowaniu sesje BGP.

## <a name="autonomous-system-numbers"></a>Numery systemu autonomicznego

Firma Microsoft będzie używać numeru AS 12076 do publicznej i prywatnej komunikacji równorzędnej Azure oraz komunikacji równorzędnej Microsoft. Firma Microsoft ma rezerwowany numerów ASN 65515 too65520 do użytku wewnętrznego. Obsługiwane są zarówno 16-, jak i 32-bitowe numery AS.

Nie ma żadnych wymagań związanych z symetrią transferu danych. ścieżki do przodu i zwracany Hello może przechodzić między nimi pary router innej. Trasy identyczne muszą być anonsowane ze wszystkich stron w wielu parach obwodów należących do użytkownika. Metryki trasy nie są wymagane toobe identyczne.

## <a name="route-aggregation-and-prefix-limits"></a>Agregacja tras i limity prefiksów

Firma Microsoft obsługuje konto too4000 prefiksy anonsowane toous za pośrednictwem hello Azure prywatnej komunikacji równorzędnej. To może być zwiększana się too10, 000 prefiksy, jeśli włączono hello dodatek usługi ExpressRoute w warstwie premium. Możemy zaakceptować prefiksy too200 sesji BGP dla publicznej platformy Azure i komunikacji równorzędnej firmy Microsoft. 

sesję protokołu BGP Hello zostanie porzucony, jeśli hello liczby prefiksów przekracza hello limit. Firma Microsoft będzie akceptować trasy domyślne łącze hello prywatnej komunikacji równorzędnej tylko. Dostawcy należy odfiltrować trasy domyślnej i prywatnych adresów IP (RFC 1918) z hello Azure publicznego i ścieżki komunikacji równorzędnej firmy Microsoft. 

## <a name="transit-routing-and-cross-region-routing"></a>Routing tranzytowy i routing obejmujący wiele regionów

Usługi ExpressRoute nie można skonfigurować jako routera tranzytowego. Użytkownik ma toorely dostawcą połączenia dla usługi routingu tranzytowego.

## <a name="advertising-default-routes"></a>Anonsowanie tras domyślnych

Trasy domyślne są dozwolone tylko w sesjach prywatnej komunikacji równorzędnej Azure. W takim przypadku firma Microsoft będzie kierować cały ruch z sieci tooyour skojarzone sieci wirtualne hello. Anonsowanie trasy domyślnej w prywatnej komunikacji równorzędnej spowoduje hello internet ścieżki z blokowany jest dostęp do platformy Azure. Muszą polegać na krawędzi firmowej tooroute ruchu z i toohello internet dla usługi hostowanej na platformie Azure. 

 tooenable łączności tooother Azure usługi i usługi infrastruktury, należy się upewnić, jeden z poniższych elementach hello jest w miejscu:

* Azure publicznej komunikacji równorzędnej jest punkty końcowe toopublic ruchu tooroute włączone
* Korzystając z połączenia internetowego tooallow tras zdefiniowanych przez użytkownika dla każdej podsieci wymaga łączności z Internetem.

> [!NOTE]
> Anonsowanie tras domyślnych spowoduje awarię aktywacji licencji maszyn wirtualnych systemu Windows i innych systemów. Postępuj zgodnie z instrukcjami [tutaj](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork obejścia tego problemu.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>Obsługa protokołu BGP społeczności (wersja zapoznawcza)

W tej sekcji przedstawiono sposób korzystania z protokołu BGP społeczności w usłudze ExpressRoute. Microsoft anonsuje trasy w hello publicznego i ścieżki komunikacji równorzędnej firmy Microsoft z społeczności odpowiednie wartości trasy. Witaj uzasadnienie w ten sposób i hello szczegóły dotyczące społeczności, które wartości są opisane poniżej. Microsoft, jednak nie zachowa do dowolnej społeczności tooMicrosoft anonsowane tooroutes oznakowanych wartości.

Jeśli jest nawiązywane za pośrednictwem usługi ExpressRoute w jednym miejscu komunikacji równorzędnej w obrębie regionu geograficznymi tooMicrosoft, konieczne będzie dostęp do usługi w chmurze Microsoft tooall we wszystkich regionach w obrębie granicy geograficznymi hello. 

Na przykład jeśli tooMicrosoft w Amsterdamie są połączone za pośrednictwem usługi ExpressRoute, konieczne będzie dostępu tooall usług chmurowych firmy Microsoft w Europa Północna, Europa i Europa Zachodnia. 

Zobacz toohello [ExpressRoute partnerów i lokalizacje komunikacji równorzędnej](expressroute-locations.md) strony szczegółową listę regionów geograficznymi, skojarzone regiony platformy Azure i odpowiednie ExpressRoute równorzędna lokalizacji.

Możesz kupić więcej niż jeden obwód usługi ExpressRoute na region geopolityczny. O wiele połączeń oferuje istotne korzyści w wysokiej dostępności z powodu nadmiarowość toogeo. W przypadkach, w którym znajduje się wiele obwody usługi ExpressRoute otrzymasz hello tego samego zestawu prefiksy anonsowane firmy Microsoft na powitania publicznej komunikacji równorzędnej i Microsoft równorzędna ścieżki. Oznacza to, że będziesz mieć wiele ścieżek ze swojej sieci do firmy Microsoft. Może to powodować nieoptymalnych toobe decyzje dotyczące routingu w sieci. W związku z tym mogą wystąpić usług toodifferent środowiska nieoptymalnych łączności. 

Microsoft będzie oznaczać prefiksów anonsowanych za pośrednictwem publicznej komunikacji równorzędnej i Microsoft komunikację równorzędną za odpowiednie wartości społeczności BGP wskazujący hello region hello prefiksy znajdują się w. Może polegać na powitania społeczności wartości toomake odpowiedniego routingu decyzje toooffer [optymalną routingu toocustomers](expressroute-optimize-routing.md).

| **Region geopolityczny** | **Region platformy Microsoft Azure** | **Wartość społeczności BGP** |
| --- | --- | --- |
| **Ameryka Północna** | | |
| Wschodnie stany USA |12076:51004 | |
| Wschodnie stany USA 2 |12076:51005 | |
| Zachodnie stany USA |12076:51006 | |
| Zachodnie stany USA 2 |12076:51026 | |
| Środkowo-zachodnie stany USA |12076:51027 | |
| Środkowo-północne stany USA |12076:51007 | |
| Środkowo-południowe stany USA |12076:51008 | |
| Środkowe stany USA |12076:51009 | |
| Kanada Środkowa |12076:51020 | |
| Kanada Wschodnia |12076:51021 | |
| **Ameryka Południowa** | | |
| Brazylia Południowa |12076:51014 | |
| **Europa** | | |
| Europa Północna |12076:51003 | |
| Europa Zachodnia |12076:51002 | |
| **Azja i Pacyfik** | | |
| Azja Wschodnia |12076:51010 | |
| Azja Południowo-Wschodnia |12076:51011 | |
| **Japonia** | | |
| Japonia Wschodnia |12076:51012 | |
| Japonia Zachodnia |12076:51013 | |
| **Australia** | | |
| Australia Wschodnia |12076:51015 | |
| Australia Południowo-Wschodnia |12076:51016 | |
| **Indie** | | |
| Indie Południowe |12076:51019 | |
| Indie Zachodnie |12076:51018 | |
| Indie Środkowe |12076:51017 | |

Wszystkie trasy anonsowane firmy Microsoft zostaną oznaczone hello społeczności odpowiednią wartość. 

> [!IMPORTANT]
> Globalne prefiksy zostaną oznaczone odpowiednią wartością społeczności i będą anonsowane tylko po włączeniu dodatku Premium usługi ExpressRoute.
> 
> 

Ponadto toohello powyżej, Microsoft będzie również tagu prefiksy opartego na usłudze hello, do których należą. Dotyczy to tylko toohello komunikacji równorzędnej firmy Microsoft. w poniższej tabeli Hello udostępnia mapowanie wartości Wspólnoty tooBGP usługi.

| **Usługa** | **Wartość społeczności BGP** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **Skype dla firm** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **Inne usługi Office 365** |12076:5100 |

> [!NOTE]
> Microsoft honoruje wartości społeczności BGP ustawionych na powitania trasy anonsowane tooMicrosoft.
> 
> 

## <a name="next-steps"></a>Następne kroki

* Skonfiguruj połączenie usługi ExpressRoute.
  
  * [Utworzyć obwodu usługi ExpressRoute dla hello klasycznego modelu wdrażania](expressroute-howto-circuit-classic.md) lub [tworzenia i modyfikowania obwodu usługi expressroute, za pomocą usługi Azure Resource Manager](expressroute-howto-circuit-arm.md)
  * [Konfigurowanie routingu dla hello klasycznego modelu wdrażania](expressroute-howto-routing-classic.md) lub [Konfigurowanie routingu dla modelu wdrażania usługi Resource Manager hello](expressroute-howto-routing-arm.md)
  * [Link klasycznego tooan sieci wirtualnej obwodu ExpressRoute](expressroute-howto-linkvnet-classic.md) lub [Link tooan Menedżera zasobów w sieci wirtualnej obwodu usługi expressroute](expressroute-howto-linkvnet-arm.md)

