---
title: Zabezpieczenia sieci aaaAzure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat przetwarzania danych usług w chmurze zawierających szeroką gamę wystąpienia obliczeniowe i usług, które można skalować w górę i w dół automatycznie toomeet hello potrzeb aplikacji lub przedsiębiorstwa."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: TomSh
ms.openlocfilehash: 7dae83bbe338a2727575447583a7fb773527dd59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security"></a>Zabezpieczenia sieci platformy Azure

Wiemy, że zabezpieczeń jest jednego zadania w chmurze hello i jak ważne jest aby znaleźć dokładne i aktualne informacje na temat zabezpieczeń platformy Azure. Jednym z hello najlepsze toouse powodów Azure dla usług i aplikacji jest tootake korzystać z platformy Azure szerokiej gamy narzędzi zabezpieczeń i możliwości. Te narzędzia i funkcje dzięki możliwości toocreate bezpiecznych rozwiązań na powitania platformy Azure.

Microsoft Azure udostępnia poufność, integralność i dostępność danych klienta, jednoczesnym accountability przezroczysty. toohelp lepiej zrozumieć hello kolekcja formantów zabezpieczeń sieci zaimplementowana w systemie Microsoft Azure z punktu widzenia powitania klienta, w tym artykule "Zabezpieczenia sieciowe Azure", są zapisywane tooprovide kompleksowe przyjrzeć się hello zabezpieczeń sieci Formanty dostępne w systemie Microsoft Azure.

Ten dokument jest przeznaczony się, że tooinform o hello szeroką gamę sieci określa, które można skonfigurować zabezpieczenia hello tooenhance hello rozwiązań, które można wdrożyć na platformie Azure. Jeśli interesuje Cię w jakie firma Microsoft toosecure hello sieci szkieletowej z hello samą platformą Azure, zobacz sekcję zabezpieczeń platformy Azure hello w hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/azure-security).

## <a name="azure-platform"></a>Platforma Azure

Azure to platforma usługi chmury publicznej, która obsługuje szeroki wybór systemów operacyjnych, programowania języków, struktury, narzędzia, baz danych i urządzeń.  Kontenery systemu Linux można uruchamiać z integracją rozwiązania Docker; Tworzenie aplikacji za pomocą języka JavaScript, Python, .NET, PHP, Java i Node.js; Kompilacja zapleczy dla systemu iOS, Android i Windows urządzeń. Usługi w chmurze Azure obsługuje hello już polegać na tej samej technologii miliony deweloperów i specjalistów IT i zaufania.

Podczas tworzenia lub migracji zasobów informatycznych do dostawcy usług w chmurze publicznej, są zależne tooprotect możliwości organizacji w aplikacji i danych za pomocą hello kontroli usług i hello zapewniają toomanage hello bezpieczeństwa sieci opartej na chmurze zasoby.

Zaprojektowano infrastruktury platformy Azure z tooapplications zakładzie hello jednocześnie hostingu miliony klientów i zapewnia foundation godne zaufania, na którym firmy mogą spełnić ich wymagań dotyczących zabezpieczeń. Ponadto Azure zapewnia obszernej kolekcji zabezpieczeń można skonfigurować opcje i hello toocontrol możliwości ich, dzięki czemu można dostosować toomeet hello unikatowe wymagania dotyczące zabezpieczeń wdrożenia w organizacji.

## <a name="abstract"></a>Abstrakcyjny

Usługi w chmurze publicznej Microsoft świadczenia usług hiperskali i infrastruktury, funkcje klasy korporacyjnej oraz wiele opcji na potrzeby łączności hybrydowej. Można wybrać tooaccess tych usług za pośrednictwem Internetu hello lub z usługi Azure ExpressRoute, który zapewnia łączność w sieci prywatnej. Platforma Microsoft Azure Hello umożliwia tooseamlessly rozszerzają infrastruktury do chmury hello i tworzenia wielu architektur. Ponadto stron trzecich można włączyć udoskonalone funkcje oferty usług zabezpieczeń oraz urządzenia wirtualnego.

Usługi sieciowe systemu Azure zwiększenie elastyczności, dostępności, odporności, bezpieczeństwa i integralności zgodnie z projektem. Ten dokument zawiera szczegółowe informacje na temat funkcji sieciowych hello Azure i informacji na temat użycia toohelp funkcji natywnego zabezpieczeń platformy Azure klienci ochrony swoimi zasobami informacyjnymi.

Witaj przeznaczony wlicza się odbiorcy na tym dokumencie:

- Menedżerowie technicznych, Administratorzy sieci i deweloperów, którzy szukają rozwiązań zabezpieczeń dostępny i obsługiwany na platformie Azure.

-   MSP lub business procesu dyrektorzy, którzy mają tooget ogólne omówienie hello Azure technologie sieciowe i usług, które mają zastosowanie w dyskusjach ze specjalistami wokół zabezpieczeń sieci w chmurze publicznej Azure hello.

## <a name="azure-networking-big-picture"></a>Azure networking duży obraz
Microsoft Azure obejmuje niezawodne toosupport infrastruktury sieci, aplikacji i wymaganiami dotyczącymi łączności usługi. Łączność sieciowa będzie możliwe między zasobami znajdującymi się na platformie Azure, między lokalnymi i Azure hostowanej zasobów oraz tooand z hello Internet i Azure.

![Azure Networking duży obraz](media/azure-network-security/azure-network-security-fig-1.png)

Witaj [infrastruktury sieci platformy Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) umożliwia toosecurely możesz Uzyskuj dostęp do zasobów platformy Azure tooeach innych sieci wirtualnych (sieci wirtualne). Sieci wirtualnej jest reprezentację sieci w chmurze hello. Sieci wirtualnej jest logiczną izolacją hello chmury Azure w wersji dedykowanej sieci tooyour subskrypcji. Możesz połączyć sieci lokalnej tooyour sieci wirtualnych.

Obsługuje platformy Azure w wersji dedykowanej sieci lokalnej tooyour łączności łącza sieci WAN i sieci wirtualnej platformy Azure z [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Powiązanie Hello Azure i witryny sieci Web używa dedykowanego połączenia nie przechodzi przez hello publicznej sieci Internet. Jeśli aplikacja Azure jest uruchomiona w wielu centrach danych, możesz użyć [usługi Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute żądania od użytkowników inteligentnie między wystąpieniami aplikacji hello. Można również przekierować tooservices ruchu nie działa na platformie Azure, jeśli są one dostępne z hello Internet.

## <a name="enterprise-view-of-azure-networking-components"></a>Widok Enterprise Azure składników sieciowych
Platforma Azure ma wiele sieci składników, które są odpowiednie toonetwork dyskusji zabezpieczeń. opisano te składniki sieci i skoncentrować się na powitania zabezpieczeń wystawia toothem powiązane.

> [!Note]
> Nie wszystkie aspekty sieci platformy Azure są opisane — omówiono tylko te toobe kluczową w planowaniu i projektowaniu bezpiecznej infrastruktury sieciowej wokół usług i aplikacji, które wdrażasz na platformie Azure.

W tym dokumencie będzie można hello okładce następujących Azure networking możliwości przedsiębiorstwa:

-   Podstawowe połączenie sieciowe

-   Połączenia hybrydowe

-   Środki zabezpieczające.

-   Sprawdzanie poprawności sieci

### <a name="basic-network-connectivity"></a>Podstawowe połączenie sieciowe

Witaj [sieci wirtualnej Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) umożliwia usługi można toosecurely Uzyskuj dostęp do zasobów platformy Azure tooeach innych sieci wirtualnych (VNet). Sieci wirtualnej jest reprezentację sieci w chmurze hello. Sieci wirtualnej jest logiczną izolacją hello sieć platformy Azure w wersji dedykowanej infrastruktury tooyour subskrypcji. Możesz również połączyć sieci wirtualnych tooeach innych i sieciami przy użyciu sieci VPN typu lokacja lokacja lokalnymi i w wersji dedykowanej tooyour [łącza sieci WAN](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

![Podstawowe połączenie sieciowe](media/azure-network-security/azure-network-security-fig-2.png)

Hello opis użyć serwerów toohost maszyn wirtualnych na platformie Azure hello pytanie jest sposób łączenia sieci tooa w tych maszyn wirtualnych. Witaj odpowiedzi jest czy maszyny wirtualne połączyć tooan [sieci wirtualnej Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

Sieci wirtualnych platformy Azure są takie jak hello wirtualnych sieci można użyć lokalnego z własnych rozwiązań platformy wirtualizacji, takich jak Microsoft Hyper-V lub VMware.

#### <a name="intra-vnet-connectivity"></a>Łączność sieci wirtualnej wewnątrz

Możesz połączyć sieci wirtualnych tooeach innych, włączanie zasoby połączone toocommunicate sieci wirtualnej tooeither ze sobą za pośrednictwem sieci wirtualnych. Można użyć jednego lub obu hello następujące opcje tooconnect sieci wirtualnych tooeach inne:

- **Komunikacja równorzędna:** umożliwia zasoby podłączone toodifferent sieci wirtualnych platformy Azure w ramach hello tej samej lokalizacji platformy Azure toocommunicate ze sobą. Witaj przepustowości i opóźnień między hello sieci wirtualnej jest hello sam tak, jakby zasoby hello był połączony toohello tej samej sieci wirtualnej. Przeczytaj toolearn więcej informacji na temat komunikacji równorzędnej, [równorzędna sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

 ![Komunikacja równorzędna](media/azure-network-security/azure-network-security-fig-3.png)

- **Połączenia do wirtualnymi:** umożliwia zasoby podłączone toodifferent sieci wirtualnej platformy Azure w ramach hello tej samej lub innej lokalizacji platformy Azure. W przeciwieństwie do komunikacji równorzędnej, przepustowości jest ograniczona między sieciami wirtualnymi, ponieważ ruch musi przepływać przez bramę sieci VPN platformy Azure.

![Połączenia do wirtualnymi](media/azure-network-security/azure-network-security-fig-4.png)


więcej informacji na temat łączenia sieci wirtualnych z połączeniem wirtualnymi do odczytu hello toolearn [skonfigurować artykułu połączenia do wirtualnymi](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json).

#### <a name="azure-virtual-network-capabilities"></a>Funkcje sieci wirtualnej platformy Azure:

Jak widać, sieci wirtualnej platformy Azure udostępnia maszyny wirtualne tooconnect toohello sieci, aby umożliwić im połączenie tooother zasobów sieciowych w sposób bezpieczny. Jednak podstawowej łączności jest po prostu hello początku. Hello następujące możliwości usługi Azure Virtual Network hello ujawnić właściwości zabezpieczeń hello sieci wirtualnej platformy Azure:

-   Izolacja

-   Łączność z Internetem

-   Łączność zasobów platformy Azure

-   Łączność sieci wirtualnej

-   Łączność lokalna

-   Filtrowanie ruchu

-   Routing

**Izolacji**

Sieci wirtualne są [izolowanego](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) od siebie nawzajem. Można utworzyć oddzielne sieci wirtualnych do tworzenia, testowania i produkcji, użyj hello takie same [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) bloki adresów. Z drugiej strony możesz utworzyć wiele sieci wirtualnych, użyj innego bloków adresów CIDR i połączyć ze sobą sieci. Sieć wirtualną można podzielić na wiele podsieci.

Platforma Azure udostępnia rozpoznawania nazw wewnętrznych dla maszyn wirtualnych i [usługi w chmurze](https://azure.microsoft.com/services/cloud-services/) wystąpień roli połączone tooa sieci wirtualnej. Opcjonalnie można skonfigurować toouse sieci wirtualnej własne serwery DNS, zamiast rozpoznawania nazw wewnętrznych platformy Azure.

Można zaimplementować wiele sieci wirtualnych w każdym Azure [subskrypcji](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json) i Azure [region](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology?toc=%2fazure%2fvirtual-network%2ftoc.json). Każda sieć wirtualna jest odizolowana od innych sieci wirtualnych. Dla każdej sieci wirtualnej można:

-   Określ niestandardowe prywatnych przestrzeni adresów IP przy użyciu prywatnych i publicznych adresów (RFC 1918). Azure przypisuje toohello połączonych zasobów sieci wirtualnej prywatnego adresu IP z hello przestrzeni adresowej, możesz przypisać.

-   Segment hello sieci wirtualnej do co najmniej jednej podsieci i przydzielić część hello sieci wirtualnej adres miejsca tooeach podsieci.

-   Korzystanie z rozpoznawania nazw platformy Azure lub Podaj własny serwer DNS do użytku przez zasoby podłączone tooa sieci wirtualnej. więcej informacji na temat rozpoznawania nazw w sieci wirtualnych, przeczytaj hello toolearn [rozpoznawanie nazw dla maszyn wirtualnych i usług w chmurze](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

**Łączność z Internetem**

Wszystkie [Azure maszyn wirtualnych (VM)](https://docs.microsoft.com/azure/virtual-machines/windows/) i toohello Internet, domyślnie dostęp do wystąpień roli usługi w chmurze ma tooa połączonych sieci wirtualnej. Można również włączyć dostęp do przychodzących toospecific zasobów, zgodnie z potrzebami. (VM) i toohello Internet, domyślnie dostęp do wystąpień roli usługi w chmurze ma tooa połączonych sieci wirtualnej. Można również włączyć dostęp do przychodzących toospecific zasobów, zgodnie z potrzebami.

Wszystkie zasoby tooa połączonych sieci wirtualnej mają łączność wychodząca toohello Internet domyślnie. Witaj prywatnego adresu IP zasobu hello jest adres sieciowy źródła przetłumaczyła publicznego adresu IP (SNAT) tooa hello infrastruktury platformy Azure. Możesz zmienić hello domyślne łączności dzięki implementacji niestandardowego routingu i filtrowanie ruchu. więcej informacji na temat wychodzące połączenie z Internetem, przeczytaj hello toolearn [Opis połączeń wychodzących na platformie Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-outbound-connections?toc=%2fazure%2fvirtual-network%2ftoc.json).

toocommunicate ruchu przychodzącego tooAzure zasobów z hello Internet lub toocommunicate toohello wychodzących, Internet bez SNAT, zasobu można przypisać do publicznego adresu IP. więcej informacji na temat publiczne adresy IP, przeczytaj hello toolearn [publicznego adresu IP, adresy](https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address).

**Łączność zasobów platformy Azure**

[Zasoby platformy Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) takie jak usługi w chmurze i maszyn wirtualnych może być połączone toohello tej samej sieci wirtualnej. Witaj zasobów mogą się łączyć tooeach innych używania prywatnych adresów IP, nawet jeśli znajdują się w różnych podsieciach. Platforma Azure udostępnia domyślny routing między podsieciami, sieci wirtualnych i sieci lokalnej, dlatego nie masz tooconfigure i Zarządzaj trasami.

Możesz połączyć kilka tooa zasobów Azure sieci wirtualnej, takie jak maszyn wirtualnych (VM), usługi w chmurze środowiska usługi App Service i zestawy skalowania maszyny wirtualnej. Maszyny wirtualne połączyć tooa podsieci w sieci wirtualnej za pośrednictwem interfejsu sieciowego (NIC). więcej informacji na temat kart sieciowych, przeczytaj hello toolearn [interfejsy sieciowe](https://docs.microsoft.com/azure/virtual-network/virtual-network-network-interface).

**Łączność sieci wirtualnej**

[Sieci wirtualne](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) może być połączone tooeach innych, włączanie zasoby podłączone tooany toocommunicate sieci wirtualnej z dowolnego zasobu w innych sieci wirtualnej.

Możesz połączyć sieci wirtualnych tooeach innych, włączanie zasoby połączone toocommunicate sieci wirtualnej tooeither ze sobą za pośrednictwem sieci wirtualnych. Można użyć jednego lub obu hello następujące opcje tooconnect sieci wirtualnych tooeach inne:

- **Komunikacja równorzędna:** umożliwia zasoby podłączone toodifferent sieci wirtualnych platformy Azure w ramach hello tej samej lokalizacji platformy Azure toocommunicate ze sobą. Witaj przepustowości i opóźnień między hello sieci wirtualnych jest hello jak w przypadku, gdy zasoby hello były połączone toohello tego samego VNet.toolearn więcej informacji na temat komunikacji równorzędnej, odczytu hello [równorzędna sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

- **Połączenia do wirtualnymi:** umożliwia zasoby podłączone toodifferent sieci wirtualnej platformy Azure w ramach hello tej samej lub innej lokalizacji platformy Azure. W przeciwieństwie do komunikacji równorzędnej, przepustowości jest ograniczona między sieciami wirtualnymi, ponieważ ruch musi przepływać przez bramę sieci VPN platformy Azure. więcej informacji na temat łączenia sieci wirtualnych z połączeniem do wirtualnymi toolearn. toolearn, przeczytaj hello [skonfigurować połączenia do wirtualnymi](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal?toc=%2fazure%2fvirtual-network%2ftoc.json) .

**Łączność lokalna**

Sieci wirtualne, które mogą być połączone za[lokalnymi](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) sieci za pośrednictwem sieci prywatnej połączeń między siecią a Azure lub za pośrednictwem połączenia sieci VPN lokacja lokacja za pośrednictwem hello Internet.

Można połączyć z tooa sieci lokalnej sieci wirtualnej przy użyciu dowolnej kombinacji hello następujące opcje:

- **Punkt lokacja wirtualnej sieci prywatnej (VPN):** między jednej sieci połączonych tooyour PC i hello sieci wirtualnej. Tego typu połączenia jest doskonałym, jeśli tylko rozpoczniesz pracę z platformą Azure, lub dla deweloperów, ponieważ wymaga żadnych zmian tooyour istniejącej sieci. Hello połączenie korzysta z komunikacji tooprovide szyfrowane protokół SSTP hello za pośrednictwem hello Internet między hello PC i hello sieci wirtualnej. Opóźnienie Hello VPN punkt lokacja jest nieprzewidywalne, ponieważ hello ruch przechodzi hello Internet.

- **Sieć VPN lokacja lokacja:** między urządzenie sieci VPN i bramy sieci VPN platformy Azure. Ten typ połączenia pozwala dowolnego zasobu lokalnego autoryzować tooaccess sieci wirtualnej. połączenie Hello jest VPN IPsec i IKE, zapewniająca szyfrowaną komunikację za pośrednictwem hello Internet między urządzeniami lokalnymi i hello bramy sieci VPN platformy Azure. Opóźnienie Hello połączenia lokacja lokacja jest nieprzewidywalne, ponieważ hello ruch przechodzi hello Internet.

- **Usługa Azure ExpressRoute:** ustanowić między siecią a Azure, za pośrednictwem partner usługi ExpressRoute. To połączenie jest prywatne. Ruch omija hello Internet. Hello opóźnienie połączenia ExpressRoute jest przewidywalne, ponieważ ruch nie przechodzenia hello Internet. więcej informacji na temat wszystkich hello poprzedniej opcji połączenia, przeczytaj hello toolearn [Diagram topologii połączenia](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

**Filtrowanie ruchu**

Wystąpienia roli maszyny Wirtualnej i usługi w chmurze [ruch sieciowy](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) można użyć do filtrowania ruchu przychodzącego i wychodzącego przez źródłowy adres IP i port docelowy adres IP i portu i protokołu.

Można filtrować ruch sieciowy między podsieciami przy użyciu jednego lub obu hello następujące opcje:

- **Sieciowe grupy zabezpieczeń (NSG):** każda grupa NSG może zawierać wiele reguł zabezpieczeń dla ruchu przychodzącego i wychodzącego umożliwiających toofilter ruch źródłowy i docelowy adres IP, portu i protokołu. Można stosować grupy NSG tooeach karty Sieciowej na maszynie wirtualnej. Można także zastosować grupy NSG podsieci toohello karty Sieciowej, lub innych zasobów platformy Azure jest połączona. więcej informacji na temat grup NSG, przeczytaj hello toolearn [sieciowej grupy zabezpieczeń](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

- **Wirtualnych urządzeń sieciowych:** urządzenie sieci wirtualnej jest uruchomione oprogramowanie, które wykonuje funkcję sieci, takie jak Zapora maszyny Wirtualnej. Wyświetl listę dostępnych NVAs w hello Azure Marketplace. NVAs są również dostępne, które zapewniają funkcje ruchu Optymalizacja sieci WAN i innych sieci. NVAs zwykle są używane przez użytkownika lub trasy protokołu BGP. Można również użyć ruchu toofilter NVA między sieciami wirtualnymi.

**Routing**

Opcjonalnie można zastąpić domyślne Azure routingu, konfigurowanie własnego trasy lub użyj trasy protokołu BGP za pośrednictwem bramy sieci.

Platforma Azure tworzy tabele tras, umożliwiających podsieci tooany połączonych zasobów w dowolnej sieci wirtualnej toocommunicate ze sobą, domyślnie. Można zaimplementować jedną lub obie następujące opcje toooverride hello hello trasy domyślne, które tworzy Azure:

- **Trasy zdefiniowane przez użytkownika:** tworzenia tabel tras niestandardowych trasy, które kontrolują, których ruch jest kierowany toofor każdej podsieci. więcej informacji na temat trasy zdefiniowane przez użytkownika, odczytać hello toolearn [trasy zdefiniowane przez użytkownika](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview).

- **Trasy protokołu BGP:** Jeśli połączyć sieci wirtualnej sieci lokalnej tooyour przy użyciu połączenia bramy sieci VPN platformy Azure lub usługi ExpressRoute, można propagować tooyour trasy protokołu BGP sieci wirtualnych.

### <a name="hybrid-internet-connectivity-connect-tooan-on-premises-network"></a>Połączenie z Internetem hybrydowego: połączyć sieć lokalną tooan
Można połączyć z tooa sieci lokalnej sieci wirtualnej przy użyciu dowolnej kombinacji hello następujące opcje:

-   Łączność z Internetem

-   Sieć VPN punkt lokacja (P2S sieci VPN)

-   Sieci VPN typu lokacja lokacja (S2S sieci VPN)

-   ExpressRoute

#### <a name="internet-connectivity"></a>Połączenie z Internetem

Zgodnie z sugestią, jego nazwa, łączności z Internetem może ułatwić obciążeń z hello Internet, konfigurując można ujawnić tooworkloads różnych publiczne punkty końcowe, przebywających w sieci wirtualnej hello. Te obciążenia mogą zostać ujawnione przy użyciu [modułu równoważenia obciążenia internetowy](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview) lub po prostu przypisywane publicznego adresu IP adresie toohello maszyny Wirtualnej. W ten sposób staje się możliwe na cokolwiek na powitania Internet toobe stanie tooreach maszyny wirtualnej, pod warunkiem zaporę hosta [sieciowej grupy zabezpieczeń (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg), i [trasy zdefiniowane przez użytkownika](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) pozwala toohappen.

W tym scenariuszu można ujawnić aplikacji, która potrzebuje toobe toohello publiczny Internet i być tooit tooconnect może z dowolnego miejsca lub z określonych lokalizacji w zależności od konfiguracji hello obciążeń.

#### <a name="point-to-site-vpn-or-site-to-site-vpn"></a>Sieć VPN punkt lokacja lub sieci VPN typu lokacja lokacja
Te dwie powróci do hello tej samej kategorii. Potrzebuje Twojej sieci wirtualnej toohave bramy sieci VPN i można się połączyć przy użyciu klienta sieci VPN dla stacji roboczej, jako część hello tooit [punkt-lokacja konfiguracji](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) lub skonfigurować lokalną [urządzenia sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) toobe tooterminate stanie VPN lokacja lokacja. W ten sposób urządzeń lokalnych, można połączyć tooresources w hello sieci wirtualnej.

Konfiguracja punkt-lokacja (P2S) umożliwia tworzenie bezpiecznego połączenia z tooa komputera klienta dla sieci wirtualnej. Połączenie punkt-lokacja (P2S) to połączenie sieci VPN nawiązywane za pośrednictwem protokołu SSTP (Secure Socket Tunneling Protocol).

![Sieć VPN punkt lokacja](media/azure-network-security/azure-network-security-fig-5.png)

Połączenia punkt-lokacja są przydatne w tooyour tooconnect sieci wirtualnej z lokalizacji zdalnej, takich jak z domu lub Centrum konferencji, lub jeśli masz tylko kilku klientów, którzy potrzebują tooconnect tooa wirtualnej sieci.

Połączenia typu punkt-lokacja nie wymagają do prawidłowego działania urządzenia sieci VPN ani publicznego adresu IP. Należy ustanowić połączenie VPN hello z komputera klienckiego hello. W związku z tym P2S nie jest zalecane tooAzure tooconnect sposób, w razie potrzeby trwałe połączenie z wielu urządzeń lokalnych i komputerach tooyour sieć platformy Azure.

![Sieci VPN typu lokacja lokacja](media/azure-network-security/azure-network-security-fig-6.png)

> [!Note]
> Aby uzyskać więcej informacji na temat połączenia punkt-lokacja, zobacz hello [punkt-lokacja FA v Q](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-classic-azure-portal).

Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2).

Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP. To połączenie ma miejsce ponad hello Internet i pozwala zbyt "tunelowe" informacji wewnątrz zaszyfrowanych łącza między siecią a Azure. Sieci VPN typu lokacja lokacja jest bezpieczne, dojrzała technologia, która jest wdrażany w przedsiębiorstwach wszystkich rozmiarów dekad. Tunel szyfrowanie odbywa się przy użyciu [trybu tunelowania IPsec](https://technet.microsoft.com/library/cc786385.aspx).

Podczas sieci VPN typu lokacja lokacja jest technologią zaufanych, niezawodny i ustalonych ruchu w tunelu hello przechodzenia hello Internet. Ponadto przepustowość jest stosunkowo ograniczonego tooa maksymalnie około 200 MB/s.

Jeśli potrzebujesz wyjątkowych poziom bezpieczeństwa i wydajności dla połączeń między różnymi lokalizacjami, zalecane jest użycie Azure ExpressRoute dla łączność między lokalizacjami. ExpressRoute jest dedykowanych sieci WAN łącza między Twojej lokalizacji lokalnej lub dostawcy usług hosta programu Exchange. Ponieważ jest to połączenie telco, dane nie są przesyłane za pośrednictwem Internetu hello i dlatego nie narażonych toohello potencjalne ryzyko związane z komunikacją internetową.

> [!Note]
> Aby uzyskać więcej informacji na temat bram sieci VPN, zobacz [bramy sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).

#### <a name="dedicated-wan-link"></a>Dedykowane łącza sieci WAN
Microsoft Azure ExpressRoute umożliwia rozszerzenie sieci lokalnej do hello Azure za pośrednictwem dedykowanego połączenia prywatne w ramach dostawcy łączności.

Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet. Dzięki toooffer połączeń ExpressRoute więcej niezawodności, szybkości szybsze niższe opóźnienia i lepsze zabezpieczenia niż typowe połączenia za pośrednictwem Internetu hello.

![ Dedykowane łącza sieci WAN](media/azure-network-security/azure-network-security-fig-7.png)

> [!Note]
> Aby uzyskać informacje na temat tooconnect Twojego tooMicrosoft sieci przy użyciu usługi ExpressRoute, zobacz [modeli połączenie ExpressRoute](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) i [opis techniczny ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

Jako z opcjami sieci VPN typu lokacja lokacja hello, ExpressRoute umożliwia także tooresources tooconnect, które nie są zawsze tylko jedna sieć wirtualną. W rzeczywistości w zależności od hello jednostka SKU, możesz połączyć too10 sieci wirtualnych. Jeśli masz hello [dodatek premium](https://docs.microsoft.com/azure/expressroute/expressroute-faqs), tooup połączeń too100 sieci wirtualne są możliwe, w zależności od przepustowości. więcej informacji na temat tych typów połączeń wygląd jak, przeczytaj toolearn [Diagram topologii połączenia](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%2fazure%2fvirtual-network%2ftoc.json).

### <a name="security-controls"></a>Środki zabezpieczające.
Sieci wirtualnej platformy Azure zapewnia bezpieczny, logiczną sieci, która jest odizolowana od innych sieci wirtualnych i obsługuje wiele kontroli bezpieczeństwa, używanych w sieci lokalnej. Klientom tworzenie własnych struktury przy użyciu: podsieci — ich użycia własnych zakresu prywatnych adresów IP, skonfigurować tabele tras, sieciowej grupy zabezpieczeń, kontroli dostępu do listy (kontroli dostępu ACL), bramy i wirtualnych urządzeń toorun ich obciążeń w chmurze hello.

Oto Hello kontroli bezpieczeństwa, używanych w sieci wirtualnej platformy Azure:

-   Kontrolę dostępu do sieci

-   Trasy zdefiniowane przez użytkownika

-   Urządzenie zabezpieczeń sieci

-   Application Gateway

-   Zapora aplikacji sieci Web platformy Azure

-   Kontrola dostępność sieci

#### <a name="network-access-controls"></a>Kontrolę dostępu do sieci
Witaj hello Azure Virtual Network (VNet) jest podstawą hello Azure model sieci i udostępnia izolacji i ochrony, [grup zabezpieczeń sieci (NSG)](https://blogs.msdn.microsoft.com/igorpag/2016/05/14/azure-network-security-groups-nsg-best-practices-and-lessons-learned/) są podstawowym narzędziem hello Użyj tooenforce i kontrola ruchu sieciowego zasady na poziomie sieci hello.

![ Kontrolę dostępu do sieci](media/azure-network-security/azure-network-security-fig-8.png)


Można kontrolować dostęp przez zezwalanie na dostęp lub odmawianie komunikacji między hello obciążeń w ramach sieci wirtualnej, od systemów w sieci klienta za pośrednictwem łączności między lokalizacjami lub bezpośrednia komunikacja z Internetem.

Na diagramie hello zarówno sieci wirtualnych, jak i grupy NSG znajdują się w określonej warstwie hello Azure ogólne bezpieczeństwo stosu, gdzie grup NSG, przez i wirtualnych urządzeń sieciowych może być używane toocreate zabezpieczeń granice tooprotect hello wdrożenia aplikacji w sieci hello chronione.

Grupy NSG ruch tooevaluate 5 parametrów (i są używane w regułach hello, które można skonfigurować dla hello NSG):

-   [Źródłowy i docelowy adres IP](https://support.microsoft.com/help/969029/the-functionality-for-source-ip-address-selection-in-windows-server-2008-and-in-windows-vista-differs-from-the-corresponding-functionality-in-earlier-versions-of-windows)

-   [Port źródłowy i docelowy](https://technet.microsoft.com/library/dd197515)

-   Protokół: [Transmission Control Protocol (TCP)](https://technet.microsoft.com/library/cc940037.aspx) lub [User Datagram Protocol (UDP)](https://technet.microsoft.com/library/cc940034.aspx)

Oznacza to, że można kontrolować dostęp do zakresu od jednej maszyny Wirtualnej do grupy maszyn wirtualnych lub pojedynczy tooanother maszyny Wirtualnej z jednym maszyny Wirtualnej, lub między całej podsieci. Ponownie należy pamiętać, że jest to prosty pakietów filtrowania, pakietów nie pełnej kontroli. Brak weryfikacji protokołu lub identyfikatorów poziomu sieci i możliwości adresów IP należących do grupy zabezpieczeń sieci.

Grupa NSG zawiera kilka wbudowanych zasad, które należy zwrócić uwagę. Są to:

-   **Zezwolić na cały ruch w sieci wirtualnej określonej:** wszystkich maszyn wirtualnych na powitania tej samej sieci wirtualnej platformy Azure mogą komunikować się ze sobą.

-   **Zezwalaj na tooinbound równoważenia obciążenia Azure:** ta reguła zezwala na ruch z dowolnego adresu docelowego tooany adresu źródłowego dla modułu równoważenia obciążenia Azure hello.

-   **Odmów wszystkich przychodzących:** ta reguła blokuje cały ruch źródłem hello internetowych, które zostały jawnie dozwolone.

-   **Zezwalaj na wszystkie ruchu wychodzącego toohello Internet:** ta zasada umożliwia maszyn wirtualnych tooinitiate połączeń toohello Internet. Jeśli nie chcesz, aby te połączenia zainicjowane, należy toocreate tooblock reguły tych połączeń lub wymuszanie tunelowania wymuszonego.

#### <a name="system-routes-and-user-defined-routes"></a>Trasy systemowe i trasy zdefiniowane przez użytkownika

Po dodaniu maszynach wirtualnych (VM) tooa sieć wirtualną (VNet) na platformie Azure można zauważyć, maszyn wirtualnych hello automatycznie są możliwe toocommunicate ze sobą za pośrednictwem sieci hello. Nie trzeba toospecify bramy, nawet jeśli hello maszyn wirtualnych znajdują się w różnych podsieciach.

Witaj dotyczy to także komunikacji z toohello maszyn wirtualnych hello publicznego Internetu i sieci lokalnej tooyour nawet gdy połączenie hybrydowe z platformy Azure tooyour własnych centrum danych jest obecny.

![Trasy systemowe](media/azure-network-security/azure-network-security-fig-9.png)

Taki przepływ komunikacji jest możliwa, ponieważ Azure korzysta z szeregu toodefine trasy systemu sposób przepływu ruchu w sieci IP. Trasy systemowe sterują przepływem hello komunikacji hello następujące scenariusze:

-   Z poziomu hello tej samej podsieci.

-   Z tooanother podsieci w sieci wirtualnej.

-   Z maszyn wirtualnych toohello Internet.

-   Z sieci wirtualnej tooanother sieci wirtualnej za pośrednictwem bramy sieci VPN.

-   Z sieci wirtualnej tooanother sieci wirtualnej za pośrednictwem sieci wirtualnej komunikacji równorzędnej ([usługi łańcucha](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview)).

-   Z sieci wirtualnej sieci lokalnej tooyour za pośrednictwem bramy sieci VPN.

W wielu przedsiębiorstwach istnieją ograniczeniami zabezpieczeń i wymagania dotyczące zgodności, które wymagają lokalnych kontroli wszystkich tooenforce pakietów sieciowych określonego zasady. Platforma Azure udostępnia mechanizm o nazwie [wymuszone tunelowanie](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-forced-tunneling) który przekierowuje ruch z hello tooon lokalnych maszyn wirtualnych, tworząc niestandardowe trasy lub [protokołu BGP (Border Gateway)](https://docs.microsoft.com/windows-server/remote/remote-access/bgp/border-gateway-protocol-bgp) anonsów za pośrednictwem ExpressRoute lub sieci VPN.

Wymuszanie tunelowania na platformie Azure jest skonfigurowana za pośrednictwem sieci wirtualnej trasy zdefiniowane przez użytkownika (przez). Przekierowywanie ruchu tooan w lokalnym witryny jest wyrażona jako brama sieci VPN platformy Azure toohello trasy domyślnej.

Witaj poniższej sekcji przedstawiono hello obecne ograniczenie hello tabeli routingu i tras dla sieci wirtualnej platformy Azure:

-   Każda podsieć sieci wirtualnej ma wbudowane, tabelę routingu systemu. Tabela routingu Hello system ma hello następujące trzy grupy tras:

 -  **Tras lokalnych sieci wirtualnej:** bezpośrednio toohello docelowego maszyny wirtualne w hello tej samej sieci wirtualnej

 - **O lokalnych trasach:** toohello bramy sieci VPN platformy Azure

 -  **Trasa domyślna:** bezpośrednio toohello Internet. Pakiety przeznaczone toohello prywatnych adresów IP nie pasuje do żadnego hello dwoma poprzednimi trasy są usuwane.

-   Hello wersji z tras zdefiniowanych przez użytkownika można utworzyć routingu tooadd tabeli trasy domyślnej i następnie skojarzyć hello routingu tabeli tooyour sieci wirtualnej podsieci tooenable wymuszone tunelowanie korzysta z tych podsieci.

-   Należy tooset "domyślnej witryny" między sieci wirtualnej podłączonej toohello hello między lokalizacjami lokalnych witryn.

-   Wymuszanie tunelowania musi być skojarzony z sieć wirtualną, która ma dynamiczne routingu bramy sieci VPN (nie bramy statyczne).

- ExpressRoute wymuszonego tunelowania nie jest skonfigurowany za pomocą ten mechanizm, ale zamiast tego jest włączana przez anonsuje trasę domyślną za pośrednictwem hello BGP usługi ExpressRoute sesje komunikacji równorzędnej.

> [!Note]
> Aby uzyskać więcej informacji, zobacz hello [dokumentacja usługi ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) Aby uzyskać więcej informacji.

#### <a name="network-security-appliances"></a>Urządzenia zabezpieczeń sieci
Gdy grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika zapewniają miary zabezpieczenia sieci na powitania sieci i transportu warstw hello [OSI model](https://en.wikipedia.org/wiki/OSI_model), będą toobe sytuacji, w której chcesz lub potrzebujesz tooenable zabezpieczenia na wyższych poziomach hello stosu sieciowego. W takich sytuacjach zalecamy wdrożenie zapewniana przez partnerów Azure urządzenia zabezpieczeń sieci wirtualnej.

![Urządzenia zabezpieczeń sieci](./media/azure-network-security/azure-network-security-fig-10.png)

Sieć platformy Azure, urządzenia zabezpieczeń poprawić bezpieczeństwo sieci wirtualnej i funkcji sieciowych i są one dostępne z wielu dostawców za pośrednictwem hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com). Te urządzenia wirtualnego zabezpieczeń może być wdrożony tooprovide:

-   Zapory wysokiej dostępności

-   Zapobieganie nieautoryzowanego dostępu

-   Wykrywania nieautoryzowanego dostępu

-   Zapory aplikacji sieci Web (WAFs)

-   Optymalizacja sieci WAN

-   Routing

-   Równoważenie obciążenia

-   Sieć VPN

-   Zarządzanie certyfikatami

-   Usługa Active Directory

-   Uwierzytelnianie wieloskładnikowe

#### <a name="application-gateway"></a>Brama aplikacji

[Brama aplikacji w Microsoft Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) jest dedykowany urządzenie wirtualne, która udostępnia kontroler dostarczania aplikacji (ADC) jako usługa.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-11.png)

Brama aplikacji pozwala toooptimize sieci web farmy wydajności i dostępności dzięki przeniesieniu Procesora znacznym SSL zakończenia toohello aplikacji bramy (odciążanie protokołu SSL). Dostępne są także inne warstwy 7 routingu możliwości, takie jak:

-   Rozdzielanie ruchu przychodzącego

-   Koligacji na podstawie plików cookie sesji

-   Routing na podstawie ścieżki adresu URL

-   Możliwość toohost wiele witryn sieci Web za jednym bramy aplikacji


A [zapory aplikacji sieci web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) jest również udostępniany w ramach bramy aplikacji hello. To zapewnia ochronę aplikacje tooweb wspólnej luk w zabezpieczeniach sieci web i luki w zabezpieczeniach. Brama aplikacji można skonfigurować jako internetowy bramy, wewnętrzny tylko bramy lub obie te grupy.

Zapory aplikacji sieci Web dla bramy aplikacji może działać w trybie wykrywania i zapobiegania. Przypadek użycia wspólnych dotyczy toorun Administratorzy w ruchu tooobserve Tryb wykrywania złośliwego wzorców. Po wykryciu potencjalnych luk zwroty tooprevention tryb blokuje ruch przychodzący podejrzane.

 ![Application Gateway](./media/azure-network-security/azure-network-security-fig-12.png)

Ponadto bramy aplikacji zapory aplikacji sieci Web ułatwia monitorowanie aplikacji sieci web przed atakami przy użyciu dziennika zapory aplikacji sieci Web w czasie rzeczywistym, które jest zintegrowany z [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) i [Centrum zabezpieczeń Azure](https://azure.microsoft.com/services/security-center/) alerty tootrack zapory aplikacji sieci Web i ułatwia monitorowanie trendów.

dziennika sformatowany JSON Hello bezpośrednio prowadzi konta magazynu toohello klienta. Mają pełną kontrolę nad te dzienniki i można zastosować zasad przechowywania.

Te dzienniki mogą również pozyskiwania do własnych analytics systemu za pomocą [integracji dziennika Azure](https://aka.ms/AzLog). Dzienniki zapory aplikacji sieci Web są również zintegrowane z [Operations Management Suite (OMS)](https://www.microsoft.com/cloud-platform/operations-management-suite) , korzystając z analizy dzienników OMS tooexecute zaawansowane opcje szczegółowych zapytania.

#### <a name="azure-web-application-firewall-waf"></a>Zapora aplikacji sieci web platformy Azure (WAF)

Aplikacje sieci Web są coraz bardziej cele złośliwe ataki wykorzystujące wspólnej znanych luk w zabezpieczeniach, takie jak iniekcji kodu SQL, atakami skryptów krzyżowych i inne ataki, które są widoczne w hello [10 pierwszych OWASP](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). Zapobieganie takie luki w zabezpieczeniach w aplikacji hello wymaga rygorystyczne konserwacji, poprawki i monitorowanie w wielu warstw Topologia aplikacji hello.

 ![Zapora aplikacji sieci Web platformy Azure (WAF)](./media/azure-network-security/azure-network-security-fig-13.png)

Scentralizowanego [zapory aplikacji sieci web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) można chronić przed atakami opartymi na sieci web i upraszcza zarządzanie zabezpieczeniami bez konieczności wprowadzania zmian w aplikacji.

Rozwiązanie zapory aplikacji sieci Web można reagować zagrożeniem bezpieczeństwa tooa szybsze przez stosowanie poprawek znane luki w zabezpieczeniach w centralnej lokalizacji i zabezpieczanie wszystkich aplikacji sieci web indywidualnych. Brama aplikacji w włączona jest Zapora aplikacji sieci web przekonwertowanego tooa można łatwo istniejącej bramy aplikacji.

#### <a name="network-availability-controls"></a>Formanty dostępność sieci

Istnieją różne opcje ruchu sieciowego dla toodistribute przy użyciu programu Microsoft Azure. Działanie tych opcji różni się między sobą, a same opcje wykorzystują różny zbiór funkcji i obsługują różne scenariusze. Można korzystać z nich osobno lub używać ich łącznie.

Poniżej są hello kontroli dostępności sieci:

-   Azure Load Balancer

-   Application Gateway

-   Traffic Manager

**Moduł równoważenia obciążenia Azure**

Zapewnia wysoką dostępność i sieci wydajność tooyour aplikacji. Jest równoważenia obciążenia warstwy 4 (TCP, UDP), który rozdziela przychodzący ruch między dobrej kondycji wystąpień usługi zdefiniowane w zestawie o zrównoważonym obciążeniu.

 ![Azure Load Balancer](media/azure-network-security/azure-network-security-fig-14.png)


Moduł równoważenia obciążenia Azure można skonfigurować w celu:

-   Obciążenie saldo przychodzące Internet ruchu toovirtual maszyn. Ta konfiguracja jest określana jako [równoważenia obciążenia internetowy](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Ruch Równoważenie obciążenia między maszynami wirtualnymi w sieci wirtualnej, między maszynami wirtualnymi w usługi w chmurze lub między komputerami lokalnymi i maszyn wirtualnych w sieci wirtualnej między lokalizacjami. Ta konfiguracja jest określana jako [równoważenia obciążenia wewnętrznego](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview).

-   Przekazuje ruch zewnętrzny tooa określonej maszyny wirtualnej.

Wszystkie zasoby w chmurze hello muszą dostępny z Internetu hello publicznego toobe adresów IP. Hello infrastruktury chmury na platformie Azure używa bez obsługi routingu adresów IP do jej zasobów. Azure używa translatora adresów sieciowych (NAT) z adresów toocommunicate toohello Internet publicznego adresu IP.

 **Bramy aplikacji**

 Brama aplikacji w działa w warstwie aplikacji hello (warstwy 7 w stosie odwołanie sieci OSI hello). Działa ona jako usługi serwera proxy wstecznego, przerywa połączenie klienta hello i przekazywania żądań punkty końcowe tooback-end.

 **Menedżer ruchu**

Menedżer ruchu Microsoft Azure umożliwia toocontrol hello dystrybucję ruchu użytkowników dla punktów końcowych usług w różnych centrach danych. Punkty końcowe usługi obsługiwane przez usługę Traffic Manager obejmują maszynach wirtualnych platformy Azure, aplikacji sieci Web i usług w chmurze. Usługi Traffic Manager można również używać z zewnętrznymi punktami końcowymi poza platformą Azure.

Używa usługi Traffic Manager hello systemu nazw domen (DNS) toodirect klient żąda najbardziej odpowiednia punktu końcowego toohello na podstawie [metody routingu ruchu](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) i kondycji hello hello punktów końcowych. Traffic Manager udostępnia szereg routingu ruchu metody toosuit różnych potrzeb aplikacji, kondycji punktu końcowego [monitorowania](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)i automatycznej pracy awaryjnej. Menedżer ruchu jest toofailure elastyczne, w tym hello awarii całego region platformy Azure.

Usługi Azure Traffic Manager umożliwia toocontrol hello Dystrybucja ruchu między punktami końcowymi aplikacji. Punkt końcowy jest internetowy usługi hostowanej wewnątrz lub na zewnątrz Azure.

Menedżer ruchu zapewnia dwie kluczowe korzyści:

-   Rozkład ruchu zgodnie z tooone kilku [metody routingu ruchu](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods).

-   [Ciągłego monitorowania kondycji punktu końcowego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring) i automatycznej pracy awaryjnej, gdy punkty końcowe nie powiedzie się.

Gdy klient próbuje tooconnect tooa usługi, najpierw musi wskazywać nazwę DNS hello adres IP tooan usługi hello. następnie powitania klienta łączy toothat — usługi hello tooaccess adresu IP. Punkty końcowe na podstawie reguł hello hello metody routingu ruchu usługi Traffic Manager używa DNS toodirect klientów toospecific. Klienci łączą bezpośrednio z punktu końcowego toohello wybrane. Menedżer ruchu nie jest serwer proxy lub bramy. Menedżer ruchu nie widzi ruchu hello przekazywania między powitania klienta i usługi hello.

### <a name="azure-network-validation"></a>Sprawdzanie poprawności sieci platformy Azure

Sprawdzanie poprawności sieci platformy Azure jest tooensure, który hello sieć platformy Azure działa zgodnie z jest skonfigurowany i sprawdzania poprawności można wykonać przy użyciu hello usługi i funkcje dostępne toomonitor hello sieci. Monitor sieci Azure, umożliwia dostęp do nadmiar rejestrowania i diagnostyki możliwości, które pozwalają z insights toounderstand Twojego wydajność sieci i kondycji. Te możliwości są udostępniane za pośrednictwem portalu, powłoki Power Shell, interfejsu wiersza polecenia, interfejs API Rest i zestawu SDK.

Azure bezpieczeństwa operacyjnego odwołuje się toohello usług, kontrolek i toousers dostępne funkcje ochrony danych, aplikacji i innych zasobów na platformie Microsoft Azure. Azure bezpieczeństwa operacyjnego w oparciu framework, która będzie zawierała wiedzę hello za pośrednictwem różnych funkcji, które są unikatowe tooMicrosoft, w tym hello Microsoft Security Development Lifecycle (SDL), hello Centrum odpowiedź zabezpieczeń firmy Microsoft Program i głębokie świadomości hello przez zabezpieczeń zagrożeń.

-   [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)

-   [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   [Azure obserwatora sieciowego](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

-   [Analizy usługi Azure Storage](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

-   Azure Resource Manager

#### <a name="azure-resource-manager"></a>Menedżer zasobów systemu Azure

osoby Hello i procesy, które działają na Microsoft Azure są prawdopodobnie hello najważniejszych funkcji zabezpieczeń hello platformy. W tej sekcji opisano funkcji firmy Microsoft globalnej infrastruktury centrum danych, które pomagają zwiększyć i zachować bezpieczeństwo, ciągłość działania i ochrony prywatności.

Hello infrastruktura aplikacji zwykle obejmuje wiele składników — może być maszynę wirtualną, konta magazynu i sieci wirtualnej lub aplikacji sieci web, bazy danych, serwer bazy danych i usług innych firm. Te składniki nie są widoczne jako osobne jednostki, tylko jako powiązane i zależne od siebie nawzajem części jednej całości. Mają toodeploy, zarządzanie i monitorowanie ich jako grupa. Usługa Azure Resource Manager umożliwia toowork z zasobami hello w rozwiązaniu jako grupa.

Można wdrożyć, zaktualizować lub usunąć wszystkie zasoby powitania dla danego rozwiązania w jednej, skoordynowanej operacji. Wdrażanie wykonuje się przy użyciu szablonu, którego można następnie używać w różnych środowiskach (testowanie, etap przejściowy i produkcja). Usługa Resource Manager zapewnia zabezpieczeń, inspekcji i znakowanie toohelp funkcje zarządzania zasobami po wdrożeniu.

**Zalety Hello za pomocą Menedżera zasobów**

Usługa Resource Manager zapewnia kilka korzyści:

-   Można wdrożyć, zarządzanie i monitorowanie wszystkich zasobów hello do rozwiązania jako grupy zamiast obsługiwania zasobów pojedynczo.

-   Można wielokrotnie wdrażania rozwiązania w całym cyklu programistycznym hello i mieć pewność, zasoby są wdrażane w spójnym stanie.

-   Możliwość zarządzania infrastrukturą przy użyciu szablonów deklaratywnych zamiast skryptów.

-   Można zdefiniować hello zależności między zasobami, aby wdrażać je w odpowiedniej kolejności hello.

-   Można zastosować usług tooall kontroli dostępu w grupie zasobów, ponieważ na platformie zarządzania hello natywnej integracji funkcji kontroli dostępu opartej na rolach (RBAC).

-   Możliwość dodawania tagów tooresources toologically organizowanie wszystkie zasoby hello w ramach subskrypcji.

-   Można również uprościć rozliczenia w organizacji, wyświetlając kosztów dla grupy zasobów, udostępnianie tagu.

> [!Note]
> Menedżer zasobów udostępnia nowe toodeploy sposób rozwiązań i zarządzania nimi. Jeśli używasz hello wcześniejszego modelu wdrożenia i mają toolearn o zmianach hello, zobacz [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="azure-network-logging-and-monitoring"></a>Monitorowanie i rejestrowanie sieć platformy Azure

Platforma Azure oferuje wiele narzędzi toomonitor, zapobiegania, wykrywania i odpowiadać toonetwork zdarzeń zabezpieczeń. Witaj najbardziej zaawansowanych narzędzi dostępnych tooyou w tym obszarze, należą:

-   Network Watcher

-   Poziom monitorowania zasobów sieciowych

-   Log Analytics

### <a name="network-watcher"></a>Obserwatora sieciowego

[Monitor sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) — na podstawie scenariusza monitorowania jest dostarczana z funkcji hello w obserwatora sieciowego. Ta usługa obejmuje przechwytywania pakietów, następnego przeskoku, przepływ IP Sprawdź widok grupy zabezpieczeń, dzienniki przepływu NSG. Scenariusz poziomu monitorowania udostępnia widok tooend zakończenia zasobów sieciowych w monitorowania zasobów sieciowych tooindividual kontrastu.

 ![Network Watcher](./media/azure-network-security/azure-network-security-fig-15.png)

Obserwatora sieciowego jest usługą regionalnych, która umożliwia toomonitor możesz i diagnozowanie warunki na poziomie sieci scenariusz w, do i z platformy Azure. Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i uzyskać informacje na temat technologii sieci tooyour na platformie Azure.

Obserwatora sieciowego ma obecnie hello następujące możliwości:

#### <a name="topology"></a>Topologia

[Topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) zwraca wykres zasobów sieciowych w sieci wirtualnej. Witaj wykres przedstawia hello połączenia między łączności sieciowej tooend hello zasobów toorepresent hello zakończenia. W portalu hello topologii zwraca hello obiektów zasobów zgodnie z harmonogramem podstawę sieci wirtualnej. Relacje Hello są określone przez linie między zasobami hello poza region obserwatora sieciowego hello, nawet jeśli w zasobie hello grupy nie zostaną wyświetlone. zasoby Hello zwracane w widoku portalu hello są podzbiorem hello składników sieciowych, które są wyświetlone na wykresie. toosee hello pełną listę zasobów sieciowych, można użyć [PowerShell](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-powershell) lub [REST](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-rest).

Ponieważ zasoby są zwracane hello połączenie między one są modelowane w obszarze dwie relacje.

- **Zawieranie** -sieć wirtualna zawiera podsieci, która zawiera jedną kartą sieciową.

- **Skojarzone** -A kart interfejsu Sieciowego jest skojarzona z maszyną Wirtualną.

#### <a name="variable-packet-capture"></a>Przechwytywania pakietów zmiennej

Monitor sieci [przechwytywania pakietów zmiennej](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) pozwala toocreate pakietów przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej. Przechwytywania pakietów pomaga anomalii sieci toodiagnose zarówno rozbudowy i proactivity. Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej.

Przechwytywania pakietów jest uruchamiana zdalnie za pomocą Monitora sieci rozszerzenia maszyny wirtualnej. Funkcja ta ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego na potrzeby hello maszynę wirtualną, która zapisuje cenny czas. Przechwytywania pakietów mogą być wyzwalane za pośrednictwem portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST. Przykład sposobu przechwytywania pakietów mogą być wyzwalane jest z alertami maszyny wirtualnej.

#### <a name="ip-flow-verify"></a>Sprawdź przepływ IP

[Sprawdź przepływów IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) sprawdza, czy pakiet jest dozwolony lub odrzucany tooor z maszyny wirtualnej na podstawie informacji 5-elementowej. Te informacje składa się z kierunku, protokół lokalny adres IP, zdalny adres IP, portu lokalnego i portu zdalnego. Jeśli pakietów hello jest zabroniony przez grupę zabezpieczeń, zwracana jest nazwa hello hello reguła odmowy pakietów hello. Podczas gdy można wybrać dowolny źródłowy lub docelowy adres IP, funkcja ta ułatwia ona administratorom szybkie diagnozowanie problemów z łącznością z lub toohello internet i z lub toohello w środowisku lokalnym.

Sprawdź przepływów IP jest przeznaczony dla interfejsu sieciowego maszyny wirtualnej. Przepływ ruchu jest następnie zweryfikować oparte na powitania skonfigurowane ustawienia tooor z tym interfejs sieciowy. Ta funkcja jest przydatna w potwierdzaniu, jeśli zasada grupy zabezpieczeń sieci blokuje tooor ruch przychodzący lub wychodzący z maszyny wirtualnej.

#### <a name="next-hop"></a>Następny przeskok

Określa hello [następnego przeskoku](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) pakiety przesyłane w hello Azure sieci szkieletowej, włączenie możesz toodiagnose żadnych błędnie skonfigurowane trasy zdefiniowane przez użytkownika. Ruch z maszyny Wirtualnej jest wysyłany tooa docelowym oparte na trasach efektywne hello skojarzony z jedną kartą sieciową. Następny przeskok pobiera typ następnego przeskoku hello i adres IP pakietu z określonej maszyny wirtualnej i karty sieciowej. Dzięki temu toodetermine hello pakietów jest docelowy skierowanego toohello lub jest holed ruchu hello jest czarny.

Następny przeskok zwraca również wartość tabeli tras hello skojarzone z następnego przeskoku hello. Podczas wykonywania zapytania następnego przeskoku, jeśli trasa hello jest zdefiniowana jako trasy zdefiniowane przez użytkownika, zostanie zwrócony tej trasy. W przeciwnym razie wartość następnego skoku zwraca "Trasa systemowa".

#### <a name="security-group-view"></a>Widok grupy zabezpieczeń

Pobiera reguły zabezpieczeń skuteczne i zastosowane hello, które są stosowane na maszynie Wirtualnej. Na poziomie podsieci lub na poziomie karty Sieciowej skojarzonych grup zabezpieczeń sieci. Skojarzone na poziomie podsieci, zastosowanie wystąpień maszyn wirtualnych hello tooall w hello podsieci. Sieci [widok grupy zabezpieczeń](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) zwraca wszystkie grupy NSG hello skonfigurowane i reguł, które są skojarzone na poziomie podsieci i karty na maszynie wirtualnej, zapewniając wgląd w konfiguracji hello. Ponadto zasady efektywnym elementem systemu zabezpieczeń hello są zwracane dla każdej z kart sieciowych hello na maszynie wirtualnej. Widok przy użyciu grup zabezpieczeń sieci można ocenić maszyny Wirtualnej dla luk w zabezpieczeniach sieci takich jak otwartych portów. Można również sprawdzić czy grupy zabezpieczeń sieci działa zgodnie z oczekiwaniami, na podstawie [porównanie hello skonfigurowane i hello reguły efektywnym elementem systemu zabezpieczeń](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-auditing-powershell).

#### <a name="nsg-flow-logging"></a>Rejestrowanie przepływu NSG

 Dzienniki przepływu dla grup zabezpieczeń sieci Włącz toocapture dzienniki pokrewne tootraffic, który ma być dozwolony lub odrzucany przez reguły zabezpieczeń hello hello grupy. Przepływ Hello jest zdefiniowana przez informacji 5-elementowej — źródłowy adres IP, docelowy adres IP, Port źródłowy, Port docelowy i protokołu.

[Grupy zabezpieczeń sieci przepływu dzienniki](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) są funkcją obserwatora sieciowego, który pozwala tooview informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci.

#### <a name="virtual-network-gateway-and-connection-troubleshooting"></a>Brama sieci wirtualnej i rozwiązywanie problemów z połączenia

Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure. Jeden z tych funkcji jest zasobem rozwiązywania problemów. [Rozwiązywanie problemów z zasobów](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) może być wywoływany przez programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST. Po wywołaniu obserwatora sieciowego sprawdza kondycję hello bramy sieci wirtualnej lub połączenie i zwraca jego wyniki.

W tej sekcji przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla zasobu Rozwiązywanie problemów z.

-   [Rozwiązywanie problemów z bramy sieci wirtualnej](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

-   [Rozwiązywanie problemów z połączeniem](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)

#### <a name="network-subscription-limits"></a>Limity subskrypcji sieci

[Limity subskrypcji sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) udostępniają szczegółowe informacje dotyczące użycia hello każdego zasobu sieciowego hello w ramach subskrypcji w regionie przed hello maksymalną liczbę dostępnych zasobów.

#### <a name="configuring-diagnostics-log"></a>Konfigurowanie dziennika diagnostyki

Zawiera obserwatora sieciowego [dzienników diagnostycznych](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) widoku. Ten widok zawiera wszystkich zasobów sieciowych, które obsługują rejestrowania diagnostycznego. Z tego widoku można włączyć i wyłączyć zasobów sieciowych, łatwo i szybko.

### <a name="network-resource-level-monitoring"></a>Poziom monitorowania zasobów sieciowych

Witaj, następujące funkcje są dostępne dla poziomu monitorowania zasobów:

#### <a name="audit-log"></a>Dziennik inspekcji

Operacje wykonywane w ramach konfiguracji hello sieci są rejestrowane. Te dzienniki inspekcji są istotne tooestablish różnych compliances. Dzienniki te mogą być wyświetlane w portalu Azure hello lub pobrany przy użyciu narzędzi firmy Microsoft, takich jak usługi Power BI lub narzędzi innych firm. Dzienniki inspekcji są dostępne za pośrednictwem portalu hello, programu PowerShell, interfejsu wiersza polecenia i interfejsu API Rest.

> [!Note]
> Aby uzyskać więcej informacji na dziennikach inspekcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
Dzienniki inspekcji są dostępne dla operacje wykonywane na wszystkich zasobów sieciowych.


#### <a name="metrics"></a>Metryki

Metryki są miar wydajności i liczniki zebrane w okresie. Metryki są obecnie dostępne dla bramy aplikacji. Metryki mogą być używane tootrigger alerty oparte na wartości progowej. Azure Application Gateway domyślnie monitoruje kondycję hello wszystkich zasobów w jego puli zaplecza i automatycznie usuwa dowolnego zasobu z puli hello określana jako zła. Brama aplikacji w nadal toomonitor hello złej kondycji wystąpień i dodaje je kopii toohello dobrej kondycji puli zaplecza po udostępnieniu i sondy toohealth odpowiedź. Brama aplikacji w wysyła hello sondy kondycji z hello tego samego portu, który jest zdefiniowany w ustawieniach protokołu HTTP zaplecza hello. Ta konfiguracja zapewnia, że tej sondy hello testuje hello sam port, że klienci będą stosowane tooconnect toohello wewnętrznej bazy danych.

> [!Note]
> Zobacz [diagnostyki bramy aplikacji](https://docs.microsoft.com/azure/application-gateway/application-gateway-probe-overview) tooview jak metryki mogą być używane toocreate alertów.

#### <a name="diagnostic-logs"></a>Dzienniki diagnostyczne

Okresowe i spontanicznych zdarzenia są tworzone przez zasobów sieciowych i zarejestrowane na kontach magazynu, wysyłane tooan Centrum zdarzeń lub analizy dzienników. Te dzienniki wgląd w kondycję hello zasobu. Te dzienniki można wyświetlać w narzędzi, takich jak Power BI i analizy dzienników. toolearn jak tooview dzienników diagnostycznych, odwiedź stronę [analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics).

Dzienniki diagnostyczne są dostępne dla [modułu równoważenia obciążenia](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [grup zabezpieczeń sieci](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), trasy i [brama aplikacji w](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Wyświetl dzienniki diagnostyczne zawiera obserwatora sieciowego. Ten widok zawiera wszystkich zasobów sieciowych, które obsługują rejestrowania diagnostycznego. Z tego widoku można włączyć i wyłączyć zasobów sieciowych, łatwo i szybko.

### <a name="log-analytics"></a>Log Analytics

[Dziennika analizy](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) jest usługą [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) Twojego toomaintain środowisk chmury i lokalnych który monitoruje ich dostępności i wydajności. Zbiera dane generowane przez zasobów w swoich środowiskach w chmurze i lokalnie i z innych monitorowania analizy tooprovide narzędzi w wielu źródeł.

Analiza dzienników oferuje hello następujące rozwiązania do monitorowania sieci:

-   Monitor wydajności sieci (NPM)

-   Azure analytics bramy aplikacji

-   Grupy zabezpieczeń sieci Azure analityka

#### <a name="network-performance-monitor-npm"></a>Monitor wydajności sieci (NPM)
Witaj [monitora wydajności sieci](https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor) rozwiązanie do zarządzania jest rozwiązanie, które monitoruje kondycję hello, dostępności i uzyskiwanie sieci do monitorowania sieci.

Jest używana toomonitor łączność między:

-   Chmura publiczna i lokalnych

-   centra danych i lokalizacje użytkownika (biurach oddziałów)

-   podsieci hosting różnych warstw aplikacji wielowarstwowych.


#### <a name="azure-application-gateway-analytics-in-log-analytics"></a>Analiza bramy aplikacji Azure w analizy dzienników

powitania po dzienniki są obsługiwane w przypadku bram aplikacji:

-   ApplicationGatewayAccessLog

-   ApplicationGatewayPerformanceLog

-   ApplicationGatewayFirewallLog

następujące metryki Hello są obsługiwane w przypadku bram aplikacji:

-   Przepływność 5 minut

#### <a name="azure-network-security-group-analytics-in-log-analytics"></a>Analiza grupy zabezpieczeń sieci platformy Azure w analizy dzienników

Witaj następujące dzienniki są obsługiwane w przypadku [sieciowej grupy zabezpieczeń](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log):

- **NetworkSecurityGroupEvent:** zawiera wpisy, dla których NSG reguły są stosowane tooVMs i wystąpienia ról na podstawie adresu MAC. Stan Hello te reguły są gromadzone co 60 sekund.

- **NetworkSecurityGroupRuleCounter:** zawiera wpisy dla ile razy każda grupa NSG do reguły jest stosowane toodeny lub zezwolić na ruch.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o zabezpieczeń, odczytując niektóre nasze tematy szczegółowe zabezpieczeń:

-   [Analizy dzienników dla grup zabezpieczeń sieci (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)

-   [Sieć innowacje tego dysku hello chmury przerw w działaniu](https://azure.microsoft.com/blog/networking-innovations-that-drive-the-cloud-disruption/)

-   [SONiC: oprogramowanie przełącznika hello firmy Microsoft w chmurze globalnych uprawnień sieciowe hello](https://azure.microsoft.com/blog/sonic-the-networking-switch-software-that-powers-the-microsoft-global-cloud/)

-   [Jak Microsoft kompilacje jego szybkie i niezawodne sieci globalnej](https://azure.microsoft.com/blog/how-microsoft-builds-its-fast-and-reliable-global-network/)

-   [Oświetlenie zapasowej innowacji sieci](https://azure.microsoft.com/blog/lighting-up-network-innovation/)
