---
title: "aaaNested profilów usługi Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano funkcja \"Zagnieżdżonych profilów\" hello usługi Azure Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>Zagnieżdżonych profilów usługi Traffic Manager

Menedżer ruchu zawiera szereg metody routingu ruchu, umożliwiających toocontrol jak wybierze Menedżera ruchu, który punkt końcowy powinny odbierać dane z każdego użytkownika końcowego. Aby uzyskać więcej informacji, zobacz [metody routingu ruchu Menedżera ruchu](traffic-manager-routing-methods.md).

Każdy profil usługi Traffic Manager określa pojedynczej metody routingu ruchu. Istnieją jednak scenariusze, które wymagają bardziej złożone routingu ruchu niż hello routingu udostępniane przez jeden profil Menedżera ruchu. Można zagnieżdżać Traffic Manager profile toocombine hello korzyści z więcej niż jedna metoda routingu ruchu. Zagnieżdżonych profilów pozwalają toooverride hello domyślnego menedżera ruchu zachowanie toosupport większych i bardziej złożone wdrożenia aplikacji.

Hello następujące przykłady przedstawiają sposób toouse zagnieżdżonych profilów usługi Traffic Manager w różnych scenariuszach.

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>Przykład 1: Połączenie "Performance" i "Ważone" routingu ruchu

Załóżmy, że wdrożono aplikację w hello następujące regiony platformy Azure: zachodnie stany USA, Europa Zachodnia i Azja Wschodnia. Korzystając z Menedżera ruchu "Performance" routingu ruchu metody toodistribute ruchu toohello region najbliższy toohello użytkownika.

![Profil Menedżera ruchu pojedynczej][4]

Teraz załóżmy, że chcesz tootest usługi tooyour aktualizacji przed udostępnieniem jej powszechnie się więcej. Ma toouse hello "ważoną" routingu ruchu metody toodirect niewielką część ruchu tooyour testowego wdrożenia. Wdrożenia testowego hello równolegle z istniejącego wdrożenia produkcyjnego hello skonfigurowane w Europa.

Nie można łączyć zarówno ważone i "wydajności-routingu ruchu w jednym profilu. toosupport tego scenariusza, możesz utworzyć profil Menedżera ruchu przy użyciu punktów końcowych Europa hello dwa i metody routingu ruchu "Ważone" hello. Następnie dodaj ten profil 'child' jako profil toohello punktu końcowego "parent". Profil nadrzędnego Hello nadal używa hello metody routingu ruchu wydajności i zawiera hello innych wdrożeń globalne jako punktów końcowych.

powitania po diagramie przedstawiono w tym przykładzie:

![Zagnieżdżonych profilów usługi Traffic Manager][2]

W tej konfiguracji ruch skierowany za pośrednictwem profilu nadrzędnego hello dystrybuuje ruch w regionach normalnie. W ramach Europa Zachodnia hello profilu zagnieżdżone polega na rozłożeniu ruchu toohello produkcyjnych i testowych punkty końcowe według wagi toohello przypisane.

Gdy profil nadrzędnego hello używa metody routingu ruchu "Performance" hello, każdego punktu końcowego musi być przypisany lokalizacji. Lokalizacja Hello jest przypisany podczas konfigurowania punktu końcowego hello. Wybierz najbliższą wdrożenia tooyour hello region platformy Azure. Hello regiony platformy Azure są wartości lokalizacji hello obsługiwane przez hello Internet opóźnienia tabeli. Aby uzyskać więcej informacji, zobacz [Menedżera ruchu "Performance" metody routingu ruchu](traffic-manager-routing-methods.md#performance).

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>Przykład 2: Monitorowania punktów końcowych w profilach zagnieżdżone

Menedżer ruchu aktywnie monitoruje kondycję hello każdego punktu końcowego usługi. Jeśli punkt końcowy jest zła, Traffic Manager kieruje użytkowników tooalternative punkty końcowe toopreserve hello dostępności usługi. To zachowanie monitorowania i trybu failover punktu końcowego stosuje tooall metody routingu ruchu. Aby uzyskać więcej informacji, zobacz [monitorowanie punktu końcowego Menedżera ruchu](traffic-manager-monitoring.md). Punkt końcowy monitorowania działa inaczej w przypadku zagnieżdżonych profilów. Zagnieżdżonych profilów hello nadrzędnego profilu nie wykonywanie kontroli kondycji w podrzędnym hello bezpośrednio. Zamiast tego kondycja hello punktów końcowych hello podrzędne profil jest używany toocalculate hello ogólną kondycję hello podrzędnych profilu. Te informacje o kondycji są propagowane hello zagnieżdżone profilu hierarchii. Hello nadrzędnego profil używa tego toodetermine zagregowane kondycji czy toodirect ruchu toohello podrzędnych profilu. Zobacz hello [— często zadawane pytania](traffic-manager-FAQs.md#traffic-manager-nested-profiles) szczegółowe informacje o monitorowanie kondycji zagnieżdżonych profilów.

Zwracanie toohello poprzedni przykład, załóżmy, że hello wdrożenia produkcyjnego w Europie zachodnie zakończy się niepowodzeniem. Domyślnie profilu 'child' hello kieruje wszystkie wdrożenia testowego toohello ruchu. Jeśli hello testowe wdrożenie nie powiedzie się także, hello nadrzędnego profil określa, czy hello podrzędnych profilu nie powinny być ruchu, ponieważ wszystkie podrzędne punkty końcowe są w złej kondycji. Następnie hello nadrzędnego profilu dystrybuuje ruch toohello innych regionów.

![Zagnieżdżone profilu trybu failover (domyślnie)][3]

Może być to rozmieszczenie modyfikowania. Lub może być cały ruch Europa to teraz będzie toohello testowego wdrożenia zamiast ruchu ograniczony podzestaw danych. Niezależnie od kondycji hello hello przetestować wdrożenie, ma toofail za pośrednictwem toohello innych regionów przypadku niepowodzenia wdrożenia produkcyjnego hello w Europa Zachodnia. tooenable tego trybu failover, można określić parametru "MinChildEndpoints" hello podczas konfigurowania profilu podrzędnych hello jako punktu końcowego w profilu nadrzędnego hello. Parametr Hello określa minimalną liczbę dostępnych punktów końcowych w profilu podrzędnych hello hello. Witaj, wartością domyślną jest "1". W tym scenariuszu należy ustawić hello MinChildEndpoints wartość too2. Poniżej tego progu profilu nadrzędnego hello uwzględnia hello całego podrzędne profil toobe niedostępny i kieruje ruchem toohello innych punktów końcowych.

Witaj rysunku przedstawiono tę konfigurację:

![Zagnieżdżone trybu failover profil z "MinChildEndpoints" = 2][4]

> [!NOTE]
> Witaj metody routingu ruchu 'Priority' dystrybuuje wszystkich ruchu tooa jeden punkt końcowy. W związku z tym jest niewiele cel ustawienie MinChildEndpoints innych niż "1" dla profilu podrzędnych.

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>Przykład 3: Priorytetów trybu failover regiony routingu ruchu "Performance"

Witaj domyślne zachowanie dla metody routingu ruchu "Performance" hello jest zaprojektowana tooavoid nadmiernie ładowanie hello obok najbliższego punktu końcowego i powoduje kaskadowych dużej liczby błędów. Gdy punkt końcowy nie powiedzie się, cały ruch, który będzie przekierowywany, że toothat punktu końcowego jest równomiernie rozłożona toohello innych punktów końcowych wszystkich regionach.

![Routing domyślny tryb failover ruchu "Performance"][5]

Jednak Załóżmy preferowane tooWest pracy awaryjnej ruchu Europa hello nam, a tylko bezpośrednie ruchu tooother regionów, gdy oba punkty końcowe są niedostępne. Można utworzyć tego rozwiązania przy użyciu profilu podrzędnego z hello metody routingu ruchu 'Priority'.

![Routingu z preferencyjne trybu failover ruchu "wydajność.][6]

Ponieważ punkt końcowy Europa hello ma wyższy priorytet niż hello endpoint zachodnie stany USA, cały ruch wysyłany toohello endpoint Europa Zachodnia, gdy oba punkty końcowe są w trybie online. W przypadku niepowodzenia Europa Zachodnia ruch jest bezpośrednie tooWest Stanów Zjednoczonych. Profil hello zagnieżdżone ruch jest bezpośrednie tooEast Azja tylko w przypadku, gdy nie powiedzie się zarówno Europa Zachodnia, jak i zachodnie stany USA.

Ten wzorzec można powtórzyć dla wszystkich regionów. Zamień wszystkich trzech punktów końcowych w profilu nadrzędnego hello trzy profile podrzędnych, każdy dostarczanie kolejność priorytetów trybu failover.

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>Przykład 4: Kontrolowanie ruchu "Performance" routing między wiele punktów końcowych w hello sam region

Załóżmy, że hello "Performance" metody routingu ruchu jest używany w profilu, który ma więcej niż jeden punkt końcowy w określonym regionie. Domyślnie ruch kierowany toothat region jest równomiernie rozłożona dostępnych punktów końcowych w tym regionie.

![Ruch "Performance" routingu ruchu w regionie dystrybucji (domyślnie)][7]

Zamiast opcji dodawania wiele punktów końcowych w Europa Zachodnia, te punkty końcowe są ujęte w profilu oddzielne podrzędnych. Profil podrzędnych Hello zostanie dodany toohello nadrzędnego jako hello tylko punkt końcowy w Europa Zachodnia. Ustawienia Hello na powitania podrzędnych profilu mogą kontrolować rozkład ruchu hello Europa Zachodnia przez włączenie routingu ruchu na podstawie priorytetu lub ważoną w tym regionie.

![Ruch "Performance" routingu z Dystrybucja ruchu w regionie niestandardowych][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>Przykład 5: Ustawienia monitorowania dla punktu końcowego

Załóżmy, że używasz toosmoothly Traffic Manager migrację ruchu starszych lokalnymi witryny sieci web tooa nowe oparte na chmurze wersji hostowana na platformie Azure. Dla starszych lokacji hello ma kondycji lokacji toomonitor URI toouse hello strony głównej. Ale hello wersji nowego oparte na chmurze w przypadku wdrażania monitorowania niestandardowej strony (ścieżka "/ monitor.aspx") zawiera dodatkowe kontrole.

![Punkt końcowy Menedżera ruchu monitorowania (domyślnie)][9]

Ustawienia monitorowania powitania w profilu usługi Traffic Manager mają zastosowanie punktów końcowych tooall w jednym profilu. Przy użyciu zagnieżdżonych profilów używany jest profil różnych podrzędnych na różne ustawienia monitorowania toodefine lokacji.

![Monitorowanie za pomocą ustawień-endpoint punktu końcowego Menedżera ruchu][10]

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [profilów usługi Traffic Manager](traffic-manager-overview.md)

Dowiedz się, jak za[Tworzenie profilu Menedżera ruchu](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
