---
title: "aaaGeneric łącznik LDAP | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób ogólny łącznik LDAP tooconfigure firmy Microsoft."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>Ogólny łącznik LDAP informacje techniczne
W tym artykule opisano hello ogólny łącznik LDAP. Witaj artykuł dotyczy toohello następujące produkty:

* Program Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Należy użyć poprawki 4.1.3671.0 lub nowszym [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 i FIM2010R2 hello łącznika jest dostępna do pobrania z hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

Podczas odwoływania się RFC tooIETF, ten dokument jest przy użyciu formatu hello (RFC [numer RFC] / [sekcji w dokumencie RFC]), na przykład (RFC 4512/4.3).
Więcej informacji można znaleźć http://tools.ietf.org/html/rfc4500 (należy tooreplace 4500 hello poprawny numer RFC).

## <a name="overview-of-hello-generic-ldap-connector"></a>Omówienie hello ogólny łącznik LDAP
Witaj ogólny łącznik LDAP umożliwia możesz toointegrate hello usługi synchronizacji z serwerem LDAP w wersji 3.

Niektórych operacji i elementy schematu, takie jak te potrzebne tooperform import zmian, nie są określone w dokumentach RFC organizacji IETF hello. Do tych operacji są obsługiwane tylko katalogów LDAP jawnie określony.

Z punktu widzenia wysokiego poziomu hello następujące funkcje są obsługiwane przez hello bieżącej wersji łącznika hello:

| Funkcja | Pomoc techniczna |
| --- | --- |
| Połączonego źródła danych |Hello łącznika jest obsługiwana przez wszystkie serwery v3 LDAP (maksymalnie ze specyfikacją RFC 4510). Był testowany z następujących hello: <li>Usługi Microsoft Active Directory Lightweight Directory Services (AD LDS)</li><li>Wykaz globalny usługi Microsoft Active Directory (AD GC)</li><li>Serwer katalogowy 389</li><li>Serwer katalogowy Apache</li><li>IBM Tivoli DS</li><li>Isode katalogu</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Otwórz DJ</li><li>Otwórz DS</li><li>Otwórz LDAP (openldap.org)</li><li>Oracle (wcześniej Sun) Directory Server Enterprise Edition</li><li>RadiantOne serwera katalogu wirtualnego (VDS)</li><li>Jeden serwer katalogowy Sun</li>**Godne katalogi nie są obsługiwane:** <li>Microsoft Active Directory Domain Services (AD DS) [Użyj hello wbudowanego łącznika usługi Active Directory zamiast]</li><li>Oracle Internet katalogu (OID)</li> |
| Scenariusze |<li>Zarządzanie cyklem życia obiektów</li><li>Zarządzanie grupami</li><li>Zarządzanie hasłami</li> |
| Operacje |Witaj następujące operacje są obsługiwane we wszystkich katalogach LDAP: <li>Pełny Import</li><li>Eksportowanie</li>Witaj, po operacji są obsługiwane tylko w określonych katalogach:<li>Import zmian</li><li>Ustawianie hasła, Zmień hasło</li> |
| Schemat |<li>Wykryto schematu z hello LDAP schematu (RFC3673 i RFC4512/4.2)</li><li>Obsługuje klasy strukturalne, aux klas i klasy obiektów extensibleObject (RFC4512/4.3)</li> |

### <a name="delta-import-and-password-management-support"></a>Obsługa zarządzania import i hasło delta
Import zmian i zarządzanie hasłami obsługiwane katalogów:

* Usługi Microsoft Active Directory Lightweight Directory Services (AD LDS)
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawione hasło
* Wykaz globalny usługi Microsoft Active Directory (AD GC)
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawione hasło
* Serwer katalogowy 389
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawianie hasła i Zmień hasło
* Serwer katalogowy Apache
  * Nie obsługuje import zmian, ponieważ ten katalog nie ma dziennik trwałych zmian
  * Obsługuje ustawione hasło
* IBM Tivoli DS
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawianie hasła i Zmień hasło
* Isode katalogu
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawianie hasła i Zmień hasło
* Novell eDirectory i NetIQ eDirectory
  * Obsługuje operacje Add, Update i zmiana nazwy dla import zmian
  * Nie obsługuje operacji usuwania dla import zmian
  * Obsługuje ustawianie hasła i Zmień hasło
* Otwórz DJ
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawianie hasła i Zmień hasło
* Otwórz DS
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawianie hasła i Zmień hasło
* Otwórz LDAP (openldap.org)
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawione hasło
  * Nie obsługuje zmiany hasła
* Oracle (wcześniej Sun) Directory Server Enterprise Edition
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawianie hasła i Zmień hasło
* RadiantOne serwera katalogu wirtualnego (VDS)
  * Musi być używana wersja 7.1.1 lub nowszej
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawianie hasła i Zmień hasło
* Jeden serwer katalogowy Sun
  * Obsługuje wszystkie operacje w import zmian
  * Obsługuje ustawianie hasła i Zmień hasło

### <a name="prerequisites"></a>Wymagania wstępne
Przed użyciem hello łącznika, upewnij się, że masz następujące hello na powitania serwera synchronizacji:

* Framework Microsoft .NET 4.5.2 lub nowszej

### <a name="detecting-hello-ldap-server"></a>Wykrywanie powitania serwera LDAP
Hello łącznika, opiera się na różnych technik toodetect i zidentyfikować powitania serwera LDAP. używa łącznika Hello hello głównego elementu DSE, nazwa/wersja dostawcy, i sprawdza on hello schematu toofind unikatowych obiektów i atrybutów znane tooexist w niektórych serwerów LDAP. Te dane, jeśli znaleziono, jest używane toopre-wypełnić hello opcje konfiguracji w hello łącznika.

### <a name="connected-data-source-permissions"></a>Połączone uprawnienia źródła danych
tooperform importowanie i eksportowanie operacje na obiektach hello w hello połączonego katalogu, hello łącznika konto musi mieć odpowiednie uprawnienia. Łącznik Hello musi tooexport stanie toobe uprawnień zapisu i stanie tooimport toobe uprawnienia do odczytu. Uprawnienie konfiguracja jest wykonywana w ramach hello środowiska zarządzania programu sam katalog docelowy hello.

### <a name="ports-and-protocols"></a>Porty i protokoły
Łącznik Hello używa numeru portu hello określony w konfiguracji hello, która domyślnie jest 389 protokołu LDAP i 636 dla LDAPS.

Dla LDAPS należy użyć protokołu SSL 3.0 i TLS. Protokół SSL 2.0 nie jest obsługiwane i nie może zostać uaktywniony.

### <a name="required-controls-and-features"></a>Formanty wymagane i funkcje
Hello następujących LDAP formanty funkcji muszą być dostępne na serwerze LDAP hello toowork łącznika hello prawidłowo:  
`1.3.6.1.4.1.4203.1.5.3`Filtry PRAWDA/FAŁSZ

Filtr PRAWDA/FAŁSZ Hello często nie został zgłoszony jako obsługiwany przez katalogów LDAP i może pojawiać się na powitania **globalne strony** w obszarze **obowiązkowe funkcji nie znaleziono**. Jest używana toocreate **lub** filtrów kwerendy LDAP, na przykład podczas importowania wiele typów obiektów. Jeśli można zaimportować więcej niż jeden typ obiektu, serwer LDAP obsługuje tę funkcję.

Jeśli używasz katalogu gdzie to unikatowy identyfikator hello zakotwiczenia hello następujące również muszą być dostępne (Aby uzyskać więcej informacji, zobacz hello [Konfiguruj zakotwiczenia](#configure-anchors) sekcji):  
`1.3.6.1.4.1.4203.1.5.1`Wszystkie atrybuty operacyjne

Jeśli katalog hello ma więcej obiektów niż co mieści się w jednym wywołaniu toohello katalogu, następnie zaleca toouse stronicowania. Dla toowork stronicowania potrzebujesz jednego z hello następujące opcje:

**Opcja 1:**  
`1.2.840.113556.1.4.319`pagedResultsControl

**Opcja 2:**  
`2.16.840.1.113730.3.4.9`VLVControl  
`1.2.840.113556.1.4.473`SortControl

Jeśli obie te opcje są włączone w konfiguracji łącznika hello, pagedResultsControl jest używany.

`1.2.840.113556.1.4.417`ShowDeletedControl

ShowDeletedControl jest używany tylko z hello USNChanged delta importowanie metody toobe toosee można usunąć obiektów.

Łącznik Hello próbuje toodetect hello opcje obecne na powitania serwera. Jeśli nie można wykryć opcje hello, ostrzeżenie jest dostępne na stronie globalne hello we właściwościach łącznika hello. Nie wszystkie serwery LDAP występuje wszystkie formanty/funkcje obsługi i nawet, jeśli to ostrzeżenie jest obecny, hello łącznika może działać bez problemów.

### <a name="delta-import"></a>Import zmian
Import zmian jest dostępna tylko w przypadku, gdy wykryto katalogu pomocy technicznej. następujące metody Hello są obecnie używane:

* LDAP Accesslog. Zobacz [http://www.openldap.org/doc/admin24/overlays.html#Access rejestrowania](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* Wykaz zmian LDAP. Zobacz [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* Sygnatura czasowa. Dla eDirectory Novell/NetIQ hello łącznik używa ostatniego daty/godziny tooget utworzony i zaktualizowane obiekty. Novell/NetIQ eDirectory nie zawiera odpowiednika oznacza tooretrieve usunięte obiekty. Tę opcję można również zastosować, gdy żadnej innej metody importu zmian jest aktywna na powitania serwera LDAP. Ta opcja nie jest możliwe tooimport usunięte obiekty.
* USNChanged. Zobacz: [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>Nieobsługiwane
Witaj, następujące funkcje LDAP nie są obsługiwane:

* Odwołań LDAP między serwerami (RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>Utwórz nowy łącznik
tooCreate ogólny łącznik LDAP w **usługi synchronizacji** wybierz **agenta zarządzania** i **Utwórz**. Wybierz hello **ogólnego LDAP (Microsoft)** łącznika.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>Łączność
Na stronie łączność hello musisz określić informacje hello hosta, Port i powiązania. W zależności od tego, czy powiązanie jest wybrany, dodatkowe informacje mogą być podane w hello następujące sekcje.

![Łączność](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* Ustawienia limitu czasu połączenia Hello jest używana tylko dla pierwszego serwera toohello połączenia hello podczas wykrywania schematu hello.
* Jeśli powiązanie jest anonimowy, następnie ani nazwy użytkownika / hasło lub certyfikat są używane.
* Dla pozostałych powiązaniach wprowadź informacje albo w nazwę użytkownika / hasło lub wybierz certyfikat.
* Jeśli używasz tooauthenticate protokołu Kerberos, określ również hello obszaru/domeny hello użytkownika.

Witaj **atrybutu aliasy** pole tekstowe jest używany dla zdefiniowanej w schemacie hello ze składnią RFC4522 atrybutów. Te atrybuty nie mogą być wykryte podczas wykrywania schematu i hello łącznika wymaga pomocy tooidentify te atrybuty. Na przykład hello poniżej należy wprowadzić w hello atrybutu aliasy pole toocorrectly należy określić atrybut certyfikatu użytkownika hello jako atrybutu danych binarnych:

`userCertificate;binary`

Hello poniżej znajduje się przykład sposobu ta konfiguracja może wyglądać jak:

![Łączność](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

Wybierz hello **zawiera atrybuty operacyjne w schemacie** tooalso wyboru zawiera atrybuty utworzonych przez serwer hello. Obejmują one atrybuty, takie jak kiedy hello obiekt został utworzony i godzina ostatniej aktualizacji.

Wybierz **zawiera atrybuty extensible w schemacie** jeśli są używane obiekty rozszerzalne (RFC4512/4.3) i włączenie tej opcji umożliwia co toobe atrybutu używane na wszystkich obiektów. Wybranie tej opcji powoduje, że schemat hello bardzo duży, chyba że używa połączonego katalogu hello zalecenie to funkcja hello jest tookeep hello opcję niezaznaczoną.

### <a name="global-parameters"></a>Parametry globalne
Na stronie parametry globalne hello skonfiguruj dziennik zmian różnicowych toohello hello nazwa Wyróżniająca i dodatkowe funkcje LDAP. Strona Hello jest wstępnie wypełniony hello informacje udostępniane przez serwer LDAP hello.

![Łączność](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

Hello pierwsza sekcja zawiera informacje o powitania serwera, takie jak nazwa hello powitania serwera. Witaj łącznika sprawdza także, czy formanty obowiązkowe hello znajdują się w hello głównego elementu DSE. Jeśli te formanty nie są wyświetlane, ostrzeżenia. Niektóre katalogów LDAP nie listę wszystkich funkcji w hello głównego elementu DSE i możliwe, że łącznik działa bez problemów Witaj, nawet jeśli jest obecne ostrzeżenie.

Witaj **obsługiwane formanty** pola wyboru kontrolowanie zachowania hello w ramach pewnych operacji:

* Drzewo Usuń zaznaczone, hierarchii jest usuwane z jednego wywołania LDAP. Usuń drzewa niezaznaczoną łącznik hello jest delete cykliczne w razie potrzeby.
* Z wyników stronicowania zaznaczone hello łącznik działa stronicowanych importu z hello rozmiar określony na powitania Uruchom kroki.
* Witaj VLVControl i SortControl jest alternatywnych toohello pagedResultsControl tooread danych z katalogiem LDAP hello.
* Jeśli wszystkie trzy opcje (pagedResultsControl, VLVControl i SortControl) są wyłączone hello łącznik importuje następnie wszystkich obiektów w jednej operacji, która może się nie powieść, jeśli jest duża katalog.
* ShowDeletedControl jest używana tylko w przypadku, gdy Metoda importu Delta hello jest USNChanged.

Dziennik zmian Hello DN jest kontekst nazewnictwa hello używany przez dziennik zmian różnicowych hello, na przykład **cn = wykaz zmian**. Ta wartość musi być określona import zmian stanie toodo toobe.

Hello poniżej znajduje się lista dziennik zmian domyślnego DNs:

| Katalog | Dziennik zmian różnicowych |
| --- | --- |
| Microsoft AD LDS i AD GC |Wykrywane automatycznie. USNChanged. |
| Serwer katalogowy Apache |Nie jest dostępna. |
| Katalog 389 |Dziennik zmian. Domyślna wartość toouse: **cn = wykaz zmian** |
| IBM Tivoli DS |Dziennik zmian. Domyślna wartość toouse: **cn = wykaz zmian** |
| Isode katalogu |Dziennik zmian. Domyślna wartość toouse: **cn = wykaz zmian** |
| Novell/NetIQ eDirectory |Nie jest dostępna. Sygnatura czasowa. Hello łącznik używa ostatni zaktualizowano daty/godziny tooget dodane, a zaktualizowane rekordy. |
| Otwórz DJ/DS. |Dziennik zmian.  Domyślna wartość toouse: **cn = wykaz zmian** |
| Otwórz LDAP |Dziennik dostępu. Domyślna wartość toouse: **cn = accesslog** |
| Oracle DSEE |Dziennik zmian. Domyślna wartość toouse: **cn = wykaz zmian** |
| RadiantOne VDS |Katalog wirtualny. Zależy od hello tooVDS katalogu połączony. |
| Jeden serwer katalogowy Sun |Dziennik zmian. Domyślna wartość toouse: **cn = wykaz zmian** |

jest atrybut password Hello hello nazwę hello atrybutu hello łącznika musi być używane hasło hello tooset w operacji set hasła i zmiany hasła.
Ta wartość jest domyślnie ustawiona zbyt**userPassword** , ale można zmienić w razie potrzeby w określonym systemie LDAP.

Na liście dodatkowe partycje hello jest dodatkowe przestrzenie nazw możliwe tooadd nie są automatycznie wykrywane. Na przykład to ustawienie umożliwia kilka serwerów tworzą logicznej klastra, który należy zaimportować wszystkie na powitania tym samym czasie. Podobnie jak Active Directory może mieć wiele domen w jednym lesie, ale wszystkie domeny udostępnianie jeden schemat, powitalne sam można symulowane wprowadzając hello dodatkowe przestrzenie nazw w tym polu. Każdej przestrzeni nazw można importować z różnych serwerów i dalsze skonfigurowano na stronie powitania Konfiguruj partycje i hierarchie. Użyj klawiszy Ctrl + Enter tooget znakiem nowego wiersza.

### <a name="configure-provisioning-hierarchy"></a>Konfigurowanie hierarchii zastrzegania
Ta strona jest używane toomap hello DN składników, na przykład jednostki Organizacyjnej, toohello typu obiektu, który powinna być przygotowana, na przykład jednostka organizacyjna.

![Inicjowanie obsługi administracyjnej hierarchii](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

Konfigurując inicjowania obsługi administracyjnej hierarchii można skonfigurować tooautomatically łącznika hello tworzenia struktury w razie potrzeby. Na przykład, jeśli jest kontrolerem domeny przestrzeń nazw = contoso, dc = com i nowych cn obiektu Jan, ou = = Seattle, c = US, kontrolera domeny = contoso, dc = com jest udostępniony, a następnie hello łącznik można utworzyć obiektu typu kraju dla Stanów Zjednoczonych i organizationalUnit dla Seattle, jeśli te nie są już w katalogu hello.

### <a name="configure-partitions-and-hierarchies"></a>Konfiguruj partycje i hierarchie
Na stronie partycje i hierarchie hello, zaznacz wszystkie przestrzenie nazw z obiektami planujesz tooimport i eksportowanie.

![Partycje](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

Dla każdej przestrzeni nazw jest również możliwe tooconfigure ustawienia łączności, zastępujące wartości hello podane na ekranie łączności hello. Jeśli te wartości są puste wartości domyślnej tootheir, hello informacji z ekranu łączności hello jest używany.

Jest również możliwe tooselect które kontenery i jednostki organizacyjne hello importowanego i eksportowania do łącznika.

Podczas wyszukiwania odbywa się we wszystkich kontenerach hello partycji. W przypadkach, gdy istnieją dużą liczbę kontenerów to działanie prowadzi degradacji tooperformance.

>[!NOTE]
Począwszy od hello 2017 marca aktualizacji toohello ogólnego LDAP wyszukiwania łącznika można ograniczone w kontenerach hello wybrane tooonly zakresu. Można to zrobić, wybierając hello wyboru "Wyszukiwanie tylko w kontenerach wybranego" jak pokazano w poniższym obrazie hello.

![Wyszukiwanie tylko wybrane kontenerów](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>Konfiguruj zakotwiczenia
Ta strona ma zawsze wartość wstępnie skonfigurowane i nie można zmienić. W razie znalezienia dostawcy serwera hello zakotwiczenia hello może być wypełnione atrybutem niezmienne, na przykład hello identyfikator GUID obiektu. Jeśli nie wykryto lub jest on znany toonot atrybutem niezmienne, a następnie hello łącznik używa nazwy domeny (nazwa wyróżniająca) jako swojej kotwicy hello.

![punkty kontrolne](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


Witaj poniżej przedstawiono listę serwerów LDAP i zakotwiczenia hello używany:

| Katalog | Atrybut zakotwiczenia |
| --- | --- |
| Microsoft AD LDS i AD GC |Atrybut objectGUID |
| Serwer katalogowy 389 |Nazwa wyróżniająca |
| Apache katalogu |Nazwa wyróżniająca |
| IBM Tivoli DS |Nazwa wyróżniająca |
| Isode katalogu |Nazwa wyróżniająca |
| Novell/NetIQ eDirectory |IDENTYFIKATOR GUID |
| Otwórz DJ/DS. |Nazwa wyróżniająca |
| Otwórz LDAP |Nazwa wyróżniająca |
| Oracle ODSEE |Nazwa wyróżniająca |
| RadiantOne VDS |Nazwa wyróżniająca |
| Jeden serwer katalogowy Sun |Nazwa wyróżniająca |

## <a name="other-notes"></a>Inne uwagi
Ta sekcja zawiera informacje o aspektach, które są określone toothis łącznik lub z innych powodów tooknow ważne.

### <a name="delta-import"></a>Import zmian
znak wodny delta Hello w otwartych LDAP jest UTC daty/godziny. Z tego powodu należy zsynchronizować zegary hello między usługę synchronizacji programu FIM a hello Otwórz LDAP. Jeśli nie może zostać pominięte niektóre wpisy w dzienniku zmian różnicowych hello.

Dla Novell eDirectory hello import zmian nie wykrywa usunięcia żadnych obiektów. Z tego powodu konieczne jest toorun pełne importowanie okresowo toofind wszystkie usunięte obiekty.

Katalogi z różnicowej zmian dziennika, który jest oparty na daty/godziny, jest zdecydowanie zalecane toorun pełny import w czasie okresowe. Ten proces umożliwia toofind aparatu synchronizacji hello i nierówności pomiędzy powitania serwera LDAP i co to jest aktualnie hello przestrzeni łącznika.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
* Aby informacji na temat sposobu rejestrowania tooenable tootroubleshoot hello łącznika, zobacz hello [jak tooEnable ETW Tracing łączników](http://go.microsoft.com/fwlink/?LinkId=335731).
