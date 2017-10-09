---
title: "aaaAzure Traffic Manager — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania dotyczące usługi Traffic Manager"
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
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Często zadawane pytania (FAQ) Menedżera ruchu

## <a name="traffic-manager-basics"></a>Podstawowe informacje dotyczące Menedżera ruchu

### <a name="what-ip-address-does-traffic-manager-use"></a>Jakiego adresu IP używa Menedżera ruchu?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na powitania poziom DNS. Wysyła odpowiedzi DNS toodirect klientów toohello odpowiednią usługę punktu końcowego. Następnie łączyć klienci punktu końcowego usługi toohello bezpośrednio, nie za pomocą Menedżera ruchu.

W związku z tym usługi Traffic Manager nie ma punktu końcowego lub adres IP dla klientów tooconnect do. W związku z tym jeśli ma statyczny adres IP dla usługi, które muszą być skonfigurowane na hello usługi, nie w usłudze Traffic Manager.

### <a name="does-traffic-manager-support-sticky-sessions"></a>Traffic Manager obsługuje "trwałe" sesje?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na powitania poziom DNS. Używa odpowiedzi DNS toodirect toohello klientów odpowiednią usługę punktu końcowego. Klienci nawiązują połączenie punktu końcowego usługi toohello bezpośrednio, nie za pomocą Menedżera ruchu. W związku z tym menedżera ruchu nie widzi ruch hello HTTP między powitania klienta i serwera hello.

Ponadto hello źródłowy adres IP zapytanie DNS hello odebranych przez usługę Traffic Manager należy usługi DNS toohello cykliczne nie powitania klienta. W związku z tym usługi Traffic Manager nie ma możliwości tootrack poszczególnych klientów i nie może implementować "trwałe" sesji. To ograniczenie jest ruchu na podstawie DNS tooall typowe systemy zarządzania i nie jest określonych tooTraffic menedżera.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>Dlaczego widzę błąd HTTP podczas korzystania z Menedżera ruchu?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na powitania poziom DNS. Używa odpowiedzi DNS toodirect toohello klientów odpowiednią usługę punktu końcowego. Następnie łączyć klienci punktu końcowego usługi toohello bezpośrednio, nie za pomocą Menedżera ruchu. Menedżer ruchu nie można znaleźć ruchu HTTP między klientem i serwerem. W związku z tym błędu HTTP widocznej musi pochodzić z aplikacji. Powitania klienta tooconnect toohello aplikacji zakończeniu wszystkich kroków rozpoznawania DNS. Zawierającej interakcji z Menedżera ruchu na przepływie ruchu aplikacji hello.

Dalsza analiza w związku z tym należy skoncentrować się na aplikacji hello.

Nagłówek hosta Hello HTTP wysyłane z przeglądarki powitania klienta jest hello źródło najbardziej typowych problemów. Upewnij się, że aplikacja hello jest nagłówek hosta poprawne hello tooaccept skonfigurowany dla nazwy domeny hello, którego używasz. Dla punktów końcowych przy użyciu hello Azure App Service, zobacz [Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service przy użyciu Menedżera ruchu](../app-service-web/web-sites-traffic-manager-custom-domain-name.md).

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>Jaki jest wpływ na wydajność hello przy użyciu Menedżera ruchu?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na powitania poziom DNS. Ponieważ klienci łączą bezpośrednio z punktów końcowych usługi tooyour, nie jest bez wpływu na wydajność poniesionych podczas korzystania z Menedżera ruchu, po nawiązaniu połączenia hello.

Ponieważ usługi Traffic Manager integruje się z aplikacjami na powitania poziom DNS, jest wymagane dodatkowe toobe wyszukiwania DNS do hello łańcucha rozpoznawania DNS. wpływ Hello Traffic Manager na czas rozpoznawania nazw DNS jest minimalny. Menedżer ruchu korzysta globalnej sieci serwerów nazw, a [emisji](https://en.wikipedia.org/wiki/Anycast) zapytania DNS tooensure sieci są zawsze routingiem toohello znajdującym się najbliżej serwera dostępne nazwy. Ponadto buforowanie odpowiedzi DNS oznacza, że hello dodatkowe DNS opóźnień przy użyciu usługi Traffic Manager ma zastosowanie tylko tooa część sesji.

Hello wydajności metody tras ruchu toohello najbliższego dostępnego punktu końcowego. Witaj wynikiem jest tym hello wpływ ogólną wydajność skojarzonych z tą metodą powinien być minimalny. Wzrost opóźnienia DNS powinien przesunięcia przy niższych punktów końcowych toohello opóźnienia sieci.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>Jakie protokoły aplikacji można używać Menedżera ruchu?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na powitania poziom DNS. Po wykonaniu wyszukiwania DNS hello Klienci nawiązują połączenie toohello punkt końcowy aplikacji bezpośrednio, nie za pomocą Menedżera ruchu. W związku z tym hello połączenia można użyć dowolnego protokołu aplikacji. W przypadku wybrania protokołu TCP, jak hello monitorowania protokołu, Menedżera ruchu monitorowania kondycji punktu końcowego mogą być przeprowadzane bez przy użyciu protokołów aplikacji. Jeśli wybierzesz kondycji hello toohave zweryfikowana przy użyciu protokołu aplikacji hello punktu końcowego musi toobe stanie toorespond tooeither HTTP lub HTTPS GET żądania.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>Nazwa domeny "naked" można używać Menedżera ruchu?

Nie. Standardy usługi DNS Hello nie zezwalają na tooco CNAME — istnieje z inne rekordy DNS hello takie same nazwy. Witaj wierzchołku lub głównego strefy DNS zawsze zawiera dwa rekordy DNS istniejące; Witaj SOA i hello autorytatywne rekordy NS. Oznacza to, że rekord CNAME nie można utworzyć w wierzchołku strefy hello bez naruszania hello standardy usługi DNS.

Menedżer ruchu wymaga nazwy DNS niestandardowych hello toomap rekordu CNAME systemu DNS. Na przykład www.contoso.com toohello Traffic Manager profilu DNS nazwy contoso.trafficmanager.net mapowania. Ponadto hello profilu usługi Traffic Manager zwraca drugi tooindicate rekordu CNAME systemu DNS, który punkt końcowy powitania klienta należy nawiązać połączenie.

toowork rozwiązać ten problem, zaleca się przy użyciu ruchu toodirect przekierowania HTTP z hello naked domeny nazwa tooa inny adres URL, którego można następnie użyć Menedżera ruchu. Na przykład hello naked domeny "contoso.com" można przekierowywać użytkowników toohello CNAME "www.contoso.com" wskazujący toohello nazwy DNS Menedżera ruchu.

Pełna obsługa naked domen w usłudze Traffic Manager są śledzone w naszym zaległości funkcji. Możesz zarejestrować programu obsługi dla tego żądania funkcji przez [głosowaniu w naszej witrynie opinii społeczności](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly).

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>Menedżer ruchu za adres podsieci powitania klienta podczas obsługi zapytań DNS? 
Nie, obecnie Traffic Manager uwzględnia tylko hello źródłowy adres IP hello DNS kwerendę, która zwykle jest adres IP hello hello rozpoznawania nazw DNS, podczas wykonywania wyszukiwania dla metody routingu Geographic i wydajności.  
W szczególności [RFC 7871 — podsieci klienta w zapytaniach DNS](https://tools.ietf.org/html/rfc7871) zapewnia [mechanizmu rozszerzenie dla serwera DNS (EDNS0)](https://tools.ietf.org/html/rfc2671) które można przekazać na powitania klienta podsieci adresów z mechanizmów rozpoznawania obsługujących serwery tooDNS jest obecnie nie jest obsługiwany w Menedżerze ruchu. Możesz zarejestrować programu obsługi dla tego żądania funkcji za pośrednictwem naszego [witrynę opinii społeczności](https://feedback.azure.com/forums/217313-networking).


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>Co to jest czas wygaśnięcia DNS i jak ma ona wpływu na użytkowników?

Jeśli zapytanie DNS wyładowuje w usłudze Traffic Manager, ustawia wartość w odpowiedzi hello o nazwie czas wygaśnięcia (TTL). Ta wartość, którego jednostka jest w sekundach, wskazuje tooDNS rozwiązujący w dół na jak długo toocache tej odpowiedzi. Podczas rozpoznawania nazw DNS nie ma gwarancji toocache tego wyniku, buforowanie ich umożliwia ich toorespond tooany następne kwerendy poza hello pamięci podręcznej, zamiast korzystania z serwerów DNS Menedżera tooTraffic. Dotyczy to hello odpowiedzi w następujący sposób:
- wyższa wartość TTL zmniejsza hello liczba zapytań, które trafić na powitania serwery DNS Menedżera ruchu, które może zmniejszyć koszt hello dla danego klienta, ponieważ liczba zapytań, obsługiwane jest użycie rozliczeniowy.
- wyższa wartość TTL potencjalnie może skrócić czas hello przyjmuje toodo wyszukiwania DNS.
- wyższe wartości TTL również oznacza, że dane nie odzwierciedla hello najnowszych informacji o kondycji uzyskiwanej Menedżera ruchu za pośrednictwem jego sondowania agentów.

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>Jak wysokie lub niskie można ustawić hello TTL odpowiedzi Menedżera ruchu?

Można ustawić na na poziomie profilu hello toobe czas wygaśnięcia DNS wynoszącymi 0 sekund i wysokości 2 147 483 647 sekund (hello zgodne z maksymalną wielkość zakresu [ze standardem RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). TTL 0 oznacza, że podrzędne rozpoznawania nazw DNS nie buforowanie odpowiedzi na kwerendy, wszystkie zapytania są oczekiwane serwerów DNS Menedżera ruchu hello tooreach do rozpoznania.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Metody routingu ruchu Geographic Menedżera ruchu

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>Co to są niektórych przypadków użycia, w którym geograficzne routing jest przydatne? 
Geograficzne typ routingu może służyć w jakimkolwiek scenariuszu gdzie klient Azure potrzebuje toodistinguish użytkowników oparte na regionów geograficznych. Na przykład przy użyciu metody routingu ruchu geograficzne hello, można udzielać użytkownikom z określonych regionów środowisko użytkownika innego niż z innych regionów. Innym przykładem jest zgodne z oczekuje suwerenności danych lokalnych, wymagających, że użytkownicy z określonego regionu obsługiwane tylko przez punkty końcowe w tym regionie.

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>Co to są hello regionów, które są obsługiwane przez usługę Traffic Manager geograficzne routingu? 
Hierarchia kraj/region Hello jest używany przez usługę Traffic Manager można znaleźć [tutaj](traffic-manager-geographic-regions.md). Gdy ta strona jest aktualizowany o zmianach, można również programowane pobieranie hello tych samych informacji za pomocą hello [Azure Traffic Manager REST API](https://docs.microsoft.com/rest/api/trafficmanager/). 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>Jak usługi traffic manager ustalić, gdzie pyta użytkownika z? 
Menedżer ruchu przegląda hello źródłowy adres IP zapytania hello (prawdopodobnie jest to lokalnego rozpoznawania nazw DNS czynności hello zapytań w imieniu użytkownika hello) i używa wewnętrznego adresu IP tooregion mapy toodetermine hello lokalizacji. Ta mapa jest aktualizowane na bieżąco tooaccount zmiany w hello internet. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>Jest on gwarantowane czy Menedżera ruchu poprawnie można określić dokładnej lokalizacji geograficznej hello hello użytkownika w każdym przypadku
Nie, Traffic Manager nie może zagwarantować tego regionu geograficznego hello możemy wywnioskować z adresu IP źródłowego hello zapytania DNS będzie zawsze odpowiada lokalizacji użytkownika toohello powodu toohello następujących powodów: 

- Po pierwsze zgodnie z opisem w poprzedniej hello — często zadawane pytania, hello źródłowy adres IP, który widzimy jest to, że podczas wyszukiwania hello w imieniu użytkownika hello program rozpoznawania nazw DNS. Gdy hello lokalizację geograficzną program rozpoznawania nazw DNS hello jest dobrym serwera proxy dla lokalizacji geograficznej hello hello użytkownika, może to być także różne w zależności od rozmiaru hello usługi rozpoznawania nazw DNS hello i hello określonego programu rozpoznawania nazw usługi DNS klient wybierze toouse. Na przykład klient znajduje się w Malezji można określić w ich urządzenia należy użyć ustawienia usługi rozpoznawania nazw DNS, których serwer DNS w Singapurze mogą zostać pobrane toohandle hello zapytania rozwiązania dla tego użytkownika/urządzenie. W tym przypadku Menedżera ruchu może zobaczyć tylko IP hello rozpoznawania adresu, który odpowiada toohello Singapuru lokalizacji. Zobacz też hello obsługuje starszych — często zadawane pytania dotyczące adres podsieci klienta na tej stronie.

- Drugie usługi Traffic Manager używa wewnętrznego mapy toodo hello IP toogeographic region translatora adresów. Gdy ta mapa jest weryfikowane i zaktualizować na bieżąco tooincrease jego dokładność i konta dla hello rozwijającymi rodzaj hello internet, jest nadal hello możliwość, że nasze informacje nie są dokładnie reprezentację hello lokalizację geograficzną wszystkich Witaj adresów IP.


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>Punkt końcowy toobe należy fizycznie znajduje się w hello tego samego regionu hello jedna jest konfigurowana dla routingu geograficzne? 
Nie, hello lokalizacji punktu końcowego hello nakłada żadnych ograniczeń, na których regionach mogą być mapowane tooit. Na przykład punkt końcowy w regionie Azure środkowe stany USA może mieć wszystkich użytkowników z tooit Indie przekierowanie.

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>Można przypisać regionów geograficznych tooendpoints w profilu, który nie został skonfigurowany, geograficzne routingu toodo? 

Tak, jeśli metoda routingu hello profilu nie jest geograficznej, możesz użyć hello [interfejsu REST API usługi Traffic Manager Azure](https://docs.microsoft.com/rest/api/trafficmanager/) tooassign tooendpoints regionach geograficznych, w tym profilu. Ta konfiguracja jest ignorowana w przypadku hello-geograficzne profilów typu routingu. Jeśli zmienisz takiego profilu toogeographic routingu typu w późniejszym czasie Traffic Manager można użyć te mapowania.


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>Dlaczego otrzymuję błąd przy próbie toochange hello metody routingu z istniejących tooGeographic profilu?

Wszystkie końcowe hello przy użyciu profilu geograficznego routingu muszą toohave tooit zamapować co najmniej jeden region. tooconvert istniejący typ routingu toogeographic profilu, musisz najpierw tooall regionów geograficznych tooassociate jego punktów końcowych przy użyciu hello [interfejsu REST API usługi Traffic Manager Azure](https://docs.microsoft.com/rest/api/trafficmanager/) przed zmianą hello routingu wpisz toogeographic. Jeśli przy użyciu portalu, najpierw usuń hello punktów końcowych, zmień metodę routingu hello hello toogeographic profilu, a następnie dodaj punkty końcowe hello wraz z ich mapowania regionu geograficznego. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>Dlaczego jest zalecane użytkownikom utworzenie zagnieżdżonych profilów zamiast punktów końcowych przy użyciu profilu z włączonym routingiem geograficzne? 

Region można przypisać tooonly jeden punkt końcowy, w obrębie profilu jeśli jego przy użyciu geograficzne typu routingu. Jeśli ten punkt końcowy nie jest typu zagnieżdżonego z tooit profilu dołączony podrzędne, jeśli tego punktu końcowego przechodzi w złej kondycji, Traffic Manager nadal tooit ruchu toosend od alternatywna hello nie wysyłać się, że cały ruch nie jest żadnym lepsze. Menedżer ruchu nie nie punkt końcowy tooanother trybu failover, nawet w przypadku, gdy region hello przypisany jest elementem "nadrzędnym" hello region przypisany punkt końcowy toohello, który zakończył się zła, (na przykład jeśli punktu końcowego, który ma Hiszpanii region przechodzi w złej kondycji, firma Microsoft będzie nie tooanother trybu failover punkt końcowy, który ma hello regionie Europy przypisany tooit). Jest to realizowane tooensure Instalator usługi Traffic Manager względem hello geograficzne granice, które odbiorca ma w swoim profilu. tooget hello zaletą awarii tooanother punktu końcowego, gdy punkt końcowy złej kondycji, zalecane jest przypisania regionów geograficznych profile toonested z wieloma punktami końcowymi w nim zamiast poszczególnych punktów końcowych. W ten sposób Jeśli punkt końcowy w hello zagnieżdżone podrzędne profil niepowodzenia, ruch może punktu końcowego tooanother pracy awaryjnej wewnątrz hello sam zagnieżdżone profilu podrzędnych.

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>Czy istnieją ograniczeń w wersji hello interfejsu API, która obsługuje ten typ routingu?

Tak, tylko do wersji interfejsu API 2017-03-01 i nowszej obsługuje hello geograficzne typ routingu. Starsze wersje interfejsu API nie może być używane toocreated profile geograficzne typu routingu ani przypisać tooendpoints regionów geograficznych. Starsza wersja interfejsu API w przypadku profilów tooretrieve używane z subskrypcją platformy Azure, dowolny profil geograficzny typ routingu nie są zwracane. Ponadto przy użyciu starszej wersji interfejsu API dowolny profil zwrócił który ma punkty końcowe z przypisaniem region geograficzny, nie ma jej przypisanie regionu geograficznego pokazano.



## <a name="traffic-manager-endpoints"></a>Punkty końcowe usługi Traffic Manager

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>Z punktami końcowymi z wieloma subskrypcjami można używać Menedżera ruchu?

Za pomocą punktów końcowych z wieloma subskrypcjami nie jest możliwe z aplikacjami sieci Web platformy Azure. Aplikacje sieci Web platformy Azure wymaga dowolną nazwę domeny niestandardowej, używany w aplikacjach sieci Web jest używana tylko w ramach jednej subskrypcji. Nie jest możliwe toouse aplikacji sieci Web z wieloma subskrypcjami z hello tą samą nazwą domeny.

Dla innych typów punktu końcowego jest możliwe toouse Menedżera ruchu z punktami końcowymi z więcej niż jedną subskrypcję. W Menedżerze zasobów punktów końcowych z dowolnej subskrypcji można dodać tooTraffic Manager, tak długo, jak hello konfigurowania profilu usługi Traffic Manager hello osoba punktu końcowego toohello dostęp do odczytu. Te uprawnienia można otrzymać za pomocą [usługi Azure Resource Manager kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md).


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>Czy można używać Menedżera ruchu z miejsc "Przemieszczania" usługi w chmurze?

Tak. Usługi w chmurze przemieszczania gniazda można skonfigurować w usłudze Traffic Manager jako zewnętrzne punkty końcowe. Kontrole kondycji nadal są naliczane opłaty szybkością hello punkty końcowe platformy Azure. Ponieważ hello typu zewnętrznego punktu końcowego jest używana, podległej usłudze toohello zmiany nie są odczytywane automatycznie. Z zewnętrzne punkty końcowe Traffic Manager nie może wykryć hello usługi w chmurze jest zatrzymana lub usunięciu. W związku z tym hello Traffic Manager nadal rozliczenia dotyczące sprawdzania kondycji, aż do punktu końcowego hello jest wyłączone lub usunięte.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>Traffic Manager obsługuje punktów końcowych protokołu IPv6?

Menedżer ruchu nie ma obecnie IPv6 addressible serwerów nazw. Jednak Menedżera ruchu, mogą nadal używane przez IPv6 klientów łączących się z punktami końcowymi tooIPv6. Nie oznacza, że klient DNS bezpośrednio żądań tooTraffic Manager. Zamiast tego powitania klienta używa usługi DNS, rekursywny. Tylko protokół IPv6 klient wysyła żądania usługi DNS cykliczne toohello za pomocą protokołu IPv6. Następnie usługa cykliczne hello powinna być stanie toocontact hello Traffic Manager serwery nazw przy użyciu protokołu IPv4.

Menedżer ruchu odpowiada o nazwie DNS hello hello punktu końcowego. punkt końcowy toosupport protokołu IPv6, AAAA usługi DNS rekord toohello nazwy DNS punktu końcowego hello wskazującego IPv6, adres musi być obecny. Kontrole kondycji usługi Traffic Manager obsługuje tylko adresy IPv4. Witaj usługi wymaga punktu końcowego tooexpose IPv4 na powitania tą samą nazwą DNS.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>Czy można używać Menedżera ruchu z więcej niż jednej aplikacji sieci Web w hello tym samym regionie?

Zazwyczaj Menedżera ruchu jest używane toodirect ruchu tooapplications wdrożone w różnych regionach. Jednak również umożliwia którym aplikacja ma więcej niż jedno wdrożenie hello tego samego regionu. Hello Azure Traffic Manager punktów końcowych nie zezwalają na więcej niż jeden punkt końcowy aplikacji sieci Web z hello tego samego regionu Azure toobe dodane toohello tego samego profilu Menedżera ruchu.

##  <a name="traffic-manager-endpoint-monitoring"></a>Monitorowanie punktu końcowego Menedżera ruchu

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>Jest błędów region tooAzure odporność Menedżera ruchu?

Menedżera ruchu jest kluczowym elementem hello dostarczania wysoką dostępność aplikacji na platformie Azure.
toodeliver wysokiej dostępności usługi Traffic Manager musi mieć wyjątkowo wysoki poziom dostępności i musi być odporne tooregional awarii.

Zgodnie z projektem składniki Menedżera ruchu są odporne tooa pełną awarii dowolny region platformy Azure. To odporności stosuje składniki usługi Traffic Manager tooall: hello serwery DNS, hello interfejsu API warstwy magazynu hello i hello punktu końcowego usługi monitorowania.

W przypadku mało prawdopodobnego hello awarii całego regionu Azure Menedżera ruchu jest oczekiwany toocontinue toofunction normalnie. Aplikacje wdrożone w wielu regionach platformy Azure może polegać na toodirect Traffic Manager ruchu tooan dostępnego wystąpienia aplikacji.

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>Jak hello wybór lokalizacji grupy zasobów wpływa Menedżera ruchu?

Menedżer ruchu jest pojedyncza usługa globalnego. Nie ma charakteru regionalnego. Hello wybór lokalizacji grupy zasobów powoduje, że nie profile Menedżera tooTraffic różnica wdrożonych w tej grupie zasobów.

Usługa Azure Resource Manager wymaga wszystkich zasobów grup toospecify lokalizacji, która określa hello domyślna lokalizacja dla zasobów wdrożonych w tej grupie zasobów. Po utworzeniu profilu Menedżera ruchu jest tworzony w grupie zasobów. Użyj wszystkich profilów usługi Traffic Manager **globalne** jako ich lokalizacji, Zastępowanie domyślnego grupy zasobów hello.

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>Jak ustalić hello bieżącą kondycję każdego punktu końcowego?

Witaj bieżący stan każdego punktu końcowego monitorowania w toohello dodanie ogólną profil, zostanie wyświetlony w hello portalu Azure. Te informacje są również dostępne za pośrednictwem hello Monitor ruchu [interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163667.aspx), [poleceń cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt125941.aspx), i [wiersza polecenia platformy Azure i platform](../cli-install-nodejs.md).

Azure nie zapewnia informacje historyczne na temat punktu końcowego w ciągu ostatnich kondycji lub hello możliwości tooraise alerty dotyczące kondycji tooendpoint zmiany.

### <a name="can-i-monitor-https-endpoints"></a>Można monitorować punktów końcowych HTTPS?

Tak. Traffic Manager obsługuje sondowanie za pośrednictwem protokołu HTTPS. Skonfiguruj **HTTPS** jako protokół hello w hello konfiguracji monitorowania.

Menedżer ruchu nie może dostarczyć żadnych weryfikacji certyfikatu w tym:

* Po stronie serwera, certyfikaty nie są weryfikowane.
* Funkcja SNI po stronie serwera certyfikatów nie są obsługiwane.
* Certyfikaty klienta nie są obsługiwane.

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>Czy można użyć Menedżera ruchu, nawet jeśli Moja aplikacja nie ma obsługi protokołu HTTP lub HTTPS?

Tak. Można określić protokołu TCP, jak hello monitorowania protokołu i Menedżera ruchu można inicjować połączenie TCP i oczekiwania na odpowiedź z punktu końcowego hello. Jeśli punkt końcowy hello odpowiedzi toohello żądanie połączenia z połączeniem hello tooestablish odpowiedzi, przed upływem limitu czasu hello okres, a następnie tego punktu końcowego jest oznaczony jako dobrej kondycji.

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>Jakie określone odpowiedzi są wymagane z punktu końcowego hello, korzystając z protokołu TCP monitorowania?

W przypadku monitorowania TCP uruchamia Menedżera ruchu TCP trójstopniowego wysyłając SYN żądania tooendpoint na hello określonego portu. Następnie oczekuje na pewien czas (jak określono w ustawieniach limitu czasu hello) na odpowiedź z punktu końcowego hello. Jeśli punkt końcowy hello odpowiada toohello SYN żądania za pomocą SYN ACK odpowiedzi w ramach hello limit czasu określony w hello ustawienia monitorowania, a następnie tego punktu końcowego jest uznawany za dobrej kondycji. Odebranie hello SYN ACK odpowiedzi hello Traffic Manager resetuje połączenie hello odpowiedzi z powrotem RST.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>Szybkość Menedżera ruchu przenieść mój użytkowników zła punktu końcowego?

Menedżer ruchu udostępnia wiele ustawień, które mogą pomóc Ci praca awaryjna hello toocontrol Twojego profilu Menedżera ruchu w następujący sposób:
- można określić, czy punkty końcowe hello sond Traffic Manager hello częściej ustawiając hello interwał sondowania na 10 sekund. Dzięki temu, jak najszybciej wykryto dowolnego punktu końcowego, przechodząc w złej kondycji. 
- można określić, jak długo toowait przed żądania sprawdzenia kondycji upłynie limit czasu (wartość minimalna limit czasu to 5 s).
- można określić, ile błędów mogą wystąpić, zanim punkt końcowy hello jest oznaczony jako w złej kondycji. Ta wartość może być niski jako 0, w którym punktem końcowym wielkość hello jest oznaczony jako niepoprawny zaraz po awarii hello Sprawdź pierwszy kondycji. Jednak używanie hello minimalną wartość 0 dla hello dopuszczalne liczba niepowodzeń może spowodować tooendpoints przełączana poza obrotu powodu tooany przejściowych problemów, które mogą wystąpić w czasie hello sondowanie.
- Witaj, time to live (TTL) można określić dla toobe odpowiedzi DNS hello możliwie jak 0. Grozi to ma oznacza, że programy rozpoznawania nazw DNS nie może buforować odpowiedź hello i każdego nowego zapytania pobiera odpowiedzi, która będzie zawierała hello najbardziej aktualne informacje o kondycji, w tym hello Menedżera ruchu.

Przy użyciu tych ustawień, Traffic Manager zapewnia tryb failover poniżej 10 sekund po punkt końcowy przechodzi złej kondycji i zapytanie DNS staje się przed hello odpowiedni profil.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>Jak określić różne ustawienia monitorowania dla różnych punktów końcowych w profilu

Ustawienia monitorowania są Menedżera ruchu na poziomie profilu. Jeśli potrzebujesz toouse różne ustawienia monitorowania dla tylko jeden punkt końcowy może odbywać dzięki użyciu tego punktu końcowego jako [zagnieżdżone profilu](traffic-manager-nested-profiles.md) którego ustawienia monitorowania różnią się od hello nadrzędnego profilu.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>Jakie hosta nagłówka punktu końcowego kondycji sprawdza użycie?

Menedżer ruchu używa nagłówków hosta kontroli kondycji HTTP i HTTPS. Nagłówek hosta Hello użyty przez Menedżera ruchu jest nazwą hello docelowego punktu końcowego hello skonfigurowane w profilu hello. Nie można określić wartości Hello używane w nagłówku hosta hello oddzielnie od hello właściwość target.

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>Co to są hello adresów IP, z których pochodzą sprawdza kondycji hello?

Witaj Poniższa lista zawiera hello adresów IP, z których mogą pochodzić sprawdza kondycji usługi Traffic Manager. Możesz użyć tej listy tooensure czy połączenia przychodzące z tych adresów IP są dozwolone na powitania punkty końcowe toocheck jej stan kondycji.

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>Ile punktu końcowego toomy kontrole kondycji można oczekiwać od Menedżera ruchu?

Liczba Hello kondycji usługi Traffic Manager sprawdza, czy osiągnięciu punktu końcowego jest zależna od następujących hello:
- Witaj wartość ustawioną dla interwał monitorowania hello (mniejszego oznacza więcej żądań kierowanych na punkt końcowy w dowolnym okresie w danym momencie).
- Witaj liczba lokalizacji, z którego kontroli kondycji hello pochodzą (hello adresy IP, z których można oczekiwać, że te sprawdzenia ma na liście hello poprzedzających — często zadawane pytania).

## <a name="traffic-manager-nested-profiles"></a>Profile zagnieżdżone Menedżera ruchu

### <a name="how-do-i-configure-nested-profiles"></a>Jak skonfigurować zagnieżdżonych profilów?

Zagnieżdżonych profilów usługi Traffic Manager można skonfigurować przy użyciu obu hello Azure Resource Manager i hello klasycznego Azure interfejsów API REST, poleceń cmdlet programu Azure PowerShell i polecenia wiersza polecenia platformy Azure i platform. Są one również obsługiwane za pośrednictwem hello nowego portalu Azure. Nie są obsługiwane w portalu klasycznym hello.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>Obsługuje liczbę warstw zagnieżdżenia wykonuje Menedżera ruchu?

Można zagnieżdżać profile poziomów too10 bezpośrednich. "Pętli" są niedozwolone.

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>Czy można mieszać inne typy punktów końcowych przy użyciu profilów zagnieżdżonych elementów podrzędnych w hello tego samego profilu Menedżera ruchu?

Tak. Nie ma żadnych ograniczeń na jak łączyć punktów końcowych różnych typów w profilu.

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>Jak modelu rozliczeń hello stosowane profilów zagnieżdżone?

Nie ma nie ujemna cennik wpływ przy użyciu zagnieżdżonych profilów.

Karta usługi Traffic Manager zawiera dwa składniki: kontroli kondycji punktu końcowego i miliony zapytań DNS

* Kontroli kondycji punktu końcowego: bez dodatkowych opłat profilu podrzędnych skonfigurowane jako punktu końcowego w profilu nadrzędny nie istnieje. Monitorowania punktów końcowych hello w profilu podrzędnych hello jest on rozliczany w hello zwykły sposób.
* Zapytania DNS: każdego zapytania są traktowane jako jeden raz. Zapytanie profil nadrzędnego, który zwraca punkt końcowy z profilu podrzędnych jest uwzględniane hello nadrzędnego tylko w przypadku profilu.

Aby uzyskać szczegółowe informacje, zobacz hello [cennikiem usługi Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>Czy istnieje negatywny wpływ na wydajność zagnieżdżonych profilów?

Nie. Nie ma żadnego wpływu wydajności, poniesionych przy użyciu zagnieżdżonych profilów.

serwery nazw Menedżera ruchu Hello przechodzenie hierarchii profilu hello wewnętrznie podczas przetwarzania każdego zapytania DNS. Profil nadrzędnej tooa zapytania DNS może otrzymywać odpowiedź DNS z punktem końcowym z profilu podrzędnych. Pojedynczy rekord CNAME jest używany zarówno w przypadku korzystania w jednym profilu lub profilach zagnieżdżonych. Brak toocreate nie konieczności rekord CNAME dla każdego profilu hello hierarchii.

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>Jak usługi Traffic Manager obliczeniowe kondycji hello zagnieżdżonych punktu końcowego w profilu nadrzędnego?

Profil nadrzędnego Hello nie sprawdzania kondycji w podrzędnym hello bezpośrednio. Zamiast tego kondycji hello hello podrzędne profil punktów końcowych są używane toocalculate hello ogólną kondycję hello podrzędnych profilu. Te informacje są propagowane prawidłowość hello zagnieżdżone profilu hierarchii toodetermine hello hello zagnieżdżone punktu końcowego. profilu nadrzędnego Hello używa tego toodetermine zagregowane kondycji czy hello ruchu może być ukierunkowanej toohello podrzędnych.

Witaj poniższej tabeli opisano zachowanie hello z Menedżera ruchu kondycji sprawdza, czy punkt końcowy zagnieżdżonych.

| Stan monitora profilowania podrzędne | Stan punktu końcowego Monitor nadrzędny | Uwagi |
| --- | --- | --- |
| Wyłączone. Profil podrzędnych Hello została wyłączona. |Zatrzymane |Stan punktu końcowego Hello nadrzędnego jest zatrzymana, nie jest wyłączone. Witaj stanem wyłączono jest zarezerwowana dla wskazujący wyłączono punktu końcowego hello hello nadrzędnego profilu. |
| Nieprawidłowe działanie. Co najmniej jeden element podrzędny punktu końcowego profilu jest w stanie obniżony. |Online: hello liczba Online punktów końcowych w profilu podrzędnych hello jest co najmniej hello wartość MinChildEndpoints.<BR>CheckingEndpoint: hello liczba Online oraz CheckingEndpoint punktów końcowych w profilu podrzędnych hello jest co najmniej hello wartość MinChildEndpoints.<BR>Ograniczone: inaczej. |Ruch jest punkt końcowy routingiem tooan stanu CheckingEndpoint. Jeśli zostanie ustawiona zbyt wysoka MinChildEndpoints, hello punktu końcowego jest zawsze znacznie mniej wydajna. |
| W trybie online. Co najmniej jeden element podrzędny punktu końcowego profilu jest w stanie Online. Żaden punkt końcowy jest hello stanu obniżony. |Zobacz powyżej. | |
| CheckingEndpoints. Co najmniej jeden element podrzędny punktu końcowego profilu jest "CheckingEndpoint". Brak punktów końcowych są "Online" lub "Ze spadkiem" |Taka sama jak powyżej. | |
| Nieaktywne. Wszystkie punkty końcowe profilu podrzędne są wyłączone lub zatrzymana lub ten profil nie ma punktów końcowych. |Zatrzymane | |

## <a name="next-steps"></a>Następne kroki:
- Dowiedz się więcej o Menedżerze ruchu [punkt końcowy monitorowania i automatycznej pracy awaryjnej](../traffic-manager/traffic-manager-monitoring.md).
- Dowiedz się więcej o Menedżerze ruchu [metody routingu ruchu](../traffic-manager/traffic-manager-routing-methods.md).