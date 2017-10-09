---
title: "monitorowanie punktu końcowego Menedżera ruchu aaaAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule może pomóc Ci zrozumieć, jak Traffic Manager używa monitorowania punktów końcowych i punktu końcowego automatycznej pracy awaryjnej toohelp Azure klienci wdrażać aplikacje wysokiej dostępności"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>Monitorowanie punktu końcowego Menedżera ruchu

Usługi Azure Traffic Manager obejmuje monitorowanie wbudowanym punktem końcowym i punktu końcowego automatycznej pracy awaryjnej. Ta funkcja pomaga aplikacje wysokiej dostępności, które są odporne tooendpoint awarii, tym awarii region platformy Azure.

## <a name="configure-endpoint-monitoring"></a>Konfigurowanie monitorowania punktów końcowych

tooconfigure monitorowania punktów końcowych, należy określić następujące ustawienia w profilu usługi Traffic Manager hello:

* **Protokół**. Wybierz HTTP, HTTPS lub TCP jako protokół hello Traffic Manager używa podczas badania toocheck Twojego punktu końcowego jej kondycji. Monitorowania HTTPS nie Sprawdź, czy certyfikat SSL jest nieprawidłowy — tylko sprawdza hello tego certyfikatu jest obecny.
* **Port**. Wybierz hello port używany do żądania hello.
* **Ścieżka**. To ustawienie konfiguracji jest prawidłowy tylko w przypadku protokołów HTTP i HTTPS hello, dla których wymagane jest określenie ustawienia ścieżki hello. Zapewnia to ustawienie dla hello TCP monitorowania protokołu powoduje błąd. Dla protokołu TCP należy podać hello względną ścieżkę i nazwę hello hello strony sieci Web lub pliku hello tego hello uzyskuje dostęp do monitorowania. Ukośnika (/) jest prawidłowym wpisem hello ścieżki względnej. Ta wartość oznacza, czy plik hello jest w katalogu głównym hello (ustawienie domyślne).
* **Interwał sondowania**. Ta wartość określa, jak często punkt końcowy jest sprawdzany pod kątem kondycji od agenta sondowania Menedżera ruchu. Można określić w tym miejscu dwóch wartości: 30 sekund (zwykłego sondowania) i 10 sekund (fast sondowanie). Jeśli wartości nie są dostarczane, profilu hello ustawia domyślną wartość tooa 30 sekund. Odwiedź hello [cennik usługi Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager) więcej o cenach sondowania szybkiego toolearn strony.
* **Liczba błędów dopuszczalne**. Ta wartość określa, ile błędów sondowania agentem menedżera ruchu zaakceptować przed oznaczeniem określonego punktu końcowego swój stan jako niezdrowy. Wartość może należeć do zakresu od 0 do 9. Wartość 0 oznacza pojedynczego uszkodzenia monitorowania może spowodować toobe tego punktu końcowego, oznaczona jako w złej kondycji. Jeśli nie określono wartości, używa hello domyślna wartość 3.
* **Limit czasu monitorowania**. Ta właściwość określa hello ilość czasu hello agenta sondowania powinien zaczekać na uwzględnieniu Menedżera ruchu, który Sprawdź awarii po wysłaniu końcowego toohello sonda sprawdzania kondycji. Jeśli powitalne interwał sondowania jest ustawiony too30 sekund, możesz można ustawić wartość limitu czasu powitania od 5 do 10 sekund. Jeśli nie określono wartości, używa wartość domyślną równą 10 sekund. Jeśli powitalne interwał sondowania jest ustawiony too10 sekund, możesz można ustawić wartość limitu czasu powitania od 5 do 9 sekund. Jeśli wartość limitu czasu nie zostanie określona, używa wartość domyślną 9 sekund.

![Monitorowanie punktu końcowego Menedżera ruchu](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**Rysunek 1: Monitorowanie punktu końcowego Menedżera ruchu**

## <a name="how-endpoint-monitoring-works"></a>Jak działa monitorowania punktów końcowych

Przypadku hello monitorowania protokołu HTTP lub HTTPS, sondowania agenta menedżera ruchu hello sprawia, że punkt końcowy toohello na żądanie GET przy użyciu hello protokół, port i ścieżka względna podane. Jeśli ponownie pobiera odpowiedź 200 OK, a następnie tego punktu końcowego jest uznawany za dobrej kondycji. Jeśli odpowiedź hello jest inną wartość, lub jeśli brak odpowiedzi nie są odbierane hello limit czasu określony, hello sondowanie agenta menedżera ruchu ponownie podejmuje zgodnie z toohello ustawienie dopuszczalne liczbę błędów (ponowne próby są wykonywane informacji, jeśli to ustawienie ma wartość 0) . Jeśli hello liczbę kolejnych niepowodzeń jest wyższa niż ustawienie dopuszczalne liczbę błędów hello, tego punktu końcowego jest oznaczona jako w złej kondycji. 

Jeśli hello monitorowania protokołu TCP, hello Traffic Manager sondowania agent inicjuje żądanie połączenia TCP za pomocą portu hello określony. Jeśli punkt końcowy hello odpowiada toohello żądanie połączenia odpowiedzi hello tooestablish, że sprawdzenie kondycji jest oznaczony jako sukcesu i sondowania agenta menedżera ruchu hello resetuje połączenie TCP hello. Jeśli odpowiedź hello jest inną wartość, lub brak odpowiedzi nie są odbierane hello limit czasu określony, hello sondowanie agenta menedżera ruchu próbuje ponownie, zgodnie z toohello ustawienie dopuszczalne liczbę błędów (ponowne próby będą Jeśli to ustawienie ma wartość 0). Jeśli hello liczbę kolejnych niepowodzeń jest wyższa niż ustawienie dopuszczalne liczbę błędów hello, ten punkt końcowy jest oznaczona złej kondycji.

We wszystkich przypadkach sondy Menedżera ruchu z wielu lokalizacji i oznaczanie niepowodzenie kolejnych hello się stanie w każdym regionie. Oznacza to również, czy punkty końcowe otrzymują sondy kondycji z Menedżera ruchu z częstotliwością wyższe niż ustawienie hello używane dla interwału sondowania.

>[!NOTE]
>Dla protokołu HTTP lub HTTPS Protokół monitorowania po stronie punktu końcowego hello popularną praktyką jest tooimplement niestandardowej strony w aplikacji — na przykład /health.aspx. Przy użyciu tej ścieżki do monitorowania, można wykonać testy specyficzne dla aplikacji, takich jak sprawdzanie liczników wydajności lub Sprawdzanie dostępności bazy danych. W oparciu o te niestandardowe kontroli, strona hello zwraca odpowiedni kod stanu HTTP.

Wszystkie punkty końcowe w profilu usługi Traffic Manager udostępnić ustawienia monitorowania. Jeśli potrzebujesz toouse różne ustawienia monitorowania dla różnych punktów końcowych, możesz utworzyć [zagnieżdżonych profilów usługi Traffic Manager](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings).

## <a name="endpoint-and-profile-status"></a>Stan punktu końcowego i profilu

Można włączyć i wyłączyć profilów usługi Traffic Manager i punktów końcowych. Jednak zmiany w stan punktu końcowego również mogą wystąpić jako wynik Traffic Manager automatycznego ustawienia i procesów.

### <a name="endpoint-status"></a>Stan punktu końcowego

Można włączyć lub wyłączyć określonego punktu końcowego. nie wpływa na podległej usłudze Hello, którym może nadal być dobrej kondycji. Zmiana formanty stanu punktu końcowego hello hello dostępność punktu końcowego hello w hello profilu usługi Traffic Manager. Po wyłączeniu stan punktu końcowego Menedżera ruchu nie sprawdza jego kondycji, a punkt końcowy hello jest niedostępna w odpowiedzi DNS.

### <a name="profile-status"></a>Stan profilu

Przy użyciu ustawienia stanu profilu hello, można włączyć lub wyłączyć określonego profilu. Gdy stan punktu końcowego ma wpływ na jeden punkt końcowy, stan profilu wpływa na całą profil hello, w tym wszystkie punkty końcowe. Po wyłączeniu profilu hello punkty końcowe nie są sprawdzane pod kątem kondycji i punkty końcowe nie są uwzględnione w odpowiedzi DNS. [NXDOMAIN](https://tools.ietf.org/html/rfc2308) kod odpowiedzi jest zwracany hello zapytania DNS.

### <a name="endpoint-monitor-status"></a>Stan monitora punktu końcowego

Punkt końcowy monitoruje stan jest wyświetlany stan hello hello punktu końcowego wartość generowanych przez Menedżera ruchu. Nie można zmienić tego ustawienia ręcznie. Stan monitora punktu końcowego Hello jest kombinacją hello wyniki monitorowania punktów końcowych i hello stan punktu końcowego skonfigurowanego. w hello w poniższej tabeli przedstawiono możliwe wartości punktu końcowego monitoruje stan Hello:

| Stan profilu | Stan punktu końcowego | Stan monitora punktu końcowego | Uwagi |
| --- | --- | --- | --- |
| Disabled (Wyłączony) |Enabled (Włączony) |Nieaktywne |Profil Hello została wyłączona. Chociaż stan punktu końcowego hello jest włączona, pierwszeństwo ma stan profilu hello (wyłączone). Punkty końcowe w profilach wyłączone nie są monitorowane. NXDOMAIN kod odpowiedzi jest zwracany hello zapytania DNS. |
| &lt;wszystkie&gt; |Disabled (Wyłączony) |Disabled (Wyłączony) |punkt końcowy Hello została wyłączona. Wyłączone punkty końcowe nie są monitorowane. Witaj punktu końcowego nie jest uwzględniony w odpowiedzi DNS, w związku z tym nie odbieranie ruchu. |
| Enabled (Włączony) |Enabled (Włączony) |Online |punkt końcowy Hello jest monitorowane i jest w dobrej kondycji. Jest dołączony do odpowiedzi DNS, a mogą odbierać dane. |
| Enabled (Włączony) |Enabled (Włączony) |Ograniczone |Monitorowania kontroli kondycji punktu końcowego kończą się niepowodzeniem. punkt końcowy Hello nie jest uwzględniony w odpowiedzi DNS i nie odbiera ruch. <br>Toothis wyjątku jest Jeśli wszystkie punkty końcowe są ograniczone, w którym to przypadku wszystkich z nich są traktowane jako toobe zwracany w odpowiedzi na kwerendę hello).</br>|
| Enabled (Włączony) |Enabled (Włączony) |CheckingEndpoint |punkt końcowy Hello jest monitorowana, ale wyniki hello hello pierwsze badanie nie zostały jeszcze odebrane. CheckingEndpoint to stan tymczasowy, który zazwyczaj występuje natychmiast po dodaniu lub włączanie punktu końcowego w profilu hello. Punkt końcowy w tym stanie jest dołączony do odpowiedzi DNS i mogą odbierać dane. |
| Enabled (Włączony) |Enabled (Włączony) |Zatrzymane |Witaj chmury usługi lub aplikacji sieci web który hello toois punktów punktu końcowego nie działa. Sprawdź hello chmury usługi lub aplikacji internetowej ustawień aplikacji. Może to również nastąpić, jeśli hello punktu końcowego jest typ zagnieżdżony punktu końcowego i profilu podrzędnych hello jest wyłączony lub jest nieaktywna. <br>Punkt końcowy ze stanem zatrzymania nie jest monitorowany. Nie jest uwzględniony w odpowiedzi DNS, a nie odbiera ruch. Toothis wyjątku jest, jeśli wszystkie punkty końcowe są ograniczone, w którym to przypadku wszystkie z nich będą uznawane za toobe zwracany w odpowiedzi na kwerendę hello.</br>|

Szczegółowe informacje na temat obliczania stan monitora punktu końcowego dla zagnieżdżonej punktów końcowych, zobacz [zagnieżdżonych profilów usługi Traffic Manager](traffic-manager-nested-profiles.md).

### <a name="profile-monitor-status"></a>Stan monitora profilu

Stan monitora profilu Hello jest kombinacją stan profilu hello skonfigurowane i wartości stanu monitora hello punktu końcowego dla wszystkich punktów końcowych. w hello w poniższej tabeli opisano Hello możliwe wartości:

| Stan profilu (zgodnie z konfiguracją) | Stan monitora punktu końcowego | Stan monitora profilu | Uwagi |
| --- | --- | --- | --- |
| Disabled (Wyłączony) |&lt;wszelkie&gt; lub profil z określonych punktów końcowych. |Disabled (Wyłączony) |Profil Hello została wyłączona. |
| Enabled (Włączony) |Stan Hello co najmniej jeden punkt końcowy jest znacznie mniej wydajna. |Ograniczone |Przejrzyj hello poszczególnych punktu końcowego stan wartości toodetermine które punkty końcowe wymagać dalszych działań. |
| Enabled (Włączony) |Stan Hello co najmniej jeden punkt końcowy jest w trybie Online. Punkty końcowe nie będą miały stan obniżony. |Online |Usługa Hello akceptuje ruch. Są wymagane żadne dalsze akcje. |
| Enabled (Włączony) |Stan Hello co najmniej jeden punkt końcowy jest CheckingEndpoint. Punkty końcowe nie są w stanie Online lub obniżony. |CheckingEndpoints |Ten stan przejścia występuje, gdy profilu, jeśli utworzone lub włączone. Kondycja punktu końcowego Hello sprawdzany powitania po raz pierwszy. |
| Enabled (Włączony) |Stany Hello wszystkich punktów końcowych w profilu hello są wyłączone lub zatrzymana lub hello profilu nie ma zdefiniowanych punktów końcowych. |Nieaktywne |Punkty końcowe nie są aktywne, ale profil hello jest nadal włączony. |

## <a name="endpoint-failover-and-recovery"></a>Punkt końcowy trybu failover i odzyskiwania

Menedżer ruchu okresowo sprawdza dostępność hello kondycję każdego punktu końcowego, w tym zła punktów końcowych. Menedżer ruchu wykrywa punkt końcowy staje się dobrej kondycji, a jego powrót do obrotu.

Punkt końcowy jest zła, gdy wystąpienia któregokolwiek z hello następujące zdarzenia:
- W przypadku hello monitorowania protokołu HTTP lub HTTPS:
    - Odebrano odpowiedź z systemem innym niż 200 (w tym kod różnych 2xx lub przekierowanie 301/302).
- Jeśli hello monitorowania protokołu TCP: 
    - Odpowiedź innych niż potwierdzenia lub SYN potwierdzenia odebranego żądanie SYNCHRONIZACJI toohello odpowiedzi wysyłane przez Menedżera ruchu tooattempt ustanawianie połączenia.
- Limit czasu. 
- Wszelkie inne połączenia problemy powodujące hello punktu końcowego nie są dostępne.

Aby uzyskać więcej informacji dotyczących rozwiązywania problemów nie powiodło się sprawdzenie, zobacz [stan rozwiązywania problemów ze spadkiem w usłudze Azure Traffic Manager](traffic-manager-troubleshooting-degraded.md). 

Hello następujący plan na rysunku 2 jest szczegółowy opis hello monitorowania procesu punktu końcowego Menedżera ruchu, który ma hello następujące ustawienia: jest monitorowanie protokołu HTTP, interwał sondowania wynosi 30 sekund, liczba niepowodzeń tolerowaną to 3, wartość limitu czasu to 10 sekund, a czas wygaśnięcia DNS wynosi 30 sekund.

![Punkt końcowy Menedżera ruchu sekwencji trybu failover i powrotu po awarii](./media/traffic-manager-monitoring/timeline.png)

**Rysunek 2: Ruchu Menedżer punktu końcowego trybu failover i odzyskiwania sekwencji**

1. **POBIERZ**. Dla każdego punktu końcowego hello monitorowania systemu Menedżera ruchu wykonuje żądanie GET na powitania ścieżce określonej w hello ustawienia monitorowania.
2. **200 OK**. system monitorowania Hello oczekuje toobe komunikat HTTP 200 OK zwrócona w ciągu 10 sekund. Po otrzymaniu tej odpowiedzi rozpoznaje, że usługa hello jest dostępna.
3. **30 sekund między każdym sprawdzeniem**. sprawdzenie kondycji punktu końcowego Hello jest powtarzany co 30 sekund.
4. **Usługa jest niedostępna**. Usługa Hello jest niedostępny. Menedżer ruchu nie będzie wiedzieć, do czasu następnego sprawdzania kondycji hello.
5. **Hello tooaccess prób monitorowania ścieżki**. Witaj monitorowania systemu wykonuje żądanie GET, ale nie otrzymał odpowiedzi w określonym przedziale czasu hello 10 sekund (alternatywnie odpowiedzi z systemem innym niż 200 mogą pojawić się). Próbuje trzy razy, w odstępach 30 sekund. Jeśli jeden z wpisów hello zakończy się pomyślnie, hello liczbę prób jest resetowany.
6. **Stan ustawiony tooDegraded**. Po czwartym niepowodzeniu kolejnych hello monitorowania systemu oznacza stan niedostępny punktu końcowego hello jako obniżony.
7. **Ruch jest punkty końcowe kierunku tooother**. Witaj serwery DNS Menedżera ruchu są aktualizowane i Traffic Manager nie będzie już zwracać hello punktu końcowego w zapytaniach tooDNS odpowiedzi. Nowe połączenia są ukierunkowanej tooother, dostępnych punktów końcowych. Jednak poprzedniej odpowiedzi DNS, które zawierają ten punkt końcowy nadal można buforować cykliczne serwery DNS i klientów DNS. Klienci kontynuują punktu końcowego hello toouse do momentu wygaśnięcia hello pamięci podręcznej DNS. Jako hello pamięć podręczna DNS wygaśnie, klienci utworzyć nowego zapytania DNS i ukierunkowanej toodifferent punktów końcowych. czas trwania pamięci podręcznej Hello jest kontrolowana przez ustawienie TTL hello w hello profilu usługi Traffic Manager, na przykład 30 sekund.
8. **Kontrole kondycji kontynuować**. Toocheck hello kondycji hello punktu końcowego Menedżera ruchu będzie nadal występować, gdy ma stan obniżony. Menedżer ruchu wykrywa toohealth zwraca hello punktu końcowego.
9. **Usługa wraca do trybu online**. Usługa Hello staną się dostępne. punkt końcowy Hello zachowuje jego stan obniżony w usłudze Traffic Manager do momentu jego następnego sprawdzania kondycji wykonuje hello monitorowania systemu.
10. **Wznawia tooservice ruchu**. Traffic Manager wysyła żądanie GET i odbiera odpowiedź 200 OK stanu. Usługa Hello zwróciła tooa dobrej kondycji. serwery nazw Menedżera ruchu Hello są aktualizowane i rozpoczęciem toohand się nazwą DNS hello usługa w odpowiedzi DNS. Ruch zwraca punkt końcowy toohello buforowane odpowiedzi DNS, które zwracają inne punkty końcowe wygasa, a jako istniejących połączeń kończą tooother punktów końcowych.

    > [!NOTE]
    > Ponieważ działanie Menedżera ruchu polega na powitania poziom DNS, nie może mieć wpływ istniejącego punktu końcowego tooany połączenia. Składającym ruchu między punktami końcowymi (albo przez ustawienia profilu zmienione albo podczas pracy awaryjnej lub powrotu po awarii), usługi Traffic Manager określa, że nowe punkty końcowe tooavailable połączenia. Jednak inne punkty końcowe może kontynuacja tooreceive ruchu za pomocą istniejących połączeń kończą się tymi sesjami. tooenable toodrain ruchu z istniejących połączeń, aplikacje należy ograniczyć hello czas trwania sesji z każdego punktu końcowego.

## <a name="traffic-routing-methods"></a>Metody routingu ruchu

Punkt końcowy ma stan obniżony, jest już zwracany w odpowiedzi tooDNS zapytania. Zamiast tego alternatywny punkt końcowy jest wybrane i zwracane. metody routingu ruchu Hello skonfigurowane w profilu hello Określa, jak wybrano hello alternatywnych punktu końcowego.

* **Priorytet**. Punkty końcowe tworzą listy priorytetów. zwracany jest zawsze Hello pierwszego dostępnego punktu końcowego na liście hello. Jeśli stan punktu końcowego jest ograniczone, zwracany jest hello następnego dostępnego punktu końcowego.
* **Ważone**. Wszystkie dostępne punkt końcowy jest wybierany losowo oparte na ich wagi przypisanej i hello wag hello innych dostępnych punktów końcowych.
* **Wydajność**. użytkownik końcowy toohello najbliższy punkt końcowy Hello jest zwracana. Jeśli ten punkt końcowy jest niedostępny, punkt końcowy jest losowo wybrany z hello wszystkich innych dostępnych punktów końcowych. Wybieranie losowy punkt końcowy pozwala uniknąć kaskadowych błąd, który może wystąpić, gdy hello najbliższy punkt końcowy jest przeciążona. Plany alternatywnych trybu failover dla routingu ruchu wydajności można skonfigurować za pomocą [zagnieżdżonych profilów usługi Traffic Manager](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region).
* **Geograficzne**. punkt końcowy Hello mapowane lokalizacji geograficznej hello tooserve na podstawie żądania zapytania hello, zwracane są adresami IP. Jeśli ten punkt końcowy jest niedostępny, inny punkt końcowy nie będzie wybranego toofailover, od lokalizacji geograficznej mogą być mapowane tylko końcowego tooone w profilu (szczegółowe informacje znajdują się w hello [— często zadawane pytania](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method)). Najlepszym rozwiązaniem, przy użyciu routingu geograficznego zaleca się klienci toouse zagnieżdżonych profilów usługi Traffic Manager z więcej niż jeden punkt końcowy jako punkty końcowe hello hello profilu.

Aby uzyskać więcej informacji, zobacz [metody routingu ruchu Menedżera ruchu](traffic-manager-routing-methods.md).

> [!NOTE]
> Jeden wyjątek toonormal routingu ruchu zachowanie występuje, gdy wszystkie kwalifikujące się punkty końcowe mają obniżeniem stanu. Sprawia, że Menedżera ruchu "optymalnego" podejmować i *odpowiada tak, jakby wszystkie punkty końcowe stan obniżony hello faktycznie znajdują się w stanie online*. To zachowanie jest ewentualnie toohello preferowane byłoby toonot zwracać żadnych punktów końcowych w hello odpowiedzi DNS. Wyłączony lub zatrzymany punkty końcowe nie są monitorowane, w związku z tym nie uważa się kwalifikujące się do ruchu sieciowego.
>
> Ten stan jest często spowodowane niewłaściwa konfiguracja usługi hello, takich jak:
>
> * Listy kontroli dostępu [ACL] blokuje kontroli kondycji hello Menedżera ruchu.
> * Niepoprawna konfiguracja hello monitorowanie portu lub protokół hello profilu Menedżera ruchu.
>
> Witaj konsekwencją to zachowanie jest czy kontroli kondycji usługi Traffic Manager nie są poprawnie skonfigurowane, mogą być wyświetlane do od ruchu hello routingu jako menedżera ruchu *jest* działa prawidłowo. Jednak w takim przypadku trybu failover punktu końcowego nie może się zdarzyć, co ma wpływ na dostępność aplikacji ogólnej. Jest ważne toocheck, że profil hello pokazuje stan Online, nie stan obniżony. Stan Online wskazuje, że hello Traffic Manager kondycji sprawdza, czy działa zgodnie z oczekiwaniami.

Aby uzyskać więcej informacji na temat rozwiązywania problemów nie przeszły pomyślnie sprawdzania kondycji, zobacz [stan rozwiązywania problemów ze spadkiem w usłudze Azure Traffic Manager](traffic-manager-troubleshooting-degraded.md).



## <a name="next-steps"></a>Następne kroki

Dowiedz się [działania Menedżera ruchu](traffic-manager-how-traffic-manager-works.md)

Dowiedz się więcej o hello [metody routingu ruchu](traffic-manager-routing-methods.md) obsługiwane przez Menedżera ruchu

Dowiedz się, jak za[Tworzenie profilu Menedżera ruchu](traffic-manager-manage-profiles.md)

[Rozwiązywanie problemów z obniżony stan](traffic-manager-troubleshooting-degraded.md) na punkt końcowy Menedżera ruchu
