---
title: "Azure VPN Gateway — często zadawane pytania | Microsoft Docs"
description: "Brama sieci VPN — często zadawane pytania Często zadawane pytania dotyczące połączeń obejmujących wiele lokalizacji, połączeń w konfiguracji hybrydowej oraz bram usługi VPN Gateway w usłudze Microsoft Azure Virtual Network."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2017
ms.author: cherylmc,yushwang,anzaman
ms.openlocfilehash: 2b648caa51eb457a62e846b74f1b95ca84974635
ms.sourcegitcommit: 901a3ad293669093e3964ed3e717227946f0af96
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="vpn-gateway-faq"></a>Brama sieci VPN — często zadawane pytania

## <a name="connecting"></a>Łączenie z sieciami wirtualnymi

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>Czy można połączyć sieci wirtualne z różnych regionów świadczenia usługi Azure?

Tak. Nie ma żadnych ograniczeń dotyczących regionów. Jedna sieć wirtualna może nawiązać połączenie z inną siecią wirtualną w tym samym lub w innym regionie świadczenia usługi Azure. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>Czy można połączyć sieci wirtualne należące do różnych subskrypcji?

Tak.

### <a name="can-i-connect-to-multiple-sites-from-a-single-virtual-network"></a>Czy można łączyć się z wieloma lokalizacjami z jednej sieci wirtualnej?

Można nawiązać połączenie z wieloma lokalizacjami za pomocą programu Windows PowerShell oraz interfejsów API REST Azure. Zobacz sekcję często zadawanych pytań dotyczących [połączeń obejmujących wiele lokacji i połączeń między sieciami wirtualnymi](#V2VMulti).

### <a name="what-are-my-cross-premises-connection-options"></a>Jakie są dostępne możliwości połączeń obejmujących wiele lokalizacji?

Obsługiwane są następujące połączenia obejmujące wiele lokalizacji:

* Lokacja-lokacja — połączenie sieci VPN nawiązywane za pośrednictwem protokołu IPsec (IKE v1 i IKE v2). Ten typ połączenia wymaga urządzenia VPN lub usługi RRAS. Aby uzyskać więcej informacji, zobacz [Lokacja-lokacja](vpn-gateway-howto-site-to-site-resource-manager-portal.md).
* Punkt-lokacja — połączenie sieci VPN nawiązywane za pośrednictwem protokołu SSTP (Secure Socket Tunneling Protocol) lub IKE v2. To połączenie nie wymaga urządzenia VPN. Aby uzyskać więcej informacji, zobacz [Punkt-lokacja](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Sieć wirtualna-sieć wirtualna — tego typu połączenie odpowiada konfiguracji typu lokacja-lokacja. Połączenie typu sieć wirtualna-sieć wirtualna to połączenie sieci VPN nawiązywane za pośrednictwem protokołu IPsec (IKE v1 i IKE v2). To połączenie nie wymaga urządzenia VPN. Aby uzyskać więcej informacji, zobacz [Sieć wirtualna-sieć wirtualna](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).
* Obejmujące wiele lokacji — konfiguracja typu lokacja-lokacja, która pozwala połączyć wiele lokacji lokalnych z siecią wirtualną. Aby uzyskać więcej informacji, zobacz [Wiele lokacji](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).
* ExpressRoute — ExpressRoute to bezpośrednie połączenie z platformą Azure nawiązywane z poziomu sieci WAN, a nie połączenie sieci VPN z publicznego Internetu. Więcej informacji zawierają tematy [ExpressRoute — opis techniczny](../expressroute/expressroute-introduction.md) i [Usługa ExpressRoute — często zadawane pytania](../expressroute/expressroute-faqs.md).

Aby uzyskać więcej informacji na temat połączeń bramy sieci VPN, zobacz artykuł [VPN Gateway — informacje](vpn-gateway-about-vpngateways.md).

### <a name="what-is-the-difference-between-a-site-to-site-connection-and-point-to-site"></a>Jaka jest różnica między połączeniem typu lokacja-lokacja i połączeniem typu punkt-lokacja?

Konfiguracje **lokacja-lokacja** (tunel VPN protokołu IPsec/IKE) dotyczą połączenia między lokalizacją lokalną a platformą Azure. Oznacza to, że z poziomu dowolnego lokalnego komputera możesz połączyć się z dowolną maszyną wirtualną lub wystąpieniem roli w ramach sieci wirtualnej, w zależności od wybranej konfiguracji routingu i uprawnień. To rozwiązanie doskonale sprawdza się w przypadku zawsze dostępnych połączeń obejmujących wiele lokalizacji; jest to także dobry wybór w przypadku konfiguracji hybrydowych. Ten typ połączenia jest oparty na urządzeniu VPN (sprzętowym lub programowym) z protokołem IPsec, które musi zostać wdrożone na granicy sieci. W celu utworzenia tego typu połączenia musisz mieć dostępny z zewnątrz adres IPv4, który nie znajduje się poza translatorem adresów sieciowych.

Konfiguracje **punkt-lokacja** (VPN z protokołem SSTP) umożliwiają połączenie się z pojedynczego komputera znajdującego się w dowolnym miejscu z innym dowolnym miejscem w sieci wirtualnej. Korzystają z wewnętrznego klienta VPN systemu Windows. W ramach konfiguracji typu punkt-lokacja należy zainstalować certyfikat i pakiet konfiguracji klienta VPN, który zawiera ustawienia umożliwiające komputerowi połączenie się z dowolną maszyną wirtualną lub wystąpieniem roli w ramach sieci wirtualnej. Doskonale sprawdzają się podczas nawiązywania połączenia z siecią wirtualną spoza obszaru organizacji. To także dobra opcja w sytuacji braku dostępu do sprzętu VPN lub adresu IPv4 dostępnego z zewnątrz, które są wymagane w przypadku połączeń typu lokacja-lokacja.

Sieć wirtualną można skonfigurować pod kątem równoległego użycia metod lokacja-lokacja i punkt-lokacja, o ile połączenie lokacja-lokacja zostanie utworzone z użyciem bramy sieci VPN opartej na trasach. Typy bramy sieci VPN oparte na trasach są w klasycznym modelu wdrażania nazywane bramami dynamicznymi.

## <a name="gateways"></a>Bramy sieci wirtualnej

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>Czy brama sieci VPN jest bramą sieci wirtualnej?

Brama sieci VPN to typ bramy sieci wirtualnej. Brama sieci VPN przesyła zaszyfrowany ruch sieciowy między siecią wirtualną a lokalizacją lokalną za pośrednictwem połączenia publicznego. Za pomocą bramy sieci VPN można również przesyłać ruch sieciowy między sieciami wirtualnymi. Po utworzeniu bramy sieci VPN dla opcji -GatewayType należy używać wartości „Vpn”. Aby uzyskać więcej informacji, zobacz temat [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md) (Informacje o ustawieniach konfiguracji bramy VPN Gateway).

### <a name="what-is-a-policy-based-static-routing-gateway"></a>Co to jest brama oparta na zasadach (o routingu statycznym)?

Bramy oparte na zasadach wdrażają sieci VPN oparte na zasadach. Sieci VPN oparte na zasadach szyfrują pakiety i kierują je bezpośrednio przez tunele protokołu IPsec na podstawie kombinacji prefiksów adresów między siecią lokalną użytkownika i siecią wirtualną platformy Azure. Zasady (lub selektor ruchu) są zazwyczaj zdefiniowane jako lista dostępu w konfiguracji VPN.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>Co to jest brama oparta na trasach (o routingu dynamicznym)?

Bramy oparte na trasach wdrażają sieci VPN oparte na trasach. Sieci VPN oparte na trasach używają „tras” w funkcji przesyłania dalej IP lub tabeli routingu do kierowania pakietów do odpowiednich interfejsów tuneli. W dalszej kolejności interfejsy tuneli szyfrują lub odszyfrowują pakiety wchodzące do tuneli lub wychodzące z nich. Zasady lub selektor ruchu dla sieci VPN opartych na trasach są skonfigurowane jako każdy z każdym (lub symbole wieloznaczne).

### <a name="can-i-update-my-policy-based-vpn-gateway-to-route-based"></a>Czy mogę zaktualizować moją bramę sieci VPN opartą na zasadach do opartej na trasach?
Nie. Nie można zmienić typu bramy sieci wirtualnej platformy Azure z opartej na zasadach na opartą na trasach ani w inny sposób. Bramę należy usunąć i utworzyć ponownie. Cały taki proces zajmie około 60 minut. Adres IP bramy ani klucz wstępny (PSK) nie zostaną zachowane.
1. Usuń wszystkie połączenia skojarzone z bramą do usunięcia.
2. Usuń bramę:
* [Azure Portal](vpn-gateway-delete-vnet-gateway-portal.md)
* [Azure PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
* [Azure PowerShell — wersja klasyczna](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
3. [Utwórz nową bramę odpowiedniego typu i zakończ konfigurowanie sieci VPN](vpn-gateway-howto-site-to-site-resource-manager-portal.md#VNetGateway)

### <a name="do-i-need-a-gatewaysubnet"></a>Czy potrzebuję podsieci „GatewaySubnet”?

Tak. Podsieć bramy zawiera adresy IP używane przez usługi bramy sieci wirtualnej. Aby skonfigurować bramę sieci wirtualnej, musisz utworzyć podsieć bramy dla sieci wirtualnej. Aby podsieć bramy działała prawidłowo, musi nosić nazwę „GatewaySubnet”. Nie należy nadawać podsieci bramy innej nazwy. Nie należy także wdrażać maszyn wirtualnych ani innych elementów w ramach podsieci bramy.

Podczas tworzenia podsieci bramy należy określić liczbę zawartych w niej adresów IP. Adresy IP w podsieci bramy są przydzielone do usługi bramy. Niektóre konfiguracje wymagają przydzielenia większej liczby adresów IP do usług bramy niż inne. Warto się upewnić, że podsieć bramy zawiera wystarczającą liczbę adresów IP na potrzeby przyszłego rozwoju i możliwe dodatkowe, nowe konfiguracje połączeń. Dlatego, chociaż można utworzyć małą podsieć bramy o rozmiarze /29, zaleca się tworzenie podsieci bramy /27 i większych (/27, /26, /25 itp.). Zapoznaj się z wymaganiami konfiguracji, którą chcesz utworzyć, i sprawdź, czy Twoja brama podsieci je spełni.

### <a name="can-i-deploy-virtual-machines-or-role-instances-to-my-gateway-subnet"></a>Czy można wdrożyć maszyny wirtualne lub wystąpienia roli w ramach podsieci bramy?

Nie.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>Czy można użyć adresu IP bramy sieci VPN przed jej utworzeniem?

Nie. Aby uzyskać adres IP bramy, należy ją najpierw utworzyć. Adres IP ulegnie zmianie, jeśli brama VPN zostanie usunięta i ponownie utworzona.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>Czy mogę zażądać przypisania statycznego publicznego adresu IP do mojej bramy sieci VPN?

Nie. Obsługiwane jest tylko dynamiczne przypisywanie adresów IP. Nie oznacza to jednak, że adres IP zmienia się po przypisaniu go do bramy sieci VPN. Jedyną sytuacją, w której ma miejsce zmiana adresu IP bramy sieci VPN, jest usunięcie bramy i jej ponowne utworzenie. Publiczny adres IP bramy sieci VPN nie zmienia się w przypadku zmiany rozmiaru, zresetowania ani w przypadku przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>W jaki sposób następuje uwierzytelnienie tunelu VPN?

Sieć VPN platformy Azure używa uwierzytelniania PSK (klucza wstępnego). Podczas tworzenia tunelu VPN generowany jest klucz wstępny (PSK). Wygenerowany automatycznie klucz wstępny można zmienić na własny klucz przy użyciu polecenia cmdlet Set Pre-Shared Key lub interfejsu API REST programu PowerShell.

### <a name="can-i-use-the-set-pre-shared-key-api-to-configure-my-policy-based-static-routing-gateway-vpn"></a>Czy za pomocą interfejsu API i polecenia cmdlet Set Pre-Shared Key można skonfigurować własną bramę sieci VPN opartą na zasadach (o routingu statycznym)?

Tak, interfejs API i polecenie cmdlet Set Pre-Shared Key programu PowerShell pozwalają konfigurować sieci wirtualne platformy Azure oparte na zasadach (o statycznym routingu) i na trasach (o dynamicznym routingu).

### <a name="can-i-use-other-authentication-options"></a>Czy są dostępne inne opcje uwierzytelniania?

Metody uwierzytelniania ograniczają się do stosowania kluczy wstępnych (PSK).

### <a name="how-do-i-specify-which-traffic-goes-through-the-vpn-gateway"></a>Jak określić, który ruch danych przechodzi przez bramę sieci VPN?

#### <a name="resource-manager-deployment-model"></a>Model wdrażania usługi Resource Manager

* Środowisko PowerShell: użyj elementu „AddressPrefix”, aby określić ruch dla lokalnej bramy sieci.
* Witryna Azure Portal: przejdź do bramy sieci lokalnej > Konfiguracja > Przestrzeń adresowa.

#### <a name="classic-deployment-model"></a>Klasyczny model wdrażania

* Witryna Azure Portal: przejdź do klasycznej sieci wirtualnej > Połączenia sieci VPN > Połączenia sieci VPN typu lokacja-lokacja > Nazwy lokacji lokalnej > Lokacja lokalna > Przestrzeń adresowa klienta. 

### <a name="can-i-configure-force-tunneling"></a>Czy mogę skonfigurować wymuszone tunelowanie?

Tak. Zobacz [Configure force tunneling](vpn-gateway-about-forced-tunneling.md) (Konfigurowanie wymuszonego tunelowania).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-to-connect-to-my-on-premises-network"></a>Czy można wdrożyć własny serwer sieci VPN na platformie Azure i używać go do nawiązywania połączenia z siecią lokalną?

Tak, można wdrożyć własne bramy lub serwery sieci VPN na platformie Azure, korzystając z portalu Azure Marketplace lub tworząc własne routery sieci VPN. W sieci wirtualnej należy skonfigurować trasy zdefiniowane przez użytkownika, aby upewnić się, że ruch jest prawidłowo przekierowywany między sieciami lokalnymi i podsieciami sieci wirtualnej.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>Dlaczego niektóre porty mojej bramy sieci VPN są otwarte?

Są one wymagane do komunikacji infrastruktury platformy Azure. Są one zabezpieczone (zablokowane) z użyciem certyfikatów Azure. Bez prawidłowych certyfikatów podmioty zewnętrzne, w tym klienci tych bram, nie będą mieć możliwości wywarcia jakiegokolwiek wpływu na te punkty końcowe.

Brama sieci VPN to zasadniczo wieloadresowe urządzenie, w przypadku którego jedna karta interfejsu sieciowego korzysta z sieci prywatnej klienta, a do drugiej można uzyskać dostęp z sieci publicznej. Podmioty infrastruktury platformy Azure nie mogą korzystać z sieci prywatnych klientów z przyczyn związanych z zachowaniem zgodności, w związku z czym muszą korzystać z publicznych punktów końcowych do komunikacji w ramach infrastruktury. Publiczne punkty końcowe są okresowo skanowane w ramach inspekcji zabezpieczeń platformy Azure.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Więcej informacji na temat typów, wymagań i przepływności bram

Aby uzyskać więcej informacji, zobacz temat [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md) (Informacje o ustawieniach konfiguracji bramy VPN Gateway).

## <a name="s2s"></a>Połączenia typu lokacja-lokacja a urządzenia sieci VPN

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>Co należy wziąć pod uwagę przy wyborze urządzenia sieci VPN?

Zweryfikowaliśmy we współpracy z dostawcami urządzeń szereg standardowych urządzeń sieci VPN wykorzystywanych w ramach połączeń typu lokacja-lokacja. Listę znanych zgodnych urządzeń sieci VPN, odpowiednie instrukcje konfiguracji lub przykłady oraz dane techniczne urządzeń można znaleźć w artykule [Informacje na temat urządzeń sieci VPN](vpn-gateway-about-vpn-devices.md). Wszystkie urządzenia z rodzin wymienionych jako rodziny o znanej zgodności powinny współpracować z siecią wirtualną. Aby skonfigurować urządzenie sieci VPN, zapoznaj się z przykładową konfiguracją urządzenia lub łączem odpowiadającym odpowiedniej rodzinie urządzeń.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>Gdzie można znaleźć ustawienia konfiguracji urządzenia sieci VPN?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>Jak edytować przykłady konfiguracji urządzenia sieci VPN?

Aby uzyskać informacje na temat edytowania przykładów konfiguracji urządzeń, zobacz [Edytowanie przykładów](vpn-gateway-about-vpn-devices.md#editing).

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>Gdzie można znaleźć parametry protokołów IPsec i IKE?

Aby zapoznać się z parametrami protokołów IPsec/IKE, zobacz [Parametry](vpn-gateway-about-vpn-devices.md#ipsec).

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>Dlaczego mój oparty na zasadach tunel VPN przestaje działać, gdy ruch jest w stanie bezczynności?

Jest to oczekiwane zachowanie bram sieci VPN opartych na zasadach (znanych także jako bramy o routingu statycznym). Jeśli ruch za pośrednictwem tunelu będzie pozostawał w stanie bezczynności przez więcej niż 5 minut, nastąpi jego usunięcie. Natychmiast po rozpoczęciu ruchu danych w dowolnym kierunku będzie można ponownie ustanowić tunel.

### <a name="can-i-use-software-vpns-to-connect-to-azure"></a>Czy można użyć oprogramowania pełniącego rolę sieci VPN do nawiązania połączenia z usługą Azure?

W ramach konfiguracji typu lokacja-lokacja obejmującej wiele lokalizacji obsługiwane są serwery Windows Server 2012 usługi Routing i dostęp zdalny (RRAS).

Inne rozwiązania o charakterze oprogramowania pełniącego rolę sieci VPN powinny współpracować z bramą, o ile są one zgodne ze standardowymi implementacjami protokołu IPsec stosowanymi w branży. W celu uzyskania pomocy technicznej oraz instrukcji konfiguracji należy skontaktować się z dostawcą oprogramowania.

## <a name="P2S"></a>Punkt-lokacja — natywne uwierzytelnianie certyfikatu platformy Azure

Ta sekcja dotyczy modelu wdrażania przy użyciu usługi Resource Manager.

[!INCLUDE [P2S Azure cert](../../includes/vpn-gateway-faq-p2s-azurecert-include.md)]

## <a name="P2SRADIUS"></a>Punkt-lokacja — uwierzytelnianie za pomocą protokołu RADIUS

Ta sekcja dotyczy modelu wdrażania przy użyciu usługi Resource Manager.

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-faq-p2s-radius-include.md)]

## <a name="V2VMulti"></a>Połączenia między sieciami wirtualnymi i połączenia obejmujące wiele lokacji

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-faq-vnet-vnet-include.md)]

### <a name="can-i-use-azure-vpn-gateway-to-transit-traffic-between-my-on-premises-sites-or-to-another-virtual-network"></a>Czy można używać bramy Azure VPN do przekazywania ruchu między lokacjami lokalnymi lub do innej sieci wirtualnej?

**Model wdrażania usługi Resource Manager**<br>
Tak. Więcej informacji zawiera sekcja [BGP](#bgp).

**Klasyczny model wdrażania**<br>
Przekazywanie ruchu za pośrednictwem bramy sieci VPN platformy Azure przy użyciu klasycznego modelu wdrażania jest możliwe, ale zależy od statycznie zdefiniowanych przestrzeni adresowych w pliku konfiguracyjnym sieci. Protokół BGP dla klasycznego modelu wdrażania nie jest jeszcze obsługiwany w połączeniu z sieciami wirtualnymi platformy Azure i bramami sieci VPN. Niezastosowanie protokołu BGP powoduje bardzo wysokie ryzyko błędów ręcznego definiowania przestrzeni adresowych przesyłania i nie jest zalecane.

### <a name="does-azure-generate-the-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-the-same-virtual-network"></a>Czy platforma Azure generuje taki sam klucz wstępny protokołu IPsec/IKE dla wszystkich połączeń sieci VPN dla danej sieci wirtualnej?

Nie. Platforma Azure domyślnie generuje różne klucze wstępne dla różnych połączeń sieci VPN. Można jednak użyć interfejsu API REST lub polecenia cmdlet Set VPN Gateway Key programu PowerShell, aby ustawić preferowaną wartość klucza. Klucz MUSI mieć postać alfanumerycznego ciągu o długości od 1 do 128 znaków.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>Czy przy większej liczbie połączeń VPN typu lokacja-lokacja można uzyskać większą przepustowość niż przy pojedynczej sieci wirtualnej?

Nie, wszystkie tunele VPN, w tym połączenia VPN typu punkt-lokacja, współdzielą tę samą bramę sieci VPN platformy Azure i dostępną przepustowość.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>Czy można skonfigurować wiele tuneli między siecią wirtualną i lokalną lokacją z użyciem sieci VPN obejmującej wiele lokacji?

Tak, ale należy skonfigurować protokół BGP w obu tunelach do tej samej lokalizacji.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>Czy można używać sieci VPN typu punkt-lokacja z siecią wirtualną z wieloma tunelami VPN?

Tak, sieci VPN typu punkt-lokacja (P2S) można używać z bramami sieci VPN łączącymi się z wieloma lokacjami lokalnymi i innymi sieciami wirtualnymi.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-to-my-expressroute-circuit"></a>Czy można połączyć sieć wirtualną z sieciami VPN wykorzystującymi protokół IPsec z obwodem ExpressRoute?

Tak, takie rozwiązanie jest obsługiwane. Aby uzyskać więcej informacji, zobacz artykuł [Configure ExpressRoute and Site-to-Site VPN connections that coexist](../expressroute/expressroute-howto-coexist-classic.md) (Konfigurowanie obwodu ExpressRoute i współistniejących połączeń sieci VPN typu lokacja-lokacja).

## <a name="ipsecike"></a>Zasady protokołu IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-faq-ipsecikepolicy-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-faq-bgp-include](../../includes/vpn-gateway-faq-bgp-include.md)]

## <a name="vms"></a>Połączenia obejmujące wiele lokalizacji a maszyny wirtualne

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-to-the-vm"></a>W jaki sposób należy połączyć się z maszyną wirtualną w przypadku, gdy należy ona do sieci wirtualnej, a dysponuję połączeniem obejmującym wiele lokalizacji?

Jest kilka możliwości. Jeśli masz włączony protokół RDP dla swojej maszyny wirtualnej, możesz się z nią łączyć, korzystając z prywatnego adresu IP. W takim przypadku należy określić prywatny adres IP i numer portu, z którym ma zostać nawiązane połączenie (zwykle 3389). Należy skonfigurować port maszyny wirtualnej pod kątem ruchu danych.

Z maszyną wirtualną można także nawiązać połączenie z poziomu innej maszyny wirtualnej, która znajduje się w tej samej sieci wirtualnej, korzystając z prywatnego adresu IP. Nie można połączyć się z maszyną wirtualną z użyciem protokołu RDP i prywatnego adresu IP, jeśli połączenie jest nawiązywane z lokalizacji spoza sieci wirtualnej. Na przykład jeśli w przypadku dostępności skonfigurowanej sieci wirtualnej typu punkt-lokacja nie zostanie ustanowione połączenie z poziomu komputera, nie będzie możliwe połączenie się z maszyną wirtualną z użyciem prywatnego adresu IP.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-the-traffic-from-my-vm-go-through-that-connection"></a>Czy jeśli maszyna wirtualna należy do sieci wirtualnej z funkcją łączności obejmującą wiele lokalizacji, to cały ruch z niej będzie przekazywany za pośrednictwem tego połączenia?

Nie. Przez bramę sieci wirtualnej przechodzi tylko ruch, którego docelowy adres IP należy do określonych zakresów adresów IP sieci lokalnej w ramach sieci wirtualnej. Ruch, którego docelowy adres IP należy do sieci wirtualnej, pozostaje w obrębie sieci wirtualnej. Inny ruch jest wysyłany do sieci publicznej za pośrednictwem usługi równoważenia obciążenia lub, w przypadku użycia wymuszonego tunelowania, wysłany przez bramę sieci VPN platformy Azure.

### <a name="how-do-i-troubleshoot-an-rdp-connection-to-a-vm"></a>Jak rozwiązywać problemy z połączeniem RDP z maszyną wirtualną

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Sieć wirtualna — często zadawane pytania

Dodatkowe informacje dotyczące sieci wirtualnej można znaleźć w artykule [Virtual Network FAQ](../virtual-network/virtual-networks-faq.md) (Sieć wirtualna — często zadawane pytania).

## <a name="next-steps"></a>Następne kroki

* Więcej informacji o usłudze VPN Gateway można znaleźć w artykule [VPN Gateway — informacje](vpn-gateway-about-vpngateways.md).
* Aby uzyskać więcej informacji o ustawieniach konfiguracji bramy VPN Gateway, zobacz temat [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md) (Informacje o ustawieniach konfiguracji bramy VPN Gateway).
