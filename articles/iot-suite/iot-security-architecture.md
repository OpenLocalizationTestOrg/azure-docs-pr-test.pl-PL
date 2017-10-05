---
title: "Architektura zabezpieczeń IoT | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2482dade7d17d05b2fc90fbf22b0466227a5983b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-architecture"></a>Architektura zabezpieczeń Internetu rzeczy
Podczas projektowania systemu, ważne jest zrozumienie potencjalnych zagrożeń dla tego systemu, a Dodaj odpowiednie zabezpieczenia w związku z tym system został zaprojektowany i zaprojektowana. Jest szczególnie ważne projektowania produktu od początku z myślą o bezpieczeństwie Opis ułatwia sposób atakujący może być w stanie naruszyć bezpieczeństwo systemu, upewnij się, że odpowiednie środki zaradcze znajdują się w miejscu od początku. 

## <a name="security-starts-with-a-threat-model"></a>Zabezpieczenia rozpoczyna się od modelu zagrożeń
Firma Microsoft długo został użyty modeli zagrożenie dla swoich produktów i wprowadził procesu publicznie dostępnych modelowania zagrożeń firmy. Doświadczenie firmy pokazuje, że modelowania ma nieoczekiwany korzyści po zrozumienia bezpośrednim jakie zagrożenia są najbardziej dotyczące. Na przykład tworzy również ścieżek Otwórz omówienie osobom spoza zespół deweloperów, co może prowadzić do nowe pomysły i ulepszenia produktu.

Celem modelowanie zagrożeń jest zrozumienie, jak osoba atakująca może być może naruszyć bezpieczeństwo systemu i upewnij się, że są stosowane odpowiednie środki zaradcze. Wymusza modelowania zagrożeń zespół projektowy wziąć pod uwagę czynniki, ponieważ system został zaprojektowany, a nie po system jest wdrażana. Ten fakt jest bardzo ważny, ponieważ modernizacji zabezpieczenia różnych urządzeń w polu jest praktyce, błąd podatnych na błędy i pozostawi klientów na ryzyko.

Wiele zespołów deweloperów czy znakomity zadanie przechwytywania wymagania funkcjonalne dla systemu, które korzystać klienci. Jednak identyfikowanie-oczywisty sposób czy ktoś może niewłaściwym użyciem systemu jest trudniejsze. Modelowanie zagrożeń może pomóc zrozumieć, co może zrobić osoba atakująca zespoły deweloperów i dlaczego. Modelowanie zagrożeń jest procesem strukturalnego, który tworzy decyzji projektowych Omówienie zabezpieczeń w systemie, a także zmiany do projektu, który zgłosił wzdłuż sposób zabezpieczenia wpływ. Gdy modelu zagrożeń jest po prostu dokumentu, tej dokumentacji reprezentuje również idealny w celu zapewnienia ciągłości wiedzy, przechowywania wnioski uzyskane i pomocy nowego zespołu dołączyć szybko. Na koniec wyniku modelowanie zagrożeń jest umożliwienie należy rozważyć inne aspekty zabezpieczeń, takich jak zobowiązań zabezpieczeń, jakie chcesz zapewnić klientom. Tych zobowiązań w połączeniu z modelowanie zagrożeń będzie informuje i dysków testowania rozwiązania Internetu rzeczy (IoT).

### <a name="when-to-threat-model"></a>Kiedy zagrożenia modelu
[Modelowanie zagrożeń](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) oferuje największa wartość, jeśli jest włączona w fazie projektowania. Podczas projektowania, masz największą elastyczność, aby wprowadzić zmiany w celu wyeliminowania zagrożenia. Eliminowanie zagrożeń zgodnie z projektem jest rezultat. Jest znacznie prostsze niż dodawanie środki zaradcze, ich testowania i zapewnienia są zawsze aktualne, a ponadto takie eliminacji nie zawsze jest możliwe. Staje się przeszkodę w celu wyeliminowania zagrożenia produktu staje się bardziej dojrzałe i z kolei ostatecznie wymaga więcej pracy co znacznie trudniejsze wady i zalety niż zagrożeń na wczesnym etapie modelowania do tworzenia.

### <a name="what-to-threat-model"></a>Co należy modelu zagrożeń
Należy wątku modelu rozwiązania jako całość i również skupić się w następujących obszarach:

* Funkcje zabezpieczeń i prywatności
* Funkcje, których błędy są istotne zabezpieczeń
* Funkcje, które touch granicy zaufania 

### <a name="who-threat-models"></a>Kto zagrożenia modele
Modelowanie zagrożeń jest procesem, jak każdy inny.  Jest dobrym pomysłem jest traktować dokument modelu zagrożeń, podobnie jak inne składnik rozwiązania i sprawdzić jego poprawność. Wiele zespołów deweloperów czy znakomity zadanie przechwytywania wymagania funkcjonalne dla systemu, które korzystać klienci. Jednak identyfikowanie-oczywisty sposób czy ktoś może niewłaściwym użyciem systemu jest trudniejsze. Modelowanie zagrożeń może pomóc zrozumieć, co może zrobić osoba atakująca zespoły deweloperów i dlaczego.

### <a name="how-to-threat-model"></a>Jak modelu zagrożeń
To zagrożenie, proces modelowania składa się z czterech kroków; dostępne są następujące kroki:

* Model aplikacji
* Wyliczanie zagrożeń
* Zmniejszenie zagrożeń związanych
* Sprawdź poprawność środki zaradcze

#### <a name="the-process-steps"></a>Kroki procesu
Trzy zasady przyjąć należy wziąć pod uwagę podczas tworzenia modelu zagrożeń:

1. Tworzenie diagramu poza architektura referencyjna struktury. 
2. Uruchom najpierw szerokości. Zapoznaj się z omówieniem i zrozumieć system jako całość, przed rozpoczęciem pracy bezpośrednich.  Pomaga to zapewnić, że należy szczegółowo w odpowiednich miejscach.
3. Dysk procesu, niech procesu dysk należy. Jeśli znaleźć problemu w fazie modelowania i aby eksplorować go, przejdź na jej!  Nie możesz się slavishly wykonaj następujące kroki.  

#### <a name="threats"></a>Zagrożenia
Są cztery podstawowe elementy modelu zagrożeń:

* Procesy (usługi sieci web, usług Win32 * nix demonów itp. Należy pamiętać, że niektóre jednostki złożonych (na przykład pole bram i czujników) można pobieranej procesu, gdy techniczne przechodzenia w tych obszarach nie jest możliwe.
* Dane przechowywane (tam, gdzie dane są przechowywane, takich jak plik konfiguracji lub bazy danych)
* Przepływ danych (gdzie dane są przenoszone między innymi elementami w aplikacji)
* Podmioty zewnętrzne (wszystkie elementy, które wchodzi w interakcję z systemem, ale nie jest pod kontrolą aplikacji, przykłady obejmują użytkowników oraz urządzeń źródła danych)

Wszystkie elementy na diagramie architektury podlegają różne zagrożenia; używamy skrót klawiszowy krok. Odczyt [modelowania zagrożeń ponownie, krok](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) Aby dowiedzieć się więcej o elementach krok.

Różne elementy na diagramie aplikacji mogą ulec niektórych zagrożeń krok:

* Procesy podlegają krok
* Przepływy danych podlegają TID
* Magazyny danych podlegają TID i czasami R, jeśli pliki dziennika w magazynie danych.
* Jednostek zewnętrznych podlegają SRD

## <a name="security-in-iot"></a>Zabezpieczenia w IoT
Połączonych urządzeń specjalnych dokonano znaczących potencjalnych obszarów powierzchni interakcji i wzorce interakcji, które należy rozważyć zapewniające strukturę zabezpieczanie cyfrowego dostępu do tych urządzeń. Termin "cyfrowego dostępu" jest używany tutaj do odróżnienia od wszystkich operacji wykonywanych za pośrednictwem urządzeń bezpośrednio interakcji gdzie zabezpieczenia dostępu jest zapewniana za pomocą sterowania dostępem fizycznym. Na przykład wprowadzenie urządzenia do miejsca z blokadą na drzwi. Gdy nie można odmówić dostępu fizycznej przy użyciu oprogramowania i sprzętu, mogą środki w celu uniemożliwić fizyczny dostęp od początku do systemu zakłóceń. 

Jak możemy zapoznać się z wzorców interakcji, zajmiemy "kontroli urządzeń" i "dane urządzenie" o tym samym poziomie uwagi. "Urządzenie control" mogą być klasyfikowane jako żadnych informacji, który został dostarczony do urządzenia przez stronę w celu zmiany lub mające wpływ na jego zachowanie w kierunku jej stan lub stanu jego środowiska. "Urządzenie danych" mogą być klasyfikowane jako wszystkie informacje, które urządzenia emituje do innych firm dotyczące stanu i obserwowanych stanu jego środowiska.

Aby zoptymalizować najlepszych rozwiązań dotyczących zabezpieczeń, zaleca się, że typowy architektury IoT podzielić na kilku składników/stref jako część zagrożeń modelowania wykonywania. Te strefy są całkowicie opisane w tej sekcji i obejmują:

* Urządzenie,
* Brama pola
* Bramy, w chmurze i
* Usługi.

Strefy są szerokie sposób posegmentować rozwiązania; każdej strefy ma często wymagania danych i uwierzytelniania i autoryzacji. Strefy można służyć do uszkodzenia izolacji i ograniczyć wpływ niski zaufania strefy na wyższe zaufania strefy.

Każdej strefy są rozdzielone przez granicę zaufania, który jest rejestrowany jako linia kropkowana red na poniższym diagramie. Reprezentuje przejście informacje o i danych z jednego źródła do innego. Podczas tego przejścia danych może podlegać Spoofing, Tampering, Repudiation, ujawnienie informacji, odmowa usługi i podniesienie uprawnień (krok).

![Strefy zabezpieczeń IoT](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Składniki przedstawione w obrębie każdej granicy również są poddawane krok, włączenie pełnego 360 widoku rozwiązania modelowania zagrożeń. W poniższych rozdziałach rozwinięcia wszystkich składników i zagadnienia dotyczące zabezpieczeń określone i rozwiązań, które powinny znajdować się w miejscu.

W kolejnych sekcjach przedstawimy standardowymi elementami, które zwykle znajdują się w tych strefach.

### <a name="the-device-zone"></a>Strefy urządzenia
Środowisko urządzenia jest natychmiastowe fizycznego miejsca wokół urządzenia w przypadku, gdy fizycznego dostępu i/lub "sieci lokalnej" peer-to-peer cyfrowego dostępu do urządzenia jest możliwe. "Sieci lokalnej" zakłada się, że sieci, która jest odrębny i odizolowanego od — ale potencjalnie mostkowania do — publicznego Internetu i zawiera wszystkie urządzenia bezprzewodowego radia technologie, które umożliwia komunikację peer-to-peer urządzeń. Robi *nie* obejmują innych technologii wirtualizacji sieci tworzenie wrażenie sieci lokalnej i również nie zawiera operator publiczny sieci, które wymagają żadne dwa urządzenia komunikują się za pośrednictwem sieci publicznej miejsce ich wprowadź relacji komunikacji peer-to-peer.

### <a name="the-field-gateway-zone"></a>Pole strefy bramy
Brama pole jest urządzeń/urządzenia lub niektóre oprogramowania komputera ogólnego przeznaczenia serwera, który działa jako czynnik komunikacji oraz w razie potrzeby jako system kontroli urządzeń i centrum przetwarzania danych urządzenia. Strefa bramy pola obejmuje brama pola i wszystkie urządzenia, które są dołączone do niego. Jak nazwa wskazuje, bram pola działania urządzenia poza dedykowanych przetwarzania danych, są zwykle lokalizacja powiązana potencjalnie podlegają fizycznych nieautoryzowanego dostępu i będzie ograniczona operacyjne nadmiarowości. Aby powiedzieć, że brama pole jest często przedmiotu jedna touch i przeszkadzają a jest jego funkcji. 

Bramy pola różni się od routera sam ruch, że posiada ona aktywną rolę w zarządzaniu dostępu i przepływem informacji, co oznacza, że jest to aplikacja rozwiązany jednostki i połączenie sieciowe lub sesję terminalu. Urządzenie NAT lub zaporą, natomiast nie kwalifikuje się pole bram, ponieważ nie są jawne połączenie lub terminale sesji, ale raczej połączeń trasy (lub blok) lub wprowadzane za pośrednictwem ich sesji. Brama pole ma dwa różne obszary powierzchni. Jeden skierowany urządzeń, które są dołączone do niego i reprezentuje wewnątrz strefy, a druga skierowany wszystkich podmiotów zewnętrznych i krawędzi strefy.   

### <a name="the-cloud-gateway-zone"></a>Strefy bramy chmury
Brama chmury to system, który umożliwia zdalnej komunikacji z i do urządzeń lub bram pola z wielu różnych lokacji w sieci publicznej przestrzeni, zwykle kierunku kontroli opartej na chmurze i systemu analizy danych, Federacji takich systemów. W niektórych przypadkach brama chmury mogą natychmiast ułatwienia dostępu na urządzeniach specjalnych z terminali, np. tabletów i telefonów. W kontekście omówione w tym miejscu "chmura" jest przeznaczona do odwoływania się do systemu dedykowanych przetwarzania danych, który nie jest powiązany z tej samej lokacji co podłączone urządzenia lub pola bramy. Również w strefie chmury środki operacyjne zapobiec docelowe dostęp fizyczny i niekoniecznie nie są widoczne dla infrastruktury "w chmurze publicznej".  

Brama chmury potencjalnie mogą być mapowane do nakładki wirtualizacji sieci, aby zabezpieczyć bramy chmury oraz wszystkie jego podłączonych urządzeń i bram pole od innego ruchu sieciowego. Brama chmury jest ani system kontroli urządzeń ani przetwarzania lub magazynu dla danych urządzenia. Interfejs te urządzenia bramy chmury. Strefa bramy chmury obejmuje bramy chmury wraz ze wszystkich bram pola i bezpośrednio lub pośrednio dołączone do niego urządzenia. Krawędź strefy jest różne powierzchni gdzie wszystkich podmiotów zewnętrznych komunikują się za pośrednictwem.

### <a name="the-services-zone"></a>Strefa usługi
"Usługa" jest zdefiniowany dla tego kontekstu jako części oprogramowania lub moduł, który jest relacje z urządzeniami za pośrednictwem bramy pola lub chmury do zbierania danych i analizy, a także polecenia i kontroli.  Usługi są mediatorów. One działa na podstawie tożsamości bramy i innych podsystemów, przechowywania i analizowania danych autonomicznie wydać polecenia urządzenia na podstawie wgląd w danych lub harmonogramy i ujawnienie informacji i kontrolowanie możliwości autoryzowanym użytkownikom końcowym.

### <a name="information-devices-vs-special-purpose-devices"></a>Urządzenia informacyjne a specjalnych urządzeń
Komputery, telefony i tablety to przede wszystkim interakcyjne informacji urządzenia. Telefony i tablety jawnie są zoptymalizowane wokół maksymalizacja baterii istnienia. One najlepiej wyłączyć częściowo, gdy nie jest od razu interakcji z osoby lub gdy nie dostarcza usługi, takie jak odtwarzanie muzyki lub skierowanie ich właściciela w określonej lokalizacji. Z punktu widzenia systemy te urządzenia technologii informacji głównie działają jako serwery proxy do osób. Są one "osób siłowniki" sugerowanie "osób czujniki" zbieranie danych wejściowych i akcje. 

Urządzenia specjalnych z czujnikami temperatury proste do wierszy produkcyjnego złożonych fabryki z tysiącami elementów zawartych w nich, są różne. W celu bardziej ograniczone tych urządzeń i nawet wtedy, gdy udostępniają część interfejsu użytkownika znacznym stopniu dostosowanych do powiązania z lub można zintegrować zasoby w świecie rzeczywistym. One mierzyć i raportu okoliczności środowiska, Włącz zawory, kontroli servos, dźwiękowej alarmy, przełącznika świateł i wykonywać inne zadania. Do pracy pomagają, dla których urządzenie informacji jest zbyt ogólne, zbyt drogie, za duży lub zbyt łamliwa. Konkretnego celu natychmiast nakazują ich projektu technicznego jako również dostępnego budżetu pieniężnego ich produkcji i okres istnienia zaplanowanych operacji. Kombinacja tych dwóch kluczowych czynników ogranicza dostępne operacyjne budżetu energii, fizycznego miejsca i w związku z tym dostępny magazyn, zasobów obliczeniowych i funkcje zabezpieczeń.  

Jeśli coś "umieszczane niewłaściwy" Automatyczna lub z zdalnego urządzenia kontrolowane, na przykład wad fizycznego lub logicznego sterowania wady willful próby uzyskania nieautoryzowanego dostępu i manipulowania nimi. Niszczone mogą partie produkcji, budynki może looted lub kiedyś w dół i osób może być struktury poszkodowanej lub nawet. Jest to oczywiście całego inną klasę uszkodzenia niż ktoś maxing się limit kradzieży karty kredytowej. Poziom zabezpieczeń dla urządzeń, które należy przenieść elementy, a także do danych czujnika, który ostatecznie powoduje poleceń, które powodują rzeczy, które należy przenieść, musi być wyższy niż w handlu elektronicznego lub scenariusz bankowości. 

### <a name="device-control-and-device-data-interactions"></a>Kontroli urządzeń i ich interakcje danych urządzenia
Połączonych urządzeń specjalnych dokonano znaczących potencjalnych obszarów powierzchni interakcji i wzorce interakcji, które należy rozważyć zapewniające strukturę zabezpieczanie cyfrowego dostępu do tych urządzeń. Termin "cyfrowego dostępu" jest używany tutaj do odróżnienia od wszystkich operacji wykonywanych za pośrednictwem urządzeń bezpośrednio interakcji gdzie zabezpieczenia dostępu jest zapewniana za pomocą sterowania dostępem fizycznym. Na przykład wprowadzenie urządzenia do miejsca z blokadą na drzwi. Gdy nie można odmówić dostępu fizycznej przy użyciu oprogramowania i sprzętu, mogą środki w celu uniemożliwić fizyczny dostęp od początku do systemu zakłóceń. 

Jak możemy zapoznać się z wzorców interakcji, zajmiemy "kontroli urządzeń" i "dane urządzenie" o tym samym poziomie uwagi podczas modelowania zagrożeń. "Urządzenie control" mogą być klasyfikowane jako żadnych informacji, który został dostarczony do urządzenia przez stronę w celu zmiany lub mające wpływ na jego zachowanie w kierunku jej stan lub stanu jego środowiska. "Urządzenie danych" mogą być klasyfikowane jako wszystkie informacje, które urządzenia emituje do innych firm dotyczące stanu i obserwowanych stanu jego środowiska. 

## <a name="threat-modeling-the-azure-iot-reference-architecture"></a>Zagrożenia modelowania architektura referencyjna Azure IoT
Firma Microsoft używa framework opisanych powyżej w celu modelowania dla Azure IoT zagrożeń. W poniższej sekcji w związku z tym używamy konkretny przykład architektura referencyjna IoT platformy Azure aby zademonstrować sposób pomyśleć o zagrożeń modelowania dla IoT i eliminowania zagrożeń zidentyfikowane. W tym przypadku określiliśmy cztery główne obszary fokus:

* Urządzenia i źródeł danych
* Transport danych
* Urządzenia i przetwarzania zdarzeń i
* Prezentacji

![Zagrożenia modelowania dla Azure IoT](media/iot-security-architecture/iot-security-architecture-fig2.png) 

Na poniższym diagramie oferuje uproszczony widok architektury IoT firmy Microsoft, za pomocą modelu Diagram przepływu danych, który jest używany przez narzędzie modelowania zagrożeń firmy Microsoft:

![Zagrożenia modelowania dla Azure IoT przy użyciu narzędzia do modelowania zagrożeń MS](media/iot-security-architecture/iot-security-architecture-fig3.png)

Należy pamiętać, że architektura oddziela możliwości urządzenia i bramy. Umożliwia użytkownikowi korzystać z urządzenia bramy, które są bardziej bezpieczne: mogą komunikować się z bramy chmury przy użyciu protokołów bezpieczny, co zwykle wymaga większej przetwarzania natywnego urządzenie — takie jak termostacie — można zapewnić na jego własnej. W strefie usługi Azure przyjęto założenie, że brama chmury jest reprezentowany przez usługę Azure IoT Hub.

### <a name="device-and-data-sourcesdata-transport"></a>Transport źródeł/danych urządzenia i danych
W tej sekcji Eksploruje architektura opisanych powyżej przez obiektyw modelowanie zagrożeń i powinien zawierać omówienie jak możemy są związane z adresowaniem niektóre problemy związane. Firma Microsoft koncentruje się na podstawowych składników modelu zagrożeń:

* Procesy (zawarte w naszym kontroli i elementów zewnętrznych)
* Komunikacja (nazywanych również przepływów danych)
* Magazyn (nazywanych również magazyny danych)

#### <a name="processes"></a>Procesy
W każdej kategorii, opisane w architekturze Azure IoT spróbujemy ograniczyć liczbę różnych zagrożeń na różnych etapach informacje o i danych istnieje w: proces, komunikację i magazynu. Poniżej możemy podać omówienie najbardziej typowe dla kategorii "proces", następuje przegląd jak te mogą być najlepiej skorygowane: 

**Fałszowanie zawartości (S)**: osoba atakująca może wyodrębnić materiał kluczy kryptograficznych z urządzenia, albo na poziomie oprogramowania lub sprzętu, a następnie podjęto dostępu do sieci z innego urządzenia fizyczne lub wirtualne z tożsamością urządzenia materiału klucza z. Dobrym ilustracja to zdalnego sterowania, który można włączyć wszystkie TV i które są prankster popularne narzędzia.

**Odmowa usługi (D)**: urządzenie może być renderowana niezdolne do funkcjonowania lub komunikacji przez zakłócać częstotliwości lub wycinanie przewodów. Na przykład aparatu nadzoru, który miał jego zasilania lub połączenia sieciowego celowo wycinane ani zgłaszać danych, w ogóle.

**Manipulowanie (T)**: osoba atakująca może częściowo lub całkowicie zastąpić oprogramowania działającego na urządzeniu, potencjalnie stosowanie zastąpionego oprogramowania wykorzystać oryginalnego tożsamości urządzenia, jeśli materiału klucza lub funkcji kryptograficznych, zawierający klucza materiałów były dostępne do nielegalnego program. Na przykład osoba atakująca może wykorzystać wyodrębnionego materiału klucza przechwycenia i Pomiń danych z urządzenia w ścieżce komunikacji i zamień ją na wartość false dane, które są uwierzytelniani kradzieży materiału klucza.

**Ujawnienie informacji, (I)**: Jeśli urządzenie działa manipulować oprogramowania, takie oprogramowanie manipulować może potencjalnie wycieku danych do osoby nieupoważnione. Na przykład osoba atakująca może wykorzystać wyodrębnionego materiału klucza iniekcję się do ścieżki komunikacji między urządzenia i brama kontrolera lub pola lub brama chmury do Lewarek poza informacji.

**Podniesienie uprawnień (E)**: urządzenie, które wykonuje określoną funkcję można wymusić, aby zrobić coś innego. Na przykład zawór zaprogramowane w taki sposób, aby otworzyć połowie można zamiarem otworzyć całej procedury.

| **Składnik** | **Zagrożenia** | **Środki zaradcze** | **Ryzyko** | **Implementacja** |
| --- | --- | --- | --- | --- |
| Urządzenie |S |Przypisywanie tożsamości na urządzeniu i uwierzytelniania urządzenia |Zastępując urządzenia lub częścią urządzenia inne urządzenie. Jak wiemy, że firma Microsoft mówimy na odpowiednim urządzeniu? |Uwierzytelniania urządzenia, za pomocą zabezpieczeń TLS (Transport Layer) lub protokołu IPSec. Infrastruktura powinna obsługiwać przy użyciu klucza wstępnego (PSK) na tych urządzeniach, które nie może obsłużyć pełnej asymetrycznego kryptografii. Wykorzystanie usługi Azure AD, [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Na przykład zastosować na urządzeniu mechanizmów tamperproof czyniąc ją bardzo trudne do niemożliwe do wyodrębnienia kluczy i innych materiałów kryptograficznych z urządzenia. |Ryzyko jest, jeśli ktoś jest manipulowanie nimi urządzenia (zakłócenia fizycznych). W jaki sposób możemy pewności, czy urządzenie nie zmodyfikowany. |Optymalne ograniczenie jest TPM możliwości module (TPM), która umożliwia przechowywanie kluczy w specjalne obwody w układzie, z którego nie można odczytać klawiszy, ale można używać tylko dla operacji kryptograficznych, które używają klucza, ale nigdy nie ujawniają klucz. Szyfrowanie pamięci urządzenia. Zarządzanie kluczami dla urządzenia. Podpisywanie kodu. | |
| E |Zapewniający kontrolę dostępu do urządzenia. Schemat autoryzacji. |Jeśli urządzenie zezwala poszczególnych czynności do wykonania oparte na polecenia ze źródła zewnętrznego lub nawet złamany czujników, umożliwi ataku w celu wykonania operacji nie dostępne. |Po autoryzacji schematu dla urządzenia | |
| Pole bramy |S |Uwierzytelnianie bramy pola do bramy chmury (certyfikat na podstawie, PSK, oświadczenia na podstawie,...). |Jeśli ktoś może spreparować pola bramy, następnie go może być wyświetlany jako dowolnego urządzenia. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). Te same klucza magazynu i zaświadczania dotyczy urządzeń, na ogół — najlepszy jest użyć modułu TPM. Rozszerzenie 6LowPAN dla protokołu IPSec do obsługi bezprzewodowej sieci czujnik (WSN). |
| TRID |Ochrona bramy pola przed naruszeniem (module TPM)? |Fałszowanie atakami wymuszać planowania bramy chmury, które rozmawia pola bramy może spowodować ujawnienie informacji i modyfikowaniu danych |Pamięć szyfrowania, modułu TPM firmy, uwierzytelniania. | |
| E |Mechanizmu kontroli dostępu dla pola bramy | | | |

Poniżej przedstawiono przykładowe zagrożenia w tej kategorii:

Fałszowanie: Osoba atakująca może wyodrębnić materiał kluczy kryptograficznych z urządzenia, albo w oprogramowania lub sprzętu poziomu, a następnie dostępu do sieci z innego urządzenia fizyczne lub wirtualne z tożsamością urządzenia materiału klucza jest zajęta z.

**Odmowa usługi**: urządzenie może być renderowana niezdolne do funkcjonowania lub komunikacji przez zakłócać częstotliwości lub wycinanie przewodów. Na przykład aparatu nadzoru, który miał jego zasilania lub połączenia sieciowego celowo wycinane ani zgłaszać danych, w ogóle.

**Manipulowanie**: osoba atakująca może częściowo lub całkowicie zastąpić oprogramowania działającego na urządzeniu, potencjalnie stosowanie zastąpionego oprogramowania wykorzystać oryginalnego tożsamości urządzenia, jeśli materiału klucza lub funkcji kryptograficznych, zawierający klucza materiałów były dostępne do nielegalnego program.

**Manipulowanie**: fotografia takie korytarz może mieć na celu kamery nadzoru, który jest wyświetlany obraz widoczne spektrum korytarz pusty. Czujnik dymu lub fire może być raportowania ktoś zawierający jaśniejszego w nim. W obu przypadkach urządzenie może być technicznie pełni zaufanego do systemu, ale będzie zgłaszać manipulować informacji.

**Manipulowanie**: osoba atakująca może wykorzystać wyodrębnionego materiału klucza przechwycenia i Pomiń danych z urządzenia w ścieżce komunikacji i zamień ją na wartość false dane, które są uwierzytelniani kradzieży materiału klucza.

**Manipulowanie**: osoba atakująca może częściowo lub całkowicie zastąpić oprogramowania działającego na urządzeniu, potencjalnie stosowanie zastąpionego oprogramowania wykorzystać oryginalnego tożsamości urządzenia, jeśli materiału klucza lub funkcji kryptograficznych, zawierający klucza materiałów były dostępne do nielegalnego program.

**Ujawnienie informacji**: Jeśli urządzenie działa manipulować oprogramowania, takie oprogramowanie manipulować może potencjalnie wycieku danych do osoby nieupoważnione.

**Ujawnienie informacji**: osoba atakująca może wykorzystać wyodrębnionego materiału klucza iniekcję się do ścieżki komunikacji między bramy urządzenia i kontrolera lub pola lub brama chmury do Lewarek poza informacji.

**Odmowa usługi**: wyłączone lub włączone w trybie, gdy komunikacja nie jest możliwe (która jest zamierzone, w wielu maszyn przemysłowych) urządzenia.

**Manipulowanie**: urządzenie można tak skonfigurować, aby w stan nieznany system kontroli (poza odwzorowania znane parametry) i w związku z tym świadczenia dane, które mogą zostać błędnie zinterpretowane

**Podniesienie uprawnień**: urządzenie, które wykonuje określoną funkcję można wymusić, aby zrobić coś innego. Na przykład zawór zaprogramowane w taki sposób, aby otworzyć połowie można zamiarem otworzyć całej procedury.

**Odmowa usługi**: urządzenie można włączyć w stanie, w których komunikacja nie jest możliwe.

**Manipulowanie**: urządzenie można tak skonfigurować, aby w stan nieznany system kontroli (poza odwzorowania znane parametry) i w związku z tym świadczenia dane, które mogą zostać błędnie zinterpretowane.

**Fałszowanie/Tampering/Repudiation**: Jeśli nie jest zabezpieczone (która jest rzadko w przypadku klienta zdalnego sterowania) atakujący można manipulować anonimowo stan urządzenia. Dobrym ilustracja to zdalnego sterowania, który można włączyć wszystkie TV i które są prankster popularne narzędzia.

#### <a name="communication"></a>Komunikacja
Zagrożenia ścieżkę komunikacji między urządzeniami, urządzeń i bram pola i bramy urządzenia i w chmurze. W poniższej tabeli ma wskazówek wokół otwarte gniazda na urządzeniu lub sieć VPN:

| **Składnik** | **Zagrożenia** | **Środki zaradcze** | **Ryzyko** | **Implementacja** |
| --- | --- | --- | --- | --- |
| Centrum IoT urządzenia |TID |(D) TLS (PSK/RSA) do szyfrowania ruchu |Podsłuchiwaniu lub konfliktu komunikacji między urządzeniem i bramy |Zabezpieczenia na poziomie protokołu. Z protokoły niestandardowe należy dowiedzieć się, jak chronić je. W większości przypadków komunikacja odbywa się z urządzenia z Centrum IoT (urządzenie inicjuje połączenie). |
| Urządzenie urządzenie |TID |(D) (PSK/RSA) do szyfrowania ruchu TLS. |Odczytywanie danych przesyłanych między urządzeniami. Manipulowanie danymi. Przeciążanie urządzenia o nowe połączenia |Zabezpieczenia na poziomie protokołu (MQTT/AMQP/HTTP/CoAP. Z protokoły niestandardowe należy dowiedzieć się, jak chronić je. Środki zaradcze na zagrożenie DoS jest elementu równorzędnego urządzeń za pośrednictwem bramy chmury lub pola i niech act tylko jako klientów do sieci. Komunikację równorzędną może spowodować bezpośrednie połączenie między komputerami równorzędnymi po o została przeprowadzana przez bramę |
| Urządzenie zewnętrznej jednostki |TID |Silne parowanie zewnętrznej jednostki do urządzenia |Podsłuchiwaniu połączenie z urządzeniem. Konfliktu komunikacji z urządzeniem |Bezpiecznie parowanie zewnętrznej jednostki do LE NFC/Bluetooth urządzenia. Kontrolowanie panelu operacyjny urządzenia (fizycznych) |
| Brama chmury bramy pola |TID |(PSK/RSA) do szyfrowania ruchu TLS. |Podsłuchiwaniu lub konfliktu komunikacji między urządzeniem i bramy |Zabezpieczenia na poziomie protokołu (MQTT/AMQP/HTTP/CoAP). Z protokoły niestandardowe należy dowiedzieć się, jak chronić je. |
| Urządzenia bramy chmury |TID |(PSK/RSA) do szyfrowania ruchu TLS. |Podsłuchiwaniu lub konfliktu komunikacji między urządzeniem i bramy |Zabezpieczenia na poziomie protokołu (MQTT/AMQP/HTTP/CoAP). Z protokoły niestandardowe należy dowiedzieć się, jak chronić je. |

Poniżej przedstawiono przykładowe zagrożenia w tej kategorii:

**Odmowa usługi**: ograniczonego urządzeń są zwykle zagrożona DoS podczas ich aktywnie nasłuchiwać połączeń przychodzących lub niechciane datagramy w sieci, ponieważ atakujący może otwierać wiele połączeń równolegle i nie ich usługi lub ich bardzo wolno usługi lub urządzenie może zostać przeciążony niepożądanego ruchu. W obu przypadkach urządzenia mogą skutecznie przestać działać w sieci.

**Fałszowania, ujawnienia informacji**: ograniczone i urządzenia specjalnych często mają zabezpieczeń co dla wszystkich urządzeń, takich jak hasła lub numeru PIN ochrony lub całkowicie opierają się na ufające sieci, co oznacza, gdy urządzenie jest w tej samej sieci, a sieci często tylko jest chroniony przez klucz współużytkowany przyznać dostęp do informacji. Oznacza to, że gdy przekazywanych wspólny klucz tajny dla urządzenia lub sieci jest możliwość sterowania urządzeniem lub obserwować dane wysyłanego z urządzenia.  

**Fałszowanie**: osoba atakująca może przechwycić lub częściowo zastąpić emisji i sfałszowanie inicjatorem (man w środku)

**Manipulowanie**: osoba atakująca może przechwycić lub częściowo zastąpić emisji i wysłać fałszywe informacje 

**Ujawnienie informacji:** osoba atakująca może podsłuchiwać emisji i uzyskiwanie informacji bez autoryzacji **"odmowa usługi":** osoba atakująca może zablokowania emisji sygnału i odmowy dystrybucji informacji

#### <a name="storage"></a>Magazyn
Co brama urządzenia i pole ma jakiegoś magazynu (tymczasowy dla usługi kolejkowania wiadomości danych, magazynu obrazu systemu operacyjnego (OS)).

| **Składnik** | **Zagrożenia** | **Środki zaradcze** | **Ryzyko** | **Implementacja** |
| --- | --- | --- | --- | --- |
| Urządzenia magazynu |TRID |Szyfrowanie magazynu, podpisywania dzienniki |Odczytywanie danych z magazynu (dane osobowe dane), manipulowanie danymi telemetrii. Manipulowanie Zakolejkowane lub polecenia kontroli danych w pamięci podręcznej. Wprowadzanie zmian w konfiguracji lub oprogramowania układowego pakietów aktualizacji w pamięci podręcznej lub lokalnie w kolejce może prowadzić do składników systemu operacyjnego i/lub system naruszenia bezpieczeństwa |Szyfrowanie, kod uwierzytelniania wiadomości (MAC) lub podpisu cyfrowego. Gdzie kontroli dostępu możliwości, silne za pośrednictwem dostęp do zasobów kontroli list (kontroli dostępu ACL) lub uprawnienia. |
| Obraz systemu operacyjnego urządzenia |TRID | |Manipulowanie systemu operacyjnego / zastępowania składników systemu operacyjnego |Tylko do odczytu partycji systemu operacyjnego, podpisany obrazu systemu operacyjnego, szyfrowania |
| Magazyn bramy pola (kolejkowania danych) |TRID |Szyfrowanie magazynu, podpisywania dzienniki |Odczytywanie danych z magazynu (dane osobowe dane), manipulowanie danymi telemetrii ingerencji w kolejce lub polecenia kontroli danych w pamięci podręcznej. Wprowadzanie zmian w konfiguracji lub oprogramowania układowego pakietów aktualizacji (przeznaczonych dla urządzenia lub pola bramy) podczas buforowane lub lokalnie w kolejce może prowadzić do składników systemu operacyjnego i/lub system naruszenia bezpieczeństwa |Funkcja BitLocker |
| Obraz systemu operacyjnego bramy pola |TRID | |Manipulowanie systemu operacyjnego / zastępowania składników systemu operacyjnego |Tylko do odczytu partycji systemu operacyjnego, podpisany obrazu systemu operacyjnego, szyfrowania |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Urządzenia i zdarzenia strefy bramy przetwarzania/w chmurze
Brama chmury to system, który umożliwia zdalnej komunikacji z i do urządzeń lub bram pola z wielu różnych lokacji w sieci publicznej przestrzeni, zwykle kierunku kontroli opartej na chmurze i systemu analizy danych, Federacji takich systemów. W niektórych przypadkach brama chmury mogą natychmiast ułatwienia dostępu na urządzeniach specjalnych z terminali, np. tabletów i telefonów. W kontekście omówione w tym miejscu "chmura" jest przeznaczona do odwoływania się do systemu dedykowanych przetwarzania danych, który nie jest powiązany z tej samej lokacji co podłączone urządzenia lub pola bramy, i gdy środki operacyjne zapobiec docelowe fizyczny dostęp, ale nie jest niezbędne do infrastruktury "w chmurze publicznej".  Brama chmury potencjalnie mogą być mapowane do nakładki wirtualizacji sieci, aby zabezpieczyć bramy chmury oraz wszystkie jego podłączonych urządzeń i bram pole od innego ruchu sieciowego. Brama chmury jest ani system kontroli urządzeń ani przetwarzania lub magazynu dla danych urządzenia. Interfejs te urządzenia bramy chmury. Strefa bramy chmury obejmuje bramy chmury wraz ze wszystkich bram pola i bezpośrednio lub pośrednio dołączone do niego urządzenia.

Brama chmury jest głównie niestandardowych wbudowanych oprogramowanie jako usługa z punktami końcowymi narażonych, z którymi się łączyć pola bramy i urządzeń. Jako takie muszą być zaprojektowane z myślą o bezpieczeństwie. Wykonaj [SDL](http://www.microsoft.com/sdl) proces projektowania i tworzenia tej usługi. 

#### <a name="services-zone"></a>Strefa usługi
System kontroli (lub kontrolera) jest rozwiązaniem oprogramowania, które z urządzeniem, lub brama pola lub brama chmury na potrzeby kontrolowania jednego lub wielu urządzeń i/lub do zbierania i/lub przechowywania i/lub analizować dane urządzenie prezentacji lub celów kolejnych kontroli. Systemów kontroli są jednostkami tylko w zakresie tej dyskusji, która może ułatwić natychmiast interakcji z użytkownikami. Wyjątek stanowi pośredni fizycznych powierzchni na urządzeniach, takich jak przełącznik, który umożliwia użytkownikowi wyłączyć urządzenie lub zmienić inne właściwości i dla którego nie ma odpowiednika funkcjonalności, które mogą uzyskiwać cyfrowo. 

Pośredni fizycznych powierzchni są gdzie dowolny rodzaj logiki regulujące ogranicza funkcji powierzchni fizycznych tak, aby zdalnie można zainicjować odpowiedniki lub można uniknąć konfliktów wejściowego przy użyciu zdalnego danych wejściowych — takich intermediated powierzchni koncepcyjnie są dołączone do system kontroli lokalnego, który korzysta z funkcji podstawowych innym systemom zdalnego sterowania, jaki urządzenie może zostać dołączony do równolegle. Górny zagrożeń dotyczących chmury obliczeniowej, może być odczytany przy [chmury zabezpieczeń Alliance (CSA)](https://cloudsecurityalliance.org/research/top-threats/) strony.

## <a name="additional-resources"></a>Dodatkowe zasoby
Zobacz następujące artykuły, aby uzyskać dodatkowe informacje:

* [Narzędzie modelowania zagrożeń SDL](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Architektura referencyjna IoT Azure firmy Microsoft](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

## <a name="see-also"></a>Zobacz też
Aby dowiedzieć się więcej na temat zabezpieczania rozwiązania IoT, zobacz [zabezpieczania wdrożenia IoT][lnk-security-deployment].

Możesz także wypróbować niektóre inne funkcje i możliwości wstępnie skonfigurowanych rozwiązań Pakietu IoT:

* [Omówienie rozwiązania konserwacji predykcyjnej wstępnie][lnk-predictive-overview]
* [Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]

Możesz przeczytać o zabezpieczeniach Centrum IoT w [kontrolować dostęp do Centrum IoT] [ lnk-devguide-security] w Podręczniku dewelopera Centrum IoT.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md