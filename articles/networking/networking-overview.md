---
title: sieci aaaAzure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat usługi sieciowe Azure i możliwości."
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Sieć platformy Azure

Platforma Azure oferuje szeroką gamę możliwości sieciowych, które mogą być używane razem lub oddzielnie. Kliknij dowolny z następujących kluczowych możliwości toolearn więcej informacji na temat ich hello:
- [Łączność między zasobami Azure](#connectivity): w bezpieczny, prywatnej sieci wirtualnej w chmurze hello zasobów Azure połączenia.
- [Połączenie z Internetem](#internet-connectivity): komunikacji tooand z zasobów platformy Azure za pośrednictwem hello Internet.
- [Połączenie lokalne](#on-premises-connectivity): łączenie zasobów tooAzure sieci lokalnej, za pośrednictwem wirtualnej sieci prywatnej (VPN) przez hello Internet, lub tooAzure dedykowanego połączenia.
- [Kierunek ruchu i równoważenie obciążenia](#load-balancing): hello tooservers ruchu równoważenia obciążenia w tej samej lokalizacji i tooservers bezpośredniego ruchu w różnych lokalizacjach.
- [Zabezpieczenia](#security): filtrowania ruchu sieciowego między podsieciami sieci lub poszczególnych maszyn wirtualnych (VM).
- [Routing](#routing): korzystać z routingu domyślne lub pełnej kontroli routingu między zasobami platformy Azure i lokalnymi.
- [Możliwości zarządzania](#manageability): Monitor i zarządzania zasobami sieci platformy Azure.
- [Wdrażanie i Konfigurowanie narzędzi](#tools): za pomocą portalu sieci web lub narzędzia wiersza polecenia i platform toodeploy i konfigurowanie zasobów sieciowych.

## <a name="Connectivity"></a>Łączność między zasobami Azure

Zasobów platformy Azure, takich jak maszyny wirtualne, usługi w chmurze, zestawy skalowania maszyn wirtualnych i środowiska usługi Azure App Service może komunikować się przez użytkowników ze sobą za pośrednictwem sieci wirtualnej platformy Azure (VNet). Sieci wirtualnej jest logiczną izolacją hello chmury Azure w wersji dedykowanej tooyour [subskrypcji](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json). Można zaimplementować wiele sieci wirtualnych w ramach każdej subskrypcji platformy Azure i Azure [region](https://azure.microsoft.com/regions). Każda sieć wirtualna jest odizolowana od innych sieci wirtualnych. Dla każdej sieci wirtualnej można:

- Określ niestandardowe prywatnych przestrzeni adresów IP przy użyciu prywatnych i publicznych adresów (RFC 1918). Azure przypisuje toohello połączonych zasobów sieci wirtualnej prywatnego adresu IP z hello przestrzeń adresów, które można przypisać.
- Segment hello sieci wirtualnej do co najmniej jednej podsieci i przydzielić część hello sieci wirtualnej adres miejsca tooeach podsieci.
- Korzystanie z rozpoznawania nazw platformy Azure lub Podaj własny serwer DNS do użytku przez zasoby podłączone tooa sieci wirtualnej.

więcej informacji na temat usługi Azure Virtual Network hello, przeczytaj hello toolearn [omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu. Możesz połączyć sieci wirtualnych tooeach innych, włączanie zasoby połączone toocommunicate sieci wirtualnej tooeither ze sobą za pośrednictwem sieci wirtualnych. Można użyć jednego lub obu hello następujące opcje tooconnect sieci wirtualnych tooeach inne:

- **Komunikacja równorzędna:** umożliwia zasoby podłączone toodifferent sieci wirtualnych platformy Azure w ramach hello tego samego regionu Azure toocommunicate ze sobą. Witaj przepustowości i opóźnień między hello sieci wirtualnych jest hello sam tak, jakby zasoby hello był połączony toohello tej samej sieci wirtualnej. toolearn więcej informacji na temat komunikacji równorzędnej, przeczytaj hello [komunikacji równorzędnej omówienie sieci wirtualnej](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Brama sieci VPN:** umożliwia zasoby podłączone toodifferent sieci wirtualnych platformy Azure w różnych regionach platformy Azure toocommunicate ze sobą. Przepływ ruchu między sieciami wirtualnymi za pośrednictwem bramy sieci VPN platformy Azure. Przepustowość między sieciami wirtualnymi jest ograniczona toohello przepustowości hello bramy. więcej informacji na temat łączenia sieci wirtualnych z bramą sieci VPN, przeczytaj hello toolearn [skonfigurować połączenia do wirtualnymi w regionach](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

## <a name="internet-connectivity"></a>Połączenie z Internetem

Wszystkich połączonych zasobów Azure tooa sieć wirtualna ma łączność wychodząca toohello Internet domyślnie. Witaj prywatnego adresu IP zasobu hello jest adres sieciowy źródła przetłumaczyła publicznego adresu IP (SNAT) tooa hello infrastruktury platformy Azure. więcej informacji na temat wychodzące połączenie z Internetem, przeczytaj hello toolearn [Opis połączeń wychodzących na platformie Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

toocommunicate ruchu przychodzącego tooAzure zasobów z hello Internet lub toocommunicate toohello wychodzących, Internet bez SNAT, zasobu można przypisać do publicznego adresu IP. więcej informacji na temat publiczne adresy IP, przeczytaj hello toolearn [publicznego adresu IP, adresy](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

## <a name="on-premises-connectivity"></a>Połączenie lokalne

Dostępne zasoby w sieci wirtualnej bezpiecznie za pośrednictwem połączenia sieci VPN lub bezpośrednie połączenie prywatne. toosend ruchu sieciowego między sieci wirtualnej platformy Azure i sieci lokalnej, należy utworzyć bramę sieci wirtualnej. Możesz skonfigurować ustawienia dla hello bramy toocreate hello typu połączenia, które chcesz, sieci VPN lub usługi ExpressRoute.

Można połączyć z tooa sieci lokalnej sieci wirtualnej przy użyciu dowolnej kombinacji hello następujące opcje:

**Punkt lokacja (sieć VPN przez protokół SSTP)**

Witaj poniższej ilustracji przedstawiono oddzielnych toosite punktu połączenia między wiele komputerów i sieci wirtualnej:

![Punkt-lokacja](./media/networking-overview/point-to-site.png)

To połączenie zostanie nawiązane między jednego komputera i sieci wirtualnej. Tego typu połączenia jest doskonałym, jeśli tylko rozpoczniesz pracę z platformą Azure, lub dla deweloperów, ponieważ wymaga żadnych zmian tooyour istniejącej sieci. Istnieje również wygodne, gdy nawiązujesz połączenie z lokalizacji zdalnej, takich jak konferencji lub macierzystego. Połączenia punkt lokacja często są połączone z połączenia lokacja lokacja za pośrednictwem hello tej samej bramy sieci wirtualnej. Hello połączenie korzysta z komunikacji tooprovide szyfrowane protokół SSTP hello za pośrednictwem hello Internet między komputerem hello i hello sieci wirtualnej. Opóźnienie Hello VPN punkt lokacja jest nieprzewidywalne, ponieważ hello ruch przechodzi hello Internet.

**Lokacja lokacja (tunel VPN IPsec i IKE)**

![Lokacja-lokacja](./media/networking-overview/site-to-site.png)

To połączenie zostanie nawiązane między lokalnego urządzenia sieci VPN i bramy sieci VPN platformy Azure. Ten typ połączenia pozwala dowolnego zasobu lokalnego, aby autoryzować hello tooaccess sieci wirtualnej. połączenie Hello jest VPN IPSec i IKE, zapewniająca szyfrowaną komunikację za pośrednictwem hello Internet między urządzeniami lokalnymi i hello bramy sieci VPN platformy Azure. Możesz połączyć wiele toohello lokacjami lokalnymi tej samej bramy sieci VPN. Witaj lokalnego urządzenia sieci VPN w każdej lokacji musi mieć zewnętrznie uwzględniającym publiczny adres IP, który nie znajduje się za urządzeniem NAT Opóźnienie Hello połączenia lokacja lokacja jest nieprzewidywalne, ponieważ hello ruch przechodzi hello Internet.

**ExpressRoute (dedykowane połączenie prywatne)**

![ExpressRoute](./media/networking-overview/expressroute.png)

Tego typu połączenie zostanie nawiązane między siecią a Azure, za pośrednictwem partner usługi ExpressRoute. To połączenie jest prywatne. Ruch omija hello Internet. Opóźnienie Hello połączenia ExpressRoute jest przewidywalne, ponieważ ruch nie przechodzenia hello Internet. ExpressRoute można łączyć za pomocą połączenia lokacja lokacja.

więcej informacji na temat wszystkich hello poprzedniej opcji połączenia, przeczytaj hello toolearn [Diagram topologii połączenia](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

## <a name="load-balancing"></a>Kierunek ruchu i równoważenia obciążenia

Microsoft Azure udostępnia wiele usług do zarządzania ruchem w sieci i równoważenia obciążenia. Można użyć dowolnego hello następujące możliwości osobno lub razem:

**Równoważenie obciążenia DNS**

Witaj usługi Azure Traffic Manager zapewnia globalnego równoważenia obciążenia DNS. Menedżer ruchu odpowiada tooclients o adresie IP hello dobrej kondycji punktu końcowego, na podstawie jednej z następujących metod routingu hello:
- **Geograficzne:** klienci są kierowani toospecific punktów końcowych (Azure, zewnętrznego lub zagnieżdżonych) oparte na które lokalizacji geograficznej ich zapytanie DNS pochodzi z. Ta metoda umożliwia realizację scenariuszy, których wiedzy o region geograficzny klienta i ich na jego podstawie routingu jest ważna. Przykładami zgodnych z danych suwerenności zleceń, lokalizacja środowiska użytkownika & zawartości i pomiar ruchu z różnych regionów.
- **Wydajność:** hello adres IP zwrócony klienta toohello hello "najbliższy" toohello klienta. punkt końcowy "najbliższy" Hello nie jest niekoniecznie najbliższego mierzony odległość geograficznej. Jednak ta metoda określa hello najbliższy punkt końcowy mierząc opóźnienia sieci. Menedżer ruchu zapisuje Internet tabeli tootrack hello obustronne czas opóźnienia między zakresów adresów IP i każdego centrum danych Azure.
- **Priorytet:** ruch jest punkt końcowy ukierunkowanej toohello głównej (najwyższy priorytet). Jeśli hello podstawowy punkt końcowy nie jest dostępna, trasy menedżera ruchu hello ruchu toohello drugiego punktu końcowego. Jeśli oba hello podstawowych i pomocniczych punkty końcowe nie są dostępne, hello ruch przechodzi toohello innej itd. Dostępność punktu końcowego hello opiera się na stan hello skonfigurowane (włączona lub wyłączona) i hello monitorowania bieżących punktów końcowych.
- **Ważone działanie okrężne:** dla każdego żądania usługi Traffic Manager losowo wybiera dostępnego punktu końcowego. prawdopodobieństwo Hello wybrać punkt końcowy jest oparta na wag hello przypisane tooall dostępnych punktów końcowych. Przy użyciu hello sama waga we wszystkich wyników punktów końcowych w nawet Dystrybucja ruchu. Za pomocą wag wyższe lub niższe w określonych punktach końcowych sprawia, że te toobe punkty końcowe częściej lub rzadziej zwracany w odpowiedzi DNS hello.

Witaj poniższej ilustracji przedstawiono żądania tooa skierowane do aplikacji sieci web aplikacji sieci Web punktu końcowego. Punkty końcowe można także innych usług Azure, takich jak maszyny wirtualne i usługi w chmurze.

![Traffic Manager](./media/networking-overview/traffic-manager.png)

Witaj, klient połączy się bezpośrednio toothat punktu końcowego. Menedżer ruchu Azure wykrywa punkt końcowy jest zła, a następnie przekierowuje klientów tooa innych, dobrej kondycji punktu końcowego. więcej na temat Menedżera ruchu, przeczytaj hello toolearn [Omówienie usługi Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

**Równoważenie obciążenia aplikacji**

Hello Usługa bramy aplikacji Azure udostępnia kontroler dostarczania aplikacji (ADC) jako usługa. Brama aplikacji w oferuje różne warstwy 7 (HTTP/HTTPS) równoważenia obciążenia możliwości dla aplikacji, w tym aplikacji sieci web dla zapory tooprotect aplikacji sieci web z luk w zabezpieczeniach i luk w zabezpieczeniach. Brama aplikacji można też wydajność kolektywu serwerów sieci web toooptimize dzięki przeniesieniu brama aplikacji w toohello zakończenia SSL użycie Procesora CPU. 

Inne funkcje routingu warstwy 7 obejmują rozdzielanie ruchu przychodzącego, koligacji na podstawie plików cookie sesji, routingu adresów URL na podstawie ścieżki i toohost możliwości hello wiele witryn sieci Web za bramy pojedynczej aplikacji. Brama aplikacji można skonfigurować jako bramy łączącej z Internetem, bramę wyłącznie wewnętrznym lub obie te grupy. Brama aplikacji jest w pełni Azure zarządzanych, skalowalności i wysokiej dostępności. Zapewnia ona bogaty zestaw funkcji diagnostyki i rejestrowania, aby uprościć zarządzanie. więcej informacji na temat bramy aplikacji, przeczytaj hello toolearn [omówienie bramy aplikacji](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

Witaj poniższej ilustracji przedstawiono adresu URL ścieżki na podstawie routingu z bramy aplikacji:

![Application Gateway](./media/networking-overview/application-gateway.png)

**Równoważenie obciążenia sieciowego**

Hello moduł równoważenia obciążenia Azure udostępnia wysokiej wydajności i małych opóźnieniach 4 warstwy równoważenia obciążenia do wszystkich protokołów UDP i TCP. Zarządza połączeń przychodzących i wychodzących. Można skonfigurować publicznych oraz wewnętrznych końcowych z równoważeniem obciążenia. Można zdefiniować toomap reguły ruchu przychodzącego miejsc docelowych puli tooback zakończenia połączenia przy użyciu protokołu TCP i HTTP badania kondycji opcje toomanage dostępności usługi. więcej informacji na temat usługi równoważenia obciążenia, przeczytaj hello toolearn [Omówienie usługi równoważenia obciążenia](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

Witaj, na poniższej ilustracji przedstawiono aplikację wielowarstwową internetowy, który używa zarówno usługi równoważenia obciążenia wewnętrznych i zewnętrznych:

![Moduł równoważenia obciążenia](./media/networking-overview/load-balancer.png)

## <a name="security"></a>Zabezpieczeń

Można filtrować ruch tooand z zasobów platformy Azure przy użyciu hello następujące opcje:

- **Sieć:** można zaimplementować sieć platformy Azure zabezpieczeń grupy (NSG) toofilter przychodzący i wychodzący ruch tooAzure zasobów. Każda grupa NSG zawiera jedną lub więcej reguł ruchu przychodzącego i wychodzącego. Każda reguła określa hello źródłowych adresów IP, docelowe adresy IP, port i protokół, który ruch jest filtrowany za pomocą. Grupy NSG można podsieci tooindividual zastosowany i indywidualnych maszyn wirtualnych. więcej informacji na temat grup NSG, przeczytaj hello toolearn [Przegląd grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Aplikacja:** przy użyciu bramy aplikacji z zapory aplikacji sieci web może chronić aplikacje sieci web z luk w zabezpieczeniach i luk w zabezpieczeniach. Typowe przykłady są SQL iniekcji atakami, skryptów krzyżowych oraz źle sformułowane nagłówki. Brama aplikacji w odfiltrowuje ten ruch i go zatrzyma dotrze do serwerów sieci web. Jesteś tooconfigure stanie reguł, które mają być włączone. Zasady negocjacji SSL Hello możliwości tooconfigure podano tooallow niektórych toobe zasad jest wyłączone. więcej informacji na temat hello zapory aplikacji sieci web, przeczytaj hello toolearn [zapory aplikacji sieci Web](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

Jeśli potrzebujesz możliwości sieci Azure nie zapewniają lub aplikacje sieci toouse użyć lokalnego można zaimplementować hello produktów na maszynach wirtualnych i podłącz je tooyour sieci wirtualnej. Witaj [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) zawiera kilka wstępnie skonfigurowane z aplikacjami sieci można obecnie używać różnych maszyn wirtualnych. Te wstępnie skonfigurowane maszyny wirtualne są zazwyczaj określonego tooas urządzeń wirtualnych sieci (NVA). NVAs są dostępne z aplikacjami, takie jak zapory i Optymalizacja sieci WAN.

## <a name="routing"></a>Routing

Platforma Azure tworzy domyślne tabele tras, umożliwiających podsieci tooany połączonych zasobów w dowolnej sieci wirtualnej toocommunicate ze sobą. Można zaimplementować lub obie następujące typy toooverride trasy hello hello trasy domyślne, które tworzy Azure:
- **Zdefiniowane przez użytkownika:** tworzenia tabel tras niestandardowych trasy, które kontrolują, których ruch jest kierowany toofor każdej podsieci. więcej informacji na temat trasy zdefiniowane przez użytkownika, odczytać hello toolearn [trasy zdefiniowane przez użytkownika](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Border gateway protocol (BGP):** Jeśli połączyć sieci wirtualnej sieci lokalnej tooyour przy użyciu połączenia bramy sieci VPN platformy Azure lub usługi ExpressRoute, można propagować tooyour trasy protokołu BGP sieci wirtualnych. Protokół BGP jest hello standardowy protokół routingu często używane w hello Internet tooexchange routingu i uzyskiwanie informacji między dwie lub więcej sieci. Gdy są używane w kontekście hello sieciach wirtualnych platformy Azure, hello umożliwia BGP bramy sieci VPN platformy Azure i lokalnego urządzenia sieci VPN, o nazwie BGP równorzędnymi użytkownikami lub sąsiadów, tooexchange "tras", który informuje zarówno bramy na powitania dostępności i uzyskiwanie dla tych prefiksów toogo za pośrednictwem bramy hello lub routery związane. Protokół BGP można także włączyć routing tranzytowy między wieloma sieciami przez propagowania tras BGP bramy uczy się z jednego tooall elementu równorzędnego protokołu BGP innych elementów równorzędnych protokołu BGP. toolearn więcej informacji na temat protokołu BGP, zobacz hello [protokołu BGP z bramy sieci VPN platformy Azure — omówienie](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

## <a name="manageability"></a>Możliwości zarządzania

Platforma Azure oferuje następujące hello narzędzi toomonitor i zarządzanie nimi sieci:
- **Dzienniki aktywności:** Azure wszystkie zasoby mają Dzienniki aktywności, które zawierają informacje o operacjach podjęte umieść stanu operacji i kto zainicjował operację hello. więcej informacji o Dzienniki aktywności, przeczytaj hello toolearn [działania rejestruje informacje o](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Dzienniki diagnostyczne:** okresowo i spontanicznych zdarzenia są tworzone przez zasobów sieciowych i zarejestrowane na kontach magazynu Azure, wysyłane tooan Azure Event Hub lub wysyłania tooAzure analizy dzienników. Dzienniki diagnostyczne zawierają szczegółowe informacje o kondycji toohello zasobu. Dzienniki diagnostyczne są dostępne dla usługi równoważenia obciążenia (internetowy), grup zabezpieczeń sieci tras i bramy aplikacji. więcej informacji na temat dzienników diagnostycznych odczytu hello toolearn [Przegląd dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Metryki:** metryki są miar wydajności i liczniki zebrane w danym okresie czasu na zasobach. Metryki mogą być używane tootrigger alerty na podstawie progów. Obecnie dostępne dla bramy aplikacji są metryki. więcej informacji na temat metryki odczytu hello toolearn [omówienie metryki](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Rozwiązywanie problemów:** informacje dotyczące rozwiązywania problemów jest dostępny bezpośrednio w hello portalu Azure. informacje Hello ułatwia diagnozowanie typowych problemów z usługi ExpressRoute, Brama sieci VPN bramy aplikacji, dzienniki zabezpieczeń sieci, tras, DNS, usługi równoważenia obciążenia i Menedżera ruchu.
- **Kontrola dostępu oparta na rolach (RBAC):** kontrolowania, kto może utworzyć zasobów i zarządzanie nimi sieci przy użyciu kontroli dostępu opartej na rolach (RBAC). Dowiedz się więcej o RBAC odczytując hello [wprowadzenie RBAC](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu. 
- **Przechwytywania pakietów:** hello obserwatora sieciowego Azure udostępnia usługę hello toorun możliwości przechwytywania pakietów na maszynie Wirtualnej za pomocą rozszerzenia w ramach hello maszyny Wirtualnej. Ta funkcja jest dostępna dla systemów Linux i maszyn wirtualnych systemu Windows. więcej informacji na temat przechwytywania pakietów, przeczytaj hello toolearn [omówienie przechwytywania pakietów](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Sprawdź IP przepływów:** obserwatora sieciowego umożliwia tooverify przepływów IP między maszyny Wirtualnej platformy Azure i toodetermine zasób zdalny czy zezwolono na dostęp lub odmowa pakietów. Ta funkcja daje administratorom możliwość hello tooquickly diagnozowanie problemów z łącznością. toolearn więcej informacji na temat jak przepływa tooverify IP odczytu hello [przepływu IP sprawdzić Przegląd](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Rozwiązywania problemów z połączeniami sieci VPN:** hello do rozwiązywania problemów z sieci VPN z obserwatora sieciowego zapewnia hello tooquery możliwości połączenia lub bramy i sprawdzać kondycję hello hello zasobów. więcej informacji na temat rozwiązywania problemów z połączenia sieci VPN, przeczytaj hello toolearn [połączenie z siecią VPN Rozwiązywanie problemów — omówienie](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Wyświetl topologii sieci:** wyświetlić graficzną reprezentację hello zasobów sieciowych w sieci wirtualnej z obserwatora sieciowego. więcej informacji na temat wyświetlania topologii sieci, przeczytaj hello toolearn [omówienie topologii](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.

## <a name="tools"></a>Wdrażanie i Konfigurowanie narzędzi

Można wdrożyć i skonfigurować zasoby sieci platformy Azure za pomocą dowolnego z hello następujące narzędzia:

- **Portalu Azure:** graficzny interfejs użytkownika uruchomiony w przeglądarce. Otwórz hello [portalu Azure](http://portal.azure.com).
- **Program Azure PowerShell:** wiersza polecenia narzędzia do zarządzania Azure, komputery z systemem Windows. Więcej informacji na temat programu Azure PowerShell za odczytywanie hello [Omówienie programu Azure PowerShell](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Azure interfejsu wiersza polecenia (CLI):** narzędzia wiersza polecenia do zarządzania z komputerów z systemem Linux, macOS lub Windows Azure. Dowiedz się więcej o hello Azure CLI za odczytywanie hello [omówienie interfejsu wiersza polecenia Azure](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- **Szablony usługi Azure Resource Manager:** pliku (w formacie JSON) definiujący hello infrastrukturę i konfigurację rozwiązania Azure. Dzięki szablonowi można wielokrotnie wdrażać rozwiązanie w całym jego cyklu życia z gwarancją spójnego stanu zasobów po każdym wdrożeniu. więcej informacji na temat tworzenia szablonów, przeczytaj hello toolearn [najlepszych rozwiązań dotyczących tworzenia szablonów](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu. Można wdrażać szablony hello portalu Azure, interfejsu wiersza polecenia lub środowiska PowerShell. tooget pracy z szablonami od razu, Wdróż jedne z hello wiele szablonów wstępnie skonfigurowane w hello [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/?term=network) biblioteki. 

## <a name="pricing"></a>Cennik

Niektóre spośród hello Azure usługi sieciowe mają opłat, a inne są wolne. Widok hello [sieci wirtualnej](https://azure.microsoft.com/pricing/details/virtual-network), [bramy sieci VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), [brama aplikacji w](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [modułu równoważenia obciążenia](https://azure.microsoft.com/pricing/details/load-balancer), [obserwatora sieciowego](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager) i [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) cennik strony, aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki

- Tworzenie pierwszej sieci wirtualnej i połączyć kilka tooit maszyn wirtualnych, wykonując kroki hello w hello [tworzenie pierwszej sieci wirtualnej](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- Połącz tooa Twojego komputera sieci wirtualnej, wykonując kroki hello hello [skonfigurować połączenie punkt lokacja](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
- Równoważenie obciążenia serwerów toopublic ruchu internetowych, wykonując kroki hello hello [utworzyć moduł równoważenia obciążenia internetowy](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) artykułu.
