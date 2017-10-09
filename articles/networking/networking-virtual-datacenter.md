---
title: aaaMicrosoft centrum danych Azure wirtualnej | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toobuild wirtualnego danych Centrum na platformie Azure"
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Wirtualne centrum danych platformy Microsoft Azure
**Microsoft Azure**: szybszą, oszczędności, integracja danych i aplikacji lokalnych

## <a name="overview"></a>Omówienie
Migracja lokalnych aplikacji tooAzure, nawet bez wprowadzania żadnych znaczących zmian (podejście jest ogólnie znana jako "przyrostu i przesunięcia"), pozwala organizacjom hello zalet infrastruktury zabezpieczonych i ekonomiczny sposób. Jednak najbardziej toomake hello z elastyczność hello przy użyciu rozwiązań w chmurze, przedsiębiorstw powinien rozwijać wykorzystują tootake architektury funkcji platformy Azure. Microsoft Azure oferuje hiperskali usług i infrastruktury, funkcje klasy korporacyjnej i niezawodność oraz wiele opcji na potrzeby łączności hybrydowej. Klienci mogą wybrać tooaccess albo za pośrednictwem usług w chmurze te hello Internet lub w Azure ExpressRoute, który zapewnia łączność w sieci prywatnej. Witaj platformy Microsoft Azure umożliwia klientom tooseamlessly rozszerzają infrastruktury do chmury hello i tworzenia wielu architektur. Ponadto partnerów firmy Microsoft zawiera udoskonalone funkcje za oferty usług zabezpieczeń i wirtualnych urządzeń, które są zoptymalizowane toorun na platformie Azure.

Ten artykuł zawiera omówienie wzorców i projekty, które mogą być używane toosolve hello architektury dotyczy skali, wydajności i zabezpieczeń czoła wielu klientów w przypadku o przenoszeniu będących masse toohello chmury. Przegląd sposobu toofit różnych organizacji IT ról do zarządzania hello i nadzór nad systemu hello również omówione, nacisk toosecurity wymagań i optymalizację kosztów.

## <a name="what-is-a-virtual-data-center"></a>Co to jest centrum danych wirtualnej?
W hello czasach, chmury rozwiązania zostały zaprojektowane toohost pojedynczego, stosunkowo izolowanego aplikacji, w publicznych spektrum hello. Takie podejście dobrze działały dla kilka lat. Jednak jako hello zalet chmury rozwiązań stała się oczywista i wiele obciążeń na dużą skalę zostały hostowanych w chmurze hello adresowania bezpieczeństwo, niezawodność, wydajność i kosztów dotyczy wdrożeń w jednym lub więcej regionów stał się niezbędne w całym hello cykl życiowy hello usługi w chmurze.

Witaj następujące chmury wdrożenia diagramie przedstawiono przykłady luk zabezpieczeń (czerwonym prostokątem) i miejsce dla optymalizacji sieci wirtualnych urządzeń między obciążeń (żółty pole).

[![0]][0]

urodziła Hello wirtualnej centrum danych (vDC) z tego konieczność skalowania obciążeń przedsiębiorstwa toosupport i hello potrzebne toodeal problemów hello wprowadzona podczas obsługi dużych aplikacji w chmurze publicznej hello.

VDC nie jest po prostu hello obciążeń aplikacji w chmurze hello, ale również hello sieci, zabezpieczeń, zarządzania i infrastruktury (na przykład, DNS i usługi katalogowe). Zwykle zapewnia także tooan wstecz prywatnego połączenia lokalnego Centrum sieci i danych. Coraz więcej obciążeń przenieść tooAzure, jest ważne toothink o hello obsługa infrastruktury i obiektów, które te obciążenia są umieszczane w. Analiza dokładnie struktury zasobów można uniknąć hello mnożenie setki "obciążenie Wyspy", które muszą być zarządzane oddzielnie z przepływu danych niezależnych, modele zabezpieczeń i zgodności wyzwania.

Centrum danych wirtualnej jest zasadniczo zbiór jednostek oddzielnej, ale powiązane z typowych funkcji pomocniczych, funkcje i infrastruktury. Wyświetlając obciążeń jako vDC zintegrowanego, można zrealizować zmniejszenie kosztów powodu centralizacji wraz z łatwiejsze operacje, zarządzania i zgodności kontroli przepływu tooeconomies skali, zoptymalizowane zabezpieczeń za pomocą składnika i danych.

> [!NOTE]
> Ważne jest, był toounderstand, który hello vDC **nie** odrębny produktu Azure, ale hello kombinacją różnych funkcji i możliwości zbyt zgodnie z wymaganiami dokładne. vDC to metoda pomyśleć o obciążeń i użycia Azure toomaximize wszystkie zasoby i możliwości w chmurze hello. Witaj wirtualny kontroler domeny jest w związku z tym podejściu na temat toobuild usług IT w hello Azure przestrzeganie organizacyjnej role i obowiązki.

Hello vDC mogą pomóc w przedsiębiorstwach uzyskać hello następujące scenariusze obciążeń i aplikacji na platformie Azure:

-   Obsługa wielu powiązanych obciążeń pracą
-   Migrowanie obciążeń z tooAzure środowiska lokalnego
-   Wdrażanie udostępnionego lub scentralizowanych zabezpieczeń i wymagania dotyczące dostępu między obciążeń
-   Mieszanie DevOps i scentralizowane IT odpowiednio dla dużych przedsiębiorstw

Witaj klucza toounlock hello zalet vDC, scentralizowane topologii (koncentrator i klienci) za pomocą różnych funkcje platformy Azure: [sieci wirtualnej Azure][VNet], [grup NSG] [ NSG], [Sieci wirtualnej komunikacji równorzędnej][VNetPeering], [trasy zdefiniowane przez użytkownika (przez)][UDR], a tożsamość platformy Azure z [ Kontrolę dostępu na podstawie ról (RBAC)][RBAC].

## <a name="who-needs-a-virtual-data-center"></a>Który musi wirtualnego centrum danych?
Dowolnego klienta Azure, wymagającym toomove więcej niż kilka obciążeń na platformie Azure mogą korzystać z myślenia o za pomocą wspólnych zasobów. W zależności od wielkości hello nawet pojedyncze aplikacje mogą korzystać z wzorców hello i składniki używane toobuild vDC.

Jeśli Twoja organizacja ma scentralizowanych zabezpieczeń IT, sieci, i/lub team/dział kontroli zgodności, vDC może pomóc wymusić zasady punktów podziału należności i zapewnić jednolitość hello podstawowych składników wspólne podczas przekazywania zespoły aplikacji jako znacznie swobodę i kontroli, ponieważ jest odpowiednią do wymagań.

Organizacje, które chce się dowiedzieć, tooDevOps mogą wykorzystywać hello vDC pojęcia tooprovide autoryzowany kieszeni zasobów platformy Azure i upewnij się, mają pełną kontrolę w grupie (albo subskrypcji lub grupy zasobów w subskrypcji wspólnej), ale hello sieci i granice zabezpieczeń pozostają zgodne, zgodnie z definicją w scentralizowanych zasad w Centrum sieci i grupy zasobów.

## <a name="considerations-on-implementing-a-virtual-data-center"></a>Uwagi dotyczące implementacji wirtualnego centrum danych
Podczas projektowania vDC, istnieje kilka tooconsider kluczową problemy:

-   Tożsamości i usług katalogowych
-   Infrastruktura zabezpieczeń
-   Łączność toohello chmury
-   Łączność w chmurze hello

##### <a name="identity-and-directory-service"></a>*Tożsamości i usługi katalogowej*
Tożsamości i usługi katalogowe są kluczowym aspektem wszystkie dane w centrach, zarówno lokalnie i w chmurze hello. Tożsamość jest powiązane tooall aspektów tooservices dostępu i autoryzacja w hello vDC. toohelp Sprawdź, czy tylko autoryzowani użytkownicy i procesy dostęp do konta platformy Azure i zasobów, Azure używa kilku typów poświadczeń do uwierzytelniania. Obejmują one hasła (tooaccess hello konto platformy Azure), kluczy kryptograficznych podpisów cyfrowych i certyfikatów. [*Usługa Azure Multi-Factor Authentication* (MFA)] [ MFA] jest dodatkową warstwę zabezpieczeń do uzyskiwania dostępu do usług platformy Azure. Usługa Azure MFA zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe — połączenie telefoniczne, wiadomość tekstowa lub powiadomienie aplikacji mobilnej — i umożliwiają klientom metody hello toochoose preferowany.

Wszystkie duże przedsiębiorstwo musi toodefine procesu zarządzania tożsamościami, opisujący hello Zarządzanie tożsamościami poszczególnych, ich uwierzytelniania, autoryzacji, role i uprawnienia lub wielu hello vDC. Witaj cele tego procesu należy tooincrease bezpieczeństwo i wydajność przy jednoczesnym ograniczeniu kosztów, czasem przestoju oraz powtarzające się zadania ręczne.

Enterprise/organizacje mogą wymagać różnych wymagających usług dla różnych wiersza elementu firm obiektów (LOB), a pracownicy często mają różne role w przypadku z różnych projektów. VDC wymaga dobrej współpracy między zespołami różnych, każdy z definicjami określoną rolę, tooget systemami z dobrego zarządzania. macierzy Hello obowiązki, dostępu i prawa mogą być bardzo skomplikowane. Zarządzanie tożsamościami w vDC jest implementowane za pośrednictwem [ *usługi Azure Active Directory* (AAD)] [ AAD] i kontroli dostępu opartej na rolach (RBAC).

Usługa katalogowa jest informacje udostępniane w infrastrukturze lokalizowanie, zarządzanie administrowanie i organizowanie elementów codziennie i zasobów sieciowych. Te zasoby mogą obejmować woluminów, folderów, plików, drukarek, użytkowników, grup, urządzeń i innych obiektów. Każdy zasób w sieci hello jest uznawany za obiektu przez serwer katalogowy hello. Informacje o zasobie jest przechowywana jako kolekcja atrybutów skojarzona z tego zasobu lub obiektu.

Wszystkie usługi biznesowe online firmy Microsoft polega na usługi Azure Active Directory (AAD) dla logowania i wymaga innych tożsamości. Usługa Azure Active Directory to kompleksowe rozwiązanie o wysokiej dostępności do zarządzania tożsamościami i dostępem w chmurze, które oferuje podstawowe usługi katalogowe, zaawansowane funkcje zarządzania tożsamościami i zarządzania dostępem do aplikacji. AAD można zintegrować z lokalną usługą Active Directory tooenable pojedynczego logowania dla wszystkich opartych na chmurze i lokalnie obsługiwanych aplikacji (lokalnego). atrybuty użytkownika Hello lokalnej usługi Active Directory mogą być automatycznie synchronizowane tooAAD.

Jednego administratora globalnego jest wszystkie uprawnienia w vDC tooassign nie jest wymagane. Zamiast tego każdego określonego działu (lub grupy użytkowników lub usług w hello usługi katalogowej) może mieć toomanage wymagane uprawnienia hello własnych zasobów w ramach vDC. Struktura uprawnień wymaga równoważenia. Zbyt wiele uprawnień, co może utrudniać wydajności wydajności i zbyt mało utracić uprawnienia można zwiększyć za zagrożenie bezpieczeństwa. Azure opartej na rolach kontroli dostępu (RBAC) pomaga tooaddress ten problem, oferując precyzyjne zarządzanie dostępem do zasobów vDC.

##### <a name="security-infrastructure"></a>*Infrastruktura zabezpieczeń*
Infrastruktura zabezpieczeń w kontekście hello vDC, jest głównie toohello powiązane podział hello vDC segmentu określonej sieci wirtualnej, i jak toocontrol przychodzące i wychodzące przepływy w całym hello vDC. Azure jest oparty na architekturze wielodostępne, który uniemożliwia nieautoryzowanym oraz niezamierzonych ruchu między wdrożeniami, przy użyciu izolacji sieci wirtualnej (VNet), listy kontroli dostępu (ACL), obciążenia równoważenia i filtry IP wraz z zasadami przepływu ruchu. Translator adresów sieciowych (NAT) oddziela ruchu w sieci wewnętrznej od zewnętrznego ruchu.

Witaj sieci szkieletowej Azure przydziela zasoby infrastruktury tootenant obciążeń i zarządza tooand komunikacji z maszyn wirtualnych (VM). Hello Azure funkcji hypervisor wymusza pamięci i procesu rozdzielenie maszyn wirtualnych i bezpiecznie trasy sieciowe ruchu tooguest OS dzierżaw.

##### <a name="connectivity-toohello-cloud"></a>*Łączność toohello chmury*
Witaj vDC musi mieć łączność z sieci zewnętrznych toooffer usług toocustomers, partnerzy i/lub użytkowników wewnętrznych. Zwykle oznacza to połączenie nie tylko toohello internetowych, ale również tooon lokalnej sieci i w centrum danych.

Klientom tworzenie ich toocontrol zasady zabezpieczeń, co i jak określonych vDC hostowanych usług są dostępne z Internetem przy użyciu sieci wirtualnych urządzeń (za pomocą filtrowania ruchu i inspekcji) i niestandardowych zasad routingu i sieci (filtrowania hello Routing zdefiniowane przez użytkownika i grupy zabezpieczeń sieci).

Przedsiębiorstwa często muszą centrów danych lokalnych tooon VDC tooconnect lub innych zasobów. Hello łączności między sieciami Azure i lokalnymi w związku z tym jest kluczowy aspekt podczas projektowania architektury skuteczne. Przedsiębiorstwach istnieją dwa różne sposoby toocreate połączenia między vDC i lokalnej na platformie Azure: przesyłania za pośrednictwem hello Internet i/lub prywatnej połączeń bezpośrednich.

[ **Azure VPN lokacja-lokacja** ] [ VPN] jest usługą połączeń za pośrednictwem hello Internet między sieciami lokalnymi i szyfrowane vDC hello, nawiązane za pośrednictwem bezpiecznego połączenia (tuneli IPsec i IKE). Azure połączenia lokacja-lokacja jest toocreate elastyczne, szybkie i nie wymaga żadnych dalszych zamówień, jak połączenia za pośrednictwem Internetu hello.

[**ExpressRoute** ] [ ExR] jest usługą łączności Azure, która umożliwia tworzenie prywatnych połączeń między vDC i hello sieci lokalnej. Połączenia ExpressRoute nie przechodzą ponad hello publicznej sieci Internet i oferują wyższy poziom zabezpieczeń, niezawodności i większe szybkości (up too10 GB/s) oraz spójne opóźnienia. ExpressRoute jest bardzo przydatna dla VDC, jak klienci mogą uzyskać hello zalet reguły zgodności skojarzone z prywatnych połączeń ExpressRoute.

Wdrażanie połączenia ExpressRoute obejmuje współpraca przy użyciu dostawcy usługi ExpressRoute. Dla użytkowników, którzy muszą toostart szybko go jest powszechne zastosowanie tooinitially sieci VPN typu lokacja-lokacja tooestablish łączności między zasobami vDC i lokalne powitania, a następnie przeprowadzić migrację tooExpressRoute połączenia.

##### <a name="connectivity-within-hello-cloud"></a>*Łączność w chmurze hello*
[Sieci wirtualne] [ VNet] i [sieci wirtualnej komunikacji równorzędnej] [ VNetPeering] są hello podstawowe sieci usług łączności wewnątrz vDC. Fizyczne granic izolacji zasobów vDC gwarantuje sieci wirtualnej i sieci wirtualnej komunikacji równorzędnej pozwala wzajemnego komunikowania między różnych sieci wirtualnych w ramach hello tego samego regionu systemu Azure. Kontrola ruchu w sieci wirtualnej i między sieciami wirtualnymi należy toomatch zestaw zabezpieczeń reguły określone za pomocą list kontroli dostępu ([sieciowej grupy zabezpieczeń][NSG]), [wirtualnych urządzeń sieciowych ] [ NVA]i niestandardowe tabele routingu ([przez][UDR]).

## <a name="virtual-data-center-overview"></a>Omówienie wirtualnych centrum danych

### <a name="topology"></a>Topologia
Koncentrator i partnerzy modelu rozszerzonej hello wirtualnej centrum danych w pojedynczym regionie Azure

[![1]][1]

Koncentrator Hello jest hello strefy centralnej, która określa i sprawdza ruch przychodzący lub wychodzący ruch między różnymi strefami: Internetu, lokalnego, i hello partnerów. topologia gwiazdy Hello daje hello dział IT efektywny sposób tooenforce zasad zabezpieczeń stosowanych w centralnej lokalizacji, przy jednoczesnym zmniejszeniu hello ryzyko błędnej konfiguracji i ekspozycji.

Koncentrator Hello zawiera hello używane przez partnerów hello wspólnych składników usługi. Poniżej przedstawiono kilka typowych przykładów typowych centralnej usług:

-   Infrastruktura usługi Active Directory systemu Windows Hello (z hello dotyczących usług AD FS) wymagane do uwierzytelniania użytkowników osób trzecich, uzyskiwanie dostępu z niezaufanych sieci przed uzyskiwania dostępu do toohello obciążeń w hello gwiazdy
-   Tooresolve usługi DNS nazewnictwa dla obciążenia hello w partnerzy hello, tooaccess zasobów lokalnych i na powitania Internet
-   Infrastruktury kluczy publicznych, tooimplement rejestracji jednokrotnej w obciążeń
-   Sterowanie przepływem (TCP/UDP) między hello partnerzy i Internet
-   Sterowanie przepływem między hello gwiazdy i lokalnych
-   W razie potrzeby przepływu sterowania między jeden gwiazdy

Witaj vDC zmniejsza całkowity koszt przy użyciu infrastruktury udostępnionej Centrum powitania od wielu partnerów.

Rola Hello każdego gwiazdy można toohost różne rodzaje obciążeń. Witaj partnerzy można też podać podejściu powtarzalnych wdrożeń (na przykład deweloperów i testowania, testów akceptacyjnych przez użytkowników, produkcji wstępnej i produkcji) z hello obciążeń tego samego. partnerzy Hello można również być toosegregate używane i włączyć różnych grup w organizacji (na przykład grupy DevOps). Wewnątrz gwiazdy jest możliwe toodeploy podstawowe obciążenie lub złożonych obciążeń wielowarstwową z ruchem formant między warstwami hello.

##### <a name="subscription-limits-and-multiple-hubs"></a>Limity subskrypcji i wiele centrów
Na platformie Azure co składnik, niezależnie od typu hello jest wdrażane w subskrypcji platformy Azure. Izolacja Hello Azure składników w innej subskrypcji platformy Azure można spełnić wymagań hello różnych obiektów LOB, takich jak konfigurowanie różne poziomy dostępu i autoryzacja.

Pojedynczy vDC można skalować toolarge liczby partnerów, mimo że, podobnie jak w przypadku każdego systemu IT są limity platform. Witaj wdrożenia Centrum jest powiązane tooa określonych subskrypcję Azure, która ma ograniczenia i limity (na przykład, zobacz maksymalna liczba komunikacji równorzędnych sieci wirtualnej - [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia] [ Limits] szczegółowe informacje). W przypadku, gdy limity może się problemu, hello architektury można skalować się dalsze przez rozszerzanie modelu hello z klastra tooa pojedynczego partnerzy Centrum koncentratora i klienci. Wiele koncentratorów w co najmniej jeden regiony platformy Azure mogą wzajemnie połączone za pomocą Express Route lub sieci VPN typu lokacja lokacja.

[![2]][2]

Witaj wprowadzenia wiele koncentratorów powoduje zwiększenie kosztów i zarządzania nakładu hello hello systemu i jest uzasadnione tylko przez skalowalność (przykłady: limity systemu lub nadmiarowości) i regionalnych replikacji (przykłady: wydajności lub awaryjnego odzyskiwania przez użytkownika końcowego). W scenariuszach wymagających wielu centrów wszystkie koncentratory hello należy dążyć hello toooffer sam zestaw usług w celu ułatwienia operacyjne.

##### <a name="interconnection-between-spokes"></a>Połączenie między partnerzy
Wewnątrz jednej gwiazdy jest możliwe tooimplement złożonych wielu warstw obciążeń. Konfiguracje wielowarstwowych można zaimplementować w tej samej sieci wirtualnej i filtrowania hello przepływa za pomocą grup NSG hello przy użyciu podsieci (po jednym dla każdej warstwy).

Na hello drugiej strony, architektów może być toodeploy wielowarstwowych obciążenia między wieloma sieciami wirtualnymi. Za pomocą sieci równorzędne — klienci mogą podłączyć partnerzy tooother w hello koncentratora tej samej lub różnych koncentratorów. Typowym przykładem ten scenariusz jest przypadek hello, gdzie serwery przetwarzania aplikacji znajdują się w jednym gwiazdy (VNet), podczas wdrażania hello bazy danych w różnych gwiazdy (VNet). W takim przypadku jest łatwe toointerconnect hello partnerzy z sieci wirtualnej komunikacji równorzędnej i tym samym uniknąć przejeżdżających przez za pośrednictwem Centrum hello. Dokładne Przegląd architekturze i zabezpieczeniach powinna być wykonywana tooensure, który pomijanie Centrum hello nie obejścia ważne zabezpieczeń lub inspekcji punktów, które mogą znajdować się tylko w Centrum hello.

[![3]][3]

Klienci mogą być również gwiazdy połączonych tooa, która pełni funkcję Centrum. Ta metoda tworzy dwupoziomowej hierarchii: hello gwiazdy w hello wyższego poziomu (poziom 0), stają się hello koncentratora o niższych partnerzy (poziom 1) hello hierarchii. partnerzy Hello z vDC muszą tooforward hello ruchu toohello centralnego tooreach toohello lokalnej sieci lub Internetu. Architektura o dwa poziomy Centrum wprowadza złożonego routingu, która usuwa korzyści hello relacji proste Gwiazda.

Mimo że Azure umożliwia złożonej topologii, jednym z hello podstawowe zasady koncepcji vDC hello jest powtarzalność i prostota. toominimize zarządzania wysiłku, projekt proste Gwiazda hello jest hello zalecane architektura referencyjna vDC.

### <a name="components"></a>Składniki
Centrum danych wirtualnej składa się z czterech typów podstawowych składników: **infrastruktury**, **sieci obwodowej**, **obciążeń**, i **monitorowanie**.

Każdy typ składnika składa się z różnych funkcji platformy Azure i zasobów. Twoje vDC składa się z wystąpień wiele typów składników i wiele zmian hello sam typ składnika. Na przykład może istnieć wiele wystąpień innych, logicznie rozdzielonych obciążenia, które reprezentują różnych aplikacji. Używanie tych typów różnych składników i wystąpień tooultimately kompilacji hello vDC.

[![4]][4]

Hello poprzedniego Architektura wysokiego poziomu vDC zawiera typy różnych składników używane w różnych strefach hello partnerzy Centrum topologii. Witaj diagram przedstawia składników infrastruktury w różnych części hello architektury.

Dostęp dobrym rozwiązaniem (dla kontrolera domeny z lokalnymi lub vDC) praw i uprawnień powinna być oparte na grupach. Dotyczących grupy zamiast poszczególnych użytkowników pomaga konserwacji zasad dostępu spójnie między zespołami i pomocy w przypadku minimalizowania błędów konfiguracji. Przypisywanie i usuwanie użytkowników tooand pomaga odpowiednich grup, aktualizując hello uprawnienia określonego użytkownika.

Każda grupa roli musi mieć unikatowy prefiks we ich nazw, dzięki czemu można łatwo tooidentify grupy, do której jest skojarzony z którym obciążenie. Na przykład obciążenie usługi uwierzytelniania hosta może być grupy o nazwie *AuthServiceNetOps, AuthServiceSecOps AuthServiceDevOps i AuthServiceInfraOps.* Podobnie dla scentralizowane ról lub ról nie związane z tooa określonej usługi, może być poprzedzone znakiem "Corp" *CorpNetOps* np.

Wiele organizacji korzysta z odmianą hello następujące grupy tooprovide poważnej awarii ról:

-   Witaj *centralna grupa IT (Corp)* hello własność prawa toocontrol infrastruktury (na przykład sieci i zabezpieczeń) składniki i dlatego wymaga toohave hello roli współautora na powitania subskrypcji (i mają kontrolę nad Koncentrator Hello) i uprawnienia współautora w hello klienci sieci. Dużej organizacji często podzielić te obowiązki zarządzania między kilka zespołów, takich jak; Operacje sieciowe (CorpNetOps) grupy (wyłączne fokus na obsługę sieci) i grupy operacje zabezpieczeń (CorpSecOps) (odpowiedzialny za zasad zapory i zabezpieczeń). W tym przypadku określone dwie różne grupy muszą toobe utworzone dla przypisania tych ról niestandardowych.
-   Witaj *deweloperów & Grupa testowa (AppDevOps)* ma hello odpowiedzialność toodeploy obciążeń (aplikacji lub usługi). Ta grupa ma hello rolę współautora maszyny wirtualnej dla wdrożenia IaaS i/lub jeden lub więcej współautora PaaS ról (zobacz [wbudowanych ról dla kontroli dostępu][Roles]). Opcjonalnie hello deweloperów & zespół może być konieczne widoczność toohave zasady zabezpieczeń (NSG) oraz zasady routingu (przez) wewnątrz Centrum hello lub określonych gwiazdy. W związku z tym z rolami toohello dodanie współautora dla obciążeń, tej grupy należy hello roli czytnika danych sieciowych.
-   Witaj *grupy operacji i konserwacji (CorpInfraOps lub AppInfraOps)* odpowiadają hello zarządzania obciążeń w środowisku produkcyjnym. Ta grupa wymaga toobe subskrypcji współautorem obciążeń w żadnych subskrypcji produkcji. Niektóre organizacje mogą również ocenić, czy potrzebują dodatkowych eskalacji pomocy technicznej zespół grupy z rolą hello Współautor subskrypcji w środowisku produkcyjnym i hello centralnego subskrypcji, w kolejności toofix potencjalnych problemów z konfiguracją w środowisku produkcyjnym hello środowisko.

VDC mają strukturę, dzięki czemu grup utworzonych dla hello centralnej grup IT zarządzanie Centrum hello mają odpowiednie grupy na poziomie obciążenia hello. Ponadto toomanaging zasobów tylko hello centralnej IT grup koncentratorów będzie toocontrol stanie dostępu zewnętrznego i najwyższego poziomu uprawnień na powitania subskrypcji. Jednak grupy obciążenia będą mogli toocontrol zasobów i uprawnień, ich sieci wirtualnej niezależnie w centralnym dziale IT.

Witaj vDC potrzeb toobe podzielonym na partycje hosta toosecurely wielu projektów w różne wiersza elementu przedsiębiorstwa (obiektów LOB). Wszystkie projekty wymagają różnych środowiskach izolowanego (deweloperów, UAT, produkcyjnego). Oddzielne subskrypcji platformy Azure dla każdego z tych środowisk zapewniają izolację fizycznych.

[![5]][5]

Hello wcześniejszym diagramie przedstawiono hello relacje między projektami, użytkowników, grup i środowisk hello gdzie hello Azure składniki są wdrażane w organizacji.

Zwykle w IT, środowisko (lub warstwy) jest system, w którym wiele aplikacji są wdrożone i są stosowane. Duże przedsiębiorstwa Użyj środowisko projektowe (gdzie zmiany pierwotnie wprowadzone i przetestowane) i środowiska produkcyjnego (co użytkownicy końcowi używają). Tych środowisk są często oddzielone z kilku środowiska Between ich przejściowe tooallow stopniowo wdrożenia (wdrażanie), testowania i wycofania w razie problemów. Wdrożenia architektury różnić, ale zazwyczaj nadal występuje hello podstawowy proces, zaczynając od rozwoju (deweloperów) i koniec (produkcyjną) w środowisku produkcyjnym.

Architektura dla tych typów środowisk wielowarstwowych składa się z DevOps (projektowania i testowania), UAT (środowisko przejściowe) i środowisk produkcyjnych. Organizacje mogą korzystać z jednego lub wielu usługi Azure AD dzierżawy środowiska toothese toodefine dostępu i praw. Witaj poprzedni diagram przedstawia przypadek w przypadku, gdy dwa różne służą dzierżaw usługi Azure AD: jeden dla DevOps i UAT i hello innych wyłącznie w środowisku produkcyjnym.

Witaj obecności innej usługi Azure AD dzierżaw wymusza hello separacji między środowiskami. Witaj tej samej grupy użytkowników (na przykład centralnym dziale IT) wymaga tooauthenticate przy użyciu różnych tooaccess URI innej dzierżawy AD zmodyfikować hello ról lub uprawnień albo hello DevOps i środowisk produkcyjnych projektu. obecność Hello inny użytkownik uwierzytelniania tooaccess różnych środowiskach zmniejsza możliwe awarie i inne problemy spowodowane przez błędy człowieka.

#### <a name="component-type-infrastructure"></a>Typ składnika: infrastruktury
Ten typ składnika jest, gdzie znajduje się większość hello infrastruktura pomocnicza. Istnieje również gdzie Twoje scentralizowane IT, zabezpieczeń, i/lub zgodności zespoły poświęcają większość czasu.

[![6]][6]

Składniki infrastruktury zapewniają połączenia między poszczególnymi składnikami vDC hello i znajdują się w Centrum hello i partnerzy hello. Hello odpowiedzialności za zarządzanie i obsługę składników infrastruktury hello jest zwykle przypisany centralnego toohello IT i/lub zespołu ochrony obiektu.

Jednym z hello podstawowych zadań z hello zespołu infrastruktury IT jest spójności hello tooguarantee Schematy adresów IP dla przedsiębiorstwa hello. Hello prywatnego adresu IP adres miejsca przypisane toohello vDC musi toobe spójne i nie nakładać się na prywatne adresy IP przypisane w sieci lokalnej.

Gdy translatora adresów Sieciowych na powitania routery brzegowe lokalnymi lub na platformie Azure środowisk można uniknąć konfliktów adresów IP, dodaje składników infrastruktury tooyour komplikacje. Łatwość zarządzania jest jeden z podstawowych celów vDC, hello, dlatego używanie dotyczy IP toohandle NAT nie jest zalecane rozwiązanie.

Składniki infrastruktury zawierają hello następujące funkcje:

-   [**Tożsamości i usługi katalogowe**][AAD]. Typ zasobu tooevery dostępu na platformie Azure jest kontrolowana przez tożsamości przechowywane w usłudze katalogowej. Magazyny usług directory Hello nie tylko hello listę użytkowników, ale również hello tooresources prawa dostępu w określonej subskrypcji platformy Azure. Te usługi może istnieć tylko na chmurze lub mogą być synchronizowane z tożsamością lokalnie przechowywane w usłudze Active Directory.
-   [**Sieć wirtualna**][VPN]. Sieci wirtualne są jednym z głównych składników vDC i włączyć toocreate granica izolacji ruchu na powitania platformy Azure. Sieć wirtualna składa się z jednym lub wielu segmentach sieci wirtualnej, każda z określonego adresu IP prefiksu sieci (podsieci). Hello sieci wirtualnej definiuje obszar obwodowej wewnętrznego, gdy maszyny wirtualne IaaS i PaaS usługi może nawiązać komunikacji prywatnej. Maszyny wirtualne (i usługi PaaS) w jednej sieci wirtualnej nie może komunikować się bezpośrednio tooVMs (i usługi PaaS) w innej sieci wirtualnej, nawet jeśli obie sieci wirtualne są tworzone przez hello tego samego klienta, w obszarze hello tej samej subskrypcji. Izolacja jest krytyczne właściwość, która zapewnia klienta maszyn wirtualnych i komunikacja pozostanie prywatnej sieci wirtualnej.
-   [**PRZEZ**][UDR]. Ruch w sieci wirtualnej jest kierowany przez domyślne na podstawie tabeli routingu hello systemu. Zdefiniuj użytkownika trasy jest niestandardowe tabeli routingu, że administratorzy sieci można skojarzyć tooone lub więcej podsieci toooverwrite hello zachowanie tabeli routingu hello systemu i zdefiniuj ścieżki komunikacji w ramach sieci wirtualnej. obecność Hello Udr gwarancje ruch wychodzący z hello gwiazdy przesyłania za pośrednictwem określonego niestandardowego maszyn wirtualnych i/lub wirtualnych urządzeń sieciowych i występuje w Centrum hello i partnerzy hello usługi równoważenia obciążenia.
-   [**GRUPA NSG**][NSG]. Grupa zabezpieczeń sieci znajduje się lista reguł zabezpieczeń, które działają jako ruchu filtrowania portów IP źródła, docelowego adresu IP, protokołów, portów IP źródłowego i docelowego adresu IP. Hello NSG może być zastosowane tooa podsieci, karty wirtualnej karty Sieciowej, skojarzonych z maszyny Wirtualnej platformy Azure lub oba. grupy NSG Hello są istotne tooimplement formantu prawidłowego przepływu w Centrum hello i partnerzy hello. Witaj poziom zabezpieczeń oferowanych przez hello NSG to funkcja otwierania portów i w jaki celu. Klientów należy zastosować filtry wirtualna dodatkowych z zapory oparta na hoście, takie jak IPtables lub hello zapory systemu Windows.
-   **DNS**. Witaj rozpoznawania nazw zasobów w sieci wirtualnych z vDC hello podano przy użyciu systemu DNS. zakres Hello rozpoznawanie nazwy domyślnej hello DNS jest ograniczona toohello sieci wirtualnej. Zazwyczaj niestandardowe usługi DNS wymaga toobe wdrożone w Centrum hello jako część wspólne usługi, ale hello konsumentów głównych usług DNS znajdują się w hello gwiazdy. Jeśli to konieczne, klienci mogą tworzyć strukturę hierarchiczną DNS z delegowania partnerzy toohello strefy DNS.
-   [** Subskrypcji] [ SubMgmt] i [zarządzania grupy zasobów][RGMgmt]**. Subskrypcja definiuje toocreate fizyczną granic wiele grup zasobów na platformie Azure. Zasobów w subskrypcji są łączone ze sobą w kontenerach logiczną o nazwie grupy zasobów. Witaj grupy zasobów reprezentuje vDC zasobów hello tooorganize logiczne grupy.
-   [**RBAC**][RBAC]. Za pomocą RBAC jest możliwe toomap ról organizacyjnych wraz z prawami tooaccess określonych zasobów platformy Azure, dzięki czemu możesz toorestrict użytkowników tooonly podzbioru akcje. Z RBAC można przyznać dostęp, przypisując hello toousers odpowiedniej roli, grupy i aplikacje w zakresie odpowiednich hello. Witaj zakres przypisania roli może być pojedynczego zasobu, grupy zasobów lub subskrypcji platformy Azure. RBAC umożliwia dziedziczenie uprawnień. Rola przypisana w zakresie nadrzędnej również udziela dostępu toohello dzieci w nim zawarte. Przy użyciu funkcji RBAC, można rozdzielenie obowiązków i udzielić tylko hello ilość toousers dostępu do potrzebnych tooperform swoich zadań. Na przykład użyj RBAC toolet jednego pracownika zarządzać maszyn wirtualnych w ramach subskrypcji, gdy inny zarządzania bazami danych SQL, w ramach hello tej samej subskrypcji.
-   [**Sieci wirtualnej komunikacji równorzędnej**][VNetPeering]. Witaj podstawowych funkcji używany toocreate hello infrastruktury vDC jest sieci wirtualnej komunikacji równorzędnej, mechanizm, który łączy dwie sieci wirtualnych (sieci wirtualne) w hello tego samego regionu za pośrednictwem sieci hello hello centrum danych Azure.

#### <a name="component-type-perimeter-networks"></a>Typ składnika: Sieci obwodowej
[Sieć obwodowa] [ DMZ] składników (znanej także jako sieci DMZ) pozwalają tooprovide łączności sieciowej z lokalnej lub w sieci centrum danych fizycznych, wraz z dowolnego tooand łączności z hello Internet. Istnieje również gdy zespoły sieciowe i zabezpieczeń może poświęcać większość czasu.

Pakiety przychodzące powinny przepływać przez hello urządzenia zabezpieczeń w Centrum hello, takie jak zapory hello, identyfikatorów i adresów IP, przed dotrze do serwerów zaplecza hello w hello partnerów. Pakiety powiązane z Internetu od obciążeń hello powinny również przepływać przez hello urządzenia zabezpieczeń w sieci obwodowej hello do wymuszania zasad inspekcji i inspekcji, przed opuszczeniem hello sieci.

Składniki sieci obwodowej zawierają hello następujące funkcje:

-   [Sieci wirtualne][VNet], [przez][UDR], [NSG][NSG]
-   [Urządzenie wirtualne sieci][NVA]
-   [Usługa równoważenia obciążenia][ALB]
-   [Brama aplikacji w][AppGW] / [zapory aplikacji sieci Web][WAF]
-   [Publiczne adresy IP][PIP]

Zazwyczaj hello centralnej IT i zespoły zabezpieczeń mają odpowiedzialność za definicja wymagania i operacje hello sieci obwodowej.

[![7]][7]

Witaj poprzedni diagram przedstawia wymuszania hello z dwóch strefy z toohello dostępu internet i lokalnej sieci, zarówno w Centrum hello. W jednego koncentratora toointernet sieci obwodowej hello można skalować toosupport dużą liczbą obiektów LOB, za pomocą wielu farmach zapór aplikacji sieci Web (WAFs) i/lub zapory.

[**Sieci wirtualne** ] [ VNet] Centrum hello zazwyczaj jest tworzony w sieci wirtualnej z wielu podsieci toohost hello innego typu usługi filtrowania i zapoznanie się tooor ruchu z Internetu za pośrednictwem NVAs, WAFs, hello i bram aplikacji Azure.

[**PRZEZ** ] [ UDR] przy użyciu przez, klienci mogą wdrożyć zapór, Identyfikatory/adresów IP i innych urządzeń wirtualnych i kierować ruchem sieciowym za pomocą tych urządzeń zabezpieczeń do wymuszania zasad granic zabezpieczeń, Inspekcja i inspekcji. Udr mogą być tworzone w obu hello koncentratora i hello partnerzy tooguarantee który tranzytów ruchu przez hello określonych niestandardowych maszyn wirtualnych, sieci wirtualnych urządzeń i moduły równoważenia obciążenia używane przez hello vDC. tooguarantee który ruch jest generowany na podstawie maszyn wirtualnych znajdują się w hello gwiazdy przesyłania toohello poprawne urządzenie wirtualne, przez musi toobe ustawiony w podsieciach hello gwiazdy hello przez ustawienie hello adres IP frontonu modułu równoważenia obciążenia wewnętrznego hello hello następnego przeskoku. Witaj wewnętrznego modułu równoważenia obciążenia dystrybuuje hello ruchu wewnętrznej toohello urządzenie wirtualne (puli zaplecza modułu równoważenia obciążenia).

[![8]][8]

[**Sieci wirtualnych urządzeń** ] [ NVA] w Centrum hello hello sieci obwodowej z toohello dostęp do Internetu zwykle odbywa się za pośrednictwem zapór i/lub zapór aplikacji sieci Web (WAFs) na farmie.

Różnych obiektów LOB często używanych wiele aplikacji sieci web, a te aplikacje często toosuffer z różnych luk w zabezpieczeniach i potencjalnych luk w zabezpieczeniach. Zapory aplikacji sieci Web to specjalny rodzaj produktu używany toodetect ataków na aplikacje sieci web (HTTP/HTTPS) bardziej szczegółowo niż ogólny zapory. W porównaniu z technologii zapory tradycji WAFs ma zestaw serwerów sieci web wewnętrznej tooprotect określonych funkcji przed zagrożeniami.

Farma zapory jest grupa zapór praca wspólnie w obszarze hello tego samego wspólnego zarządzania z zestawem obciążeń hello tooprotect reguły zabezpieczeń obsługiwane w hello partnerzy i kontroli dostępu lokalnego tooon sieci. Farma zapory ma mniej specjalizowany oprogramowania w porównaniu z zapory aplikacji sieci Web, ale ma aplikacją szeroki zakres toofilter i sprawdzić dowolnego typu ruch wychodzący i przychodzący. Zapora farm zwykle są implementowane na platformie Azure za pośrednictwem sieci wirtualnych urządzeń (NVAs), które są dostępne w hello Azure marketplace.

Zalecane jest toouse jeden zestaw NVAs dla ruchu pochodzącego na powitania Internet, a drugą dla ruchu pochodzącego lokalnymi. Przy użyciu tylko jeden zestaw NVAs zarówno stanowi zagrożenie bezpieczeństwa, ponieważ zapewnia nie granicznej zabezpieczeń między dwoma zestawami hello ruchu sieciowego. Przy użyciu osobnych NVAs zmniejsza się złożoność hello sprawdzanie zasad zabezpieczeń i czyni go wyczyścić reguły odpowiada toowhich przychodzących żądań sieci.

Najbardziej dużych przedsiębiorstw Zarządzanie wielu domen. Usługa DNS platformy Azure można rekordy DNS hello toohost używane dla określonej domeny. Przykład Witaj wirtualny adres IP (VIP) hello Azure zewnętrznej usługi równoważenia obciążenia (lub hello WAFs) mogą być rejestrowane w rekord A hello rekordu DNS platformy Azure.

[**Moduł równoważenia obciążenia Azure** ] [ ALB] modułu równoważenia obciążenia Azure oferuje wysoką dostępność usługi warstwy 4 (TCP, UDP), który można dystrybuować przychodzący ruch między wystąpieniami usługi zdefiniowane w zestawie o zrównoważonym obciążeniu. Ruch wysyłany się, że można można rozpowszechniać toohello usługi równoważenia obciążenia z frontonu punktów końcowych (publicznego adresu IP punktów końcowych lub prywatnego adresu IP punktów końcowych), z lub bez zbiór tooa translacji adresów puli adresów IP zaplecza (przykłady są; Urządzenie wirtualne sieci lub maszyn wirtualnych).

Moduł równoważenia obciążenia Azure można sondy kondycji hello hello także różne wystąpienia serwera, a jeśli badanie nie powiedzie się toorespond hello obciążenia równoważenia zatrzymuje wysyłania ruchu toohello zła wystąpienia. W vDC mamy hello obecności zewnętrznej usługi równoważenia obciążenia w Centrum hello (na przykład saldo hello ruchu tooNVAs) i partnerzy hello (tooperform zadania, takie jak Równoważenie ruchu między różnych maszyn wirtualnych wielowarstwowej aplikacji).

[**Brama aplikacji w** ] [ AppGW] bramę aplikacji usługi Microsoft Azure jest dedykowany urządzenie wirtualne udostępniające kontroler dostarczania aplikacji (ADC) jako usługa, oferty różnych warstwy 7 równoważenia obciążenia możliwości aplikacji. Pozwala ona wydajność kolektywu serwerów sieci web toooptimize dzięki przeniesieniu Procesora znacznym SSL zakończenia toohello bramy aplikacji. Udostępnia również inne funkcje routingu warstwy 7 tym działanie okrężne dystrybucję ruchu przychodzącego, koligacji na podstawie plików cookie sesji, routingu adresów URL na podstawie ścieżki i toohost możliwości hello wiele witryn sieci Web za pojedyncza brama aplikacji. Zapora aplikacji sieci web (WAF) jest również udostępniany w ramach bramy aplikacji hello SKU zapory aplikacji sieci Web. Ta jednostka SKU zapewnia ochronę aplikacje tooweb wspólnej luk w zabezpieczeniach sieci web i luki w zabezpieczeniach. Usługę Application Gateway można skonfigurować jako bramę umożliwiającą dostęp do Internetu, bramę tylko wewnętrzną lub jako kombinację obu tych opcji. 

[**Publiczne adresy IP** ] [ PIP] Włącz funkcje niektóre Azure możesz tooassociate usługi punktów końcowych tooa publiczny adres IP umożliwiający toobe zasobów tooyour użytkowcy hello internet. Ten punkt końcowy używa translatora adresów sieciowych (NAT) tooroute ruchu toohello wewnętrzny adres i port na powitania sieci wirtualnej platformy Azure. Ta ścieżka jest podstawowy sposobem toopass zewnętrznego ruchu w sieci wirtualnej hello hello. Witaj publiczny adres IP może być skonfigurowany toodetermine, których ruch jest przekazywany w i jak i gdzie jest translacja na toohello sieci wirtualnej.

#### <a name="component-type-monitoring"></a>Typ składnika: monitorowania
Składniki monitorowania zapewniają wgląd i alertów ze wszystkich innych typów składników hello. Wszystkie zespoły powinien mieć dostęp toomonitoring hello składników i usług mają dostęp do. Jeśli masz scentralizowane pomocy technicznej lub operacji zespołów wymagałoby danych toohello dostępu toohave zintegrowane dostarczonych przez tych składników.

Azure oferuje różne typy rejestrowania i monitorowania zachowanie hello tootrack usług Azure hostowanych zasobów. Zarządzanie i sterowanie obciążeń na platformie Azure jest oparte na nie tylko na zbieranie danych dziennika, ale akcje tootrigger możliwości hello na podstawie określonych zdarzeń zgłoszony.

Istnieją dwa główne typy dzienników na platformie Azure:

-   [**Dzienniki aktywności** ] [ ActLog] (określane również jako "Dziennik operacyjny") zapewniają wgląd w operacji hello, które były wykonywane na zasobach w programie hello subskrypcji platformy Azure. Te dzienniki raport hello płaszczyzny kontroli zdarzeń dla subskrypcji. Każdy zasób Azure tworzy dzienniki inspekcji.

-   [**Azure dzienników diagnostycznych** ] [ DiagLog] są dzienniki generowane przez zasób, które zapewniają bogate, często dane dotyczące operacji hello tego zasobu. zawartość Hello te dzienniki zależy od typu zasobu.

[![9]][9]

W vDC jest bardzo ważne tootrack hello grup NSG dzienniki, szczególnie tych informacji:

-   [**Dzienniki zdarzeń**][NSGLog]: zawiera informacje o jakie reguły NSG są stosowane tooVMs i wystąpienia ról na podstawie adresu MAC.
-   [**Licznik dzienniki**][NSGLog]: śledzi, ile razy w poszczególnych grupach NSG reguły zostało wykonane toodeny lub zezwolić na ruch.

Wszystkie dzienniki mogą być przechowywane na kontach magazynu Azure do inspekcji, analizę statyczną lub wykonywania kopii zapasowych. Gdy hello dzienniki są przechowywane na koncie magazynu platformy Azure, klienci mogą użyć różnych typów z tooretrieve struktury przygotowywanie, analizowanie i wizualizacji ten stan hello tooreport danych i kondycji zasobów w chmurze.

Duże przedsiębiorstwa powinna już zostały nabyte standardowych ramy monitorowania lokalnych systemów i można rozszerzyć że framework toointegrate dzienniki generowane przez wdrożenia chmury. Dla organizacji, które chcesz, aby wszystkie hello rejestrowania w chmurze hello tookeep [programu Microsoft Operations Management Suite (OMS)] [ OMS] jest doskonałym wyborem. Ponieważ oprogramowanie OMS jest zaimplementowane jako usługa w chmurze, może być dostępne szybko przy minimalnym poziomie inwestycji w usługi infrastruktury. OMS można również zintegrować ze składnikami programu System Center, takich jak System Center Operations Manager tooextend istniejące inwestycje w technologie zarządzania hello chmury.

Analiza dzienników OMS jest składnik hello OMS framework toohelp zebrać, korelując, wyszukiwanie i ustawy o dane dziennika i wydajności wygenerowane przez systemy operacyjne, aplikacje, infrastruktury chmury składników. Udostępnia klientom w czasie rzeczywistym operational insights zastosowanie wyszukiwanie zintegrowane i niestandardowe pulpity nawigacyjne tooanalyze wszystkie rekordy hello dla wszystkich obciążeń w vDC.

#### <a name="component-type-workloads"></a>Typ składnika: obciążeń
Składniki obciążenia są, gdzie znajdują się rzeczywista aplikacji i usług. Istnieje również gdzie zespołów deweloperów aplikacji spędzają większość czasu.

możliwości obciążenia Hello są naprawdę nieskończona. Witaj poniżej przedstawiono kilka typów możliwe obciążenie hello:

**Aplikacje LOB wewnętrzny**

Aplikacji biznesowych z są trwającą operację krytyczne toohello komputera aplikacje przedsiębiorstwa. Aplikacje LOB ma pewne cechy wspólne:

-   **Interakcyjne**. Aplikacje BIZNESOWE są interaktywne natury: wprowadzone dane, a wynik/raporty są zwracane.
-   **Opartych na danych**. Aplikacje LOB są intensywnie korzystających z częste toohello baz danych lub innych magazynów danych.
-   **Zintegrowane**. BIZNESOWE aplikacje oferta integracji z innymi systemami, lub poza hello organizacji.

**Klientów witryn sieci web (skierowany do Internetu lub wewnętrzne)** większość aplikacji wchodzących w interakcję z hello Internet to witryny sieci web. Platforma Azure oferuje hello możliwości toorun witryny sieci web na maszynie Wirtualnej IaaS lub z [Azure Web Apps] [ WebApps] lokacji (PaaS). Aplikacje sieci Web platformy Azure obsługuje integrację z sieciami wirtualnymi, umożliwiające wdrożenie hello hello aplikacje sieci Web w hello gwiazdy z vDC. W przypadku hello integracji sieci Wirtualnej nie ma potrzeby tooexpose internetowego punktu końcowego dla aplikacji, ale zamiast tego użyć hello zasobów z systemem innym niż internet routingu adres prywatny z sieci prywatnej.

**Big Data/Analytics** gdy danych musi tooscale tooa bardzo dużych objętości, baz danych może nie skalowanie w górę poprawnie. Technologia Hadoop oferuje system kwerend toorun rozproszone na wielu węzłach. Klienci mają hello opcja toorun danych obciążeń w maszyny wirtualne IaaS i PaaS ([HDInsight][HDI]). HDInsight obsługuje wdrażanie na podstawie lokalizacji sieci wirtualnej, może być klastrem tooa wdrożonej w gwiazdy hello vDC.

**Zdarzenia i komunikatów**
[Azure Event Hubs] [ EventHubs] jest usługą wprowadzanie telemetrii w hiperskali, która zbiera, przekształca i przechowuje miliony zdarzeń. Jako rozproszonej platformy przesyłania strumieniowego zapewnia małe opóźnienia i można skonfigurować czas przechowywania, umożliwiając tooingest olbrzymich ilości danych telemetrycznych na platformie Azure i odczytywania danych z wielu aplikacji. Z usługą Event Hubs jednego strumienia może obsługiwać potoków w czasie rzeczywistym i na podstawie partii.

Chmurę wysokiej niezawodnej obsługi komunikatów usługi między aplikacjami i usługami, można zaimplementować za pośrednictwem [Azure Service Bus] [ ServiceBus] czy oferty asynchroniczne komunikatów obsługiwanych przez brokera między klientem a serwerem, wraz z programem strukturę pierwszy w pierwszym out (FIFO) do obsługi komunikatów i możliwości publikowania/subskrypcji.

[![10]][10]

### <a name="multiple-vdc"></a>Wiele vDC
Do tej pory w tym artykule ma fokus w jednego kontrolera vDC opisujący hello podstawowe składniki i architekturę, która współtworzenia vDC odporność tooa. Funkcje platformy Azure, takich jak zestawy dostępności NVAs, moduł równoważenia obciążenia Azure, zestawy skalowania, oraz innych mechanizmów wpływ tooa system, który pozwala toobuild stałe poziomy SLA do usług produkcji.

Jednak pojedynczy vDC znajduje się w jednym regionie i jest narażony toomajor awarii, mogą mieć wpływ na cały regionu. Klienci, którzy mają tooachieve wysokiej SLA muszą tooprotect hello usług za pomocą wdrożeń hello sam projekt w VDC dwie (lub więcej), umieszczone w różnych regionach.

Dodanie tooSLA kwestie istnieją kilka typowych scenariuszy, w którym wdrażania wielu VDC sens:

-   Obecność regionalne/Global
-   Odzyskiwanie po awarii
-   Mechanizm toodivert ruch między kontrolera domeny

#### <a name="regionalglobal-presence"></a>Obecność regionalne/Global
Centra danych platformy Azure znajdują się w wielu regionach na całym świecie. Podczas wybierania wielu centrów danych Azure, klienci muszą tooconsider dwa składniki pokrewne: odległości geograficzne i opóźnień. Klienci muszą tooevaluate hello geograficzne odległość między VDC hello i hello odległość między hello vDC i użytkownikach końcowych hello toooffer hello najlepsze środowisko użytkownika.

Witaj regionu Azure, gdzie hostowane są VDC może też być konieczne tooconform z przepisami dotyczącymi działalności ustala żadnych właściwości prawne, pod którą działa organizacji.

#### <a name="disaster-recovery"></a>Odzyskiwanie po awarii
Implementacja Hello planu odzyskiwania po awarii jest silnie pokrewne toohello typu danego obciążenia i hello możliwości toosynchronize hello obciążenia stanu między różnych VDC. Najlepiej, jeśli dane aplikacji toosynchronize między wdrożeniami w dwóch różnych VDC tooimplement szybkiego awaryjnej mechanizmu mają większość klientów. Większość aplikacji są toolatency poufnych, a które mogą spowodować potencjalne limitu czasu i opóźnienia w synchronizacji danych.

Synchronizacji lub Puls monitorowania aplikacji w różnych VDC wymaga komunikacji między nimi. Dwa VDC w różnych regionach, mogą zostać połączone za pomocą:

-   Prywatnej komunikacji równorzędnej ExpressRoute podczas hello vDC centra są połączone toohello tego samego obwodu usługi expressroute
-   wiele obwody usługi ExpressRoute połączonych za pośrednictwem sieci firmowej sieci szkieletowej i siatkę z vDC połączonych toohello obwody usługi ExpressRoute
-   Połączenia sieci VPN lokacja-lokacja między Twojej koncentratorów vDC w każdym regionie Azure

Zazwyczaj hello połączenia ExpressRoute jest mechanizm hello preferowane powodu większej przepustowości i opóźnień spójne, gdy przejeżdżających przez za pośrednictwem hello firmy Microsoft w sieci szkieletowej.

Brak nie toovalidate magic przepisu aplikacji rozdzielone między dwa (lub więcej), różnych VDC znajdujących się w różnych regionach. Klienci powinni uruchamiać sieci kwalifikacji testy tooverify hello opóźnienia i przepustowości połączenia hello i docelowej, czy Replikacja synchroniczna lub asynchroniczna danych jest odpowiedni i jakie celu czasu odzyskiwania optymalne hello (RTO) może być dla użytkownika obciążeń.

#### <a name="mechanism-toodivert-traffic-between-dc"></a>Mechanizm toodivert ruch między kontrolera domeny
Jeden skuteczne technika toodivert hello ruchu przychodzącego w jednym tooanother kontrolera domeny jest oparta na DNS. [Menedżer ruchu Azure] [ TM] używa hello systemu nazw domen (DNS, Domain Name System) mechanizm toodirect hello użytkownika końcowego ruchu toohello najbardziej odpowiednia publiczny punkt końcowy w określonych vDC. Za pomocą sondy Traffic Manager okresowo sprawdza, czy usługa kondycji hello publiczne punkty końcowe w różnych VDC i w razie awarii tych punktów końcowych, kieruje automatycznie toohello vDC dodatkowej.

Traffic Manager działa na publiczne punkty końcowe systemu Azure i mogą być używane, na przykład toocontrol/kierowanie ruchu tooAzure maszyn wirtualnych i aplikacji sieci Web w hello odpowiednie vDC. Menedżera ruchu jest odporność nawet w fazie hello niepowodzenie całego regionu Azure oraz kontrolować hello dystrybucję ruchu użytkowników dla punktów końcowych usług w różnych VDC na podstawie wielu kryteriów (na przykład błąd usługi w określonych vDC, lub wybierz Witaj vDC z hello najniższe opóźnienia sieci dla powitania klienta).

### <a name="conclusion"></a>Podsumowanie
Witaj wirtualnej centrum danych jest podejście toodata center migracji do chmury hello, który jest kombinacją funkcji i możliwości toocreate Skalowalna architektura platformy Azure, które pozwala zmaksymalizować wykorzystanie zasobów chmury, zmniejszenie kosztów i uproszczenia systemu ładu. koncepcja vDC Hello jest oparta na topologii partnerzy koncentratora, udostępnia typowe usługi udostępnionych w Centrum hello, dzięki czemu określonych aplikacji/obciążeń w partnerzy hello. VDC odpowiada struktury hello ról firmy, gdzie różnych działów (centralnym dziale IT, metodyki DevOps, operacji i konserwacji) współdziałają ze sobą, każda z określonej listy ról i obowiązków. VDC spełnia wymagania hello dotyczące migracji "Przyrostu i Shift", ale również zapewnia wiele zalet toonative wdrożenia chmury.

## <a name="references"></a>Dokumentacja
Witaj następujące funkcje zostały omówione w tym dokumencie. Kliknij przycisk toolearn łącza hello więcej.

| | | |
|-|-|-|
|Funkcje sieci|Równoważenie obciążenia|Łączność|
|[Sieci wirtualnych platformy Azure][VNet]</br>[Grupy zabezpieczeń sieci][NSG]</br>[Dzienniki grupy NSG][NSGLog]</br>[Routing zdefiniowane przez użytkownika][UDR]</br>[Urządzenie wirtualne sieci][NVA]</br>[Publiczny adres IP][PIP]|[Moduł równoważenia obciążenia Azure (L3)][ALB]</br>[Brama aplikacji (P7)][AppGW]</br>[Zapora aplikacji sieci Web][WAF]</br>[Usługi Azure Traffic Manager][TM] |[Komunikacja równorzędna sieci wirtualnej][VNetPeering]</br>[Wirtualna sieć prywatna][VPN]</br>[ExpressRoute][ExR]
|Tożsamość</br>|Monitorowanie</br>|Najlepsze rozwiązania</br>|
|[Usługa Azure Active Directory][AAD]</br>[Uwierzytelnianie wieloskładnikowe][MFA]</br>[Rola dostępu bazowego formantów][RBAC]</br>[Domyślne role usługi AAD][Roles] |[Dzienniki aktywności][ActLog]</br>[Dzienniki diagnostyczne][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[Najlepsze rozwiązania w zakresie sieci obwodowej][DMZ]</br>[Zarządzanie subskrypcją][SubMgmt]</br>[Zarządzanie grupami zasobów][RGMgmt]</br>[Limity subskrypcji platformy Azure][Limits] |
|Innymi usługami platformy Azure|
|[Aplikacje sieci Web Azure][WebApps]</br>[HDInsights (Hadoop)][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|



## <a name="next-steps"></a>Następne kroki
 - Eksploruj [sieci wirtualnej komunikacji równorzędnej][VNetPeering], hello technologii pomocniczych vDC koncentratora i gwiazda projektów
 - Implementowanie [AAD] [ AAD] tooget wprowadzenie [RBAC] [ RBAC] eksploracji
 - Tworzenie subskrypcji i zasobu model zarządzania i RBAC modelu toomeet hello struktury, wymagania i zasady organizacji. działanie najważniejszych Hello jest planowania. Jak praktyczne Zaplanuj reorganizacji, łączenia, nowych wierszy produktu, itp.

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "Przykłady nakładają się na siebie składnika" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "Przykład wysokiego poziomu vDC gwiazdy"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "Klaster koncentratorów i partnerów"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "Gwiazdy gwiazdy"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Diagram poziomu bloku hello vDC"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "Użytkownicy, grupy, subskrypcje i projektów"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "Diagram infrastruktury wysokiego poziomu"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "Diagram infrastruktury wysokiego poziomu"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "Równorzędna sieci wirtualnej i obwód sieci"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "Diagramu wysokiego poziomu do monitorowania"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "Diagram ogólny dla obciążenia"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
