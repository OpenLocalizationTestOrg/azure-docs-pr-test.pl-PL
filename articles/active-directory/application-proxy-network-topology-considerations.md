---
title: "zagadnienia dotyczące topologii aaaNetwork przy użyciu serwera Proxy usługi Azure Active Directory aplikacji | Dokumentacja firmy Microsoft"
description: "Obejmuje zagadnienia dotyczące topologii sieci, używając serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Zagadnienia dotyczące topologii sieci przy użyciu serwera Proxy usługi Azure Active Directory aplikacji

W tym artykule opisano zagadnienia dotyczące topologii sieci, podczas publikowania i zdalny dostęp do aplikacji przy użyciu serwera Proxy aplikacji usługi Azure Active Directory (Azure AD).

## <a name="traffic-flow"></a>Przepływ ruchu

Gdy aplikacja zostanie opublikowana przy użyciu serwera Proxy aplikacji usługi Azure AD, ruch z poziomu aplikacji toohello użytkowników hello przechodzi przez trzy połączenia:

1. Użytkownik Hello łączy toohello serwera Proxy aplikacji usługi Azure AD publiczny punkt końcowy usługi na platformie Azure
2. Usługa serwera Proxy aplikacji Hello łączy toohello łącznika serwera Proxy aplikacji
3. Łącznik serwera Proxy aplikacji Hello łączy toohello aplikacji docelowej

![Diagram przedstawiający przepływ ruchu z aplikacji tootarget użytkownika](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>Lokalizacja dzierżawy i usługę serwera Proxy aplikacji

Po utworzeniu konta dla dzierżawy usługi Azure AD, region hello dzierżawy zależy od kraju hello, które określisz. Po włączeniu serwera Proxy aplikacji hello wystąpień usługi Serwer Proxy aplikacji dzierżawy są wybrane, albo utworzony w hello sam region dzierżawy usługi Azure AD lub hello najbliższy region tooit.

Na przykład jeśli region dzierżawy usługi Azure AD jest hello Unii Europejskiej (UE), wszystkich łączników serwera Proxy aplikacji użyj wystąpień usługi w centrach danych platformy Azure w hello UE. Jeśli dostęp użytkowników opublikowane aplikacje, ruch przechodzi przez wystąpień usługi Serwer Proxy aplikacji hello w tej lokalizacji.

## <a name="considerations-for-reducing-latency"></a>Zagadnienia dotyczące zmniejszenia opóźnienia

Wszystkie rozwiązania proxy wprowadzić czas oczekiwania na połączenie sieciowe. Niezależnie od tego, który serwer proxy lub rozwiązanie sieci VPN wybierz jako rozwiązania dostępu zdalnego zawsze zawiera zestaw serwerów włączenie hello tooinside połączenia z siecią firmową.

Organizacje zwykle zawierają punkty końcowe serwera w sieci obwodowej. Z serwera Proxy aplikacji usługi Azure AD jednak ruch przechodzi przez hello usługi serwera proxy w chmurze hello podczas łączniki hello znajdują się w sieci firmowej. Brak sieci obwodowej jest wymagana.

Hello następne sekcje zawierają dodatkowe sugestie toohelp zmniejszenia opóźnień w jeszcze bardziej. 

### <a name="connector-placement"></a>Umieszczanie łącznika

Serwer Proxy aplikacji wybrał lokalizacji hello wystąpień, na podstawie lokalizacji użytkownika dzierżawcy. Jednak uzyskać toodecide gdzie tooinstall hello łącznika, umożliwiając hello zasilania toodefine hello opóźnienia właściwości ruchu sieciowego.

Podczas konfigurowania powitania serwera Proxy aplikacji usługi, poproś hello następujące pytania:

* Gdzie znajduje się aplikacja hello?
* Gdzie są większość użytkowników, którzy uzyskują dostęp do aplikacji hello znajduje się?
* Gdzie znajduje się wystąpienie serwera Proxy aplikacji hello?
* Już masz dedykowanej sieci połączenia tooAzure centrów danych konfiguracji, takich jak usługa Azure ExpressRoute lub podobne sieci VPN?

Łącznik Hello ma toocommunicate z platformy Azure i aplikacji (kroki 2 i 3 w diagram przepływu ruchu hello), więc hello umieszczania hello łącznika wpływa na powitania opóźnienia te dwa połączenia. Podczas szacowania położenia hello hello łącznika, należy pamiętać hello następujące punkty:

* Jeśli chcesz toouse ograniczone delegowanie protokołu Kerberos (KCD) dla logowania jednokrotnego, łącznik hello musi datacenter tooa procesów z wiersza. Ponadto serwer łącznika hello musi przyłączony do domeny toobe.  
* W razie wątpliwości, zainstaluj hello łącznika bliżej toohello aplikacji.

### <a name="general-approach-toominimize-latency"></a>Ogólne podejście toominimize opóźnienia

Aby zminimalizować opóźnienie hello hello end-to-end ruchu, optymalizacja każdego połączenia sieciowego. Każde połączenie może zostać zoptymalizowana przez:

* Zmniejszenie hello odległość między dwa końce hello hello przeskoku.
* Wybieranie hello tootraverse prawo sieci. Na przykład przechodzenie z sieci prywatnej zamiast hello publicznego Internetu może być szybsze, powodu toodedicated łącza.

Jeśli masz dedykowane łącza sieci VPN lub usługi platformy Azure i z siecią firmową, można toouse który.

## <a name="focus-your-optimization-strategy"></a>Skoncentruj się strategii optymalizacji

Brak małego możliwość toocontrol hello połączenia między użytkownikami i powitania serwera Proxy aplikacji usługi. Użytkownicy mogą uzyskiwać dostęp do aplikacji z siecią domową, kawiarni lub innego kraju. Zamiast tego można zoptymalizować hello połączeń z usługi Serwer Proxy aplikacji hello toohello aplikacji toohello łączniki serwera Proxy aplikacji. Należy rozważyć zawierających powitania po wzorce w danym środowisku.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>Wzorzec 1: Aplikacja toohello Zamknij łącznika hello Put

Miejsce hello łącznika Zamknij toohello aplikacji docelowej w powitania klienta sieci. Ta konfiguracja minimalizuje kroku 3 w diagramie topografii hello, ponieważ Zamknij hello łączników i aplikacji. 

Jeśli Twoje łącznika wymaga kontrolera domeny toohello procesów z wiersza, ten wzorzec jest korzystne. Większość klientów użycia tego wzorca, ponieważ działa dobrze w przypadku większości scenariuszy. Ten wzorzec również można łączyć z wzorca 2 toooptimize ruchu między usługą hello i hello łącznika.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>Wzorzec 2: Korzystanie z usługi ExpressRoute z publicznej komunikacji równorzędnej

Jeśli skonfigurowano publicznej komunikacji równorzędnej ExpressRoute, można użyć hello szybsze połączenia ExpressRoute ruch między serwera Proxy aplikacji i hello łącznika. Łącznik Hello jest nadal w sieci, zamknij toohello aplikacji.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>Wzorzec 3: Korzystać z usługi ExpressRoute z prywatnej komunikacji równorzędnej

Jeśli masz dedykowane sieci VPN lub ustawienie usługi ExpressRoute z prywatnej komunikacji równorzędnej platformy Azure i z siecią firmową, masz inną opcję. W tej konfiguracji hello sieci wirtualnej na platformie Azure zazwyczaj jest traktowana jako rozszerzenie hello sieci firmowej. Można więc zainstalować łącznik hello w hello centrum danych Azure i nadal spełniają wymagania małych opóźnieniach hello połączenia łącznika do aplikacji hello.

Czas oczekiwania nie zostanie naruszony, ponieważ ruch jest przepływających przez dedykowane połączenie. Ulepszone opóźnienia łącznika usługi Serwer Proxy aplikacji jest również pobrać, ponieważ łącznik hello jest zainstalowany w centrum danych Azure tooyour Zamknij lokalizacja dzierżawy usługi Azure AD.

![Diagram przedstawiający łącznika instalowane w ramach centrum danych Azure](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>Inne podejścia

Chociaż hello ten artykuł koncentruje się umieszczanie łącznika, można również zmienić położenie hello hello tooget lepsze opóźnienia cechy aplikacji.

Organizacje są coraz, przenoszenie ich sieci w środowiskach hostowanych. Umożliwia tooplace swoje aplikacje w środowisku hostowanej, która jest również częścią sieci firmowej i nadal mieścić się w domenie hello. W takim przypadku wzorców hello opisano w powyższej sekcji hello może być zastosowane toohello nowej lokalizacji aplikacji. Jeśli rozważasz tej opcji, zobacz [usług domenowych Azure AD](../active-directory-domain-services/active-directory-ds-overview.md).

Ponadto należy wziąć pod uwagę organizowanie za pomocą łączników [grup łącznika](active-directory-application-proxy-connectors.md) tootarget aplikacje, które znajdują się w różnych lokalizacjach i sieci. 

## <a name="common-use-cases"></a>Typowe przypadki użycia

W tej sekcji możemy przeprowadzenie kilka typowych scenariuszy. Załóżmy, że hello dzierżawy usługi Azure AD (i w związku z tym serwer proxy usługi punktu końcowego) znajduje się w hello Stanów Zjednoczonych (USA). Witaj zagadnienia omówione w tym przypadki użycia mają zastosowanie również w regionach tooother na całym świecie hello.

W tych sytuacjach możemy wywołać każdego połączenia "przeskok" i numer je łatwiej omówienie:

- **Przeskoku 1**: toohello użytkownika serwera Proxy aplikacji usługi
- **Przeskoku 2**: łącznika serwera Proxy aplikacji toohello usługi Serwer Proxy aplikacji
- **Przeskoku 3**: aplikacja docelowa toohello łącznika serwera Proxy aplikacji 

### <a name="use-case-1"></a>Przypadek użycia 1

**Scenariusz:** aplikacja hello jest w sieci organizacji w hello US, z użytkownikami w hello tego samego regionu. Nie ExpressRoute VPN istnieje lub między hello centrum danych Azure i hello sieci firmowej.

**Zalecenie:** wzorzec wykonaj 1, wyjaśniono w poprzedniej sekcji hello. Dla opóźnienia lepsze Rozważ użycie usługi ExpressRoute, w razie potrzeby.

Jest to prosty wzorzec. Przez umieszczenie łącznika hello niemal aplikacji hello zoptymalizować przeskoku 3. To także wybór fizycznych, ponieważ łącznik hello jest zazwyczaj zainstalowany z procesów z wiersza toohello aplikacji i toohello operacji centrum danych tooperform KCD.

![Diagram pokazujący, że użytkownicy, serwer proxy, łącznika i aplikacji są w hello nam](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>Przypadek użycia 2

**Scenariusz:** aplikacja hello jest w sieci organizacji w hello US, użytkownikom rozłożenia globalnie. Nie ExpressRoute VPN istnieje lub między hello centrum danych Azure i hello sieci firmowej.

**Zalecenie:** wzorzec wykonaj 1, wyjaśniono w poprzedniej sekcji hello. 

Ponownie wspólnego wzorca hello przeskoku toooptimize 3, umieszczane są hello łącznik aplikacji hello w pobliżu. Przeskoku 3 nie jest zwykle kosztowne, jeśli wszystkie poziomu hello sam region. Jednak przeskoku 1 może być droższe w zależności od tego, gdzie jest hello użytkownika, ponieważ użytkowników między Witaj świecie muszą uzyskać dostęp do wystąpienia serwera Proxy aplikacji hello w hello Stanów Zjednoczonych. Warto zauważyć, że żadne rozwiązanie do serwera proxy ma podobnej charakterystyce dotyczące użytkowników rozkłada się globalnie.

![Diagram pokazujący, że użytkownicy są rozkładane globalnie, ale powitania serwera proxy, łączników i aplikacji w hello nam](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>Przypadek użycia 3

**Scenariusz:** aplikacji hello znajduje się w sieci organizacji w hello NAS. Istnieje ExpressRoute z publicznej komunikacji równorzędnej między Azure i hello sieci firmowej.

**Zalecenie:** wykonaj wzorce 1 i 2 wyjaśniono w poprzedniej sekcji hello.

Najpierw umieścić łącznika hello jak możliwe toohello aplikacji. Następnie hello system automatycznie używa ExpressRoute przeskoku 2. 

Jeśli hello ExpressRoute link używa publicznej komunikacji równorzędnej, hello ruchu między powitania serwera proxy i łącznik hello przepływy za pośrednictwem tego łącza. Przeskok 2 optymalizacji opóźnień.

![Diagram przedstawiający między powitania serwera proxy i łącznik usługi ExpressRoute](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>Przypadek użycia 4

**Scenariusz:** aplikacji hello znajduje się w sieci organizacji w hello NAS. Istnieje ExpressRoute z prywatnej komunikacji równorzędnej między Azure i hello sieci firmowej.

**Zalecenie:** wzorzec wykonaj 3, wyjaśniono w poprzedniej sekcji hello.

Umieść łącznika hello hello centrum danych Azure, który jest połączony toohello sieci firmowej za pośrednictwem prywatnej komunikacji równorzędnej ExpressRoute. 

Witaj łącznika można umieścić w hello centrum danych Azure. Ponieważ hello łącznik nadal ma wiersza z procesów toohello aplikacji i centrum danych hello za pośrednictwem sieci prywatnej hello, przeskoku 3 pozostaje zoptymalizowane. Ponadto przeskoku 2 jest zoptymalizowany dalej.

![Diagram przedstawiający hello łącznika w centrum danych Azure i ExpressRoute hello łączników i aplikacji](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>Przypadek użycia 5

**Scenariusz:** aplikacji hello znajduje się w sieci organizacji w hello UE, z wystąpienia serwera Proxy aplikacji hello i większość użytkowników w hello NAS.

**Zalecenie:** łącznika hello miejsce w pobliżu aplikacji hello. Ponieważ USA użytkownicy uzyskują dostęp do wystąpienia serwera Proxy aplikacji wykonywanej toobe w hello tego samego regionu przeskoku 1 nie jest zbyt drogie. Przeskoku 3 jest zoptymalizowany. Należy rozważyć użycie usługi ExpressRoute toooptimize przeskoku 2. 

![Diagram przedstawiający użytkowników i serwera proxy w hello USA, przy użyciu łącznika hello i aplikacji w hello UE](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

Można także rozważyć użycie jednego innego elementu variant w takiej sytuacji. W przypadku większości użytkowników w organizacji hello w hello nam, istnieje prawdopodobieństwo są czy sieci rozszerza toohello nam również. Umieścić hello łącznika w hello USA i użyć hello dedykowanego wewnętrzną siecią firmową wiersza toohello aplikacji w hello UE. Są optymalizowane w ten sposób liczba przeskoków 2 i 3.

![Diagram przedstawiający użytkowników, proxy i łącznika w hello USA, aplikację w hello UE](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>Następne kroki

- [Włączanie serwera Proxy aplikacji](active-directory-application-proxy-enable.md)
- [Włączanie logowania jednokrotnego](active-directory-application-proxy-sso-using-kcd.md)
- [Włączanie dostępu warunkowego](active-directory-application-proxy-conditional-access.md)
- [Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji](active-directory-application-proxy-troubleshoot.md)
