---
title: aaaConnector Historia wersji | Dokumentacja firmy Microsoft
description: "W tym temacie wymieniono wszystkie wersje hello łączników dla programu Forefront Identity Manager (FIM) i Microsoft Identity Manager (MIM)"
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a>Historia wersji łącznika
Witaj łączników programu Forefront Identity Manager (FIM) i Microsoft Identity Manager (MIM) są często aktualizowane.

> [!NOTE]
> Ten temat dotyczy tylko programu FIM i MIM. Te łączniki nie są obsługiwane dla instalacji na Azure AD Connect. Łączniki wydanej jest preinstalowany na AADConnect podczas uaktualniania toospecified kompilacji.

Ten temat zawiera wszystkie wersje hello łączniki, które zostały wydane.

Linki pokrewne:

* [Pobierz najnowsze łączników](http://go.microsoft.com/fwlink/?LinkId=717495)
* [Ogólny łącznik LDAP](active-directory-aadconnectsync-connector-genericldap.md) odwołania dokumentacji
* [Ogólny Łącznik usług SQL](active-directory-aadconnectsync-connector-genericsql.md) odwołania dokumentacji
* [Łącznik usług Web](http://go.microsoft.com/fwlink/?LinkID=226245) odwołania dokumentacji
* [Łącznik programu PowerShell](active-directory-aadconnectsync-connector-powershell.md) odwołania dokumentacji
* [Łącznika programu Lotus Domino](active-directory-aadconnectsync-connector-domino.md) odwołania dokumentacji


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0 (AADConnect do czasu zwolnienia)


### <a name="fixed-issues"></a>Rozwiązane problemy:

* Usługi sieci Web ogólne:
  * Rozwiązano problem uniemożliwia tworzone podczas wystąpiły co najmniej dwa punkty końcowe projektu protokołu SOAP.
* Ogólny SQL:
  * W operacji hello importu hello GSQL został nie konwertowania czasu poprawnie, po zapisaniu tooconnector miejsca. Witaj domyślny format daty i godziny dla przestrzeni łącznika hello GSQL został zmieniony z "RRRR MM-dd: ssZ" too'yyyy-MM-dd: ssZ ".

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>Rozwiązane problemy:

* Usługi sieci Web ogólne:
  * Narzędzie Wsconfig Hello nie zostały przekonwertowane poprawnie hello tablicy Json z "przykładowe żądanie" dla metody usługi REST hello. Przyczyną problemów z serializacji tej tablicy Json dla żądania REST hello.
  * Narzędzie konfiguracji łącznika usług sieci Web nie obsługuje użycia miejsca symboli w nazwach atrybutów JSON 
    * Wzorzec podstawienia mogą być dodawane ręcznie toohello WSConfigTool.exe.config pliku, np.```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Program Lotus Notes:
  * Gdy hello opcja **Zezwalaj na niestandardowe wydających świadectwa dla jednostki organizacyjnej/organizacji** jest wyłączona, a następnie hello łącznika kończy się niepowodzeniem podczas eksportu (aktualizacji), po eksportu hello przepływu wszystkie atrybuty są tooDomino wyeksportowany, ale w czasie hello Eksport KeyNotFoundException jest zwracana tooSync. 
    * Zdarza się to hello zmienić operacja kończy się niepowodzeniem podczas próby toochange nazwa Wyróżniająca (atrybut nazwy użytkownika), zmieniając jeden z atrybutów hello poniżej:  
      - Nazwisko
      - Imię
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - jednostki organizacyjnej
      - altcommonname

  * Gdy **Zezwalaj na niestandardowe wydających świadectwa dla jednostki organizacyjnej/organizacji** opcja jest włączona, ale wydających świadectwa wymagane są nadal puste, a następnie KeyNotFoundException występuje.

### <a name="enhancements"></a>Ulepszenia:

* Ogólny SQL:
  * **Scenariusz: przeprojektowany implementowany:** "*" funkcji
  * **Opis rozwiązania:** zmienić podejście do [Obsługa atrybuty wielowartościowe odwołanie](active-directory-aadconnectsync-connector-genericsql.md).


### <a name="fixed-issues"></a>Rozwiązane problemy:

* Usługi sieci Web ogólne:
  * Nie można zaimportować konfigurację serwera, jeśli znajduje się łącznik usługi sieci Web
  * Łącznik usługi sieci Web nie działa z wieloma usługami sieci Web

* Ogólny SQL:
  * Brak typów obiektu są wyświetlane pojedynczą wartość atrybutu do którego istnieje odwołanie
  * Import zmian śledzenia zmian wartość zostanie usunięty z tabeli wielowartościowych obiektu usuwa strategii
  * Overflowexception — w łączniku GSQL z bazy danych DB2 na AS / 400

Program Lotus:
  * Dodano opcję tooenable\disable wyszukiwanie jednostki organizacyjne przed otwarciem GlobalParameters strony

## <a name="114430"></a>1.1.443.0

Wydanie: 2017 marca

### <a name="enhancements"></a>Ulepszenia

* Ogólny SQL:</br>
  **Scenariusz symptomy:** jest dobrze znane ograniczenie z hello łącznik SQL, w którym możemy tylko Zezwalaj typu obiektu tooone odwołania i wymagają odwołań z elementami członkowskimi. </br>
  **Opis rozwiązania:** w kroku przetwarzania hello odwołań "*" zostanie wybrana opcja, wszystkich kombinacji typów obiektów, zostanie zwrócony wstecz toohello aparatu synchronizacji.

>[!Important]
- Spowoduje to utworzenie wielu symboli zastępczych
- Jest wymagane toomake się, że nazewnictwa hello jest unikatowa między typami obiektów.


* Ogólny LDAP:</br>
 **Scenariusz:** po wybraniu kilku kontenerów w określonej partycji, następnie wyszukiwania hello nadal będzie realizowane w całej partycji. Właściwe będą filtrowane przez usługę synchronizacji, ale nie MA, co może spowodować obniżenie wydajności. </br>

 **Opis rozwiązania:** łącznik GLDAP zmienić kod toomake możliwe przechodzi przez wszystkie kontenery i wyszukiwania obiektów w każdej z nich, zamiast wyszukiwanie w całej partycji hello.


* Programu Lotus Domino:

  **Scenariusz:** Domino poczty usunięcia obsługę usunięcie osoby podczas eksportowania. </br>
  **Rozwiązanie:** obsługi usuwania można skonfigurować poczty do usunięcia osoby, podczas eksportowania.

### <a name="fixed-issues"></a>Rozwiązane problemy:
* Usługi sieci Web ogólne:
 * W przypadku zmiany adresu URL usługi hello w domyślnym SAP wsconfig projektów za pomocą narzędzia do konfiguracji usługi sieci Web, a następnie sytuacji hello następujący błąd: nie można odnaleźć części ścieżki hello

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* Ogólny LDAP:
 * Łącznik GLDAP nie widzieć wszystkie atrybuty w usług AD LDS
 * Podziały kreatora po wykryciu żadnych atrybutów nazwy UPN od schematu katalogu LDAP hello
 * Delta importów niepowodzeniem z powodu błędów odnajdywania nie występuje podczas pełnego importu, gdy atrybut "objectclass" nie jest zaznaczona.
 * Stronę konfiguracji "Konfiguruj partycje i hierarchie" nie wyświetla żadnych obiektów, który typ jest równy toohello partycji dla nowych serwerów w hello ogólny  
LDAP MA. Pokazują one tylko obiekty z partycji RootDSE.


* Ogólny SQL:
 * Napraw dla znaku wodnego ogólnego SQL usterki atrybutu wielowartościowego niezaimportowanych Import zmian
 * Podczas eksportowania deleted\added wartości atrybutu wielowartościowego, nie są one deleted\added w źródle danych.  


* Program Lotus Notes:
 * Określone pole "Pełna nazwa" jest wyświetlany w magazynie metaverse hello poprawnie jednak eksportowanie tooNotes hello wartość dla atrybutu hello po wartości Null lub jest pusta.
 * Usuń zduplikowane Certifier błędu
 * W przypadku wybrania hello obiektu bez żadnych danych na powitania łącznika programu Lotus Domino z innymi obiektami następnie Otrzymaliśmy hello odnajdywania błędu podczas wykonywania pełnego importu.
 * Gdy Import zmian jest była uruchomiona na powitania łącznika programu Lotus Domino na końcu tego działania, hello hello usługi Microsoft.IdentityManagement.MA.LotusDomino.Service.exe czasami zwraca błąd aplikacji.
 * Członkostwo w grupach ogólną działa prawidłowo i jest obsługiwany, ale podczas uruchamiania hello eksportu tootry tooremove użytkownika z członkostwa pokazuje pomyślnym przeprowadzeniu z aktualizacją, ale faktycznie nie pobrać usunąć użytkownika hello z członkostwa programu Lotus Notes.
 * Tryb toochoose możliwość eksportowania jako "Dołącz element u dołu" został dodany w konfiguracji graficznego interfejsu użytkownika programu Lotus MA tooappend nowych elementów u dołu podczas eksportowania hello atrybutów wielowartościowych.
 * Łącznik spowoduje to dodanie hello potrzebne logiki toodelete hello plik z folderu poczty hello i identyfikator magazynu.
 * Usuń członkostwa nie pracuje w cross NAB elementu członkowskiego.
 * Wartości, które powinny być pomyślnie usunięte z atrybutu wielowartościowego

## <a name="111170"></a>1.1.117.0
Wydanie: 2016 marca

**Nowy łącznik**  
Początkowa wersja hello [ogólny Łącznik usług SQL](active-directory-aadconnectsync-connector-genericsql.md).

**Nowe funkcje:**

* Ogólny łącznik LDAP:
  * Dodano obsługę import zmian z Isode.
* Łącznik usług sieci Web:
  * Zaktualizowano hello csEntryChangeResult działania i setImportErrorCode działania tooallow obiektu błędy na poziomie toobe zwrócony toohello wstecz aparatu synchronizacji.
  * Zaktualizowano hello SAP6 i SAP6User szablony toouse hello nowy błąd poziomu funkcji obiektu.
* Programu Lotus Domino łącznika:
  * Eksportu należy co certifier na książce adresowej. Można teraz Użyj hello samo hasło dla wszystkich wydających świadectwa toomake hello zarządzania łatwiejsze.

**Rozwiązane problemy:**

* Ogólny łącznik LDAP:
  * Dla IBM Tivoli DS niektóre atrybuty odwołania nie został wykryty poprawnie.
  * Dla usługi LDAP otwarte podczas importowania różnicowych odstępy na powitania początek i koniec ciągów została obcięta.
  * Novell i NetIQ eksportu przeniesiona obiektu między jednostkami organizacyjnymi/kontenerów i na powitania sam czasu obiektu hello zmienioną nazwę nie powiodło się.
* Łącznik usług sieci Web:
  * Jeśli usługa sieci web hello miał wiele punkty końcowe dla tego samego powiązania, następnie hello łącznika nie poprawnie wykrył te punkty końcowe.
* Programu Lotus Domino łącznika:
  * Eksport hello Pełna nazwa atrybutu tooa w poczty bazy danych zakończyło się niepowodzeniem.
  * Eksport, który zarówno dodania i usunięcia elementu członkowskiego z grupy, tylko do wyeksportowanego hello dodane elementy członkowskie.
  * Jeśli dokument o wersji jest nieprawidłowy (isValid atrybutu hello Ustaw toofalse), następnie hello łącznika kończy się niepowodzeniem.

## <a name="older-releases"></a>Starsze wersje
Przed marca 2016 hello łączników zostały wydane jako tematy pomocy technicznej.

**Ogólny LDAP**

* [KB3078617](https://support.microsoft.com/kb/3078617) -1.0.0597, września 2015
* [KB3044896](https://support.microsoft.com/kb/3044896) -1.0.0549, marca 2015 roku
* [KB3031009](https://support.microsoft.com/kb/3031009) -1.0.0534, stycznia 2015
* [KB3008177](https://support.microsoft.com/kb/3008177) -1.0.0419, września 2014 r.
* [KB2936070](https://support.microsoft.com/kb/2936070) -4.3.1082, marca 2014 r.

**Usługi sieci Web**

* [KB3008178](https://support.microsoft.com/kb/3008178) -1.0.0419, września 2014 r.

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) -1.0.0419, września 2014 r.

**Programu Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) -1.0.0597, września 2015
* [KB3044895](https://support.microsoft.com/kb/3044895) -1.0.0549, marca 2015 roku
* [KB2977286](https://support.microsoft.com/kb/2977286) -5.3.0712, sierpnia 2014 r.
* [KB2932635](https://support.microsoft.com/kb/2932635) -5.3.1003, luty 2014 r.  
* [KB2899874](https://support.microsoft.com/kb/2899874) -5.3.0721, październik 2013
* [KB2875551](https://support.microsoft.com/kb/2875551) -5.3.0534, sierpnia 2013

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
