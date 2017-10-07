---
title: "aaaLotus łącznik Domino | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooconfigure Microsoft programu Lotus Domino łącznika."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Dokumentacja techniczna programu Lotus Domino łącznika
W tym artykule opisano hello łącznika programu Lotus Domino. Witaj artykuł dotyczy toohello następujące produkty:

* Program Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Należy użyć poprawki 4.1.3671.0 lub nowszym [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 i FIM2010R2 hello łącznika jest dostępna do pobrania z hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-lotus-domino-connector"></a>Omówienie hello łącznika programu Lotus Domino
Witaj łącznika programu Lotus Domino umożliwia toointegrate hello synchronizacji usługi z serwerem programu Lotus Domino firmy IBM.

Z punktu widzenia wysokiego poziomu hello następujące funkcje są obsługiwane przez hello bieżącej wersji łącznika hello:

| Funkcja | Pomoc techniczna |
| --- | --- |
| Połączonego źródła danych |Serwer: <li>Programu Lotus Domino 8.5.x</li><li>Programu Lotus Domino 9.x</li>Klient:<li>Programu Lotus Domino 8.5.x</li><li>Program Lotus Notes 9.x</li> |
| Scenariusze |<li>Zarządzanie cyklem życia obiektów</li><li>Zarządzanie grupami</li><li>Zarządzanie hasłami</li> |
| Operacje |<li>Pełne i różnicowe importu</li><li>Eksportowanie</li><li>Ustaw i Zmień hasło na hasło HTTP</li> |
| Schemat |<li>Osoby (mobilnego użytkownika, skontaktuj się z pomocą (osób z żadnego certyfikatu))</li><li>Grupa</li><li>Zasób (zasobu, miejsca, spotkań Online)</li><li>Poczty w bazie danych</li><li>Dynamiczne odnajdowanie atrybuty obsługiwanych obiektów</li> |

Łącznik programu Lotus Domino Hello używa toocommunicate klienta programu Lotus Notes hello z programu Lotus Domino serwera. Wyniku tę zależność obsługiwany klient programu Lotus Notes muszą być zainstalowane na serwerze synchronizacji hello. Witaj komunikacji między powitania klienta i serwera hello jest implementowane za pośrednictwem interfejsu programu Lotus Notes .NET Interop (Interop.domino.dll) hello. Ten interfejs umożliwia hello komunikację między hello platformy Microsoft.NET i klienta programu Lotus Notes i obsługuje dostęp tooLotus Domino dokumentów i widoków. Import zmian jego jest również możliwe służy interfejsu macierzystego hello C++ (w zależności od hello wybrana metoda importu delta).

### <a name="prerequisites"></a>Wymagania wstępne
Przed użyciem hello łącznika, upewnij się, że masz następujące wymagania wstępne dotyczące serwera synchronizacji hello hello:

* Framework Microsoft .NET 4.5.2 lub nowszej
* musi być zainstalowany klient programu Lotus Notes Hello na serwerze synchronizacji
* Witaj łącznika programu Lotus Domino wymaga hello domyślnego programu Lotus Domino LDAP schematu bazy danych (schema.nsf) toobe występuje na serwerze katalogu Domino hello. Jeśli nie jest obecny, można zainstalować go przez uruchomiona lub ponowne uruchomienie usługi LDAP hello na powitania serwera Domino.

### <a name="connected-data-source-permissions"></a>Połączone uprawnienia źródła danych
tooperform obsługiwane wszystkie hello zadania w łącznika programu Lotus Domino, użytkownik musi należeć do następujących grup:

* Pełny dostęp do administratorów
* Administratorzy
* Administratorzy baz danych

Witaj poniższej tabeli wymieniono hello uprawnienia, które są wymagane dla każdej operacji:

| Operacja | Prawa dostępu |
| --- | --- |
| Import |<li>Odczytywać dokumenty publiczne</li><li> Pełny dostęp administratora (gdy jesteś członkiem grupy administratorów pełny dostęp automatycznie masz tooin dostęp czynny hello ACL.)</li> |
| Eksportowanie i ustawienia hasła |Dostęp czynny: <li>Tworzenie dokumentów</li><li>Usuwanie dokumentów</li><li>Odczytywać dokumenty publiczne</li><li>Zapis dokumenty publiczne</li><li>Replikacja lub kopiowania dokumentów</li>Dla operacji eksportowania potrzebne są także hello następujące role: <li>Metoda CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>Operacje bezpośredniego i AdminP
Operacje przejdź bezpośrednio toohello Domino katalogu lub za pośrednictwem hello AdminP przetworzyć. Witaj poniższe tabele zawierają wszystkie obiekty obsługiwane operacje i, jeśli to konieczne, hello związanych implementacji metody:

**Książka adresowa podstawowego**

| Obiekt | Przycisk Utwórz | Aktualizacja | Usuwanie |
| --- | --- | --- | --- |
| Osoby |AdminP |Bezpośrednie |AdminP |
| Grupa |AdminP |Bezpośrednie |AdminP |
| MailInDB |Bezpośrednie |Bezpośrednie |Bezpośrednie |
| Zasób |AdminP |Bezpośrednie |AdminP |

**Książka adresowa dodatkowej**

| Obiekt | Przycisk Utwórz | Aktualizacja | Usuwanie |
| --- | --- | --- | --- |
| Osoby |Nie dotyczy |Bezpośrednie |Bezpośrednie |
| Grupa |Bezpośrednie |Bezpośrednie |Bezpośrednie |
| MailInDB |Bezpośrednie |Bezpośrednie |Bezpośrednie |
| Zasób |Nie dotyczy |Nie dotyczy |Nie dotyczy |

Po utworzeniu zasobu, tworzony jest dokument uwagi. Podobnie jeśli zasób zostanie usunięty, dokument uwagi hello jest usuwany.

### <a name="ports-and-protocols"></a>Porty i protokoły
IBM Lotus Notes klientów i serwerów Domino komunikują się za pomocą uwagi dotyczące zdalnego procedury wywołania (NRPC) gdzie NRPC należy używać protokołu TCP/IP. Domyślny numer portu Hello jest 1352, ale może zostać zmieniona przez administratora Domino hello.

### <a name="not-supported"></a>Nieobsługiwane
Hello następujące operacje nie są obsługiwane w bieżącej wersji łącznika programu Lotus Domino hello hello:

* Przenoszenie skrzynek pocztowych między serwerami.

## <a name="create-a-new-connector"></a>Utwórz nowy łącznik
### <a name="client-software-installation-and-configuration"></a>Instalacja oprogramowania klienta i konfiguracji
Program Lotus Notes musi być zainstalowany na serwerze hello **przed** hello łącznik jest zainstalowany.

Po zainstalowaniu, pamiętaj, aby **zainstalować pojedynczego użytkownika**. Witaj domyślne **zainstalować wielu użytkowników** nie działa.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

Na stronie funkcji hello Instaluj tylko hello wymagane funkcje programu Lotus Notes i **logowania jednokrotnego klienta**. Wymagany stanie toolog toobe hello łącznika na serwerze Domino toohello jest logowania jednokrotnego.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**Uwaga:** Start programu Lotus Notes po z użytkownikiem, który znajduje się na powitania tym samym serwerze co hello konta należy używać hello konta usługi łącznika. Upewnij się, że klient programu Lotus Notes hello tooclose również na powitania serwera. Nie mogą być uruchomione na powitania tym samym czasie hello łącznika próbuje tooconnect toohello Domino serwera.

### <a name="create-connector"></a>Tworzenie łącznika
tooCreate łącznika programu Lotus Domino w **usługi synchronizacji** wybierz **agenta zarządzania** i **Utwórz**. Wybierz hello **programu Lotus Domino (Microsoft)** łącznika.  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

Jeśli swoją wersję usługi synchronizacji oferuje hello możliwości tooconfigure **architektura**, upewnij się, że łącznik hello ustawiono tooits domyślną wartość toorun **procesu**.

### <a name="connectivity"></a>Łączność
Na stronie łączność hello należy określić nazwę serwera programu Lotus Domino hello i wprowadź poświadczenia logowania hello.  
![Łączność](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

właściwości serwera Domino Hello obsługuje dwa formaty dla nazwy serwera hello:

* serverName
* ServerName/DirectoryName

Witaj **ServerName/DirectoryName** format jest hello preferowanym formatem dla tego atrybutu, ponieważ zapewnia szybszej odpowiedzi kontaktów łącznika hello hello Domino serwera.

Hello pod warunkiem, że nazwa użytkownika plik jest przechowywany w bazie danych konfiguracji hello hello usługi synchronizacji.

Aby uzyskać **Import zmian** dostępne są następujące opcje:

* **Brak**. Witaj łącznika nie importuje żadnych zmian.
* **Dodawanie aktualizacji**. import zmian ma łącznika Hello Dodaj i operacje aktualizacji. Do usunięcia **pełny Import** operacji jest wymagany. Ta operacja jest przy użyciu hello .net interop.
* **Dodaj/aktualizowania/usuwania**. import zmian ma łącznika Hello dodawania, aktualizacji i usuwania operacji. Ta operacja jest przy użyciu macierzystych interfejsów C++ hello.

W **opcje schematu** masz hello następujące opcje:

* **Domyślny schemat**. Hello łącznika wykrywa hello schematu z hello Domino serwera. Ta opcja jest hello opcji domyślnej.
* **Schemat DSML**. Użyć tylko w przypadku serwera Domino hello nie ujawnia hello schematu. Następnie można utworzyć plik DSML ze schematem hello i zaimportuj go w zamian. Aby uzyskać więcej informacji o DSML, zobacz [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml).

Po kliknięciu przycisku Dalej zweryfikować hello identyfikator użytkownika i hasło Parametry konfiguracji.

### <a name="global-parameters"></a>Parametry globalne
Na stronie parametry globalne hello skonfiguruj hello strefy czasowej, a następnie zaimportuj hello i export — opcja operacji.  
![Parametry globalne](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

Witaj **strefy czasowej serwera Domino** hello lokalizację serwera Domino definiuje parametru.

Ta opcja konfiguracji jest wymagana toosupport **import zmian** operacji ponieważ dzięki usługi synchronizacji hello Określanie zmian między hello importów ostatnie dwa.

>[!Note]
Począwszy od hello 2017 marca aktualizacji hello parametry globalne ekranu baza hello opcja toodelete hello użytkownika poczty podczas usuwania hello użytkownika.

![Usuwanie skrzynki pocztowej użytkownika](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>Importowanie ustawień — metoda
Witaj **Wykonaj pełny Import przez** zawiera następujące opcje:

* Wyszukiwanie
* Widok (zalecane)

**Wyszukiwanie** jest przy użyciu indeksowania w Domino, ale jest typowe hello indeksy nie są aktualizowane w czasie rzeczywistym, a nie danych hello zwrócony z serwera hello zawsze jest poprawna. Dla systemu z dużej liczby zmian ta opcja zwykle nie działa prawidłowo i zapewnia usuwa false w niektórych sytuacjach. Jednak **wyszukiwania** jest szybsza niż **widoku**.

**Widok** jest hello opcja zalecana, ponieważ zapewnia hello faktyczny stan danych. Jest nieco wolniej niż wyszukiwania.

#### <a name="creation-of-virtual-contact-objects"></a>Tworzenie wirtualnych obiektów kontaktów
Witaj **umożliwiają tworzenie \_obiektu kontaktu** zawiera następujące opcje:

* Brak
* Wartości-Reference
* Wartości odwołania i -Reference

W Domino atrybutów odwołania może zawierać wielu różnych formatach tooreference inne obiekty. toobe toorepresent stanie możliwych kombinacji hello implementuje łącznika \_skontaktuj się z obiektów, znanej także jako **wirtualnego kontaktów** (VC). Te obiekty są tworzone może dołączyć do obiektów tooexisting MV lub przekazywany jako nowych obiektów. W ten sposób odwołania atrybut będzie możliwe.

Po włączeniu tego ustawienia i w razie hello zawartość jest atrybut odwołania nie jest format nazwy domeny, \_tworzony jest obiekt kontaktu. Na przykład atrybutem elementu członkowskiego grupy może zawierać adresów SMTP. Możliwe jest również możliwe toohave nazwa_skrócona i inne atrybuty obecnych w atrybutów odwołania. W tym scenariuszu wybierz **wartości inne niż odwołanie**. Ta konfiguracja jest hello najczęstsze ustawienie Domino implementacji.

W przypadku programu Lotus Domino toohave skonfigurowanych książki adresowe oddzielne o różnych nazwach wyróżniającej reprezentujący hello tego samego obiektu, Utwórz tooalso możliwe jego \_skontaktuj się z pomocą obiektów, wszystkie wartości odwołania, które znajdują się w książce adresowej. W tym scenariuszu wybierz hello **odwołania i wartości inne niż odwołanie** opcji.

Jeśli masz wiele wartości w atrybucie hello **imię i nazwisko** w Domino, następnie również mają tooenable hello Tworzenie wirtualnych kontaktów, odwołań, mogą zostać rozwiązane. Na przykład ten atrybut może mieć wielu wartości po unieważnienie lub rozwodu. Zaznacz pole wyboru hello **włączyć... Imię i nazwisko ma wiele wartości** dla tego scenariusza.

Łącząc hello prawidłowe atrybuty hello \_skontaktuj się z pomocą obiektów będą połączone toohello MV obiektu.

Te obiekty mają VC =\_kontakt dodany tootheir DN.

#### <a name="import-settings-conflict-object"></a>Importowanie ustawień, konflikt obiektu
**Wyklucz obiekty konflikt**

W dużych implementacji Domino jest to możliwe, że wiele obiektów ma hello DN tego samego powodu tooreplication problemów. W takich przypadkach łącznika hello zobaczy dwa obiekty o różnych UniversalIDs, ale tej samej nazwy domeny. Obiekt przejściowej tworzony w przestrzeni łącznika hello spowoduje, że ten konflikt. Witaj łącznika można zignorować hello obiektów, które zostały wybrane w Domino jako ofiary replikacji. zalecenie Hello jest tookeep to pole wyboru jest zaznaczone.

#### <a name="export-settings"></a>Eksportowanie ustawień
Jeśli hello opcję **AdminP używać do aktualizowania odwołań** nie jest zaznaczona, eksport atrybutów odwołania, takich jak elementu członkowskiego, bezpośrednie wywołania i nie używa hello AdminP procesu. Tej opcji należy używać tylko wtedy, gdy AdminP nie został skonfigurowany toomaintain integralności referencyjnej.

#### <a name="routing-information"></a>Informacje dotyczące routingu
W Domino istnieje możliwość, że atrybut odwołania ma informacje o routing osadzony jako toohello sufiks nazwy domeny. Na przykład może zawierać atrybut member hello w grupie **CN =example/organization@ABC**. sufiks Hello @ABC hello informacje routingu. informacje o routing Hello jest używany przez Domino toosend wiadomości e-mail toohello poprawne Domino system, który może być systemu w innej organizacji. W polu informacje routingu hello można określić routing sufiksów hello używane w ramach hello organizacji w zakresie hello łącznika. Jeśli jeden z tych wartości zostanie znaleziony sufiks atrybut odwołania, informacje routingu hello jest usuwany z hello odwołania. Jeśli sufiks routingu hello na wartość odwołania nie może być dopasowane tooone tych wartości jest określony, \_tworzony jest obiekt kontaktu. Te \_kontaktu obiekty są tworzone z **RO = @<RoutingSuffix>**  wstawione do hello nazwy domeny. W tym \_obiekty kontaktu hello następujące atrybuty są również dodane tooallow dołączenie tooa rzeczywistego obiektu w razie potrzeby: \_routingName, \_przedstawiciel, \_displayName i UniversalID.

#### <a name="additional-address-books"></a>Dodatkowe książki adresowe
Jeśli nie masz **pomocy katalogu** zainstalowany, zapewniające hello nazwę książki adresowe dodatkowej, a następnie możesz ręcznie wprowadzić te książki adresowej.

#### <a name="multivalued-transformation"></a>Transformacja wielowartościowego
Wiele w Lotus Domino atrybuty wielowartościowe. Witaj odpowiednie atrybuty metaverse są zwykle jednej wartości. Konfigurując hello Import i opcja operacji eksportowania hello, należy włączyć hello toohelp łącznika z tłumaczenia hello wymaganych atrybutów hello, których to dotyczy.

**Eksportuj**  
Opcja operacji eksportowania Hello obsługuje dwa tryby:

* Dołączanie elementu
* Zastąp element

**Zastąp element** — po wybraniu tej opcji, zawsze łącznika hello hello Usuń bieżące wartości atrybutu hello w Domino i zastąpi je wartościami hello podane. Witaj, pod warunkiem o wartościach można jednowartościowych lub wielokrotne wartości.

Przykład: hello Asystenta atrybut obiektu osoba ma hello następujące wartości:

* CN = Winston/OU=Contoso/O=Americas,NAB=names.nsf Gregowi
* CN = Smith/OU=Contoso/O=Americas,NAB=names.nsf Jan

Jeśli nowego Asystenta o nazwie **Alexander Dominik** jest przypisany obiekt osoby toothis, wynik hello jest:

* CN = Alexander/OU=Contoso/O=Americas,NAB=names.nsf Dominik

**Dołączanie elementu** — po wybraniu tej opcji, łącznik hello zachowuje hello istniejące wartości w atrybucie hello Domino i Wstaw nowe wartości na początku hello hello danych listy.

Przykład: hello Asystenta atrybut obiektu osoba ma hello następujące wartości:

* CN = Winston/OU=Contoso/O=Americas,NAB=names.nsf Gregowi
* CN = Smith/OU=Contoso/O=Americas,NAB=names.nsf Jan

Jeśli nowego Asystenta o nazwie **Alexander Dominik** jest przypisany obiekt osoby toothis, wynik hello jest:

* CN = Alexander/OU=Contoso/O=Americas,NAB=names.nsf Dominik
* CN = Winston/OU=Contoso/O=Americas,NAB=names.nsf Gregowi
* CN = Smith/OU=Contoso/O=Americas,NAB=names.nsf Jan

**Importowanie**  
Witaj opcję operacji importu obsługuje dwa tryby:

* Domyślne
* Wielowartościowy tooSingle wartość

**Domyślna** — po wybraniu opcji domyślnej hello wszystkie wartości hello wszystkie atrybuty są importowane.

**Wielowartościowy tooSingle wartość** — po wybraniu tej opcji wielowartościowy atrybut jest konwertowany na atrybutu jednowartościowego. Jeśli istnieje więcej niż jedną wartość, zostanie użyta wartość hello na górze hello (Ta wartość jest zazwyczaj również hello najnowsza wersja).

Przykład: hello Asystenta atrybut obiektu osoba ma hello następujące wartości:

* CN = Alexander/OU=Contoso/O=Americas,NAB=names.nsf Dominik
* CN = Winston/OU=Contoso/O=Americas,NAB=names.nsf Gregowi
* CN = Smith/OU=Contoso/O=Americas,NAB=names.nsf Jan

Witaj najnowszych aktualizacji toothis atrybut jest **Alexander Dominik**. Ponieważ hello opcję operacja importu ma wartość tooSingle tooMultivalued wartość, łącznik importuje jedynie **Alexander Dominik** do przestrzeni łącznika hello.

atrybuty wielowartościowe tooconvert logiki Hello na atrybuty jednowartościowe nie ma zastosowania atrybutu elementu członkowskiego grupy toohello i atrybut imię i nazwisko osoby toohello.

On również możliwe tooconfigure importowanie i eksportowanie reguł przekształcania dla atrybutów wielowartościowych dla atrybutu, jako wyjątek toohello globalnej reguły. tooconfigure tę opcję, wprowadź [objecttype]. [attributename] w hello **zaimportować listy wykluczeń atrybutu** i **wyeksportować listę wykluczeń atrybutu** pól tekstowych. Na przykład Person.Assistant i ustawiono flagi globalne hello tooimport wszystkie wartości, tylko pierwsza wartość hello jest importowany Asystenta hello.

#### <a name="certifiers"></a>Wydających świadectwa
Wszystkie jednostki organizacyjnej/organizacji są wyświetlane według hello łącznika. toobe tooexport stanie osoby obiektów toohello głównej książkę adresową, certifier z jego hasło jest wymagane.

Jeśli wszystkie wydających świadectwa hello tego samego hasła, hello **hasła dla wszystkich Certifers** mogą być używane. Następnie można wprowadzić hasło hello tutaj i tylko określić plik certifier hello.

Jeśli importowany tylko, następnie nie masz toospecify żadnych wydających świadectwa.

### <a name="configure-provisioning-hierarchy"></a>Konfigurowanie hierarchii zastrzegania
Podczas konfigurowania łącznika programu Lotus Domino hello, Pomiń tę stronę okna dialogowego. Łącznik programu Lotus Domino Hello nie obsługuje inicjowania obsługi administracyjnej hierarchii.  
![Inicjowanie obsługi administracyjnej hierarchii](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>Konfiguruj partycje i hierarchie
Po skonfigurowaniu partycje i hierarchie, musisz wybrać książki adresowej głównej hello o nazwie NAB=names.nsf. Ponadto toohello książki adresowej podstawowej, można wybrać książki adresowe dodatkowej jeżeli istnieją.  
![Partycje](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>Wybierz atrybuty
Po skonfigurowaniu sieci atrybuty, należy wybrać wszystkie atrybuty, które mają przedrostek  **\_MMS\_**. Te atrybuty są wymagane podczas obsługi administracyjnej nowych obiektów tooLotus Domino

![Atrybuty](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>Zarządzanie cyklem życia obiektów
Ta sekcja zawiera przegląd różnych obiektów hello w Domino.

### <a name="person-objects"></a>Obiekty osoby
Obiekt osoby Hello reprezentuje użytkowników w organizacji i jednostek organizacyjnych. Ponadto toohello domyślne atrybuty, hello Domino administrator można dodać obiektu osoby tooa atrybutów niestandardowych. Co najmniej obiektu osoby musi zawierać wszystkie wymagane atrybuty. Aby uzyskać pełną listę atrybutów obowiązkowych, zobacz [programu Lotus Notes właściwości](#lotus-notes-properties). muszą być spełnione tooregister obiektu osoby hello następujące wymagania wstępne:

* Książka adresowa Hello (names.nsf) musi została określona i powinna być hello książki adresowej podstawowego.
* Musisz mieć hello O/OU certifier identyfikator i hello hasła tooregister dany użytkownik w organizacji hello / jednostka organizacyjna.
* Musisz ustawić określony zbiór właściwości programu Lotus Notes dla obiekt osoby. Te właściwości są używane do inicjowania obsługi hello osoby obiektu. Aby uzyskać więcej informacji, zobacz sekcję hello o nazwie [programu Lotus Notes właściwości](#lotus-notes-properties) dalszej części tego dokumentu.
* hasła początkowego HTTP Hello osoby to atrybut i zestaw podczas inicjowania obsługi.
* Obiekt osoby Hello musi mieć jedną z hello następujące trzy obsługiwane typy:
  1. Użytkownik normalny z pliku poczty i plik identyfikator użytkownika
  2. Mobilnych użytkownika (zwykle użytkownik, który zawiera wszystkie pliki bazy danych mobilnych)
  3. Kontakty (użytkownika z żadnego pliku id)

Osoby (z wyjątkiem kontaktów) można grupować w nam użytkownicy i międzynarodowej dalsze określone przez wartość hello hello \_MMS\_IDRegType właściwości. Te osoby używają powitania klienta uwagi tooaccess serwerów programu Lotus Domino, ma identyfikator uwagi i zarządzania dokumentami osoby. Jeśli używają poczty uwagi, następnie mają także plik poczty. Witaj, użytkownik musi być zarejestrowany toobecome active. Aby uzyskać więcej informacji, zobacz:

* [Konfigurowanie użytkowników o wersji](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [Rejestracja użytkownika](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [Zarządzanie użytkownikami](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [Zmiana nazwy użytkowników](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

Te operacje są wykonywane w Lotus Domino i następnie zaimportować do usługi synchronizacji hello.

### <a name="resources-and-rooms"></a>Zasoby i pomieszczenia
Zasób jest innego typu z bazą danych programu Lotus Domino. Zasoby mogą być sal konferencyjnych z różnymi typami urządzeń, takich jak projektorów. Istnieją podtypów zasobów obsługiwane przez łącznik programu Lotus Domino, które są definiowane przez hello atrybutu Typ zasobu:

| Typ zasobu | Atrybut typu zasobu |
| --- | --- |
| Miejsca |1 |
| Zasób (inny) |2 |
| Spotkań online |3 |

Dla hello zasobów obiektu typu toowork wymagane jest spełnienie następujących hello:

* Bazy danych zasobów rezerwacji powinna już istnieć w hello połączony serwer Domino
* Witaj witryny jest już zdefiniowany dla hello zasobów

Baza danych rezerwacji zasobów Hello zawiera trzy typy dokumentów:

* Profil lokacji
* Zasób
* Rezerwacja

Aby uzyskać więcej informacji na temat konfigurowania rezerwacji zasobów bazy danych, zobacz [konfigurowania bazy danych zasobów zastrzeżenia hello](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html).

**Tworzenia, aktualizacji i usuwania zasobów**  
Witaj tworzenia, aktualizowania lub usuwania operacje są wykonywane przez łącznik programu Lotus Domino hello w hello rezerwacji zasobów w bazie danych. Zasoby są tworzone jako dokumenty w Names.nsf (to znaczy Książka adresowa głównej hello). Aby uzyskać więcej informacji na temat edytowanie i usuwanie zasobów, zobacz [edytowanie i usuwanie dokumentów zasobu](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html).

**Importowanie i eksportowanie operacji dla zasobów**  
Hello zasoby mogą być importowane tooand wyeksportowany z usługi synchronizacji hello, takie jak dowolny inny typ obiektu. Witaj wybierz typ obiektu jako zasób podczas konfiguracji. Dla operacji eksportowania pomyślnie powinien mieć szczegółowe informacje dotyczące typu zasobu, konferencji bazy danych i nazwa lokacji.

### <a name="mail-in-databases"></a>Poczty w bazach danych
Baza danych w poczty jest bazy danych, która jest zaprojektowana tooreceive wiadomości. Jest skrzynki pocztowej programu Lotus Domino, która nie jest skojarzony z dowolnego określonego konta użytkownika programu Lotus Domino (to znaczy, że nie ma własny plik ID i hasło). Poczty w bazie danych ma unikatowy identyfikator użytkownika ("krótkiej nazwy") z nią związane oraz adres e-mail.

Jeśli istnieje potrzeba oddzielne skrzynki pocztowej swój własny adres e-mail, które mogą być współużytkowane przez różnych użytkowników (na przykład group@contoso.com), zostanie utworzona baza danych w wiadomości. Skrzynka pocztowa toothis dostępu Hello jest kontrolowany za pośrednictwem jego listy kontroli dostępu (ACL), zawierający nazwy hello hello uwagi użytkowników, którzy mogą tooopen hello pocztowej.

Lista atrybutów hello wymagane sekcji hello o nazwie [atrybutów obowiązkowych](#mandatory-attributes) dalszej części tego artykułu.

Gdy baza danych jest zaprojektowana tooreceive wiadomości e-mail, dokumentów poczty w bazie danych jest tworzony w Lotus Domino. Ten dokument musi istnieć w katalogu Domino na każdym serwerze, który przechowuje kopię hello bazy danych. Aby uzyskać szczegółowy opis o tworzeniu dokumentów w poczty bazy danych, zobacz [tworzenia dokumentu poczty w bazie danych](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html).

Przed utworzeniem poczty w bazie danych, bazy danych hello powinna już istnieć (powinna zostać utworzona przez administratora programu Lotus) na serwerze Domino hello.

### <a name="group-management"></a>Zarządzanie grupami
Szczegółowe omówienie hello Lotus Domino grupy zarządzania można uzyskać z hello następujące zasoby:

* [Przy użyciu grup](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [Tworzenie grupy](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [Tworzenie i modyfikowanie grup](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [Zarządzanie grupami](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [Zmiana nazwy grupy](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>Zarządzanie hasłami
W przypadku zarejestrowanego użytkownika programu Lotus Domino istnieją dwa typy haseł:

1. Hasło użytkownika (przechowywane w pliku User.id)
2. Internet / HTTP hasła

Łącznik programu Lotus Domino Hello obsługuje tylko operacje hasłem HTTP.

Zarządzanie hasłami tooperform, należy włączyć zarządzanie hasłami dla łącznika hello w hello projektanta agenta zarządzania. Zarządzanie hasłami tooenable, wybierz opcję **włączyć zarządzanie hasłami** na powitania **skonfigurować rozszerzenia** strony okna dialogowego.  
![Konfigurowanie rozszerzeń](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

Obsługa łącznika programu Lotus Domino Hello następujące operacje na Internet hasło:

* Ustaw hasło: Ustaw hasło ustawia hello użytkownika w Domino nowe hasło HTTP w Internecie. Domyślnie konto hello jest także odblokowane. Hello odblokowywania flagi jest narażony na powitania WMI interfejsu hello aparatu synchronizacji.
* Zmień hasło: W tym scenariuszu użytkownik może chcieć toochange hello hasła lub jest toochange zostanie wyświetlony monit o hasło po określonym czasie. Tego miejsca tootake operacji zarówno (hello starego i nowego hasła hello) są obowiązkowe. Po zmianie, hello nowe hasło jest aktualizowana w Lotus Domino.

Aby uzyskać więcej informacji, zobacz:

* [Przy użyciu funkcji blokady hello Internet](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [Zarządzanie hasłami Internet](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>Informacje referencyjne
Ta sekcja zawiera informacje takie jak opisy atrybutów i wymagania dotyczące atrybutów dla łącznika programu Lotus Domino hello.

### <a name="lotus-notes-properties"></a>Właściwości programu Lotus Notes
Podczas obsługi administracyjnej osoby obiektów tooyour Lotus Domino katalogu obiektów musi mieć określony zestaw właściwości z określonymi wartościami wypełnione. Te wartości są wymagane tylko dla operacji tworzenia.

Witaj poniższej tabeli wymieniono te właściwości oraz opis ich.

| Właściwość | Opis |
| --- | --- |
| \_MMS_AltFullName |Witaj alternatywny imię i nazwisko użytkownika. |
| \_MMS_AltFullNameLanguage |Witaj toobe język używany do określania hello alternatywny pełną nazwę użytkownika. |
| \_MMS_CertDaysToExpire |Hello liczbę dni od hello bieżącą datę przed hello certyfikat wygaśnie. Jeśli nie zostanie określony, hello domyślna data wynosi dwa lata z hello bieżącą datę. |
| \_MMS_Certifier |Właściwość, która zawiera nazwę organizacji hierarchii hello hello certifier. Na przykład: OU = OrganizationUnit, O = Org, C = kraju. |
| \_MMS_IDPath |Jeśli właściwość hello jest pusta, plik identyfikator użytkownika nie jest tworzony lokalnie na powitania serwera synchronizacji. Jeśli właściwość hello zawiera nazwę pliku, plik identyfikator użytkownika jest tworzony w folderze madata hello. Właściwość Hello może również zawierać pełną ścieżkę. |
| \_MMS_IDRegType |Osoby mogą być klasyfikowane jako kontakty, nam użytkowników i międzynarodowe użytkowników. Witaj Poniższa tabela zawiera listę możliwych wartości hello: <li>0 — kontakt</li><li>1 - użytkownik stany USA</li><li>2 - międzynarodowe użytkownika</li> |
| \_MMS_IDStoreType |Wymagana właściwość amerykańskie i międzynarodowe użytkowników. Właściwość Hello zawiera wartość całkowitą, która określa, czy identyfikator użytkownika hello jest przechowywana jako załącznik w książce adresowej uwagi hello lub w pliku wiadomości powitania osoby. Jeśli plik identyfikator użytkownika hello jest załącznik w książce adresowej hello, opcjonalnie można go utworzyć jako plik z \_MMS_IDPath. <li>Empty — identyfikator magazynu plików w magazynie identyfikator, plik nie identyfikacji (używanych do kontaktów).</li><li> 1 - załącznika w książce adresowej hello uwagi. Witaj \_musi być ustawiona właściwość MMS_Password plików identyfikacji użytkownika, które są załączników</li><li>2 — identyfikator sklepu w pliku Mail osoby. Witaj \_MMS_UseAdminP musi być ustawiona toofalse toolet hello poczty podczas hello osoby rejestracji można utworzyć pliku. Witaj \_musi być ustawiona właściwość MMS_Password plików identyfikacji użytkownika.</li> |
| \_MMS_MailQuotaSizeLimit |Witaj liczba megabajtów, które są dozwolone dla hello e-mail plik bazy danych. |
| \_MMS_MailQuotaWarningThreshold |Witaj liczba megabajtów, które są dozwolone dla hello e-mail plik bazy danych, zanim pojawi się ostrzeżenie. |
| \_MMS_MailTemplateName |Witaj e-mail plik szablonu użytkownika hello toocreate używanych poczty e-mail plików. Jeśli szablon zostanie określona, plik poczty hello jest tworzony przy użyciu hello określonego szablonu. Jeśli szablon nie zostanie określony, hello domyślnego szablonu jest używane toocreate hello plik. |
| \_MMS_OU |Opcjonalna właściwość jest hello nazwę jednostki Organizacyjnej, w obszarze hello certifier. Ta właściwość powinna być pusta kontaktów. |
| \_MMS_Password |Wymagana właściwość dla użytkowników. Właściwość Hello zawiera hello hasło dla pliku identyfikacji hello hello obiektu. |
| \_MMS_UseAdminP |Właściwość powinna być tootrue zestawu, jeśli plik poczty hello powinien zostać utworzony przez proces AdminP hello na serwerze Domino hello (proces eksportu toohello asynchroniczne). Jeśli ustawiono właściwość toofalse hello poczty jest tworzony plik z hello Domino użytkownika (synchroniczne w procesie eksportu hello). |

Dla użytkownika przy użyciu pliku skojarzony identyfikator hello \_właściwości MMS_Password musi zawierać wartość. Aby uzyskać dostęp do poczty e-mail za pomocą klienta programu Lotus Notes hello hello MailServer i MailFile właściwości użytkownika musi zawierać wartość.

tooaccess wiadomości e-mail za pośrednictwem przeglądarki sieci Web, hello następujące właściwości muszą zawierać wartości:

* MailFile - wymaganą właściwość, która zawiera ścieżkę hello na serwerze programu Lotus Domino hello przechowywania plików wiadomości powitania.
* MailServer - wymaganą właściwość, która zawiera nazwę hello hello Lotus Domino serwera. Ta wartość jest toouse nazwa hello podczas tworzenia pliku poczty Lotus hello na powitania serwera Domino.
* HTTPPassword — opcjonalnie właściwość, która zawiera hello hasła dostępu do sieci Web dla obiekt hello.

tooaccess hello serwera Domino bez możliwości poczty, hello właściwość HTTPPassword musi zawierać wartość. Witaj MailFile właściwości i hello MailServer właściwość może być puste.

Z \_MMS_ IDStoreType (identyfikator magazynu w pliku poczty), 2 = hello MailSystem właściwość NotesRegistrationclass ustawiono tooREG_MAILSYSTEM_INOTES (3).

### <a name="mandatory-attributes"></a>Atrybutów obowiązkowych
Łącznik programu Lotus Domino Hello głównie obsługuje te typy obiektów (typów dokumentów):

* Grupa
* Poczty w bazie danych
* Osoby
* Skontaktuj się z pomocą (osoba mająca nie certifier)
* Zasób

Ta sekcja zawiera listę atrybutów hello, które są wymagane dla każdego obsługiwanego obiektu tooexport tooa Domino serwera.

| Typ obiektu | Atrybutów obowiązkowych |
| --- | --- |
| Grupa |<li>Zdefiniowana</li> |
| Główny w bazie danych |<li>Imię i nazwisko</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Osoby |<li>Nazwisko</li><li>MailFile</li><li>Nazwa_skrócona</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| Skontaktuj się z pomocą (osoba mająca nie certifier) |<li>\_MMS_IDRegType</li> |
| Zasób |<li>Imię i nazwisko</li><li>ResourceType</li><li>ConfDB</li><li>Dyspozycyjność zasobu</li><li>Lokacji</li><li>Nazwa wyświetlana</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>Najczęściej występujących problemów i pytania
### <a name="schema-detection-does-not-work"></a>Wykrywanie schematu nie działa.
Schemat hello stanie toodetect toobe, konieczne jest czy plik schema.nsf hello jest obecna na serwerze Domino hello. Ten plik jest wyświetlany tylko, jeśli LDAP jest zainstalowany na powitania serwera. Jeśli schemat hello nie jest wykrywalny, sprawdź następujące hello:

* schema.nsf pliku Hello jest dostępne w folderze głównym hello powitania serwera Domino
* Witaj użytkownik ma uprawnienia toosee hello schema.nsf pliku.
* Wymusić ponowne uruchomienie serwera LDAP hello. Otwórz **programu Lotus Domino konsoli** i użyj **Poinformuj ReloadSchema LDAP** polecenia tooreload hello schematu.

### <a name="not-all-secondary-address-books-are-visible"></a>Nie wszystkie książki adresowe dodatkowej są widoczne
Witaj łącznika Domino zależy od funkcji hello **pomocy katalogu** książki adresowe dodatkowej hello stanie toofind toobe. Jeśli brakuje hello książki adresowe dodatkowej, sprawdź, czy [pomocy katalogu](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) została włączona i skonfigurowana na powitania serwera Domino.

### <a name="custom-attributes-in-domino"></a>Atrybuty niestandardowe w Domino
Istnieje kilka metod w schemacie hello tooextend Domino, więc pojawia się jako atrybut niestandardowy eksploatacyjny przez hello łącznika.

**Podejście 1: Rozszerzenie schematu programu Lotus Domino**

1. Utwórz kopię szablonu katalogu Domino {PUBNAMES. NTF} wykonując [te kroki](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (należy nie dostosować hello IBM Lotus Domino katalogu szablonu):
2. Otwórz hello kopiowania Domino katalogu szablonu {CONTOSO. Szablon NTF}, który został utworzony w Projektancie Domino i wykonaj następujące kroki:
   * Kliknij pozycję udostępnione elementy, a następnie rozwiń węzeł podformularze
   * Kliknij dwukrotnie podformularz InheritableSchema ${ObjectName} ({ObjectName} w przypadku hello nazwę klasy hello domyślnego obiektu strukturalnego, na przykład: osoby).
   * Nazwa atrybutu hello ma tooadd do schematu {MyPersonAtrribute} i odpowiedniego atrybutu toothat. Utwórz pole przez wybierz hello **Utwórz** Menu, a następnie wybierz **pola** z menu.
   * W polu dodano hello ustawienia swoich właściwości, wybierając jego typ, Style, rozmiar, czcionki i inne powiązane parametry w oknie właściwości pola.
   * Atrybut hello utrzymania wartością domyślną takie same jak nazwa hello podany dla tego atrybutu (na przykład, jeśli nazwa atrybutu jest MyPersonAttribute, należy zachować wartość domyślną hello z hello tej samej nazwy).
   * Zapisz hello ${ObjectName} InheritableSchema podformularz zaktualizowane wartości.
3. Zastąp hello Domino katalogu szablonu {PUBNAMES. NTF} z hello nowe dostosowany szablon {CONTOSO. NTF} wykonując [te kroki](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
4. Zamknij Domino administratora i otwórz hello toorestart Domino konsoli usługi LDAP i hello tooReload schematu LDAP:
   * W konsoli Domino Wstaw polecenie hello w obszarze **polecenia Domino** tekst zachowano usługi LDAP hello toorestart — [Uruchom ponownie zadanie LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
   * Schemat LDAP tooreload, użyj polecenia Poinformuj LDAP - Poinformuj ReloadSchema LDAP
5. Otwórz administratora Domino i wybierz osoby i grupy toosee kartę dodać atrybut jest widoczny w domino Dodaj osobę.
6. Otwórz Schema.nsf z **pliki** karcie i zobacz, dodane atrybuty jest uwzględniane w klasie obiektów dominoPerson LDAP.

**Podejście 2: Tworzenie auxClass z atrybutu niestandardowego i skojarzyć z hello klasy obiektów**

1. Utwórz kopię szablonu katalogu Domino {PUBNAMES. NTF} wykonując [te kroki](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (Dostosowywanie nigdy nie hello IBM Lotus Domino katalogu szablonu):
2. Otwórz hello kopiowania Domino katalogu szablonu {CONTOSO. Szablon NTF}, który został utworzony w Projektancie Domino.
3. W okienku po lewej stronie powitania wybierz współużytkowanego kodu, a następnie podformularze.
4. Kliknij przycisk nowy podformularz
5. Witaj następujących właściwości hello toospecify dla nowego podformularza hello:
   * Nowy podformularz hello jest otwarty, wybierz projekt - podformularz właściwości
   * Dalej toohello właściwości Name, wprowadź nazwę dla klasy pomocnicze obiektów hello — na przykład TestSubform.
   * Zachowaj właściwości Options powitania "Dołącz podformularza Insert... okna dialogowego" wybrane
   * Anuluj wybór właściwości Options powitania "Renderowania przekazują HTML w notatkach".
   * Pozostaw hello innych hello takie same właściwości i zamknąć okno właściwości podformularza hello.
   * Zapisz i zamknij hello nowy podformularz.
6. Witaj następujących tooadd pola toodefine hello pomocnicze obiektu klasy:
   * Otwórz podformularz hello, który został utworzony.
   * Wybierz opcję Utwórz — pole.
   * TooName dalej na karcie podstawy hello powitalne okno dialogowe pola, określić dowolną nazwę, na przykład: {MyPersonTestAttribute}.
   * W polu dodano hello ustawienia swoich właściwości, wybierając typ, Style, rozmiar, czcionki i powiązanych właściwości.
   * Atrybut hello utrzymania wartością domyślną takie same jak nazwa hello podany dla tego atrybutu (na przykład, jeśli nazwa atrybutu jest MyPersonTestAttribute, należy zachować wartość domyślną hello z hello tej samej nazwy).
   * Zapisz podformularz hello z zaktualizowane wartości i hello następujące:
     * W okienku po lewej stronie powitania wybierz współużytkowanego kodu, a następnie podformularze
     * Wybierz nowy podformularz hello i wybierz projekt - właściwości projektu.
     * Kliknij kartę trzeci powitania od lewej hello, a następnie wybierz **propagację zakaz zmianę projektu**.
7. Otwórz podformularzu ExtensibleSchema ${ObjectName} ({ObjectName} określa hello nazwę klasy hello domyślnego obiektu strukturalnego, na przykład — osoby).
8. Wstaw zasób i wybierz hello podformularza (który został utworzony, na przykład — TestSubform) i Zapisz hello ${ObjectName} ExtensibleSchema podformularz.
9. Zastąp hello Domino katalogu szablonu {PUBNAMES. NTF} z hello nowe dostosowany szablon {CONTOSO. NTF} wykonując [te kroki](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
10. Zamknij Domino administratora i otwórz hello toorestart Domino konsoli usługi LDAP i hello tooReload schematu LDAP:
    * W konsoli Domino Wstaw polecenie hello w obszarze **polecenia Domino** tekst zachowano usługi LDAP hello toorestart — [Uruchom ponownie zadanie LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
    * polecenie tooreload LDAP schematu, poinformuj LDAP **Poinformuj ReloadSchema LDAP**.
11. Otwórz administratora Domino i wybierz toosee kartę osoby i grupy dodane atrybutu jest widoczny w domino Dodaj osobę (w obszarze innym tabulacji).
12. Otwórz Schema.nsf z **pliki** karcie i zobacz, dodane atrybuty jest odzwierciedlone w obszarze TestSubform LDAP pomocnicze klasy obiektów.

**Podejście 3: Dodaj hello atrybutu niestandardowego toohello ExtensibleObject klasy**

1. Otwórz plik {Schema.nsf} umieszczona w katalogu głównym hello
2. Wybierz klasy obiektu LDAP z menu po lewej stronie powitania w obszarze **wszystkie dokumenty schematu** i kliknij przycisk **Dodaj obiekt klasy** przycisk:
3. Podaj nazwę LDAP w hello formę {zzzExtensibleSchema} (gdzie zzz jest nazwą hello hello domyślną klasę obiektu strukturalnego, na przykład osoby). Na przykład tooextend hello schemat dla klasy obiektu osoby, podaj nazwę LDAP {PersonExtensibleSchema}.
4. Podaj nazwę klasy obiekt nadrzędny, dla której ma zostać tooextend hello schematu. Na przykład tooextend hello schemat dla klasy obiektu osoby, podaj nazwę klasy obiekt nadrzędny {dominoPerson}:
5. Podaj prawidłowy identyfikator OID odpowiedniego toohello obiektu klasy.
6. Wybierz atrybuty rozszerzone/niestandardowe w obszarze obowiązkowe i opcjonalne typy atrybutów pola zgodnie z harmonogramem hello wymaganie:
7. Po dodanie wymaganych atrybutów toohello ExtensibleObjectClass, kliknij przycisk **Zapisz i Zamknij**.
8. ExtensibleObjectClass jest tworzona dla odpowiednich domyślną klasę obiektu z rozszerzonymi atrybutami.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
* Aby informacji na temat sposobu rejestrowania tooenable tootroubleshoot hello łącznika, zobacz hello [jak tooEnable ETW Tracing łączników](http://go.microsoft.com/fwlink/?LinkId=335731).
