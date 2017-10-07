---
title: "Architektura zabezpieczeń aaaIoT | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące architektury zabezpieczeń IoT i zagadnienia"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 18ed3eb0-9406-44e1-8a3a-93dc6726c7ac
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 5b59133f6b1b45573318c3bd5b621d27b147d71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-architecture"></a>Architektura zabezpieczeń Internetu rzeczy
Podczas projektowania systemu, jest ważne toounderstand hello potencjalne zagrożenia toothat systemu i dodaj odpowiednie zabezpieczenia w związku z tym, jak hello system został zaprojektowany i zaprojektowana. Jest szczególnie ważne, toodesign ponieważ zrozumienie, jak osoba atakująca może być możliwe toocompromise systemu pomaga, upewnij się, że odpowiednie środki zaradcze są stosowane od początku hello hello produktu od początku hello z myślą o bezpieczeństwie. 

## <a name="security-starts-with-a-threat-model"></a>Zabezpieczenia rozpoczyna się od modelu zagrożeń
Firma Microsoft długo został użyty modeli zagrożenie dla swoich produktów i wprowadził procesu publicznie dostępnych modelowania zagrożeń hello firmy. Witaj środowisko firmy pokazuje, że modelowania hello ma nieoczekiwany korzyści poza hello natychmiastowego zrozumienia jakie zagrożenia są hello dotyczące większości. Na przykład tworzy również ścieżek Otwórz omówienie osobom spoza hello zespół deweloperów, co może prowadzić toonew pomysły i ulepszenia w produkcie hello.

Celem Hello modelowanie zagrożeń jest toounderstand jak osoba atakująca może być możliwe toocompromise systemu i upewnij się, że są stosowane odpowiednie środki zaradcze. Modelowanie zagrożeń wymusza hello projektu zespołowego tooconsider czynniki identycznie hello systemu, a nie po wdrożeniu systemu. Ten fakt jest bardzo ważny, ponieważ modernizacji zabezpieczeń zabezpieczenia tooa większą liczbą urządzeń w polu hello jest w praktyce, błąd podatnych na błędy i pozostawi klientów na ryzyko.

Wiele zespołów deweloperów czy znakomity zadanie przechwytywania hello wymagań dotyczących funkcjonalności systemu hello przeznaczone dla klientów. Jednak identyfikowanie sposoby widoczne czy ktoś może niewłaściwym użyciem systemu hello jest trudniejsze. Modelowanie zagrożeń może pomóc zrozumieć, co może zrobić osoba atakująca zespoły deweloperów i dlaczego. Modelowanie zagrożeń jest procesem strukturalnego, który tworzy Omówienie zabezpieczeń hello decyzje dotyczące projektu w hello systemu, a także projekt toohello zmiany zostały wprowadzone wzdłuż sposób hello mieć wpływ na zabezpieczenia. Gdy modelu zagrożeń jest po prostu dokumentu, tej dokumentacji reprezentuje również idealny ciągłości tooensure wiedzy, przechowywania — lekcje rozpoznawane i szybko pomocy dołączyć nowy zespół. Na koniec wyniku modelowanie zagrożeń jest tooenable tooconsider możesz inne aspekty zabezpieczeń, takich jak zobowiązań zabezpieczeń, jakie mają tooprovide tooyour klientów. Tych zobowiązań w połączeniu z modelowanie zagrożeń będzie informuje i dysków testowania rozwiązania Internetu rzeczy (IoT).

### <a name="when-toothreat-model"></a>Gdy toothreat modelu
[Modelowanie zagrożeń](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) oferty hello największa wartość, jeśli jest włączona w fazie projektowania hello. Podczas projektowania, masz hello największą elastyczność toomake zmiany tooeliminate zagrożeń. Eliminowanie zagrożeń zgodnie z projektem jest pożądany hello. Jest znacznie prostsze niż dodawanie środki zaradcze, ich testowania i zapewnienia są zawsze aktualne, a ponadto takie eliminacji nie zawsze jest możliwe. Staje się on przeszkodę tooeliminate zagrożenia wraz ze wzrostem więcej produktu dojrzałych, a także z kolei ostatecznie wymaga więcej pracy co znacznie trudniejsze wady i zalety niż zagrożeń na wczesnym etapie modelowania w rozwoju hello.

### <a name="what-toothreat-model"></a>Jaki model toothreat
Należy wątku rozwiązania hello modelu jako całości, a także fokusu w hello następujące obszary:

* funkcje zabezpieczeń i prywatności Hello
* Funkcje Hello którego błędy są istotne zabezpieczeń
* Funkcje Hello touch granicy zaufania 

### <a name="who-threat-models"></a>Kto zagrożenia modele
Modelowanie zagrożeń jest procesem, jak każdy inny.  Jest dobrze tootreat hello zagrożeń modelu dokumentu podobnie jak inne składnik rozwiązania hello i go zweryfikować. Wiele zespołów deweloperów czy znakomity zadanie przechwytywania hello wymagań dotyczących funkcjonalności systemu hello przeznaczone dla klientów. Jednak identyfikowanie sposoby widoczne czy ktoś może niewłaściwym użyciem systemu hello jest trudniejsze. Modelowanie zagrożeń może pomóc zrozumieć, co może zrobić osoba atakująca zespoły deweloperów i dlaczego.

### <a name="how-toothreat-model"></a>Jak toothreat modelu
procesu modelowania zagrożeń Hello składa się z czterech etapów; kroki Hello są:

* Aplikacja hello modelu
* Wyliczanie zagrożeń
* Zmniejszenie zagrożeń związanych
* Sprawdź poprawność hello środki zaradcze

#### <a name="hello-process-steps"></a>kroki procesu Hello
Trzy zasady przyjąć tookeep pamiętać podczas konstruowania modelu zagrożeń:

1. Tworzenie diagramu poza architektura referencyjna struktury. 
2. Uruchom najpierw szerokości. Zapoznaj się z omówieniem i zrozumieć hello system jako całość, przed rozpoczęciem pracy bezpośrednich.  Dzięki temu upewnij się, należy szczegółowo w prawo hello miejsca.
3. Dysk hello procesu, niech procesu hello dysk należy. Jeśli znaleźć problemu hello modelowania fazy i chcesz tooexplore Przejdź dla niego!  Nie możesz należy toofollow te kroki slavishly.  

#### <a name="threats"></a>Zagrożenia
Witaj cztery podstawowe elementy modelu zagrożeń to:

* Procesy (usługi sieci web, usług Win32 * nix demonów itp. Należy pamiętać, że niektóre jednostki złożonych (na przykład pole bram i czujników) można pobieranej procesu, gdy techniczne przechodzenia w tych obszarach nie jest możliwe.
* Dane przechowywane (tam, gdzie dane są przechowywane, takich jak plik konfiguracji lub bazy danych)
* Przepływ danych (gdzie dane są przenoszone między innymi elementami w aplikacji hello)
* Podmioty zewnętrzne (wszystkie elementy, które wchodzi w interakcję z systemem hello, ale nie jest pod kontrolą hello aplikacji hello, przykłady obejmują użytkowników oraz urządzeń źródła danych)

Wszystkie elementy na diagramie architektury hello są zagrożenia toovarious podmiotu; używamy skrót klawiszowy krok hello. Odczyt [modelowania zagrożeń ponownie, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow więcej o elementach krok hello.

Różnych elementów diagramu aplikacji hello są zagrożenia STRIDE toocertain podmiotu:

* Procesy są tooSTRIDE podmiotu
* Przepływy danych są tooTID podmiotu
* Magazyny danych czy tooTID podmiotu, a czasami R, magazyny danych hello są pliki dziennika.
* Podmioty zewnętrzne są tooSRD podmiotu

## <a name="security-in-iot"></a>Zabezpieczenia w IoT
Połączonych urządzeń specjalnych dokonano znaczących potencjalnych obszarów powierzchni interakcji i wzorce interakcji, które muszą być traktowane jako tooprovide framework zabezpieczania dostępu cyfrowe toothose urządzeń. Hello termin "cyfrowego dostępu" jest używany tutaj toodistinguish z żadnych działań, które są przeprowadzane za pośrednictwem urządzeń bezpośrednio interakcji gdzie zabezpieczenia dostępu jest zapewniana za pomocą sterowania dostępem fizycznym. Na przykład wprowadzenie hello urządzenia do miejsca z blokadą na powitania drzwi. Gdy nie można odmówić dostępu fizycznej przy użyciu sprzętu i oprogramowania, można środki tooprevent fizyczny dostęp z wiodące toosystem zakłóceń. 

Jak możemy zapoznać się z wzorców interakcji hello, zajmiemy "kontroli urządzeń" i "urządzenie danych" za pomocą hello tym samym poziomie uwagi. "Urządzenie control" mogą być klasyfikowane jako wszystkie informacje, które jest udostępniane tooa urządzenia przez stronę z celem hello zmiana lub mające wpływ na jego zachowanie w kierunku jej stan lub hello stan swojego środowiska. "Urządzenie danych" mogą być klasyfikowane jako żadnych informacji, że urządzenie emituje tooany innych firm o jego stan i hello obserwowanych stan swojego środowiska.

W kolejności toooptimize najlepszych rozwiązań dotyczących zabezpieczeń zaleca się, że typowy architektury IoT podzielić na kilku składników/stref jako część zagrożeń hello modelowania wykonywania. Te strefy są całkowicie opisane w tej sekcji i obejmują:

* Urządzenie,
* Brama pola
* Bramy, w chmurze i
* Usługi.

Strefy są szerokie toosegment sposób rozwiązania; każdej strefy ma często wymagania danych i uwierzytelniania i autoryzacji. Strefy mogą być również używane tooisolation uszkodzenia i ograniczyć wpływ hello niski zaufania strefy na wyższe zaufania strefy.

Każdej strefy są rozdzielone przez granicę zaufania, które jest wymienione jako hello kropkami czerwona linia hello diagramie poniżej. Reprezentuje przejście informacje o i danych z jednego źródła tooanother. Podczas tego przejścia hello danych może być tooSpoofing podmiotu, Tampering, Repudiation, ujawnienie informacji, odmowa usługi i podniesienie uprawnień (krok).

![Strefy zabezpieczeń IoT](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Witaj składniki przedstawione w obrębie każdej granicy są również poddane tooSTRIDE, włączenie pełnego 360 widoku hello rozwiązania modelowania zagrożeń. Poniższe rozdziały zawierają Hello rozwinięcia poszczególnych składników hello i zagadnienia dotyczące zabezpieczeń określone i rozwiązań, które powinny znajdować się w miejscu.

kolejnych sekcjach Hello przedstawimy standardowymi elementami, które zwykle znajdują się w tych strefach.

### <a name="hello-device-zone"></a>Witaj strefy urządzenia
Hello urządzenia środowisko jest natychmiastowe fizycznego miejsca hello wokół urządzenia hello, gdzie dostęp fizyczny i/lub cyfrowy peer-to-peer "sieci lokalnej" dostęp do toohello urządzeń jest możliwe. "Sieci lokalnej" zakłada, że toobe sieci, która jest odrębny i odizolowanego od — ale potencjalnie mostkowania publicznej sieci Internet za — Witaj i zawiera wszystkie urządzenia bezprzewodowego radia technologie, które umożliwia komunikację peer-to-peer urządzeń. Robi *nie* obejmują innych technologii wirtualizacji sieci tworzenie hello wrażenie sieci lokalnej i również nie obejmować sieci operator publiczny, które wymagają toocommunicate żadnych urządzeń w sieci publicznej miejsca Jeśli były relacji komunikacji tooenter peer-to-peer.

### <a name="hello-field-gateway-zone"></a>Witaj pola bramy strefy
Brama pole jest urządzeń/urządzenia lub niektóre oprogramowania komputera ogólnego przeznaczenia serwera, który działa jako czynnik komunikacji oraz w razie potrzeby jako system kontroli urządzeń i centrum przetwarzania danych urządzenia. strefy bramy pola Hello obejmuje hello pola bramy oraz wszystkie urządzenia, które są dołączone tooit. Jak nazwa hello wskazuje, bramy pola działania urządzenia poza dedykowanych przetwarzania danych, są zwykle lokalizacji powiązany, są potencjalnie włamań toophysical podmiotu i będzie ograniczona operacyjne nadmiarowości. Wszystkie toosay, który często jest brama pola operacją, co może touch i przeszkadzają a jest jego funkcji. 

Bramy pola różni się od routera sam ruch, że posiada ona aktywną rolę w zarządzaniu dostępu i przepływem informacji, co oznacza, że jest to aplikacja rozwiązany jednostki i połączenie sieciowe lub sesję terminalu. Urządzenie NAT lub zaporą, natomiast nie kwalifikuje się pole bram, ponieważ nie są jawne połączenie lub terminale sesji, ale raczej połączeń trasy (lub blok) lub wprowadzane za pośrednictwem ich sesji. Brama pola Hello ma dwa różne obszary powierzchni. Jeden skierowany hello urządzenia, które są dołączone tooit i reprezentuje hello wewnątrz hello strefy i hello innych skierowany wszystkich podmiotów zewnętrznych i krawędzi hello hello strefy.   

### <a name="hello-cloud-gateway-zone"></a>strefy bramy chmury Hello
Brama chmury to system, który umożliwia zdalnej komunikacji z i bram toodevices lub pola z wielu różnych lokacji w sieci publicznej miejsca, zwykle na chmurze i kontroli danych analizy systemu, Federacji takich systemów. W niektórych przypadkach brama chmury natychmiast może ułatwić urządzenia cel toospecial dostępu z terminali, np. tabletów i telefonów. W kontekście hello omówione w tym miejscu "w chmurze" oznacza toorefer tooa dedykowanego przetwarzania danych system, który nie jest powiązane toohello lokacji takie same jak hello dołączone urządzenia lub pola bramy. Również w strefie chmury środki operacyjne uniemożliwić docelowe fizyczny dostęp i nie są tooa niekoniecznie narażonych infrastruktury "w chmurze publicznej".  

Brama chmury potencjalnie mogą być mapowane do bramy wirtualizacji sieci nakładki tooinsulate hello chmury oraz wszystkie jego podłączonych urządzeń i bram pole od innego ruchu sieciowego. Witaj chmury brama jest ani system kontroli urządzeń ani przetwarzania lub magazynu dla danych urządzenia. te urządzenia interfejsu hello bramy chmury. Strefa bramy chmury Hello obejmuje hello chmury brama wraz ze wszystkich bram pola i urządzenia tooit podłączone bezpośrednio lub pośrednio. Krawędź Hello strefy hello jest różne powierzchni gdzie wszystkich podmiotów zewnętrznych komunikują się za pośrednictwem.

### <a name="hello-services-zone"></a>Witaj usług strefy
"Usługa" jest zdefiniowany dla tego kontekstu jako części oprogramowania lub moduł, który jest relacje z urządzeniami za pośrednictwem bramy pola lub chmury do zbierania danych i analizy, a także polecenia i kontroli.  Usługi są mediatorów. One działać w ramach ich tożsamości bramy i innych podsystemów, przechowywania i analizowania danych, autonomicznie toodevices polecenia problemu na podstawie wgląd w danych lub harmonogramy i udostępnianie informacji i użytkownicy końcowi tooauthorized możliwości kontroli.

### <a name="information-devices-vs-special-purpose-devices"></a>Urządzenia informacyjne a specjalnych urządzeń
Komputery, telefony i tablety to przede wszystkim interakcyjne informacji urządzenia. Telefony i tablety jawnie są zoptymalizowane wokół maksymalizacja baterii istnienia. One najlepiej wyłączyć częściowo, gdy nie jest od razu interakcji z osoby lub gdy nie dostarcza usługi, takie jak odtwarzanie muzyki lub skierowanie ich właściciela tooa określonej lokalizacji. Z punktu widzenia systemy te urządzenia technologii informacji głównie działają jako serwery proxy do osób. Są one "osób siłowniki" sugerowanie "osób czujniki" zbieranie danych wejściowych i akcje. 

Urządzenia specjalnych z prostego temperatury czujników toocomplex fabryki produkcji wierszy z tysiącami elementów zawartych w nich, są różne. Bardziej ograniczone te urządzenia w celu i nawet wtedy, gdy udostępniają część interfejsu użytkownika są przede wszystkim zakresie toointerfacing z lub można zintegrować zasoby w Witaj świecie fizycznych. One mierzyć i raportu okoliczności środowiska, Włącz zawory, kontroli servos, dźwiękowej alarmy, przełącznika świateł i wykonywać inne zadania. Pomagają toodo pracy, dla których urządzenie informacji jest zbyt ogólne, zbyt drogie, za duży lub zbyt łamliwa. Witaj konkretnego celu natychmiast nakazują ich projektu technicznego jako dostępnego budżetu pieniężnego dobrze hello ich produkcji i okres istnienia zaplanowanych operacji. Kombinacja Hello te dwa czynniki klucza ogranicza hello dostępne operacyjne budżetu energii, fizycznego miejsca i w związku z tym dostępny magazyn, zasobów obliczeniowych i funkcje zabezpieczeń.  

Jeśli coś "umieszczane niewłaściwy" urządzeniami automatyczna lub z zdalnego kontrolowane, na przykład wad fizycznego lub formant logiki wady toowillful nieautoryzowany nieautoryzowanego dostępu i manipulowania nimi. może zostać zniszczone Hello produkcji partii, budynków może looted lub kiedyś w dół i osób może być poszkodowanej lub nawet struktury. Jest to oczywiście całego inną klasę uszkodzenia niż ktoś maxing się limit kradzieży karty kredytowej. Hello pasek zabezpieczeń na urządzeniach, które spowodowały rzeczy Przenieś, a także dla danych czujnika czy ostatecznie powoduje poleceń, które powodują toomove rzeczy, musi być wyższy niż w handlu elektronicznego lub scenariusz bankowości. 

### <a name="device-control-and-device-data-interactions"></a>Kontroli urządzeń i ich interakcje danych urządzenia
Połączonych urządzeń specjalnych dokonano znaczących potencjalnych obszarów powierzchni interakcji i wzorce interakcji, które muszą być traktowane jako tooprovide framework zabezpieczania dostępu cyfrowe toothose urządzeń. Hello termin "cyfrowego dostępu" jest używany tutaj toodistinguish z żadnych działań, które są przeprowadzane za pośrednictwem urządzeń bezpośrednio interakcji gdzie zabezpieczenia dostępu jest zapewniana za pomocą sterowania dostępem fizycznym. Na przykład wprowadzenie hello urządzenia do miejsca z blokadą na powitania drzwi. Gdy nie można odmówić dostępu fizycznej przy użyciu sprzętu i oprogramowania, można środki tooprevent fizyczny dostęp z wiodące toosystem zakłóceń. 

Jak możemy zapoznać się z wzorców interakcji hello, zajmiemy "kontroli urządzeń" i "urządzenie danych" za pomocą hello tym samym poziomie uwagi podczas modelowania zagrożeń. "Urządzenie control" mogą być klasyfikowane jako wszystkie informacje, które jest udostępniane tooa urządzenia przez stronę z celem hello zmiana lub mające wpływ na jego zachowanie w kierunku jej stan lub hello stan swojego środowiska. "Urządzenie danych" mogą być klasyfikowane jako żadnych informacji, że urządzenie emituje tooany innych firm o jego stan i hello obserwowanych stan swojego środowiska. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>Architektura referencyjna Azure IoT hello modelowania zagrożeń
Firma Microsoft używa framework hello opisanych powyżej zagrożeń toodo modelowania dla Azure IoT. W poniższej sekcji hello w związku z tym używany hello konkretny przykład sposób identyfikowania toothink o zagrożeń modelowania IoT i jak tooaddress hello zagrożenia toodemonstrate architektura referencyjna IoT platformy Azure. W tym przypadku określiliśmy cztery główne obszary fokus:

* Urządzenia i źródeł danych
* Transport danych
* Urządzenia i przetwarzania zdarzeń i
* Prezentacji

![Zagrożenia modelowania dla Azure IoT](media/iot-security-architecture/iot-security-architecture-fig2.png) 

Poniższy diagram Hello oferuje uproszczony widok architektury IoT firmy Microsoft, za pomocą modelu Diagram przepływu danych, który jest używany przez narzędzie modelowania zagrożeń Microsoft hello:

![Zagrożenia modelowania dla Azure IoT przy użyciu narzędzia do modelowania zagrożeń MS](media/iot-security-architecture/iot-security-architecture-fig3.png)

Jest ważne toonote, który hello architektura oddziela hello możliwości urządzenia i bramy. Dzięki temu tooleverage użytkownika hello urządzenia bramy, które są bardziej bezpieczne: mogą komunikować się z chmury hello bramy przy użyciu bezpiecznych protokołów, która zwykle wymaga większej przetwarzania czy natywnego urządzenie — takie jak termostacie — można Podaj samodzielnie. W strefie usługi Azure hello przyjęto założenie, powitalne tej bramy chmury jest reprezentowana przez hello usługa Azure IoT Hub.

### <a name="device-and-data-sourcesdata-transport"></a>Transport źródeł/danych urządzenia i danych
W tej sekcji Eksploruje architektura hello opisanych powyżej za pośrednictwem obiektyw hello modelowania zagrożeń i powinien zawierać omówienie jak możemy są niektóre problemy związane z hello adresowania. Firma Microsoft koncentruje się na powitania podstawowe elementy modelu zagrożeń:

* Procesy (zawarte w naszym kontroli i elementów zewnętrznych)
* Komunikacja (nazywanych również przepływów danych)
* Magazyn (nazywanych również magazyny danych)

#### <a name="processes"></a>Procesy
W każdej kategorii hello opisane w hello Azure IoT architektura spróbujemy toomitigate w istnieje szereg różnych zagrożeń między informacje danych różnych etapach hello: proces, komunikację i magazynu. Poniżej możemy podać omówienie hello najbardziej typowe dla kategorii "proces" hello, następuje przegląd jak te mogą być najlepiej skorygowane: 

**Fałszowanie zawartości (S)**: osoba atakująca może wyodrębnić materiał kluczy kryptograficznych z urządzenia, albo na poziomie oprogramowania lub sprzętu hello i następnie dostępu hello systemu z innego urządzenia fizyczne lub wirtualne tożsamością hello Witaj Witaj urządzenia materiał klucza jest zajęta z. Dobrym ilustracja to zdalnego sterowania, który można włączyć wszystkie TV i które są prankster popularne narzędzia.

**Odmowa usługi (D)**: urządzenie może być renderowana niezdolne do funkcjonowania lub komunikacji przez zakłócać częstotliwości lub wycinanie przewodów. Na przykład aparatu nadzoru, który miał jego zasilania lub połączenia sieciowego celowo wycinane ani zgłaszać danych, w ogóle.

**Manipulowanie (T)**: osoba atakująca może częściowo lub całkowicie zastąpić oprogramowania hello działającej na urządzeniu hello, potencjalnie, jeśli hello, dzięki czemu hello zastąpione oprogramowania tooleverage hello oryginalnego tożsamości urządzenia hello materiału klucza lub hello kryptograficznych urządzeń gospodarstwa materiałów klucza były dostępne toohello nielegalnemu program. Na przykład osoba atakująca może wykorzystać wyodrębnionego toointercept materiału klucza i Pomiń danych z urządzenia hello w ścieżce komunikacji hello i zamień ją na wartość false dane, które są uwierzytelniani hello kradzieży materiału klucza.

**Ujawnienie informacji, (I)**: Jeśli urządzenie hello jest uruchomione oprogramowanie manipulować, manipulować oprogramowania może potencjalnie wycieku danych toounauthorized strony. Na przykład osoba atakująca może wykorzystać wyodrębnionego klucza materiału tooinject się do ścieżki komunikacji hello między urządzeniem hello i bramy kontrolera lub pola lub toosiphon bramy poza informacji w chmurze.

**Podniesienie uprawnień (E)**: urządzenie, które wykonuje określoną funkcję może być wymuszone toodo coś innego. Na przykład zawór jest zaprogramowanych tooopen połowy sposób może być zamiarem tooopen wszystkie hello sposób.

| **Składnik** | **Zagrożenia** | **Środki zaradcze** | **Ryzyko** | **Implementacja** |
| --- | --- | --- | --- | --- |
| Urządzenie |S |Przypisywanie urządzeń toohello tożsamości i uwierzytelniania hello urządzenia |Zastępując urządzenia lub częścią urządzenia hello inne urządzenie. Jak wiemy, że firma Microsoft mówimy toohello odpowiednim urządzeniu? |Uwierzytelniania urządzenia hello, przy użyciu zabezpieczeń TLS (Transport Layer) lub protokołu IPSec. Infrastruktura powinna obsługiwać przy użyciu klucza wstępnego (PSK) na tych urządzeniach, które nie może obsłużyć pełnej asymetrycznego kryptografii. Wykorzystanie usługi Azure AD, [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Na przykład zastosować tamperproof mechanizmów toohello urządzenia klucze tooextract tooimpossible bardzo trudne i innych materiałów kryptograficznych z urządzenia hello co. |ryzyko Hello jest, jeśli ktoś jest manipulowanie nimi hello urządzenia (zakłócenia fizycznych). W jaki sposób możemy pewności, czy urządzenie nie zmodyfikowany. |środki zaradcze najbardziej efektywne Hello jest TPM możliwości module (TPM), która umożliwia przechowywanie kluczy w specjalne obwody w układzie, z których hello nie można odczytać klawiszy, ale można używać tylko dla operacji kryptograficznych, które używają klucza hello, ale nigdy nie ujawniają hello klucza . Szyfrowanie pamięci hello urządzenia. Zarządzanie kluczami hello urządzenia. Podpisywanie kodu hello. | |
| E |Zapewniający kontrolę dostępu hello urządzenia. Schemat autoryzacji. |Jeśli urządzenie hello umożliwia dla poszczególnych działań toobe wykonywane polecenia ze źródła zewnętrznego — na podstawie lub naruszony nawet czujników, umożliwia atak powitania tooperform operacji nie jest dostępna w przeciwnym razie wartość. |Po autoryzacji schemat hello urządzenia | |
| Pole bramy |S |Uwierzytelnianie hello pola bramy tooCloud bramy (certyfikat na podstawie, PSK, oświadczenia na podstawie,...). |Jeśli ktoś może spreparować pola bramy, następnie go może być wyświetlany jako dowolnego urządzenia. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). Wszystkie hello tego samego magazynu kluczy i zaświadczania dotyczy urządzeń, na ogół — najlepszy jest użyć modułu TPM. Rozszerzenie 6LowPAN toosupport IPSec bezprzewodowej sieci czujnik (WSN). |
| TRID |Ochrona hello bramy pola przed naruszeniem (module TPM)? |Fałszowanie atakami wymuszać bramy chmury hello sądząc, że jest mówić toofield bramy może spowodować ujawnienie informacji i modyfikowaniu danych |Pamięć szyfrowania, modułu TPM firmy, uwierzytelniania. | |
| E |Mechanizmu kontroli dostępu dla pola bramy | | | |

Poniżej przedstawiono przykładowe zagrożenia w tej kategorii:

Fałszowanie: Osoba atakująca może wyodrębnić materiał kluczy kryptograficznych z urządzenia, zarówno na poziomie hello oprogramowania lub sprzętu, a następnie dostępu zostało hello systemu z innego urządzenia fizyczne lub wirtualne tożsamością hello hello materiału klucza hello urządzenia pobrana z.

**Odmowa usługi**: urządzenie może być renderowana niezdolne do funkcjonowania lub komunikacji przez zakłócać częstotliwości lub wycinanie przewodów. Na przykład aparatu nadzoru, który miał jego zasilania lub połączenia sieciowego celowo wycinane ani zgłaszać danych, w ogóle.

**Manipulowanie**: osoba atakująca może częściowo lub całkowicie zastąpić oprogramowania hello działającej na urządzeniu hello, potencjalnie, jeśli hello, dzięki czemu hello zastąpione oprogramowania tooleverage hello oryginalnego tożsamości urządzenia hello materiału klucza lub hello kryptograficznych urządzeń gospodarstwa materiałów klucza były dostępne toohello nielegalnemu program.

**Manipulowanie**: fotografia takie korytarz może mieć na celu kamery nadzoru, który jest wyświetlany obraz widoczne spektrum korytarz pusty. Czujnik dymu lub fire może być raportowania ktoś zawierający jaśniejszego w nim. W obu przypadkach hello urządzenie może być technicznie pełni zaufanego kierunku hello systemu, ale będzie zgłaszać manipulować informacji.

**Manipulowanie**: osoba atakująca może wykorzystać wyodrębnionego toointercept materiału klucza i Pomiń danych z urządzenia hello w ścieżce komunikacji hello i zastąp go false dane, które są uwierzytelniani hello kradzieży materiału klucza.

**Manipulowanie**: osoba atakująca może częściowo lub całkowicie zastąpić oprogramowania hello działającej na urządzeniu hello, potencjalnie, jeśli hello, dzięki czemu hello zastąpione oprogramowania tooleverage hello oryginalnego tożsamości urządzenia hello materiału klucza lub hello kryptograficznych urządzeń gospodarstwa materiałów klucza były dostępne toohello nielegalnemu program.

**Ujawnienie informacji**: Jeśli urządzenie hello jest uruchomione oprogramowanie manipulować, manipulować oprogramowania może potencjalnie wycieku danych toounauthorized strony.

**Ujawnienie informacji**: osoba atakująca może wykorzystać wyodrębnionego klucza materiału tooinject się do ścieżki komunikacji hello między urządzeniem hello i bramy kontrolera lub pola lub toosiphon bramy poza informacji w chmurze.

**Odmowa usługi**: hello urządzenia można ją wyłączyć lub przekształcane w tryb, gdy komunikacja nie jest możliwe (która jest zamierzone, w wielu maszyn przemysłowych).

**Manipulowanie**: hello urządzenie może być ponownie skonfigurowanych toooperate w stanie Nieznany toohello systemu (poza odwzorowania znane parametry) kontroli, a zatem mogą udostępniać dane, które mogą zostać błędnie zinterpretowane

**Podniesienie uprawnień**: urządzenie, które wykonuje określoną funkcję może być wymuszone toodo coś innego. Na przykład zawór jest zaprogramowanych tooopen połowy sposób może być zamiarem tooopen wszystkie hello sposób.

**Odmowa usługi**: hello urządzenia można włączyć w stanie, w których komunikacja nie jest możliwe.

**Manipulowanie**: hello urządzenie może być ponownie skonfigurowanych toooperate w stanie Nieznany toohello systemu (poza odwzorowania znane parametry) kontroli, a zatem mogą udostępniać dane, które mogą zostać błędnie zinterpretowane.

**Fałszowanie/Tampering/Repudiation**: Jeśli nie jest zabezpieczone (która jest rzadko powitania klienta zdalnego sterowania w przypadku) atakujący można manipulować anonimowo hello stan urządzenia. Dobrym ilustracja to zdalnego sterowania, który można włączyć wszystkie TV i które są prankster popularne narzędzia.

#### <a name="communication"></a>Komunikacja
Zagrożenia ścieżkę komunikacji między urządzeniami, urządzeń i bram pola i bramy urządzenia i w chmurze. w poniższej tabeli Hello ma wskazówek wokół otwarte gniazda na powitania urządzenia lub sieć VPN:

| **Składnik** | **Zagrożenia** | **Środki zaradcze** | **Ryzyko** | **Implementacja** |
| --- | --- | --- | --- | --- |
| Centrum IoT urządzenia |TID |(D) Ruch hello tooencrypt TLS (PSK/RSA) |Podsłuchiwaniu lub konfliktu hello komunikacji między urządzeniami hello i hello bramy |Zabezpieczenia na poziomie protokołu hello. Protokoły niestandardowe, firma Microsoft wymaga toofigure się, jak tooprotect je. W większości przypadków hello komunikacja odbywa się z hello toohello urządzenia IoT Hub (urządzenie inicjuje połączenie hello). |
| Urządzenie urządzenie |TID |(D) TLS (PSK/RSA) tooencrypt hello ruchu. |Odczytywanie danych przesyłanych między urządzeniami. Manipulowanie danymi hello. Przeciążanie hello urządzenia przy użyciu nowych połączeń |Zabezpieczenia na poziomie protokołu hello (MQTT/AMQP/HTTP/CoAP. Protokoły niestandardowe, firma Microsoft wymaga toofigure się, jak tooprotect je. Hello ograniczenie dotyczące hello DoS zagrożenie jest toopeer na urządzeniach za pośrednictwem bramy chmury lub pola i je tylko act jako klienci kierunku hello sieci. równorzędna Hello może spowodować bezpośrednie połączenie między komputerami równorzędnymi powitania po o została przeprowadzana przez bramę hello |
| Urządzenie zewnętrznej jednostki |TID |Silne parowanie hello zewnętrznej jednostki toohello urządzenia |Podsłuchem hello toohello urządzenia. Mieszających hello komunikacji z urządzeniem hello |Bezpiecznie parowanie hello zewnętrznej jednostki toohello urządzenia LE NFC/Bluetooth. Kontrolowanie hello panelu operacyjne hello urządzenia (fizycznych) |
| Brama chmury bramy pola |TID |TLS (PSK/RSA) tooencrypt hello ruchu. |Podsłuchiwaniu lub konfliktu hello komunikacji między urządzeniami hello i hello bramy |Zabezpieczenia na poziomie protokołu hello (MQTT/AMQP/HTTP/CoAP). Protokoły niestandardowe, firma Microsoft wymaga toofigure się, jak tooprotect je. |
| Urządzenia bramy chmury |TID |TLS (PSK/RSA) tooencrypt hello ruchu. |Podsłuchiwaniu lub konfliktu hello komunikacji między urządzeniami hello i hello bramy |Zabezpieczenia na poziomie protokołu hello (MQTT/AMQP/HTTP/CoAP). Protokoły niestandardowe, firma Microsoft wymaga toofigure się, jak tooprotect je. |

Poniżej przedstawiono przykładowe zagrożenia w tej kategorii:

**Odmowa usługi**: ograniczonego urządzenia są zazwyczaj zagrożona DoS podczas ich aktywnie nasłuchiwać połączeń przychodzących lub niechciane datagramy w sieci, ponieważ atakujący można otwierać wiele połączeń równolegle, a nie ich usługi lub usługi bardzo wolno lub hello urządzenie może być przeciążony niepożądanego ruchu je. W obu przypadkach hello urządzenia mogą skutecznie przestać działać w hello sieci.

**Fałszowania, ujawnienia informacji**: ograniczone i urządzenia specjalnych często mają zabezpieczeń co dla wszystkich urządzeń, takich jak hasła lub numeru PIN ochrony lub całkowicie opierają się na ufających hello sieci, co oznacza przyznać dostęp tooinformation, gdy urządzenie jest na powitania tej samej sieci, a ta sieć jest często tylko chronione przez klucza wspólnego. Oznacza to, że hello udostępnionych tajny toodevice lub ujawnić sieci, jest możliwe toocontrol hello urządzenia lub obserwować dane wysyłanego z hello urządzenia.  

**Fałszowanie**: osoba atakująca może przechwycić lub częściowo zastąpienie hello emisji i fałszywe hello nadawca (man w środku hello)

**Manipulowanie**: osoba atakująca może przechwycić lub częściowo zastąpić hello emisji i wysłać fałszywe informacje 

**Ujawnienie informacji:** osoba atakująca może podsłuchiwać emisji i uzyskiwanie informacji bez autoryzacji **"odmowa usługi":** osoba atakująca może zablokowania hello emisji sygnale i odmowy dystrybucji informacji

#### <a name="storage"></a>Magazyn
Co brama urządzenia i pole ma jakiegoś magazynu (tymczasowe kolejkowania wiadomości powitania danych, magazynu obrazu systemu operacyjnego (OS)).

| **Składnik** | **Zagrożenia** | **Środki zaradcze** | **Ryzyko** | **Implementacja** |
| --- | --- | --- | --- | --- |
| Urządzenia magazynu |TRID |Szyfrowanie magazynu, podpisywania hello dzienników |Odczytywania danych z magazynu hello (dane osobowe dane), manipulowanie danymi telemetrii. Manipulowanie Zakolejkowane lub polecenia kontroli danych w pamięci podręcznej. Wprowadzanie zmian w konfiguracji lub oprogramowania układowego pakietów aktualizacji w pamięci podręcznej lub lokalnie w kolejce może prowadzić tooOS i/lub system składniki naruszenia bezpieczeństwa |Szyfrowanie, kod uwierzytelniania wiadomości (MAC) lub podpisu cyfrowego. Gdzie kontroli dostępu możliwości, silne za pośrednictwem dostęp do zasobów kontroli list (kontroli dostępu ACL) lub uprawnienia. |
| Obraz systemu operacyjnego urządzenia |TRID | |Manipulowanie systemu operacyjnego / zastępowania składniki hello systemu operacyjnego |Tylko do odczytu partycji systemu operacyjnego, podpisany obrazu systemu operacyjnego, szyfrowania |
| Magazyn bramy pola (kolejkowania wiadomości powitania danych) |TRID |Szyfrowanie magazynu, podpisywania hello dzienników |Odczytywanie danych z magazynu hello (dane osobowe dane), manipulowanie danymi telemetrii ingerencji w kolejce lub polecenia kontroli danych w pamięci podręcznej. Wprowadzanie zmian w konfiguracji lub oprogramowania układowego pakietów aktualizacji (przeznaczonych dla urządzenia lub pola bramy) podczas buforowane lub lokalnie w kolejce może prowadzić tooOS i/lub system składniki naruszenia bezpieczeństwa |Funkcja BitLocker |
| Obraz systemu operacyjnego bramy pola |TRID | |Manipulowanie systemu operacyjnego / zastępowania składniki hello systemu operacyjnego |Tylko do odczytu partycji systemu operacyjnego, podpisany obrazu systemu operacyjnego, szyfrowania |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Urządzenia i zdarzenia strefy bramy przetwarzania/w chmurze
Brama chmury to system, który umożliwia zdalnej komunikacji z i bram toodevices lub pola z wielu różnych lokacji w sieci publicznej miejsca, zwykle na chmurze i kontroli danych analizy systemu, Federacji takich systemów. W niektórych przypadkach brama chmury natychmiast może ułatwić urządzenia cel toospecial dostępu z terminali, np. tabletów i telefonów. W kontekście hello omówione w tym miejscu "cloud" oznacza toorefer tooa dedykowanego przetwarzania danych systemu, który nie jest powiązane toohello tej samej lokacji hello podłączonego urządzenia lub pola bramy, a w przypadku, gdy środki operacyjne zapobiec docelowym fizyczny dostęp, ale nie jest koniecznie tooa "publiczne" infrastruktury w chmurze.  Brama chmury potencjalnie mogą być mapowane do bramy wirtualizacji sieci nakładki tooinsulate hello chmury oraz wszystkie jego podłączonych urządzeń i bram pole od innego ruchu sieciowego. Witaj chmury brama jest ani system kontroli urządzeń ani przetwarzania lub magazynu dla danych urządzenia. te urządzenia interfejsu hello bramy chmury. Strefa bramy chmury Hello obejmuje hello chmury brama wraz ze wszystkich bram pola i urządzenia tooit podłączone bezpośrednio lub pośrednio.

Brama chmury jest głównie niestandardowych wbudowanych oprogramowanie jako Usługa bramy pola toowhich narażonych punktów końcowych i łączenia urządzeń. Jako takie muszą być zaprojektowane z myślą o bezpieczeństwie. Wykonaj [SDL](http://www.microsoft.com/sdl) proces projektowania i tworzenia tej usługi. 

#### <a name="services-zone"></a>Strefa usługi
System kontroli (lub kontrolera) jest rozwiązaniem oprogramowania, które interfejsy z urządzenia, lub brama pola lub brama chmury hello w celu kontrolowania jednego lub wielu urządzeń i/lub toocollect i/lub magazynu i/lub analizowania danych urządzeń do prezentacji, lub celów kolejnych kontroli. Systemów kontroli są hello jednostek tylko w zakresie hello tej dyskusji, która może ułatwić natychmiast interakcji z użytkownikami. wyjątek Hello jest pośrednie fizycznych powierzchni na urządzeniach, takich jak przełącznik, który umożliwia osoby tooturn hello urządzenia poza lub zmienić inne właściwości i dla którego nie ma odpowiednika funkcjonalności, które mogą uzyskiwać cyfrowo. 

Pośredni fizycznych powierzchni są gdzie dowolny rodzaj logiki regulujące ogranicza hello funkcji powierzchni hello fizycznych odpowiedniki może zostać uruchomiona zdalnie lub wejściowych powoduje konflikt z danych wejściowych zdalnego może być zaoszczędzone — takich intermediated powierzchni są system kontroli lokalnego koncepcyjnie dołączonych tooa wykorzystanie hello samą funkcjonalność, jak inne systemy zdalnego sterowania, który hello urządzenie może być dołączone tooin równoległych. Przetwarzania może być odczytany przy w górnym zagrożenia toohello chmurze [chmury zabezpieczeń Alliance (CSA)](https://cloudsecurityalliance.org/research/top-threats/) strony.

## <a name="additional-resources"></a>Dodatkowe zasoby
Można znaleźć toohello następujące artykuły, aby uzyskać dodatkowe informacje:

* [Narzędzie modelowania zagrożeń SDL](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Architektura referencyjna IoT Azure firmy Microsoft](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

## <a name="see-also"></a>Zobacz też
Zobacz toolearn więcej informacji na temat zabezpieczania rozwiązania IoT [zabezpieczania wdrożenia IoT][lnk-security-deployment].

Możesz też przeglądać niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:

* [Omówienie rozwiązania konserwacji predykcyjnej wstępnie][lnk-predictive-overview]
* [Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]

Możesz przeczytać o zabezpieczeniach Centrum IoT w [kontroli dostępu tooIoT Centrum] [ lnk-devguide-security] w hello przewodnik dewelopera Centrum IoT.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md