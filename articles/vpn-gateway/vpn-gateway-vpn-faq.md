---
title: "aaaAzure bramy sieci VPN — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Witaj bramy sieci VPN — często zadawane pytania. Często zadawane pytania dotyczące połączeń obejmujących wiele lokalizacji, połączeń w konfiguracji hybrydowej oraz bram usługi VPN Gateway w usłudze Microsoft Azure Virtual Network."
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
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>Brama sieci VPN — często zadawane pytania

## <a name="connecting"></a>Łączenie z sieciami toovirtual

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>Czy można połączyć sieci wirtualne z różnych regionów świadczenia usługi Azure?

Tak. Nie ma żadnych ograniczeń dotyczących regionów. Jedną sieć wirtualną można połączyć sieć wirtualną tooanother w hello tego samego regionu, lub w innym regionie Azure. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>Czy można połączyć sieci wirtualne należące do różnych subskrypcji?

Tak.

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>Z jednej sieci wirtualne można łączyć toomultiple witryn?

Możesz połączyć toomultiple witryny przy użyciu programu Windows PowerShell i hello interfejsów API REST usługi Azure. Zobacz hello [obejmujący wiele lokacji i łączności do wirtualnymi](#V2VMulti) sekcji często zadawanych PYTAŃ.

### <a name="what-are-my-cross-premises-connection-options"></a>Jakie są dostępne możliwości połączeń obejmujących wiele lokalizacji?

powitania po między lokalizacjami się, że połączenia są obsługiwane:

* Lokacja-lokacja — połączenie sieci VPN nawiązywane za pośrednictwem protokołu IPsec (IKE v1 i IKE v2). Ten typ połączenia wymaga urządzenia VPN lub usługi RRAS. Aby uzyskać więcej informacji, zobacz [Lokacja-lokacja](vpn-gateway-howto-site-to-site-resource-manager-portal.md).
* Punkt-lokacja — połączenie sieci VPN nawiązywane za pośrednictwem protokołu SSTP (Secure Socket Tunneling Protocol). To połączenie nie wymaga urządzenia VPN. Aby uzyskać więcej informacji, zobacz [Punkt-lokacja](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Aby wirtualnymi — tego typu połączenia jest hello taki sam jak konfiguracji lokacja-lokacja. TooVNet sieci wirtualnej jest połączenie sieci VPN za pośrednictwem protokołu IPsec (IKE v1 i IKE v2). To połączenie nie wymaga urządzenia VPN. Aby uzyskać więcej informacji, zobacz [Sieć wirtualna-sieć wirtualna](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).
* Obejmujący wiele lokacji — jest to zmianę konfiguracji lokacja-lokacja, która pozwala tooconnect wiele witryn tooa wirtualnej sieci lokalnej. Aby uzyskać więcej informacji, zobacz [Wiele lokacji](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).
* ExpressRoute — ExpressRoute jest tooAzure bezpośrednie połączenie z sieci WAN, nie połączenie sieci VPN za pośrednictwem hello publicznej sieci Internet. Aby uzyskać więcej informacji, zobacz hello [opis techniczny ExpressRoute](../expressroute/expressroute-introduction.md) i hello [ExpressRoute — często zadawane pytania](../expressroute/expressroute-faqs.md).

Aby uzyskać więcej informacji na temat połączeń bramy sieci VPN, zobacz artykuł [VPN Gateway — informacje](vpn-gateway-about-vpngateways.md).

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>Jaka jest różnica hello połączenie lokacja-lokacja i punkt-lokacja?

Konfiguracje **lokacja-lokacja** (tunel VPN protokołu IPsec/IKE) dotyczą połączenia między lokalizacją lokalną a platformą Azure. Oznacza to, że można połączyć z wszelkich komputerów znajdujących się na lokalnej maszynie wirtualnej tooany lub wystąpienia roli w ramach sieci wirtualnej, w zależności od wybranego sposobu tooconfigure routingu i uprawnienia. To rozwiązanie doskonale sprawdza się w przypadku zawsze dostępnych połączeń obejmujących wiele lokalizacji; jest to także dobry wybór w przypadku konfiguracji hybrydowych. Urządzenia IPsec sieci VPN (urządzenia sprzętowego lub nietrwałego urządzenia), które muszą być wdrożone na krawędzi hello sieci zależy od tego typu połączenia. toocreate połączenia tego typu musi mieć adres IPv4 połączonej zewnętrznie, który nie znajduje się za urządzeniem NAT;

**Punkt-lokacja** konfiguracji (sieć VPN przez protokół SSTP) umożliwiają nawiązywanie połączenia z jednego komputera z dowolnego miejsca tooanything znajduje się w sieci wirtualnej. Klient sieci VPN w polu Windows hello jest używany. W ramach konfiguracji hello punkt do lokacji należy zainstalować certyfikat i pakiet konfiguracji klienta sieci VPN, zawierający ustawienia hello, które zezwalają na Twojej maszyny wirtualnej tooany tooconnect komputera lub wystąpienia roli w ramach sieci wirtualnej hello. Jest bardzo mają sieci wirtualnej tooa tooconnect, ale nie są znajdujących się lokalnie. Jest również dobrym rozwiązaniem, gdy nie masz dostępu do sprzętu tooVPN lub adres IPv4 połączonej zewnętrznie, które są wymagane dla połączenia lokacja-lokacja.

I toouse Twojej sieci wirtualnej można skonfigurować zarówno do lokacji typu punkt-lokacja jednocześnie, tak długo, jak utworzyć połączenie lokacja-lokacja przy użyciu sieci VPN opartej na trasach dla bramy. Typy sieci VPN opartej na trasach są nazywane bramy dynamiczne hello klasycznego modelu wdrażania.

## <a name="gateways"></a>Bramy sieci wirtualnej

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>Czy brama sieci VPN jest bramą sieci wirtualnej?

Brama sieci VPN to typ bramy sieci wirtualnej. Brama sieci VPN przesyła zaszyfrowany ruch sieciowy między siecią wirtualną a lokalizacją lokalną za pośrednictwem połączenia publicznego. Umożliwia także ruchu toosend bramy sieci VPN między sieciami wirtualnymi. Podczas tworzenia bramy sieci VPN, możesz użyć wartości elementu GatewayType — Witaj "Vpn". Aby uzyskać więcej informacji, zobacz temat [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md) (Informacje o ustawieniach konfiguracji bramy VPN Gateway).

### <a name="what-is-a-policy-based-static-routing-gateway"></a>Co to jest brama oparta na zasadach (o routingu statycznym)?

Bramy oparte na zasadach wdrażają sieci VPN oparte na zasadach. Sieci VPN oparte na zasadach szyfrują i kierowania pakietów przez tunel protokołu IPsec na podstawie hello kombinacji prefiksów adresów między siecią lokalną a hello sieci wirtualnej platformy Azure. Witaj zasady (lub selektor ruchu) są zazwyczaj zdefiniowane jako lista dostępu w konfiguracji sieci VPN hello.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>Co to jest brama oparta na trasach (o routingu dynamicznym)?

Wdrożenie bramy oparte na trasach hello VPN opartej na trasach. VPN opartej na trasach używają "tras" hello IP przekazywania lub pakietów toodirect tabeli routingu do odpowiednich interfejsów tuneli. następnie interfejsów tuneli Hello szyfrowania lub odszyfrowywania pakietów hello i hello tuneli. Witaj selektor zasad lub ruchu dla VPN opartej na trasach są skonfigurowane jako dowolny z każdym (lub symbole wieloznaczne).

### <a name="do-i-need-a-gatewaysubnet"></a>Czy potrzebuję podsieci „GatewaySubnet”?

Tak. podsieć bramy Hello zawiera adresy IP hello korzystających z usługi bramy sieci wirtualnej hello. Należy toocreate podsieci bramy sieci wirtualnej w kolejności tooconfigure bramy sieci wirtualnej. Wszystkie podsieci bramy muszą nosić nazwy "GatewaySubnet" toowork poprawnie. Nie należy nadawać podsieci bramy innej nazwy. I nie wdrażać maszyny wirtualne lub cokolwiek innego toohello podsieci bramy.

Podczas tworzenia podsieci bramy hello Określ zawiera hello liczbę adresów IP, które hello podsieci. Witaj w podsieci bramy hello adresy IP toohello Usługa bramy. Niektóre konfiguracje wymagają więcej toobe adresy IP przydzielone toohello usługi bramy niż innym. Ma toomake się, że podsieć bramy zawiera za mało adresów IP tooaccommodate przyszłego rozwoju i możliwe dodatkowe konfiguracje nowego połączenia. Dlatego, chociaż można utworzyć małą podsieć bramy o rozmiarze /29, zaleca się tworzenie podsieci bramy /27 i większych (/27, /26, /25 itp.). Obejrzyj hello wymagania dotyczące konfiguracji hello mają toocreate i sprawdź, czy podsieci bramy hello posiadanego będzie spełnienia tych wymagań.

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>Można wdrożyć maszyn wirtualnych lub podsieci bramy toomy wystąpień roli?

Nie.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>Czy można użyć adresu IP bramy sieci VPN przed jej utworzeniem?

Nie. Masz toocreate Twojego pierwszego tooget hello adres IP bramy. Witaj zmiany adresu IP, jeśli usunięcie i ponowne utworzenie bramy sieci VPN.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>Czy mogę zażądać przypisania statycznego publicznego adresu IP do mojej bramy sieci VPN?

Nie. Obsługiwane jest tylko dynamiczne przypisywanie adresów IP. Jednak nie oznacza to, że adres IP hello ulegnie zmianie po przypisaniu tooyour bramy sieci VPN. Hello czasu tylko zmiany adresu IP bramy sieci VPN hello jest hello gdy brama zostanie usunięta i utworzona ponownie. Witaj publiczny adres IP bramy sieci VPN nie powoduje zmiany całej zmiany rozmiaru, resetowania lub innych wewnętrzny konserwacji/uaktualnienia bramy sieci VPN. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>W jaki sposób następuje uwierzytelnienie tunelu VPN?

Sieć VPN platformy Azure używa uwierzytelniania PSK (klucza wstępnego). Firma Microsoft generowania klucza wstępnego (PSK) utworzymy hello tunel VPN. Możesz zmienić hello automatycznie generowanej PSK tooyour własnych hello Ustaw wstępny klucz polecenia cmdlet programu PowerShell lub interfejsu API REST.

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>Można używać tooconfigure ustawić API klucz wstępny hello Moje opartych na zasadach (statyczny routing) bramy sieci VPN?

Tak, hello Ustaw wstępny klucz interfejsu API i programu PowerShell polecenia cmdlet mogą być używane tooconfigure zarówno Azure oparta na zasadach (statyczny) sieci VPN i opartej na trasach (dynamiczny) routingu sieci VPN.

### <a name="can-i-use-other-authentication-options"></a>Czy są dostępne inne opcje uwierzytelniania?

Możemy kluczy wstępnych toousing ograniczone (PSK) do uwierzytelniania.

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>Jak określić, którego ruch przechodzi przez bramy sieci VPN hello?

#### <a name="resource-manager-deployment-model"></a>Model wdrażania usługi Resource Manager

* Środowiska PowerShell: Użyj "Prefiks adresu" toospecify ruchu dla bramy sieci lokalnej hello.
* Portalu Azure: Przejdź bramy sieci lokalnej toohello > Konfiguracja > przestrzeni adresów.

#### <a name="classic-deployment-model"></a>Klasyczny model wdrażania

* Portalu Azure: toohello klasycznej sieci wirtualnej Przejdź > połączeń sieci VPN > połączenia sieci VPN typu lokacja lokacja > Nazwa lokacji lokalnej > lokalnej lokacji > przestrzeni adresowej klienta. 
* Klasyczny portal: Dodaj każdy zakres, który ma być wysłane za pośrednictwem bramy powitania dla sieci wirtualnej, na stronie sieci hello w sieci lokalnej. 

### <a name="can-i-configure-forced-tunneling"></a>Czy można skonfigurować wymuszone tunelowanie?

Tak. Zobacz artykuł [Configure forced tunneling](vpn-gateway-about-forced-tunneling.md) (Konfiguracja wymuszonego tunelowania).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>Można skonfigurować własny serwer sieci VPN w systemie Azure i używany w sieci lokalnej toomy tooconnect?

Tak, można wdrażać własne bramy sieci VPN lub serwerów na platformie Azure z hello Azure Marketplace lub tworzenie routery sieci VPN. Należy tooconfigure trasy zdefiniowane przez użytkownika w sieci wirtualnej tooensure ruch jest przekierowywany prawidłowo między sieci lokalnej i podsieci sieci wirtualnej.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>Dlaczego niektóre porty mojej bramy sieci VPN są otwarte?

Są one wymagane do komunikacji infrastruktury platformy Azure. Są one zabezpieczone (zablokowane) z użyciem certyfikatów Azure. Bez prawidłowego certyfikatów jednostek zewnętrznych, w tym klientom Witaj tych bramach nie będą mogli toocause żadnego wpływu na te punkty końcowe.

Bramy sieci VPN jest zasadniczo wieloadresowego urządzenia z jedną kartą Sieciową, wybierając w sieci prywatnej powitania klienta i jednej karty Sieciowej połączonej hello sieci publicznej. Jednostek infrastruktury platformy Azure nie naciśnij w sieciach prywatnych klienta ze względu na zgodność, więc potrzebują tooutilize publiczne punkty końcowe komunikacji infrastruktury. publiczne punkty końcowe Hello okresowo są skanowane przez inspekcji zabezpieczeń platformy Azure.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Więcej informacji na temat typów, wymagań i przepływności bram

Aby uzyskać więcej informacji, zobacz temat [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md) (Informacje o ustawieniach konfiguracji bramy VPN Gateway).

## <a name="s2s"></a>Połączenia typu lokacja-lokacja a urządzenia sieci VPN

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>Co należy wziąć pod uwagę przy wyborze urządzenia sieci VPN?

Zweryfikowaliśmy we współpracy z dostawcami urządzeń szereg standardowych urządzeń sieci VPN wykorzystywanych w ramach połączeń typu lokacja-lokacja. Lista znanych zgodne urządzenia sieci VPN, ich odpowiednie instrukcje konfiguracji lub przykładów i dane techniczne urządzeń można znaleźć w hello [urządzenia sieci VPN o](vpn-gateway-about-vpn-devices.md) artykułu. Wszystkie urządzenia z rodziny urządzeń hello wymienionym znany zgodny powinien współpracować z sieci wirtualnej. toohelp skonfigurować urządzenie sieci VPN, można znaleźć przykładowej konfiguracji urządzenia toohello lub łącze, które odpowiada tooappropriate rodziny urządzeń.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>Gdzie można znaleźć ustawienia konfiguracji urządzenia sieci VPN?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>Jak edytować przykłady konfiguracji urządzenia sieci VPN?

Aby uzyskać informacje na temat edytowania przykładów konfiguracji urządzeń, zobacz [Edytowanie przykładów](vpn-gateway-about-vpn-devices.md#editing).

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>Gdzie można znaleźć parametry protokołów IPsec i IKE?

Aby zapoznać się z parametrami protokołów IPsec/IKE, zobacz [Parametry](vpn-gateway-about-vpn-devices.md#ipsec).

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>Dlaczego mój oparty na zasadach tunel VPN przestaje działać, gdy ruch jest w stanie bezczynności?

Jest to oczekiwane zachowanie bram sieci VPN opartych na zasadach (znanych także jako bramy o routingu statycznym). Gdy hello ruchu za pośrednictwem tunelu hello jest w stanie bezczynności przez więcej niż 5 minut, będzie działo hello tunelu. Po uruchomieniu przepływu w żadnym kierunku ruchu tunelu hello będzie można ponownie ustanowić natychmiast.

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>Można użyć oprogramowania VPN tooconnect tooAzure?

W ramach konfiguracji typu lokacja-lokacja obejmującej wiele lokalizacji obsługiwane są serwery Windows Server 2012 usługi Routing i dostęp zdalny (RRAS).

Inne rozwiązania sieci VPN oprogramowania powinien współpracować z naszych bramy tak długo, jak są one zgodne tooindustry standardowe implementacje protokołu IPsec. Instrukcje dotyczące konfiguracji i pomocy technicznej, skontaktuj się z dostawcą hello hello oprogramowania.

## <a name="P2S"></a>Połączenia typu punkt-lokacja

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>Połączenia między sieciami wirtualnymi i połączenia obejmujące wiele lokacji

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>Można użyć ruchu tootransit bramy sieci VPN platformy Azure między Moje lokacjami lokalnymi lub tooanother sieci wirtualnej?

**Model wdrażania usługi Resource Manager**<br>
Tak. Zobacz hello [BGP](#bgp) sekcji, aby uzyskać więcej informacji.

**Klasyczny model wdrażania**<br>
Ruch przesyłania za pośrednictwem bramy sieci VPN platformy Azure przy użyciu hello klasycznego modelu wdrażania, ale zależy od przestrzeni adresowych statycznie zdefiniowanych w pliku konfiguracji sieci hello. Protokół BGP nie jest jeszcze obsługiwany z bram sieci wirtualnych Azure i sieci VPN przy użyciu hello klasycznego modelu wdrażania. Niezastosowanie protokołu BGP powoduje bardzo wysokie ryzyko błędów ręcznego definiowania przestrzeni adresowych przesyłania i nie jest zalecane.

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>Azure generuje hello tego samego protokołu IPsec/IKE wstępnego klucz dla moich połączeń sieci VPN dla hello sama sieć wirtualną?

Nie. Platforma Azure domyślnie generuje różne klucze wstępne dla różnych połączeń sieci VPN. Jednak możesz użyć hello ustawić VPN bramy klucz interfejsu API REST lub programu PowerShell polecenia cmdlet tooset hello klucza wartości preferowany. klucz Hello musi być alfanumerycznego ciągu o długości od 1 too128 znaków.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>Czy przy większej liczbie połączeń VPN typu lokacja-lokacja można uzyskać większą przepustowość niż przy pojedynczej sieci wirtualnej?

Nie, wszystkie tuneli VPN, sieci VPN typu punkt-lokacja, w tym udostępnianie hello tej samej sieci VPN platformy Azure, bramy i hello dostępną przepustowość.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>Czy można skonfigurować wiele tuneli między siecią wirtualną i lokalną lokacją z użyciem sieci VPN obejmującej wiele lokacji?

Tak, ale należy skonfigurować protokołu BGP na obu toohello tuneli tej samej lokalizacji.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>Czy można używać sieci VPN typu punkt-lokacja z siecią wirtualną z wieloma tunelami VPN?

Tak, sieci VPN typu punkt-lokacja (P2S) może służyć z bramy sieci VPN hello łączenia toomultiple lokacjami lokalnymi i innych sieci wirtualnych.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>Z protokołu IPsec, VPN toomy obwodu ExpressRoute można połączyć sieć wirtualną?

Tak, takie rozwiązanie jest obsługiwane. Aby uzyskać więcej informacji, zobacz artykuł [Configure ExpressRoute and Site-to-Site VPN connections that coexist](../expressroute/expressroute-howto-coexist-classic.md) (Konfigurowanie obwodu ExpressRoute i współistniejących połączeń sieci VPN typu lokacja-lokacja).

## <a name="ipsecike"></a>Zasady protokołu IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>Połączenia obejmujące wiele lokalizacji a maszyny wirtualne

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>Jak należy łączyć toohello wirtualna Moja maszyna wirtualna znajduje się w sieci wirtualnej, I mieć połączenie między lokalizacjami?

Jest kilka możliwości. Jeśli masz protokołu RDP dla maszyny Wirtualnej włączone, można połączyć maszyny wirtualnej tooyour przy użyciu hello prywatnego adresu IP. W takim przypadku należy określić hello prywatnego adresu IP i port hello, które mają tooconnect zbyt (zazwyczaj 3389). Należy tooconfigure hello portu na maszynie wirtualnej hello ruchu.

Można także połączyć tooyour maszyny wirtualnej prywatnego adresu IP z innej maszyny wirtualnej, która ma znajdujących się na powitania takie same sieci wirtualnej. Nie można wykonać maszyny wirtualnej tooyour RDP za pomocą hello prywatnego adresu IP, jeśli łączysz się z lokalizacji spoza sieci wirtualnej. Na przykład jeśli masz punkt-lokacja sieci wirtualnej, skonfigurowane i nie można ustanowić połączenia z komputera, nie można połączyć toohello maszyny wirtualnej za pomocą prywatnego adresu IP.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>Moja maszyna wirtualna jest w łączności między lokalizacjami z sieci wirtualnej, cały ruch hello z maszyną Wirtualną z systemem przejść przez to połączenie?

Nie. Tylko ruch hello miejsce docelowe przejdzie IP zawarte w hello wirtualnej sieci lokalnej sieci zakresów adresów IP określonego przez bramę sieci wirtualnej hello. Ruch ma docelowego, który znajduje się w sieci wirtualnej hello IP pozostaje w ramach sieci wirtualnej hello. Ruch jest wysyłanych za pośrednictwem sieci publicznych toohello usługi równoważenia obciążenia hello, lub jeśli wymuszanie tunelowania jest używany, wysyłane za pośrednictwem bramy sieci VPN platformy Azure hello.

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>Jak rozwiązywać tooa połączenia RDP maszyny Wirtualnej

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Sieć wirtualna — często zadawane pytania

Możesz wyświetlić informacje dodatkowe sieci wirtualnej w hello [często zadawane pytania dotyczące sieci wirtualnych](../virtual-network/virtual-networks-faq.md).

## <a name="next-steps"></a>Następne kroki

* Więcej informacji o usłudze VPN Gateway można znaleźć w artykule [VPN Gateway — informacje](vpn-gateway-about-vpngateways.md).
* Aby uzyskać więcej informacji o ustawieniach konfiguracji bramy VPN Gateway, zobacz temat [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md) (Informacje o ustawieniach konfiguracji bramy VPN Gateway).
