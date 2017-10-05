---
title: "Menedżer ruchu Azure — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera odpowiedzi na często zadawane pytania dotyczące usługi Traffic Manager"
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
ms.openlocfilehash: 44762864e0a5adf568fcd4928b48661196f05b9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Często zadawane pytania (FAQ) Menedżera ruchu

## <a name="traffic-manager-basics"></a>Podstawowe informacje dotyczące Menedżera ruchu

### <a name="what-ip-address-does-traffic-manager-use"></a>Jakiego adresu IP używa Menedżera ruchu?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na poziomie DNS. Wysyła odpowiedzi DNS, aby kierować klientów do punktu końcowego odpowiednią usługę. Klienci następnie połączyć się z punktem końcowym usługi bezpośrednio, nie za pomocą Menedżera ruchu.

W związku z tym menedżera ruchu nie zawiera punktu końcowego lub adres IP dla klientów nawiązać połączenie. W związku z tym jeśli ma statyczny adres IP dla usługi, które muszą być skonfigurowane na usługę, a nie w usłudze Traffic Manager.

### <a name="does-traffic-manager-support-sticky-sessions"></a>Traffic Manager obsługuje "trwałe" sesje?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na poziomie DNS. Wykorzystuje odpowiedzi DNS, aby kierować klientów do punktu końcowego odpowiednią usługę. Klienci łączą się z punktem końcowym usługi bezpośrednio, nie za pomocą Menedżera ruchu. W związku z tym Menedżer ruchu nie widzi ruch HTTP między klientem a serwerem.

Ponadto źródłowy adres IP zapytanie DNS odebranych przez usługę Traffic Manager należy do usługi DNS cykliczne nie klienta. W związku z tym usługi Traffic Manager nie ma możliwości śledzenia poszczególnych klientów i nie może implementować "trwałe" sesji. To ograniczenie jest wspólny dla wszystkich systemów zarządzania systemem DNS ruch i nie jest specyficzne dla Menedżera ruchu.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>Dlaczego widzę błąd HTTP podczas korzystania z Menedżera ruchu?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na poziomie DNS. Wykorzystuje odpowiedzi DNS, aby kierować klientów do punktu końcowego odpowiednią usługę. Klienci następnie połączyć się z punktem końcowym usługi bezpośrednio, nie za pomocą Menedżera ruchu. Menedżer ruchu nie można znaleźć ruchu HTTP między klientem i serwerem. W związku z tym błędu HTTP widocznej musi pochodzić z aplikacji. Dla klienta w celu połączenia się z aplikacją zakończeniu wszystkich kroków rozpoznawania DNS. Zawierającej interakcji z Menedżera ruchu na przepływie ruchu aplikacji.

Dalsza analiza w związku z tym należy skoncentrować się na aplikacji.

Nagłówek hosta HTTP wysyłane z przeglądarki klienta jest źródłem najbardziej typowych problemów. Upewnij się, że aplikacja jest skonfigurowana do akceptowania nagłówek hosta poprawny dla nazwy domeny, którego używasz. Dla punktów końcowych przy użyciu usługi Azure App Service, zobacz [Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service przy użyciu Menedżera ruchu](../app-service-web/web-sites-traffic-manager-custom-domain-name.md).

### <a name="what-is-the-performance-impact-of-using-traffic-manager"></a>Co to jest jego wpływ na wydajność przy użyciu Menedżera ruchu?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na poziomie DNS. Ponieważ klienci łączą się z punktami końcowymi usługi bezpośrednio, nie jest bez wpływu na wydajność poniesionych podczas korzystania z Menedżera ruchu, po nawiązaniu połączenia.

Ponieważ usługi Traffic Manager integruje się z aplikacjami na poziomie DNS, jest wymagane dodatkowe wyszukiwania DNS, który ma zostać wstawiony do łańcucha rozpoznawania DNS. Wpływ Traffic Manager na czas rozpoznawania nazw DNS jest minimalny. Menedżer ruchu korzysta globalnej sieci serwerów nazw, a [emisji](https://en.wikipedia.org/wiki/Anycast) sieci w celu zapewnienia DNS zapytania zawsze są kierowane do najbliższego serwera dostępnych nazw. Ponadto buforowanie odpowiedzi DNS oznacza, że dodatkowe DNS opóźnień przy użyciu Menedżera ruchu dotyczy tylko część sesji.

Metoda wydajności kieruje ruchem do najbliższego dostępnego punktu końcowego. Wynikiem jest, że wpływ ogólną wydajność skojarzonych z tą metodą powinien być minimalny. Wzrost opóźnienia DNS powinien być przesunięty mniejsze opóźnienia sieci do punktu końcowego.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>Jakie protokoły aplikacji można używać Menedżera ruchu?

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), działanie Menedżera ruchu polega na poziomie DNS. Po wykonaniu wyszukiwania DNS klienci łączą się z punktem końcowym aplikacji bezpośrednio, nie za pomocą Menedżera ruchu. W związku z tym połączenie można użyć dowolnego protokołu aplikacji. Jeśli wybierzesz TCP jako monitorowania protokołu, Menedżera ruchu monitorowania kondycji punktu końcowego mogą być przeprowadzane bez przy użyciu protokołów aplikacji. Jeśli wybierzesz opcję kondycji zweryfikowana przy użyciu protokołu aplikacji, punkt końcowy musi być mogą odpowiadać na żądania HTTP lub HTTPS GET.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>Nazwa domeny "naked" można używać Menedżera ruchu?

Nie. Standardy usługi DNS nie zezwalają na CNAME współistnieć z inne rekordy DNS o takiej samej nazwie. Szczytu (lub głównego) strefy DNS zawsze zawiera dwa rekordy DNS, istniejące; SOA i autorytatywne rekordy NS. Oznacza to, że rekord CNAME nie można utworzyć w wierzchołku strefy bez naruszania standardy usługi DNS.

Menedżer ruchu wymaga rekordu CNAME systemu DNS do mapowania nazwy DNS niestandardowych. Na przykład należy mapować www.contoso.com contoso.trafficmanager.net nazwy DNS profilu Menedżera ruchu. Ponadto profilu usługi Traffic Manager zwraca drugi rekordu CNAME systemu DNS w celu wskazania, który punkt końcowy klient ma nawiązać.

Aby obejść ten problem, firma Microsoft zaleca używanie przekierowania HTTP do bezpośredniego ruchu na podstawie nazwy domeny bez do innego adresu URL, którego można następnie użyć Menedżera ruchu. Na przykład naked domeny "contoso.com" może przekierować użytkowników do CNAME "www.contoso.com", który wskazuje nazwę DNS Menedżera ruchu.

Pełna obsługa naked domen w usłudze Traffic Manager są śledzone w naszym zaległości funkcji. Możesz zarejestrować programu obsługi dla tego żądania funkcji przez [głosowaniu w naszej witrynie opinii społeczności](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly).

### <a name="does-traffic-manager-consider-the-client-subnet-address-when-handling-dns-queries"></a>Menedżer ruchu za adres podsieci klienta podczas obsługi zapytań DNS? 
Nie, obecnie Traffic Manager uwzględnia tylko źródłowy adres IP DNS kwerendę, która zwykle jest adres IP program rozpoznawania nazw DNS podczas przeprowadzania wyszukiwania dla metody routingu Geographic i wydajności.  
W szczególności [7871 RFC — podsieci klienta w zapytaniach DNS](https://tools.ietf.org/html/rfc7871) zapewnia [mechanizmu rozszerzenie dla serwera DNS (EDNS0)](https://tools.ietf.org/html/rfc2671) które można przekazać na adres podsieci klienta z mechanizmów rozpoznawania obsługujących go do serwerów DNS jest obecnie nie jest obsługiwany w Menedżerze ruchu. Możesz zarejestrować programu obsługi dla tego żądania funkcji za pośrednictwem naszego [witrynę opinii społeczności](https://feedback.azure.com/forums/217313-networking).


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>Co to jest czas wygaśnięcia DNS i jak ma ona wpływu na użytkowników?

Jeśli zapytanie DNS wyładowuje w usłudze Traffic Manager, ustawia wartość w odpowiedzi o nazwie czas wygaśnięcia (TTL). Tej wartości, którego jednostka jest w sekundach, wskazuje do rozpoznawania nazw DNS downstream na jak długo buforować odpowiedź. Podczas rozpoznawania nazw DNS nie ma gwarancji pamięci podręcznej tego wyniku, buforowanie ich umożliwia im odpowiadanie na wszystkie kolejne kwerendy poza pamięci podręcznej, zamiast do serwerów DNS Menedżera ruchu. Dotyczy to odpowiedzi w następujący sposób:
- wyższa wartość TTL zmniejsza liczbę zapytań, które na serwery DNS Menedżera ruchu, które można zmniejszyć koszt dla odbiorcy, ponieważ liczba zapytań, obsługiwane jest użycie rozliczeniowy.
- wyższa wartość TTL potencjalnie może skrócić czas potrzebny do wyszukiwania DNS.
- wyższe wartości TTL oznacza także, czy dane nie są widoczne najnowsze informacje o kondycji uzyskiwanej Menedżera ruchu za pośrednictwem jego sondowania agentów.

### <a name="how-high-or-low-can-i-set-the-ttl-for-traffic-manager-responses"></a>Jak wysokie lub niskie można ustawić czas TTL odpowiedzi Menedżera ruchu?

Można ustawić na na poziomie profilu, czas wygaśnięcia DNS być możliwie jak 0 sekund i wysokości 2 147 483 647 sekund (zgodne z maksymalną wielkość zakresu [ze standardem RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). TTL 0 oznacza, że podrzędne rozpoznawania nazw DNS nie buforowanie odpowiedzi na kwerendy, wszystkie zapytania mogą uzyskać dostęp do usługi Traffic Manager w systemie DNS i serwerów rozpoznawania.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Metody routingu ruchu Geographic Menedżera ruchu

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>Co to są niektórych przypadków użycia, w którym geograficzne routing jest przydatne? 
Geograficzne typ routingu może służyć w jakimkolwiek scenariuszu których Azure klienta wymaga rozróżnienia użytkowników oparte na regionów geograficznych. Na przykład przy użyciu metody routingu ruchu geograficznych, użytkownicy mogli z określonych regionów różnych użytkowników z innych regionów niż. Innym przykładem jest zgodne z oczekuje suwerenności danych lokalnych, wymagających, że użytkownicy z określonego regionu obsługiwane tylko przez punkty końcowe w tym regionie.

### <a name="what-are-the-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>Co to są regionów, które są obsługiwane przez usługę Traffic Manager geograficzne routingu? 
Hierarchii kraj/region, jaka jest używana przez usługę Traffic Manager można znaleźć [tutaj](traffic-manager-geographic-regions.md). Gdy ta strona jest aktualizowany o zmianach, można również programowane pobieranie tych samych informacji za pomocą [Azure Traffic Manager REST API](https://docs.microsoft.com/rest/api/trafficmanager/). 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>Jak usługi traffic manager ustalić, gdzie pyta użytkownika z? 
Menedżer ruchu sprawdza źródłowy adres IP zapytania (prawdopodobnie jest to lokalnego rozpoznawania nazw DNS wykonywania zapytań w imieniu użytkownika) i używa wewnętrznego adresu IP do obszaru mapy w celu określenia lokalizacji. Ta mapa jest aktualizowane na bieżąco, aby uwzględnić zmiany w Internecie. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-the-exact-geographic-location-of-the-user-in-every-case"></a>Jest on gwarantowane czy Menedżera ruchu można prawidłowo określić dokładnej lokalizacji geograficznej użytkownika w każdym przypadku
Nie, Traffic Manager nie może zagwarantować, że region geograficzny, które firma Microsoft wywnioskować z adresu IP źródłowego zapytania DNS zawsze odpowiada lokalizacji użytkownika z następujących powodów: 

- Po pierwsze zgodnie z opisem w poprzedniej odpowiedzi na pytanie, źródłowy adres IP, które przedstawiono jest który program rozpoznawania nazw DNS podczas wyszukiwania w imieniu użytkownika. Lokalizacja geograficzna program rozpoznawania nazw DNS jest dobrym serwera proxy dla lokalizacji geograficznej użytkownika, również można różne w zależności od rozmiaru usługi rozpoznawania nazw DNS i określonych usługa rozpoznawania nazw DNS, który klient ma wybranego do użycia. Na przykład klient znajduje się w Malezji można określić w ich urządzenia należy użyć ustawienia usługi rozpoznawania nazw DNS, których serwer DNS w Singapurze może pobrać wybierany do obsługi rozwiązania zapytania dla tego użytkownika/urządzenie. W takim przypadku Menedżera ruchu może zobaczyć tylko mechanizm rozpoznawania adresu IP, który odpowiada lokalizacji Singapuru. Zobacz też wcześniejszych — często zadawane pytania dotyczące pomocy technicznej adres podsieci klienta na tej stronie.

- Drugie usługi Traffic Manager używa wewnętrznego mapy do wykonywania adres IP do tłumaczenia regionu geograficznego. Ta mapa jest weryfikowane i aktualizowane na bieżąco, aby zwiększyć jego dokładność oraz konto dla charakter zmieniające się przez internet, nadal jest możliwość, że nasze informacje nie są dokładnie reprezentację lokalizację geograficzną wszystkich IP adresy.


###  <a name="does-an-endpoint-need-to-be-physically-located-in-the-same-region-as-the-one-it-is-configured-with-for-geographic-routing"></a>Czy punkt końcowy musi się znajdować w tym samym regionie, który jest konfigurowana dla routingu geograficzne? 
Nie, lokalizacja punktu końcowego nakłada żadnych ograniczeń, na których regionach mogą być mapowane do niego. Na przykład punkt końcowy w regionie Azure środkowe stany USA mają wszyscy użytkownicy z Indie skierowane do niego.

### <a name="can-i-assign-geographic-regions-to-endpoints-in-a-profile-that-is-not-configured-to-do-geographic-routing"></a>Regionów geograficznych można przypisać do punktów końcowych w profil, który nie jest skonfigurowany do czy routingu geograficzne? 

Tak, jeśli metoda routingu profilu nie jest geograficznej, możesz użyć [interfejsu REST API usługi Traffic Manager Azure](https://docs.microsoft.com/rest/api/trafficmanager/) można przypisać regionów geograficznych do punktów końcowych w tym profilu. W przypadku profilów typu routingu-geograficznego ta konfiguracja jest ignorowana. Jeśli zmienisz takiego profilu geograficznego typ routingu w późniejszym czasie, Traffic Manager można użyć tych mapowania.


### <a name="why-am-i-getting-an-error-when-i-try-to-change-the-routing-method-of-an-existing-profile-to-geographic"></a>Dlaczego otrzymuję błąd przy próbie Zmień metodę routingu istniejącego profilu Geographic?

Wszystkie punkty końcowe przy użyciu profilu geograficznego routingu musi być co najmniej jeden region mapowane. Aby przekonwertować istniejącego profilu geograficznego typ routingu, najpierw należy skojarzyć regionach geograficznych, aby wszystkie jego punktów końcowych przy użyciu [interfejsu REST API usługi Traffic Manager Azure](https://docs.microsoft.com/rest/api/trafficmanager/) przed zmianą typu routingu geograficznych. Jeśli za pomocą portalu, należy najpierw usunąć punkty końcowe, zmień metodę routingu profil geograficzny, a następnie dodaj punkty końcowe wraz z ich mapowania regionu geograficznego. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>Dlaczego jest zalecane użytkownikom utworzenie zagnieżdżonych profilów zamiast punktów końcowych przy użyciu profilu z włączonym routingiem geograficzne? 

Region można przypisać do tylko jeden punkt końcowy w profilu, jeśli jego przy użyciu geograficzne typu routingu. Jeśli ten punkt końcowy nie jest typem zagnieżdżonym z profilem podrzędnych dołączonych do niego, jeśli ruch tego punktu końcowego, przechodząc w złej kondycji, Menedżer nadal do wysyłania ruchu do niego od alternatywnej nie wysyłać cały ruch nie jest żadnym lepiej. Menedżer ruchu nie nie trybu failover do innego punktu końcowego, nawet w przypadku, gdy region przypisany jest "nadrzędnej" region przypisany do punktu końcowego, który zakończył się zła, (na przykład jeśli punktu końcowego, który ma Hiszpanii region przechodzi w złej kondycji, firma Microsoft będzie nie trybu failover do innego punktu końcowego mający regionie, w którym Europy przypisane do niej). Można to zrobić, aby upewnić się, że Menedżer ruchu szanuje granice geograficzne, że klient ma ustawienia w swoim profilu. Aby skorzystać z zalet awarii do innego punktu końcowego, gdy punkt końcowy złej kondycji, zalecane jest przypisania regionów geograficznych zagnieżdżonych profilów z wieloma punktami końcowymi w nim zamiast poszczególnych punktów końcowych. W przypadku niepowodzenia punktu końcowego w profilu zagnieżdżonych elementów podrzędnych ruchu w ten sposób można trybu failover do innego punktu końcowego w ramach tego samego profilu zagnieżdżonych elementów podrzędnych.

### <a name="are-there-any-restrictions-on-the-api-version-that-supports-this-routing-type"></a>Czy istnieją ograniczeń z wersją interfejsu API, który obsługuje ten typ routingu?

Tak, tylko wersja interfejsu API 2017-03-01 i nowszej obsługuje routing geograficzne typu. Starsze wersje interfejsu API nie może służyć do utworzone profile geograficzne typ routingu lub przypisać regionów geograficznych do punktów końcowych. Jeśli starszej wersji interfejsu API jest używany do pobierania profile z subskrypcją platformy Azure, dowolny profil geograficzny typ routingu nie są zwracane. Ponadto przy użyciu starszej wersji interfejsu API dowolny profil zwrócił który ma punkty końcowe z przypisaniem region geograficzny, nie ma jej przypisanie regionu geograficznego pokazano.



## <a name="traffic-manager-endpoints"></a>Punkty końcowe usługi Traffic Manager

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>Z punktami końcowymi z wieloma subskrypcjami można używać Menedżera ruchu?

Za pomocą punktów końcowych z wieloma subskrypcjami nie jest możliwe z aplikacjami sieci Web platformy Azure. Aplikacje sieci Web platformy Azure wymaga dowolną nazwę domeny niestandardowej, używany w aplikacjach sieci Web jest używana tylko w ramach jednej subskrypcji. Nie jest możliwe korzystanie z aplikacji sieci Web z wieloma subskrypcjami z tą samą nazwą domeny.

Dla innych typów punktu końcowego jest możliwe za pomocą Menedżera ruchu z punktami końcowymi z więcej niż jedną subskrypcję. W Menedżerze zasobów punktów końcowych z dowolnej subskrypcji można dodać do usługi Traffic Manager, tak długo, jak osoby konfigurowania profilu usługi Traffic Manager ma dostęp do odczytu do punktu końcowego. Te uprawnienia można otrzymać za pomocą [usługi Azure Resource Manager kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md).


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>Czy można używać Menedżera ruchu z miejsc "Przemieszczania" usługi w chmurze?

Tak. Usługi w chmurze przemieszczania gniazda można skonfigurować w usłudze Traffic Manager jako zewnętrzne punkty końcowe. Kontrole kondycji nadal są naliczane opłaty szybkością punkty końcowe platformy Azure. Ponieważ typu zewnętrznego punktu końcowego jest używana, zmiany w usłudze podstawowych nie są odczytywane automatycznie. Z zewnętrzne punkty końcowe Traffic Manager nie może wykryć po zatrzymaniu usługa w chmurze lub usunąć. W związku z tym Menedżer ruchu nadal rozliczenia dotyczące sprawdzania kondycji, aż do punktu końcowego zostało wyłączone lub usunięte.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>Traffic Manager obsługuje punktów końcowych protokołu IPv6?

Menedżer ruchu nie ma obecnie IPv6 addressible serwerów nazw. Jednak Menedżera ruchu, mogą nadal używane przez klientów IPv6 łączących się z punktami końcowymi protokołu IPv6. Klient nie powoduje żądania DNS bezpośrednio do usługi Traffic Manager. Zamiast tego klient korzysta z usługi DNS cyklicznego. Tylko protokół IPv6 klienta wysyła żądania do usługi DNS cykliczne za pośrednictwem protokołu IPv6. Następnie usługa cykliczne powinno być możliwe do kontaktowania się z serwerów nazw usługi Traffic Manager przy użyciu protokołu IPv4.

Menedżer ruchu odpowiada o nazwie DNS punktu końcowego. Do obsługi punktu końcowego protokołu IPv6, musi istnieć rekord AAAA usługi DNS wskazuje nazwę DNS punkt końcowy adres IPv6. Kontrole kondycji usługi Traffic Manager obsługuje tylko adresy IPv4. Usługa musi ujawniać punkt końcowy IPv4 na tej samej nazwy DNS.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-the-same-region"></a>Z więcej niż jednej aplikacji sieci Web w tym samym regionie można używać Menedżera ruchu?

Zazwyczaj Menedżera ruchu jest używany do kierowania ruchem danych do aplikacji wdrożonych w różnych regionach. Jednak może również służyć, gdzie ma więcej niż jedno wdrożenie aplikacji w tym samym regionie. Punkty końcowe usługi Azure Traffic Manager zezwala na więcej niż jeden punkt końcowy aplikacji sieci Web z tego samego regionu Azure, które mają zostać dodane do tego samego profilu Menedżera ruchu.

##  <a name="traffic-manager-endpoint-monitoring"></a>Monitorowanie punktu końcowego Menedżera ruchu

### <a name="is-traffic-manager-resilient-to-azure-region-failures"></a>Menedżer ruchu jest odporność na awarie region platformy Azure?

Menedżer ruchu jest kluczowym składnikiem dostarczania wysoką dostępność aplikacji na platformie Azure.
Aby zapewnić wysoką dostępność, Traffic Manager musi mieć wyjątkowo wysoki poziom dostępności i zapewnienie odporności na awarie regionalne.

Zgodnie z projektem składniki usługi Traffic Manager są odporności na awarie pełną żadnych regionu Azure. Odporność to ma zastosowanie do wszystkich składników usługi Traffic Manager: nazw DNS, serwery, interfejsu API warstwy magazynu i monitorowanie usługi punktu końcowego.

Na wypadek wystąpienia awarii całego regionu Azure Traffic Manager powinien nadal działać normalnie. Aplikacje wdrożone w wielu regionach platformy Azure może polegać na Menedżera ruchu do kierowania ruchem danych do dowolnego dostępnego wystąpienia aplikacji.

### <a name="how-does-the-choice-of-resource-group-location-affect-traffic-manager"></a>Jak wybór lokalizacji grupy zasobów wpływa Menedżera ruchu?

Menedżer ruchu jest pojedyncza usługa globalnego. Nie ma charakteru regionalnego. Wybór lokalizacji grupy zasobów nie ma wpływu na profilów usługi Traffic Manager wdrożonych w tej grupie zasobów.

Usługa Azure Resource Manager wymaga wszystkich grup zasobów określić lokalizację, który określa domyślną lokalizację zasoby wdrożone w tej grupie zasobów. Po utworzeniu profilu Menedżera ruchu jest tworzony w grupie zasobów. Użyj wszystkich profilów usługi Traffic Manager **globalne** jako ich lokalizacji, Zastępowanie domyślnego grupy zasobów.

### <a name="how-do-i-determine-the-current-health-of-each-endpoint"></a>Jak określającymi bieżącą kondycję każdego punktu końcowego?

Bieżący stan monitorowania każdego punktu końcowego, oprócz ogólną profil jest wyświetlana w portalu Azure. Te informacje są również dostępne za pośrednictwem Monitora ruchu [interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163667.aspx), [poleceń cmdlet programu PowerShell](https://msdn.microsoft.com/library/mt125941.aspx), i [wiersza polecenia platformy Azure i platform](../cli-install-nodejs.md).

Azure nie zapewnia informacje historyczne na temat poprzednich kondycji punktu końcowego lub możliwości, aby zgłaszał alerty dotyczące zmiany kondycji punktu końcowego.

### <a name="can-i-monitor-https-endpoints"></a>Można monitorować punktów końcowych HTTPS?

Tak. Traffic Manager obsługuje sondowanie za pośrednictwem protokołu HTTPS. Skonfiguruj **HTTPS** jako protokół w konfiguracji monitorowania.

Menedżer ruchu nie może dostarczyć żadnych weryfikacji certyfikatu w tym:

* Po stronie serwera, certyfikaty nie są weryfikowane.
* Funkcja SNI po stronie serwera certyfikatów nie są obsługiwane.
* Certyfikaty klienta nie są obsługiwane.

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>Czy można użyć Menedżera ruchu, nawet jeśli Moja aplikacja nie ma obsługi protokołu HTTP lub HTTPS?

Tak. Można określić monitorowania protokołu TCP i usługi Traffic Manager można inicjować połączenie TCP i oczekiwania na odpowiedź z punktu końcowego. Jeśli punkt końcowy odpowiada na żądania połączenia za pomocą odpowiedzi do nawiązania połączenia, przed upływem limitu czasu, tego punktu końcowego jest oznaczona jako w dobrej kondycji.

### <a name="what-specific-responses-are-required-from-the-endpoint-when-using-tcp-monitoring"></a>Jakie określone odpowiedzi są wymagane z punktu końcowego, korzystając z protokołu TCP monitorowania?

Podczas monitorowania TCP jest używany, usługi Traffic Manager uruchamia TCP trójstopniowego poprzez wysłanie żądania SYN punkt końcowy pod adresem określonego portu. Następnie czeka na pewien czas (jak określono w ustawieniach limitu czasu) na odpowiedź z punktu końcowego. Jeśli punkt końcowy odpowiada na żądania SYN za pomocą SYN ACK odpowiedzi przed upływem limitu czasu określonego w ustawieniach monitorowania, następnie tego punktu końcowego jest traktowany jako dobrej kondycji. Odebranie odpowiedzi potwierdzenia SYN Traffic Manager resetuje połączenie odpowiedzi z powrotem RST.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>Szybkość Menedżera ruchu przenieść mój użytkowników zła punktu końcowego?

Menedżer ruchu udostępnia wiele ustawień, które ułatwiają kontrolowanie zachowania pracy awaryjnej w profilu usługi Traffic Manager w następujący sposób:
- można określić, że Menedżer ruchu sondy punkty końcowe częściej przez ustawienie interwału sondowania na 10 sekund. Dzięki temu, jak najszybciej wykryto dowolnego punktu końcowego, przechodząc w złej kondycji. 
- można określić, jak długo czekać przed kondycję wyewidencjonować razy żądanie (wartość minimalna limit czasu to 5 s).
- można określić, ile błędów mogą wystąpić, zanim punkt końcowy jest oznaczony jako w złej kondycji. Ta wartość może być niski jako 0, w których przypadku punkt końcowy jest oznaczony jako niepoprawny zaraz po awarii pierwszego sprawdzania kondycji. Jednak przy użyciu minimalnej wartości 0 dla tolerowaną liczba błędów może prowadzić do punktów końcowych przełączana poza obrotu z powodu przejściowych problemów, które mogą wystąpić podczas badania.
- czas wygaśnięcia (TTL) można określić dla odpowiedź DNS do brakować jako 0. Grozi to oznacza, że programy rozpoznawania nazw DNS nie można buforować odpowiedzi i każdego nowego zapytania pobiera odpowiedź, który zawiera najbardziej aktualne informacje kondycji z Menedżera ruchu.

Przy użyciu tych ustawień, Traffic Manager zapewnia tryb failover poniżej 10 sekund po punkt końcowy przechodzi złej kondycji i zapytanie DNS staje się przed odpowiedni profil.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>Jak określić różne ustawienia monitorowania dla różnych punktów końcowych w profilu

Ustawienia monitorowania są Menedżera ruchu na poziomie profilu. Jeśli musisz użyć różnych ustawienia monitorowania dla tylko jeden punkt końcowy może odbywać dzięki użyciu tego punktu końcowego jako [zagnieżdżone profilu](traffic-manager-nested-profiles.md) którego ustawienia monitorowania różnią się od profilu nadrzędnej.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>Jakie hosta nagłówka punktu końcowego kondycji sprawdza użycie?

Menedżer ruchu używa nagłówków hosta kontroli kondycji HTTP i HTTPS. Nagłówek hosta używane przez Menedżera ruchu jest nazwą elementu docelowego punktu końcowego skonfigurowane w profilu. Wartość nagłówka hosta nie można określić osobno z właściwością target.

### <a name="what-are-the-ip-addresses-from-which-the-health-checks-originate"></a>Co to są adresy IP, z których pochodzą sprawdza kondycję?

Poniższa lista zawiera adresy IP, z których mogą pochodzić sprawdza kondycji usługi Traffic Manager. Może Użyj tej listy, aby upewnić się, że połączenia przychodzące z tych adresów IP są dozwolone w punktach końcowych sprawdzić jej stan kondycji.

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

### <a name="how-many-health-checks-to-my-endpoint-can-i-expect-from-traffic-manager"></a>Ile kontroli kondycji do mojego punktu końcowego można spodziewać się z Menedżera ruchu?

Liczba kondycji usługi Traffic Manager sprawdza, czy osiągnięciu punktu końcowego zależy od następujących czynników:
- wartość ustawioną dla interwał monitorowania (mniejszego oznacza więcej żądań kierowanych na punkt końcowy w dowolnym okresie w danym momencie).
- Liczba lokalizacji, z którego kontroli kondycji pochodzą (adresy IP, z których można oczekiwać, że kontrole jest wymieniony w poprzednim — często zadawane pytania).

## <a name="traffic-manager-nested-profiles"></a>Profile zagnieżdżone Menedżera ruchu

### <a name="how-do-i-configure-nested-profiles"></a>Jak skonfigurować zagnieżdżonych profilów?

Zagnieżdżonych profilów usługi Traffic Manager można skonfigurować przy użyciu zarówno usługi Azure Resource Manager i klasycznym Azure interfejsów API REST, poleceń cmdlet programu Azure PowerShell i polecenia wiersza polecenia platformy Azure i platform. Są one również obsługiwane za pośrednictwem portalu Azure. Nie są obsługiwane w klasycznym portalu.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>Obsługuje liczbę warstw zagnieżdżenia wykonuje Menedżera ruchu?

Można zagnieżdżać profile maksymalnie 10 poziomów w głąb. "Pętli" są niedozwolone.

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-the-same-traffic-manager-profile"></a>Czy można mieszać inne typy punktów końcowych przy użyciu profilów zagnieżdżonych elementów podrzędnych, w tym samym profilu Menedżera ruchu

Tak. Nie ma żadnych ograniczeń na jak łączyć punktów końcowych różnych typów w profilu.

### <a name="how-does-the-billing-model-apply-for-nested-profiles"></a>Jak modelu rozliczeń stosowane profilów zagnieżdżone?

Nie ma nie ujemna cennik wpływ przy użyciu zagnieżdżonych profilów.

Karta usługi Traffic Manager zawiera dwa składniki: kontroli kondycji punktu końcowego i miliony zapytań DNS

* Kontroli kondycji punktu końcowego: bez dodatkowych opłat profilu podrzędnych skonfigurowane jako punktu końcowego w profilu nadrzędny nie istnieje. Monitorowania punktów końcowych w profilu podrzędnych jest on rozliczany w zwykły sposób.
* Zapytania DNS: każdego zapytania są traktowane jako jeden raz. Zapytanie profil nadrzędnego, który zwraca punkt końcowy z profilu podrzędnych jest uwzględniane w profilu nadrzędnej.

Aby uzyskać szczegółowe informacje, zobacz [cennikiem usługi Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>Czy istnieje negatywny wpływ na wydajność zagnieżdżonych profilów?

Nie. Nie ma żadnego wpływu wydajności, poniesionych przy użyciu zagnieżdżonych profilów.

Serwery nazw Menedżera ruchu przechodzenie przez hierarchię profilu wewnętrznie podczas przetwarzania każdego zapytania DNS. Zapytanie DNS do profilu nadrzędnej można otrzymywać odpowiedź DNS z punktem końcowym profilu podrzędnych. Pojedynczy rekord CNAME jest używany zarówno w przypadku korzystania w jednym profilu lub profilach zagnieżdżonych. Nie istnieje potrzeba aby utworzyć rekord CNAME dla każdego profilu w hierarchii.

### <a name="how-does-traffic-manager-compute-the-health-of-a-nested-endpoint-in-a-parent-profile"></a>Jak usługi Traffic Manager obliczeniowe kondycji zagnieżdżonych punktu końcowego w profilu nadrzędnego?

Profil nadrzędnego nie sprawdzania kondycji w elemencie podrzędnym bezpośrednio. Zamiast tego kondycji profilu podrzędnych punktów końcowych są używane do obliczenia ogólnej kondycji profilu podrzędnych. Te informacje są propagowane w górę hierarchii profilu zagnieżdżone ustalenie kondycji zagnieżdżonych punktu końcowego. Profil nadrzędnego używa tego zagregowane kondycji do określenia, czy ruch może zostać skierowany do podrzędnych.

W poniższej tabeli opisano zachowanie z Menedżera ruchu kondycji sprawdza, czy punkt końcowy zagnieżdżonych.

| Stan monitora profilowania podrzędne | Stan punktu końcowego Monitor nadrzędny | Uwagi |
| --- | --- | --- |
| Wyłączone. Wyłączono profil podrzędnych. |Zatrzymane |Stan punktu końcowego nadrzędnego jest zatrzymana, nie jest wyłączone. Stanem wyłączono jest zarezerwowana dla wskazujący wyłączono punktu końcowego w profilu nadrzędnej. |
| Nieprawidłowe działanie. Co najmniej jeden element podrzędny punktu końcowego profilu jest w stanie obniżony. |Online: liczba Online punktów końcowych w profilu podrzędnych jest co najmniej wartość MinChildEndpoints.<BR>CheckingEndpoint: liczba Online oraz CheckingEndpoint punktów końcowych w profilu podrzędnych jest co najmniej wartość MinChildEndpoints.<BR>Ograniczone: inaczej. |Ruch jest kierowany do stanu CheckingEndpoint punktu końcowego. Jeśli zostanie ustawiona zbyt wysoka MinChildEndpoints, punkt końcowy jest zawsze znacznie mniej wydajna. |
| W trybie online. Co najmniej jeden element podrzędny punktu końcowego profilu jest w stanie Online. Żaden punkt końcowy jest w stanie obniżony. |Zobacz powyżej. | |
| CheckingEndpoints. Co najmniej jeden element podrzędny punktu końcowego profilu jest "CheckingEndpoint". Brak punktów końcowych są "Online" lub "Ze spadkiem" |Taka sama jak powyżej. | |
| Nieaktywne. Wszystkie punkty końcowe profilu podrzędne są wyłączone lub zatrzymana lub ten profil nie ma punktów końcowych. |Zatrzymane | |

## <a name="next-steps"></a>Następne kroki:
- Dowiedz się więcej o Menedżerze ruchu [punkt końcowy monitorowania i automatycznej pracy awaryjnej](../traffic-manager/traffic-manager-monitoring.md).
- Dowiedz się więcej o Menedżerze ruchu [metody routingu ruchu](../traffic-manager/traffic-manager-routing-methods.md).