---
title: "Integracja aaaDirectory uwierzytelnianie wieloskładnikowe Azure i usługi Active Directory"
description: "Jest to hello Azure Multi-Factor authentication strona, która w tym artykule opisano, jak toointegrate hello Azure aplikacji serwer Multi-Factor Authentication z usługą Active Directory, więc mogą wykonywać synchronizację katalogów hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Integracja katalogu między serwerem Azure MFA i usługą Active Directory
Użyj sekcji Integracja katalogu hello hello toointegrate serwera usługi Azure MFA z usługą Active Directory lub innym katalogu LDAP. Można skonfigurować atrybuty toomatch hello katalogu schematu i Konfigurowanie synchronizacji użytkowników.

## <a name="settings"></a>Ustawienia
Domyślnie hello Azure Multi-Factor Authentication (MFA) serwer jest skonfigurowany tooimport lub synchronizowania użytkowników z usługi Active Directory.  Karta integracji katalogów Hello umożliwia możesz toooverride hello domyślne zachowanie i toobind tooa innym katalogiem LDAP, katalogiem ADAM lub określonym kontrolerem domeny usługi Active Directory.  Udostępnia również na użytek hello tooproxy uwierzytelniania LDAP LDAP lub wiązania LDAP jako celu serwera RADIUS, wstępnego uwierzytelniania dla uwierzytelniania usług IIS lub podstawowego uwierzytelniania dla aplikacji Portal użytkowników.  Witaj w poniższej tabeli opisano hello poszczególnych ustawień.

![Ustawienia](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| Funkcja | Opis |
| --- | --- |
| Użyj usługi Active Directory |Wybierz toouse opcję Użyj usługi Active Directory hello usługi Active Directory w celu importowania i synchronizowania.  To jest ustawienie domyślne hello. <br>Uwaga: Dla usługi Active Directory toowork integracji poprawnie, Dołącz hello komputera tooa domeny i zaloguj się przy użyciu konta domeny. |
| Uwzględnij domeny zaufane |Sprawdź **Dołącz zaufane domeny** toohave hello agenta próba tooconnect toodomains uważany za zaufany przez hello w bieżącej domenie, innej domeny w lesie hello lub związane z relacją zaufania lasu domen.  Jeśli nie importowanie lub synchronizowanie użytkowników z dowolnego hello zaufanych domen, usuń zaznaczenie pola wyboru hello wyboru tooimprove wydajności.  domyślne Hello jest zaznaczone. |
| Użyj określonej konfiguracji LDAP |Wybierz określony do importowania i synchronizowania hello użyj katalogu LDAP opcja toouse hello LDAP ustawienia. Uwaga: Po wybraniu opcji Użyj katalogu LDAP hello zmiany interfejsu użytkownika odwołań z tooLDAP usługi Active Directory. |
| Przycisk Edytuj |Witaj przycisk Edytuj pozwala hello toomodified ustawienia w bieżącej konfiguracji LDAP. |
| Użyj zapytań dotyczących zakresu atrybutów |Określa, czy należy użyć zapytań dotyczących zakresu atrybutów.  Zapytania dotyczące atrybutów umożliwiają wydajne katalogu wyszukiwanie odpowiednich rekordów w oparciu o hello wpisów w atrybucie innego rekordu.  powitania serwera usługi Azure Multi-Factor Authentication używa zapytań tooefficiently użytkowników kwerendy zakresu atrybutów hello będących członkami grupy zabezpieczeń.   <br>Uwaga: w określonych przypadkach zapytania dotyczące zakresu atrybutów są obsługiwane, nie powinny jednak być używane.  Na przykład w usłudze Active Directory mogą wystąpić problemy z zapytaniami dotyczącymi zakresu atrybutów, jeśli grupa zabezpieczeń zawiera członków z więcej niż jednej domeny. W takim przypadku usuń zaznaczenie pola wyboru hello. |

Witaj w poniższej tabeli opisano ustawienia konfiguracji LDAP hello.

| Funkcja | Opis |
| --- | --- |
| Serwer |Wprowadź nazwę hello hosta lub adres IP hello serwerem katalogu LDAP hello.  Serwer zapasowy można także określić osobno, oddzielając go średnikiem. <br>Uwaga: jeśli typ powiązania to SSL, wymagana jest w pełni kwalifikowana nazwa hosta. |
| Podstawowa nazwa wyróżniająca |Wprowadź nazwę wyróżniającą hello hello obiektu podstawowego katalogu, z którego uruchomić wszystkie zapytania katalogu.  Na przykład: dc=abc,dc=com. |
| Typ powiązania — zapytania |Wybierz hello odpowiedni typ zapytania do użycia podczas wiązania z katalogiem LDAP hello toosearch.  Ten typ jest wykorzystywany do importowania, synchronizacji oraz rozpoznania nazw użytkowników. <br><br>  Anonimowe — jest tworzone anonimowe powiązanie.  Powiązana nazwa wyróżniająca oraz powiązane hasło nie są używane.  Ta działa tylko wtedy, jeśli hello katalog LDAP umożliwia tworzenie wiązań anonimowych, a uprawnienia zezwalają na wyszukiwanie hello hello odpowiednich rekordów i atrybutów.  <br><br> Prosty — bazowa nazwa Wyróżniająca i hasło są przekazywane jako katalog LDAP toohello toobind w postaci zwykłego tekstu.  Jest do celów testowych, tooverify, który hello serwer jest osiągalny i powiązania hello mającego hello odpowiedni dostęp. Po zainstalowaniu odpowiedniego certyfikatu hello, należy użyć protokołu SSL.  <br><br> Protokół SSL — bazowa nazwa Wyróżniająca i hasło są szyfrowane za pomocą katalogu LDAP toohello toobind protokołu SSL.  Zainstalowania lokalnie certyfikatu, który hello zaufania katalogu LDAP.  <br><br> System Windows — wiązanie nazwa wyróżniająca i hasło są używane toosecurely połączenia kontrolera domeny usługi Active Directory tooan lub katalogiem ADAM.  Jeśli nazwa użytkownika wiązania pozostanie puste, toobind używane jest konto hello zalogowanego użytkownika. |
| Typ powiązania — uwierzytelnienia |Wybierz hello odpowiedni typ zapytania do użytku podczas uwierzytelniania wiązania LDAP.  Zobacz opisy typów powiązania hello w sekcji Typ wiązania — zapytania.  Na przykład dzięki temu toobe wiązania anonimowego użyć zapytań podczas uwierzytelniania wiązania LDAP używane toosecure powiązania SSL. |
| Powiązana nazwa wyróżniająca lub powiązana nazwa użytkownika |Wprowadź hello nazwę wyróżniającą rekordu użytkownika hello hello konta toouse podczas wiązania z katalogiem LDAP toohello.<br><br>Nazwa wyróżniająca wiązania Hello jest używana tylko w przypadku, gdy jest typ wiązania proste lub SSL.  <br><br>Wprowadź nazwę użytkownika hello toouse konta systemu Windows hello podczas wiązania z katalogiem LDAP toohello, gdy typ powiązania to Windows.  Jeśli pole pozostanie puste, hello zalogowanego konta użytkownika jest używana toobind. |
| Powiązane hasło |Wprowadź hasło wiązania hello hello bazowa nazwa Wyróżniająca lub nazwa użytkownika jest katalogiem LDAP toohello toobind używane.  hasło hello tooconfigure hello usługi Multi-Factor Authentication Server AdSync, Włącz synchronizację i upewnij się, że usługa hello jest uruchomiona na komputerze lokalnym hello.  hasło Hello jest zapisywany w hello Windows magazynie zapisanych nazw użytkowników i haseł w obszarze hello powitalne konta usługi Multi-Factor Authentication Server AdSync działa jako.  Hello hasła jest także zapisane w obszarze powitalne konta powitania serwera uwierzytelniania wieloskładnikowego interfejs użytkownika działa jako, a w obszarze hello hello konta usługi serwera uwierzytelniania wieloskładnikowego jest uruchomiona jako.  <br><br>Ponieważ hello hasło jest zapisywane tylko w hello lokalnego serwera Windows przechowywane nazwy użytkowników i hasła, powtórz ten krok na każdym serwerze uwierzytelniania wieloskładnikowego, który wymaga hasła toohello dostępu. |
| Limit rozmiaru zapytania |Określ limit rozmiaru hello hello maksymalną liczbę użytkowników, które zwraca wyszukiwanie w katalogu.  Ten limit powinien być zgodny konfiguracji hello na powitania katalogu LDAP.  Dla dużych operacji wyszukiwania, który nie obsługuje stronicowania importowania i synchronizacji próbuje tooretrieve użytkowników w partiach.  Jeśli limit rozmiaru hello określony w tym miejscu jest większy niż limit hello skonfigurowany na powitania katalogu LDAP, niektórzy użytkownicy mogą zostać pominięci. |
| Przycisk Testuj |Kliknij przycisk **testu** serwera LDAP toohello powiązania tootest.  <br><br>Nie ma potrzeby tooselect hello **użyj katalogu LDAP** opcję tootest powiązania. Dzięki temu toobe powiązania hello przetestowane przed użyciem konfiguracji katalogu LDAP hello. |

## <a name="filters"></a>Filtry
Filtry zezwalać tooset kryteria tooqualify rekordów wyszukiwania w katalogu.  Przez ustawienie filtru hello zakres hello obiekty mają toosynchronize.  

![Filtry](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

Usługa Azure Multi-Factor Authentication ma następujące trzy opcje filtru hello:

* **Filtr kontenerów** — Określ kryteria filtrowania hello używane tooqualify rekordów kontenerów podczas wyszukiwania w katalogu.  W przypadku katalogów Active Directory i ADAM często używane są kryteria filtrowania (|(objectClass=organizationalUnit)(objectClass=container)).  W przypadku innych katalogów LDAP należy użyć kryteriów filtrowania, które kwalifikują poszczególne typy obiektów kontenera, w zależności od schematu katalogu hello.  <br>Uwaga: jeśli pole pozostanie puste, domyślnie używane są kryteria filtrowania ((objectClass=organizationalUnit)(objectClass=container)).
* **Filtr grupy zabezpieczeń** — Określ kryteria filtrowania hello używane rekordów grup zabezpieczeń tooqualify podczas wyszukiwania w katalogu.  W przypadku katalogów Active Directory i ADAM często używane są kryteria filtrowania (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)).  W przypadku innych katalogów LDAP należy użyć kryteriów filtrowania, które kwalifikują poszczególne typy obiektów grupy zabezpieczeń, w zależności od schematu katalogu hello.  <br>Uwaga: jeśli pole pozostanie puste, domyślnie używane są kryteria filtrowania (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)).
* **Filtr użytkowników** — Określ kryteria filtrowania hello używane tooqualify rekordów użytkowników podczas wyszukiwania w katalogu.  W przypadku katalogów Active Directory i ADAM często używane są kryteria filtrowania (&(objectClass=user)(objectCategory=person)).  W przypadku innych katalogów LDAP należy użyć (objectClass = inetOrgPerson) lub coś podobnego, w zależności od schematu katalogu hello. <br>Uwaga: jeśli pole pozostanie puste, domyślnie używane są kryteria filtrowania (&(objectCategory=person)(objectClass=user)).

## <a name="attributes"></a>Atrybuty
Atrybuty można w razie potrzeby dostosować pod kątem określonego katalogu.  To pozwala tooadd atrybuty niestandardowe i dostosowywać hello synchronizacji tooonly hello atrybuty, które należy. Użyj nazwy hello hello attricute, zgodnie z definicją w schemacie katalogu hello hello wartość każdego pola atrybutu. Witaj Poniższa tabela zawiera dodatkowe informacje dotyczące każdej funkcji.

Atrybuty można wprowadzać ręcznie i nie są wymagane toomatch atrybutu na liście atrybutów hello.

![Atrybuty](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| Funkcja | Opis |
| --- | --- |
| Unikatowy identyfikator |Wprowadź nazwę atrybutu hello hello atrybutu, która służy jako unikatowy identyfikator hello kontenera, grupy zabezpieczeń i rekordów użytkowników.  W katalogu Active Directory jest to zazwyczaj wartość elementu objectGUID. Inne implementacje katalogu LDAP mogą używać wartości entryUUID lub podobnej.  Witaj domyślna to objectGUID. |
| Typ unikatowego identyfikatora |Wybierz typ hello hello atrybutu unikatowego identyfikatora.  W usłudze Active Directory atrybut objectGUID hello jest typu GUID. Inne implementacje katalogu LDAP mogą używać typu tablicy bajtowej znaków ASCII lub ciągu.  domyślne Hello jest identyfikatorem GUID. <br><br>Jest ważne tooset tego typu poprawnie od elementów synchronizacji odwołuje się ich identyfikatora unikatowego. Hello Unikatowy identyfikator typu jest używane toodirectly Znajdź hello obiektu w katalogu hello.  Ustawienie tooString tego typu, gdy hello katalog zapisuje wartość hello jako tablica bajtowa znaków ASCII uniemożliwia poprawne działanie synchronizacji. |
| Nazwa wyróżniająca |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera hello nazwę wyróżniającą każdego rekordu.  W katalogu Active Directory jest to zazwyczaj atrybut distinguishedName. Inne implementacje katalogu LDAP mogą używać atrybutu entryDN lub podobnego.  Witaj domyślna to distinguishedName. <br><br>Jeśli nie istnieje atrybut zawierający tylko nazwę wyróżniającą hello, można użyć atrybutu adspath hello.  Witaj "LDAP: / /\<serwera\>/" część ścieżki hello jest automatycznie odłączany, pozostawiając tylko hello nazwy wyróżniającej obiektu hello. |
| Nazwa kontenera |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera nazwę hello w rekordzie kontenera.  Witaj wartość tego atrybutu jest wyświetlany w hello hierarchii kontenera podczas importowania z usługi Active Directory lub dodawania elementów synchronizacji.  Domyślnie Hello jest nazwa. <br><br>Jeśli w różnych kontenerach używane są odmienne atrybuty dla ich nazw, Użyj średników tooseparate wiele atrybutów nazwy kontenera.  pierwszy atrybut nazwy kontenera Hello znalezione w obiekcie kontenera jest używane toodisplay jego nazwy. |
| Nazwa grupy zabezpieczeń |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera nazwę hello w rekordzie grupy zabezpieczeń.  Hello wartość tego atrybutu jest wyświetlany na liście grupy zabezpieczeń hello podczas importowania z usługi Active Directory lub dodawania elementów synchronizacji.  Domyślnie Hello jest nazwa. |
| Nazwa użytkownika |Wprowadź nazwę atrybutu hello hello atrybutu, która zawiera nazwę hello użytkownika w rekordzie użytkownika.  Hello wartość tego atrybutu jest używana jako nazwa użytkownika serwera Multi-Factor Auth hello.  Drugi atrybut mogą być określone jako kopii zapasowej toohello najpierw.  drugi atrybut Hello jest używane, jeśli pierwszy atrybut hello nie zawiera wartości dla hello użytkownika.  Hello domyślne to userPrincipalName i sAMAccountName. |
| Imię |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera hello imię w rekordzie użytkownika.  Witaj domyślna to givenName. |
| Nazwisko |Wprowadź nazwę atrybutu hello atrybutu hello, który zawiera hello nazwisko w rekordzie użytkownika.  Witaj domyślna to sn. |
| Adres e-mail |Wprowadź nazwę atrybutu hello hello atrybut, który zawiera hello adres e-mail w rekordzie użytkownika.  Adres e-mail jest używany toosend powitalnej i aktualizacji użytkownika toohello wiadomości e-mail.  Witaj domyślna to mail. |
| Grupa użytkowników |Wprowadź nazwę atrybutu hello hello atrybut, który zawiera hello grupy użytkowników w rekordzie użytkownika.  Grupa użytkowników może być użytkowników toofilter używanych w agencie hello i w raportach w hello portalu zarządzania serwera uwierzytelniania wieloskładnikowego. |
| Opis |Wprowadź nazwę atrybutu hello hello atrybut, który zawiera opis hello w rekordzie użytkownika.  Opis jest wykorzystywany wyłącznie do celów wyszukiwania.  Witaj domyślna to description. |
| Język połączenia telefonicznego |Wprowadź nazwę atrybutu hello hello atrybut, który zawiera hello krótką nazwę hello toouse języka dla połączeń głosowych hello użytkownika. |
| Język wiadomości SMS |Wprowadź nazwę atrybutu hello hello atrybut, który zawiera hello krótką nazwę hello toouse język wiadomości tekstowych programu SMS dla użytkownika hello. |
| Język aplikacji mobilnej |Wprowadź nazwę atrybutu hello hello atrybut, który zawiera hello krótką nazwę hello toouse język wiadomości tekstowych aplikacji phone hello użytkownika. |
| Język tokenu OATH |Wprowadź nazwę atrybutu hello atrybutu hello, który zawiera hello krótką nazwę hello toouse język wiadomości tekstowych tokenu OATH dla użytkownika hello. |
| Telefon służbowy |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera hello telefonu służbowego w rekordzie użytkownika.  Witaj domyślna to telephoneNumber. |
| Telefon domowy |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera hello numer telefonu domowego w rekordzie użytkownika.  Witaj domyślna to homePhone. |
| Pager |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera hello numer pagera w rekordzie użytkownika.  Witaj domyślna to pager. |
| Telefon komórkowy |Wprowadź nazwę atrybutu hello atrybutu hello, który zawiera hello numer telefonu komórkowego w rekordzie użytkownika.  Witaj domyślna to mobile. |
| Faks |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera hello numer faksu w rekordzie użytkownika.  Witaj domyślna to facsimileTelephoneNumber. |
| Telefon VoIP |Wprowadź nazwę atrybutu hello hello atrybut, który zawiera hello numer telefonu IP w rekordzie użytkownika.  Witaj domyślna to ipPhone. |
| Niestandardowy |Wprowadź nazwę atrybutu hello hello atrybutu, który zawiera niestandardowy numer telefonu w rekordzie użytkownika.  domyślne Hello jest puste. |
| Wewnętrzny |Wprowadź nazwę atrybutu hello hello atrybut, który zawiera hello numer telefonu wewnętrznego w rekordzie użytkownika.  Hello wartości pola rozszerzenie hello jest używany jako hello rozszerzenia toohello głównego numeru telefonu tylko.  domyślne Hello jest puste. <br><br>Jeśli nie określono atrybutu rozszerzenia hello, może być dołączane jako część atrybutu telefonu hello rozszerzenia. W takim przypadku należy poprzedzić rozszerzenie "x" hello tak, aby pobiera poprawnie przeanalizować.  Na przykład 555-123-4567 x890 spowoduje 555-123-4567 jak numer telefonu hello i 890 hello rozszerzenie. |
| Przycisk Przywróć domyślne |Kliknij przycisk **Przywróć domyślne** tooreturn wszystkie atrybuty kopii tootheir wartości domyślnej.  Witaj wartości domyślne powinny działać poprawnie ze hello normalne schematu usługi Active Directory lub ADAM. |

atrybuty tooedit, kliknij przycisk **Edytuj** na powitania kartę atrybuty.  Spowoduje to wyświetlenie okna, w którym można edytować atrybuty hello. Wybierz hello **...**  dalej tooany tooopen atrybut okna, w którym można wybrać toodisplay atrybuty, które.

![Edytuj atrybuty](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>Synchronizacja
Synchronizacja pozwala hello Azure MFA zsynchronizowanie bazy danych użytkowników z hello użytkowników w usłudze Active Directory lub innym katalogu dostępu protokołu LDAP (Lightweight Directory). proces Hello jest podobnych użytkowników tooimporting ręcznie z usługi Active Directory, ale okresowo sonduje użytkownika usługi Active Directory i tooprocess zmiany grupy zabezpieczeń.  Ponadto wyłącza lub usuwa on użytkowników, którzy zostali usunięci z kontenera, grupy zabezpieczeń lub katalogu Active Directory.

Hello usługi Multi-Factor Authentication ADSync to usługa systemu Windows, która wykonuje okresowo sondowanie usługi Active Directory hello.  To nie jest toobe mylić jej z usługi Azure AD Sync lub Azure AD Connect.  Hello usługi Multi-Factor Authentication ADSync, chociaż zbudowane na podstawie podobny kod jest toohello określonego serwera usługi Azure Multi-Factor Authentication.  Jest instalowana w stanie zatrzymania i jest uruchomiona przez hello usługi serwera uwierzytelniania wieloskładnikowego podczas konfigurowania toorun.  Jeśli masz konfiguracji serwera Multi-Factor Auth wielu serwerów hello usługi Multi-Factor Authentication ADSync może działać tylko na jednym serwerze.

Witaj usługi Multi-Factor Authentication ADSync używa hello rozszerzenie serwera DirSync LDAP udostępniane przez Microsoft tooefficiently sondowania zmian.  Ten obiekt wywołujący formantu DirSync musi mieć hello "directory pobieranie zmian" prawo i DS-Replication-Get-Changes rozszerzonej prawo dostępu.  Domyślnie te uprawnienia są przypisane toohello kont administratora oraz systemu lokalnego na kontrolerach domeny.  Domyślnie Hello usługi Multi-Factor Authentication AdSync jest toorun skonfigurowany jako system lokalny.  W związku z tym jest najprostsza usługa hello toorun na kontrolerze domeny.  Jeśli skonfigurujesz tooalways usługi hello wykonać pełną synchronizację, można uruchamiać przy użyciu konta z mniejszymi uprawnieniami.  Jest to mniej wydajne rozwiązanie, ale wymaga mniejszych uprawnień konta.

Jeśli katalog LDAP hello obsługuje i jest skonfigurowana dla narzędzia DirSync, następnie sondowania dla zmian w grupach użytkowników i zabezpieczeń będzie działać hello takie same jak w przypadku usługi Active Directory.  Jeśli hello katalogu LDAP nie obsługuje hello kontrolkę DirSync, Pełna synchronizacja jest wykonywane podczas jednego cyklu.

![Synchronizacja](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

Witaj Poniższa tabela zawiera dodatkowe informacje na temat każdego z ustawieniami tabulacji hello synchronizacji.

| Funkcja | Opis |
| --- | --- |
| Włącz synchronizację z usługą Active Directory |Po zaznaczeniu tej opcji, hello usługi serwera uwierzytelniania wieloskładnikowego okresowo sonduje zmiany usługi Active Directory. <br><br>Uwaga: należy dodać co najmniej jeden element synchronizacji i Synchronizuj teraz musi zostać wykonana przed powitania serwera uwierzytelniania wieloskładnikowego usługi rozpocznie przetwarzanie zmian. |
| Synchronizuj co |Określ hello czasu interwału powitania serwera uwierzytelniania wieloskładnikowego usługi będzie czekać między operacjami sondowania i przetwarzania zmian. <br><br> Uwaga: hello interwał jest określany hello czas między rozpoczęciami poszczególnych cyklów hello.  Jeśli hello czas przetwarzania zmian przekroczy interwał powitania hello usługa natychmiast ponownie wykona sondowanie. |
| Usuń użytkowników, którzy nie są już zarejestrowani w usłudze Active Directory |Po zaznaczeniu tej opcji, hello usługi serwera Multi-Factor Authentication będzie przetwarzać relikty użytkownika usługi Active Directory, usunąć i Usuń hello związane z serwera Multi-Factor Authentication użytkownika. |
| Zawsze wykonuj pełną synchronizację |Po zaznaczeniu tej opcji, hello usługi serwera Multi-Factor Authentication będzie zawsze wykonywać pełną synchronizację.  Po usunięciu zaznaczenia hello usługi serwera Multi-Factor Authentication będzie wykonywać synchronizację przyrostową, Sondując tylko użytkowników, które zostały zmienione.  Witaj domyślnie zaznaczenie jest usunięte. <br><br>W przypadku usunięcia zaznaczenia serwera usługi Azure MFA wykonuje synchronizację przyrostową tylko wtedy, gdy hello katalog obsługuje kontrolkę DirSync hello i hello konta powiązania toohello katalog ma zapytań przyrostowych DirSync tooperform uprawnienia.  Jeśli hello konto nie ma odpowiednich uprawnień hello lub wielu domen są zaangażowane w synchronizacji hello, serwera usługi Azure MFA wykonuje pełną synchronizację. |
| Wyłączenie lub usunięcie więcej niż X użytkowników powinno być zatwierdzane przez administratora. |Elementy synchronizacji można toodisable skonfigurowany lub usuń użytkowników, którzy nie są już członkami hello elementu kontenera lub grupy zabezpieczeń.  Ze względów bezpieczeństwa zatwierdzenia przez administratora może być wymagane, jeśli liczba hello toodisable użytkowników lub usuń przekracza próg.  W przypadku zaznaczenia pola zatwierdzenie jest wymagane dla określonego progu.  Witaj domyślna to 5 i hello zakres to 1 too999. <br><br> Umożliwiają to zatwierdzania najpierw wysyłane tooadministrators powiadomień e-mail. powiadomienie e-mail Hello zawiera instrukcje dotyczące sprawdzania i zatwierdzania hello wyłączenia i usunięcia użytkowników.  Po uruchomieniu interfejsu użytkownika serwera Multi-Factor Auth hello, pojawi się monit o zatwierdzenie. |

Witaj **Synchronizuj teraz** przycisk umożliwia toorun hello synchronizacji pełnej synchronizacji określonych elementów.  Pełna synchronizacja jest wymagana za każdym razem, gdy elementy synchronizacji są dodawane, modyfikowane, usuwane lub gdy zostaje zmieniona ich kolejność.  Możliwe jest również wymagana przed hello usługi Multi-Factor Authentication AdSync działa ponieważ określa hello początkowy z którego hello usługa będzie sondować zmiany przyrostowe.  Jeśli wprowadzono zmiany elementów toosynchronization, ale nie została wykonana synchronizacja pełna, zostanie wyświetlony monit o tooSynchronize będziesz mieć teraz.

Witaj **Usuń** przycisk umożliwia toodelete administratora hello jeden lub więcej elementów synchronizacji z listy elementów synchronizacji serwera uwierzytelniania wieloskładnikowego hello.

> [!WARNING]
> Usuniętego elementu synchronizacji nie można odzyskać. Konieczne będzie tooadd hello synchronizacji elementu rekordów ponownie Jeśli usunięto go przez pomyłkę.

Element synchronizacji Hello lub elementy synchronizacji zostały usunięte z serwera Multi-Factor Authentication.  Hello usługi serwera Multi-Factor Authentication nie będzie już przetwarzać elementów synchronizacji hello.

przyciski Przenieś w górę i Przenieś w dół Hello Zezwalaj administratorowi hello toochange hello kolejności elementów synchronizacji hello.  Witaj kolejność jest ważna, ponieważ hello tego samego użytkownika może być członkiem więcej niż jeden element synchronizacji (np. kontenera i grupy zabezpieczeń).  Ustawienia Hello użytkownika toohello zastosowane podczas synchronizacji będą pobierane z hello pierwszego elementu synchronizacji hello listy toowhich hello użytkownika jest skojarzony.  W związku z tym hello elementów synchronizacji należy umieścić w kolejności priorytetu.

> [!TIP]
> Po usunięciu elementów synchronizacji należy przeprowadzić pełną synchronizację.  Po określeniu kolejności elementów synchronizacji należy przeprowadzić pełną synchronizację.  Kliknij przycisk **Synchronizuj teraz** tooperform pełną synchronizację.

## <a name="multi-factor-auth-servers"></a>Serwery usługi Multi-Factor Auth
Dodatkowe serwery uwierzytelniania wieloskładnikowego można skonfigurować tooserve jako kopii zapasowej proxy RADIUS, serwera proxy LDAP, lub uwierzytelniania usług IIS. Konfiguracja synchronizacji Hello jest współdzielona przez wszystkich agentów hello. Jednak tylko jeden z tych agentów może mieć powitania serwera uwierzytelniania wieloskładnikowego usługa jest uruchomiona. Ta karta służy hello tooselect Multi-Factor Auth serwera, który powinien być włączony dla synchronizacji.

![Serwery usługi Multi-Factor Auth](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)
