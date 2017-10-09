---
title: aaaWhat jest Traffic Manager | Dokumentacja firmy Microsoft
description: "Ten artykuł pomoże poznać Menedżera ruchu jest i czy jest wybór routingu ruchu prawo hello aplikacji"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Omówienie usługi Traffic Manager

Menedżer ruchu Microsoft Azure umożliwia toocontrol hello dystrybucję ruchu użytkowników dla punktów końcowych usług w różnych centrach danych. Punkty końcowe usługi obsługiwane przez usługę Traffic Manager obejmują maszynach wirtualnych platformy Azure, aplikacji sieci Web i usług w chmurze. Usługi Traffic Manager można również używać z zewnętrznymi punktami końcowymi poza platformą Azure.

Menedżer ruchu używa hello systemu nazw domen (DNS, Domain Name System) toodirect żądań toohello najbardziej odpowiednia końcowego klienta na podstawie metody routingu ruchu i kondycji hello hello punktów końcowych. Menedżer ruchu udostępnia szereg [metody routingu ruchu](traffic-manager-routing-methods.md) i [punktu końcowego opcje monitorowania](traffic-manager-monitoring.md) toosuit inną aplikację potrzeb i modele automatycznej pracy awaryjnej. Menedżer ruchu jest toofailure elastyczne, w tym hello awarii całego region platformy Azure.

## <a name="traffic-manager-benefits"></a>Zalety usługi Traffic Manager

Menedżer ruchu może ułatwić:

* **Zwiększanie dostępności ważnych aplikacji**

    Menedżer ruchu zapewnia wysoką dostępność dla aplikacji dla monitorowania punktów końcowych i podając automatycznej pracy awaryjnej, gdy punkt końcowy przestanie działać.

* **Zwiększyć czas odpowiedzi dla aplikacji wysokiej wydajności**

    Azure umożliwia toorun usługi w chmurze lub witryny sieci Web w całym hello world w centrach danych. Menedżer ruchu skraca czas odpowiedzi aplikacji, kierując punktu końcowego toohello ruchu z hello najniższe opóźnienia sieci dla powitania klienta.

* **Przeprowadź obsługę usługi bez przestoju**

    Można wykonać operacji zaplanowanej konserwacji na aplikacje bez przestoju. Menedżer ruchu kieruje punkty końcowe tooalternative ruchu podczas konserwacji hello jest w toku.

* **Łączenie lokalnych i aplikacji działających w chmurze**

    Traffic Manager obsługuje zewnętrzne, innych niż Azure punkty końcowe umożliwiające toobe używane z hybrydowym w chmurze i lokalnych wdrożeń, w tym hello "serii chmurą," "migracji do chmury," i "trybu failover z chmurą" scenariuszy.

* **Dystrybuuj ruch we wdrożeniach dużych, złożonych**

    Przy użyciu [zagnieżdżonych profilów usługi Traffic Manager](traffic-manager-nested-profiles.md), metody routingu ruchu mogą być połączone toocreate zaawansowane i elastycznych zasad toosupport hello wymaga większych i bardziej skomplikowanych wdrożeń.

## <a name="how-traffic-manager-works"></a>Jak działa usługa Traffic Manager

Usługi Azure Traffic Manager umożliwia toocontrol hello Dystrybucja ruchu między punktami końcowymi aplikacji. Punkt końcowy jest internetowy usługi hostowanej wewnątrz lub na zewnątrz Azure.

Menedżer ruchu zapewnia dwie kluczowe korzyści:

1. Rozkład ruchu zgodnie z tooone kilku [metody routingu ruchu](traffic-manager-routing-methods.md)
2. [Ciągłego monitorowania kondycji punktu końcowego](traffic-manager-monitoring.md) i automatycznej pracy awaryjnej, gdy punkty końcowe nie powiedzie się.

Gdy klient próbuje tooconnect tooa usługi, najpierw musi wskazywać nazwę DNS hello adres IP tooan usługi hello. następnie powitania klienta łączy toothat — usługi hello tooaccess adresu IP.

**Hello najważniejszych toounderstand punktu jest, że Traffic Manager działa na poziomie DNS hello.**  Punkty końcowe na podstawie reguł hello hello metody routingu ruchu usługi Traffic Manager używa DNS toodirect klientów toospecific. Klienci łączą się punkt końcowy toohello wybrane **bezpośrednio**. Menedżer ruchu nie jest serwer proxy lub bramy. Menedżer ruchu nie widzi ruchu hello przekazywania między powitania klienta i usługi hello.

### <a name="traffic-manager-example"></a>Przykład Menedżera ruchu

Firmy Contoso Corp zostały opracowane nowego portalu dla partnerów. adres URL Hello tego portalu jest https://partners.contoso.com/login.aspx. Aplikacja Hello jest hostowana w trzech regionach platformy Azure. dostępność tooimprove i zmaksymalizować wydajność globalnych, używają usługi Traffic Manager toodistribute klienta ruchu toohello najbliższego dostępnego punktu końcowego.

tooachieve tej konfiguracji ukończyć powitalnych następujące kroki:

1. Wdrażanie trzech wystąpień usługi. nazwy DNS Hello te wdrożenia są ".net us.cloudapp firmy contoso", "contoso-eu.cloudapp .net" i "contoso-asia.cloudapp .net".
2. Utwórz profil usługi Traffic Manager o nazwie "contoso.trafficmanager.net" i skonfigurować metody routingu ruchu "Performance" hello toouse między punktami końcowymi hello trzech.
* Konfigurowanie ich nazwy domeny niestandardowych, "partners.contoso.com", toopoint too'contoso.trafficmanager.net ", przy użyciu rekordu CNAME systemu DNS.

![Konfiguracja DNS Menedżera ruchu][1]

> [!NOTE]
> Podczas korzystania z usługi Azure Traffic Manager domen niestandardowych, możesz korzystać CNAME toopoint nazwy domeny niestandardowych domeny nazwa tooyour Menedżera ruchu. Standardy usługi DNS nie zezwalają toocreate CNAME na powitania "wierzchołku" (lub głównego) do domeny. W związku z tym nie można utworzyć rekord CNAME dla domeny "contoso.com" (nazywane czasem "naked" domeny). Można utworzyć tylko rekord CNAME dla domeny, w obszarze "contoso.com", takie jak "www.contoso.com". toowork wokół to ograniczenie, zalecamy używanie prostych żądań toodirect przekierowania HTTP "contoso.com" tooan alternatywnej nazwy takie jak "www.contoso.com".

### <a name="how-clients-connect-using-traffic-manager"></a>Jak klienci łączą przy użyciu Menedżera ruchu

Kontynuacja z poprzedniego przykładu hello, gdy klient żąda https://partners.contoso.com/login.aspx strony hello powitania klienta wykonuje następujące nazwy DNS hello tooresolve kroki hello i nawiązania połączenia:

![Ustanawianie połączenia za pomocą Menedżera ruchu][2]

1. powitania klienta wysyła DNS cykliczne tooits skonfigurowane zapytania DNS usługa tooresolve hello nazwy "partners.contoso.com". Cykliczne usługi DNS, czasem nazywane usługą "DNS lokalnych" nie obsługuje bezpośrednio domen DNS. Zamiast powitania klienta off-loads pracy hello skontaktowania się hello DNS autorytatywne różnych usług między tooresolve Internet potrzebne hello nazwy DNS.
2. tooresolve hello nazwy DNS, usługi DNS cykliczne hello znajduje hello serwery nazw dla domeny "contoso.com" hello. Te nazwy serwerów toorequest hello "partners.contoso.com" DNS rekordu się następnie skontaktuje. serwery DNS contoso.com Hello zwracać hello rekord CNAME, który wskazuje toocontoso.trafficmanager.net.
3. Następnie usługa DNS cykliczne hello znajduje hello serwery nazw dla domeny "trafficmanager.net" hello, które są udostępniane przez hello usługi Azure Traffic Manager. Wysyła następnie żądanie toothose rekordów DNS "contoso.trafficmanager.net" hello serwerów DNS.
4. serwery nazw Hello Traffic Manager mógł odebrać Żądanie hello. Wybiera on punkt końcowy na podstawie:

    - Witaj skonfigurowany stan każdego punktu końcowego (wyłączone punkty końcowe nie są zwracane)
    - sprawdza, czy Hello bieżącą kondycję każdego punktu końcowego, zgodnie z ustaleniami hello kondycji usługi Traffic Manager. Aby uzyskać więcej informacji, zobacz [monitorowanie punktu końcowego Menedżera ruchu](traffic-manager-monitoring.md).
    - Witaj wybrane metody routingu ruchu. Aby uzyskać więcej informacji, zobacz [metody routingu ruchu Menedżera](traffic-manager-routing-methods.md).

5. Witaj wybrany punkt końcowy jest zwracana jako innego rekordu CNAME systemu DNS. W takim przypadku Daj nam Załóżmy, że jest zwracana contoso us.cloudapp.net.
6. Następnie usługa DNS cykliczne hello znajduje hello serwery nazw dla domeny "cloudapp.net" hello. Kontaktuje się hello toorequest serwery te nazwy "contoso-us.cloudapp .net" rekordu DNS. Rekord DNS "A", zawierający adres IP punktu końcowego usługi amerykańskiej hello hello jest zwracana.
7. Usługa DNS cykliczne Hello konsoliduje hello wyniki i zwraca jednego klienta toohello odpowiedzi DNS.
8. Witaj klient otrzyma hello wyniki DNS i łączy toohello podany adres IP. powitania klienta łączy punkt końcowy usługi aplikacji toohello bezpośrednio, nie za pomocą Menedżera ruchu. Ponieważ chodzi o punkt końcowy HTTPS, przeprowadza niezbędne Uzgadnianie SSL/TLS hello powitania klienta, a następnie zgłasza żądanie HTTP GET dla hello "/ login.aspx" strony.

Usługa DNS cykliczne Hello buforuje hello odpowiedzi DNS, który odbiera. Program rozpoznawania nazw DNS w Hello na urządzeniu klienckim hello buforuje hello wynik. Buforowanie umożliwia kolejnych toobe zapytań DNS szybciej odpowiedzi przy użyciu danych z pamięci podręcznej hello zamiast badania inne serwery. czas trwania pamięci podręcznej hello Hello jest określana przez hello "time-to-live" (TTL) właściwości każdego rekordu DNS. Krótszej wartości powoduje szybsze wygaśnięcia pamięci podręcznej i w związku z tym więcej operacji toohello Traffic Manager serwery nazw. Dłużej wartości oznaczają może potrwać dłużej ruchu toodirect od punktu końcowego nie powiodło się. Menedżer ruchu pozwala tooconfigure hello TTL używany w możliwie jak 0 sekund toobe odpowiedzi DNS Menedżera ruchu, możliwie jak 2 147 483 647 sekund (hello zgodne z maksymalną wielkość zakresu [ze standardem RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), umożliwiając toochoose hello wartość Aby najlepiej równoważy hello wymagań aplikacji.

## <a name="pricing"></a>Cennik

Aby uzyskać informacje o cenach, zobacz [cennik usługi Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="faq"></a>Często zadawane pytania

Często zadawane pytania dotyczące usługi Traffic Manager, zobacz [Traffic Manager — często zadawane pytania](traffic-manager-FAQs.md)

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o Menedżerze ruchu [punkt końcowy monitorowania i automatycznej pracy awaryjnej](traffic-manager-monitoring.md).

Dowiedz się więcej o Menedżerze ruchu [metody routingu ruchu](traffic-manager-routing-methods.md).

Dowiedz się więcej o niektórych hello innego klucza [możliwości w zakresie obsługi](../networking/networking-overview.md) platformy Azure.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

