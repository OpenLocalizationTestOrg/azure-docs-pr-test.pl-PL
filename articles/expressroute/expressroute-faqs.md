---
title: "aaaAzure ExpressRoute — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Witaj ExpressRoute — często zadawane pytania zawiera informacje o obsługiwanych usług Azure, kosztów, danych i połączeń, umowy SLA, dostawców i lokalizacje, przepustowości i dodatkowe szczegóły techniczne."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>Usługa ExpressRoute — często zadawane pytania

## <a name="what-is-expressroute"></a>Co to jest ExpressRoute?

ExpressRoute jest usługa Azure, która umożliwia tworzenie prywatnych połączeń między centrach danych firmy Microsoft i infrastrukturę, która jest lokalnie lub w zakładzie wspólnej lokalizacji. Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet i oferty wyższy poziom zabezpieczeń, niezawodności i szybkości pracy zmniejszyć opóźnienia niż typowe połączenia za pośrednictwem hello Internet.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>Jakie są zalety hello programu ExpressRoute, jak i połączeń sieci prywatnej?

Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet. Oferują one wyższej bezpieczeństwa, niezawodności i szybkości pracy, dolnej i spójny opóźnienia niż typowe połączenia za pośrednictwem hello Internet. W niektórych przypadkach przy użyciu danych tootransfer połączeń ExpressRoute między lokalnymi urządzeniami i Azure może spowodować znaczne oszczędności.

### <a name="where-is-hello-service-available"></a>Gdzie jest hello usługi?

Zobacz tę stronę w celu lokalizacji usługi i dostępność: [ExpressRoute partnerów i lokalizacje](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>Jak można użyć ExpressRoute tooconnect tooMicrosoft, jeśli nie mam powiązania z jednym z partnerów operatora ExpressRoute hello?

Można wybrać operator regionalnych i trafić tooone połączenia Ethernet wymiany hello obsługiwanych lokalizacji dostawcy. Następnie można elementu równorzędnego z firmą Microsoft w hello lokalizacji dostawcy. Sprawdź hello ostatniej sekcji [ExpressRoute partnerów i lokalizacje](expressroute-locations.md) toosee Jeśli usługodawca znajduje się w tych lokalizacjach exchange hello. Następnie można zamówić obwodu usługi ExpressRoute za pośrednictwem tooAzure tooconnect dostawcy usługi hello.

### <a name="how-much-does-expressroute-cost"></a>Jaki jest koszt usługi ExpressRoute?

Sprawdź [szczegóły cennika](https://azure.microsoft.com/pricing/details/expressroute/) uzyskać informacje o cenach.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>Jeśli będę płacić dla obwodu usługi ExpressRoute danego przepustowości, hello połączenia sieci VPN, które można kupić z usługodawcą sieci ma toobe hello samej szybkości?

Nie. Połączenia sieci VPN, o dowolnym szybkości możesz kupić od dostawcy usług. TooAzure Twojego połączenia jest jednak ograniczona toohello przepustowości obwodu ExpressRoute, zakupu.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>Jeśli opłacać obwodu usługi ExpressRoute danego przepustowości należy hello możliwości tooburst się szybkości toohigher w razie potrzeby?

Tak. Obwody usługi ExpressRoute są skonfigurowane tooallow tooburst się razy tootwo hello limit przepustowości, który został uzyskany dla bez dodatkowych kosztów. Skontaktuj się z Twojego toosee dostawcy usługi, które obsługują tę możliwość.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>Można użyć hello połączenia z siecią wirtualną i innych usług Azure sam prywatnej sieci jednocześnie?

Tak. Obwodu usługi ExpressRoute, gdy zostanie ustawiona, można tooaccess usług sieci wirtualnej i innych usług Azure jednocześnie. Połączenia sieci toovirtual za pośrednictwem ścieżki prywatnej komunikacji równorzędnej hello i usług tooother odbywa się za pośrednictwem publicznej komunikacji równorzędnej ścieżki hello.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>ExpressRoute oferuje Umowa dotycząca poziomu usług (SLA)?

Aby uzyskać informacje, zobacz hello [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) strony.

## <a name="supported-services"></a>Obsługiwane usługi

Obsługuje ExpressRoute [trzy domeny routingu](expressroute-circuit-peerings.md) dla różnych typów usług.

### <a name="private-peering"></a>Prywatna komunikacja równorzędna

* Sieci wirtualne, w tym wszystkie maszyny wirtualne i usługi w chmurze

### <a name="public-peering"></a>Publiczna komunikacja równorzędna

* Power BI
* Dynamics 365 Finanse i operacji (wcześniej znane jako Dynamics AX Online)
* Większość hello Azure usługi z powitania po kilka wyjątków:
  * CDN
  * Visual Studio Team Services testów obciążenia
  * Multi-Factor Authentication
  * Traffic Manager

### <a name="microsoft-peering"></a>Komunikacja równorzędna firmy Microsoft

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Dynamics 365 zaangażowanie klientów aplikacji (wcześniej znane jako CRM Online)
  * Dynamics 365 sprzedaży
  * Dynamics 365 dla klientów usługi
  * Dynamics 365 usługi pola
  * Dynamics 365 usługi projektu

## <a name="data-and-connections"></a>Dane i połączeń

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>Czy istnieją ograniczenia dotyczące hello ilość danych, które można przenosić za pomocą usługi ExpressRoute?

Nie możemy ustawić limit na powitania wielkości transferu danych. Odwołuje się zbyt[szczegóły cennika](https://azure.microsoft.com/pricing/details/expressroute/) informacji o szybkości przepustowości.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Szybkość połączenia, które są obsługiwane przez usługi ExpressRoute?

Obsługiwane oferty przepustowości:

50 Mb/s, 100 Mb/s, 200 Mb/s, 500 Mb/s, 1 Gb/s, 2 Gb/s, 5 Gb/s, 10 Gb/s

### <a name="which-service-providers-are-available"></a>Dostawcy usług, które są dostępne?

Zobacz [ExpressRoute partnerów i lokalizacje](expressroute-locations.md) hello listy usługodawców i lokalizacji.

## <a name="technical-details"></a>Szczegóły techniczne

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>Jakie są wymagania techniczne hello podłączania Mój tooAzure lokalizacji lokalnej?

Zobacz [strony wymagania wstępne usługi ExpressRoute](expressroute-prerequisites.md) wymagania.

### <a name="are-connections-tooexpressroute-redundant"></a>Czy nadmiarowe tooExpressRoute połączenia?

Tak. Każdy obwód usługi ExpressRoute ma parę nadmiarowych cross połączeń skonfigurowanych tooprovide wysokiej dostępności.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>Łączność zostaną utracone w przypadku awarii jednego łącza ExpressRoute?

Nie nastąpi utrata połączenia, jeśli jeden z hello cross połączenia kończy się niepowodzeniem. Nadmiarowe połączenie jest dostępne toosupport hello obciążenia sieci. Ponadto można tworzyć wiele obwodów w różnych komunikacji równorzędnej lokalizacji tooachieve odporność na awarie.

### <a name="onep2plink"></a>Jeśli nie mam umieszczonych w chmurze programu exchange i usługodawcą oferuje połączeniem, należy tooorder dwóch fizycznego połączenia między Moja sieć lokalną i firmy Microsoft?

Jeśli usługodawca może nawiązać dwie wirtualne obwody Ethernet za pośrednictwem połączenia fizycznego hello, wystarczy tylko jedno połączenie fizyczne. Witaj fizycznych połączenie (na przykład, światłowód) zostało zakończone w warstwie 1 urządzenia (L1) (zobacz obraz powitania). oznakowane obwodów wirtualnych Witaj dwie sieci Ethernet z różnych identyfikatorów sieci VLAN, jeden dla obwodu głównej hello i jedną dla hello dodatkowej. Te identyfikatory sieci VLAN są w nagłówku Ethernet hello 802.1Q zewnętrzne. Nagłówek Ethernet Hello wewnętrznego standardu 802.1Q (tego nie pokazano) jest mapowanych tooa określonych [domeny routingu usługi ExpressRoute](expressroute-circuit-peerings.md).

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>Rozszerzenie jest jedną z mojej tooAzure sieci VLAN za pomocą usługi ExpressRoute można?

Nie. Warstwy 2 łączności rozszerzenia nie jest obsługiwana na platformie Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>Czy można mieć więcej niż jeden obwód usługi ExpressRoute w mojej subskrypcji?

Tak. Może mieć więcej niż jeden obwód usługi ExpressRoute w ramach subskrypcji. Witaj domyślny limit wynosi too10. W razie potrzeby można skontaktować się Microsoft Support tooincrease hello limitu.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>Czy można mieć obwody usługi ExpressRoute z innego usługodawcy.

Tak. Może mieć obwody usługi ExpressRoute z wielu usługodawców. Każdy obwód usługi ExpressRoute, jest skojarzona z tylko jedną usługę dostawcy. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>Czy można mieć wiele obwody usługi ExpressRoute w hello tej samej lokalizacji?

Tak. Można mieć wiele obwody usługi ExpressRoute, z hello takie same lub innego usługodawcy w hello tej samej lokalizacji. Jednak nie można połączyć więcej niż jeden toohello obwodu ExpressRoute sam wirtualnych sieci z hello sam lokalizacji.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>Jak połączyć Mój tooan sieci wirtualnych obwodu ExpressRoute

podstawowe kroki Hello są:

* Ustanów obwodu usługi ExpressRoute i dostawcy usług hello ją włączyć.
* Użytkownik lub dostawcy hello, należy skonfigurować hello komunikacji równorzędnej BGP (s).
* Połącz obwodu ExpressRoute toohello hello w sieci wirtualnej.

Aby uzyskać więcej informacji, zobacz [przepływy pracy usługi ExpressRoute dla aprowizacji obwodów i stanów obwodów](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>Czy istnieją granice łączności dla obwód usługi ExpressRoute?

Tak. Witaj [ExpressRoute partnerów i lokalizacje](expressroute-locations.md) artykuł zawiera omówienie hello łączności granic dla obwodu usługi ExpressRoute. Łączność dla obwodu usługi ExpressRoute jest pojedynczym regionie geograficznymi tooa ograniczone. Łączność może być rozwinięty toocross geograficznymi regionów przez włączenie funkcji premium ExpressRoute hello.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>Czy można połączyć toomore niż jedną sieć wirtualną tooan obwodu ExpressRoute?

Tak. Może mieć too10 połączenia sieci wirtualnych na standardowe obwodu ExpressRoute oraz too100 [obwodu ExpressRoute premium](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>Masz wiele subskrypcji Azure, zawierające sieci wirtualnych. Czy można połączyć sieci wirtualnych, które znajdują się w oddzielnych subskrypcje tooa pojedynczego obwodu ExpressRoute?

Tak. Można autoryzować się too10 toouse innych subskrypcji platformy Azure pojedynczego obwodu usługi expressroute. Przez włączenie funkcji premium ExpressRoute hello można zwiększyć ten limit.

Aby uzyskać więcej informacji, zobacz [udostępnianie obwodu usługi ExpressRoute między wieloma subskrypcjami](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>Czy toohello połączonych sieci wirtualnych tego samego obwodu izolowane od siebie?

Nie. Z routingu toohello połączonego perspektywy, wszystkie wirtualne sieci tego samego obwodu ExpressRoute są częścią tej samej domenie routingu hello i nie są od siebie odizolowane. Należy rozesłać izolacji, należy najpierw toocreate oddzielne obwodu usługi expressroute.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>Czy można mieć jeden toomore połączone sieci wirtualnej niż jeden obwód usługi ExpressRoute

Tak. Możesz połączyć pojedynczy sieć wirtualną z zapasowej toofour obwody usługi ExpressRoute. Musi zostać określona przez cztery różne [lokalizacje ExpressRoute](expressroute-locations.md).

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>Można uzyskać dostęp hello Internet z mojej obwody tooExpressRoute połączonych sieci wirtualnych?

Tak. Jeśli ma nie anonsowane trasy domyślne (0.0.0.0/0) lub prefiksy trasy Internet za pośrednictwem sesji BGP hello, możesz połączyć toohello Internetu z sieci wirtualnej połączone tooan obwodu usługi expressroute.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>Czy można zablokować Internet łączności toovirtual sieci połączonych tooExpressRoute obwody?

Tak. Może anonsować domyślne trasy (0.0.0.0/0) tooblock wszystkie maszyny toovirtual połączenie internetowe wdrożyć w ramach sieci wirtualnej i rozsyłać cały ruch się za pośrednictwem hello obwodu ExpressRoute.

Jeśli anonsują tras domyślnych, możemy wymusić tooservices ruchu oferowane za pośrednictwem publicznej komunikacji równorzędnej (takie jak usługa Azure storage i bazy danych SQL) lokalne tooyour Wstecz. Konieczne będzie tooconfigure Twojego routery tooreturn ruchu tooAzure za pośrednictwem publicznej komunikacji równorzędnej ścieżki hello lub hello Internet.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>Można toohello połączone sieci wirtualnych tego samego obwodu ExpressRoute porozmawiać tooeach innych?

Tak. Maszyn wirtualnych wdrożonych w toohello połączonych sieci wirtualnych, które samego obwodu ExpressRoute może komunikować się ze sobą.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>Dla sieci wirtualnych w połączeniu z ExpressRoute można używać połączenia lokacja lokacja?

Tak. ExpressRoute może współistnieć z sieci VPN typu lokacja lokacja.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>Można przenieść sieć wirtualną z toouse site-to-site / punkt lokacja konfiguracji usługi ExpressRoute?

Tak. Konieczne będzie toocreate bramę usługi ExpressRoute w ramach sieci wirtualnej. Brak małych przestoju, związane z procesem hello.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>Dlaczego jest publiczny adres IP skojarzone z hello bramę usługi ExpressRoute w sieci wirtualnej

Hello publiczny adres IP jest używana tylko wewnętrzny zarządzania. Ten publiczny adres IP nie jest narażonych toohello Internet i nie stanowi zagrożenie bezpieczeństwa, sieci wirtualnych.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>Czego potrzebuję tooconnect tooAzure magazynu za pośrednictwem usługi ExpressRoute?

Należy ustanowić obwodu usługi ExpressRoute i skonfigurować tras dla publicznej komunikacji równorzędnej.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>Czy istnieją ograniczenia dotyczące liczby hello I może anonsować tras?

Tak. Możemy zaakceptować too4000 prefiksy tras dla prywatnej komunikacji równorzędnej i 200 dla publicznej komunikacji równorzędnej i komunikacji równorzędnej firmy Microsoft. Można zwiększyć ten too10 000 tras dla prywatnej komunikacji równorzędnej po włączeniu funkcji premium ExpressRoute hello.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>Czy istnieją ograniczenia dotyczące zakresów adresów IP I może anonsować hello sesji protokołu BGP?

Firma Microsoft nie akceptują prywatnej prefiksy (RFC1918) hello publicznego i Microsoft komunikacji równorzędnej BGP sesji.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>Co się stanie, jeśli I przekraczają limity BGP hello?

Sesje BGP zostanie usunięty. One zostaną zresetowane, gdy liczba prefiks hello przechodzi poniżej limitu hello.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>Co to jest hello czas przechowywania BGP usługi ExpressRoute? Czy można je dostosować?

czas wstrzymania Hello jest 180. wiadomości powitania od keep-alive są wysyłane co 60 sekund. Te określone ustawienia są na powitania po stronie firmy Microsoft, nie można jej zmienić. Można automatycznie czasomierze różnych tooconfigure i parametry sesji BGP hello będzie odpowiednio negocjowane.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>Po I anonsowanie sieci wirtualnych toomy hello domyślne trasy (0.0.0.0/0), nie można aktywować systemu Windows na moich maszynach wirtualnych platformy Azure. Jak tooI rozwiązać ten problem?

rozpoznaje żądanie aktywacji hello Azure pomocy w Hello następujące kroki:

1. Ustanów hello publicznej komunikacji równorzędnej dla obwodu usługi ExpressRoute.
2. Wyszukiwania DNS i znaleźć adres IP hello **kms.core.windows.net**
3. Witaj usługi zarządzania kluczami musi rozpoznać tej hello żądanie aktywacji pochodzi z platformy Azure i honoruj hello żądania. Wykonaj jedną z następujących trzech zadań hello:

   * W sieci lokalnej kierować ruchem hello przeznaczonych dla hello adres IP, który został uzyskany w kroku 2 tooAzure wstecz za pośrednictwem publicznej komunikacji równorzędnej hello.
   * Mieć Twoje NSP dostawcy hello numeru pin włosów ruchu wstecz tooAzure za pośrednictwem publicznej komunikacji równorzędnej hello.
   * Utworzenie trasy zdefiniowanej przez użytkownika tego adresu IP hello punktów, z Internetu, jako następnego przeskoku i zastosować je toohello adresy podsieci używane, gdy te maszyny wirtualne są.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Czy można zmienić hello przepustowości obwodu ExpressRoute?

Tak, możesz spróbować tooincrease hello przepustowość obwodu usługi ExpressRoute w hello portalu Azure lub za pomocą programu PowerShell. Brak dostępnej pojemności na powitania fizyczny port, na którym utworzono obwodu, zmiany zakończy się pomyślnie. 

Jeśli ta zmiana nie powiedzie się, oznacza to, albo nie jest dostępna wystarczająca pojemność na powitania bieżącego portu i potrzebujesz toocreate nowego obwodu usługi expressroute z większej przepustowości hello, lub gdy w tej lokalizacji nie ma żadnych dodatkowych pojemności, w tym przypadku nie będzie można tooincrease hello przepustowość. 

Ponadto mają toofollow z Twojego tooensure dostawcy łączności zaktualizowania limity hello w ich podwyższanie przepustowości sieci toosupport hello. Nie można jednak zmniejszyć hello przepustowość obwodu usługi ExpressRoute. Masz toocreate nowego obwodu usługi expressroute z mniejszej przepustowości sieci i Usuń stare obwodu hello.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Jak zmienić hello przepustowości obwodu ExpressRoute?

Można aktualizować hello przepustowości obwodu ExpressRoute hello przy użyciu polecenia cmdlet interfejsu API REST lub programu PowerShell hello.

## <a name="expressroute-premium"></a>ExpressRoute — wersja premium

### <a name="what-is-expressroute-premium"></a>Co to jest w wersji premium ExpressRoute?

ExpressRoute — wersja premium jest kolekcją hello następujące funkcje:

* Zwiększyć limit tabeli routingu z 4000 too10 tras, 000 tras dla prywatnej komunikacji równorzędnej.
* Większa liczba sieci wirtualnych, które mogą być połączone toohello obwodu ExpressRoute (wartość domyślna to 10). Aby uzyskać więcej informacji, zobacz hello [limity ExpressRoute](#limits) tabeli.
* Łączność tooOffice 365 i Dynamics 365.
* Globalne łączność za pośrednictwem sieci podstawowej Microsoft hello. Teraz możesz połączyć sieć wirtualną w jednym regionie geograficznymi z obwodu usługi ExpressRoute w innym regionie.<br>
    **Przykłady:**

    *  Możesz połączyć utworzony w tooan Europa Zachodnia obwodu ExpressRoute utworzone w Dolinie Krzemowej sieci wirtualnej. 
    *  Na powitania publicznej komunikacji równorzędnej, prefiksy z innych regionów geograficznymi są rozgłaszane w taki sposób, że można nawiązać, na przykład SQL Azure w Europie zachodnie z obwodem w Dolinie Krzemowej.


### <a name="limits"></a>Jak wiele sieci wirtualnych można łączyć obwodu ExpressRoute tooan włączenie ExpressRoute premium?

Witaj w poniższych tabelach hello limity ExpressRoute i hello liczba sieci wirtualnych na obwodu ExpressRoute:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>Jak włączyć ExpressRoute premium?

ExpressRoute funkcji premium można włączyć, gdy jest włączona funkcja hello i może zostać wyłączony, aktualizując hello stanu obwodu. Możesz włączyć w czasie tworzenia obwodu ExpressRoute — wersja premium lub można wywołać interfejsu API REST hello / polecenia cmdlet programu PowerShell.

### <a name="how-do-i-disable-expressroute-premium"></a>Jak wyłączyć ExpressRoute premium?

Wywołując hello interfejsu API REST lub programu PowerShell polecenia cmdlet, można wyłączyć premium usługi ExpressRoute. Należy się upewnić, mają skalować z łączności potrzeb toomeet hello domyślne limity przed wyłączeniem premium usługi ExpressRoute. Jeśli Twoje użycie skaluje poza hello domyślne limity, hello żądania toodisable ExpressRoute w warstwie premium nie powiedzie się.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>Można można wybrać funkcje hello, interesujące z zestawem funkcji premium hello?

Nie. Nie można wybrać funkcje hello. Po włączeniu premium usługi ExpressRoute włączyć wszystkie funkcje.

### <a name="how-much-does-expressroute-premium-cost"></a>Jaki jest koszt premium ExpressRoute?

Odwołuje się zbyt[szczegóły cennika](https://azure.microsoft.com/pricing/details/expressroute/) kosztów.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>Będę płacić za ExpressRoute premium dodatkowo toostandard opłat ExpressRoute?

Tak. ExpressRoute premium opłaty na górze obciążenia obwodu ExpressRoute i obciążeń, wymagane przez dostawcę łączności hello.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>Usługi dla usługi Office 365 i Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>Jak utworzyć tooconnect obwodu ExpressRoute tooOffice 365 usług i Dynamics 365?

1. Przejrzyj hello [strony wymagania wstępne usługi ExpressRoute](expressroute-prerequisites.md) toomake się, że spełniają wymagania hello.
2. tooensure wymagające łączność są spełnione, zapoznaj się z listą hello usługodawców i lokalizacje w hello [ExpressRoute partnerów i lokalizacje](expressroute-locations.md) artykułu.
3. Planowanie wymagań dotyczących pojemności, przeglądając [Planowanie sieci i dostrajania wydajności dla usługi Office 365](http://aka.ms/tune/).
4. Wykonaj kroki hello na liście tooset przepływy pracy hello zapasowej łączności [przepływy pracy usługi ExpressRoute dla aprowizacji obwodów i stanów obwodów](expressroute-workflows.md).

> [!IMPORTANT]
> Upewnij się, czy włączono dodatek usługi ExpressRoute w warstwie premium w przypadku konfigurowania usług tooOffice 365 łączności i Dynamics 365.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>Należy tooenable Azure publicznej komunikacji równorzędnej tooconnect tooOffice 365 usług i Dynamics 365?

Nie, wystarczy tooenable Peering firmy Microsoft. TooAzure ruchu uwierzytelniania AD są wysyłane za pośrednictwem Peering firmy Microsoft. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>Mój istniejący obwody usługi ExpressRoute obsługują usług 365 tooOffice łączności i Dynamics 365?

Tak. Istniejącym obwodem usługi expressroute może być skonfigurowany toosupport usług 365 tooOffice łączności. Upewnij się, że masz wystarczającą pojemność tooconnect tooOffice 365 usług i włączono dodatek w warstwie premium. [Planowanie sieci i dostrajania wydajności dla usługi Office 365](http://aka.ms/tune/) musi pomaga zaplanować łączność. Zobacz też [tworzenia i modyfikowania obwodu usługi expressroute](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>Jakie usługi Office 365, usług jest dostępna za pośrednictwem połączenia ExpressRoute?

Odwołuje się zbyt[zakresów adresów IP i URL usługi Office 365](http://aka.ms/o365endpoints) strony aktualną listę usług obsługiwanych przez usługi ExpressRoute.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Ile kosztuje ExpressRoute dla usług Office 365 i Dynamics 365 kosztów?

Usługi Office 365 i Dynamics 365 wymagają toobe dodatek premium włączone. Zobacz hello [cennikiem szczegóły](https://azure.microsoft.com/pricing/details/expressroute/) kosztów.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>W jakich regionach jest obsługiwana ExpressRoute dla usługi Office 365?

Zobacz [ExpressRoute partnerów i lokalizacje](expressroute-locations.md) informacji.

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>Można uzyskać dostęp do usługi Office 365 za pośrednictwem hello Internet, nawet jeśli ExpressRoute został skonfigurowany dla mojej organizacji?

Tak. Punkty końcowe programu Office 365 usługi są dostępny za pośrednictwem hello Internet, nawet jeśli skonfigurowano usługi ExpressRoute w sieci. Jeśli w lokalizacji, która jest skonfigurowany tooconnect tooOffice 365 usługi ExpressRoute, będzie łączyć się za pośrednictwem usługi ExpressRoute.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Można uzyskać dostęp do usług Office 365 instytucji rządowych Stanów Zjednoczonych społeczności (GCC) za pośrednictwem usługi Azure instytucji rządowych USA obwodu usługi ExpressRoute?

Tak. Punkty końcowe usługi GCC usługi Office 365 są dostępne za pośrednictwem hello Azure instytucji rządowych USA ExpressRoute. Jednak możesz pierwszy potrzeby tooopen bilet pomocy technicznej na hello mają tooadvertise tooMicrosoft prefiksy hello tooprovide portalu Azure. Po usunięciu biletu pomocy technicznej hello zostanie nawiązane połączenie tooOffice 365 GCC usług. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>365 Dynamics dla operacji (wcześniej znane jako Dynamics AX Online) jest dostępna za pośrednictwem połączenia ExpressRoute?

Tak. [Dynamics 365 operacjach](https://www.microsoft.com/dynamics365/operations) jest hostowana na platformie Azure. Można włączyć publicznej komunikacji równorzędnej platformy Azure na Twojej tooit tooconnect obwodu usługi ExpressRoute.

## <a name="route-filters-for-microsoft-peering"></a>Filtry trasy dla komunikacji równorzędnej firmy Microsoft

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>Am I włączenie komunikacji równorzędnej firmy Microsoft dla powitania po raz pierwszy, jakie trasy zobaczą?

Nie będą widzieć żadnych trasy. Masz tooattach anonsów tras filtru tooyour obwodu toostart prefiks. Aby uzyskać instrukcje, zobacz [Konfigurowanie filtrów trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>I włączony komunikacji równorzędnej firmy Microsoft i teraz jestem w trakcie tooselect usługi Exchange Online, ale jego nadanie mnie wystąpił błąd, że nie mam autoryzowanych toodo go.

Podczas korzystania z filtrów tras, każdy klient można włączyć w komunikacji równorzędnej firmy Microsoft. Jednak służący do konsumowania usługi Office 365, nadal należy tooget uprawnień przez usługę Office 365.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>Należy autoryzacji tooget włączania Dynamics 365 za pośrednictwem komunikacji równorzędnej firmy Microsoft?

Nie, nie trzeba autoryzacji dla usługi Dynamics 365. Można utworzyć regułę, a następnie wybierz społeczności Dynamics 365 bez autoryzacji.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>Mam już komunikacji równorzędnej firmy Microsoft, jak możliwość korzystania z filtrów tras?

Można utworzyć filtr trasy, wybierz hello usług toouse, a następnie dołączyć hello komunikacji równorzędnej firmy Microsoft tooyour filtru. Aby uzyskać instrukcje, zobacz [Konfigurowanie filtrów trasy dla komunikacji równorzędnej firmy Microsoft](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>Mam Microsoft równorzędna w jednej lokalizacji, w obecnie próbuję tooenable ją w innej lokalizacji, a nie widzę żadnych prefiksów.

* Komunikacji równorzędnej firmy Microsoft z obwody usługi ExpressRoute, które zostały skonfigurowane wcześniejsze tooAugust 1, 2017 ma wszystkie prefiksy usługi anonsowane za pomocą komunikacji równorzędnej firmy Microsoft, nawet jeśli nie zdefiniowano filtrów trasy.

* Z obwody usługi ExpressRoute, które są skonfigurowane na lub po 1 sierpnia 2017 komunikacji równorzędnej firmy Microsoft nie będzie miał wszystkie prefiksy anonsowane, dopóki nie zostanie podłączone filtr tras toohello obwodu. Prefiksy nie będą widzieć domyślnie.
