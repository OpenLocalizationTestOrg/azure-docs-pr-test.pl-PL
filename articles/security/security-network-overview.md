---
title: "aaaNetwork pojęcia dotyczące zabezpieczeń i wymagania dotyczące platformy Azure | Dokumentacja firmy Microsoft"
description: " Ten artykuł ułatwia toounderstand należy co Microsoft Azure ma toooffer w obszarze hello zabezpieczeń sieci. Firma Microsoft udostępnia podstawowe wyjaśnienia dotyczące pojęcia dotyczące zabezpieczeń sieci podstawowej i wymagania i informacje, jakie Azure ma toooffer w każdym z tych obszarów. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Przegląd zabezpieczeń sieci platformy Azure
Microsoft Azure obejmuje niezawodne toosupport infrastruktury sieci, aplikacji i wymaganiami dotyczącymi łączności usługi. Łączność sieciowa będzie możliwe między zasobami znajdującymi się na platformie Azure, między lokalnymi i Azure hostowanej zasobów oraz tooand z hello Internet i Azure.

Witaj celem tego artykułu jest toomake go toounderstand można łatwiej co Microsoft Azure ma toooffer w obszarze hello zabezpieczeń sieci. W tym miejscu udostępniamy wyjaśnienia podstawowe pojęcia dotyczące zabezpieczeń sieci podstawowej i wymagań. Firma Microsoft udostępnia również informacji jakie Azure ma toooffer w każdym z tych obszarów, a także łączy toohelp uzyskania lepiej zrozumieć interesujące obszary.

W tym artykule Przegląd zabezpieczeń sieci Azure koncentruje się na powitania w następujących obszarach:

* Sieć platformy Azure
* Kontrola dostępu do sieci
* Bezpiecznego połączenia zdalnego dostępu i między lokalizacjami
* Dostępność
* Rozpoznawanie nazw
* Architektura DMZ
* Monitorowanie i wykrywania zagrożeń


## <a name="azure-networking"></a>Sieci systemu Azure
Maszyny wirtualne muszą łączność sieciową. toosupport tego wymogu Azure wymaga toobe maszyny wirtualne podłączone tooan sieci wirtualnej platformy Azure. Sieci wirtualnej platformy Azure jest konstrukcją logiczną, rozszerzający hello fizycznej Azure sieci szkieletowej. Każdy logicznej sieci wirtualnej platformy Azure jest odizolowana od wszystkich innych sieciach wirtualnych platformy Azure. Dzięki temu można mieć pewność, że ruch sieciowy we wdrożeniach nie jest dostępny tooother klientów Microsoft Azure.

Więcej informacji:

* [Omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>Kontrola dostępu do sieci
Kontrola dostępu do sieci polega hello ograniczanie tooand łączności z określonymi urządzeniami lub podsieci w sieci wirtualnej platformy Azure. Celem Hello kontroli dostępu do sieci jest maszyn wirtualnych tooyour dostępu toolimit i usług tooapproved użytkowników i urządzeń. Kontroli dostępu są oparte na akceptować lub odrzucać decyzje dotyczące tooand połączeń z maszyny wirtualnej lub usługi.

Azure obsługuje kilka typów kontroli dostępu do sieci, takich jak:

* Kontrola warstwy sieci
* Trasy kontroli oraz wymuszonego tunelowania
* Urządzenia zabezpieczeń sieci wirtualnej

### <a name="network-layer-control"></a>Kontrola warstwy sieci
Wszystkie wdrożenia bezpiecznego wymaga niektóre miary kontroli dostępu do sieci. Celem Hello kontroli dostępu do sieci jest toorestrict maszyny wirtualnej komunikacji toohello niezbędnych systemów i że inne próby komunikacji są blokowane.

Jeśli potrzebujesz kontroli dostępu na poziomie sieci podstawowej (na podstawie adresu IP i hello TCP lub UDP protokołów), można użyć grup zabezpieczeń sieci. Grupy zabezpieczeń sieci (NSG) jest filtrowanie Zapora podstawowa pakietów stanowe i umożliwia toocontrol dostępu na podstawie [5-elementowej](https://www.techopedia.com/definition/28190/5-tuple). Grupy NSG nie udostępniają kontroli warstwy aplikacji lub uwierzytelnionego kontroli dostępu.

Więcej informacji:

* [Grupy zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>Formant trasy i wymuszanie tunelowania
Hello możliwości toocontrol routingu w sieci wirtualnej platformy Azure jest możliwości kontroli dostępu i zabezpieczeń sieci w krytycznych. Routing jest niepoprawnie skonfigurowana, aplikacji i usług hostowanych na maszynie wirtualnej może połączyć z toounauthorized urządzeń, takich jak systemy i jest przez potencjalnymi atakami.

Sieć platformy Azure obsługuje zachowania routingu hello toocustomize możliwości hello ruchu w sieci dla sieci wirtualne platformy Azure. Dzięki temu tooalter hello domyślne pozycje tabeli routingu w sieci wirtualnej platformy Azure. Kontroli zachowania routingu pomaga upewnij się, że cały ruch z niektórych urządzeń lub grupy urządzeń wprowadza lub pozostawia sieci wirtualnej do określonej lokalizacji.

Na przykład może być urządzenie zabezpieczeń sieci wirtualnych w sieci wirtualnej platformy Azure. Chcesz, aby się upewnić, że wszystkie tooand ruch z sieci wirtualnej Azure przechodzi przez tego urządzenia wirtualnego zabezpieczeń toomake. Można to zrobić przez skonfigurowanie [trasy zdefiniowane przez użytkownika](../virtual-network/virtual-networks-udr-overview.md) na platformie Azure.

[Wymuszone tunelowanie](https://www.petri.com/azure-forced-tunneling) jest mechanizm służy tooensure, że usługi nie są dozwolone tooinitiate toodevices połączenia na powitania Internet. Należy pamiętać, że jest inny niż przyjmowanie połączeń przychodzących, a następnie odpowiada toothem. Serwery frontonu sieci web muszą toorequests toorespond z hostami w Internecie, a więc powierzając jej ich konserwację Internet ruch jest dozwolony dla ruchu przychodzącego toothese serwerów sieci web i serwery sieci web hello są dozwolone toorespond.

Co chcesz tooallow jest tooinitiate serwera frontonu sieci web żądania wychodzącego. Takich żądań może reprezentować zagrożenie bezpieczeństwa, ponieważ te połączenia może być używane toodownload złośliwego oprogramowania. Nawet wtedy, gdy mają one frontonu toohello Internet żądań wychodzących tooinitiate serwerów, może być tooforce ich toogo za pośrednictwem lokalnej sieci web serwerów proxy, dzięki czemu możesz korzystać z adresu URL filtrowanie i rejestrowanie.

Zamiast tego czy chcesz toouse wymuszonego tunelowania tooprevent to. Włączenie tunelowania wymuszonego wszystkich toohello połączenia internetowe są wymuszone za pośrednictwem bramy sieci lokalnej. Można skonfigurować wymuszanie tunelowania dzięki wykorzystaniu trasy zdefiniowane przez użytkownika.

Więcej informacji:

* [Co to są trasy zdefiniowane przez użytkownika i przesyłania dalej IP](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>Urządzenia zabezpieczeń sieci wirtualnej
Gdy grup zabezpieczeń sieci, trasy zdefiniowane przez użytkownika i wymuszanie tunelowania zapewniają poziom zabezpieczeń na poziomie warstwy sieci i transportu hello hello [OSI model](https://en.wikipedia.org/wiki/OSI_model), czasami, kiedy zechcesz tooenable zabezpieczeń na wyższych poziomach niż hello sieci.

Na przykład wymagań dotyczących zabezpieczeń mogą być następujące:

* Uwierzytelnianie i autoryzacja przed zezwoleniem na dostęp do aplikacji tooyour
* Wykrywania nieautoryzowanego dostępu i odpowiedzi nieautoryzowanego dostępu
* Kontrolę warstwy aplikacji protokołów wysokiego poziomu
* Filtrowanie adresów URL
* Oprogramowanie antywirusowe poziomu sieci i ochrony przed złośliwym oprogramowaniem
* Ochrona przed bot
* Kontrola dostępu aplikacji
* Dodatkowa ochrona przed atakami DDoS (powyżej hello ochrony przed atakami DDoS hello Azure sieci szkieletowej, sam)

Te funkcje zabezpieczeń rozszerzonych sieci mogą korzystać za pomocą rozwiązania Azure partnera. Można znaleźć hello najbardziej aktualne Azure partnerskich rozwiązań zabezpieczeń sieci, przechodząc na stronę hello [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/) i wyszukując "zabezpieczenia" i "zabezpieczenia sieciowe".

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>Bezpieczny dostęp zdalny i łączność między różnymi lokalizacjami
Instalacji, konfiguracji i zarządzania zasobami Azure musi toobe wykonywane zdalnie. Ponadto możesz toodeploy [hybrydowego IT](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) rozwiązania, które ma składniki lokalnej i w chmurze publicznej Azure hello. Te scenariusze wymaga bezpiecznego dostępu zdalnego.

Sieć platformy Azure obsługuje następujące scenariusze bezpieczny dostęp zdalny hello:

* Połącz tooan poszczególnych stacji roboczych sieci wirtualnej platformy Azure
* Połącz z tooan sieci lokalnej sieci wirtualnej platformy Azure z sieci VPN
* Połączenie z tooan sieci lokalnej sieci wirtualnej platformy Azure z dedykowanych łącza sieci WAN
* Połączyć sieci wirtualnych Azure tooeach innych

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>Połącz tooan poszczególnych stacji roboczych sieci wirtualnej platformy Azure
Może to być godziny zużycia tooenable poszczególnych deweloperów i operacji personelu toomanage maszyn wirtualnych i usług Azure. Na przykład konieczne dostępu tooa maszyny wirtualnej w sieci wirtualnej platformy Azure i zasady zabezpieczeń nie zezwala RDP lub SSH dostępu zdalnego tooindividual maszyn wirtualnych. W takim przypadku można użyć połączenia sieci VPN punkt lokacja.

Witaj punkt lokacja połączenie VPN używa hello [sieć VPN SSTP](https://technet.microsoft.com/library/cc731352.aspx) tooenable protokołu tooset prywatne i bezpiecznego połączenia między użytkownikiem hello a hello sieci wirtualnej platformy Azure. Po ustanowieniu połączenia sieci VPN hello hello użytkownicy będą mogli tooRDP lub SSH za pośrednictwem sieci VPN hello link do żadnej maszyny wirtualnej na powitania sieci wirtualnej platformy Azure (przy założeniu, że hello użytkownika mogą uwierzytelniać i daje uprawnienia).

Więcej informacji:

* [Skonfiguruj tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu programu PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>Tooan siecią lokalną sieć wirtualna Azure Uzyskuj dostęp do sieci VPN
Możesz tooconnect całej sieci firmowej, lub w części, tooan sieci wirtualnej platformy Azure. To jest typowe w przypadku hybrydowych IT scenariusze gdzie firmy [rozszerzenie ich lokalnych centrów danych na platformie Azure](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84). W wielu przypadkach firmy będą hosta usługi w programie Azure i w częściach lokalnymi, np. gdy rozwiązanie zawiera serwerów frontonu sieci web w Azure i bazy danych zaplecza lokalnie. Typy połączeń "między lokalizacjami" Upewnij się również zarządzania Azure znajduje się zasoby bardziej bezpieczny i włączyć scenariuszy, takich jak rozszerzanie kontrolerów domeny usługi Active Directory na platformie Azure.

Jednym ze sposobów tooaccomplish jest toouse [sieci VPN typu lokacja lokacja](https://www.techopedia.com/definition/30747/site-to-site-vpn). Różnica Hello VPN lokacja lokacja i sieć VPN punkt lokacja jest VPN punkt lokacja łączy tooan pojedyncze urządzenie sieci wirtualnej platformy Azure, gdy sieć VPN lokacja lokacja łączy tooan całej sieci (na przykład sieci lokalnej) sieci wirtualnej platformy Azure . Tooan sieci VPN typu lokacja lokacja sieci wirtualnej platformy Azure, użyj hello bardzo bezpieczny tunel tryb VPN protokołu IPsec.

Więcej informacji:

* [Tworzenie sieci wirtualnej Resource Manager się przez połączenie VPN lokacja lokacja za pomocą hello portalu Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Planowanie i projektowanie bramy sieci VPN](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>Uzyskuj tooan z sieci lokalnej sieci wirtualnej platformy Azure w wersji dedykowanej łącza sieci WAN
Połączenia VPN punkt lokacja i lokacja lokacja obowiązują umożliwiających łączności między lokalizacjami. Jednak niektóre organizacje wziąć pod uwagę ich hello toohave następujące wady:

* Połączenia sieci VPN przenoszenia danych za pośrednictwem Internetu hello — to przedstawia tych połączeń toopotential problemy z zabezpieczeniami dotyczące przenoszenia danych za pośrednictwem publicznej sieci. Ponadto nie można zagwarantować niezawodność i dostępność dla połączenia z Internetem.
* TooAzure połączenia sieci VPN między sieciami wirtualnymi można uznać się, że przepustowość jest ograniczona do niektóre aplikacje i celów, w miarę ich maksymalny limit na około 200 MB/s.

Organizacje, które muszą zwykle hello najwyższy poziom bezpieczeństwa i dostępności do ustanawiania połączeń między różnymi lokalizacjami Użyj dedykowanego łącza sieci WAN tooconnect tooremote witryny. Azure oferuje hello toouse możliwości dedykowane łącza sieci WAN, których można używać tooconnect Twojego tooan sieci lokalnej sieci wirtualnej platformy Azure. Ta opcja jest włączona za pomocą usługi Azure ExpressRoute.

Więcej informacji:

* [Opis techniczny ExpressRoute](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>Połączyć sieci wirtualnych Azure tooEach innych
Istnieje możliwość, że możesz toouse wiele sieci wirtualnych Azure wdrożeń. Istnieje wiele przyczyn, dlaczego można to zrobić. Jednym z powodów hello może być toosimplify zarządzania; inny może być ze względów bezpieczeństwa. Niezależnie od tego, czy motywacją hello lub uzasadnienie umieszczanie zasobów w różnych sieciach wirtualnych platformy Azure może być godziny zużycia zasobów na każdym hello sieci tooconnect ze sobą.

Jedną z opcji byłoby dla usług na jeden tooservices tooconnect sieci wirtualnej platformy Azure w innej sieci wirtualnej platformy Azure "pętli ponownie" za pośrednictwem hello Internet. połączenia Hello czy uruchomić na jedną sieć wirtualną platformy Azure, przejdź za pośrednictwem Internetu hello i następnie wrócić toohello docelowej sieci wirtualnej platformy Azure. Ta opcja udostępnia hello połączenia toohello zabezpieczeń problemy związane tooany komunikacji z Internetem.

Lepszym rozwiązaniem może być toocreate Azure wirtualnego VPN lokacja lokacja sieci wirtualnej sieci do platformy Azure. Tej sieci wirtualnej Azure wirtualnej sieci do Azure, sieci VPN typu lokacja lokacja używa hello sam [trybu tunelowania IPsec](https://technet.microsoft.com/library/cc786385.aspx) protokołem hello między lokalizacjami lokacja lokacja połączenia sieci VPN wymienionych powyżej.

Zaletą Hello Azure wirtualnej VPN lokacja lokacja sieci wirtualnej sieci do platformy Azure jest, że za pośrednictwem hello Azure sieci szkieletowej, a nie połączenie za pośrednictwem Internetu hello ustanowieniu połączenia sieci VPN hello. To zapewnia dodatkową warstwę zabezpieczeń można porównać toosite-to-site VPN, łączących się za pośrednictwem Internetu hello.

Więcej informacji:

* [Konfigurowanie połączenia do wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Dostępność
Dostępność jest kluczowym składnikiem programu zabezpieczeń. Jeśli nie jakie one dostępu użytkowników i systemów muszą tooaccess za pośrednictwem hello sieci, hello usługi mogą być uważane za naruszenia zabezpieczeń. Platforma Azure ma technologie sieciowe tego hello pomocy technicznej następujące mechanizmy wysokiej dostępności:

* Równoważenie obciążenia oparte na protokole HTTP
* Równoważenie obciążenia poziomu sieci
* Globalnego równoważenia obciążenia

Równoważenie obciążenia jest tooequally mechanizmu zaprojektowane dystrybucji połączeń między wieloma urządzeniami. cele Hello Równoważenie obciążenia sieciowego są:

* Zwiększ dostępność — podczas ładowania saldo połączenia między wieloma urządzeniami, co najmniej jedno z urządzeń hello może stać się niedostępne i hello usługi działające na powitania pozostałych urządzeń online można kontynuować tooserve hello zawartość z usługi hello
* Zwiększyć wydajność — podczas ładowania saldo połączeń na wielu urządzeniach, pojedyncze urządzenie nie ma procesora hello tootake trafień. Zamiast tego hello pamięci i przetwarzania żądania dotyczące dostarczania zawartości hello zostanie rozmieszczona na wielu urządzeniach.

### <a name="http-based-load-balancing"></a>Równoważenie obciążenia oparte na protokole HTTP
Organizacje, czy działa usług sieci web często toohave dążenie do modułu równoważenia obciążenia opartą na protokole HTTP przed tych toohelp usług sieci web ułatwieniu zapewnienia odpowiednich poziomów wydajności i wysokiej dostępności. Z kolei tootraditional sieciowej usługi równoważenia obciążenia, hello równoważenia obciążenia decyzje na przez usługi równoważenia obciążenia oparty na protokole HTTP są oparte na właściwości protokołu hello HTTP, nie na powitania protokołami warstwy transportu i sieci.

tooprovide możesz oparte na protokole HTTP równoważenia obciążenia dla usług opartych na sieci web, platforma Azure udostępnia hello Azure Application Gateway. Hello Azure Application Gateway obsługuje:

* Oparte na protokole HTTP Równoważenie obciążenia — decyzje równoważenia obciążenia są wykonywane na podstawie protokołu charakterystyczny toohello specjalne HTTP
* Koligacji na podstawie plików cookie sesji — ta funkcja sprawdza, czy nawiązywane połączenia tooone serwery hello za ten moduł równoważenia obciążenia pozostaje niezmieniona między powitania klienta i serwera. Dzięki temu stabilności transakcji.
* Odciążanie protokołu SSL — gdy klienta nawiązaniu połączenia z modułem równoważenia obciążenia hello, że sesja między powitania klienta i usługi równoważenia obciążenia hello jest szyfrowana przy użyciu hello HTTPS (SSL /) protokołu. Jednak w kolejności tooincrease wydajności, masz hello opcja toohave hello połączenie między hello modułu równoważenia obciążenia i serwer sieci web hello za protokół HTTP (bez szyfrowania) hello Użyj hello równoważenia obciążenia. Jest określony tooas "odciążanie protokołu SSL", ponieważ serwerów sieci web hello za usługą równoważenia obciążenia hello nie występują hello procesora koszty związane z szyfrowaniem i dlatego powinien być szybciej tooservice stanie żądania.
* Adres URL routingu opartego na protokole zawartości — ta funkcja umożliwia decyzji dotyczących toomake usługi równoważenia obciążenia hello na którym tooforward połączenia na podstawie hello docelowego adresu URL. Zapewnia to znacznie większą elastyczność niż rozwiązania, które należy załadować równoważenia decyzje na podstawie adresów IP.

Więcej informacji:

* [Omówienie bramy aplikacji](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>Równoważenie obciążenia poziomu sieci
Z kolei na podstawie tooHTTP równoważenia obciążenia, równoważenia obciążenia poziomu sieci sprawia, że obciążenia równoważenia decyzje oparte na adres i port (TCP lub UDP) numery IP.
Aby uzyskać hello zalet poziomu równoważenia obciążenia sieciowego w Azure przy użyciu hello moduł równoważenia obciążenia Azure. Niektóre właściwości klucza hello modułu równoważenia obciążenia Azure obejmują:

* Równoważenie obciążenia poziomu oparte na numery adres i port IP
* Obsługa protokołu warstwy żadnych aplikacji
* Maszyny wirtualne tooAzure równoważy obciążenie i wystąpień roli usług w chmurze
* Można użyć zarówno internetowy (zewnętrzne Równoważenie obciążenia sieciowego), jak i z systemem innym niż Internet skierowane w aplikacji (równoważenia obciążenia wewnętrznego) i maszyny wirtualne
* Punkt końcowy monitorowania, które jest używane toodetermine w przypadku usług hello za usługą równoważenia obciążenia hello stały się niedostępne

Więcej informacji:

* [Moduł równoważenia obciążenia nakierowany na Internet między maszynami wirtualnymi lub usługami](../load-balancer/load-balancer-internet-overview.md)
* [Omówienie usługi równoważenia obciążenia wewnętrznego](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>Globalnego równoważenia obciążenia
Niektóre organizacje będzie możliwe hello najwyższy poziom dostępności. Jednym ze sposobów tooreach, ten cel jest globalnie toohost aplikacji w rozproszonych centrów danych. Kiedy aplikacji znajduje się w centrach danych znajdujących się na Witaj świecie, jest możliwe toobecome całego regionu geograficznymi niedostępne i nadal mieć aplikacji hello i działa.

Ponadto toohello dostępności korzyści, jakie można uzyskać za pomocą obsługi aplikacji w rozproszonych globalnie centrach danych, również można uzyskać zwiększenia wydajności. Te korzyści wydajności można uzyskać za pomocą mechanizmu, który kieruje żądania hello usługi toohello datacenter, który najbliższego urządzenia toohello, do której wysłano żądanie hello.

Równoważenie obciążenia globalny może umożliwić obu tych korzyści. Na platformie Azure Aby uzyskać hello zalet globalnego równoważenia obciążenia za pomocą usługi Azure Traffic Manager.

Więcej informacji:

* [Co to jest usługa Traffic Manager?](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>Rozpoznawanie nazw
Rozpoznawanie nazw jest funkcją krytyczne dla wszystkich usług, które są hostowane na platformie Azure. Z punktu widzenia zabezpieczeń naruszenia funkcja rozpoznawania nazw hello może prowadzić tooan atakująca przekierowania żądania z witryny atakująca tooan witryny. Rozpoznawanie nazw bezpiecznego jest wymagane dla wszystkich usług w chmurze hostowanej.

Istnieją dwa typy rozpoznawania nazw potrzebne tooaddress:

* Rozpoznawania nazw wewnętrznych — rozpoznawania nazw wewnętrznych jest używany przez usługi w sieci wirtualne platformy Azure i/lub sieci lokalnej. Nazwy używane do rozpoznawania nazw wewnętrznych nie są dostępne za pośrednictwem hello Internet. Optymalne zabezpieczeń jest ważne, czy schematem rozpoznawania nazw wewnętrznych nie jest dostępny tooexternal użytkowników.
* Rozpoznawanie nazw zewnętrznych — rozpoznawanie nazw zewnętrznych jest używany przez osoby i urządzenia poza sieci lokalnej i sieci wirtualnych Azure. Są to nazwy hello, które są widoczne toohello internetowych i używanych toodirect połączenia tooyour usług w chmurze.

Do rozpoznawania nazw wewnętrznych dostępne są dwie opcje:

* Serwer DNS sieci wirtualnej platformy Azure — podczas tworzenia nowej sieci wirtualnej Azure, serwer DNS jest tworzony automatycznie. Ten serwer DNS może rozpoznawać nazwy hello maszyn hello znajdujących się w tej sieci wirtualnej platformy Azure. Ten serwer DNS nie jest konfigurowalne i jest zarządzany przez Menedżera sieci szkieletowej Azure hello, co czyni go rozwiązania rozpoznawania nazwy bezpieczne.
* Przełącz serwer DNS — dostępna opcja hello umieszczenie serwera DNS wybranej przez użytkownika w sieci wirtualnej platformy Azure. Ten serwer DNS może być zintegrowane usługi Active Directory, serwer DNS lub dedykowane rozwiązania serwera DNS podany przez partnera Azure, który można uzyskać z hello Azure Marketplace.

Więcej informacji:

* [Omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md)
* [Zarządzanie serwerami DNS używanymi przez sieć wirtualną (VNet)](../virtual-network/virtual-network-manage-network.md#dns-servers)

Dla zewnętrznych rozpoznawanie nazw DNS dostępne są dwie opcje:

* Host własne zewnętrznych DNS serwera lokalnego
* Host własne zewnętrznego serwera DNS z dostawcą usług

W wielu organizacjach dużych będzie obsługiwać własne DNS serwerów lokalnych. Mogą one to robić, ponieważ mają one hello tak sieci wiedzę i toodo globalnego.

W większości przypadków jest lepsze toohost usług programu rozpoznawania nazw DNS z dostawcą usług. Ci dostawcy usług mają hello doświadczenia z sieci i globalnego tooensure bardzo wysoka dostępność dla Twojej usługi rozpoznawania nazw. Dostępność jest niezbędne, usług DNS, ponieważ jeśli programu rozpoznawania nazw usług kończyć się niepowodzeniem, nie będą się mogli tooreach Twojego internetowy usług.

Azure zapewnia wysoką dostępność i wydajność zewnętrznych DNS rozwiązanie w formie hello Azure DNS. To rozwiązanie rozpoznawania nazw zewnętrznych wykorzystuje hello na całym świecie infrastruktury usługi Azure DNS. Umożliwia toohost domeny za pomocą usługi Azure hello tego samego poświadczeń, interfejsy API, narzędzia i rozliczeń jak innymi usługami Azure. W ramach platformy Azure również dziedziczy hello silne zabezpieczenie formantów wbudowanych w platformy hello.

Więcej informacji:

* [Omówienie usługi Azure DNS](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>Architektura DMZ
W wielu organizacjach enterprise Użyj toosegment sieci DMZ ich strefę buforu toocreate sieci między hello Internet i swoich usług. część sieci hello w strefie DMZ Hello jest uznawany za strefy niskim poziomie zabezpieczeń i nie zasoby wysokiej wartości są umieszczane w tym segmencie sieci. Zwykle zobaczysz urządzeniach zabezpieczeń sieciowych z karty sieciowej na segment hello DMZ i innej sieci interfejsu tooa połączonych sieci maszyn wirtualnych i usług, które akceptują połączenia przychodzące z Internetu hello.

Istnieje wiele zmian projektu DMZ i toodeploy decyzji hello strefą DMZ, a następnie jakiego rodzaju DMZ toouse decydując toouse, jest na podstawie wymagań dotyczących zabezpieczeń sieci.

Więcej informacji:

* [Usługi w chmurze firmy Microsoft i zabezpieczenia sieci](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>Monitorowanie i wykrywania zagrożeń

Platforma Azure oferuje możliwości toohelp można w tym obszarze klucza z wczesnym wykrywania, monitorowania i hello możliwości toocollect i przejrzyj ruchu sieciowego.

### <a name="azure-network-watcher"></a>Monitor sieci platformy Azure
Azure obserwatora sieciowego zawiera wiele funkcji, które pomóc w rozwiązywaniu problemów, a także zapewnić zupełnie nowy zestaw narzędzi tooassist hello identyfikacji problemów z zabezpieczeniami.

[Widok grupy zabezpieczeń ](/network-watcher/network-watcher-security-group-view-overview.md) ułatwia utrzymanie zgodności inspekcji i zabezpieczeń maszyn wirtualnych i mogą być używane tooperform programowe inspekcje porównanie hello linie bazowe zasady zdefiniowane przez organizacji tooeffective reguł dla poszczególnych maszyn wirtualnych. Może to pomóc w identyfikacji dowolnego odejście konfiguracji.

[Przechwytywania pakietów](/network-watcher/network-watcher-packet-capture-overview.md) pozwala tooand ruchu sieciowego toocapture z hello maszyny wirtualnej. Oprócz myśl zezwalając statystyk sieciowych toocollect i hello rozwiązywania problemów z aplikacji przechwytywania pakietów problemów może być cenne w hello zbadanie wtargnięcia sieci. Możesz również tej funkcji można używać razem z usługi Azure Functions w odpowiedzi toospecific Azure przechwytywania ruchu sieciowego toostart alertów.

Aby uzyskać więcej informacji na obserwatora sieciowego Azure oraz jak toostart testowania niektórych funkcji hello w Twojej labs Spójrz na powitania [obserwatora sieciowego Azure monitorowania — omówienie](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Azure obserwatora sieciowego jest wciąż w publicznej wersji zapoznawczej, nie może mieć hello sam poziom dostępności i niezawodności jako usługi, które są zwykle wersji dostępności. Niektóre funkcje mogą nie być obsługiwane, mogą mieć ograniczone możliwości i mogą nie być dostępne we wszystkich lokalizacjach Azure. Najbardziej aktualne powiadomień hello na dostępność i stan tej usługi, sprawdź hello [strony aktualizacji platformy Azure](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Azure Security Center
Centrum zabezpieczeń pomaga zapobiec, wykrywania i reagowania toothreats i zapewnia zwiększyć widoczność i kontrolę nad, hello zabezpieczeń zasobów platformy Azure. Zapewnia zabezpieczenia zintegrowane monitorowanie i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które mogłyby w przeciwnym razie pozostać niezauważone, a także współpracuje z dużym zestawem rozwiązań zabezpieczających.

Centrum zabezpieczeń Azure ułatwia optymalizacji i monitorować przez zabezpieczenia sieci:

* Udostępnia zalecenia dotyczące zabezpieczeń sieci
* Monitorowanie stanu hello konfiguracji zabezpieczeń sieci
* Alerty na podstawie toonetwork zagrożenia obu poziomach hello punktu końcowego i sieci

Więcej informacji:

* [Wprowadzenie tooAzure Centrum zabezpieczeń](../security-center/security-center-intro.md)


### <a name="logging"></a>Rejestrowanie
Rejestrowanie na poziomie sieci jest funkcją klucza w żadnym scenariuszu zabezpieczeń sieci. Na platformie Azure możesz zalogować się informacjami uzyskanymi na poziomie sieci tooget grup zabezpieczeń sieci rejestrowania informacji. Z rejestrowaniem grupy NSG można uzyskać informacji o:

* [Dzienniki aktywności](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) — te dzienniki są używane tooview wszystkie operacje przesłane tooyour Azure subskrypcji. Te dzienniki są domyślnie włączone i mogą być używane w hello portalu Azure. Zostały one wcześniej znana jako "Dzienników inspekcji" lub "Operacyjne dzienniki".
* Dzienniki zdarzeń — te dzienniki zawierają informacje dotyczące reguły NSG, jakie zostały zastosowane.
* Licznik dzienników — te dzienniki let wiadomo, ile razy każdej reguły NSG został zastosowany toodeny lub zezwolić na ruch.

Można również użyć [Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/), wizualizację danych zaawansowane narzędzia, tooview i analizować te dzienniki.

Więcej informacji:

* [Analizy dzienników dla grup zabezpieczeń sieci (NSG)](../virtual-network/virtual-network-nsg-manage-log.md)
