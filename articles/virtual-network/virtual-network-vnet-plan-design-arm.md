---
title: "aaaAzure sieć wirtualną (VNet) planowania i projektowania przewodnik | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooplan i projektowania sieci wirtualnych platformy Azure zgodnie z wymaganiami izolacji, łączności i lokalizacji."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Planowanie i projektowanie sieci wirtualnych Azure
Tworzenie tooexperiment sieci wirtualnej, z jest dość proste, ale prawdopodobnie, wdroży wiele sieci wirtualnych za pośrednictwem czasu toosupport hello produkcji potrzeb organizacji. Z pewnego planowania i projektowania będzie można stanie toodeploy sieci wirtualnych i połączyć efektywniej potrzebne zasoby hello. Jeśli nie masz doświadczenia z sieciami wirtualnymi, jest zalecane możesz [Dowiedz się więcej o sieci wirtualnych](virtual-networks-overview.md) i [jak toodeploy](virtual-networks-create-vnet-arm-pportal.md) jeden przed kontynuowaniem.

## <a name="plan"></a>Planowanie
Dokładne zrozumienie subskrypcji platformy Azure, regiony i zasobów sieciowych jest szczególnie ważne w przypadku powodzenia. Lista hello uwagi poniżej służy jako punkt początkowy. Po zrozumieniu tych zagadnień można zdefiniować hello wymagania dla projektu sieci.

### <a name="considerations"></a>Zagadnienia do rozważenia
Przed odpowiedzią hello poniżej pytania dotyczące planowania, należy wziąć pod uwagę następujące hello:

* Wszystkie obiekty, które można utworzyć na platformie Azure składa się z co najmniej jeden zasób. Maszynę wirtualną (VM) jest zasobem, hello karty interfejsu sieciowego (NIC) używany przez maszynę Wirtualną jest zasobem hello publiczny adres IP używany przez kartę Sieciową jest zasobem, hello hello sieci wirtualnej karty Sieciowej jest połączonych toois zasobu.
* Utwórz zasoby w [regionu Azure](https://azure.microsoft.com/regions/#services) i subskrypcji. Zasoby mogą być tylko tooa połączonych sieci wirtualnej w hello tego samego regionu i subskrypcji zasobu hello to.
* Można połączyć sieci wirtualnych tooeach innych przy użyciu:
    * **[Sieci wirtualnej komunikacji równorzędnej](virtual-network-peering-overview.md)**: hello sieci wirtualnych musi istnieć w hello sam region platformy Azure. Przepustowość między zasobami w sieciach wirtualnych połączyć za pomocą jest sama hello tak, jakby zasoby hello był połączony toohello tej samej sieci wirtualnej.
    * **Azure [bramy sieci VPN](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: hello sieci wirtualnych może istnieć w hello, lub w różnych regionach platformy Azure. Przepustowość między zasobami w sieciach wirtualnych połączone za pośrednictwem bramy sieci VPN jest ograniczona przepustowość hello hello bramy sieci VPN.
* Możesz połączyć sieć lokalną tooyour sieci wirtualnych za pomocą jednego z hello [opcji łączności](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) dostępnej na platformie Azure.
* Różne zasoby można grupować w [grup zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups), dzięki czemu można łatwiej toomanage hello zasobu jako jednostka. Grupa zasobów może zawierać zasobów z wielu regionach, tak długo, jak zasoby hello należeć toohello tej samej subskrypcji.

### <a name="define-requirements"></a>Określenie wymagań w zakresie
Użycie tych pytań hello poniżej jako punkt początkowy dla projektu sieci platformy Azure.    

1. Co Azure lokalizacje będziesz używać toohost sieci wirtualnych?
2. Potrzebujesz tooprovide komunikacji między tymi lokalizacjami Azure?
3. Potrzebujesz tooprovide komunikacji między VNet(s) Twojego Azure i datacenter(s) sieci lokalnej?
4. Ile infrastruktura jako usługa (IaaS) maszyn wirtualnych, usług w chmurze role i aplikacji sieci web potrzebne do rozwiązania?
5. Potrzebujesz tooisolate ruchu na podstawie grup maszyn wirtualnych (tj. fronton sieci web serwerów i serwerów bazy danych zaplecza)?
6. Potrzebujesz toocontrol ruchu przy użyciu wirtualnych urządzeń?
7. Czy użytkownicy muszą różnych zestawów uprawnień toodifferent zasobów platformy Azure?

### <a name="understand-vnet-and-subnet-properties"></a>Zrozumienie właściwości sieci wirtualnej i podsieci
Zasoby sieci wirtualnej i podsieci pomocy, zdefiniuj granicę zabezpieczeń dla obciążeń działających na platformie Azure. Kolekcja przestrzeni adresów, zdefiniowany jako bloków CIDR charakteryzuje się sieci wirtualnej.

> [!NOTE]
> Administratorzy sieci znają notacji CIDR. Jeśli nie znasz CIDR, [Dowiedz się więcej o](http://whatismyipaddress.com/cidr).
>
>

Sieci wirtualne zawierają hello następujące właściwości.

| Właściwość | Opis | Ograniczenia |
| --- | --- | --- |
| **Nazwa** |Nazwa sieci wirtualnej |Ciąg się too80 znaków. Może zawierać litery, cyfry, podkreślenia, kropki i łączniki. Musi zaczynać się literą lub cyfrą. Musi kończyć się literą, cyfrą lub podkreśleniem. Można zawiera wielkich i małych liter. |
| **location** |Lokalizacja platformy Azure (również tooas określonego regionu). |Musi mieć jedną z hello prawidłowych lokalizacji platformy Azure. |
| **Element addressSpace** |Kolekcja prefiksów adresów, które tworzą hello sieci wirtualnej w notacji CIDR. |Musi być tablicą prawidłowy bloków adresów CIDR, w tym zakresy publicznych adresów IP. |
| **podsieci** |Kolekcja podsieci, które tworzą hello sieci wirtualnej |Zobacz tabelę właściwości podsieci hello poniżej. |
| **dhcpOptions** |Obiekt, który zawiera jednej wymaganej właściwości o nazwie **dnsServers**. | |
| **dnsServers** |Tablica serwery DNS używane przez hello sieci wirtualnej. Jeśli nie zostanie podana, rozpoznawania nazw wewnętrznych Azure jest używana. |Musi być tablicą too10 serwery DNS, za pomocą adresu IP. |

Podsieć jest zasobem podrzędnych sieci wirtualnej i pomaga zdefiniować segmenty przestrzeni adresów w obrębie blok CIDR, przy użyciu prefiksów adresów IP. Karty sieciowe mogą być dodawane toosubnets i tooVMs połączone, zapewniają łączność dla różnych obciążeń.

Podsieci zawierają hello następujące właściwości.

| Właściwość | Opis | Ograniczenia |
| --- | --- | --- |
| **Nazwa** |Nazwa podsieci |Ciąg się too80 znaków. Może zawierać litery, cyfry, podkreślenia, kropki i łączniki. Musi zaczynać się literą lub cyfrą. Musi kończyć się literą, cyfrą lub podkreśleniem. Można zawiera wielkich i małych liter. |
| **location** |Lokalizacja platformy Azure (również tooas określonego regionu). |Musi mieć jedną z hello prawidłowych lokalizacji platformy Azure. |
| **addressPrefix** |Prefiks pojedynczy adres, który tworzą hello podsieci w notacji CIDR |Musi być jeden blok CIDR, który wchodzi w skład jednej przestrzeni adresowych hello sieci wirtualnej. |
| **grupy networkSecurityGroup** |Grupa NSG stosowana toohello podsieci | |
| **Stan** |Tabela tras stosowane toohello podsieci | |
| **elementy Ipconfiguration** |Kolekcja obiektów konfiguracji IP używane przez karty sieciowe połączone toohello podsieci | |

### <a name="name-resolution"></a>Rozpoznawanie nazw
Domyślnie korzysta z sieci wirtualnej [rozpoznawania nazw platformy Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md) nazwy tooresolve wewnątrz hello sieci wirtualnej, a następnie na hello publicznej sieci Internet. Jednak jeśli łączysz się z centrów danych lokalnych tooyour sieci wirtualnych, należy tooprovide [serwer DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md) nazwy tooresolve od sieci.  

### <a name="limits"></a>Limity
Przejrzyj hello limity sieci w hello [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) tooensure artykułu, który projektu nie koliduje to z dowolnymi hello limitów. Niektóre limity można zwiększyć przez otwarcie biletu pomocy technicznej.

### <a name="role-based-access-control-rbac"></a>Kontrola dostępu oparta na rolach (RBAC)
Można użyć [Azure RBAC](../active-directory/role-based-access-built-in-roles.md) toocontrol hello poziom dostępu różnych użytkowników może być toodifferent zasobów na platformie Azure. W ten sposób może też oddzielić hello pracy przez zespół na podstawie swoich potrzeb.

Jeżeli sieci wirtualne są dane użytkowników w hello **współautora sieci** roli mają pełną kontrolę nad zasobami sieci wirtualnej Azure Resource Manager. Podobnie, użytkownicy w hello **klasycznego współautora sieci** rola ma pełną kontrolę nad zasoby klasyczne sieci wirtualnej.

> [!NOTE]
> Możesz również [tworzyć własne role](../active-directory/role-based-access-control-configure.md) tooseparate potrzeb administracyjnych.
>
>

## <a name="design"></a>Projektowanie
Jeśli znasz już odpowiedzi hello pytania toohello w hello [Planowanie](#Plan) Przejrzyj następujące hello przed zdefiniowaniem Twojej sieci wirtualnych.

### <a name="number-of-subscriptions-and-vnets"></a>Liczba subskrypcji i sieci wirtualnych
Należy rozważyć utworzenie wielu sieci wirtualnych w hello następujące scenariusze:

* **Maszyny wirtualne wymagające toobe umieszczone w różnych lokalizacjach Azure**. Sieci wirtualne na platformie Azure są regionalne. Nie obejmują one lokalizacji. W związku z tym należy co najmniej jedną sieć wirtualną dla każdej lokalizacji platformy Azure, który ma toohost maszyn wirtualnych w.
* **Obciążenia wymagające toobe całkowicie odizolowane od siebie nawzajem**. Można utworzyć oddzielne sieci wirtualnych, że nawet Użyj hello tej samej przestrzeni adresów IP, tooisolate różnych obciążeń od siebie nawzajem.

Należy pamiętać, że limity hello, wyświetlone powyżej są na region na subskrypcję. Oznacza to, że można użyć wielu subskrypcji tooincrease hello limit zasobów, które można zachować na platformie Azure. Można użyć sieci VPN lokacja lokacja lub obwodu usługi ExpressRoute, tooconnect sieci wirtualnych w ramach różnych subskrypcji.

### <a name="subscription-and-vnet-design-patterns"></a>Subskrypcja i wzorce projektowe sieci wirtualnej
Witaj w poniższej tabeli przedstawiono niektóre typowe wzorce projektowe dotyczące korzystania z subskrypcji i sieci wirtualnych.

| Scenariusz | Diagram | Specjaliści | Wady |
| --- | --- | --- | --- |
| Jedną subskrypcją, dwie sieci wirtualne dla aplikacji |![Jedną subskrypcją](./media/virtual-network-vnet-plan-design-arm/figure1.png) |Toomanage tylko jedna subskrypcja. |Maksymalna liczba sieci wirtualnych na region platformy Azure. Potrzebujesz więcej subskrypcji po tym. Przejrzyj hello [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu, aby uzyskać szczegółowe informacje. |
| Z jedną subskrypcją jednej aplikacji, dwie sieci wirtualne dla aplikacji |![Jedną subskrypcją](./media/virtual-network-vnet-plan-design-arm/figure2.png) |Używa tylko dwie sieci wirtualne na subskrypcję. |Przeszkodę toomanage istnieje zbyt wiele aplikacji. |
| Z jedną subskrypcją jednej jednostki biznesowej, dwie sieci wirtualne dla aplikacji. |![Jedną subskrypcją](./media/virtual-network-vnet-plan-design-arm/figure3.png) |Równowaga między liczbę subskrypcji i sieci wirtualnych. |Maksymalna liczba sieci wirtualnych na jednostki biznesowej (subscription). Przejrzyj hello [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu, aby uzyskać szczegółowe informacje. |
| Z jedną subskrypcją jednej jednostki biznesowej, dwie sieci wirtualne dla każdej grupy aplikacji. |![Jedną subskrypcją](./media/virtual-network-vnet-plan-design-arm/figure4.png) |Równowaga między liczbę subskrypcji i sieci wirtualnych. |Aplikacje muszą występować samodzielnie za pomocą podsieci i grup NSG. |

### <a name="number-of-subnets"></a>Liczba podsieci
Należy rozważyć wiele podsieci w sieci wirtualnej w hello następujące scenariusze:

* **Za mało prywatnych adresów IP dla wszystkich kart sieciowych w podsieci**. Przestrzeń adresowa podsieci hello liczbę kart sieciowych w podsieci hello nie zawiera za mało adresów IP, należy najpierw toocreate wielu podsieci. Należy pamiętać, że Azure rezerwuje 5 prywatnych adresów IP z każdej podsieci, której nie można użyć: hello pierwszy i ostatni adresów hello przestrzeń adresowa (adres podsieci hello oraz multiemisji) i toobe 3 adresy używane wewnętrznie (na potrzeby DHCP i DNS).
* **Bezpieczeństwo** Można użyć podsieci tooseparate grupy maszyn wirtualnych od siebie nawzajem dla obciążenia, które mają wielowarstwową struktury i zastosowania różnych [sieciowej grupy zabezpieczeń (NSG)](virtual-networks-nsg.md#subnets) dla tych podsieci.
* **Połączenia hybrydowe**. Korzystania z bramy sieci VPN i obwody usługi ExpressRoute za[połączyć](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) tooone Twojego sieci wirtualnych innym, i tooyour center(s) danych lokalnymi. Bramy sieci VPN i obwody usługi ExpressRoute wymagają podsieci własnych toobe utworzony.
* **Urządzenie wirtualne**. Urządzenie wirtualne, takie jak zapory, sieci WAN akceleratora lub brama sieci VPN można użyć w sieć wirtualną platformy Azure. W przypadku zrobić, należy za[kierować ruchem](virtual-networks-udr-overview.md) toothose urządzenia i je odizolować w ich własnych podsieci.

### <a name="subnet-and-nsg-design-patterns"></a>Wzorce projektowe podsieci i grupy NSG
Witaj w poniższej tabeli przedstawiono niektóre typowe wzorce projektowe dotyczące korzystania z podsieci.

| Scenariusz | Diagram | Specjaliści | Wady |
| --- | --- | --- | --- |
| Jednej podsieci, grupy NSG na warstwie aplikacji dla aplikacji |![Pojedyncza podsieć](./media/virtual-network-vnet-plan-design-arm/figure5.png) |Tylko jeden toomanage podsieci. |Wiele grup NSG tooisolate niezbędne każdej aplikacji. |
| Podsieć każdej aplikacji, grupy NSG na warstwie aplikacji |![Podsieć każdej aplikacji](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Toomanage mniejszą liczbę grup NSG. |Toomanage wielu podsieci. |
| Jednej podsieci na warstwie aplikacji, grup NSG dla aplikacji. |![Podsieci w warstwie](./media/virtual-network-vnet-plan-design-arm/figure7.png) |Równowaga między wiele podsieci i grup NSG. |Maksymalna liczba grup NSG na subskrypcję. Przejrzyj hello [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu, aby uzyskać szczegółowe informacje. |
| W jednej podsieci na warstwie aplikacji dla aplikacji, grup NSG dla podsieci |![Podsieci w warstwie aplikacji](./media/virtual-network-vnet-plan-design-arm/figure8.png) |Prawdopodobnie mniejszą liczbę grup NSG. |Toomanage wielu podsieci. |

## <a name="sample-design"></a>Przykładowy projekt
Aplikacja hello tooillustrate hello informacji w tym artykule, należy wziąć pod uwagę powitania od scenariusza.

Pracujesz dla firmy, która ma 2 centrów danych w Ameryce Północnej i centrów danych dwa Europy. Zidentyfikowano 6 różnych klientów aplikacji obsługiwanego przez 2 różnych jednostek biznesowych, które mają tooAzure toomigrate jako pilotażu. Podstawowa architektura aplikacji hello Hello są następujące:

* App1, App2 App3 i App4 są hostowane na serwerach Linux z systemem Ubuntu aplikacji sieci web. Każda aplikacja łączy tooa oddzielnej aplikacji serwera obsługującego usługi RESTful na serwerach Linux. usługi RESTful Hello połączyć tooa wewnętrzna baza danych MySQL.
* App5 i App6 są aplikacji sieci web na serwerach z systemem Windows z systemem Windows Server 2012 R2. Każda aplikacja nawiązuje połączenie bazy danych programu SQL Server zaplecza tooa.
* Wszystkie aplikacje są obecnie hostowane w jednym z firmy hello centrów danych w Ameryce Północnej.
* centra danych lokalne powitania Użyj przestrzeni adresowej 10.0.0.0/8 hello.

Należy toodesign rozwiązania sieci wirtualnej, który spełnia następujące wymagania hello:

* Zużycie zasobów w innych jednostek biznesowych nie powinny mieć wpływ na poszczególnych jednostek biznesowych.
* Należy zminimalizować ilość hello sieci wirtualnych i podsieci zarządzania toomake łatwiejsze.
* Poszczególnych jednostek biznesowych powinien mieć pojedynczy test/programowanie używane dla wszystkich aplikacji w sieci wirtualnej.
* Każda aplikacja znajduje się w 2 różnych Azure centrach danych na kontynencie (Ameryce Północnej i Europie).
* Każda aplikacja jest całkowicie odizolowane od siebie nawzajem.
* Każda aplikacja jest dostępna przez klientów za pośrednictwem hello Internet przy użyciu protokołu HTTP.
* Każdej aplikacji są dostępne w centrach danych lokalnych toohello połączonych użytkowników przy użyciu tunelu zaszyfrowane.
* Centra danych lokalnych tooon połączenia należy używać istniejącego urządzenia sieci VPN.
* Witaj firmy sieci grupa musi zawierać pełną kontrolę nad hello konfigurację sieci wirtualnej.
* Deweloperzy w poszczególnych jednostek biznesowych powinien mieć tylko stanie toodeploy maszyn wirtualnych tooexisting podsieci.
* Wszystkie aplikacje zostaną poddane migracji, ponieważ są one tooAzure (przyrostu i zmiany).
* bazy danych Hello w każdej lokalizacji powinien replikować tooother Azure lokalizacje raz dziennie.
* Każdej aplikacji należy używać 5 serwerów sieci web frontonu, 2 serwery aplikacji (w razie potrzeby) i 2 serwery bazy danych.

### <a name="plan"></a>Planowanie
Należy rozpocząć planowanie o udzielenie odpowiedzi na pytanie hello hello projektu [określenie wymagań w zakresie](#Define-requirements) sekcji, jak pokazano poniżej.

1. Co Azure lokalizacje będziesz używać toohost sieci wirtualnych?

    2 lokalizacje w Ameryce Północnej i 2 lokalizacji w Europie. Należy wybrać te, na podstawie fizycznej lokalizacji hello centrami danych lokalnych. W ten sposób połączenia z Twojej tooAzure lokalizacje fizyczne będą mieć lepszą opóźnienia.
2. Potrzebujesz tooprovide komunikacji między tymi lokalizacjami Azure?

    Tak. Ponieważ hello bazy danych musi być replikowane tooall lokalizacji.
3. Potrzebujesz tooprovide komunikacji między VNet(s) Twojego Azure i center(s) danych sieci lokalnej?

    Tak. Ponieważ użytkowników połączonych centrów danych lokalnych toohello musi być aplikacji hello tooaccess mogli za pośrednictwem tunelu zaszyfrowane.
4. Jak wiele maszyn wirtualnych IaaS należy użyć dla rozwiązania?

    200 maszyn wirtualnych IaaS. App1, App2 App3 i App4 wymagają 5 serwerów sieci web, każdy, 2 aplikacji na każdym serwerze i serwerami baz danych 2 każdego. To suma 9 maszyn wirtualnych IaaS na aplikację lub 36 maszyn wirtualnych IaaS. App5 i App6 wymagają 5 serwerów sieci web, jak i 2 serwery baz danych. To suma 7 maszyn wirtualnych IaaS na aplikację lub 14 maszyn wirtualnych IaaS. W związku z tym należy 50 maszyn wirtualnych IaaS dla wszystkich aplikacji w każdym regionie Azure. Ponieważ potrzebujemy regionów toouse 4 będzie 200 maszyn wirtualnych IaaS.

    Należy również tooprovide serwerów DNS w każdej sieci wirtualnej lub w nazwie tooresolve lokalnych centrów danych między maszyn wirtualnych IaaS platformy Azure i siecią lokalną.
5. Potrzebujesz tooisolate ruchu na podstawie grup maszyn wirtualnych (tj. fronton sieci web serwerów i serwerów bazy danych zaplecza)?

    Tak. Każda aplikacja powinna być całkowicie odizolowane od siebie, a także każdej warstwy aplikacji powinna zostać odizolowana.
6. Potrzebujesz toocontrol ruchu przy użyciu wirtualnych urządzeń?

    Nie. Urządzenie wirtualne może być używane tooprovide większą kontrolę nad przepływem ruchu, tym bardziej szczegółowe rejestrowanie płaszczyzna danych.
7. Czy użytkownicy muszą różnych zestawów uprawnień toodifferent zasobów platformy Azure?

    Tak. Hello sieci zespół musi pełnej kontroli dla ustawień sieci wirtualnej hello, gdy deweloperzy powinni mieć tylko stanie toodeploy swoje podsieci istniejących toopre maszyn wirtualnych.

### <a name="design"></a>Projektowanie
Należy stosować projektowania hello określenie subskrypcji, sieci wirtualnych, podsieci i grup NSG. W tym miejscu omówimy grup NSG, ale powinien więcej informacji o [grup NSG](virtual-networks-nsg.md) przed zakończeniem projektu.

**Liczba subskrypcji i sieci wirtualnych**

Witaj następujące wymagania są powiązane toosubscriptions i sieci wirtualnych:

* Zużycie zasobów w innych jednostek biznesowych nie powinny mieć wpływ na poszczególnych jednostek biznesowych.
* Należy zminimalizować ilość hello sieci wirtualnych i podsieci.
* Poszczególnych jednostek biznesowych powinien mieć pojedynczy test/programowanie używane dla wszystkich aplikacji w sieci wirtualnej.
* Każda aplikacja znajduje się w 2 różnych Azure centrach danych na kontynencie (Ameryce Północnej i Europie).

Na podstawie tych wymagań, musisz mieć subskrypcję dla poszczególnych jednostek biznesowych. W ten sposób zużycia zasobów przy użyciu jednostki biznesowe zostaną nie wchodzą w skład limity dla innych jednostek biznesowych. I od ma toominimize hello liczba sieci wirtualnych, należy rozważyć użycie hello **z jedną subskrypcją jednej jednostki biznesowej, dwie sieci wirtualne dla każdej grupy aplikacji** wzorca, jak pokazano poniżej.

![Jedną subskrypcją](./media/virtual-network-vnet-plan-design-arm/figure9.png)

Należy również przestrzeni adresowej hello toospecify dla każdej sieci wirtualnej. Ponieważ należy połączenie między hello lokalnych centrów danych i hello regiony platformy Azure, przestrzeni adresowej hello używane dla sieci wirtualnych platformy Azure nie mogą powodować konfliktów z sieci lokalnej hello i używane przez każdego sieci wirtualnej przestrzeni adresowej hello powinien nie mogą powodować konfliktów z innych istniejących sieci wirtualnych. Przestrzenie adresowe hello w tabeli hello poniżej toosatisfy można użyć tych wymagań.  

| **Subskrypcja** | **Sieć wirtualna** | **Region platformy Azure** | **Przestrzeń adresowa** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |Zachodnie stany USA |172.16.0.0/16 |
| BU1 |ProdBU1US2 |Wschodnie stany USA |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |Europa Północna |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |Europa Zachodnia |172.19.0.0/16 |
| BU1 |TestDevBU1 |Zachodnie stany USA |172.20.0.0/16 |
| BU2 |TestDevBU2 |Zachodnie stany USA |172.21.0.0/16 |
| BU2 |ProdBU2US1 |Zachodnie stany USA |172.22.0.0/16 |
| BU2 |ProdBU2US2 |Wschodnie stany USA |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |Europa Północna |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |Europa Zachodnia |172.25.0.0/16 |

**Liczba podsieci i grupy NSG**

Hello następujące wymagania są powiązane toosubnets i grup NSG:

* Należy zminimalizować ilość hello sieci wirtualnych i podsieci.
* Każda aplikacja jest całkowicie odizolowane od siebie nawzajem.
* Każda aplikacja jest dostępna przez klientów za pośrednictwem hello Internet przy użyciu protokołu HTTP.
* Każdej aplikacji są dostępne w centrach danych lokalnych toohello połączonych użytkowników przy użyciu tunelu zaszyfrowane.
* Centra danych lokalnych tooon połączenia należy używać istniejącego urządzenia sieci VPN.
* bazy danych Hello w każdej lokalizacji powinien replikować tooother Azure lokalizacje raz dziennie.

Na podstawie tych wymagań, można użyć jednej podsieci na warstwie aplikacji i grup NSG toofilter ruch na aplikację. Dzięki temu wystarczy tylko 3 podsieci w każdej sieci wirtualnej (frontonu, warstwy aplikacji i warstwą danych) i jeden NSG na aplikację w każdej podsieci. W takim przypadku należy rozważyć przy użyciu hello **jednej podsieci na warstwie aplikacji, grup NSG dla aplikacji** wzorzec projektowy. Hello na poniższej ilustracji pokazano sposób użycia wzorca projektowego hello reprezentujący hello hello **ProdBU1US1** sieci wirtualnej.

![W jednej podsieci na warstwę, co grupa NSG dla aplikacji w warstwie](./media/virtual-network-vnet-plan-design-arm/figure11.png)

Jednak należy również toocreate dodatkowe podsieci dla połączenia sieci VPN hello między hello sieci wirtualnych i sieci lokalnych centrów danych. I przestrzeń adresową hello toospecify są niezbędne dla każdej podsieci. Witaj na poniższej ilustracji przedstawiono przykładowe rozwiązanie dla **ProdBU1US1** sieci wirtualnej. W tym scenariuszu zostanie zreplikowany dla każdej sieci wirtualnej. Każdy kolor reprezentuje inną aplikację.

![Przykład sieci wirtualnej](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**Kontrola dostępu**

Witaj poniżej przedstawiono wymagania dotyczące powiązanych tooaccess sterowania:

* Witaj firmy sieci grupa musi zawierać pełną kontrolę nad hello konfigurację sieci wirtualnej.
* Deweloperzy w poszczególnych jednostek biznesowych powinien mieć tylko stanie toodeploy maszyn wirtualnych tooexisting podsieci.

Na podstawie tych wymagań, można dodać użytkowników z hello sieci toohello zespołu wbudowanych **współautora sieci** roli w każdej subskrypcji; i utworzyć niestandardową rolę dla hello deweloperzy aplikacji w każdej subskrypcji, podając ich praw tooadd maszyn wirtualnych tooexisting podsieci.

## <a name="next-steps"></a>Następne kroki
* [Wdrażanie sieci wirtualnej](virtual-networks-create-vnet-arm-template-click.md) oparta na scenariuszu.
* Zrozumienie sposobu zbyt[równoważenia obciążenia](../load-balancer/load-balancer-overview.md) maszyny wirtualne IaaS i [Zarządzanie routingu w wielu regionach platformy Azure](../traffic-manager/traffic-manager-overview.md).
* Dowiedz się więcej o [grup NSG i w jaki sposób tooplan i projektowania](virtual-networks-nsg.md) rozwiązania NSG.
* Dowiedz się więcej o sieci [między lokalizacjami oraz opcji łączności sieci wirtualnej](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti).
