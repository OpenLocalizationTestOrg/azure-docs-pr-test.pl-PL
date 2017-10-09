---
title: "Funkcje aparatu reguł aaaAzure CDN | Dokumentacja firmy Microsoft"
description: "Dokumentacja referencyjna dla usługi Azure CDN zasady warunków dopasowania aparatu i funkcje."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Zasady usługi Azure CDN aparat funkcji
Ten temat zawiera szczegółowe opisy dostępnych funkcji powitania dla Azure Content Delivery Network (CDN) [aparatu reguł](cdn-rules-engine.md).

Hello trzeci część reguły jest funkcja hello. Funkcja definiuje typ hello akcji, który ma być stosowany toohello typ żądania identyfikowane przez zestaw warunków dopasowania.

## <a name="access"></a>Dostęp

Te funkcje są zaprojektowane toocontrol toocontent dostępu.


Nazwa | Przeznaczenie
-----|--------
Odmowa dostępu | Określa, czy wszystkie żądania są odrzucane odpowiedź 403 Zabroniony.
Token uwierzytelniania | Określa, czy tokenów uwierzytelniania będzie stosowane tooa żądania.
Kod odmowa tokenu uwierzytelniania | Określa typ hello odpowiedź zwracana użytkownika tooa Jeśli żądanie zostanie odrzucone powodu uwierzytelniania opartego na tooToken.
Token uwierzytelniania Ignoruj wielkość liter adresu URL | Określa, czy wprowadzone przez uwierzytelniania opartego na tokenie porównania adres URL będzie uwzględniana wielkość liter.
Parametr tokenu uwierzytelniania | Określa, czy parametr ciągu zapytania uwierzytelniania opartego na tokenie hello powinny zostać zmienione.

### <a name="deny-access"></a>Odmowa dostępu
**Cel**: Określa, czy wszystkie żądania są odrzucane odpowiedź 403 Zabroniony.

Wartość | wynik
------|-------
Enabled (Włączony)| Powoduje, że wszystkie żądania, które spełniają hello pasującego toobe kryteria odrzucane odpowiedź 403 Zabroniony.
Disabled (Wyłączony)| Przywraca hello domyślne zachowanie. Witaj domyślne zachowanie to tooallow powitania serwera toodetermine hello typ źródła odpowiedzi, który zostanie zwrócony.

**Domyślne zachowanie**: wyłączone

> [!TIP]
   > Jedno możliwe użycie tej funkcji jest tooassociate go przy użyciu nagłówka żądania odpowiada warunku tooblock dostępu tooHTTP odwołań, korzystających z wbudowanym łącza tooyour zawartości.

### <a name="token-auth"></a>Token uwierzytelniania
**Cel:** Określa, czy tokenów uwierzytelniania będzie stosowane tooa żądania.

Włączenie uwierzytelniania opartego na tokenie tylko żądania, które zapewniają zaszyfrowany token i wykonania toohello wymagania określone przez token będą honorowane.

Hello klucza szyfrowania, które będą używane wartości tooencrypt i odszyfrowywania tokenu jest określana przez klucz podstawowy i opcje tworzenia kopii zapasowej klucza na stronie tokenu uwierzytelniania. Należy pamiętać, że klucze szyfrowania są specyficzne dla platformy.

Wartość | wynik
------|---------
Enabled (Włączony) | Chroni hello żądanej zawartości przy użyciu uwierzytelniania opartego na tokenie. Tylko żądania od klientów, podaj prawidłowy token, które spełniają jej wymagań dotyczących będą honorowane. Transakcje FTP są wykluczone z uwierzytelniania opartego na tokenie.
Disabled (Wyłączony)| Przywraca hello domyślne zachowanie. Witaj domyślne zachowanie jest tooallow Twojego toodetermine konfiguracji uwierzytelniania opartego na tokenie, czy żądanie będzie zabezpieczony.

**Domyślne zachowanie:** wyłączone.

###<a name="token-auth-denial-code"></a>Kod odmowa tokenu uwierzytelniania
**Cel:** Określa typ hello odpowiedź zwracana użytkownika tooa Jeśli żądanie zostanie odrzucone powodu uwierzytelniania opartego na tooToken.

Kody odpowiedzi dostępne Hello są wymienione poniżej.

Kod odpowiedzi|Nazwa odpowiedzi|Opis
----------------|-----------|--------
301|Trwale przeniesiona|Ten kod stanu przekierowania określony w nagłówku lokalizacji URL toohello nieautoryzowanych użytkowników.
302|Znaleziono|Ten kod stanu przekierowania określony w nagłówku lokalizacji URL toohello nieautoryzowanych użytkowników. Ten kod stanu jest hello standardowa metoda wykonywania przekierowania.
307|Przekierowanie tymczasowe|Ten kod stanu przekierowania określony w nagłówku lokalizacji URL toohello nieautoryzowanych użytkowników.
401|Brak autoryzacji|Łączenie z nagłówka WWW-Authenticate odpowiedzi ten kod stanu umożliwia tooprompt użytkownika do uwierzytelniania.
403|Dostęp zabroniony|Jest to standardowe 403 Zabroniony stan wiadomości powitania nieautoryzowany użytkownik zostanie wyświetlony, gdy w trakcie tooaccess zawartości chronionej.
404|Nie można odnaleźć pliku|Ten kod stanu wskazuje, że klient HTTP hello był stanie toocommunicate z serwerem hello, ale hello zażądał nie odnaleziono zawartości.

#### <a name="url-redirection"></a>Adres URL przekierowania

Ta funkcja obsługuje URL zdefiniowane przez użytkownika adresu URL przekierowania tooa, gdy jest skonfigurowany tooreturn 3xx kod stanu. Ten adres URL zdefiniowany przez użytkownika, można określić, wykonując następujące kroki hello:

1. Wybierz kod odpowiedzi 3xx hello Token uwierzytelniania odmowa kodu funkcji.
2. Wybierz "Lokalizacja" z opcją opcjonalna nazwa nagłówka.
3. Ustaw adres URL żądanego toohello opcji opcjonalna wartość nagłówka.

Jeśli adres URL nie jest zdefiniowany dla kodu stanu 3xx, następnie hello strony standardowe odpowiedzi dla kodu stanu 3xx zostanie zwrócony toohello użytkownika.

Adres URL przekierowania dotyczy tylko 3xx kody odpowiedzi.

Opcja opcjonalna wartość nagłówka obsługuje znaki alfanumeryczne, znaki cudzysłowu i spacje.

#### <a name="authentication"></a>Authentication

Ta funkcja obsługuje nagłówka WWW-Authenticate tooinclude możliwości hello wysyłanej tooan nieautoryzowanego żądania dla zawartości chronionej przez uwierzytelniania opartego na tokenie. Jeżeli nagłówek WWW-Authenticate ustawiono zbyt "basic" w konfiguracji, następnie hello nieautoryzowany użytkownik pojawi się monit o poświadczenia konta.

Witaj powyżej konfiguracji można osiągnąć, wykonując następujące kroki hello:

1. Wybierz "401" jako kod odpowiedzi hello hello Token uwierzytelniania odmowa kodu funkcji.
2. Wybierz "WWW-Authenticate" z opcją opcjonalna nazwa nagłówka.
3. Ustaw opcję opcjonalna wartość nagłówka zbyt "podstawowa."

Nagłówek WWW-Authenticate dotyczy tylko kodów odpowiedzi 401.

### <a name="token-auth-ignore-url-case"></a>Token uwierzytelniania Ignoruj wielkość liter adresu URL
**Cel:** Określa, czy wprowadzone przez uwierzytelniania opartego na tokenie porównania adres URL będzie uwzględniana wielkość liter.

Parametry Hello wpływ tej funkcji są:

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

Prawidłowe wartości to:

Wartość|wynik
---|----
Enabled (Włączony)|Powoduje, że nasze serwer graniczny przypadku tooignore podczas porównywania adresów URL dla uwierzytelniania opartego na tokenie parametrów.
Disabled (Wyłączony)|Przywraca hello domyślne zachowanie. Witaj domyślne zachowanie to dla adresu URL porównań toobe tokenu uwierzytelniania z uwzględnieniem wielkości liter.

**Domyślne zachowanie:** wyłączone.
 
### <a name="token-auth-parameter"></a>Parametr tokenu uwierzytelniania
**Cel:** Określa, czy parametr ciągu zapytania uwierzytelniania opartego na tokenie hello powinny zostać zmienione.

Informacje o kluczu:

- Opcja wartość definiuje hello Nazwa parametru ciągu kwerendy za pośrednictwem której można określić token.
- Nie można ustawić opcji wartość zbyt "ec_token."
- Upewnij się, tę nazwę hello zdefiniowane w opcji tylko wartości 
- zawiera nieprawidłowy adres URL znaki.

Wartość|wynik
----|----
Enabled (Włączony)|Opcja wartość definiuje hello Nazwa parametru ciągu kwerendy za pośrednictwem której można zdefiniować tokenów.
Disabled (Wyłączony)|Tokenu można określić jako parametr ciągu zapytania niezdefiniowana w adresie URL żądania hello.

**Domyślne zachowanie:** wyłączone. Tokenu można określić jako parametr ciągu zapytania niezdefiniowana w adresie URL żądania hello.

## <a name="caching"></a>Buforowanie

Te funkcje są zaprojektowane toocustomize sposób zawartość jest buforowana i.

Nazwa | Przeznaczenie
-----|--------
Parametry przepustowości | Określa, czy przepustowości parametrów (tj. ec_rate i ec_prebuf) będzie aktywny.
Ograniczanie przepustowości | Ogranicza przepustowość hello odpowiedź hello udostępniane przez serwery krawędzi.
Pomiń pamięć podręczną | Określa, czy hello żądania mogą korzystać z naszych technologię buforowania.
Traktowanie nagłówek Cache-Control | Formanty hello generowania nagłówków Cache-Control przez serwer graniczny hello włączeniu funkcji zewnętrznych Max-Age.
Ciąg zapytania klucz pamięci podręcznej | Określa, czy klucz pamięci podręcznej hello zostaną dołączone lub wykluczone parametrów ciągu zapytania skojarzonego z żądaniem.
Napisz ponownie klucz pamięci podręcznej | Ponownie zapisuje klucz pamięci podręcznej hello skojarzone z żądaniem.
Zakończenie wypełnienie pamięci podręcznej | Określa, co się stanie, gdy żądanie powoduje Chybienie pamięci podręcznej częściowe na serwer graniczny.
Kompresuj typów plików | Definiuje hello formatów plików, które zostanie skompresowany na powitania serwera.
Max-Age wewnętrzny domyślne | Określa hello domyślny interwał maksymalny wiek ponowna Walidacja buforu serwera tooorigin serwer krawędzi.
Wygasa traktowania nagłówka | Formanty hello generowania Expires headers przez serwer graniczny, gdy funkcji zewnętrznych Max-Age hello jest aktywny.
Max-Age zewnętrznych | Określa interwał maksymalny wiek hello przeglądarki tooedge serwera pamięci podręcznej ponownego sprawdzania poprawności.
Wymuszanie wewnętrznych Max-Age. | Określa interwał maksymalny wiek hello ponowna Walidacja buforu serwera tooorigin serwer krawędzi.
Obsługa H.264 (pobierania progresywnego HTTP) | Określa typy hello H.264 formaty plików, które mogą być używane toostream zawartości.
Honoruj No-Cache żądania | Określa, czy klient HTTP żądań pamięci podręcznej nie zostanie przekazany toohello serwera źródłowego.
Ignoruj pochodzenia No-Cache | Określa, czy naszych CDN zignoruje niektórych dyrektyw z serwera pochodzenia.
Ignoruj Unsatisfiable zakresów | Określa odpowiedź hello, która zostanie zwrócona tooclients po żądanie generuje 416 żądany zakres nie niewłaściwego kod stanu.
Wewnętrzny odświeżona maksymalna | Określa, jak długo minął czas wygaśnięcia normalne hello zasobów pamięci podręcznej może być obsługiwana z serwer graniczny po serwer graniczny hello toorevalidate hello buforowanych zasobów z serwera źródłowego hello.
Udostępnianie częściowe pamięci podręcznej | Określa, czy żądanie może wygenerować częściowo buforowaną zawartość.
Prevalidate zawartości w pamięci podręcznej | Określa, czy przed wygaśnięciem wartość TTL będzie kwalifikuje się do wcześniejszego ponowna Walidacja zawartości w pamięci podręcznej.
Odśwież Zero bajtów pamięci podręcznej plików | Określa sposób obsługi żądania klienta HTTP dla trwałego 0 bajtów pamięci podręcznej przez serwery krawędzi.
Kody stanu Buforowalnej zestawu | Definiuje zestaw hello kodów stanu, które mogą skutkować zawartości w pamięci podręcznej.
Stałe dostarczanie zawartości w przypadku błędu | Określa, czy ważność zawartości w pamięci podręcznej zostanie dostarczona, gdy wystąpi błąd podczas ponownego sprawdzania poprawności pamięci podręcznej lub zleconą hello podczas pobierania zawartości z serwera źródłowego powitania klienta.
Nieaktualne podczas Revalidate | Zwiększa wydajność, zezwalając na naszych serwerach krawędzi tooserve nieodświeżeni klienci toohello. strona żądająca podczas ponownego sprawdzania poprawności ma miejsce.
Komentarz | Funkcja komentarz Hello umożliwia toobe Uwaga, dodane w regule.

###<a name="bandwidth-parameters"></a>Parametry przepustowości
**Cel:** Określa, czy przepustowości parametrów (tj. ec_rate i ec_prebuf) będzie aktywny.

Parametry ograniczania przepustowości określają, czy hello szybkość transferu danych dla żądania klienta będzie ograniczona tooa szybkość niestandardowych.

Wartość|wynik
--|--
Enabled (Włączony)|Umożliwia nasze serwery krawędzi toohonor przepustowości żądania.
Disabled (Wyłączony)|Powoduje, że serwery krawędzi tooignore parametry ograniczenia przepustowości. Witaj zażądał zawartość będzie zazwyczaj podawana (tzn. bez ograniczania przepustowości).

**Domyślne zachowanie:** włączone.

###<a name="bandwidth-throttling"></a>Ograniczanie przepustowości
**Cel:** limity hello przepustowości dla odpowiedzi hello udostępniane przez serwery krawędzi.

Zarówno hello następujące opcje musi być zdefiniowany tooproperly Konfigurowanie ograniczania przepustowości.

Opcja|Opis
--|--
KB na sekundę|Ustaw to opcja toohello maksymalnej przepustowości (Kb na sekundę), które mogą być używane toodeliver hello odpowiedzi.
Prebuf sekund|Ustaw opcję tego toohello liczbę sekund oczekiwania nasze serwery krawędzi do ograniczania przepustowości. Celem Hello przepustowości nieograniczony okres ten jest tooprevent Windows media player z występują przestojów lub problemów z powodu ograniczania toobandwidth buforowania.

**Domyślne zachowanie:** wyłączone.

###<a name="bypass-cache"></a>Pomiń pamięć podręczną
**Cel:** Określa, czy hello żądania mogą korzystać z naszych technologię buforowania.

Wartość|wynik
--|--
Enabled (Włączony)|Powoduje, że wszystkie żądania toofall za pośrednictwem serwera pochodzenia toohello, nawet jeśli zawartość hello wcześniej była buforowana na serwerach krawędzi.
Disabled (Wyłączony)|Powoduje, że serwery krawędzi toocache zasobów zgodnie z toohello pamięci podręcznej zasad zdefiniowanych w jego nagłówków odpowiedzi.

**Domyślne zachowanie:**

- **Duże HTTP:** wyłączone

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Traktowanie nagłówka kontroli pamięci podręcznej
**Cel:** kontroluje Generowanie hello nagłówków Cache-Control przez serwer graniczny hello, gdy funkcja maksymalny wiek zewnętrznych jest aktywna.

Witaj najprostszym tooachieve sposób takiej konfiguracji jest hello tooplace zewnętrznych Max-Age hello traktowania nagłówek Cache-Control funkcji i w tej samej instrukcji hello.

Wartość|wynik
--|--
Zastąp|Gwarantuje, że ten hello następujące akcje będą miały miejsce:<br/> -Zastępuje nagłówek Cache-Control generowane przez powitania serwera źródłowego. <br/>-Dodaje nagłówek Cache-Control utworzonego przez hello odpowiedzi toohello funkcji zewnętrznych Max-Age.
Przekazuj|Gwarantuje, że nagłówek Cache-Control utworzonej przez funkcję zewnętrznych Max-Age hello nigdy nie został dodany toohello odpowiedzi. <br/> Jeśli serwer pochodzenia hello generuje nagłówek Cache-Control, przekaże toohello przez użytkownika końcowego. <br/> Jeśli serwer pochodzenia hello nie generuje nagłówek Cache-Control, a następnie ta opcja może toonot nagłówka odpowiedzi hello Przyczyna zawierać nagłówek Cache-Control.
Jeśli brakuje dodać|Jeśli z serwera źródłowego hello nie odebrano nagłówek Cache-Control, ta opcja dodaje nagłówek Cache-Control utworzonej przez funkcję zewnętrznych Max-Age hello. Ta opcja jest przydatna do zapewnienia, że wszystkie zasoby zostaną przypisane nagłówek Cache-Control.
Remove| Tej opcji zapewnia, że nagłówek Cache-Control nie jest dołączony do odpowiedzi nagłówek hello. Jeśli przypisano już nagłówek Cache-Control, następnie go będzie być usunięte z hello nagłówka odpowiedzi.

**Domyślne zachowanie:** zastąpić.

###<a name="cache-key-query-string"></a>Ciąg zapytania klucz pamięci podręcznej
**Cel:** Określa, czy klucz pamięci podręcznej zostaną dołączone lub wykluczone parametrów ciągu zapytania skojarzonego z żądaniem.

Informacje o kluczu:

- Określ co najmniej jeden nazwy parametru ciągu zapytania. Nazwy parametrów powinny być rozdzielane z jednego miejsca.
- Ta funkcja określa, czy zostaną uwzględnione lub wykluczone z klucz pamięci podręcznej hello parametrów ciągu zapytania. Dodatkowe informacje dla każdego z poniższych opcji.

Typ|Opis
--|--
 Obejmują|  Wskazuje, że każdy określony parametr powinien być uwzględniany w klucz pamięci podręcznej hello. Unikatowy klucz pamięci podręcznej zostanie wygenerowany dla każdego żądania, który zawiera unikatową wartość dla parametru ciągu zapytania, zdefiniowane w tej funkcji. 
 Uwzględnij wszystkie  |Wskazuje, że dla każdego żądania zawartości tooan, który zawiera ciąg zapytania unikatowy zostanie utworzona Unikatowy klucz pamięci podręcznej. Ten typ konfiguracji nie jest zwykle zalecane, ponieważ może spowodować tooa niewielki procent trafień w pamięci podręcznej. Zwiększy hello obciążenia na serwerze źródłowym hello, ponieważ jej tooserve więcej żądań. Ta konfiguracja jest duplikatem hello buforowanie znana jako "Unikatowy pamięci podręcznej" na stronie buforowanie ciągu zapytania. 
 Wyklucz | Wskazuje, że hello tylko określony, parametrów, które zostaną wykluczone z klucz pamięci podręcznej hello. Wszystkie pozostałe parametry ciągu zapytania będą uwzględniane w klucz pamięci podręcznej hello. 
 Wyklucz wszystkie  |Wskazuje, że wszystkie parametry ciągu zapytania zostaną wykluczone z klucz pamięci podręcznej hello. Ta konfiguracja jest duplikatem domyślne hello buforowanie, nazywanego "pamięci podręcznej standard" na stronie buforowanie ciągu zapytania. 

power Hello aparatu reguł HTTP umożliwia toocustomize hello sposób, w którym buforowania ciągu kwerendy jest zaimplementowana. Na przykład można określić zapytania ciąg buforowanie tylko wykonanie w określonych lokalizacjach lub typów plików.

Jeśli chcesz ciągu zapytania hello tooduplicate buforowanie znana jako "no-cache" na stronie buforowanie ciągu zapytania, wymagana będzie toocreate regułę, która zawiera warunek dopasowanie symbolu wieloznacznego zapytanie adresu URL i funkcja pomijania pamięci podręcznej. Hello warunku dopasowanie symbolu wieloznacznego zapytania adres URL powinien mieć wartość tooan gwiazdki (*).

#### <a name="sample-scenarios"></a>Przykładowe scenariusze

Poniżej znajduje się przykład użycia dla tej funkcji. Przykładowe żądanie i hello domyślny klucz pamięci podręcznej są podane poniżej.

- **Przykładowe żądanie:** http://wpc.0001.&lt; Domeny&gt;/800001/Origin/folder/asset.htm?sessionid=1234 i język = EN & userid = 01
- **Domyślny klucz pamięci podręcznej:** /800001/Origin/folder/asset.htm

##### <a name="include"></a>Obejmują

Przykładowa konfiguracja:

- **Typ:** obejmują
- **Parametry:** języka

Ten typ konfiguracji powoduje wygenerowanie hello następującego parametru ciągu zapytania pamięci podręcznej klucza:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>Uwzględnij wszystkie

Przykładowa konfiguracja:

- **Typ:** obejmują wszystkie

Ten typ konfiguracji powoduje wygenerowanie hello następującego parametru ciągu zapytania pamięci podręcznej klucza:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>Wyklucz

Przykładowa konfiguracja:

- **Typ:** wykluczenia
- **Parametry:** sessionid userid

Ten typ konfiguracji powoduje wygenerowanie hello następującego parametru ciągu zapytania pamięci podręcznej klucza:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>Wyklucz wszystkie

Przykładowa konfiguracja:

- **Typ:** wykluczyć wszystkie

Ten typ konfiguracji powoduje wygenerowanie hello następującego parametru ciągu zapytania pamięci podręcznej klucza:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Napisz ponownie klucz pamięci podręcznej
**Cel:** ponownego hello klucz pamięci podręcznej skojarzonej z żądaniem.

Klucz pamięci podręcznej jest ścieżką względną hello, identyfikujący zasób do celów hello buforowania. Innymi słowy nasze serwery będą sprawdzać dostępności buforowanej wersji zasobów zgodnie z tooits ścieżki zgodnie z definicją w jej klucz pamięci podręcznej.

Tej funkcji można skonfigurować, definiując zarówno hello następujące opcje:

Opcja|Opis
--|--
Oryginalna ścieżka| Definiowanie typów toohello ścieżki względnej hello żądań, których klucz pamięci podręcznej zostanie ponownie zapisać. Ścieżka względna mogą być definiowane przez wybranie ścieżka do podstawowego źródła, a następnie wzorzec wyrażenia regularnego.
Nowa ścieżka|Zdefiniuj ścieżkę względną hello nowy klucz pamięci podręcznej hello. Ścieżka względna mogą być definiowane przez wybranie ścieżka do podstawowego źródła, a następnie wzorzec wyrażenia regularnego. Ta ścieżka względna można dynamicznie utworzyć przy użyciu hello zmiennych HTTP
**Domyślne zachowanie:** klucz pamięci podręcznej żądania jest określana przez identyfikator URI żądania hello.

###<a name="complete-cache-fill"></a>Zakończenie wypełnienie pamięci podręcznej
**Cel:** Określa, co się dzieje, gdy żądanie powoduje Chybienie pamięci podręcznej częściowe, na serwerze granicznym.

Chybienia pamięci podręcznej częściowe opisuje hello stan pamięci podręcznej dla zasobu, który nie został całkowicie pobrany tooan serwer graniczny. Jeśli zasób jest tylko częściowo buforowane na serwerze granicznym, następnie hello następnego żądania dla tego zasobu zostaną przekazane ponownie toohello serwera źródłowego.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
Chybienia pamięci podręcznej częściowe zazwyczaj występuje po użytkownik porzuca pobieranie lub trwałych żądanych wyłącznie przy użyciu żądania range HTTP. Ta funkcja jest najbardziej przydatny w przypadku dużych zasobów, których użytkownicy nie zwykle pobierze je z toofinish start (np. pliki wideo). W związku z tym ta funkcja jest włączona domyślnie na powitania dużych HTTP platformy. Jest ona wyłączona w innych platform.

Zalecane jest tooleave hello domyślną konfigurację hello dużych HTTP platformy, ponieważ będzie zmniejszyć obciążenie powitania klienta serwera pochodzenia i zwiększyć szybkość hello, w którym klienci pobierania zawartości.

Ze względu na sposób toohello, w których pamięci podręcznej ustawienia są śledzone, ta funkcja nie może być skojarzony z hello następujące warunki dopasowania: Cname krawędzi, literału nagłówka żądania wieloznaczny nagłówek żądania, adres URL zapytania literału i adres URL zapytania z symboli wieloznacznych.

Wartość|wynik
--|--
Enabled (Włączony)|Przywraca hello domyślne zachowanie. Witaj domyślne zachowanie to tooforce hello krawędzi serwera tooinitiate pobieranie w tle trwałego hello z serwera źródłowego hello. Po upływie którego hello zasobów będą znajdować się w lokalnej pamięci podręcznej serwera granicznego hello.
Disabled (Wyłączony)|Serwer graniczny uniemożliwia wykonywanie pobieranie w tle dla hello zasobów. Oznacza to, że to żądanie dalej hello tego zasobu z tego regionu spowoduje, że toorequest serwer krawędzi go z serwera źródłowego powitania klienta.

**Domyślne zachowanie:** włączone.

###<a name="compress-file-types"></a>Kompresuj typów plików
**Cel:** definiuje hello formatów plików, które zostanie skompresowany na powitania serwera.

Format pliku można określić za pomocą jego typ nośnika Internetu (tj., Content-Type). Typ nośnika Internet jest metadanych niezależne od platformy, które umożliwia naszych serwerów tooidentify hello format pliku określonego zasobu. Listę typowych nośnika Internet podano poniżej.

Typ nośnika Internet|Opis
--|--
zwykły tekst|Pliki w formacie zwykłego tekstu
tekst i html| Pliki HTML
tekst/css|Kaskadowe arkusze stylów (CSS)
Application/x-javascript|Javascript
Aplikacja/javascript|Javascript
Informacje o kluczu:

- Oddzielającego każdej z nich z jednego miejsca, aby określić wiele typów nośników Internet. 
- Ta funkcja będzie Kompresuj tylko zasoby, którego rozmiar jest mniejszy niż 1 MB. Większe zasoby nie zostanie skompresowany przez serwery.
- Niektórych typów zawartości, takich jak obrazy, wideo i audio nośnika zasobów (np. JPG, MP3, MP4, itp.), są już kompresowane. Dodatkowe kompresję dla tych typów zasobów nie będzie znacznie zmniejsza rozmiar pliku. W związku z tym zaleca się, że nie należy włączać kompresję dla tych typów zasobów.
- Symbole wieloznaczne, takie jak gwiazdek, nie są obsługiwane.
- Przed dodaniem tej funkcji tooa reguły, upewnij się, że tooset opcję kompresji wyłączone na stronie kompresji hello toowhich platformy, które zostanie zastosowana ta reguła.

###<a name="default-internal-max-age"></a>Max-Age wewnętrzny domyślne
**Cel:** określa hello domyślny maksymalny wiek interwał ponowna Walidacja buforu serwera tooorigin serwer krawędzi. Innymi słowy hello ilość czasu, jaki upłynie przed serwer graniczny sprawdzi, czy buforowanych zasobów zgodny hello zasobów przechowywanych na powitania serwera źródłowego.

Informacje o kluczu:

- Ta akcja ma miejsce tylko dla odpowiedzi z serwera pochodzenia, które nie zostały przypisane oznaczenie maksymalny wiek w nagłówek Cache-Control lub Expires.
- Ta akcja nie zostanie przeprowadzone zasobów, które nie są uważane za buforowalnej.
- Ta akcja nie ma wpływu na revalidations pamięci podręcznej serwera tooedge przeglądarki. Tego rodzaju revalidations są określane przez Cache-Control lub Expires headers wysłanych toohello przeglądarki, które można dostosować za pomocą funkcji Max-Age zewnętrznych.
- wyniki Hello tej akcji nie mają zauważalne wpływ na powitania nagłówki odpowiedzi i zawartości hello zwrócony z serwerów krawędzi dla zawartości, ale może mieć wpływ na powitania ilość ruchu ponowna Walidacja wysłanych z serwera źródłowego tooyour serwerów krawędzi.
- Konfigurowanie tej funkcji przez:
    - Wybieranie hello kod stanu, dla którego można zastosować domyślnego wewnętrzny max wieku.
    - Określanie wartość całkowitą, a następnie wybierając hello jednostki żądany czas (tj., sekund, minuty, godziny itd.). Ta wartość Określa domyślny hello wewnętrzny interwał maksymalny wiek.

- Jednostka czasu hello ustawienie zbyt "Off" zostanie przypisany domyślny wewnętrzny maksymalny wiek interwał 7 dni dla żądań, które nie zostały przypisane oznaczenie maksymalny wiek w ich Cache-Control lub Expires nagłówka.
- Ze względu na sposób toohello, w których pamięci podręcznej ustawienia są śledzone ta funkcja nie może być skojarzony z hello następujące warunki dopasowania: 
    - Krawędzi 
    - CNAME
    - Literał nagłówka żądania
    - Symbol wieloznaczny nagłówka żądania
    - Request — metoda
    - Adres URL zapytania literału
    - Adres URL zapytania z symboli wieloznacznych

**Wartość domyślna:** 7 dni

###<a name="expires-header-treatment"></a>Wygasa traktowania nagłówka
**Cel:** kontroluje Generowanie hello Expires headers przez serwer graniczny, gdy funkcja zewnętrznych Max-Age jest aktywna.

Witaj najprostszym tooachieve sposób takiej konfiguracji jest hello tooplace zewnętrznych Max-Age hello wygasa traktowania nagłówka funkcji i w tej samej instrukcji hello.

Wartość|wynik
--|--
Zastąp|Gwarantuje, że ten hello następujące akcje będą miały miejsce:<br/>-Zastępuje generowane przez serwer pochodzenia hello nagłówek Expires.<br/>-Dodaje nagłówek Expires utworzonego przez hello zewnętrznych Max-Age funkcji toohello odpowiedzi.
Przekazuj|Sprawia, że nagłówek Expires utworzonej przez funkcję zewnętrznych Max-Age hello nigdy nie są dodawane toohello odpowiedzi. <br/> Jeśli serwer pochodzenia hello generuje nagłówek Expires, przekaże toohello przez użytkownika końcowego. <br/>Jeśli serwer pochodzenia hello nie generuje nagłówek Expires, a następnie ta opcja może toonot nagłówka odpowiedzi hello Przyczyna zawierać nagłówek Expires.
Jeśli brakuje dodać| Jeśli nie odebrano nagłówek Expires z serwera źródłowego hello, ta opcja dodaje nagłówek Expires utworzonej przez funkcję zewnętrznych Max-Age hello. Ta opcja jest przydatna do zapewnienia, że wszystkie zasoby zostaną przypisane nagłówek Expires.
Remove| Zapewnia, że nagłówek Expires nie jest dołączony do odpowiedzi nagłówek hello. Jeśli już przypisano nagłówek Expires, następnie go będzie być usunięte z hello nagłówka odpowiedzi.

**Domyślne zachowanie:** zastępowania

###<a name="external-max-age"></a>Max-Age zewnętrznych
**Cel:** hello określa maksymalny wiek interwał ponownego sprawdzania poprawności przeglądarki tooedge serwera pamięci podręcznej. Innymi słowy hello ilość czasu, jaki upłynie przed przeglądarką można sprawdzić nowej wersji zasób z serwer graniczny.

Włączenie tej funkcji spowoduje wygenerowanie pamięci podręcznej-kontrolki: max-wieku i wygasa nagłówków z naszych serwerów krawędzi i wysyłać je toohello HTTP klienta. Domyślnie te nagłówki spowoduje zastąpienie utworzone przez powitania serwera źródłowego. Jednak traktowania nagłówek Cache-Control i funkcje wygasa traktowania nagłówka mogą być używane tooalter to zachowanie.

Informacje o kluczu:

- Ta akcja nie ma wpływu na krawędzi serwera tooorigin serwera pamięci podręcznej revalidations. Tego rodzaju revalidations są określane na podstawie nagłówków pamięci podręcznej-formant/Expires otrzymanego z serwera źródłowego hello i można dostosować za pomocą domyślnych wewnętrznych Max-Age i funkcji Force wewnętrzny Max-Age.
- Tej funkcji można skonfigurować, określając wartość całkowitą i wybierając jednostkę czasu żądaną hello (tj., sekund, minuty, godziny itd.).
- Ustawienie wartości ujemnej tooa funkcji powoduje, że nasze toosend serwerów krawędzi pamięci podręcznej-Control: no-pamięci podręcznej i czas wygaśnięcia ustawioną w hello przeszłości z każdą przeglądarkę toohello odpowiedzi. Mimo że klient HTTP nie będzie buforować odpowiedź hello, to ustawienie nie będzie miało wpływ na nasze serwery krawędzi możliwości toocache hello odpowiedzi z serwera źródłowego hello.
- Jednostka czasu hello ustawienie zbyt "Off" spowoduje wyłączenie tej funkcji. Nagłówki Expires-formant/pamięci podręcznej w pamięci podręcznej z odpowiedzią powitania serwera pochodzenia hello będzie przekazywał toohello przeglądarki.

**Domyślne zachowanie:** wyłączone

###<a name="force-internal-max-age"></a>Wymuszanie wewnętrznych Max-Age.
**Cel:** hello określa maksymalny wiek interwał ponowna Walidacja buforu serwera tooorigin serwer krawędzi. Innymi słowy hello ilość czasu, jaki upłynie przed serwer graniczny można sprawdzić, czy buforowanych zasobów zgodny hello zasobów przechowywanych na powitania serwera źródłowego.

Informacje o kluczu:

- Ta funkcja spowoduje zastąpienie interwału maksymalny wiek powitania zdefiniowanej w Cache-Control lub Expires nagłówki wygenerowane z serwera pochodzenia.
- Ta funkcja nie ma wpływu na revalidations pamięci podręcznej serwera tooedge przeglądarki. Tego rodzaju revalidations są określane przez Cache-Control lub Expires headers wysłanych toohello przeglądarki.
- Ta funkcja nie ma widocznych wpływ na powitania odpowiedzi dostarczonych przez żądający toohello serwer krawędzi. Jednak może mieć wpływ na powitania ilość ruchu ponowna Walidacja wysłanych z serwera pochodzenia toohello serwerów krawędzi.
- Konfigurowanie tej funkcji przez:
    - Wybieranie hello kod stanu, dla których zostaną zastosowane wewnętrzny wieku max.
    - Określanie całkowitą i wybierając hello jednostki żądany czas (tj., sekund, minuty, godziny itd.). Ta wartość Określa interwał maksymalny wiek hello żądania.

- Jednostka czasu hello ustawienie zbyt "Off" powoduje wyłączenie tej funkcji. Wewnętrzny interwał maksymalny wiek nie zostaną przypisane toorequested zasoby. Jeśli oryginalny nagłówek hello nie zawiera instrukcji buforowania, następnie hello zasobów będą buforowane zgodnie z toohello aktywne ustawienie w funkcji domyślne wewnętrzny Max-Age.
- Ze względu na sposób toohello, w których pamięci podręcznej ustawienia są śledzone ta funkcja nie może być skojarzony z hello następujące warunki dopasowania: 
    - Krawędzi 
    - CNAME
    - Literał nagłówka żądania
    - Symbol wieloznaczny nagłówka żądania
    - Request — metoda
    - Adres URL zapytania literału
    - Adres URL zapytania z symboli wieloznacznych

**Domyślne zachowanie:** wyłączone

###<a name="h264-support-http-progressive-download"></a>Obsługa H.264 (pobierania progresywnego HTTP)
**Cel:** Określa typy hello H.264 formaty plików, które mogą być używane toostream zawartości.

Informacje o kluczu:

- Zdefiniuj zestaw dozwolonych rozszerzenia nazw plików H.264 rozdzielonych spacjami w opcji rozszerzenia plików. Opcja rozszerzenia pliku spowoduje zastąpienie hello domyślne zachowanie. Obsługa MP4 i F4V pomocy technicznej przez dołączenie te rozszerzenia nazw plików, ustawiając tę opcję. 
- Upewnij się, że tooinclude okres, podczas określania każde rozszerzenie nazwy pliku (np. plik MP4 .f4v).

**Domyślne zachowanie:** pobierania progresywnego HTTP obsługuje nośników MP4 i F4V domyślnie.

###<a name="honor-no-cache-request"></a>Honoruj nie-cache żądania
**Cel:** Określa, czy klient HTTP żądań pamięci podręcznej nie zostanie przekazany toohello serwera źródłowego.

Żądanie pamięci podręcznej nie występuje podczas hello HTTP, klient wysyła pamięci podręcznej-kontrolki: nie-pamięci podręcznej i/lub Pragma:no-pamięci podręcznej nagłówka w żądaniu hello HTTP.

Wartość|wynik
--|--
Enabled (Włączony)|Umożliwia pamięci podręcznej klienta HTTP nie żąda serwera pochodzenia przekazywane toohello toobe i serwera pochodzenia hello zwróci hello nagłówki odpowiedzi i treści hello przez serwer graniczny hello wstecz toohello HTTP klienta.
Disabled (Wyłączony)|Przywraca hello domyślne zachowanie. Witaj domyślne zachowanie to żądań pamięci podręcznej nie tooprevent przekazywanie toohello serwera źródłowego.

Dla całego ruchu w środowisku produkcyjnym, jest zdecydowanie zalecane tooleave tę funkcję w stanie domyślnym wyłączone. W przeciwnym razie nie będzie można włączyć osłony serwerów pochodzenie od użytkowników końcowych, którzy mogą przypadkowo wyzwalać wiele żądań pamięci podręcznej nie podczas odświeżania strony sieci web lub z hello wiele odtwarzacze multimedialne popularnych, które są ustalone toosend nagłówka buforu nie każde żądanie wideo. Niemniej jednak ta funkcja może być przydatna tooapply toocertain nieprodukcyjnych przemieszczania lub testowanie katalogów, w kolejności tooallow świeże zawartości toobe pobierane na żądanie z serwera źródłowego hello.

stan pamięci podręcznej Hello zgłoszenia żądania jest dozwolone serwera pochodzenia tooan toobe przekazywane powodu funkcji toothis jest TCP_Client_Refresh_Miss. Raport stany pamięci podręcznej, który jest dostępny w moduł raportowania Core hello, informacje statystyczne według stanu pamięci podręcznej. Dzięki temu można tootrack hello liczbę i odsetek żądań, które są przesyłane dalej do serwera pochodzenia tooan powodu toothis funkcji.

**Domyślne zachowanie:** wyłączone.

###<a name="ignore-origin-no-cache"></a>Ignoruj pochodzenia no-cache
**Cel:** Określa, czy naszych CDN zignoruje hello dyrektywy udostępniane przez serwer źródła po:

- Cache-Control: prywatne
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: nie-cache

Informacje o kluczu:

- Tej funkcji można skonfigurować, definiując rozdzieloną spacjami listę kodów stanu, dla których hello powyżej dyrektywy zostaną zignorowane.
- Witaj zestaw kodów nieprawidłowy stan dla tej funkcji są: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 i 505.
- Wyłączyć tę funkcję, ustawiając tooa pustej wartości.
- Ze względu na sposób toohello, w których pamięci podręcznej ustawienia są śledzone ta funkcja nie może być skojarzony z hello następujące warunki dopasowania: 
    - Krawędzi 
    - CNAME
    - Literał nagłówka żądania
    - Symbol wieloznaczny nagłówka żądania
    - Request — metoda
    - Adres URL zapytania literału
    - Adres URL zapytania z symboli wieloznacznych

**Domyślne zachowanie:** domyślne zachowanie to hello toohonor powyżej dyrektywy.

###<a name="ignore-unsatisfiable-ranges"></a>Ignoruj Unsatisfiable zakresów 
**Cel:** określa hello odpowiedzi, która zostanie zwrócona tooclients po żądanie generuje 416 żądany zakres nie niewłaściwego kod stanu.

Domyślnie ten kod stanu jest zwracany podczas hello określone żądania zakresu bajtów nie mogą być spełnione przez serwer graniczny i nie określono pola nagłówka żądania If-Range.

Wartość|wynik
-|-
Enabled (Włączony)|Zapobiega nasze serwery krawędzi z odpowiada tooan żądania nieprawidłowy zakres bajtów z 416 żądany zakres nie niewłaściwego kodem stanu. Zamiast tego serwery dostarczania hello żądanych zasobów i zwrócić 200 OK na powitania klienta.
Disabled (Wyłączony)|Przywraca hello domyślne zachowanie. Witaj domyślne zachowanie to toohonor 416 żądany zakres nie niewłaściwego kod stanu.

**Domyślne zachowanie:** wyłączone.

###<a name="internal-max-stale"></a>Wewnętrzny odświeżona maksymalna
**Cel:** Określa, jak długo ostatnich czas normalne wygaśnięcie hello zasobów pamięci podręcznej mogą być udostępniane przez serwer graniczny, gdy serwer graniczny hello jest hello toorevalidate buforowanych zasobów z serwera źródłowego hello.

Zwykle po upływie czasu maksymalny wiek zasobów, serwer graniczny hello wyśle serwer pochodzenia toohello żądanie ponownego sprawdzania poprawności. Witaj serwera pochodzenia następnie odpowie albo 304 niezmodyfikowane umożliwiają serwer graniczny hello świeże dzierżawy na powitania buforowanych zasobów lub z 200 OK aby zapewnić serwer graniczny hello zaktualizowaną wersję hello zasobów pamięci podręcznej.

Jeśli serwer graniczny hello jest tooestablish połączenia z serwerem pochodzenia hello podczas próby ponowna Walidacja, ta funkcja wewnętrzny odświeżona Max Określa, czy i jak długo hello serwer graniczny mogą nadal tooserve hello teraz przestarzały zasobów.

Należy pamiętać, że dany interwał czasu zaczyna się po wygaśnięciu wieku max hello zasobów, nie sytuacji hello ponownego sprawdzania poprawności nie powiodło się. W związku z tym hello maksymalny okres, w którym mogą być przekazywane zasób bez ponownego sprawdzania poprawności pomyślne to hello czas określone przez kombinację hello maksymalny wiek plus odświeżona max. Na przykład jeśli zasób był buforowany 9:00, maksymalny wiek 30 minut i max przestarzały 15 minut, a następnie spróbuj nie powiodło się ponownego sprawdzania poprawności na 9:44 dadzą w wyniku przez użytkownika końcowego odbierania hello starych buforowanych zasobów, podczas ponownego sprawdzania poprawności nie powiodło się próba 9:46 dadzą w wyniku użytkownik końcowy Hello odbieranie 504 Limit czasu bramy.

Wartości skonfigurowane dla tej funkcji są zastępowane przez pamięć podręczną-kontrolki: musi — Sprawdź poprawność ponownie, lub buforować —: serwer proxy kontroli-ponownie sprawdź poprawność nagłówki otrzymanego z serwera źródłowego hello. Jeśli jest jedną z tych nagłówków otrzymany z serwera pochodzenia hello, gdy zasób jest początkowo buforowany, następnie hello serwer graniczny nie będzie obsługiwać starych zasobów pamięci podręcznej. W takim przypadku gdy serwer graniczny hello toorevalidate z pochodzenia hello Jeśli wygasł interwał maksymalny wiek hello zasobów, to serwer graniczny hello zwróci 504 Limit czasu bramy.

Informacje o kluczu:

- Konfigurowanie tej funkcji przez:
    - Wybieranie hello kod stanu, dla których zostaną zastosowane odświeżona max.
    - Określanie wartość całkowitą, a następnie wybierając hello jednostki żądany czas (tj., sekund, minuty, godziny itd.). Ta wartość określa hello wewnętrzny max odświeżona które zostaną zastosowane.

- Jednostka czasu hello ustawienie zbyt "Off" spowoduje wyłączenie tej funkcji. Zasobów pamięci podręcznej nie zostanie obsłużona poza jego czas wygaśnięcia normalnego.
- Ze względu na sposób toohello, w których pamięci podręcznej ustawienia są śledzone ta funkcja nie może być skojarzony z hello następujące warunki dopasowania: 
    - Krawędzi 
    - CNAME
    - Literał nagłówka żądania
    - Symbol wieloznaczny nagłówka żądania
    - Request — metoda
    - Adres URL zapytania literału
    - Adres URL zapytania z symboli wieloznacznych

**Domyślne zachowanie:** 2 minuty

###<a name="partial-cache-sharing"></a>Udostępnianie częściowe pamięci podręcznej
**Cel:** Określa, czy żądanie może wygenerować częściowo buforowaną zawartość.

Częściowe pamięci podręcznej będzie wtedy toofulfill używane nowe żądania dla tej zawartości do momentu hello żądanie zawartości jest w pełni pamięci podręcznej.

Wartość|wynik
-|-
Enabled (Włączony)|Żądania mogą generować częściowo buforowaną zawartość.
Disabled (Wyłączony)|Żądania można generować tylko pełni buforowane wersji hello żądanej zawartości.

**Domyślne zachowanie:** wyłączone.

###<a name="prevalidate-cached-content"></a>Prevalidate zawartości w pamięci podręcznej
**Cel:** Określa, czy przed wygaśnięciem wartość TTL będzie kwalifikuje się do wcześniejszego ponowna Walidacja zawartości w pamięci podręcznej.

Zdefiniuj okres hello toohello przed wygaśnięciem hello żądany czas wygaśnięcia zawartości, w którym będzie kwalifikuje się do wcześniejszego ponownego sprawdzania poprawności.

Informacje o kluczu:

- Wybór "Off" jako jednostka czasu hello wymaga ponownego sprawdzania poprawności tootake miejsce, po upływie TTL hello w pamięci podręcznej zawartości. Nie należy określać czas i zostaną zignorowane.

**Domyślne zachowanie:** Off. Ponowna Walidacja może mieć miejsce jedynie po hello wygasł czas wygaśnięcia zawartości pamięci podręcznej.

###<a name="refresh-zero-byte-cache-files"></a>Odśwież Zero bajtów pamięci podręcznej plików
**Cel:** określa sposób obsługi żądań klienta HTTP dla trwałego 0 bajtów pamięci podręcznej przez serwery krawędzi.

Prawidłowe wartości to:

Wartość|wynik
--|--
Enabled (Włączony)|Powoduje, że nasze krawędzi serwera pobierania toore hello zasobów z serwera źródłowego hello.
Disabled (Wyłączony)|Przywraca hello domyślne zachowanie. Witaj domyślne zachowanie to tooserve się zasoby prawidłowy pamięci podręcznej na żądanie.
Ta funkcja nie jest wymagany do buforowania poprawne i dostarczania zawartości, ale może służyć jako obejście tego problemu. Na przykład dynamiczne generatory zawartości na serwerach pochodzenia przypadkowo może spowodować 0 bajtów odpowiedzi wysyłane toohello serwery krawędzi. Tych typów odpowiedzi, zazwyczaj są buforowane przez serwery krawędzi. Jeśli wiesz, że odpowiedź 0-bajtowych nigdy nie jest prawidłowa odpowiedź 

takie zawartości następnie tej funkcji uniemożliwia tych typów zasobów obsługiwanej tooyour klientów.

**Domyślne zachowanie:** wyłączone.

###<a name="set-cacheable-status-codes"></a>Kody stanu Buforowalnej zestawu
**Cel:** definiuje zestaw hello kodów stanu, które mogą skutkować zawartości w pamięci podręcznej.

Domyślnie buforowanie jest włączona tylko 200 OK odpowiedzi.

Zdefiniuj zestaw hello potrzeby kodów stanu rozdzielonych spacjami.

Informacje o kluczu:

- Włącz również funkcję Ignoruj pochodzenia No-Cache. Jeśli ta funkcja nie jest włączona, następnie odpowiedzi z systemem innym niż 200 OK może nie można buforować.
- Witaj zestaw kodów nieprawidłowy stan dla tej funkcji są: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 i 505.
- Ta funkcja nie może być używane toodisable buforowanie odpowiedzi, które generują kod 200 OK stanu.

**Domyślne zachowanie:** buforowanie jest włączona tylko w przypadku odpowiedzi generujących kod 200 OK stanu.
###<a name="stale-content-delivery-on-error"></a>Stałe dostarczanie zawartości w przypadku błędu
**Cel:** 

Określa, czy ważność zawartości w pamięci podręcznej zostanie dostarczona, gdy wystąpi błąd podczas ponownego sprawdzania poprawności pamięci podręcznej lub zleconą hello podczas pobierania zawartości z serwera źródłowego powitania klienta.

Wartość|wynik
-|-
Enabled (Włączony)|Zawartość zostanie obsłużona żądający toohello podczas serwer pochodzenia tooan połączenia po wystąpieniu błędu.
Disabled (Wyłączony)|Błąd serwera pochodzenia Hello zostaną przekazane toohello żądającego.

**Domyślne zachowanie:** wyłączone

###<a name="stale-while-revalidate"></a>Nieaktualne podczas Revalidate
**Cel:** zwiększa wydajność, zezwalając na naszych serwerach krawędzi tooserve starych toohello zawartości. strona żądająca podczas ponownego sprawdzania poprawności ma miejsce.

Informacje o kluczu:

- zachowanie Hello tej funkcji zależy zgodnie z toohello wybrana wartość czasu jednostki.
    - **Jednostka czasu:** określ długość czasu, a następnie wybierz czas jednostki (np. sekundy, minuty, godziny itp.) tooallow starych dostarczania zawartości. Ten typ Instalatora umożliwia hello CDN tooextend hello długość czasu, który może zostać zawartości przed wymaganiem weryfikacji zgodnie z toohello następującej formuły:**TTL** + **opcję czas starych podczas Sprawdź poprawność ponownie** 
    - **OFF:** wybierz "Off" ponowna Walidacja toorequire przed żądanie może zostać wyświetlona zawartość.
        - Nie określaj długość czasu, ponieważ nie ma zastosowania i zostaną zignorowane.

**Domyślne zachowanie:** Off. Ponowna Walidacja musi odbywać się przed hello zażądał zawartości mogą być udostępniane.

###<a name="comment"></a>Komentarz
**Cel:** umożliwia toobe Uwaga, dodane w regule.

Jedno użycie tej funkcji jest tooprovide dodatkowe informacje na temat hello ogólnego przeznaczenia, reguły lub dlaczego zgodne z określonego warunku lub funkcja została dodana reguła toohello.

Informacje o kluczu:

- Można określić maksymalnie 150 znaków.
- Upewnij się, że tooonly korzystać ze znaków alfanumerycznych.
- Ta funkcja nie ma wpływu na zachowanie hello hello reguły. Tylko ten tooprovide obszaru, w którym należy podać informacje do przyszłego wykorzystania lub które mogą pomóc podczas rozwiązywania problemów reguły hello.
 
## <a name="headers"></a>Nagłówki

Te funkcje są zaprojektowane tooadd, modyfikowanie lub usuwanie nagłówków z hello żądania lub odpowiedzi.

Nazwa | Przeznaczenie
-----|--------
Nagłówek odpowiedzi wieku | Określa, czy nagłówek odpowiedzi wieku mają być uwzględnieni w odpowiedzi hello wysłanych toohello żądający.
Debugowanie nagłówki odpowiedzi pamięci podręcznej | Określa, czy odpowiedź może obejmować hello nagłówka odpowiedzi we-X-Debug, który zawiera informacje na temat hello zasady pamięci podręcznej dla żądanego zasobu hello.
Modyfikowanie nagłówek żądania klienta | Zastępowanie, dołącza lub usuwa nagłówek z żądania.
Modyfikowanie nagłówka odpowiedzi klienta | Zastępowanie, dołącza lub usuwa nagłówek z odpowiedzi.
Wartość niestandardowego nagłówka adresu IP klienta | Umożliwia hello adres IP klienta hello toobe żądania toohello dodany jako nagłówek żądania niestandardowych.

###<a name="age-response-header"></a>Nagłówek odpowiedzi wieku
**Cel**: Określa, czy nagłówek odpowiedzi wieku zostaną uwzględnione w żądający toohello odpowiedzi wysłanych hello.
Wartość|wynik
--|--
Enabled (Włączony) | Nagłówek odpowiedzi wieku Hello zostaną uwzględnione w odpowiedzi hello wysłanych toohello żądający.
Disabled (Wyłączony) | Nagłówek odpowiedzi wieku Hello zostaną wykluczone z hello odpowiedzi wysłanych toohello żądającego.

**Domyślne zachowanie**: wyłączone.

###<a name="debug-cache-response-headers"></a>Debugowanie nagłówki odpowiedzi pamięci podręcznej
**Cel:** Określa, czy odpowiedź może obejmować nagłówka odpowiedzi we-X-Debug, który zawiera informacje na temat hello zasady pamięci podręcznej dla hello żądanego zasobu.

Debugowanie odpowiedzi pamięci podręcznej, który nagłówki mają być uwzględnieni w odpowiedzi hello, gdy są spełnione oba poniższe hello:

- Witaj debugowania funkcji nagłówki odpowiedzi pamięci podręcznej został włączony na powitania odpowiednie żądania.
- Witaj powyżej żądania definiuje zestaw hello debugowania nagłówki odpowiedzi pamięci podręcznej, które zostaną uwzględnione w odpowiedzi hello.

Debugowanie odpowiedzi pamięci podręcznej nagłówki może wystąpić przy tym powitania po nagłówka i hello żądaną dyrektywy w żądaniu hello:

X-WE Debug: _Directive1_,_Directive2_,_DirectiveN_

**Przykład:**

WE-X-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

Wartość|wynik
-|-
Enabled (Włączony)|Żądania dla strony nagłówki odpowiedzi pamięci podręcznej debugowania będzie zwracać odpowiedzi, który zawiera nagłówek X-WE-Debug.
Disabled (Wyłączony)|Nagłówka X-WE-Debug odpowiedzi zostaną wykluczone z hello odpowiedzi.

**Domyślne zachowanie:** wyłączone.

###<a name="modify-client-response-header"></a>Modyfikowanie nagłówka odpowiedzi klienta
**Cel:** każdego żądania zawiera zestaw [nagłówki żądań]() opisują go. Ta funkcja może być:

- Dołącz lub zastąpienie wartości hello przypisane tooa nagłówek żądania. Jeśli hello określonego nagłówka żądania nie istnieje, następnie ta funkcja zostanie dodane toohello żądania.
- Usuń nagłówek żądania z hello żądania.

Żądania, które są przekazywane do serwera pochodzenia tooan zostaną one zastosowane hello zmiany wprowadzone przez tę funkcję.

W nagłówku żądania można wykonać jedną z hello następujące akcje:

Opcja|Opis|Przykład
-|-|-
Append|Witaj określono wartość zostanie dodana toend hello istniejącą wartość nagłówka żądania.|**Wartość nagłówka (klient) żądania:**wartość1 <br/> **Żądanie wartość nagłówka (aparat reguł HTTP):** wartość2 <br/>**Nowa wartość nagłówka żądania:** Value1Value2
Zastąp|Żądanie hello wartość nagłówka będą toohello zestaw określona wartość.|**Wartość nagłówka (klient) żądania:**wartość1 <br/>**Żądanie wartość nagłówka (aparat reguł HTTP):** wartość2 <br/>**Nowa wartość nagłówka żądania:** wartość2 <br/>
Usuwanie|Usuwa hello określonego nagłówka żądania.|**Wartość nagłówka (klient) żądania:**wartość1 <br/> **Zmodyfikuj konfigurację nagłówek żądania klienta:** w nagłówku żądania hello Delete. <br/>**Wynik:** hello określony nagłówek żądania nie zostaną przekazane toohello serwera źródłowego.

Informacje o kluczu:

- Upewnij się, że hello wartość określoną w opcji Nazwa jest dokładnego dopasowania dla nagłówka żądania żądaną hello.
- Case nie jest brana pod uwagę hello w celu zidentyfikowania nagłówka. Na przykład żadnego hello następujące zmiany nazwy nagłówka Cache-Control mogą być używane tooidentify go:
    - Kontrola pamięci podręcznej
    - CACHE-CONTROL
    - cachE-Control
- Upewnij się, że tooonly Użyj znaki alfanumeryczne, łączniki i podkreślenia, określając nazwę nagłówka.
- Usuwanie nagłówka będą zapobiegać jej są przekazywane do serwera pochodzenia tooan przez serwery krawędzi.
- Witaj następujące nagłówki są zarezerwowane i nie można modyfikować za pomocą tej funkcji:
    - przekazany
    - Host
    - za pomocą
    - Ostrzeżenie
    - x przekazywane do
    - Wszystkie nazwy nagłówka rozpoczynających się od "x WE" są zastrzeżone.

###<a name="modify-client-response-header"></a>Modyfikowanie nagłówka odpowiedzi klienta
Każda odpowiedź zawiera zbiór [nagłówki odpowiedzi]() opisują go. Ta funkcja może być:

- Dołącz lub zastąpienie wartości hello przypisane tooa nagłówka odpowiedzi. Jeśli hello określonego nagłówka żądania nie istnieje, następnie ta funkcja zostanie dodane toohello odpowiedzi.
- Usuń nagłówek odpowiedzi z hello odpowiedzi.

Domyślnie wartości nagłówka odpowiedzi są definiowane przez serwer pochodzenia i serwery krawędzi.

Nagłówka odpowiedzi można wykonać jedną z hello następujące akcje:

Opcja|Opis|Przykład
-|-|-
Append|Witaj określono wartość zostanie dodana toend hello istniejącą wartość nagłówka żądania.|**Wartość nagłówka odpowiedzi (klient):**wartość1 <br/> **Wartość nagłówka odpowiedzi (aparat reguł HTTP):** wartość2 <br/>**Nowa wartość nagłówka odpowiedzi:** Value1Value2
Zastąp|Żądanie hello wartość nagłówka będą toohello zestaw określona wartość.|**Wartość nagłówka odpowiedzi (klient):**wartość1 <br/>**Wartość nagłówka odpowiedzi (aparat reguł HTTP):** wartość2 <br/>**Nowa wartość nagłówka odpowiedzi:** wartość2 <br/>
Usuwanie|Usuwa hello określonego nagłówka żądania.|**Wartość nagłówka (klient) żądania:** wartość1 <br/> **Zmodyfikuj konfigurację nagłówka żądania klienta:** zagrożona nagłówka odpowiedzi hello Delete. <br/>**Wynik:** hello określony nagłówek odpowiedzi nie zostaną przekazane toohello żądającego.

Informacje o kluczu:

- Upewnij się, że hello wartość określoną w opcji Nazwa jest dokładnego dopasowania dla nagłówka odpowiedzi żądaną hello. 
- Case nie jest brana pod uwagę hello w celu zidentyfikowania nagłówka. Na przykład żadnego hello następujące zmiany nazwy nagłówka Cache-Control mogą być używane tooidentify go:
    - Kontrola pamięci podręcznej
    - CACHE-CONTROL
    - cachE-Control
- Usuwanie nagłówka będą zapobiegać jej przesyłane dalej toohello żądającego.
- Witaj następujące nagłówki są zarezerwowane i nie można modyfikować za pomocą tej funkcji:
    - Zaakceptuj kodowania
    - okres ważności
    - połączenie
    - kodowanie zawartości
    - Długość zawartości
    - zakres zawartości
    - Data
    - serwer
    - przyczepy
    - Transfer-encoding
    - Uaktualnienie
    - różnią się
    - za pomocą
    - Ostrzeżenie
    - Wszystkie nazwy nagłówka rozpoczynających się od "x WE" są zastrzeżone.

###<a name="set-client-ip-custom-header"></a>Wartość niestandardowego nagłówka adresu IP klienta
**Cel:** dodaje niestandardowy nagłówek, który identyfikuje klienta hello przez żądanie toohello adresów IP.

Opcja nazwy nagłówka definiuje nazwę hello nagłówek żądania niestandardowe hello przechowywania adresu IP powitania klienta.

Ta funkcja umożliwia klienta toofind serwera pochodzenia się adresy IP klientów za pośrednictwem nagłówków żądań niestandardowych. Jeśli Żądanie hello jest obsługiwana z pamięci podręcznej, serwer pochodzenia hello nie wyświetli się informacja powitania klienta adresu IP. W związku z tym zaleca się, że można użyć tej funkcji w sieci ADN lub zasobów, które nie będą buforowane.

Upewnij się, że nie pasuje do żadnego z następujących hello tę nazwę określony nagłówek hello:

- Nazwy nagłówków żądań standardowych. Lista nazw standardowy nagłówek znajdują się w [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).
- Nazwy nagłówków zastrzeżone:
    - przekazywane do
    - Host
    - różnią się
    - za pomocą
    - Ostrzeżenie
    - x przekazywane do
    - Wszystkie nazwy nagłówka rozpoczynających się od "x WE" są zastrzeżone.
 
## <a name="logs"></a>Dzienniki

Funkcje te są przechowywane w plikach dziennika pierwotnych danych hello toocustomize zaprojektowane.

Nazwa | Przeznaczenie
-----|--------
Pole niestandardowe dziennika 1 | Określa hello format i hello zawartość, która zostanie przypisana toohello logu niestandardowego pola w nowego pliku dziennika.
Ciąg zapytania dziennika | Określa, czy ciąg zapytania będą przechowywane wraz z adresu URL hello w dziennikach dostępu.

###<a name="custom-log-field-1"></a>Pole niestandardowe dziennika 1
**Cel:** określa hello format i hello zawartość, która zostanie przypisana toohello logu niestandardowego pola w nowego pliku dziennika.

głównym celem Hello za to pole niestandardowe jest tooallow toodetermine żądań i odpowiedzi nagłówka wartości, które będą przechowywane w plikach dziennika.

Domyślnie pole dziennik niestandardowy hello jest nazywany "x-ec_custom-1." Jednak można dostosować nazwę hello to pole z [strony pierwotnych ustawień dziennika]().

formatowanie, że należy używać nagłówki żądań i odpowiedzi toospecify Hello jest zdefiniowana poniżej.

Header — typ|Format|Przykłady
-|-|-
Nagłówek żądania|%{[RequestHeader]()}[i]() | % {Zaakceptować kodowania} i <br/> {Odnośnik} i <br/> % {Autoryzacji} i
Nagłówek odpowiedzi|%{[ResponseHeader]()}[o]()| O % {wieku} <br/> O % {content-Type} <br/> O % {cookie}

Informacje o kluczu:

- Pola niestandardowe dziennika może zawierać dowolną kombinację pola nagłówka i zwykły tekst.
- Prawidłowe znaki dla tego pola obejmują następujące hello: alfanumeryczne (tj. 0-9, a-z, a A-Z), łączniki, dwukropki średnikami, apostrofów, przecinkami, kropki, podkreślenia, znaku równości, nawiasy, nawiasy i spacje. Witaj symbol procentu i nawiasów klamrowych jest dozwolony tylko w przypadku używane toospecify pola nagłówka.
- Hello pisowni dla każdego pola określony nagłówek musi być zgodna nazwa nagłówka hello żądaną żądanie/odpowiedź.
- Jeśli chcesz toospecify wiele nagłówków, to jest zalecane używanie tooindicate separatora każdy nagłówek. Na przykład można użyć skrótu każdy nagłówek. Poniżej znajduje się przykład składni.
    - AE: % {zaakceptować kodowania} i odpowiedź: % {autoryzacji} i IERZ: % {Content-Type} o 

**Wartość domyślna:** -

###<a name="log-query-string"></a>Ciąg zapytania dziennika
**Cel:** Określa, czy ciąg zapytania będą przechowywane wraz z adresu URL hello w dziennikach dostępu.

Wartość|wynik
-|-
Enabled (Włączony)|Umożliwia hello magazynu ciągów zapytań, podczas rejestrowania w dzienniku dostępu do adresów URL. Jeśli adres URL zawiera ciąg zapytania, następnie ta opcja nie będzie miało wpływu.
Disabled (Wyłączony)|Przywraca hello domyślne zachowanie. zachowanie domyślne Hello jest tooignore ciągi zapytań podczas rejestrowania w dzienniku dostępu do adresów URL.

**Domyślne zachowanie:** wyłączone.

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>Origin

Te funkcje są zaprojektowane toocontrol jak hello CDN komunikuje się z serwera pochodzenia.

Nazwa | Przeznaczenie
-----|--------
Maksymalna liczba żądań Keep-Alive | Definiuje hello maksymalną liczbę żądań Keep-Alive połączenia przed jego zamknięciem.
Serwer proxy specjalnych nagłówków | Definiuje zestaw hello nagłówków żądania specyficzne dla usługi CDN, które zostaną przekazane z serwera pochodzenia tooan serwer krawędzi.


###<a name="maximum-keep-alive-requests"></a>Maksymalna liczba żądań Keep-Alive
**Cel:** definiuje hello maksymalną liczbę żądań Keep-Alive połączenia przed jego zamknięciem.

Ustawienie hello maksymalną liczbę żądań tooa niskiej wartości jest zalecane i może spowodować obniżenie wydajności.

Informacje o kluczu:

- Tę wartość można określić jako liczbą całkowitą.
- Nie dołączaj kropki i przecinki w hello określona wartość.

**Wartość domyślna:** 10000 żądań

###<a name="proxy-special-headers"></a>Serwer proxy specjalnych nagłówków
**Cel:** definiuje zestaw hello [nagłówki żądania specyficzne dla usługi CDN]() zostaną natychmiast przekazane z serwera pochodzenia tooan serwer krawędzi.

Informacje o kluczu:

- Każdy nagłówek żądania specyficzne dla usługi CDN zdefiniowany w tej funkcji zostanie przekazany tooan serwera źródłowego.
- Nagłówek żądania specyficzne dla usługi CDN uniemożliwić są przekazywane serwera pochodzenia tooan przez usunięcie go z tej listy.

**Domyślne zachowanie:** wszystkie [nagłówki żądania specyficzne dla usługi CDN]() zostaną przekazane toohello serwera źródłowego.

## <a name="specialty"></a>Specjalne

Funkcje te zapewniają zaawansowane funkcje, które mają być używane tylko przez użytkowników zaawansowanych.

Nazwa | Przeznaczenie
-----|--------
Metody HTTP buforowalnej | Określa zbiór hello dodatkowe metody HTTP, które mogą być buforowane w naszej sieci.
Rozmiar treści żądania buforowalnej | Określa próg hello do określenia, czy odpowiedź POST mogą być buforowane.

###<a name="cacheable-http-methods"></a>Metody HTTP buforowalnej
**Cel:** określa zestaw hello dodatkowe metody HTTP, które mogą być buforowane w naszej sieci.

Informacje o kluczu:

- Ta funkcja przyjęto założenie, że zawsze mają być buforowane odpowiedzi GET. W związku z tym nie powinny być dołączone hello metodę GET HTTP, ustawiając tę funkcję.
- Ta funkcja obsługuje tylko hello Metoda POST HTTP. Włącz buforowanie odpowiedzi POST przez ustawienie dla tej funkcji: POST 
- Domyślnie tylko żądania, których treść jest mniejszy niż 14 Kb będą buforowane. Buforowalnej funkcja rozmiar treści żądania umożliwia ustawienie rozmiaru treści żądania maksymalną hello.

**Domyślne zachowanie:** tylko GET odpowiedzi będą buforowane.

###<a name="cacheable-request-body-size"></a>Rozmiar treści żądania buforowalnej

**Cel:** definiuje hello próg do określenia, czy odpowiedź POST mogą być buforowane.

Wartość progu jest określana przez określania rozmiaru treści żądania maksymalna. Żądań zawierających większą treści żądania nie będą buforowane.

Informacje o kluczu:

- Ta funkcja ma zastosowanie tylko w przypadku, gdy odpowiedzi POST kwalifikują się do buforowania. Użyj hello Buforowalnej funkcji metod HTTP, aby włączyć buforowanie żądania POST.
- Treść żądania Hello jest brana pod uwagę dla:
    - wartości x--www-form-urlencoded
    - Zapewnienie Unikatowy klucz pamięci podręcznej
- Definiowanie dużego żądania maksymalny rozmiar treści może mieć wpływ na wydajność dostarczania danych.
    - **Zalecana wartość:** 14 Kb
    - **Wartość minimalna:** 1 Kb

**Domyślne zachowanie:** 14 Kb
 
## <a name="url"></a>ADRES URL

Te funkcje umożliwiają toobe żądania przekierowany lub ulegną tooa inny adres URL.

Nazwa | Przeznaczenie
-----|--------
Wykonaj przekierowania | Określa, czy żądanie nie może być hostname przekierowanego toohello zdefiniowane w nagłówku lokalizacji hello zwróconych przez serwer pochodzenia klienta.
Adres URL przekierowania | Przekierowuje żądania za pośrednictwem hello nagłówek lokalizacji.
Ponowne zapisywanie adresów URL  | Ponownie zapisuje hello adresu URL żądania.

###<a name="follow-redirects"></a>Wykonaj przekierowania
**Cel:** Określa, czy żądanie nie może być hostname przekierowanego toohello zdefiniowane w nagłówku lokalizacji zwróconych przez serwer pochodzenia klienta.

Informacje o kluczu:

- Żądania mogą być tylko przekierowanego tooedge rekordów CNAME, które odpowiadają toohello tej samej platformy.

Wartość|wynik
-|-
Enabled (Włączony)|Można przekierować żądania.
Disabled (Wyłączony)|Nie będzie można przekierować żądania.

**Domyślne zachowanie:** wyłączone.
###<a name="url-redirect"></a>Adres URL przekierowania
**Cel:** przekierowuje żądania za pośrednictwem nagłówek lokalizacji.

Witaj konfiguracji tej funkcji wymaga ustawienia hello następujące opcje:

Opcja|Opis
-|-
Kod|Wybierz kod odpowiedzi hello zwracana toohello żądającego.
Wzorzec & źródła| Te ustawienia definiują wzorzec identyfikatora URI żądania, który identyfikuje typ hello żądań, które mogą zostać przekierowane. Nastąpi przekierowanie tylko żądania, którego adres URL spełnia zarówno hello następujące kryteria: <br/> <br/> **Źródło:** (lub punktu dostępu do zawartości) wybierz ścieżkę względną, którą identyfikuje serwer pochodzenia. Jest to sekcja "/XXXX/" hello i nazwa punktu końcowego. <br/> **Źródło (wzorzec):** wzorca, który identyfikuje żądania za pomocą ścieżki względnej musi być zdefiniowany. Ten wzorzec wyrażenia regularnego musi definiować ścieżką, która rozpoczyna się bezpośrednio po hello poprzednio zaznaczony punkt dostępu do zawartości (zobacz powyżej). <br/> -Upewnij się, że kryteria hello żądanie identyfikatora URI (np. źródła & wzorzec) zdefiniowanych powyżej nie koliduje to z warunkom dopasowania zdefiniowane dla tej funkcji. <br/> — Upewnić się, że toospecify wzorca. Przy użyciu pustej wartości jako wzorzec hello tylko będzie pasował do folderu głównego toohello żądań hello pochodzenia wybranego serwera (np. http://cdn.mydomain.com/).
Element docelowy| Zdefiniuj adres URL hello hello toowhich powyżej żądania nastąpi przekierowanie. <br/> Dynamicznie utworzyć przy użyciu tego adresu URL: <br/> -Wzorzec wyrażenia regularnego <br/>-Zmienne HTTP <br/> Zastąp wartości hello przechwytywane we wzorcu źródła hello do wzorca docelowego hello przy użyciu $ _n_  gdzie  _n_  identyfikuje wartość według kolejności hello, w którym została przechwycona. Na przykład $1 reprezentuje pierwszą wartość hello przechwycone we wzorcu źródła hello, podczas gdy hello druga wartość reprezentuje $2. <br/> 
Jest zdecydowanie zalecane toouse bezwzględnego adresu URL. Użycie Hello względny adres URL może przekierować adresy URL CDN tooan nieprawidłową ścieżkę.

**Przykładowy scenariusz**

W tym przykładzie przedstawiono sposób tooredirect krawędzi URL CNAME, który jest rozpoznawany jako toothis bazowy adres URL usługi CDN: http://marketing.azureedge.net/brochures

Kwalifikowanie żądań, zostanie przekierowany toothis krawędzi podstawowy adres URL CNAME: http://cdn.mydomain.com/resources

Ten adres URL przekierowania można osiągnąć za pomocą hello następującej konfiguracji:![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**Kwestie kluczowe:**

- Funkcja Przekierowywanie adresu URL Hello definiuje hello adresów URL, które zostanie przekierowany żądań. W rezultacie dopasowanie dodatkowe warunki nie są wymagane. Mimo że warunek dopasowania hello został zdefiniowany jako "Always", tylko żądania tego punktu toohello "broszury" nastąpi przekierowanie folderu na powitania "marketing" pochodzenia klienta. 
- Wszystkie żądania pasujące będzie krawędzi toohello przekierowany adres URL CNAME zdefiniowany w opcji docelowej. 
    - Przykładowy scenariusz #1: 
        - Przykładowe żądanie (adres URL usługi CDN): http://marketing.azureedge.net/brochures/widgets.pdf 
        - Adres URL żądania (po przekierowania): http://cdn.mydomain.com/resources/widgets.pdf  
    - Przykładowy scenariusz #2: 
        - Przykładowe żądanie (krawędzi CNAME adres URL): http://marketing.mydomain.com/brochures/widgets.pdf 
        - Adres URL żądania (po przekierowania): http://cdn.mydomain.com/resources/widgets.pdf przykładowy scenariusz
    - Przykładowy scenariusz #3: 
        - Przykładowe żądanie (krawędzi CNAME adres URL): http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - Adres URL żądania (po przekierowania): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- Zmienna żądania schematu (% {schemat}) Hello został wykorzystywana w opcji docelowej. Dzięki temu to Żądanie hello systemu pozostaje niezmieniona po przekierowaniu.
- segmenty adresu URL Hello przechwyconych z żądania hello jest dołączany toohello nowego adresu URL za pośrednictwem "$1."
 
###<a name="url-rewrite"></a>Ponowne zapisywanie adresów URL
**Cel:** ponownie zapisuje hello adresu URL żądania.

Informacje o kluczu:

- Witaj konfiguracji tej funkcji wymaga ustawienia hello następujące opcje:

Opcja|Opis
-|-
 Wzorzec & źródła | Te ustawienia definiują wzorzec identyfikatora URI żądania, który identyfikuje typ hello żądań, które mogą być napisany od nowa. Zostanie ponownego napisania tylko żądania, którego adres URL spełnia zarówno hello następujące kryteria: <br/>     - **Źródło (lub punktu dostępu do zawartości):** wybierz ścieżkę względną, którą identyfikuje serwer pochodzenia. Jest to sekcja "/XXXX/" hello i nazwa punktu końcowego. <br/> - **Źródło (wzorzec):** wzorca, który identyfikuje żądania za pomocą ścieżki względnej musi być zdefiniowany. Ten wzorzec wyrażenia regularnego musi definiować ścieżką, która rozpoczyna się bezpośrednio po hello poprzednio zaznaczony punkt dostępu do zawartości (zobacz powyżej). <br/> Upewnij się, że hello żądanie identyfikatora URI kryteria (np. źródła & wzorzec) zdefiniowanych powyżej nie koliduje to z hello dopasowania warunki zdefiniowane dla tej funkcji. Upewnij się, że toospecify wzorca. Przy użyciu pustej wartości jako wzorzec hello tylko będzie pasował do folderu głównego toohello żądań hello pochodzenia wybranego serwera (np. http://cdn.mydomain.com/). 
 Element docelowy  |Zdefiniuj względny adres URL hello hello toowhich powyżej żądania będą ulegną przez: <br/>    1. Wybieranie punktu dostępu do zawartości, który identyfikuje serwer pochodzenia. <br/>    2. Definiowanie za pomocą ścieżki względnej: <br/>        -Wzorzec wyrażenia regularnego <br/>        -Zmienne HTTP <br/> <br/> Zastąp wartości hello przechwytywane we wzorcu źródła hello do wzorca docelowego hello przy użyciu $ _n_  gdzie  _n_  identyfikuje wartość według kolejności hello, w którym została przechwycona. Na przykład $1 reprezentuje pierwszą wartość hello przechwycone we wzorcu źródła hello, podczas gdy hello druga wartość reprezentuje $2. 
 Ta funkcja umożliwia nasze serwery krawędzi toorewrite hello URL bez wykonywania tradycyjnych przekierowania. Oznacza to, że tej osoby żądającej hello otrzymają hello odpowiedzi tego samego kodu tak, jakby zażąda hello ulegną adresu URL.

**Przykładowy scenariusz 1**

W tym przykładzie przedstawiono sposób tooredirect krawędzi URL CNAME, który jest rozpoznawany jako toothis bazowy adres URL usługi CDN: http://marketing.azureedge.net/brochures/

Kwalifikowanie żądań, zostanie przekierowany toothis krawędzi podstawowy adres URL CNAME: http://MyOrigin.azureedge.net/resources/

Ten adres URL przekierowania można osiągnąć za pomocą hello następującej konfiguracji:![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**Przykładowy scenariusz 2**

W tym przykładzie przedstawiono sposób tooredirect krawędzi CNAME URL z wielkich toolowercase za pomocą wyrażeń regularnych.

Ten adres URL przekierowania można osiągnąć za pomocą hello następującej konfiguracji:![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**Kwestie kluczowe:**

- Funkcja ponowne zapisywanie adresów URL Hello definiuje hello żądania adresów URL, które będą napisany od nowa. W rezultacie dopasowanie dodatkowe warunki nie są wymagane. Mimo że warunek dopasowania hello został zdefiniowany jako "Always", tylko żądania tego punktu toohello "broszury" folderu na powitania "marketing" pochodzenia klienta zostanie ponownie zapisać.

- segmenty adresu URL Hello przechwyconych z żądania hello jest dołączany toohello nowego adresu URL za pośrednictwem "$1."



###<a name="compatibility"></a>Zgodność

Ta funkcja obejmuje spełniających kryteria, które muszą zostać spełnione, aby można było stosowane tooa żądania. W kolejności tooprevent ustawienie powodujące konflikt kryteriów dopasowania, ta funkcja jest niezgodny z hello następujące warunki dopasowania:

- JAKO liczba
- Źródła usługi CDN
- Adres IP klienta
- Pochodzenie klienta
- Schemat żądania
- Adres URL ścieżki katalogu
- Rozszerzenie ścieżki adresu URL
- Nazwa pliku ścieżki adresu URL
- Literał ścieżki adresu URL
- Wyrażenie regularne ścieżki adresu URL
- Symbol wieloznaczny ścieżki adresu URL
- Adres URL zapytania literału
- Adres URL parametru zapytania
- Adres URL zapytania Regex
- Adres URL zapytania z symboli wieloznacznych


## <a name="next-steps"></a>Następne kroki
* [Odwołanie do aparatu reguł](cdn-rules-engine-reference.md)
* [Wyrażenia warunkowe aparatu reguł](cdn-rules-engine-reference-conditional-expressions.md)
* [Warunki uzgadniania aparatu reguł](cdn-rules-engine-reference-match-conditions.md)
* [Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello](cdn-rules-engine.md)
* [Omówienie usługi Azure CDN](cdn-overview.md)
