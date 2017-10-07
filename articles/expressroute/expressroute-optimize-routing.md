---
title: "Optymalizacja routingu usługi ExpressRoute: Azure| Microsoft Docs"
description: "Ta strona zawiera szczegóły dotyczące sposobu toooptimize routingu, jeśli masz więcej niż jeden ExpressRoute obwody który połączenia między firmą Microsoft a corp sieci."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>Optymalizacja routingu usługi ExpressRoute
Jeśli masz wiele obwody usługi ExpressRoute, masz więcej niż jeden tooMicrosoft tooconnect ścieżki. W związku z tym nieoptymalne routingu może się tak zdarzyć - oznacza to, że ruchu może potrwać dłużej tooreach ścieżka firmy Microsoft i sieci tooyour firmy Microsoft. Witaj dłużej hello ścieżki sieciowej, większego opóźnienia hello hello. Opóźnienie ma bezpośredni wpływ na wydajność aplikacji i środowisko użytkownika. W tym artykule zilustrować ten problem, a także opisano, jak toooptimize routingu przy użyciu hello standardowych technologii routingu.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>Nieoptymalne routingu z tooMicrosoft klienta
Spójrzmy Zamknij na powitania problem routingu za przykład. Załóżmy, że masz dwie oddziałów w hello USA, drugi w Gdańsku, a drugi w Nowym Jorku. Biura są połączone za pośrednictwem sieci WAN, która może być Twoją siecią podstawową lub siecią IP VPN dostawcy usług. Masz dwie obwody usługi ExpressRoute, jeden Indie Zachodnie nam i jeden w nam wschodnie, które także są połączone w sieci WAN hello. Oczywiście masz dwie ścieżki tooconnect toohello sieci firmy Microsoft. Teraz wyobraź sobie, że dysponujesz wdrożeniem platformy Azure (np. usługą Azure App Service) zarówno w zachodnich, jak i wschodnich stanach USA. Masz zamiar jest tooconnect użytkowników w Warszawie tooAzure nam Zachodnia, jak i użytkowników w Nowym Jorku tooAzure nam wschodnie, ponieważ administrator usługi służy do anonsowania, że użytkowników w każdej office access hello w pobliżu usług platformy Azure dla środowiska optymalne. Niestety hello plan działa dobrym rozwiązaniem dla użytkowników wschodniego hello, ale nie dla hello zachodnie wybrzeże użytkowników. Witaj przyczyną problemu hello jest hello poniżej. Obwód usługi ExpressRoute możemy anonsują tooyou zarówno prefiks hello w Azure nam wschodnie (23.100.0.0/16) i prefiksu hello w Azure nam zachodnie (13.100.0.0/16). Jeśli nie wiesz, które prefiks jest w danym regionie, nie masz tootreat może on inaczej. Sieci WAN może wziąć pod uwagę zarówno prefiksy hello są bliższe wschód tooUS niż zachodnie nam i w związku z tym trasy toohello użytkownicy obu office obwodu usługi expressroute w nam wschodnie. W celu hello będziesz mieć wielu użytkowników niezadowolonych hello Gdańsku pakietu office.

![Problem ExpressRoute przypadek 1 - nieoptymalne routingu z tooMicrosoft klienta](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Rozwiązanie: użyj społeczności BGP
toooptimize routingu dla obu użytkowników pakietu office, należy tooknow prefiks, który pochodzi z Azure nam Zachodnia, które z Azure nam wschodnie. Kodujemy te informacje przy użyciu [wartości społeczności BGP](expressroute-routing.md). Firma Microsoft przypisane unikatowe tooeach wartość społeczności BGP regionu Azure, np. „12076:51004” dla wschodnich, a „12076:51006” dla zachodnich stanów USA. Skoro już wiesz, który prefiks odpowiada któremu regionowi świadczenia usługi Azure, możesz skonfigurować preferowany obwód usługi ExpressRoute. Ponieważ używamy informacje routingu tooexchange BGP hello, można użyć protokołu BGP w lokalnym preferencji tooinfluence routingu. W naszym przykładzie można przypisać wyższej too13.100.0.0/16 wartość preferencji lokalnego Indie Zachodnie nam niż w nam wschodnie i podobnie wyższej too23.100.0.0/16 wartość preferencji lokalnego w nam wschodnie niż Indie Zachodnie NAS. Ta konfiguracja będzie upewnij się, po obu tooMicrosoft ścieżki są dostępne, użytkownikom w Warszawie będzie trwać hello obwodu usługi expressroute w tooAzure tooconnect zachodnie nam nam zachodnie użytkowników w Nowym Jorku podjąć hello ExpressRoute w tooAzure nam wschodnie nam wschodnie . Routing jest zoptymalizowany po obu stronach. 

![Rozwiązanie przypadku 1 dotyczącego usługi ExpressRoute — używanie społeczności BGP](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> Witaj tę samą metodę, przy użyciu lokalnego preferencji, może być zastosowane toorouting z klienta tooAzure sieci wirtualnej. Nie możemy tagu prefiksy toohello wartość społeczności BGP anonsowane z sieci tooyour platformy Azure. Jednak ponieważ wiadomo, które wdrożenia sieci wirtualnej jest Zamknij toowhich z pakietu office, można skonfigurować routery odpowiednio tooprefer jeden tooanother obwodu usługi ExpressRoute.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Nieoptymalne routingu z toocustomer firmy Microsoft
Oto inny przykład gdzie połączenia od firmy Microsoft trwać dłużej tooreach ścieżki sieci. W tym przypadku używasz lokalnych serwerów programu Exchange i usługi Exchange Online w [środowisku hybrydowym](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx). Biura są tooa połączenia sieci WAN. Ogłosić prefiksy hello serwerów lokalnych w obu tooMicrosoft Twojego oddziałów za pośrednictwem hello dwa obwody usługi ExpressRoute. Exchange Online spowoduje zainicjowanie połączenia toohello lokalnych serwerów w przypadkach, takich jak migracja skrzynki pocztowej. Niestety tooyour połączenia hello Gdańsku office jest routingiem toohello obwodu usługi expressroute w nam wschodnie przed przechodzenie hello całego kontynencie toohello wstecz zachodnie wybrzeże. Witaj przyczyną problemu hello jest podobne toohello pierwszy z nich. Bez żadnych wskazówki sieci firmy Microsoft hello nie wiadomo, które prefiks klienta jest Zamknij tooUS Wschodnia i która z nich zamknąć tooUS zachodnie. Zdarza się toopick hello nieprawidłowy tooyour office w Gdańsku.

![ExpressRoute przypadku 2 - nieoptymalne routingu z toocustomer firmy Microsoft](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Rozwiązanie: użyj dołączania ścieżki AS
Istnieją dwa rozwiązania toohello problem. Witaj najpierw jeden jest po prostu anonsowanie prefiksu użytkownika lokalnego dla pakietu office Gdańsku 177.2.0.0/31 obwodu ExpressRoute hello Indie Zachodnie nam oraz lokalnej prefiks dla pakietu office z nowego Jorku, 177.2.0.2/31 obwodu ExpressRoute hello w nam wschodnie. W związku z tym jest tylko jedną ścieżkę dla Microsoft tooconnect tooeach biur. Nie ma żadnych niejednoznaczności i routing zostaje zoptymalizowany. Ten projekt należy toothink o strategii trybu failover. W hello zdarzenie, które hello tooMicrosoft ścieżkę za pośrednictwem usługi ExpressRoute został przerwany, konieczne toomake się, że usługi Exchange Online można nadal tooyour serwerów lokalnych. 

drugim rozwiązaniem Hello jest nadal tooadvertise zarówno prefiksy hello na obu obwody usługi ExpressRoute, czy dodatkowo możesz Przekaż nam wskazówkę prefiks, który jest toowhich Zamknij jedną biur. Ponieważ firma Microsoft obsługuje dołączanie ścieżki AS protokołu BGP, można skonfigurować hello ścieżki AS routingu tooinfluence prefiks. W tym przykładzie możesz zwiększyć hello ścieżki AS dla 172.2.0.0/31 w nam wschodnie tak, aby firma Microsoft preferowane obwodu ExpressRoute hello Indie Zachodnie nam na ruch kierowany do tego prefiksu (zgodnie z naszej sieci będą wydaje się, że prefiks toothis ścieżka hello jest krótszy, Indie Zachodnie hello). Podobnie można wydłużyć hello ścieżki AS dla 172.2.0.2/31 Indie Zachodnie nam tak, aby firma Microsoft będzie preferowane hello obwodu usługi expressroute w nam wschodnie. Routing zostaje zoptymalizowany dla obu biur. W tym projekcie jeśli jeden obwód usługi ExpressRoute zostanie uszkodzony, usługa Exchange Online może nadal uzyskać dostęp do użytkownika za pośrednictwem innego obwodu usługi ExpressRoute i sieci WAN. 

> [!IMPORTANT]
> Usuwamy prywatnych numerów hello ścieżki AS dla prefiksów hello ODBIERANE na Peering firmy Microsoft. Należy tooappend publicznego jako liczby w hello ścieżki AS tooinfluence routingu dla Peering firmy Microsoft.
> 
> 

![Rozwiązanie przypadku 2 dotyczącego usługi ExpressRoute — używanie dołączania ścieżki AS](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Gdy hello podanych tutaj przykładów dla firmy Microsoft i publicznej komunikacji równorzędnych, firma Microsoft obsługuje hello takie same możliwości dla prywatnej komunikacji równorzędnej hello. Dołączanie ścieżki AS hello działa także w jeden pojedynczy obwodu ExpressRoute, wybór hello tooinfluence hello ścieżki podstawowego i pomocniczego.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Suboptymalny routing między sieciami wirtualnymi
Z usługi ExpressRoute, można włączyć tooVirtual sieci wirtualnej sieci (co jest także znana jako "Sieci wirtualnej") komunikację przez łączenie ich tooan obwodu ExpressRoute. Łącząc je toomultiple obwody usługi ExpressRoute, routing nieoptymalne może nastąpić między hello sieci wirtualnych. Rozważmy przykład. Dostępne są dwa obwody usługi ExpressRoute: jeden w zachodnich stanach USA i jeden we wschodnich stanach USA. W każdym regionie znajdują się dwie sieci wirtualne. Serwerów sieci web są wdrażane w jednej sieci wirtualnej i serwerów aplikacji w hello innych. W celu zapewnienia nadmiarowości łącze Witaj dwie sieci wirtualne w każdy region tooboth hello lokalnego obwodu usługi expressroute i hello zdalnego obwodu usługi expressroute. Jak są widoczne poniżej, w każdej sieci wirtualnej istnieją dwie ścieżki toohello innych sieci wirtualnej. Hello sieci wirtualne nie wiadomo, które obwodu ExpressRoute jest lokalny, a które z nich jest zdalny. W związku z tym tak samo, jak routingu ruchu między sieciami wirtualnymi saldo tooload równości-koszt-Multi-Path (ECMP), niektóre przepływy ruchu potrwa hello dłuższe ścieżki i pobrać kierowane na powitania zdalnego obwodu ExpressRoute.

![Przypadek 3 dotyczący usługi ExpressRoute — suboptymalny routing między sieciami wirtualnymi](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>Rozwiązanie: przypisywanie połączenia toolocal wysokiej wagi
rozwiązanie Hello jest proste. Ponieważ wiadomo, gdzie obwody sieci wirtualnych i hello hello są, chcesz nam powiedzieć których ścieżka powinna preferowane każdej sieci wirtualnej. W szczególności w tym przykładzie należy przypisać wyższe wagi toohello połączenie lokalne niż toohello połączenia zdalnego (Zobacz przykład konfiguracji hello [tutaj](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Prefiks hello hello odebrania sieci wirtualnej innych sieci wirtualnej na wiele połączeń go preferowane hello połączenia z hello najwyższej wagi toosend ruch kierowany do tego prefiksu.

![Rozwiązanie ExpressRoute przypadku 3 - przypisać wagi wysokiej toolocal połączenia](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> Można również wpływ routingu w sieci lokalnej tooyour sieci wirtualnej, jeśli masz wiele obwody usługi ExpressRoute, konfigurując wagi hello połączenia zamiast stosować ścieżki AS dołączanie techniki opisane w hello drugi scenariusz powyżej. Dla każdego prefiksu zawsze zajmiemy hello wagi połączenia przed hello długość ścieżki AS podczas podejmowania decyzji o sposobie toosend ruchu.
>
>
