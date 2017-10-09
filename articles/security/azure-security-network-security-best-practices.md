---
title: "aaaAzure najlepszych rozwiązań dotyczących zabezpieczeń sieci | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera zestaw najlepsze rozwiązania dotyczące sieci zabezpieczeń przy użyciu wbudowanych funkcji platformy Azure."
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Najlepsze rozwiązania sieci platformy Azure
Microsoft Azure umożliwia urządzeń tooother sieci maszyn wirtualnych i urządzenia tooconnect przez umieszczenie ich w sieciach wirtualnych platformy Azure. Sieć wirtualna Azure jest konstrukcja sieci wirtualnej, która pozwala tooconnect sieci wirtualnej interfejsu karty tooa sieci wirtualnej tooallow opartych na protokole TCP/IP komunikacji między urządzeniami sieciowymi włączone. Tooan połączonych sieci wirtualnej platformy Azure są możliwe tooconnect toodevices na maszynach wirtualnych platformy Azure hello tej samej sieci wirtualnej platformy Azure, różnych sieciach wirtualnych platformy Azure, na powitania Internet, a nawet w sieci lokalnej.

W tym artykule omówiono kolekcja najlepszych rozwiązań dotyczących zabezpieczeń sieci platformy Azure. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z platformy Azure w sieci i doświadczenia hello klientów, takich jak samodzielnie.

Dla każdego ze względów wyjaśniamy:

* Jakie hello najlepszym rozwiązaniem jest
* Dlaczego chcesz tooenable tej najlepsze praktyki
* Co może wynikać hello tooenable hello najlepszym rozwiązaniem w przeciwnym przypadku
* Najlepszym rozwiązaniem toohello możliwe alternatywy
* Jak można znaleźć tooenable hello najlepsze praktyki

W tym artykule Azure sieci najlepsze rozwiązania w zakresie zabezpieczeń jest na podstawie opinii konsensu i funkcji platformy Azure i zestawy funkcji istniejących w chwili hello, który został zapisany w tym artykule. Opinie i technologie ulegną zmianom i będą w tym artykule zaktualizowane na tooreflect regularnie tych zmian.

Azure sieci najlepsze rozwiązania omówione w tym artykule obejmują:

* Logicznie segmentu podsieci
* Kontrolowania zachowania routingu
* Włączanie tunelowania wymuszonego
* Użyj wirtualnych urządzeń sieciowych
* Wdrażanie sieci DMZ podziału na strefy zabezpieczeń
* Unikaj narażenia toohello Internet dedykowane łącza sieci WAN
* Optymalizuj czas działania i wydajności
* Użyj równoważenia obciążenia globalne
* Wyłącz tooAzure dostępu RDP maszyny wirtualne
* Centrum zabezpieczeń Azure Włącz
* Rozszerzanie centrum danych na platformie Azure

## <a name="logically-segment-subnets"></a>Logicznie segmentu podsieci
[Sieci wirtualnych platformy Azure](https://azure.microsoft.com/documentation/services/virtual-network/) są podobne LAN tooa w sieci lokalnej. Witaj ideą sieci wirtualnej platformy Azure jest utworzenie pojedynczej prywatny adres przestrzennych sieci IP na którym można umieścić wszystkie Twoje [maszyny wirtualne Azure](https://azure.microsoft.com/services/virtual-machines/). Hello prywatnych przestrzeni adresów IP dostępne są w hello klasy A (10.0.0.0/8) klasy B (172.16.0.0/12) i Klasa C zakresów (192.168.0.0/16).

Podobne toowhat można lokalnie, należy toosegment hello większych przestrzeń adresów w podsieci. Można użyć [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) oparty na tworzeniu zasad toocreate podsieci.

Routing między podsieciami nastąpi automatycznie i nie trzeba toomanually skonfigurować tabele routingu. Jednak hello domyślne ustawienie zakłada, że bez kontroli dostępu do sieci między podsieciami hello, utworzone na powitania sieci wirtualnej platformy Azure. W kolejności toocreate sieci kontroli dostępu między podsieciami będziesz potrzebować tooput coś między podsieciami hello.

Z hello czynności można użyć tooaccomplish to zadanie jest [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) (NSG). Grupy NSG są proste pakietów kontroli urządzeń używających hello 5 parametrów (hello źródłowy adres IP, port źródłowy, docelowy adres IP, docelowy port i protokół warstwy 4) podejścia toocreate zezwalania/niezezwalania reguły dla ruchu sieciowego. Można akceptować lub odrzucać tooand ruchu z pojedynczego adresu IP, tooand z wielu adresów IP lub nawet tooand w całej podsieci.

Za pomocą grup NSG dla kontroli dostępu do sieci między podsieciami pozwala tooput zasobów, które należą toohello tej samej strefie zabezpieczeń lub roli w swoich własnych podsieciach. Na przykład traktować prostą aplikację 3-warstwowej warstwa sieci web, warstwy logiki aplikacji i warstwy bazy danych. Możesz zaznaczyć maszyn wirtualnych, które należą do swoich własnych podsieciach tooeach tych warstw. Następnie można użyć grupy NSG toocontrol ruch między podsieciami hello:

* Maszyny wirtualne warstwy sieci Web tylko mogą inicjować połączenia toohello aplikacji logiki maszyn i może akceptować tylko połączenia z hello Internet
* Maszyny wirtualne logiki aplikacji tylko mogą inicjować połączenia z warstwą bazy danych i może akceptować tylko połączenia z hello warstwa sieci web
* Maszyny wirtualne warstwy bazy danych nie można zainicjować połączenia z niczego poza ich własnych podsieci i może akceptować tylko połączenia z warstwy logiki aplikacji hello

toolearn więcej o grup zabezpieczeń sieci i korzystania z nich toologically segmentu sieci wirtualne platformy Azure, przeczytaj artykuł hello [co to jest grupa zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) (NSG).

## <a name="control-routing-behavior"></a>Kontrolowania zachowania routingu
Po umieszczeniu maszyny wirtualnej w sieci wirtualnej platformy Azure można zauważyć hello maszyny wirtualnej można połączyć tooany inną maszynę wirtualną na hello tej samej sieci wirtualnej Azure, nawet jeśli hello inne maszyny wirtualne są w różnych podsieciach. Dlaczego jest to możliwe przyczyny Hello jest brak zbiór tras systemowych, które są domyślnie włączone zezwalające na ten typ komunikacji. Te trasy domyślnej połączeń maszyny wirtualnej na powitania tej samej sieci wirtualnej Azure tooinitiate ze sobą oraz z hello Internet (dla komunikacji wychodzącej toohello Internet tylko).

Trasy systemowe domyślna hello są przydatne w przypadku wiele scenariuszy wdrażania, Brak godziny, kiedy ma konfigurację routingu hello toocustomize wdrożeń. Te modyfikacje pozwoli tooconfigure hello następnego przeskoku adres tooreach określonych miejsc docelowych.

Zaleca się skonfigurowanie trasy zdefiniowane przez użytkownika podczas wdrażania urządzenia zabezpieczeń sieci wirtualnej, które będzie są omawiane w późniejszym najlepszym rozwiązaniem.

> [!NOTE]
> Trasy zdefiniowane przez użytkownika nie są wymagane i tras systemowych domyślne hello będzie działać w większości przypadków.
>
>

Dowiedz się więcej na temat trasy zdefiniowane przez użytkownika i w jaki sposób tooconfigure ich od przeczytania artykułu hello [co to są trasy zdefiniowane przez użytkownika i przesyłania dalej protokołu IP](../virtual-network/virtual-networks-udr-overview.md).

## <a name="enable-forced-tunneling"></a>Włączanie tunelowania wymuszonego
zrozumienie toobetter tunelowania wymuszonego, jest przydatne toounderstand jakie "tunelowania podzielonego" jest.
najbardziej typowym przykładem Hello tunelowania podzielonego pojawia się przy użyciu połączeń VPN. Wyobraź sobie ustanowić połączenie sieci VPN z hoteli miejsca tooyour sieci firmowej. To połączenie umożliwia tooconnect tooresources w sieci firmowej i przejść wszystkie tooresources komunikacji w sieci firmowej za pośrednictwem tunelu VPN hello.

Co się stanie, jeśli chcesz tooresources tooconnect na powitania Internet? Po włączeniu tunelowania podzielonego tych połączeń przejdź bezpośrednio toohello Internet i nie za pośrednictwem sieci VPN hello tunelu. Niektóre ekspertów zabezpieczeń należy wziąć pod uwagę toobe to potencjalne zagrożenie i dlatego zaleca się, że tunelowanie podzielone wyłączone i wszystkie połączenia tych przeznaczonych dla hello Internet i te przeznaczonych dla zasobów firmowych, przejdź za pośrednictwem tunelu VPN hello. Zaletą Hello w ten sposób jest tym toohello połączenia internetowe są następnie wymuszone za pośrednictwem hello sieci firmowej zabezpieczeń urządzeń, które nie będą przypadku hello, jeśli toohello Internet poza tunel VPN hello połączony powitania klienta sieci VPN.

Teraz załóżmy Przełącz to kopii toovirtual maszyny w sieci wirtualnej platformy Azure. Hello trasy domyślnej dla sieci wirtualnej platformy Azure umożliwiają maszyn wirtualnych tooinitiate ruchu toohello Internet. To zbyt może reprezentować zagrożenie bezpieczeństwa tych połączeń wychodzących można zwiększyć podatność hello maszyny wirtualnej i być wykorzystywane przez osoby atakujące.
Z tego powodu zaleca się włączenie wymuszanie tunelowania na maszynach wirtualnych, jeśli masz łączności między lokalizacjami między sieci wirtualnej platformy Azure i siecią lokalną. Omawianiu będzie między lokalnym łączności dalej w tej sieci najlepsze rozwiązania w zakresie dokumentów w usłudze Azure.

Jeśli nie masz połączenia między różnymi lokalizacjami, upewnij się, możesz korzystać z grup zabezpieczeń sieci (opisanych wcześniej) lub Azure sieci wirtualnej zabezpieczeń urządzenia (obok opisano) tooprevent połączeń wychodzących toohello Internet z wirtualnej Azure Maszyny.

więcej informacji o toolearn wymuszone tunelowanie i jak tooenable, przeczytaj artykuł hello [skonfigurować wymuszonego tunelowania przy użyciu programu PowerShell i usługi Azure Resource Manager](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md).

## <a name="use-virtual-network-appliances"></a>Użyj urządzeń sieci wirtualnej
Gdy grup zabezpieczeń sieci i routingu zdefiniowane użytkownika zapewniają miary zabezpieczenia sieci na powitania sieci i transportu warstw hello [OSI model](https://en.wikipedia.org/wiki/OSI_model), będą toobe sytuacji, w którym będzie mają lub potrzebujesz tooenable zabezpieczenia w wysokim hello stosu. W takich sytuacjach zalecamy wdrożenie zapewniana przez partnerów Azure urządzenia zabezpieczeń sieci wirtualnej.

Urządzenia zabezpieczeń sieci platformy Azure może zapewnić znaczne zwiększenie poziomu zabezpieczeń przez dostarczanych przez kontrolę poziomu sieci. Oto niektóre z funkcji zabezpieczeń sieci hello udostępniane przez urządzenia zabezpieczeń sieci wirtualnej:

* Zapory
* Wykrywania nieautoryzowanego dostępu/włamań zapobiegania
* Zarządzanie luki w zabezpieczeniach
* Formant aplikacji
* Wykrywanie anomalii opartych na sieci
* Filtrowanie sieci Web
* Oprogramowanie antywirusowe
* Botnet ochrony

Jeśli potrzebujesz wyższy poziom zabezpieczeń sieci, nie można uzyskać z kontroli dostępu na poziomie sieci, następnie zalecamy zbadać, a następnie wdrożyć urządzenia zabezpieczeń sieci wirtualnej platformy Azure.

toolearn dotyczące jakiego urządzenia zabezpieczeń sieci wirtualnej platformy Azure są dostępne i ich możliwości, odwiedź stronę hello [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/) i wyszukaj "zabezpieczenia" i "zabezpieczenia sieciowe".

## <a name="deploy-dmzs-for-security-zoning"></a>Wdrażanie sieci DMZ podziału na strefy zabezpieczeń
Strefa DMZ lub "w sieci obwodowej" jest fizycznego lub segment sieci logicznej, która jest zaprojektowana tooprovide dodatkową warstwę zabezpieczeń między zasobów i hello Internet. Celem Hello hello DMZ jest tooplace specjalizowany urządzenia kontroli dostępu do sieci na granicy hello hello DMZ sieci, aby tylko żądany ruch jest dozwolony, urządzenie ochrony sieci hello i w sieci wirtualnej platformy Azure.

Sieci DMZ są przydatne, ponieważ monitorowania, rejestrowania i raportowania na urządzeniach hello hello krawędzi sieci wirtualnej platformy Azure można skupić się zarządzanie kontrolą dostępu z sieci. W tym miejscu zwykle czy włączyć zapobiegania DDoS, systemów zapobiegania włamań/wykrywania nieautoryzowanego dostępu (Identyfikatory/adresów IP), reguły zapory i zasady, filtrowanie sieci web, sieci ochrony przed złośliwym oprogramowaniem i więcej. urządzeń zabezpieczeń sieciowych Hello znajdują się między hello Internetu i sieci wirtualnej platformy Azure i interfejs w obu sieciach.

Jest to hello podstawowego projektu strefą DMZ, istnieją wiele różnych projektów DMZ, takie jak symetryczna, adresem IP tri, wieloadresowego i inne.

Firma Microsoft zaleca wdrożeń wysokiego poziomu zabezpieczeń rozważ wdrożenie DMZ tooenhance hello poziom zabezpieczeń sieci dla zasobów platformy Azure.

więcej informacji na temat sieci DMZ i jak toodeploy je na platformie Azure, przeczytaj artykuł hello toolearn [usług chmurowych firmy Microsoft i zabezpieczeń sieciowych](../best-practices-network-security.md).

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>Unikaj narażenia toohello Internet dedykowane łącza sieci WAN
W wielu organizacjach wybrane hello IT hybrydowego trasy. Hybrydowy IT niektóre zasobów informacji firmy hello są na platformie Azure, podczas gdy inne pozostają lokalnymi. W wielu przypadkach niektóre składniki usługi będzie uruchomiony w Azure, podczas gdy inne składniki pozostają lokalnymi.

IT scenariusz hybrydowy hello jest zwykle pewien typ łączności między lokalizacjami. To między różnymi lokalizacjami, połączenie umożliwia hello firmy tooconnect ich tooAzure sieci lokalnej sieci wirtualnych. Dostępne są dwa rozwiązania w zakresie łączności między lokalizacjami:

* Sieci VPN typu lokacja lokacja
* ExpressRoute

[Sieci VPN typu lokacja lokacja](../vpn-gateway/vpn-gateway-site-to-site-create.md) reprezentuje połączenie prywatnej wirtualnej między siecią lokalną a sieci wirtualnej platformy Azure. To połączenie ma miejsce ponad hello Internet i pozwala zbyt "tunelowe" informacji wewnątrz zaszyfrowanych łącza między siecią a Azure. Sieci VPN typu lokacja lokacja jest bezpieczne, dojrzała technologia, która jest wdrażany w przedsiębiorstwach wszystkich rozmiarów dekad. Tunel szyfrowanie odbywa się przy użyciu [trybu tunelowania IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Podczas sieci VPN typu lokacja lokacja jest technologią zaufanych, niezawodny i ustalonych ruchu w tunelu hello przechodzenia hello Internet. Ponadto przepustowość jest stosunkowo ograniczonego tooa maksymalnie o 200 MB/s.

Jeśli potrzebujesz wyjątkowych poziom bezpieczeństwa i wydajności dla połączeń między różnymi lokalizacjami, zalecane jest użycie Azure ExpressRoute dla łączność między lokalizacjami. ExpressRoute jest dedykowanych sieci WAN łącza między Twojej lokalizacji lokalnej lub dostawcy usług hosta programu Exchange. Ponieważ jest to połączenie telco, dane nie są przesyłane za pośrednictwem Internetu hello i dlatego nie narażonych toohello potencjalne ryzyko związane z komunikacją internetową.

więcej informacji na temat jak działa usługa Azure ExpressRoute toolearn i jak toodeploy, przeczytaj artykuł hello [opis techniczny ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="optimize-uptime-and-performance"></a>Optymalizuj czas działania i wydajności
Poufności, integralności i dostępności (CIA) obejmują Triada hello współczesnych najbardziej znaczenie modelu zabezpieczeń. O szyfrowaniu i ochronie prywatności jest poufność, integralność jest upewnienie się, że dane nie ulega zmianie przez nieautoryzowane osoby i dostępności jest upewnienie się, że uprawnionych osób są możliwe tooaccess hello informacje, które użytkownik jest uprawniony tooaccess. Błąd w jednym z tych obszarów reprezentuje potencjalne naruszenie zabezpieczeń.

Dostępność można traktować jako o dostępności i wydajności. Jeśli usługa nie działa, informacje są niedostępne. Jeśli wydajność jest więc słaba jako bezużyteczne dane hello toomake, firma Microsoft może rozważ toobe danych hello niedostępny. W związku z tym z punktu widzenia zabezpieczeń, potrzebujemy toodo niezależnie od możemy toomake się naszych usług optymalnej dostępności i wydajności.
Metoda popularnych i skuteczne używana tooenhance dostępności i wydajności jest równoważenia obciążenia toouse. Równoważenie obciążenia sieciowego jest metoda dystrybucji ruchu sieciowego na serwerach, które są częścią usługi. Na przykład jeśli masz serwerów frontonu sieci web w ramach usługi, można użyć równoważeniem obciążenia toodistribute hello ruch na wiele serwerów frontonu sieci web.

Tej dystrybucji ruchu sieciowego zwiększa dostępność, ponieważ jeśli jeden z serwerów sieci web hello staje się niedostępny, usługi równoważenia obciążenia hello przestanie wysyłania ruchu toothat serwera i przekierowanie ruchu toohello serwerów, które są nadal w trybie online. Równoważenie obciążenia sieciowego pomaga również wydajności, ponieważ hello procesora, sieci i pamięci w czasie obsługująca żądania jest dystrybuowana do wszystkich serwerów z równoważeniem obciążenia hello.

Zaleca się, że zostanie zastosowana równoważenia obciążenia zawsze można się odpowiednie dla Twojej usługi. Czy w hello następujące sekcje będzie można rozwiązać.
Na powitania poziomu sieci wirtualnej platformy Azure Azure zapewnia z trzech podstawowych ładowania równoważenia opcje:

* Równoważenie obciążenia oparte na protokole HTTP
* Zewnętrzne Równoważenie obciążenia
* Wewnętrzne równoważenie obciążenia

## <a name="http-based-load-balancing"></a>Równoważenie obciążenia oparte na protokole HTTP
Równoważenie obciążenia oparte na protokole HTTP podstawowych decyzji dotyczących połączenia toosend serwera przy użyciu właściwości protokołu hello HTTP. Platforma Azure ma usługi równoważenia obciążenia HTTP, który jest przesyłany przez hello nazwy bramy aplikacji.

Zalecamy, aby użytkownik nam brama aplikacji w usłudze Azure po:

* Aplikacje, które wymagają żądań z hello tego samego użytkownika/klienta sesji tooreach hello tej samej maszyny wirtualnej zaplecza. Przykłady to będzie zakupów, koszyka aplikacji i serwerów poczty w sieci web.
* Aplikacje, które mają toofree farmach serwerów sieci web z kończenia żądań SSL narzut korzystając z bramy aplikacji [odciążania SSL](https://f5.com/glossary/ssl-offloading) funkcji.
* Aplikacje, takie jak sieci dostarczania zawartości, które wymagają wielu żądań HTTP na powitania tego samego toobe połączenia protokołu TCP długotrwałe trasę lub serwerami zaplecza toodifferent równoważeniem obciążenia.

toolearn więcej informacji na temat działania bramy aplikacji Azure i jak go używać w ramach wdrożeń, przeczytaj artykuł hello [omówienie bramy aplikacji](../application-gateway/application-gateway-introduction.md).

## <a name="external-load-balancing"></a>Zewnętrzne Równoważenie obciążenia
Równoważenie obciążenia zewnętrznych ma miejsce, gdy połączenia przychodzące z Internetu hello jest równoważone między serwerów znajdujących się w sieci wirtualnej platformy Azure. Hello Azure zewnętrznej usługi równoważenia obciążenia zapewnia tej możliwości i zalecane jest użycie jej nie wymagają trwałe sesje hello lub odciążanie protokołu SSL.

Z kolei na podstawie tooHTTP równoważenia obciążenia, hello zewnętrznej usługi równoważenia obciążenia używa informacji w hello sieci i transportu warstw hello OSI modelu toomake decyzji na jakie tooload saldo połączenie serwera.

Firma Microsoft zaleca użycie zewnętrznego równoważenia obciążenia zawsze [aplikacji bezstanowych](http://whatis.techtarget.com/definition/stateless-app) akceptować żądania przychodzące z Internetu hello.

toolearn więcej informacji o sposobie działania hello Azure zewnętrzną usługą równoważenia obciążenia i jak można wdrożyć, przeczytaj artykuł hello [rozpocząć tworzenie Internet ukierunkowane modułu równoważenia obciążenia w Menedżerze zasobów przy użyciu programu PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md).

## <a name="internal-load-balancing"></a>Wewnętrzne Równoważenie obciążenia
Równoważenie obciążenia wewnętrznego jest podobne tooexternal Równoważenie obciążenia i używa hello sam mechanizm tooload saldo połączeń toohello serwerów za ich. Witaj tylko różnica jest ten moduł równoważenia obciążenia hello w takim przypadku akceptowania połączeń z maszyn wirtualnych, które nie znajdują się na powitania Internet. W większości przypadków hello połączeń, które są akceptowane Równoważenie obciążenia sieciowego są inicjowane przez urządzenia w sieci wirtualnej platformy Azure.

Firma Microsoft zaleca użycie wewnętrzne Równoważenie obciążenia dla scenariuszy, które będą korzystać z tej funkcji, takich jak potrzebne tooload saldo połączeń tooSQL serwerów lub serwerów sieci web wewnętrznej.

toolearn więcej informacji na temat działania wewnętrznego równoważenia obciążenia Azure i jak można wdrożyć, przeczytaj artykuł hello [rozpocząć tworzenie przy użyciu programu PowerShell do wewnętrznego modułu równoważenia obciążenia](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer).

## <a name="use-global-load-balancing"></a>Użyj równoważenia obciążenia globalne
Chmura publiczna obliczeniowych umożliwia toodeploy globalnie rozproszone aplikacje, które mają składniki znajdujące się w centrach danych na całym świecie hello. Jest to możliwe w systemie Microsoft Azure powodu tooAzure w obecności globalne centrum danych. Z kolei technologii równoważenia obciążenia toohello wspomniano wcześniej, równoważenie obciążenia globalne jej udostępnienie usług toomake możliwe nawet wtedy, gdy cały centrów danych mogą stać się niedostępne.

Możesz uzyskać tego typu globalnego równoważenia obciążenia w Azure dzięki wykorzystaniu [usługi Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/). Sprawia, że Menedżera ruchu jest możliwe tooload saldo usług tooyour połączenia na podstawie hello lokalizacji hello użytkownika.

Na przykład jeśli użytkownik hello jest usługą tooyour żądania hello UE, połączenie hello jest ukierunkowanej tooyour usług znajduje się w centrum danych Unii Europejskiej. Ta część usługi Traffic Manager obciążenia globalnego równoważenia wydajności tooimprove pomaga ponieważ łączenie toohello najbliższego centrum danych jest szybsza niż łączenie toodatacenters, które są daleko.

Na stronie dostępności hello Równoważenie obciążenia globalne upewnia się, usługa jest dostępna, nawet wtedy, gdy całe centrum danych powinny stać się niedostępne.

Na przykład, jeśli Centrum danych Azure powinny stać się niedostępny z powodu przyczyn tooenvironmental lub termin toooutages (np. błędy sieciowe), połączenia usługi tooyour będzie przekierowany toohello najbliższego centrum danych w trybie online. Dzięki wykorzystaniu zasad DNS, które można utworzyć w usłudze Traffic Manager odbywa się to równoważenia obciążenia globalnego.

Firma Microsoft zaleca, użyj Menedżera ruchu dla dowolnego chmury rozwiązania wprowadzane ma zakres dystrybucji w różnych regionach i wymaga hello najwyższy poziom czas pracy jest możliwe.

toolearn więcej o usłudze Azure Traffic Manager oraz sposób toodeploy, przeczytaj artykuł hello [co to jest Menedżer ruchu](../traffic-manager/traffic-manager-overview.md).

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>Wyłącz tooAzure dostępu protokołu RDP/SSH maszyny wirtualne
Jest możliwe tooreach maszyn wirtualnych platformy Azure przy użyciu hello [protokołu Remote Desktop Protocol](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) i hello [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) protokołów (SSH). Te protokoły była możliwa toomanage maszyn wirtualnych z lokalizacji zdalnych i standardowe w centrum danych obliczeniowych.

Witaj potencjalny problem zabezpieczeń przy użyciu tych protokołów za pośrednictwem hello Internet jest osoby atakujące mogą wykorzystać różnych [siłowych](https://en.wikipedia.org/wiki/Brute-force_attack) techniki toogain dostępu tooAzure maszyn wirtualnych. Po dostęp osoby atakujące hello ich użyć maszyny wirtualnej jako punkt wyjścia do naruszenia innych komputerów w sieci wirtualnej platformy Azure lub nawet ataki urządzeń sieciowych poza platformą Azure.

W związku z tym zaleca się wyłączenie bezpośredniego RDP i SSH dostępu tooyour maszyn wirtualnych platformy Azure z hello Internet. Po bezpośrednim RDP i SSH dostępu z hello Internet jest wyłączone, masz inne opcje służy tooaccess tych maszyn wirtualnych do zdalnego zarządzania:

* Sieć VPN punkt lokacja
* Sieci VPN typu lokacja lokacja
* ExpressRoute

[Sieć VPN punkt lokacja](../vpn-gateway/vpn-gateway-point-to-site-create.md) jest inna nazwa połączenia VPN klienta/serwera dostępu zdalnego. Sieć VPN punkt lokacja umożliwia tooan tooconnect pojedynczego użytkownika sieci wirtualnej platformy Azure za pośrednictwem hello Internet. Po nawiązaniu połączenia punkt lokacja hello, hello użytkownicy będą mogli toouse RDP lub SSH tooconnect tooany maszyn wirtualnych znajdujących się na powitania sieci wirtualnej platformy Azure, które hello użytkownika połączone toovia punkt lokacja sieci VPN. Przy założeniu, ten użytkownik hello jest autoryzowanym tooreach tych maszyn wirtualnych.

Sieci VPN typu punkt lokacja jest bezpieczniejsza niż bezpośrednich połączeń protokołu RDP lub SSH, ponieważ użytkownik hello ma tooauthenticate zanim łączące maszyny wirtualnej tooa. Najpierw hello tooauthenticate potrzebom użytkownika (i autoryzowanie) połączenie VPN punkt lokacja hello tooestablish; Po drugie, hello tooauthenticate potrzebom użytkownika (i autoryzowanie) hello tooestablish sesji protokołu RDP lub SSH.

A [sieci VPN typu lokacja lokacja](../vpn-gateway/vpn-gateway-site-to-site-create.md) łączy sieć tooanother cała sieć za pośrednictwem hello Internet. Możesz użyć tooconnect sieci VPN typu lokacja lokacja z tooan sieci lokalnej sieci wirtualnej platformy Azure. W przypadku wdrożenia sieci VPN lokacja lokacja, użytkownicy w sieci lokalnej będą mogli tooconnect toovirtual maszyny w sieci wirtualnej platformy Azure przy użyciu hello RDP lub protokołu SSH ponad hello połączenia sieci VPN lokacja lokacja i nie wymaga tooallow bezpośrednie połączenie RDP lub SSH dostęp za pośrednictwem hello Internet.

Można również użyć dedykowanego łącza sieci WAN toohello podobne funkcje tooprovide sieci VPN typu lokacja lokacja. główne różnice Hello to 1. dedykowane łącza sieci WAN Hello nie przechodzenia hello Internet i 2. dedykowane łącza sieci WAN są zazwyczaj więcej stabilności i wydajności. Platforma Azure udostępnia rozwiązanie dedykowane łącza sieci WAN w formie hello [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="enable-azure-security-center"></a>Centrum zabezpieczeń Azure Włącz
Centrum zabezpieczeń Azure pomaga zapobiec, wykrywania i reagowania toothreats i zapewnia zwiększyć widoczność i kontrolę nad, hello zabezpieczeń zasobów platformy Azure. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

Centrum zabezpieczeń Azure ułatwia optymalizacji i monitorować przez zabezpieczenia sieci:

* Udostępnia zalecenia dotyczące zabezpieczeń sieci
* Monitorowanie stanu hello konfiguracji zabezpieczeń sieci
* Alerty na podstawie toonetwork zagrożenia obu poziomach hello punktu końcowego i sieci

Zdecydowanie zaleca się włączenie Centrum zabezpieczeń Azure dla wszystkich wdrożeń platformy Azure.

więcej informacji na temat Centrum zabezpieczeń Azure oraz jak tooenable dla wdrożeń, przeczytaj artykuł hello toolearn [tooAzure wprowadzenie Centrum zabezpieczeń](../security-center/security-center-intro.md).

## <a name="securely-extend-your-datacenter-into-azure"></a>Bezpieczne rozszerzenie centrum danych na platformie Azure
Wiele organizacji IT organizacji szukasz tooexpand w chmurze hello zamiast rośnie ich lokalnych centrów danych. To rozwinięcie reprezentuje rozszerzeniem istniejącej infrastruktury informatycznej do chmury publicznej hello. Dzięki wykorzystaniu między lokalizacjami jest możliwe tootreat opcji łączności sieci wirtualne Azure jako po prostu inną podsieć w lokalnej sieci infrastruktury.

Jednak wiele planowania i zagadnienia, które wymagają toobe rozwiązany pierwszy. Jest to szczególnie ważne w obszarze hello zabezpieczeń sieci. Jeden hello najlepszych metod toounderstand podejście do tego projektu jest toosee przykład.

Firma Microsoft opracowała hello [Diagram architektury odwołanie rozszerzenia Datacenter](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) i obsługi dodatkowych toohelp rozumiesz, jak będzie wyglądać rozszerzenia centrum danych. Zapewnia to przykładem implementacji odniesienia można użyć tooplan i chmurę toohello rozszerzenia centrum danych przedsiębiorstwa bezpiecznego projektu. Firma Microsoft zaleca zapoznanie się tego dokumentu tooget pomysł hello najważniejsze składniki bezpiecznego rozwiązania.

toolearn więcej informacji na temat sposobu toosecurely rozszerzona centrum danych Azure, zapoznaj się z wideo hello [tooMicrosoft rozszerzanie Your Datacenter Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA).
