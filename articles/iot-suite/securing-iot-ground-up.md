---
title: "aaaSecuring z Internetu rzeczy z hello tła w górę | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello wbudowanych funkcji zabezpieczeń hello pakiet IoT Microsoft Azure"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 10252dfa-8313-4a97-9bd6-a3f1345dd3be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: a97e8cea753641e1e3c895f44e3fde1e5739d665
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-from-hello-ground-up"></a>Zabezpieczeń Internetu rzeczy z hello tła w
Witaj Internetu rzeczy (IoT) stanowi unikatowy zabezpieczeń, prywatności i zgodności wyzwania toobusinesses na całym świecie. W przeciwieństwie do tradycyjnych przez technologii gdzie te problemy koncentrują się wokół oprogramowania i jak jest implementowane IoT dotyczy, co się stanie po hello ataków i hello względem fizycznego łączenia. Ochrona rozwiązania IoT wymaga zapewnienia bezpiecznego inicjowania obsługi urządzeń i bezpieczna łączność między tymi urządzeniami i chmury hello i ochronę danych w chmurze hello podczas przetwarzania i przechowywania. Jednak działać z takich funkcji, są ograniczone zasobów urządzeń, rozmieszczenie geograficzne wdrożeń i dużej liczby urządzeń w ramach rozwiązania.

Ten artykuł opisuje sposób hello pakiet IoT Microsoft Azure oferuje bezpieczeństwo i prywatność rozwiązanie chmury Internetu rzeczy. Hello pakiet IoT Azure zapewnia kompleksowe rozwiązanie end-to-end przy zabezpieczeń wbudowanych w każdym etapie z hello tła w. W firmie Microsoft, opracowywanie bezpiecznego oprogramowania jest częścią hello oprogramowanie inżynieryjne rozwiązaniem, umieszczone w naszym dekad długo środowisko rozwoju oprogramowania bezpieczne. tooensure, metodologii podstawowych programowanie hello, w połączeniu z hostem usługi zabezpieczeń na poziomie infrastruktury, takie jak operacyjnej gwarancji bezpieczeństwa (OSA) i hello Microsoft jednostki, jest Security Development Lifecycle (SDL) Microsoft Security Response Center, a w Centrum ochrony przed złośliwym oprogramowaniem firmy Microsoft. 

Witaj pakiet IoT Azure oferuje unikatowe funkcje tego programu, inicjowania obsługi administracyjnej, nawiązywanie połączenia i przechowywanie danych z urządzeń IoT łatwe i przejrzysty i najbardziej, bezpieczna. W tym artykule omówione funkcje zabezpieczeń hello pakiet IoT Azure i są opisane strategie tooensure zabezpieczeń, prywatności i zgodności związane z wdrożeniem. 

## <a name="introduction"></a>Wprowadzenie
Hello Internetu rzeczy (IoT) jest hello rzutu hello przyszłych oferty firmy natychmiastowego i możliwości rzeczywistych kosztów tooreduce, zwiększyć przychody i przekształcanie firmy. Wiele firm są jednak wątpliwości toodeploy IoT w organizacjach z powodu tooconcerns dotyczące zabezpieczeń, prywatności i zgodności. Główne punktu potencjalnie pochodzi z unikatowości hello hello IoT infrastruktury, który łączy przez hello i względem fizycznego łączenia poszczególnych ryzyko związane z tych dwóch względem razem. Zabezpieczenia IoT dotyczy tooensuring hello integralności kodu działające na urządzeniach, zapewniając uwierzytelniania użytkowników i urządzeń, definiowanie wyczyść własność urządzeń (a także dane generowane przez te urządzenia) i jest toocyber odporne i fizycznym. 

Następnie jest problem hello zasad zachowania poufności informacji. Firmach przezroczystość dotyczące zbierania danych, w jakie zbierane i do czego, którzy mogą przeglądać go, która kontroluje dostęp i tak dalej. Ponadto istnieją problemów występujących w ogólne bezpieczeństwo urządzeń hello wraz z osób hello ich działania i utrzymania standardy branżowe zgodności.

Biorąc pod uwagę hello zabezpieczeń, ochrony prywatności, przezroczystość i dotyczy zgodności, wybieranie dostawcy rozwiązania IoT prawo hello pozostaje żądanie. Łączenia ze sobą poszczególne IoT oprogramowania i usług świadczonych przez różnych dostawców wprowadza luk w zabezpieczeń, ochrony prywatności, przezroczystość i zgodności, które mogą być twarde toodetect nawet rozwiązać. Wybór Hello prawo hello IoT dostawcy oprogramowania i usługa jest oparta na wyszukiwanie dostawców ma zbiorczych doświadczeń uruchamiania usług, które obejmują w przypadkach i lokalizacji geograficznych, ale jest również możliwe tooscale w sposób bezpieczny i przezroczysty. Podobnie, pomaga uzyskać hello wybrany dostawca toohave dekad dzięki opracowywania oprogramowania bezpiecznego uruchomionego na ogromną maszyn na całym świecie, oraz mieć hello możliwości tooappreciate hello zagrożeń spowodowane tego nowego world hello Internet z Rzeczy.

## <a name="secure-infrastructure-from-hello-ground-up"></a>Zabezpieczanie infrastruktury z hello tła w
Witaj [Microsoft Cloud](https://www.microsoft.com/enterprise/microsoftcloud/default.aspx#fbid=WzBsRQi6aGk) infrastruktury obsługuje więcej niż 1 miliard klientów w krajach 127. Rysowanie na naszym doświadczeniu long dekad tworzenia oprogramowania korporacyjnego i uruchamiania niektórych hello największy usług online w hello world, udostępniamy wyższego poziomu zwiększonych zabezpieczeń, ochrony prywatności, zgodności i zagrożeń rozwiązań środki zaradcze niż większość klientów może osiągnięcia samodzielnie.

Nasze [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/) udostępnia proces obowiązkowe programowanie całej firmy, który osadza wymagania dotyczące zabezpieczeń w cyklu życia oprogramowania całego hello. toohelp upewnij się, że działania operacyjne wykonaj hello tym samym poziomie praktyk związanych z zabezpieczeniami, korzystamy z zasadami bezpieczeństwa rygorystyczne w procesu operacyjnej gwarancji bezpieczeństwa (OSA). Ponadto współpracujemy z innych firm inspekcji przedsiębiorstwa bieżących weryfikacji możemy naszych zobowiązań zgodności, czy możemy prowadzenia działań szerokie zabezpieczeń poprzez tworzenie hello centrów doskonałości, w tym hello Microsoft jednostki, Microsoft Security Centrum odpowiedzi, a w Centrum ochrony przed złośliwym oprogramowaniem firmy Microsoft.

## <a name="microsoft-azure---secure-iot-infrastructure-for-your-business"></a>Microsoft Azure - bezpiecznej infrastruktury IoT dla biznesu
Microsoft Azure oferuje rozwiązania pełnej chmury, który łączy stale rosnącego zbiór usług w chmurze zintegrowane — analytics, machine learning, magazynu, zabezpieczeń, sieci i sieci web — z branży zobowiązań toohello ochrony i ochrona prywatności danych. Nasze [założono naruszenia](https://azure.microsoft.com/blog/red-teaming-using-cutting-edge-threat-simulation-to-harden-the-microsoft-enterprise-cloud/) strategii używa dedykowanego "red zespołu" ekspertów zabezpieczeń oprogramowania, którzy symulować ataków, testowanie możliwości hello Azure toodetect ochrony przed zagrożeniami i odzyskanie naruszeń. Nasze [odpowiedzi na zdarzenia globalne](https://www.microsoft.com/TrustCenter/Security/DesignOpSecurity) działania zespołu wokół hello zegara toomitigate hello skutki ataków i złośliwych działań. zespołu Hello wykonuje określone procedury zarządzania zdarzeniami, komunikację i odzyskiwania, a następnie używa interfejsów wykrywalny i przewidywalne partnerom wewnętrznych i zewnętrznych.

Naszych systemów zapewniają ciągłego włamań i zapobiegania, zapobieganie atakom usługi, penetracji regularne testowania i śledczej narzędzi, które pomagają zidentyfikować i uniknięcie zagrożeń. [Uwierzytelnianie wieloskładnikowe](../multi-factor-authentication/multi-factor-authentication.md) zapewnia dodatkową warstwę zabezpieczeń dla użytkowników końcowych tooaccess hello sieci. I dla aplikacji hello i dostawcy hosta hello oferujemy kontroli dostępu, monitorowanie przed złośliwym oprogramowaniem, skanowanie luki w zabezpieczeniach, poprawki i zarządzanie konfiguracją.

Witaj pakiet IoT Microsoft Azure wykorzystuje hello zabezpieczeń i prywatności wbudowane hello platformy Azure, wraz z naszych SDL i OSA procesów związanych z bezpieczeństwem programowania i działania oprogramowania firmy Microsoft. Te procedury Podaj ochrony infrastruktury, ochrony sieci i tożsamości, zarządzania i zabezpieczeń toohello podstawowych funkcji od wszelkich rozwiązań. 

Witaj [Centrum IoT Azure](../iot-hub/iot-hub-what-is-iot-hub.md) w hello [pakiet IoT](iot-suite-what-is-azure-iot.md) oferuje w pełni zarządzaną usługę i niezawodności dwukierunkową komunikację między urządzeniami IoT i usług Azure, takich jak [Usługi azure Machine Learning](../machine-learning/machine-learning-what-is-machine-learning.md) i [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) przy użyciu poświadczeń zabezpieczeń urządzenia i kontrola dostępu.

toobest komunikacji funkcje zabezpieczeń i prywatności, które są wbudowane w hello pakiet IoT Azure, możemy zostały podzielone suite hello na trzy obszary głównej zabezpieczeń hello. 

![Pakiet IoT Azure](media/securing-iot-ground-up/securing-iot-ground-up-fig3.png)

### <a name="secure-device-provisioning-and-authentication"></a>Zabezpieczenia, inicjowanie obsługi administracyjnej urządzeń i uwierzytelniania
Hello pakiet IoT Azure chroni urządzenia, gdy są one się w polu hello podając unikatową tożsamość klucz dla każdego urządzenia, które mogą być używane przez hello IoT infrastruktury toocommunicate z urządzeniem hello podczas operacji. proces Hello jest szybkie i łatwe tooset w górę. Witaj wygenerowany klucz na bazie hello wybrane przez użytkownika urządzenia identyfikator formularze używane w cała komunikacja między urządzeniem hello i hello Azure IoT Hub tokenu.

Identyfikatory urządzeń mogą być skojarzone z urządzeniem podczas produkcji (tj. zainstalowany w module zaufania sprzętu) lub można użyć istniejącego stałej tożsamości jako serwer proxy (na przykład numery seryjne Procesora). Ponieważ zmiana ta informacje identyfikacyjne na urządzeniu hello nie jest proste, jest ważne toointroduce urządzenia logicznego identyfikatorów w przypadku hello podstawowej zmiany sprzętowe urządzenia, ale pozostaje urządzenia logicznego hello hello takie same. W niektórych przypadkach hello skojarzenie tożsamości urządzenia może nastąpić podczas wdrażania urządzenia (tj. inżyniera uwierzytelnionego pola fizycznie konfiguruje nowego urządzenia podczas komunikacji z zapleczem rozwiązania hello). Witaj [rejestru tożsamości Centrum IoT Azure](../iot-hub/iot-hub-devguide.md) zapewnia bezpieczne przechowywanie tożsamości urządzenia i kluczy zabezpieczeń dla rozwiązania. Osoby lub grupy tożsamości urządzenia można dodać tooan Zezwalaj listy lub listę zablokowanych umożliwiające pełną kontrolę nad uzyskiwania dostępu do urządzenia.

Zasady kontroli dostępu Centrum IoT Azure w chmurze hello włączyć aktywacji i wyłączanie tożsamości urządzenia, zapewniając toodisassociate sposób urządzenia z wdrożenia IoT, gdy jest to wymagane. To skojarzenie i usuwanie skojarzeń urządzenia jest oparta na tożsamości każdego urządzenia.

Funkcje zabezpieczeń dodatkowe urządzenia hello następujące czynności:

* Urządzenia nie akceptują połączeń sieciowych niepożądane. Nawiązaniu wszystkie połączenia i tras w sposób tylko ruchu wychodzącego. Dla tooreceive urządzenia polecenie z poziomu zaplecza hello hello urządzenia muszą inicjować toocheck połączenia dla dowolnego tooprocess oczekującego polecenia. Po bezpiecznie nawiązaniu połączenia między urządzeniem hello a Centrum IoT wiadomości powitania chmury toohello urządzenia i urządzenia toohello chmury mogą być wysyłane przezroczysty.  
* Tylko łączenia urządzeń tooor ustanowić usług znane toowell trasy z których one są połączyć za pomocą, takich jak Azure IoT Hub.
* Poziom systemu autoryzację i uwierzytelnianie Użyj tożsamości na urządzeniu, dostęp do poświadczeń i uprawnień w pobliżu — natychmiastowe odwoływalny.

### <a name="secure-connectivity"></a>Bezpieczna komunikacja
Trwałość wiadomości jest ważna cecha każde rozwiązanie IoT. Witaj muszą toodurably dostarczania poleceń i/lub odbieranie danych z urządzenia jest podkreślona hello fakt, że urządzenia IoT są połączone za pośrednictwem Internetu hello lub inne podobne sieci, które mogą być nieprawidłowe. Centrum IoT Azure oferuje trwałości komunikatów między chmurą i urządzeniami za pomocą systemu potwierdzenia w odpowiedzi toomessages. Dodatkowe trwałości wiadomości jest to osiągane przez buforowanie wiadomości powitania Centrum IoT dla tooseven dni na potrzeby telemetrii i dwa dni na potrzeby poleceń.

Wydajność jest ważne tooensure ochrony zasobów i operacji w środowisku ograniczonej zasobów. HTTPS (HTTP bezpieczne), hello standardowych bezpiecznego wersji protokołu http popularnych hello, jest obsługiwana przez Centrum IoT Azure, umożliwiające sprawną komunikację. Zaawansowane komunikatów usługi kolejkowania wiadomości protokołu (AMQP) i komunikatów usługi kolejkowania wiadomości Telemetrii transportu (MQTT), obsługiwane przez Centrum IoT Azure, są przeznaczone nie tylko w celu zwiększenia wydajności pod względem użycia zasobów, ale także dostarczanie komunikatów niezawodnej. 

Skalowalność wymaga toosecurely możliwości hello współdziałać z szeroką gamą urządzeń. Centrum IoT Azure umożliwia urządzeń obsługujących protokół IP i włączone IP tooboth bezpiecznego połączenia. Adres IP włączony urządzenia są niemożliwe toodirectly połączenia i komunikować się z hello Centrum IoT za pośrednictwem bezpiecznego połączenia. Włączono IP urządzenia są ograniczone zasobów i łączyć tylko za pośrednictwem protokołów komunikacyjnych niedaleko, takich jak Zwave, ZigBee i Bluetooth. Brama pole jest używane tooaggregate tych urządzeń i wykonuje protokołu tłumaczenia tooenable bezpiecznego dwukierunkową komunikację z chmurą hello.

Funkcje zabezpieczeń dodatkowego połączenia hello następujące czynności:

* Witaj ścieżki komunikacji między urządzeniami a Centrum IoT Azure lub między bramami i Azure IoT Hub jest zabezpieczone przy użyciu standardowych zabezpieczeń TLS (Transport Layer) z Centrum IoT Azure uwierzytelniony przy użyciu protokołu X.509.
* Centrum IoT Azure w kolejności tooprotect urządzenia z niechciane połączenia przychodzące, nie powoduje otwarcia dowolnego urządzenia toohello połączenia. urządzenie Hello inicjuje wszystkie połączenia. 
* Centrum IoT Azure trwale przechowuje komunikaty dla urządzeń i czeka na powitania tooconnect urządzenia. Te polecenia są przechowywane przez dwa dni, włączanie urządzeń łączących się sporadycznie, powodu kwestie łączność lub toopower tooreceive tych poleceń. Centrum IoT Azure obsługuje kolejki na urządzenie, dla każdego urządzenia.

### <a name="secure-processing-and-storage-in-hello-cloud"></a>Bezpieczne przetwarzanie i magazynowanie w chmurze hello
Szyfrowanie komunikacji tooprocessing danych w chmurze hello hello pakiet IoT Azure pomaga chronić dane. Zapewnia elastyczność tooimplement dodatkowego szyfrowania i zarządzania kluczy zabezpieczeń. Za pomocą usługi Azure Active Directory (AAD) do uwierzytelniania i autoryzacji użytkowników, pakiet IoT Azure zapewnia modelu autoryzacji na podstawie zasad dla danych w chmurze hello włączania inspekcji i przejrzeć zarządzania łatwy dostęp. Ten model umożliwia także niemal natychmiastowe odwoływanie toodata dostęp w chmurze hello i urządzenia połączone toohello pakiet IoT Azure.

Po umieszczeniu danych w chmurze hello można przetwarzania i przechowywania w przepływie pracy użytkownika. Dostępu tooeach część danych hello jest kontrolowany przy użyciu usługi Azure Active Directory, w zależności od usługi magazynu hello używane.

Wszystkich kluczy używanych przez infrastrukturę IoT hello są przechowywane w chmurze hello w bezpiecznym magazynie z tooroll możliwości hello za pośrednictwem na wypadek klucze muszą toobe ponownie zainicjować obsługi administracyjnej. Dane mogą być przechowywane w [bazy danych Azure rozwiązania Cosmos](../documentdb/documentdb-introduction.md) lub [baz danych](../sql-database/sql-database-faq.md), włączenie definicji hello poziom zabezpieczeń potrzebne. Ponadto Azure udostępnia toomonitor sposób i inspekcji wszystkich tooalert danych tooyour dostępu z nieautoryzowanego dostępu ani nieautoryzowanego dostępu.

## <a name="conclusion"></a>Podsumowanie
Witaj Internetu rzeczy rozpoczyna się od sieci rzeczy — Witaj ważnej zawartości większości toobusinesses. IoT zapewnia niesamowite firm tooa wartości przez zmniejszenie kosztów, zwiększenie przychodów i przekształcanie biznesowych. Powodzenie tej transformacji zależy przede wszystkim Wybieranie hello prawo IoT oprogramowania i usługi dostawcy. Oznacza to, znajdowanie dostawcę, który nie tylko catalyzes tej transformacji zrozumienie potrzeb biznesowych i wymagania dotyczące, ale udostępnia również wbudowane pomocą zabezpieczeń, prywatności i zgodności jako główne projektowania przezroczystości oprogramowania i usług. Firma Microsoft zbiorczych doświadczeń tworzenie i wdrażanie bezpiecznych oprogramowania i usług i kontynuuje toobe znaki wiodące w tej nowej wieku Internetu rzeczy. 

Hello pakiet IoT Microsoft Azure kompilacje w środki bezpieczeństwa zgodnie z projektem, włączanie bezpiecznego monitorowania zasobów tooimprove efektywności, innowacji tooenable operacyjne wydajności dysku, i zatrudnienia zaawansowane analizy danych tootransform firmy. Z warstwowego podejścia do zabezpieczeń, wiele funkcji zabezpieczeń i wzorce projektowe pakiet IoT Azure ułatwia wdrażanie infrastruktury, które mogą być zaufane tootransform dowolnego rodzaju działalności. 

## <a name="additional-information"></a>Dodatkowe informacje
Każdy pakiet IoT Azure wstępnie skonfigurowane rozwiązanie tworzy wystąpienia usług Azure, takich jak hello poniżej:

* [**Centrum IoT Azure**](https://azure.microsoft.com/services/iot-hub/): bramy łączącej hello chmury za "czynności". Można też skalować toomillions połączeń na proces i koncentrator bardzo dużych woluminów danych z obsługą uwierzytelniania na urządzenie pomaga zabezpieczyć rozwiązanie sieci.
* [**Azure DB rozwiązania Cosmos**](https://azure.microsoft.com/services/documentdb/): skalowalne, pełni indeksowana bazy danych usługi częściowo ustrukturyzowanych danych zarządza metadanych dla urządzeń hello udostępnieniem, takich jak atrybuty, konfiguracji i właściwości zabezpieczeń. Rozwiązania cosmos DB oferuje przetwarzanie wysokiej wydajności i wysokiej przepustowości, niezależny od schematu indeksowania danych i interfejs zaawansowanych zapytań SQL.
* [**Usługa Azure Stream Analytics**](https://azure.microsoft.com/services/stream-analytics/): strumienia w czasie rzeczywistym przetwarzania w chmurze hello, która umożliwia toorapidly możesz opracowywania i wdrażania analytics niskokosztowych rozwiązań toouncover w czasie rzeczywistym wgląd w dane dotyczące urządzeń, czujników, infrastruktury, a aplikacje. Hello danych z tej usługi pełni zarządzane można skalować tooany woluminów jednocześnie uzyskanie wysokiej przepływności, małych opóźnień i elastyczność.
* [**Usługa Azure App Service**](https://azure.microsoft.com/services/app-service/): cloud platform toobuild zaawansowanych sieci web i aplikacji mobilnych, łączących toodata w dowolnym miejscu; w chmurze hello lub lokalnie. Twórz interesujące aplikacje mobilne dla systemów iOS, Android i Windows. Integracja z oprogramowanie jako usługa (SaaS) i enterprise aplikacji za pomocą toodozens poza pole łączności z usługami w chmurze i aplikacje przedsiębiorstwa. Kod w języku ulubionych i IDE — .NET, Node.js, PHP, Python lub Java — toobuild sieci web aplikacji i interfejsów API szybciej niż kiedykolwiek.
* [**Logic Apps**](https://azure.microsoft.com/services/app-service/logic/): funkcja Logic Apps hello Azure App Service ułatwia integrują się z istniejącymi systemami — biznesowych IoT rozwiązania tooyour i automatyzację procesów przepływu pracy. Logic Apps umożliwia deweloperom przepływy pracy toodesign uruchamianych wyzwalaczami i wykonujących serie kroków, reguł i akcji, które toointegrate łączniki zaawansowanych za pomocą procesów biznesowych. Logic Apps zapewnia łączność poza pole tooa przeważająca ekosystemu SaaS, oparte na chmurze i lokalnych aplikacji.
* [**Magazyn obiektów blob platformy Azure**](https://azure.microsoft.com/services/storage/): magazynu w chmurze niezawodnych i ekonomiczny dla danych hello, że urządzenia wysyłać toohello chmury.

## <a name="next-steps"></a>Następne kroki
Zobacz toolearn więcej informacji na temat zabezpieczania rozwiązania IoT:

* [Najlepsze rozwiązania IoT][lnk-security-best-practices]
* [Architektura zabezpieczeń IoT][lnk-security-architecture]
* [Zabezpieczanie wdrożenia IoT][lnk-security-deployment]

[lnk-security-best-practices]: iot-security-best-practices.md
[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md

Możesz też przeglądać niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:

* [Omówienie rozwiązania konserwacji predykcyjnej wstępnie][lnk-predictive-overview]
* [Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]

Możesz przeczytać o zabezpieczeniach Centrum IoT w [kontroli dostępu tooIoT Centrum] [ lnk-devguide-security] w hello przewodnik dewelopera Centrum IoT.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
