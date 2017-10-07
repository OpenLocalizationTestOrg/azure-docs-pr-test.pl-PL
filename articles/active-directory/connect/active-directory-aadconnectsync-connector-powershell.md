---
title: "aaaPowerShell łącznik | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób łącznik usługi tooconfigure Microsoft Windows PowerShell."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Informacje techniczne dotyczące łącznika usługi Windows PowerShell
W tym artykule opisano hello łącznik usługi Windows PowerShell. Witaj artykuł dotyczy toohello następujące produkty:

* Program Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Należy użyć poprawki 4.1.3671.0 lub nowszym [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 i FIM2010R2 hello łącznika jest dostępna do pobrania z hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-powershell-connector"></a>Omówienie hello łącznika programu PowerShell
Hello łącznika programu PowerShell włącza usługę synchronizacji hello toointegrate z systemami zewnętrznymi, które oferują środowiska Windows PowerShell na podstawie interfejsów API. Łącznik Hello zapewnia mostka między hello możliwości agenta zarządzania na podstawie rozmów extensible łączności hello 2 framework (ECMA2) i programu Windows PowerShell. Aby uzyskać więcej informacji na temat hello ECMA framework, zobacz hello [Extensible odwołanie agenta zarządzania 2.2 łączności](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx).

### <a name="prerequisites"></a>Wymagania wstępne
Przed użyciem hello łącznika, upewnij się, że masz następujące hello na powitania serwera synchronizacji:

* Framework Microsoft .NET 4.5.2 lub nowszej
* Program Windows PowerShell 2.0, 3.0 lub 4.0

zasady wykonywania Hello na powitania serwera usługi synchronizacji musi być skryptów programu Windows PowerShell toorun tooallow skonfigurowanych hello łącznika. O ile nie są podpisane cyfrowo hello skrypty hello łącznik działa, należy skonfigurować zasady wykonywania hello, uruchamiając polecenie:  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>Utwórz nowy łącznik
toocreate łącznika programu Windows PowerShell w usłudze synchronizacji hello, musisz podać szereg skryptów programu Windows PowerShell, których wykonanie czynności hello żądanej przez usługę synchronizacji hello. W zależności od źródła danych hello połączyć tooand hello funkcje, które są wymagane skrypty hello, którą musi implementować zależy. W tej części opisano poszczególne skrypty hello może być zaimplementowany oraz gdy są one wymagane.

Witaj środowiska Windows PowerShell jest łącznik przeznaczony toostore skryptów hello wewnątrz bazy danych usługi synchronizacji hello. Mimo że jest możliwe toorun skrypty, które są przechowywane w systemie plików hello, jest łatwiejsze treści hello tooinsert każdego skryptu bezpośrednio w konfiguracji łącznika toohello.

tooCreate łącznika programu PowerShell w **usługi synchronizacji** wybierz **agenta zarządzania** i **Utwórz**. Wybierz hello **środowiska PowerShell (Microsoft)** łącznika.

![Tworzenie łącznika](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>Łączność
Podaj parametry konfiguracji podłączania tooa systemu zdalnego. Te wartości są bezpiecznie przechowywane przez hello usługi synchronizacji i wprowadzone skryptów programu Windows PowerShell tooyour dostępne po uruchomieniu hello łącznika.

![Łączność](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

Można skonfigurować hello następujące parametry połączenia:

**Łączność**

| Parametr | Wartość domyślna | Przeznaczenie |
| --- | --- | --- |
| Serwer |<Blank> |Nazwa serwera, który hello łącznika ma nawiązać. |
| Domeny |<Blank> |Domena hello toostore poświadczenia do użycia po uruchomieniu hello łącznika. |
| Użytkownik |<Blank> |Nazwa hello toostore poświadczenia do użycia po uruchomieniu hello łącznika. |
| Hasło |<Blank> |Hasło hello toostore poświadczenia do użycia po uruchomieniu hello łącznika. |
| Personifikuj konto łącznika |False |W przypadku wartości PRAWDA Usługa synchronizacji hello działa hello skryptów programu Windows PowerShell w kontekście hello dostarczone poświadczenia hello. Jeśli to możliwe, zaleca się tym hello **$Credentials** parametr jest przekazywany tooeach skryptu jest używany zamiast personifikacji. Aby uzyskać więcej informacji na temat dodatkowe uprawnienia, które są wymagane toouse tej opcji, zobacz [dodatkowej konfiguracji personifikacji](#additional-configuration-for-impersonation). |
| Załaduj profil użytkownika, gdy personifikacji |False |Powoduje, że profil użytkownika hello tooload Windows hello łącznika poświadczeń podczas personifikacji. Jeśli hello personifikowanego użytkownika ma mobilny profil, łącznik hello nie załadować hello profilu mobilnego. Aby uzyskać więcej informacji na temat dodatkowe uprawnienia, które są wymagane toouse tego parametru, zobacz [dodatkowej konfiguracji personifikacji](#additional-configuration-for-impersonation). |
| Typ logowania, gdy personifikacji |Brak |Typ logowania podczas personifikacji. Aby uzyskać więcej informacji, zobacz hello [dwLogonType] [ dw] dokumentacji. |
| Tylko skrypty podpisane |False |Jeśli PRAWDA, łącznik programu Windows PowerShell hello sprawdza, czy każdy skrypt ma nieprawidłowy podpis cyfrowy. W przypadku wartości FAŁSZ, upewnij się, że zasady wykonywania programu Windows PowerShell hello Usługa synchronizacji serwera jest RemoteSigned lub bez ograniczeń. |

**Typowe modułu**  
Łącznik Hello umożliwia toostore udostępnionego moduł programu Windows PowerShell w konfiguracji hello. Po uruchomieniu skryptu łącznika hello hello jest moduł programu Windows PowerShell wyodrębnić toohello systemu plików, aby można było importować przez każdego skryptu.

Skryptów importu, eksportu i synchronizacja haseł wspólnego modułu hello jest folder MAData wyodrębnionego toohello łącznika. Schematu, sprawdzanie poprawności hierarchii i partycji skryptów odnajdywania hello wspólnego modułu jest folderu wyodrębnionego toohello % TEMP %. W obu przypadkach hello wyodrębnić wspólnego modułu skryptu o nazwie zgodnie z toohello ustawienie Nazwa pospolita skryptu modułu.

tooload modułu o nazwie FIMPowerShellConnectorModule.psm1 z folderu MAData hello, użyj następującej instrukcji hello:`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

tooload modułu o nazwie FIMPowerShellConnectorModule.psm1 z folderu % TEMP % hello, użyj następującej instrukcji hello:`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**Sprawdzanie poprawności parametru**  
Skrypt do weryfikowania Hello jest opcjonalny skrypt programu Windows PowerShell, które mogą być używane tooensure, że parametry konfiguracji łącznika dostarczane przez administratora hello są prawidłowe. Sprawdzania poprawności serwera, poświadczenia połączenia i parametry połączenia są typowe zastosowania skrypt do weryfikowania hello. Witaj skrypt do weryfikowania jest wywoływana po hello następujące karty i okna dialogowe zostaną zmodyfikowane:

* Łączność
* Parametry globalne
* Partycja konfiguracji

skrypt do weryfikowania Hello otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |Karta Konfiguracja Hello lub okna dialogowego, która wyzwoliła hello sprawdzania poprawności żądania. |
| ConfigParameters |[KeyedCollection] [ keyk] [ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |

skrypt do weryfikowania Hello powinien zwrócić pojedynczy potok toohello ParameterValidationResult obiektu.

**Odnajdywanie schematu**  
Witaj skrypt wykrywania schematu jest obowiązkowe. Ten skrypt zwraca hello typy obiektów i atrybuty atrybut ograniczenia tego hello używanych przez usługę synchronizacji podczas konfigurowania reguły przepływu atrybutu. Hello skrypt wykrywania schematu jest uruchamiany podczas tworzenia łącznika i wypełnia schematu hello łącznika. Jest on również używany przez hello akcji Odśwież schemat w hello Synchronization Service Manager.

skrypt wykrywania schematu Hello otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection] [ keyk] [ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |

skrypt Hello musi zwracać jedną [schematu] [ schema] obiektu toohello potoku. obiekt schematu Hello składa się z [elementu SchemaType] [ schemaT] obiektów, które reprezentują typy obiektów (na przykład: użytkowników i grup). Obiekt elementu SchemaType Hello przetrzymuje kolekcję [SchemaAttribute] [ schemaA] obiekty reprezentujące hello atrybutów (na przykład: imię, nazwisko i adres pocztowy) hello typu.

**Dodatkowe parametry**  
Ponadto toohello standardowych ustawień konfiguracji, można zdefiniować dodatkowe niestandardowych ustawień konfiguracji znajdujących się na wystąpienie określonego toohello hello łącznika. Te parametry można określić na powitania łącznika, partycji, lub wykonywania kroku poziomy i dostępne w hello odpowiedni skrypt programu Windows PowerShell. Ustawienia konfiguracji niestandardowej mogą być przechowywane w bazie danych usługi synchronizacji hello w formacie zwykłego tekstu lub może być zaszyfrowany. Witaj usługi synchronizacji automatycznie szyfruje i odszyfrowuje ustawienia konfiguracji bezpiecznego, gdy jest to wymagane.

toospecify niestandardowych ustawień konfiguracji, oddzielne hello nazwę każdego parametru za pomocą przecinka (,).

tooaccess niestandardowych ustawień konfiguracji ze skryptu, musi sufiks nazwy powitania od znaku podkreślenia ( \_ ) i zakresu hello parametru hello (Global, partycji lub RunStep). Na przykład tooaccess hello parametrów globalnych, użyj następujący fragment kodu:`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>Możliwości
hello projektanta agenta zarządzania na karcie możliwości Hello definiuje zachowanie hello i funkcjonalność hello łącznika. Nie można zmodyfikować Hello wybrane na tej karcie, gdy hello łącznik został utworzony. Ta tabela zawiera listę ustawień możliwości hello.

![Możliwości](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| Możliwości | Opis |
| --- | --- |
| [Styl nazwy wyróżniającej][dnstyle] |Wskazuje, jeśli łącznik hello obsługuje nazwy wyróżniającej i jeśli tak, jakie stylu. |
| [Typ eksportu][exportT] |Określa typ hello obiektów, które są przedstawiane toohello skrypt eksportu. <li>AttributeReplace — obejmuje pełny zestaw wartości dla atrybutu wielowartościowego powitania po zmianie atrybutów hello.</li><li>AttributeUpdate — obejmuje tylko hello delty tooa atrybutów wielowartościowych po zmianie hello atrybutu.</li><li>MultivaluedReferenceAttributeUpdate — zawiera pełen zestaw wartości dla atrybutów wielowartościowych-reference i delty tylko dla atrybutów wielowartościowych odwołania.</li><li>ObjectReplace — zawiera wszystkie atrybuty obiektu, gdy dowolne zmiany atrybutów</li> |
| [Normalizacji danych][DataNorm] |Powoduje, że atrybuty zakotwiczenia toonormalize usługi synchronizacji hello przed tooscripts są udostępniane. |
| [Potwierdzenie obiektu][oconf] |Konfiguruje hello oczekującego procesu importowania w hello usługi synchronizacji. <li>Normalny — domyślne zachowanie, która oczekuje eksportowane wszystkie zmiany toobe potwierdzone przez import</li><li>NoDeleteConfirmation — obiekt jest usunięty, nie ma żadnych oczekującego importowania wygenerowany.</li><li>NoAddAndDeleteConfirmation — obiekt jest tworzony lub usunięty, nie ma żadnych oczekującego importowania wygenerowany.</li> |
| Użyj nazwy domeny jako swojej kotwicy |Jeśli hello styl nazwa wyróżniająca ustawiono tooLDAP, atrybut zakotwiczenia hello przestrzeni łącznika hello jest również hello nazwy wyróżniającej. |
| Równoczesne wykonywanie operacji kilka łączników |Po zaznaczeniu tej opcji, jednocześnie uruchomić wiele łączników programu Windows PowerShell. |
| Partycje |Po zaznaczeniu tej opcji, hello łącznik obsługuje wiele partycji i odnajdywania partycji. |
| Hierarchii |Po zaznaczeniu tej opcji, hello łącznik obsługuje strukturę hierarchiczną styl LDAP. |
| Włącz importu |Po zaznaczeniu tej opcji, hello łącznik importuje dane za pomocą skryptów importu. |
| Włącz Import zmian |Po zaznaczeniu tej opcji, hello łącznika może prosić o delty z hello importowania skryptów. |
| Włącz eksportu |Po zaznaczeniu tej opcji, łącznik hello eksportuje danych za pomocą skryptów eksportu. |
| Włącz pełną eksportu |Po zaznaczeniu tej opcji, hello wyeksportować eksportowania przestrzeni łącznika całego hello obsługi skryptów. toouse, który również należy sprawdzić tej opcji, należy włączyć eksportowanie. |
| Brak wartości odwołania w pierwszej eksportu — dostęp próbny |Po zaznaczeniu tej opcji, atrybutów odwołania są eksportowane w drugim przebiegu eksportu. |
| Włącz zmiany nazwy obiektu |Po zaznaczeniu tej opcji, można zmodyfikować nazwy wyróżniającej. |
| Usuń Dodaj zastępowania |Po zaznaczeniu tej opcji, Usuń — Dodaj operacje są eksportowane jako jednego zastąpienia. |
| Włącz operacje na hasłach |Po zaznaczeniu tej opcji, skrypty synchronizacji hasła są obsługiwane. |
| Włącz hasło eksportu w pierwszej — dostęp próbny |Po zaznaczeniu tej opcji, eksportowane są hasła ustawione podczas inicjowania obsługi, gdy tworzony jest obiekt hello. |

### <a name="global-parameters"></a>Parametry globalne
Karta parametry globalne Hello w hello projektanta agenta zarządzania umożliwia skryptów programu Windows PowerShell hello tooconfigure, które są uruchamiane przez łącznik hello. Można również skonfigurować globalne wartości ustawień konfiguracji niestandardowej zdefiniowane na karcie Połączenie hello.

**Odnajdywanie partycji**  
Partycja to oddzielne przestrzeni nazw w obrębie jednego udostępnionego schematu. W każdej domenie, na przykład w usłudze Active Directory jest partycji w obrębie jednego lasu. Partycja to logiczne grupowanie hello importu i eksportu operacji. Importowanie i eksportowanie mieć partycji, które kontekst i wszystkie operacje odbywa się w tym kontekście. Partycje są powinien toorepresent hierarchii w protokole LDAP. Nazwa wyróżniająca Hello partycji jest używany podczas importowania tooverify wszystkie zwracane obiekty są w zakresie hello partycji. Nazwa wyróżniająca partycji Hello również jest używany podczas inicjowania obsługi administracyjnej z hello metaverse toohello łącznika miejsca toodetermine hello partycji obiektu musi być skojarzony z podczas eksportowania.

skrypt wykrywania partycji Hello otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |

Hello skryptu musi zwracać jedną [partycji] [ part] obiektu lub listy [T] potoku toohello obiektów partycji.

**Odnajdowanie hierarchii**  
skrypt odnajdowania hierarchii Hello jest używana tylko w przypadku hello możliwości styl nazwę wyróżniającą LDAP. skrypt Hello jest używane tooallow możesz toobrowse i wybierz zestaw kontenerów, który jest uznawany za w lub poza zakres importowania i eksportowania operacji. skrypt Hello powinien dostarczać wyłącznie listę węzłów, które są bezpośrednimi elementami podrzędnymi skryptu toohello Podany węzeł główny hello.

skrypt odnajdowania hierarchii Hello otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |
| ParentNode |[HierarchyNode][hn] |węzeł główny Hello hello hierarchii, w których hello skrypt powinien zwrócić bezpośrednich działań podrzędnych. |

skrypt Hello musi zwracać albo obiekt HierarchyNode pojedynczy element potomny lub listy [T] podrzędnych HierarchyNode obiektów toohello potoku.

#### <a name="import"></a>Import
Łączniki, które obsługują operacji importowania musi implementować trzy skryptów.

**Rozpocznij importu**  
Witaj rozpocząć importu skrypt jest uruchamiany na początku hello kroku importu Uruchom. W tym kroku można ustanowić połączenia toohello źródłowy system i wykonaj czynności przygotowawcze przed importowania danych z hello połączony system.

Witaj rozpocząć importu skrypt otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informuje o hello skryptu o typie hello importu Uruchom (delta lub pełne), partycji, hierarchii, znaku wodnego i oczekiwany rozmiar. |
| Typy |[Schemat][schema] |Schemat dla hello przestrzeni łącznika, który jest importowany. |

skrypt Hello musi zwracać jedną [OpenImportConnectionResults] [ oicres] obiekt toohello potoku, na przykład:`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**Importowanie danych**  
Hello importu danych skryptu jest wywoływana przez łącznik hello, dopóki skryptu hello wskazuje, czy jest nie więcej tooimport danych. Łącznik programu Windows PowerShell Hello ma rozmiar strony 9999 obiektów. Jeśli skrypt zwraca więcej niż 9999 obiekty do importu, musi obsługiwać stronicowania. ujawnia łącznika Hello, gdy właściwość danych niestandardowych, można użyć magazynu tooa znaku wodnego, aby każdy hello czas importowania danych skryptu zostanie wywołana, skrypt zostanie wznowione Importowanie obiektów, w którym przerwał.

Hello importu danych skryptu otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |Blokad hello znaku wodnego (CustomData) mogą być używane podczas importów stronicowana i importuje delta. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informuje o hello skryptu o typie hello importu Uruchom (delta lub pełne), partycji, hierarchii, znaku wodnego i oczekiwany rozmiar. |
| Typy |[Schemat][schema] |Schemat dla hello przestrzeni łącznika, który jest importowany. |

Witaj skryptu importu danych musi być zapisana listy [[CSEntryChange][csec]] obiektu toohello potoku. Ta kolekcja składa się z CSEntryChange atrybuty, które reprezentują każdy obiekt importowany. Podczas wykonywania pełnego importu tej kolekcji ma pełny zestaw CSEntryChange obiektów, które mają wszystkie atrybuty dla każdego obiektu. Podczas importowania różnicowych hello CSEntryChange obiektu albo powinien zawierać hello atrybut poziomu delty dla każdego obiektu tooimport lub pełną reprezentację hello obiektów, które zostały zmienione (tryb Zastąp).

**Importuj zakończenia**  
Po zakończeniu hello importu hello Uruchom hello zakończenia importowania skrypt jest uruchamiany. Ten skrypt należy wykonać wszystkie zadania czyszczenia niezbędne (na przykład, zamknij połączeń toosystems i odpowiedź toofailures).

skryptu importu zakończenia Hello otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informuje o hello skryptu o typie hello importu Uruchom (delta lub pełne), partycji, hierarchii, znaku wodnego i oczekiwany rozmiar. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Informuje o skryptu hello o przyczynie hello, który hello importowania została zakończona. |

skrypt Hello musi zwracać jedną [CloseImportConnectionResults] [ cicres] obiekt toohello potoku, na przykład:`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>Eksportowanie
Architektura importu identyczne toohello hello łącznika, łączniki, które obsługują eksportu musi implementować trzy skryptów.

**Rozpoczęcie eksportu**  
Witaj rozpocząć eksport skrypt jest uruchamiany na początku hello kroku uruchamiania eksportu. W tym kroku można ustanowić połączenia toohello źródła system i przeprowadzanie żadnych czynności przygotowawczych, przed eksportowanie danych toohello połączony system.

Witaj rozpocząć eksport skrypt otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informuje o hello skryptu o typie hello uruchamiania eksportu (delta lub pełne), partycji, hierarchii i oczekiwany rozmiar. |
| Typy |[Schemat][schema] |Schemat dla hello przestrzeni łącznika, który został wyeksportowany. |

Witaj skryptu nie może zwracać żadnych danych wyjściowych toohello potoku.

**Eksportowanie danych**  
Hello usługi synchronizacji wywołuje skrypt eksportowanie danych hello tyle razy, ile jest to konieczne tooprocess wszystkie oczekujące operacje eksportowania. Jeśli przestrzeni łącznika hello ma więcej oczekujące operacje eksportowania niż rozmiar strony łącznika Witaj, hello eksportu hello danych skryptu można wywoływać wielokrotnie i prawdopodobnie wiele razy dla tego samego obiektu.

skrypt danych eksportu Hello otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |
| CSEntries |IList[CSEntryChange][csec] |Lista wszystkich przestrzeni łącznika hello obiekty z oczekujących toobe eksportuje przetworzonych w trakcie tego przebiegu. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informuje o hello skryptu o typie hello uruchamiania eksportu (delta lub pełne), partycji, hierarchii i oczekiwany rozmiar. |
| Typy |[Schemat][schema] |Schemat dla hello przestrzeni łącznika, który został wyeksportowany. |

Witaj skrypt eksportu danych musi zwracać [PutExportEntriesResults] [ peeres] obiektu toohello potoku. Ten obiekt nie tooinclude wynik informacje potrzebne dla każdego wyeksportowanego łącznika, chyba że wystąpi błąd lub atrybutem zakotwiczenia toohello zmiany. Na przykład tooreturn PutExportEntriesResults obiektu toohello potoku:`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**Końcowy eksportu**  
Po zakończeniu hello eksportu hello Uruchom, hello toorun skryptu zakończenia eksportowania. Ten skrypt należy wykonać wszystkie zadania czyszczenia niezbędne (na przykład, zamknij połączeń toosystems i odpowiedź toofailures).

skrypt eksportu zakończenia Hello otrzymuje następujące parametry z łącznika hello hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informuje o hello skryptu o typie hello uruchamiania eksportu (delta lub pełne), partycji, hierarchii i oczekiwany rozmiar. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Informuje o skryptu hello o przyczynie hello, który hello eksport został zakończony. |

Witaj skryptu nie może zwracać żadnych danych wyjściowych toohello potoku.

#### <a name="password-synchronization"></a>Synchronizacja haseł
Łączniki programu Windows PowerShell może służyć jako miejsce docelowe dotyczących resetowania zmiany hasła.

skrypt hasła Hello otrzymuje hello poniższych parametrów z łącznika hello:

| Nazwa | Typ danych | Opis |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][ciągu [ConfigParameter][cp]] |Tabela parametry konfiguracji hello łącznika. |
| Poświadczenie |[PSCredential][pscred] |Zawiera wszystkie podane przez administratora hello na karcie Połączenie hello poświadczenia. |
| Partycja |[Partycji][part] |Witaj CSEntry partycji katalogu jest. |
| CSEntry |[CSEntry][cse] |Wpis obszaru łącznika dla obiekt hello otrzymał zmiany hasła lub zresetować. |
| Typ operacji |Ciąg |Wskazuje, czy operacja hello jest zresetowanie (**UstawianieHasła**) lub zmiany (**Element ChangePassword**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Flagi określające hello przeznaczone zachowanie resetowania hasła. Ten parametr jest dostępna tylko jeśli jest OperationType **UstawianieHasła**. |
| Stare_hasło |Ciąg |Wypełniane przy użyciu obiektu hello stare hasło do zmiany hasła. Ten parametr jest dostępna tylko jeśli jest OperationType **Element ChangePassword**. |
| NoweHasło |Ciąg |Wypełniane przy użyciu obiektu hello nowe hasło, które należy ustawić hello skryptu. |

Witaj skryptu hasła jest tooreturn nie oczekiwano żadnych potoku środowiska Windows PowerShell toohello wyników. Jeśli wystąpi błąd w skrypcie hasła hello, skrypt hello powinien zgłosić jedną hello następujące wyjątki tooinform hello usługi synchronizacji o problemie hello:

* [PasswordPolicyViolationException] [ pwdex1] — element zgłaszany, gdy hello hasło nie spełnia zasad haseł hello w systemie hello połączony.
* [PasswordIllFormedException] [ pwdex2] — wygenerowany, jeśli hasło hello nie jest możliwa do hello połączony system.
* [PasswordExtension] [ pwdex3] — wyjątek dla wszystkich błędów w skrypcie hasła hello.

## <a name="sample-connectors"></a>Łączniki próbki
Pełne omówienie hello próbki dostępnych łączników, zobacz [Windows PowerShell łącznika próbki łącznika kolekcji][samp].

## <a name="other-notes"></a>Inne uwagi
### <a name="additional-configuration-for-impersonation"></a>Dodatkowe konfiguracje dla personifikacji
Przyznaj hello użytkownika, który jest personifikowanej hello następujące uprawnienia na serwerze usługi synchronizacji hello:

Dostęp do odczytu toohello następujące klucze rejestru:

* HKEY_USERS\\\Software\Microsoft\PowerShell [SynchronizationServiceServiceAccountSID]
* HKEY_USERS\\\Environment [SynchronizationServiceServiceAccountSID]

Witaj toodetermine identyfikator zabezpieczeń (SID) konta usługi synchronizacji usługi hello, uruchom następujące polecenia programu PowerShell hello:

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

Dostęp do odczytu toohello po folderów systemu plików:

* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft forefront Identity Manager\2010\Synchronization Service\MaData\\{łącznik}

Zastąp symbol zastępczy {łącznik} hello hello nazwę łącznika programu Windows PowerShell hello.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
* Aby informacji na temat sposobu rejestrowania tooenable tootroubleshoot hello łącznika, zobacz hello [jak tooEnable ETW Tracing łączników](http://go.microsoft.com/fwlink/?LinkId=335731).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
