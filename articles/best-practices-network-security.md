---
title: "najlepsze rozwiązania zabezpieczeń sieci aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się niektóre hello najważniejsze funkcje dostępne w Azure toohelp utworzyć bezpiecznego środowiska sieci"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Chmury Microsoft bezpieczeństwa usług i sieci
Usługi w chmurze firmy Microsoft świadczenia usług hiperskali i infrastruktury, funkcje klasy korporacyjnej oraz wiele opcji na potrzeby łączności hybrydowej. Klienci mogą wybrać tooaccess tych usług za pośrednictwem Internetu hello lub z usługi Azure ExpressRoute, który zapewnia łączność w sieci prywatnej. Witaj platformy Microsoft Azure umożliwia klientom tooseamlessly rozszerzają infrastruktury do chmury hello i tworzenia wielu architektur. Ponadto stron trzecich można włączyć udoskonalone funkcje oferty usług zabezpieczeń oraz urządzenia wirtualnego. Ten dokument zawiera omówienie architektury problemów, które klientów należy wziąć pod uwagę podczas korzystania z usługi w chmurze firmy Microsoft dostępne za pośrednictwem usługi ExpressRoute i zabezpieczeń. Obejmuje ona również tworzenia bardziej bezpieczne usług w sieci wirtualnych platformy Azure.

## <a name="fast-start"></a>Szybki start
powitania po logiki wykresu można kierować możesz tooa określonych przykład hello wiele metody zabezpieczeń dostępne z hello platformy Azure. Dla wygody można znaleźć przykład Witaj, który najlepiej odpowiada Twoim przypadku. Rozwinięte wyjaśnień nadal odczytywania za pośrednictwem hello papieru.
[![0]][0]

[Przykład 1: Tworzenie sieci obwodowej (znanej także jako strefa DMZ, strefą zdemilitaryzowaną lub podsiecią ekranowaną) toohelp ochrona aplikacji przy użyciu grup zabezpieczeń sieci (NSG).](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[Przykład 2: Tworzenie obwodu toohelp sieci chronić aplikacje z zaporą i grup NSG.](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[Przykład 3: Tworzenie obwodu toohelp sieci ochrony sieci z zapory, trasy zdefiniowane przez użytkownika (przez) i grupy NSG.](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[Przykład 4: Dodaj połączenie hybrydowe z urządzenia do lokacji, wirtualne wirtualnej sieci prywatnej (VPN).](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[Przykład 5: Dodaj połączenie hybrydowe lokacja lokacja, Brama sieci VPN platformy Azure.](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[Przykład 6: Dodaj połączenie hybrydowe z usługi ExpressRoute.](#example-6-add-a-hybrid-connection-with-expressroute)</br>
Przykłady dodawania połączeń między sieciami wirtualnymi, wysokiej dostępności i łańcucha usługi zostanie dodany toothis dokumentu za pośrednictwem hello następnych kilku miesięcy.

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Ochrona zgodności i infrastruktury firmy Microsoft
organizacje toohelp wykonania national charakteru regionalnego, i branżowe regulujące hello zbierania i używania danych poszczególnych osób, firma Microsoft oferuje ponad 40 certyfikaty oraz poświadczenia. Witaj najbardziej kompleksowy zestaw dowolnego dostawcy usług w chmurze.

Aby uzyskać więcej informacji, zobacz informacje o zgodności hello na powitania [Microsoft Trust Center][TrustCenter].

Firma Microsoft udostępnia kompleksowe rozwiązanie tooprotect infrastrukturę potrzebną toorun hiperskali globalne usługi w chmurze. Infrastruktury chmury firmy Microsoft obejmuje sprzętu, oprogramowania, sieci i administracyjnych i operatorów, oprócz toohello fizycznych w centrach danych.

![2]

Takie podejście zapewnia bardziej bezpieczną podstawę dla klientów toodeploy usług w hello firmy Microsoft w chmurze. Witaj, następnym krokiem jest przeznaczony dla klientów toodesign i Utwórz tooprotect architektury zabezpieczeń tych usług.

## <a name="traditional-security-architectures-and-perimeter-networks"></a>Tradycyjne zabezpieczenia architektury i sieci obwodowej
Mimo że Microsoft intensywnie inwestuje w ochrona powitalnych infrastruktury chmury, klienci muszą również ochronę ich usługi w chmurze i grup zasobów. Toosecurity wielowarstwowe podejście zapewnia najlepszą ochronę hello. Strefy zabezpieczeń sieci obwodowej chroni wewnętrznych zasobów sieciowych z niezaufaną siecią. Sieć obwodowa odwołuje się krawędzie toohello lub części hello sieci, które znajdują się między hello Internet i enterprise hello chronione infrastruktury IT.

W sieciach typowego przedsiębiorstwa infrastrukturze podstawowej hello jest silnie wzmocnionego w granicach hello, z wielu warstw zabezpieczeń urządzeń. granic Hello każdej warstwy składa się z urządzeniami i punkty wymuszania zasad. Każda warstwa może zawierać kombinację powitania po urządzeń zabezpieczeń sieciowych: zapór, zapobiegania przeprowadzenie ataku typu "odmowa usługi" (DoS), wykrywania nieautoryzowanego dostępu lub systemy ochrony (Identyfikatory/IP) i urządzenia sieci VPN. Wymuszanie zasad może zająć formularza hello zasad zapory, listy kontroli dostępu (ACL) lub specyficznego routingu. Hello pierwszą linię obrony w sieci hello, bezpośrednio akceptować ruch przychodzący z hello Internetu, to kombinacja tych mechanizmów tooblock ataków i szkodliwy ruch umożliwiając dalsze uprawnionych żądań do hello sieci. Ten ruch trasy bezpośrednio tooresources w sieci obwodowej hello. Ten zasób może następnie "komunikować" tooresources więcej danych w sieci hello, przejeżdżających przez hello granic dalej do sprawdzania poprawności pierwszy. Warstwa peryferyjnych Hello jest nazywany hello sieci obwodowej, ponieważ ta część sieci hello jest narażonych toohello Internetu, zazwyczaj z jakiegoś ochrony po obu stronach. Hello poniższej ilustracji przedstawiono przykład sieci obwodowej pojedynczej podsieci w sieci firmowej, z dwóch granic zabezpieczeń.

![3]

Istnieje wiele tooimplement architektury używane sieci obwodowej. Te architektury można w zakresie od sieci obwodowej wieloma podsieciami tooa usługi równoważenia obciążenia proste zróżnicowane mechanizmów w każdej granicy tooblock ruchu i ochrony hello głębiej warstw hello sieci firmowej. Jak sieci obwodowej hello jest wbudowana zależy od hello specyficznych potrzeb organizacji hello i jego ogólnej tolerancji ryzyka.

Klienci przenieść ich obciążeń chmury toopublic, jest podobne możliwości toosupport krytyczne dla architektury sieci obwodowej zgodności Azure toomeet i wymagania dotyczące zabezpieczeń. Ten dokument zawiera wskazówki, w jaki sposób klienci mogą tworzyć środowisku bezpiecznej sieci na platformie Azure. Skupiono się w sieci obwodowej hello, ale również zawiera kompleksowe omówienie wiele aspektów zabezpieczeń sieci. Witaj następujące pytania o tej dyskusji:

* Jak można wbudować sieci obwodowej na platformie Azure
* Co to są sieci obwodowej hello hello Azure funkcje dostępne toobuild?
* Jak można chronić obciążeń zaplecza
* W jaki sposób obciążeń toohello komunikacji kontrolowane przez Internet na platformie Azure?
* Jak sieci lokalne powitania mogą być chronione od wdrożenia na platformie Azure?
* Podczas funkcje zabezpieczeń platformy Azure natywnego powinny być używane lub innych urządzeń lub usług?

powitania po diagram przedstawia różnych warstw zabezpieczeń, które platforma Azure udostępnia toocustomers. Te warstwy są natywne w hello samą platformą Azure i funkcje zdefiniowane przez klientów:

![4]

Przychodzące z hello Internet, DDoS Azure pomaga chronić przed atakami na dużą skalę przed Azure. Kolejna warstwa Hello jest zdefiniowany przez klienta publicznych adresów IP (punkty końcowe), które są używane toodetermine ruchu, które można przekazać za pośrednictwem sieci wirtualnej usługi toohello hello chmury. Azure macierzystego wirtualnego izolacji sieci zapewnia pełnej izolacji od innych sieci i czy ruch przepływa tylko za pośrednictwem ścieżki użytkownika skonfigurowane i. Tych ścieżek i metody są hello kolejnej warstwy, których grup NSG, przez i wirtualnych urządzeń sieciowych mogą być używane toocreate zabezpieczeń granice tooprotect hello wdrożenia aplikacji w sieci hello chronione.

Witaj Następna sekcja zawiera omówienie sieci wirtualnych platformy Azure. Te sieci wirtualne są tworzone przez klientów i są w ich wdrożonych obciążeń podłączonych do. Sieci wirtualne są podstawy hello wszystkie funkcje zabezpieczeń sieci hello wymaganych tooestablish wdrożeń klienta obwodowej sieci tooprotect na platformie Azure.

## <a name="overview-of-azure-virtual-networks"></a>Omówienie sieci wirtualnych platformy Azure
Zanim ruchu internetowego można pobrać toohello sieci wirtualnych platformy Azure, istnieją dwie warstwy dostępu do właściwych toohello zabezpieczeń platformy Azure:

1.    **Ochrona przed atakami DDoS**: ochrona przed atakami DDoS to warstwa hello Azure sieci fizycznej, która chroni przed atakami na dużą skalę internetowego hello samą platformą Azure. Tego rodzaju ataki Użyj wielu węzłów "bot" w toooverwhelm próba usługi internetowe. Platforma Azure ma niezawodne siatki ochrony przed atakami DDoS na wszystkie połączenia przychodzące, wychodzące i Azure między regionu. Ta warstwa ochrony przed atakami DDoS nie ma żadnych atrybutów można skonfigurować użytkownika i nie jest dostępny toohello klienta. warstwę ochrony przed atakami DDoS Hello chroni Azure jako platformę przed atakami na dużą skalę, również monitoruje ruchu wyjściowego powiązane i regionu Azure między ruchu. Przy użyciu wirtualnych urządzeń sieciowych na powitania sieci wirtualnej, dodatkowe warstwy odporności można skonfigurować przez powitania klienta przed mniejszych ataki skalowania, które nie rzeczy przed wyjazdem hello platformy ochrony na poziomie. Przykład DDoS w akcji; Jeśli internetowy adres IP zaatakowany przez na dużą skalę ataków DDoS, Azure może wykryć źródeł hello hello ataków i wyczyść hello naruszeń ruchu przed osiągnięciem jego przeznaczenia. W większości przypadków, hello zaatakowane punkt końcowy nie ma wpływu na atak powitania. W rzadkich przypadkach hello dotyczy punkt końcowy żaden ruch jest tooother odpowiednich punktów końcowych, tylko atak powitania punktu końcowego. W związku z tym innych klientów i usług zobaczy bez wpływu na tym ataki. Jest toonote krytyczny, który Azure DDoS tylko szuka ataków na dużą skalę. Istnieje możliwość, że określone usługi można przeciążony przed przekroczenia progów ochrony na poziomie platformy hello. Na przykład witryny sieci web na jednym serwerze A0 IIS, można podjąć w trybie offline takiego ataku przed zagrożeniem platformy Azure poziom ochrony przed atakami DDoS.

2.  **Publiczne adresy IP**: publicznego adresu IP adresów (włączone za pośrednictwem punktów końcowych usługi, publiczny adres IP adresy bramy aplikacji i innych funkcji platformy Azure, udostępniające publicznego adresu IP adres toohello kierowane tooyour zasobu internetowego) umożliwiają usługi w chmurze lub grupy zasobów toohave publiczne adresy Internet IP i portów. punkt końcowy Hello używa translatora adresów sieciowych (NAT) tooroute ruchu toohello wewnętrzny adres i port na powitania sieci wirtualnej platformy Azure. Ta ścieżka jest podstawowy sposobem toopass zewnętrznego ruchu w sieci wirtualnej hello hello. Hello publiczne adresy IP są konfigurowalne toodetermine, których ruch jest przekazywany w i jak i gdzie jest translacja na toohello sieci wirtualnej.

Gdy ruch osiągnie hello sieci wirtualnej, istnieje wiele funkcji, które są dostarczane do gry. Sieci wirtualnych platformy Azure są hello podstawę tooattach klientów, ich obciążeń i których dotyczy podstawowych zabezpieczeń na poziomie sieci. Jest siecią prywatną (w nakładce sieci wirtualnej) w systemie Azure dla klientów z hello następujące funkcje i właściwości:

* **Izolacja ruchu**: sieć wirtualna jest granica izolacji ruchu hello na powitania platformy Azure. Maszynach wirtualnych (VM) w jednej sieci wirtualnej nie może komunikować się bezpośrednio tooVMs w innej sieci wirtualnej, nawet jeśli obie sieci wirtualne są tworzone przez hello tego samego klienta. Izolacja jest krytyczne właściwość, która zapewnia klienta maszyn wirtualnych i komunikacja pozostanie prywatnej sieci wirtualnej.

>[!NOTE]
>Izolacja ruchu odwołuje się tylko tootraffic *przychodzących* toohello sieci wirtualnej. Domyślne ruch wychodzący z toohello sieci wirtualnej hello internet jest dozwolone, ale w razie potrzeby przez grupy NSG można zapobiec.
>
>

* **Topologia wielowarstwowa**: sieci wirtualne umożliwiają klientom topologii wielowarstwowej toodefine przydzielając podsieci i wyznaczenie przestrzeni adresowych osobne dla różnych elementów lub "warstwy" ich obciążeń. Tych grup logicznych i topologii Włącz zasady dostępu różnych toodefine klientów na podstawie typów obciążenia hello, a także kontrolować ruch między warstwami hello.
* **Łączność między lokalizacjami**: klientów może nawiązać łączności między lokalizacjami między sieci wirtualnej i wieloma lokacjami lokalnymi lub innych sieci wirtualnych na platformie Azure. tooconstruct połączenia, klienci mogą użyć sieci wirtualnej komunikacji równorzędnej, bram sieci VPN platformy Azure, wirtualnych urządzeń sieciowych innych firm lub ExpressRoute. Azure obsługuje za pomocą standardowych protokołów IPsec i IKE i prywatne połączenie ExpressRoute sieci VPN typu lokacja lokacja (S2S).
* **Grupa NSG** umożliwia klientom toocreate zasady (kontroli dostępu ACL) na potrzeby hello poziom szczegółowości: sieci interfejsy poszczególnych maszyn wirtualnych i podsieci wirtualne. Klientów można kontrolować dostęp przez zezwalanie na dostęp lub odmawianie komunikacji między hello obciążeń w ramach sieci wirtualnej, od systemów w sieci klienta za pośrednictwem łączności między lokalizacjami lub bezpośrednia komunikacja z Internetem.
* **PRZEZ** i **przesyłania dalej protokołu IP** umożliwiają klientom toodefine hello ścieżki do komunikacji między warstwami innej sieci wirtualnej. Klienci mogą wdrażać zaporą, Identyfikatory/adresów IP i inne urządzenia wirtualnego oraz kierować ruchem sieciowym za pomocą tych urządzeń zabezpieczeń do wymuszania zasad granic zabezpieczeń, inspekcji i inspekcji.
* **Sieci wirtualnych urządzeń** w portalu Azure Marketplace hello: urządzenia zabezpieczeń, takie jak zapory, moduły równoważenia obciążenia i Identyfikatory/adresów IP są dostępne w portalu Azure Marketplace hello i hello Galeria obrazów maszyny Wirtualnej. Klienci mogą wdrożyć te urządzenia w sieciach wirtualnych, a w szczególności na ich bezpieczne środowisko sieciowe zabezpieczeń granic (w tym podsieci sieci obwodowej hello) toocomplete wielowarstwowych.

Z tych funkcji i możliwości przykładem sposobu architektury sieci obwodowej mogła zostać zbudowana na platformie Azure jest powitania po diagramu:

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>Właściwości sieci obwodowej i wymagania
sieć obwodowa Hello jest hello fronton sieci hello, bezpośrednio relacje komunikacji z hello Internet. pakiety przychodzące Hello powinny przepływać przez hello urządzenia zabezpieczeń, takie jak zapory hello, identyfikatorów i adresów IP, przed osiągnięciem hello serwerami zaplecza. Pakiety powiązane z Internetu od obciążeń hello również mogą przepływać przez hello urządzenia zabezpieczeń w sieci obwodowej hello do wymuszania zasad inspekcji i inspekcji, przed opuszczeniem hello sieci. Ponadto sieci obwodowej hello może obsługiwać bramy sieci VPN między lokalizacjami między sieci wirtualne klienta i sieci lokalnej.

### <a name="perimeter-network-characteristics"></a>Właściwości sieci obwodowej
Odwołanie do powyższej ilustracji hello, czynniki hello sieci obwodowej dobrej są następujące:

* Internetowy:
  * podsieć sieci obwodowej Hello sam jest skierowane do Internetu, bezpośrednio komunikacji z hello Internet.
  * Publiczne adresy IP, adresy VIP i/lub punktów końcowych usługi przekazywania sieci frontonu toohello ruch do Internetu i urządzeń.
  * Ruchu przychodzącego ruchu z powitalne Internet przechodzi przez urządzenia zabezpieczeń przed innymi zasobami na powitania sieć frontonu.
  * Włączenie zabezpieczeń dla ruchu wychodzącego ruch przechodzi przez urządzeń zabezpieczeń, co hello ostatni krok przed przekazaniem toohello Internet.
* Sieć chroniona:
  * Brak bezpośredniego ścieżka z hello Internet toohello podstawowej infrastruktury.
  * Kanały toohello podstawowej infrastruktury muszą przejść za pomocą urządzeń zabezpieczeń, takich jak grupy NSG, zapory lub urządzenia sieci VPN.
  * Inne urządzenia nie musi zestawiania Internet i hello infrastrukturze podstawowej.
  * Urządzenia zabezpieczeń zarówno hello internetowy i hello sieci chronionego ukierunkowane granice hello sieci obwodowej (na przykład Witaj dwie zapory ikony hello poprzedniej rysunku) faktycznie może być pojedynczego urządzenia wirtualnego przy użyciu reguł zróżnicowanych lub interfejsy dla każdej granicy. Na przykład jeden urządzenie fizyczne, logicznie rozdzielone, obsługi hello obciążenia dla obu granice hello sieci obwodowej.
* Inne typowe wskazówki i ograniczenia:
  * Obciążeń nie mogą przechowywać newralgicznych danych biznesowych.
  * Konfiguracje sieci tooperimeter dostępu i aktualizacje i wdrożeniami są ograniczone tooonly uprawnień administratorów.

### <a name="perimeter-network-requirements"></a>Wymagania dotyczące sieci obwodowej
tooenable te właściwości, skorzystaj z następujących wskazówek w sieci wirtualnej wymagania tooimplement sieci obwodowej powiodło się:

* **Architektura podsieci:** sieci wirtualnej hello Określ tak, aby w całej podsieci dedykowanego jako hello sieci obwodowej, oddzielona od innych podsieci w hello sam sieci wirtualnej. Ta separacja zapewnia hello ruchu między hello sieci obwodowej oraz innych przepływów warstw wewnętrznego lub prywatnego podsieci za pośrednictwem zapory lub urządzenia wirtualnego Identyfikatory/adresów IP.  Trasy zdefiniowane przez użytkownika na powitania granicę, którą podsieci są wymagane tooforward urządzenie wirtualne toohello ruchu.
* **Grupa NSG:** hello podsieci sieci obwodowej, sam powinien być otwarty tooallow komunikację z hello Internet, ale nie oznacza klientów należy pomijanie grup NSG. Postępuj zgodnie z typowych zabezpieczeń rozwiązań toominimize hello sieci powierzchnie widoczne toohello Internet. Zablokowanie zakresów adresów zdalnego hello dozwolone tooaccess hello wdrożenia lub hello określonej aplikacji protokoły i porty, które są otwarte. Może to być sytuacji, w których pełną blokowanie nie jest możliwe. Na przykład, jeśli klienci mają zewnętrznej witryny sieci Web na platformie Azure, sieci obwodowej hello powinna zezwalać na powitania przychodzących żądań sieci web z publicznych adresów IP, ale należy otwierać tylko porty aplikacji sieci web hello: ruch TCP na porcie 80 i/lub TCP na porcie 443.
* **Tabela routingu:** hello podsieci sieci obwodowej, sama powinno być możliwe toocommunicate toohello Internet bezpośrednio, ale nie należy zezwalać tooand bezpośrednia komunikacja z tyłu zakończenia lub lokalnej sieci hello bez przechodzenia przez zaporę lub urządzenia zabezpieczeń.
* **Konfiguracja urządzenia zabezpieczeń:** tooroute i inspekcję pakietów między hello sieci obwodowej i rest hello sieci hello chronione, hello urządzenia zabezpieczeń, takie jak zapory, Identyfikatory, i adresy IP urządzeń mogą być wieloadresowych. Mogą mieć oddzielnych kart sieciowych dla sieci obwodowej hello i hello podsieci wewnętrznej. karty sieciowe Hello w sieci obwodowej hello komunikować się bezpośrednio tooand z hello Internet, o hello odpowiednich grup NSG i obwód hello sieci tabeli routingu. karty sieciowe Hello łączenie podsieci wewnętrznej toohello mają bardziej ograniczone grup NSG i tabelach routingu hello odpowiednie podsieci wewnętrznej.
* **Funkcje urządzenia zabezpieczeń:** urządzenia zabezpieczeń hello wdrożonego w sieci obwodowej hello zwykle wykonać hello następujące funkcje:
  * Zapora: Wymuszania reguł zapory lub zasady kontroli dostępu hello żądań przychodzących.
  * Zagrożenia i zapobiegania: wykrywanie i zmniejszenia złośliwych ataków z hello Internet.
  * Inspekcja i rejestrowanie: Obsługa szczegółowe dzienniki inspekcji i analizy.
  * Odwrotny serwer proxy: przekierowywanie hello przychodzących żądań toohello odpowiadających serwerów zaplecza. Przekierowanie obejmuje mapowania i zwykle translacji adresów docelowego hello na urządzeniach z frontonu hello zapory, toohello adresów serwerów zaplecza.
  * Przekazuj serwera proxy: zapewnianie NAT i przeprowadzania inspekcji dla komunikacji inicjowane przy użyciu hello toohello wirtualnej sieci Internet.
  * Router: Przesyłania ruchu przychodzącego i między podsieciami wewnątrz hello sieci wirtualnej.
  * Urządzenia sieci VPN: działa jako hello między lokalizacjami bramy sieci VPN dla między lokalizacjami połączenie sieci VPN między sieciami lokalnymi klientów i sieci wirtualnych platformy Azure.
  * Serwer sieci VPN: akceptowanie połączenie wirtualnej sieci tooAzure klientów sieci VPN.

> [!TIP]
> Zachowaj hello następujące dwa oddzielne grup: hello osoby autoryzowane tooaccess hello obwodowej sieci zabezpieczeń narzędzi i hello osoby autoryzowane jako administratorzy programowanie, wdrożenia i działania aplikacji. Oddzieleniu tych grup umożliwia podział obowiązków i uniemożliwia jedna osoba z pominięciem aplikacji, zabezpieczeń i kontroli zabezpieczeń sieci.
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>Toobe pytania zadawane podczas tworzenia granic sieci
W tej sekcji, chyba że wyraźnie wymienionych hello termin "sieci" odnosi się tooprivate Azure sieci wirtualnych utworzonych przez administratora subskrypcji. termin Hello nie odwołuje się toohello podstawowe sieci fizyczne w systemie Azure.

Ponadto sieci wirtualnych platformy Azure są często używane tooextend tradycyjnych, lokalnie sieci. Jest to możliwe tooincorporate lokacja lokacja lub hybrydowego ExpressRoute networking solutions z architektury sieci obwodowej. To łącze hybrydowego jest ważną kwestią tworzenia granic zabezpieczeń sieci.

Witaj następujące trzy pytania są krytyczne tooanswer gdy tworzysz sieci z siecią obwodową a wielu granic zabezpieczeń.

#### <a name="1-how-many-boundaries-are-needed"></a>1) ile granice są potrzebne?
pierwszy punkt decyzji Hello jest toodecide ile granic zabezpieczeń są potrzebne w danej sytuacji:

* Pojedyncza granica: jeden w sieci obwodowej frontonu hello, między hello sieci wirtualnej i hello Internet.
* Granice dwóch: jedną na powitania po stronie Internetu hello sieci obwodowej, a drugą między podsieci sieci obwodowej hello i podsieci wewnętrznej hello w hello sieci wirtualnych platformy Azure.
* Trzy granice: na stronie Internetu hello hello sieci obwodowej, między siecią obwodową hello i podsieci wewnętrznej, a drugi między podsieciami zaplecza hello i hello sieci lokalnej.
* Granice N: Numer zmiennej. W zależności od wymagań dotyczących zabezpieczeń nie istnieje limit nie toohello liczba granic zabezpieczeń, które mogą być stosowane w danej sieci.

Witaj liczbę i rodzaj potrzebne różnią się granic na podstawie firmy ryzyko uszkodzenia i hello danego scenariusza implementowana. Ta decyzja często staje się wraz z wielu grup w organizacji, często tym zespół ryzyka i zgodności, sieć i zespołu platformy i zespół deweloperów aplikacji. Osobom wiedzę na temat zabezpieczeń, hello danych związane i technologie hello używany powinien mieć powiedzieć w tej decyzji tooensure hello zabezpieczeń odpowiednich zasobów dla każdego wdrożenia.

> [!TIP]
> Użyj hello najmniejsza liczba granic, które spełniają wymagania dotyczące zabezpieczeń hello w danej sytuacji. O granicach więcej operacji i rozwiązywania problemów można trudniej, a także hello wiele granic zasad zarządzania obciążenie związane z zarządzaniem hello wraz z upływem czasu. Jednak za mało granic zwiększenie ryzyka. Znajdowanie hello saldo jest krytyczne.
>
>

![6]

Hello powyższej ilustracji przedstawiono ogólny widok sieci granicznej zabezpieczeń trzy. granice Hello należą do zakresu od sieci obwodowej hello i hello Internet, hello Azure frontonu i zaplecza podsieci prywatne i hello Azure zaplecza podsieci i sieci firmowej lokalne powitania.

#### <a name="2-where-are-hello-boundaries-located"></a>2) granice hello lokalizację?
Po hello liczba granice są ustalane, gdzie tooimplement jest ich hello dalej podjęcie decyzji. Zazwyczaj są trzy opcje:

* Przy użyciu Internetowych usług pośredniczących (na przykład oparte na chmurze Zapora aplikacji sieci Web, który nie został omówiony w niniejszym dokumencie)
* Przy użyciu funkcji macierzystego i/lub wirtualnych urządzeń sieciowych na platformie Azure
* Za pomocą urządzeń fizycznych na powitania sieci lokalnej

W sieciach czysto Azure opcje hello są natywnego funkcje platformy Azure (na przykład równoważenia obciążenia Azure) lub wirtualnych urządzeń sieciowych z hello sformatowanego partnera ekosystemu platformy Azure (na przykład zapory Check Point).

Jeśli granica jest potrzebny platformy Azure i siecią lokalną, hello urządzeń zabezpieczeń może znajdować się po obu stronach połączenia hello (lub obu stronach). W związku z tym decyzji muszą być wprowadzane na powitania lokalizacji tooplace zabezpieczeń sprzęcie.

Hello poprzedniej ilustracji sieci Internet obwodowej hello granice przodu do tyłu zakończenia hello całkowicie znajdują się w obrębie platformy Azure i musi być natywnego funkcje platformy Azure lub wirtualnych urządzeń sieciowych. Urządzenia zabezpieczeń w hello granicę między Azure (podsieci wewnętrznej) oraz sieci firmowej hello można na hello Azure po stronie lub po stronie lokalne powitania lub nawet kombinację urządzeń po obu stronach. Może to być istotne zalety i wady opcji tooeither poważnie rozważane.

Na przykład przy użyciu istniejącego sprzętu zabezpieczeń fizycznych na powitania w lokalnym sieci po stronie ma hello zaletę, że niezbędna jest żadnych nowych narzędzi. Wystarczy ponownej konfiguracji. Wadą Hello jest jednak, że cały ruch musi wrócić z toobe sieci lokalnej Azure toohello widziana przez hello narzędzi zabezpieczeń. W związku z tym ruchu Azure do platformy Azure może pociągnąć za sobą znaczne opóźnienia i wpłynąć na wydajność i środowisko aplikacji, jeśli jego wymuszono wstecz toohello lokalnej sieci do wymuszania zasad zabezpieczeń.

#### <a name="3-how-are-hello-boundaries-implemented"></a>3) granice hello implementowania?
Każda granica zabezpieczeń prawdopodobnie będzie miała wymagania różne możliwości (na przykład identyfikatorów i reguły zapory na powitania po stronie Internetu hello sieci obwodowej, ale tylko listy ACL między siecią obwodową hello i podsieci wewnętrznej). Wcześniejsze podjęcie decyzji dotyczących urządzenia, które (lub ile urządzeń), zależy od toouse hello wymagań scenariusza i zabezpieczeń. W następującej sekcji hello przykłady 1, 2 i 3 omówiono niektóre opcje, które mogłyby zostać użyte. Przeglądanie hello funkcji natywnego sieć platformy Azure i urządzenia hello dostępnej na platformie Azure z ekosystemem partnerów hello pokazuje toosolve dostępne opcje tysięcy hello praktycznie dowolne scenariusza.

Inną kwestią implementacji klucza jest sposób tooconnect hello lokalnej sieci platformy Azure. Należy użyć hello Azure wirtualnej bramy lub urządzenie wirtualne sieci? Te opcje omówiono bardziej szczegółowo na powitania po sekcji (przykłady 4, 5 i 6).

Ponadto ruchu między sieciami wirtualnymi w obrębie platformy Azure mogą być wymagane. Te scenariusze zostanie dodana w przyszłych hello.

Jeśli znasz już odpowiedzi hello toohello wstecz pytania, hello [szybkiego startu](#fast-start) sekcji mogą ułatwić identyfikację, przykłady, które są najbardziej odpowiednie dla danego scenariusza.

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>Przykłady: Tworzenie granic zabezpieczeń z sieci wirtualnych platformy Azure
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>Przykład 1 kompilacji toohelp sieci obwodowej ochrony aplikacji za pomocą grup NSG
[Kopii tooFast start](#fast-start) | [szczegółowy kompilacji instrukcje w tym przykładzie][Example1]

[![7]][7]

#### <a name="environment-description"></a>Opis elementu środowiska
W tym przykładzie jest subskrypcji, która zawiera hello następujące zasoby:

- Pojedyncza grupa zasobów
- Sieć wirtualną z dwiema podsieciami: "FrontEnd" i "Wewnętrzna"
- Grupy zabezpieczeń sieci jest stosowane tooboth podsieci
- Windows server, który reprezentuje serwer sieci web aplikacji ("IIS01")
- Dwa serwery systemu Windows, które reprezentują serwery zaplecza aplikacji ("AppVM01", "AppVM02")
- Windows server, który reprezentuje serwer DNS ("DNS01")
- Publicznego adresu IP skojarzonego z serwerem sieci web aplikacji hello

Skrypty i szablonu usługi Azure Resource Manager, zobacz hello [szczegółowe instrukcje kompilacji][Example1].

#### <a name="nsg-description"></a>Opis grupy NSG
W tym przykładzie grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł.

> [!TIP]
> Ogólnie rzecz biorąc, należy utworzyć określone reguł "Zezwalaj" najpierw następuje hello bardziej ogólnym reguły "odmowy". priorytet Hello nakazują reguły są sprawdzane jako pierwsze. Po znalezieniu tooapply tooa określonej reguły ruchu nie dodatkowe reguły są sprawdzane. Reguły NSG można zastosować w albo hello kierunek ruchu przychodzącego lub wychodzącego (z perspektywy hello hello podsieci).
>
>

Deklaratywnie hello następujące reguły są tworzone dla ruchu przychodzącego:

1. Wewnętrzny ruch DNS (port 53) jest dozwolone.
2. Ruch protokołu RDP (port 3389) z tooany Internet hello maszyny wirtualnej jest dozwolony.
3. Ruch HTTP (port 80) z serwera tooweb internetowej hello (IIS01) jest dozwolony.
4. Cały ruch z IIS01 tooAppVM1 (wszystkich portów) jest dozwolone.
5. Odmowa cały ruch (wszystkie porty) z hello Internet toohello całej sieci wirtualnej (obie podsieci).
6. Odmowa cały ruch (wszystkie porty) z hello podsieci frontonu toohello zaplecza podsieci.

Z tych podsieci tooeach powiązane zasady, jeśli żądanie HTTP zostało ruch przychodzący z serwera sieci web toohello Internet hello zarówno 3 reguły (Zezwalaj) i 5 (odmówić go) powinna zostać zastosowana. Jednak ponieważ reguła 3 ma wyższy priorytet, tylko będą miały zastosowania i reguły 5 nie przybyły do odtwarzania. W związku z tym żądania HTTP hello mogliby toohello serwera sieci web. Jeśli ten sam ruch próbował tooreach hello DNS01 serwera, zasada 5 (odmówić go) będzie hello pierwszy tooapply i ruchu hello nie mogliby toopass toohello serwera. Reguła 6 (odmówić go) bloki hello podsieci frontonu z mówić podsieci wewnętrznej toohello (z wyjątkiem dozwolonego ruchu w regułach 1 i 4). Ten zestaw reguł chroni hello sieci wewnętrznej, w przypadku, gdy osoba atakująca obniża hello aplikacja sieci web frontonu hello. Osoba atakująca Hello będzie ograniczona "chronionych" sieciowej zaplecza toohello dostępu (tylko tooresources udostępniane na serwerze AppVM01 hello).

Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego toohello Internet. Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących. toolock dół ruchu w obu kierunkach, routing zdefiniowane przez użytkownika jest wymagana (Zobacz przykład 3).

#### <a name="conclusion"></a>Podsumowanie
W tym przykładzie jest względnie proste i bezpośrednie sposobem izolowanie podsieci wewnętrznej hello z ruchu przychodzącego. Aby uzyskać więcej informacji, zobacz hello [szczegółowe instrukcje kompilacji][Example1]. Instrukcje te obejmują:

* Jak toobuild obwodowej tej sieci z klasycznym skryptów programu PowerShell.
* Jak toobuild obwodowej tej sieci z szablonem usługi Azure Resource Manager.
* Szczegółowy opis każdego polecenia NSG.
* Scenariusze przepływu ruchu szczegółowe, przedstawiający sposób ruch jest dozwolony lub zabroniony w każdej warstwie.


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>Przykład 2 kompilacji toohelp sieci obwodowej chronić aplikacje z zaporą i grupy NSG
[Kopii tooFast start](#fast-start) | [szczegółowy kompilacji instrukcje w tym przykładzie][Example2]

[![8]][8]

#### <a name="environment-description"></a>Opis elementu środowiska
W tym przykładzie jest subskrypcji, która zawiera hello następujące zasoby:

* Pojedyncza grupa zasobów
* Sieć wirtualną z dwiema podsieciami: "FrontEnd" i "Wewnętrzna"
* Grupy zabezpieczeń sieci jest stosowane tooboth podsieci
* Urządzenie wirtualne sieci, w tym przypadku a zapory, podłączone podsieci frontonu toohello
* Windows server, który reprezentuje serwer sieci web aplikacji ("IIS01")
* Dwa serwery systemu Windows, które reprezentują serwery zaplecza aplikacji ("AppVM01", "AppVM02")
* Windows server, który reprezentuje serwer DNS ("DNS01")

Skrypty i szablonu usługi Azure Resource Manager, zobacz hello [szczegółowe instrukcje kompilacji][Example2].

#### <a name="nsg-description"></a>Opis grupy NSG
W tym przykładzie grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł.

> [!TIP]
> Ogólnie rzecz biorąc, należy utworzyć określone reguł "Zezwalaj" najpierw następuje hello bardziej ogólnym reguły "odmowy". priorytet Hello nakazują reguły są sprawdzane jako pierwsze. Po znalezieniu tooapply tooa określonej reguły ruchu nie dodatkowe reguły są sprawdzane. Reguły NSG można zastosować w albo hello kierunek ruchu przychodzącego lub wychodzącego (z perspektywy hello hello podsieci).
>
>

Deklaratywnie hello następujące reguły są tworzone dla ruchu przychodzącego:

1. Wewnętrzny ruch DNS (port 53) jest dozwolone.
2. Ruch protokołu RDP (port 3389) z tooany Internet hello maszyny wirtualnej jest dozwolony.
3. Wszelkie Internet ruchu (wszystkie porty) toohello sieci urządzenie wirtualne (zapory) jest dozwolone.
4. Cały ruch z IIS01 tooAppVM1 (wszystkich portów) jest dozwolone.
5. Odmowa cały ruch (wszystkie porty) z hello Internet toohello całej sieci wirtualnej (obie podsieci).
6. Odmowa cały ruch (wszystkie porty) z hello podsieci frontonu toohello zaplecza podsieci.

Z tych podsieci tooeach powiązane zasady, jeśli żądanie HTTP zostało ruch przychodzący z toohello hello zaporę, zarówno 3 reguły (Zezwalaj) i 5 (odmówić go) powinna zostać zastosowana. Jednak ponieważ reguła 3 ma wyższy priorytet, tylko będą miały zastosowania i reguły 5 nie przybyły do odtwarzania. W związku z tym żądaniu hello HTTP będzie dozwolone toohello zapory. Jeśli ten sam ruch próbował tooreach hello IIS01 serwera, nawet jeśli komputer jest w podsieci frontonu hello, zasada 5 (odmówić go) powinna zostać zastosowana, i ruchu hello nie mogliby toopass toohello serwera. Reguła 6 (odmówić go) bloki hello podsieci frontonu z mówić podsieci wewnętrznej toohello (z wyjątkiem dozwolonego ruchu w regułach 1 i 4). Ten zestaw reguł chroni hello sieci wewnętrznej, w przypadku, gdy osoba atakująca obniża hello aplikacja sieci web frontonu hello. Osoba atakująca Hello będzie ograniczona "chronionych" sieciowej zaplecza toohello dostępu (tylko tooresources udostępniane na serwerze AppVM01 hello).

Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego toohello Internet. Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących. toolock dół ruchu w obu kierunkach, routing zdefiniowane przez użytkownika jest wymagana (Zobacz przykład 3).

#### <a name="firewall-rule-description"></a>Opis reguły zapory
W zaporze hello powinny być tworzone zasady przekazywania. Ponieważ ten przykład tylko trasy Internet ruchu przychodzącego toohello zapory i następnie toohello serwera sieci web, tylko jeden przekazywania sieci translacji adresów (NAT) reguły jest wymagane.

Hello przekazywania Reguła akceptuje każdego adresu źródłowego dla ruchu przychodzącego, który trafienia zapory hello próby tooreach HTTP (port 80 i 443 dla protokołu HTTPS). Ma ona wysyłane poza interfejsu lokalne powitania zapory i Przekierowanie toohello serwera sieci web z hello 10.0.1.5 adres IP.

#### <a name="conclusion"></a>Podsumowanie
W tym przykładzie jest względnie łatwe ochronie aplikacji za pomocą zapory i izolowanie podsieci wewnętrznej hello z ruchu przychodzącego. Aby uzyskać więcej informacji, zobacz hello [szczegółowe instrukcje kompilacji][Example2]. Instrukcje te obejmują:

* Jak toobuild obwodowej tej sieci z klasycznym skryptów programu PowerShell.
* Jak toobuild w tym przykładzie z szablonem usługi Azure Resource Manager.
* Szczegółowy opis każdego polecenia i zapory reguły NSG.
* Scenariusze przepływu ruchu szczegółowe, przedstawiający sposób ruch jest dozwolony lub zabroniony w każdej warstwie.

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>Przykład 3 kompilacji toohelp sieci obwodowej ochrony sieci zapory i przez i grupy NSG
[Kopii tooFast start](#fast-start) | [szczegółowy kompilacji instrukcje w tym przykładzie][Example3]

[![9]][9]

#### <a name="environment-description"></a>Opis elementu środowiska
W tym przykładzie jest subskrypcji, która zawiera hello następujące zasoby:

* Pojedyncza grupa zasobów
* Sieć wirtualną przy użyciu trzech podsieci: "SecNet", "Fronton" i "Wewnętrzna"
* Urządzenie wirtualne sieci, w tym przypadku, a Zapora połączona toohello SecNet podsieci
* Windows server, który reprezentuje serwer sieci web aplikacji ("IIS01")
* Dwa serwery systemu Windows, które reprezentują serwery zaplecza aplikacji ("AppVM01", "AppVM02")
* Windows server, który reprezentuje serwer DNS ("DNS01")

Skrypty i szablonu usługi Azure Resource Manager, zobacz hello [szczegółowe instrukcje kompilacji][Example3].

#### <a name="udr-description"></a>Opis elementu przez
Domyślnie program hello następujące trasy systemowe są zdefiniowane jako:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Witaj VNETLocal jest zawsze prefiksy adresów zdefiniowanych, wchodzące w skład hello sieci wirtualnej dla określonej sieci (czyli jego zmiany z sieci toovirtual sieci wirtualnej, w zależności od tego, jak zdefiniowano każdej określonej sieci wirtualnej). trasy systemowe pozostałych Hello są statyczne i domyślne jak wskazano w tabeli hello.

W tym przykładzie dwie tabele routingu są tworzone, jeden dla hello podsieci frontonu i zaplecza. Każda tabela tras statycznych, które są odpowiednie dla podanej podsieci hello jest załadowana. W tym przykładzie każda tabela zawiera trzy tras, na których kierować cały ruch (0.0.0.0/0) za pośrednictwem zapory hello (następnego przeskoku = adres IP urządzenia wirtualnego):

1. Ruchu w podsieci lokalnej z następnego przeskoku zdefiniowane tooallow podsieci lokalnej ruchu toobypass hello zapory.
2. Ruchu w sieci wirtualnej z przeskoku dalej zdefiniowany jako zapory. Ta następnego przeskoku przesłania hello domyślna reguła, która umożliwia bezpośrednio tooroute ruchu lokalną sieć wirtualną.
3. Wszystkie pozostałe ruchu (0/0) z następnego przeskoku zdefiniowany jako hello zapory.

> [!TIP]
> Nie ma wpisu podsieci lokalnej hello w hello przez podziały podsieci lokalnej komunikacji.
>
> * W naszym przykładzie 10.0.1.0/24 wskazanie tooVNETLocal jest krytyczny! Bez tego pakietu, pozostawiając powitania serwera sieci Web (10.0.1.4) przeznaczone tooanother serwer lokalny (na przykład) 10.0.1.25 wystąpi błąd, ponieważ zostaną wysłane toohello NVA. Hello NVA wysyła on toohello podsieci i podsieci hello zostanie ponownie toohello NVA w pętli nieskończonej.
> * ryzyko Hello Pętla routingu są zazwyczaj wyższe na urządzeniach z wieloma kartami sieciowymi, które są połączone tooseparate podsieci, które jest często tradycyjnych, lokalnie urządzeń.
>
>

Po utworzeniu hello tabele routingu, muszą być powiązane tootheir podsieci. Witaj podsieci frontonu tabeli routingu, utworzonej i powiązany toohello podsieci, będzie wyglądać te dane wyjściowe:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> PRZEZ teraz mogą być zastosowane toohello podsieć bramy, na które hello ExpressRoute obwód jest połączony.
>
> W przykładach 3 i 4 przedstawiono przykładowe jak tooenable sieci obwodowej sieci ExpressRoute lub sieci lokacja lokacja.
>
>

#### <a name="ip-forwarding-description"></a>Opis usługi przesyłania dalej protokołu IP
Przekazywanie adresów IP jest tooUDR funkcji pomocnika. Przekazywanie adresów IP to ustawienie na urządzenie wirtualne, które umożliwia jej tooreceive ruchu kierowanego nie specjalnie toohello urządzenia, a następnie przesyła ten ruch tooits ostatecznym miejscem przeznaczenia.

Na przykład jeśli AppVM01 sprawia, że serwer DNS01 toohello żądania, przez czy trasy Zapora toohello ruchu. Włączone przekazywanie adresów IP hello ruchu dla miejsca docelowego DNS01 hello (10.0.2.4) jest akceptowane przez urządzenia hello (10.0.0.4) i przesyłane dalej ostatecznym miejscem przeznaczenia tooits (10.0.2.4). Bez przesyłania dalej protokołu IP włączone na zaporze hello ruch może nie zostać zaakceptowane przez hello urządzenia nawet hello tabeli tras ma zapory hello jako hello następnego przeskoku. toouse urządzenie wirtualne jest krytyczne tooremember tooenable IP przekazywania oraz przez.

#### <a name="nsg-description"></a>Opis grupy NSG
W tym przykładzie grupa NSG jest wbudowana i następnie ładowane przy użyciu jednej reguły. Ta grupa jest następnie powiązany tylko toohello frontonu i zaplecza podsieci (nie hello SecNet). Deklaratywnie budowanego hello następujące reguły:

* Odmowa cały ruch (wszystkie porty) z hello Internet toohello całej sieci wirtualnej (wszystkie podsieci).

Mimo że grupy NSG są używane w tym przykładzie, głównym celem jest jako dodatkowej warstwy obrony przed ręcznej konfiguracji. Witaj celem jest tooblock cały ruch przychodzący z hello Internet tooeither hello podsieci frontonu lub zaplecza. Ruch powinny przepływać tylko za pośrednictwem zapory toohello podsieci SecNet hello (i następnie w razie potrzeby podsieci frontonu lub zaplecza toohello). Plus przy użyciu reguł przez hello w miejscu, cały ruch, że na powitania podsieci frontonu lub zaplecza czy przekierowanie limit toohello zapory (Dziękujemy tooUDR). Zapora Hello będzie wyświetlać ten ruch asymetrycznego przepływu i spowoduje pominięcie hello ruchu wychodzącego. W związku z tym są trzy warstwy zabezpieczeń Ochrona powitalnych podsieci:

* Nie publiczny adres IP frontonu lub wewnętrznej bazy danych kart sieciowych.
* Grupy NSG uniemożliwienie ruchu hello Internet.
* Witaj zapory usunięcie asymetrycznego ruchu.

Jeden punkt interesujące dotyczące hello NSG, w tym przykładzie jest zawiera tylko jedną regułę, czyli toodeny Internet ruchu toohello całej sieci wirtualnej, tym hello zabezpieczeń podsieci. Jednak ponieważ hello grupa NSG jest tylko powiązany toohello frontonu i zaplecza podsieci, reguła hello nie jest przetwarzane na ruch ruchu przychodzącego toohello zabezpieczeń podsieci. W związku z tym podsieci zabezpieczeń toohello przepływa ruch.

#### <a name="firewall-rules"></a>Reguły zapory
W zaporze hello powinny być tworzone zasady przekazywania. Ponieważ Zapora hello jest blokowanie lub przekazywania wszystkich przychodzące, wychodzące i ruchu w sieci wirtualnej w obrębie, wiele reguł zapory są wymagane. Ponadto cały ruch przychodzący trafienia hello usługi zabezpieczeń publicznego adresu IP (różne porty), toobe przetworzony przez zaporę Windows hello. Najlepszym rozwiązaniem jest toodiagram hello logicznej przepływów przed rozpoczęciem konfigurowania hello podsieci i reguły zapory, tooavoid zmian później. Witaj poniższej ilustracji jest widok logiczny hello reguły zapory w tym przykładzie:

![10]

> [!NOTE]
> Oparte na powitania używanych przez urządzenie wirtualne sieci, hello porty zarządzania różnią się. W tym przykładzie zapory NextGen Barracuda odwołuje się, który używa portów 22, 801 i 807. Zapoznaj się hello urządzenia dostawcy dokumentacji toofind hello porty używane do zarządzania hello urządzenie używane.
>
>

#### <a name="firewall-rules-description"></a>Opis reguł zapory
W hello poprzedzających diagram logiczny hello zabezpieczeń podsieci nie jest wyświetlane, ponieważ Zapora hello jest hello tylko zasobów tej podsieci. Hello diagram jest pokazywany hello reguły zapory i sposób ich logicznie akceptować lub odrzucać przepływów ruchu sieciowego, nie hello routingiem ścieżkę. Ponadto zewnętrzne porty hello wybrany na potrzeby hello na ruch RDP są wyższe ranged portów (8014 — 8026) i zostały wybrane tooloosely są wyrównane z hello ostatni dwa oktety hello lokalny adres IP dla czytelności łatwiejsze (na przykład serwer lokalny adres 10.0.1.4 jest skojarzony z portu zewnętrznego 8014). Wszystkie porty wyższej niekolidujących, mogą zostać wykorzystane.

W tym przykładzie potrzebne są nam siedem typów zasad:

* Reguły zewnętrzne (dla ruchu przychodzącego):
  1. Reguły zapory zarządzania: ten przekierowania aplikacji reguła zezwala toopass ruchu porty zarządzania toohello hello sieci wirtualne urządzenia.
  2. Zasady protokołu RDP (na każdym serwerze z systemem Windows): następujące cztery reguły (po jednym dla każdego serwera) Zezwalaj na zarządzanie hello poszczególnych serwerów za pomocą protokołu RDP. cztery reguły protokołu RDP Hello może zostać zwinięty również do jednej reguły, w zależności od możliwości hello urządzenie wirtualne sieci hello jest używany.
  3. Reguły ruchu aplikacji: istnieją dwa z tych zasad, hello najpierw transmisji hello frontonu sieci web i hello drugi transmisji hello zaplecza (na przykład warstwa sieci web serwera toodata). Konfiguracja Hello tych reguł zależy od tego, hello architektury sieci (w którym są umieszczane serwerów) oraz ruch (które ruchu hello kierunek przepływu i które porty są używane).
     * Pierwsza reguła Hello zezwala serwerowi aplikacji hello tooreach hello rzeczywistej aplikacji ruchu. Hello inne reguły zezwalają na potrzeby zabezpieczeń i zarządzania, reguły ruchu aplikacji są co Pozwól zewnętrznych tooaccess użytkowników lub usług aplikacji hello. Ten przykład jest jednym serwerze sieci web na porcie 80. W związku z tym pojedynczą aplikacji regułę zapory przekierowuje ruch przychodzący toohello IP zewnętrznego, toohello serwerów wewnętrzny adres IP sieci web. Czy można przetłumaczyć Hello przekierowanie ruchu sesji za pośrednictwem NAT toohello wewnętrznego serwera.
     * drugą regułę Hello jest hello reguły zaplecza tooallow hello web tootalk toohello AppVM01 serwera (ale nie AppVM02) za pomocą dowolnego portu.
* Reguły wewnętrzne (dla ruchu w sieci wirtualnej w obrębie)
  1. Reguła ruchu wychodzącego tooInternet: Ta reguła zezwala na ruch z żadną siecią toopass toohello wybrane sieci. Ta reguła jest zwykle domyślna reguła już na powitania zapory, ale w stanie wyłączenia. Ta reguła powinna być włączona w tym przykładzie.
  2. Reguła DNS: ta zasada umożliwia tylko DNS (port 53) ruchu toopass toohello serwera DNS. Dla tego środowiska większość ruchu z wewnętrznego hello frontonu toohello jest zablokowany. Ta zasada umożliwia w szczególności DNS z żadnych podsieci lokalnej.
  3. Reguła toosubnet podsieci: Ta reguła jest tooallow dowolnego serwera na powitania podsieci wewnętrznej tooconnect tooany serwera na powitania podsieci frontonu (ale nie hello odwrotnej).
* Reguła awaryjnego (dla ruchu, który nie spełnia żadnego z poprzednich hello):
  1. Odmów wszystkie reguły ruchu: Ta reguła odmowy zawsze powinna być hello reguły końcowego (w zakresie priorytet) i jako taki przypadku przepływ ruchu niepowodzenia toomatch żadnego hello poprzedzających reguły zostanie usunięte przez tę regułę. Ta reguła jest regułą domyślnego i zwykle w miejscu i aktywne. Modyfikacje nie są zazwyczaj potrzebne toothis reguły.

> [!TIP]
> Na powitania reguły, toosimplify ruchu drugiej aplikacji, w tym przykładzie jest dozwolone dowolnego portu. W rzeczywistym scenariuszu hello najbardziej określonych zakresów port i adres powinien być używany tooreduce hello ataku tej reguły.
>
>

Po utworzeniu reguły poprzedniej hello, ważne jest tooreview hello priorytetu ruchu tooensure każdej reguły jest dozwolony lub odrzucany zgodnie z potrzebami. W tym przykładzie są reguły hello w kolejności priorytetu.

#### <a name="conclusion"></a>Podsumowanie
W tym przykładzie jest bardziej złożonych ale sposób ochrony i izolowanie hello sieci niż w poprzednich przykładach hello ukończenia. (Przykład 2 chroni tylko aplikacji hello oraz przykład 1 po prostu wyodrębnia podsieci). Ten projekt umożliwia monitorowanie ruchu w obu kierunkach i chroni nie tylko hello przychodzących aplikacji serwera, ale wymusza zasady zabezpieczeń sieci dla wszystkich serwerów w tej sieci. Ponadto w zależności od urządzenia hello używane pełne ruchu inspekcji i rozpoznawanie można osiągnąć. Aby uzyskać więcej informacji, zobacz hello [szczegółowe instrukcje kompilacji][Example3]. Instrukcje te obejmują:

* Jak toobuild obwodowej ten przykład sieci z klasycznym skryptów programu PowerShell.
* Jak toobuild w tym przykładzie z szablonem usługi Azure Resource Manager.
* Szczegółowe opisy każdej przez NSG polecenia, a reguły zapory.
* Scenariusze przepływu ruchu szczegółowe, przedstawiający sposób ruch jest dozwolony lub zabroniony w każdej warstwie.

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>Przykład 4 Dodaj połączenie hybrydowe z lokacja lokacja, wirtualne urządzenia sieci VPN
[Kopii tooFast start](#fast-start) | Szczegółowe instrukcje kompilacji jest dostępny wkrótce

[![11]][11]

#### <a name="environment-description"></a>Opis elementu środowiska
Sieci hybrydowe przy użyciu urządzenie wirtualne sieci (NVA) można dodać tooany typów sieci obwodowej hello opisanego w przykładach 1, 2 lub 3.

Jak pokazano na poprzedniej ilustracji hello, połączenie sieci VPN za pośrednictwem hello Internet (site-to-site) jest używane tooconnect tooan sieci lokalnej sieci wirtualnej platformy Azure za pośrednictwem NVA.

> [!NOTE]
> Jeśli używasz usługi ExpressRoute z włączoną opcją publicznej komunikacji równorzędnej platformy Azure hello, należy utworzyć tras statycznych. Tej trasy statyczne powinny kierować toohello adres IP sieci VPN NVA firmowej Internetu, a nie za pomocą hello połączenia ExpressRoute. Hello NAT wymagane na hello Azure publicznej komunikacji równorzędnej ExpressRoute opcji mogą być dzielone hello sesji sieci VPN.
>
>

Po NVA hello powitalne sieci VPN jest już na miejscu, staje się hello Centrum dla wszystkich sieci i podsieci. zasady przekazywania zapory Hello określić, jaki ruch przepływy są dozwolone, są tłumaczone za pośrednictwem translatora adresów Sieciowych, są przekierowywane lub porzuconych (nawet w przypadku przepływów ruchu sieciowego między hello siecią lokalną a platformą Azure).

Ruch należy rozważyć, jak mogą być optymalizowane lub ograniczone przez ten wzorzec projektowania, w zależności od określonych hello przypadek użycia.

Przy użyciu środowiska hello wbudowane w przykładzie 3, a następnie dodanie połączenia sieciowego hybrydowego sieci VPN typu lokacja lokacja, tworzy hello następującego projektu:

[![12]][12]

router lokalny Hello lub innego urządzenia sieciowego, zgodny z Twojej NVA dla sieci VPN, będą powitania klienta sieci VPN. To fizyczne urządzenie będzie odpowiedzialny za inicjowanie i utrzymywanie hello połączenia sieci VPN z Twojego NVA.

Logicznie toohello NVA sieci hello wygląda cztery oddzielne "strefy zabezpieczeń" przy użyciu reguł hello na powitania NVA trwa hello Dyrektor głównej ruchu między tych stref:

![13]

#### <a name="conclusion"></a>Podsumowanie
Dodanie Hello site-to-site VPN hybrydowego sieci połączenia tooan sieci wirtualnej platformy Azure można rozszerzyć sieć lokalną hello na platformie Azure w bezpieczny sposób. Korzystając z połączenia sieci VPN, ruchu są szyfrowane i kieruje za pośrednictwem hello Internet. Witaj NVA w tym przykładzie zapewnia tooenforce centralnej lokalizacji i zarządzania zasadami zabezpieczeń hello. Aby uzyskać więcej informacji, zobacz hello szczegółowe instrukcje (nadchodzącego) kompilacji. Instrukcje te obejmują:

* Jak toobuild obwodowej ten przykład sieci za pomocą skryptów środowiska PowerShell.
* Jak toobuild w tym przykładzie z szablonem usługi Azure Resource Manager.
* Scenariusze przepływu ruchu szczegółowe, przedstawiający sposób ruch przechodzi przez ten projekt.

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>Przykład 5 Dodaj połączenie hybrydowe z bramą sieci VPN platformy Azure do lokacji,
[Kopii tooFast start](#fast-start) | Szczegółowe instrukcje kompilacji jest dostępny wkrótce

[![14]][14]

#### <a name="environment-description"></a>Opis elementu środowiska
Typ sieci obwodowej tooeither opisanego w przykładach 1 lub 2 można dodać sieci hybrydowe przy użyciu bramy sieci VPN platformy Azure.

Jak pokazano na powyższej ilustracji hello, połączenie sieci VPN za pośrednictwem hello Internet (site-to-site) jest używane tooconnect tooan sieci lokalnej sieci wirtualnej platformy Azure za pośrednictwem bramy sieci VPN platformy Azure.

> [!NOTE]
> Jeśli używasz usługi ExpressRoute z włączoną opcją publicznej komunikacji równorzędnej platformy Azure hello, należy utworzyć tras statycznych. Tej trasy statyczne powinny kierować toohello adres IP sieci VPN NVA firmowej Internetu, a nie za pośrednictwem sieci WAN ExpressRoute hello. Hello NAT wymagane na hello Azure publicznej komunikacji równorzędnej ExpressRoute opcji mogą być dzielone hello sesji sieci VPN.
>
>

Witaj poniższej ilustracji przedstawiono Witaj dwie sieci krawędzie w tym przykładzie. Na pierwszym krawędzi hello hello NVA i grup NSG kontrolować ruch do sieci w obrębie platformy Azure i między Azure i hello Internet. drugi krawędź Hello jest bramy sieci VPN platformy Azure hello, czyli krawędzi oddzielne sieci między lokalną i platformą Azure.

Ruch należy rozważyć, jak mogą być optymalizowane lub ograniczone przez ten wzorzec projektowania, w zależności od określonych hello przypadek użycia.

Przy użyciu środowiska hello wbudowane w przykładzie 1, a następnie dodanie połączenia sieciowego hybrydowego sieci VPN typu lokacja lokacja, tworzy hello następującego projektu:

[![15]][15]

#### <a name="conclusion"></a>Podsumowanie
Dodanie Hello site-to-site VPN hybrydowego sieci połączenia tooan sieci wirtualnej platformy Azure można rozszerzyć sieć lokalną hello na platformie Azure w bezpieczny sposób. Przy użyciu bramy sieci VPN platformy Azure z natywnego hello, ruchu jest IPSec szyfrowane i tras za pomocą hello Internet. Ponadto przy użyciu bramy sieci VPN platformy Azure hello zapewnić to opcja tanie (nie dodatkowych licencji koszt tak jak w przypadku innych firm NVAs). Ta opcja jest najbardziej ekonomiczne w przykładzie 1, gdzie są używane nie NVA. Aby uzyskać więcej informacji, zobacz hello szczegółowe instrukcje (nadchodzącego) kompilacji. Instrukcje te obejmują:

* Jak toobuild obwodowej ten przykład sieci za pomocą skryptów środowiska PowerShell.
* Jak toobuild w tym przykładzie z szablonem usługi Azure Resource Manager.
* Scenariusze przepływu ruchu szczegółowe, przedstawiający sposób ruch przechodzi przez ten projekt.

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>Przykład 6 Dodaj połączenie hybrydowe z usługi ExpressRoute
[Kopii tooFast start](#fast-start) | Szczegółowe instrukcje kompilacji jest dostępny wkrótce

[![16]][16]

#### <a name="environment-description"></a>Opis elementu środowiska
Sieci hybrydowe przy użyciu usługi ExpressRoute prywatnej komunikacji równorzędnej połączenia może być dodany typ sieci obwodowej tooeither opisanego w przykładach 1 lub 2.

Jak pokazano na powyższej ilustracji hello, prywatnej komunikacji równorzędnej ExpressRoute zawiera bezpośrednie połączenie między siecią lokalną a hello sieci wirtualnej platformy Azure. Ruch tranzytu tylko hello usługi dostawcy sieci i hello Microsoft Azure, nigdy nie dotknięcie hello Internet.

> [!TIP]
> Przy użyciu usługi ExpressRoute przechowuje ruchu w sieci firmowej poza hello Internet. Pozwala także umów dotyczących poziomu usług z dostawcy usługi ExpressRoute. Hello Azure bramy można przekazać się too10 GB/s z usługi ExpressRoute, natomiast hello Azure bramy maksymalną przepustowość sieci VPN typu lokacja lokacja, jest 200 MB/s.
>
>

Jak w powitania po diagramu z tej opcji hello środowiska ma teraz dwie krawędzie sieci. Witaj NVA i NSG kontroli ruch do sieci w obrębie platformy Azure i platformy Azure i hello Internetu, gdy bramy hello jest krawędzi oddzielne sieci między lokalną i platformą Azure.

Ruch należy rozważyć, jak mogą być optymalizowane lub ograniczone przez ten wzorzec projektowania, w zależności od określonych hello przypadek użycia.

Przy użyciu środowiska hello wbudowane w przykładzie 1, a następnie dodanie połączenia sieciowego hybrydowego usługi ExpressRoute, tworzy hello następującego projektu:

[![17]][17]

#### <a name="conclusion"></a>Podsumowanie
Dodanie Hello połączenie sieciowe w komunikacji równorzędnej ExpressRoute prywatnego można rozszerzyć sieć lokalną hello na platformie Azure w bezpieczny, dolna opóźnienia nowszego wykonywania sposób. Ponadto przy użyciu hello natywnego bramy Azure, jak w poniższym przykładzie zapewnia opcję tanie (Brak dodatkowych licencjonowania, podobnie jak w przypadku innych firm NVAs). Aby uzyskać więcej informacji, zobacz hello szczegółowe instrukcje (nadchodzącego) kompilacji. Instrukcje te obejmują:

* Jak toobuild obwodowej ten przykład sieci za pomocą skryptów środowiska PowerShell.
* Jak toobuild w tym przykładzie z szablonem usługi Azure Resource Manager.
* Scenariusze przepływu ruchu szczegółowe, przedstawiający sposób ruch przechodzi przez ten projekt.

## <a name="references"></a>Dokumentacja
### <a name="helpful-websites-and-documentation"></a>Przydatne witryn sieci Web i dokumentacji
* Dostęp do platformy Azure z usługą Azure Resource Manager:
* Uzyskiwanie dostępu do platformy Azure przy użyciu programu PowerShell: [https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* Dokumentacja sieci wirtualnych: [https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* Dokumentacja grupy zabezpieczeń sieci: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* Zdefiniowane przez użytkownika routingu dokumentacji: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Azure bram wirtualnego: [https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* Sieci VPN typu lokacja lokacja: [https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* Dokumentacja usługi ExpressRoute (być toocheck się się w sekcji "Wprowadzenie" i "How" hello): [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "Schemat blokowy opcji zabezpieczeń"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "funkcje zabezpieczeń platformy azure"
[3]: ./media/best-practices-network-security/dmzcorporate.png "DMZ A w sieci firmowej"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "architektury zabezpieczeń platformy azure"
[5]: ./media/best-practices-network-security/dmzazure.png "DMZ w sieci wirtualnej platformy Azure"
[6]: ./media/best-practices-network-security/dmzhybrid.png "sieci hybrydowe za pomocą trzech granic zabezpieczeń"
[7]: ./media/best-practices-network-security/example1design.png "Przychodzący DMZ z grupy NSG"
[8]: ./media/best-practices-network-security/example2design.png "Przychodzący DMZ NVA i grupy NSG"
[9]: ./media/best-practices-network-security/example3design.png "Dwukierunkowe DMZ NVA, NSG i przez"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "widok logiczny hello reguły zapory"
[11]: ./media/best-practices-network-security/example3designoptions.png "DMZ z NVA połączonych sieci hybrydowe"
[12]: ./media/best-practices-network-security/example4designs2s.png "DMZ z NVA nawiązano połączenie przy użyciu sieci VPN lokacja lokacja"
[13]: ./media/best-practices-network-security/example4networklogical.png "sieci logicznej z punktu widzenia NVA"
[14]: ./media/best-practices-network-security/example5designoptions.png "DMZ Azure bramy połączonej sieci hybrydowe lokacja lokacja"
[15]: ./media/best-practices-network-security/example5designs2s.png "DMZ Azure bramy przy użyciu sieci VPN lokacja lokacja"
[16]: ./media/best-practices-network-security/example6designoptions.png "DMZ Azure bramy połączonej sieci hybrydowe usługi ExpressRoute"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "DMZ Azure bramy przy użyciu połączenia ExpressRoute"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md
