---
title: "Historia wersji łącznika | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera listę wszystkich wersji łączników dla programu Forefront Identity Manager (FIM) i Microsoft Identity Manager (MIM)"
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
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a>Historia wersji łącznika
Łączników programu Forefront Identity Manager (FIM) i Microsoft Identity Manager (MIM) są często aktualizowane.

> [!NOTE]
> Ten temat dotyczy tylko programu FIM i MIM. Te łączniki nie są obsługiwane dla instalacji na Azure AD Connect. Wydanych łączników są preinstalowane na AADConnect w przypadku uaktualniania do kompilacji.

Ten temat zawiera wszystkie wersje łączników, które zostały wydane.

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
  * W operacji importu GSQL został nie konwertowania czasu poprawnie, podczas zapisywania do przestrzeni łącznika. Domyślny format daty i godziny przestrzeni łącznika GSQL został zmieniony z "RRRR MM-dd: ssZ" na "RRRR MM-dd: ssZ".

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>Rozwiązane problemy:

* Usługi sieci Web ogólne:
  * Narzędzie Wsconfig nie zostały przekonwertowane poprawnie tablicy Json z "przykładowe żądanie" dla metody usługi REST. Przyczyną problemów z serializacji tej tablicy Json dla żądania REST.
  * Narzędzie konfiguracji łącznika usług sieci Web nie obsługuje użycia miejsca symboli w nazwach atrybutów JSON 
    * Wzorzec podstawienia można dodać ręcznie do pliku WSConfigTool.exe.config, np.```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Program Lotus Notes:
  * Gdy opcja **Zezwalaj na niestandardowe wydających świadectwa dla jednostki organizacyjnej/organizacji** jest wyłączony łącznik zakończy się niepowodzeniem podczas eksportu (aktualizacja) po przepływu eksportu wszystkie atrybuty zostaną wyeksportowane do Domino, ale w czasie eksportu KeyNotFoundException jest zwracana do synchronizacji. 
    * Dzieje się tak, ponieważ operacja zmiany nazwy nie powiodło się, gdy próbuje zmienić nazwy domeny (atrybut nazwy użytkownika), zmieniając jeden z atrybutów poniżej:  
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
  * Dodano możliwość enable\disable wyszukiwanie jednostki organizacyjne przed otwarciem GlobalParameters strony

## <a name="114430"></a>1.1.443.0

Wydanie: 2017 marca

### <a name="enhancements"></a>Ulepszenia

* Ogólny SQL:</br>
  **Scenariusz symptomy:** jest dobrze znane ograniczenie z łącznikiem SQL, w którym możemy tylko Zezwalaj na odwołanie do typu jeden obiekt i wymagają odwołań z elementami członkowskimi. </br>
  **Opis rozwiązania:** w kroku przetwarzania dla odwołania "*" zostanie wybrana opcja, wszystkich kombinacji typów obiektów zostaną zwrócone do aparatu synchronizacji.

>[!Important]
- Spowoduje to utworzenie wielu symboli zastępczych
- Jest on wymagany do upewnij się, że nazwy są unikatowe między typami obiektów.


* Ogólny LDAP:</br>
 **Scenariusz:** po wybraniu kilku kontenerów w określonej partycji, następnie wyszukiwania nadal będzie realizowane w całej partycji. Właściwe będą filtrowane przez usługę synchronizacji, ale nie MA, co może spowodować obniżenie wydajności. </br>

 **Opis rozwiązania:** zmienić GLDAP łącznika kod, aby była możliwa przejdź przez wszystkie kontenery i wyszukiwania obiektów w każdej z nich, zamiast wyszukiwanie w całej partycji.


* Programu Lotus Domino:

  **Scenariusz:** Domino poczty usunięcia obsługę usunięcie osoby podczas eksportowania. </br>
  **Rozwiązanie:** obsługi usuwania można skonfigurować poczty do usunięcia osoby, podczas eksportowania.

### <a name="fixed-issues"></a>Rozwiązane problemy:
* Usługi sieci Web ogólne:
 * W przypadku zmiany domyślnego adresu URL usługi SAP wsconfig projektów za pomocą narzędzia do konfiguracji usługi sieci Web, a następnie wystąpił następujący błąd: nie można odnaleźć części ścieżki

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* Ogólny LDAP:
 * Łącznik GLDAP nie widzieć wszystkie atrybuty w usług AD LDS
 * Podziały kreatora po wykryciu żadnych atrybutów nazwy UPN od schematu katalogu LDAP
 * Delta importów niepowodzeniem z powodu błędów odnajdywania nie występuje podczas pełnego importu, gdy atrybut "objectclass" nie jest zaznaczona.
 * Stronę konfiguracji "Konfiguruj partycje i hierarchie" nie wyświetla żadnych obiektów typu jest równa partycji dla nowych serwerów w ogólnej  
LDAP MA. Pokazują one tylko obiekty z partycji RootDSE.


* Ogólny SQL:
 * Napraw dla znaku wodnego ogólnego SQL usterki atrybutu wielowartościowego niezaimportowanych Import zmian
 * Podczas eksportowania deleted\added wartości atrybutu wielowartościowego, nie są one deleted\added w źródle danych.  


* Program Lotus Notes:
 * Określone pole "Pełna nazwa" jest wyświetlane w magazynie metaverse poprawnie jednak podczas eksportowania notatek wartość atrybutu ma wartość Null lub pusty.
 * Usuń zduplikowane Certifier błędu
 * W przypadku wybrania obiekt bez żadnych danych łącznika programu Lotus Domino z innymi obiektami następnie Otrzymaliśmy błąd odnajdywania podczas wykonywania pełnego importu.
 * Gdy Import zmian jest była uruchomiona łącznika programu Lotus Domino na końcu tego przebiegu Microsoft.IdentityManagement.MA.LotusDomino.Service.exe usługi czasami zwraca błąd aplikacji.
 * Członkostwo w grupach ogólną działa prawidłowo i jest obsługiwany, ale podczas uruchamiania eksportu, aby spróbować usunąć użytkownika z członkostwa są wyświetlane pomyślnym przeprowadzeniu z aktualizacją, ale faktycznie nie pobrać usunąć użytkownika z członkostwa programu Lotus Notes.
 * Pozwala wybrać tryb eksportu "Dołącz element u dołu" został dodany w konfiguracji graficznego interfejsu użytkownika programu Lotus MA dołączyć nowe elementy u dołu podczas eksportowania dla atrybutów wielowartościowych.
 * Łącznik spowoduje dodanie logiki potrzebne do Usuń plik z folderu poczty i identyfikator magazynu.
 * Usuń członkostwa nie pracuje w cross NAB elementu członkowskiego.
 * Wartości, które powinny być pomyślnie usunięte z atrybutu wielowartościowego

## <a name="111170"></a>1.1.117.0
Wydanie: 2016 marca

**Nowy łącznik**  
Początkowa wersja [ogólny Łącznik usług SQL](active-directory-aadconnectsync-connector-genericsql.md).

**Nowe funkcje:**

* Ogólny łącznik LDAP:
  * Dodano obsługę import zmian z Isode.
* Łącznik usług sieci Web:
  * Zaktualizowano csEntryChangeResult a działaniem setImportErrorCode umożliwia błędów poziomu obiekt ma zostać zwrócony aparatu synchronizacji.
  * Zaktualizowano SAP6 SAP6User szablonów i korzystać z nowych funkcji błąd poziomu obiektu.
* Programu Lotus Domino łącznika:
  * Eksportu należy co certifier na książce adresowej. Można teraz używać tego samego hasła dla wszystkich wydających świadectwa aby ułatwić zarządzanie.

**Rozwiązane problemy:**

* Ogólny łącznik LDAP:
  * Dla IBM Tivoli DS niektóre atrybuty odwołania nie został wykryty poprawnie.
  * Dla usługi LDAP otwarte podczas importowania różnicowych białe znaki na początku i na końcu ciągów została obcięta.
  * Novell i NetIQ eksportu przeniesiona obiektu między jednostkami organizacyjnymi/kontenery i w tym samym czasie, należy zmienić nazwy obiektu nie powiodło się.
* Łącznik usług sieci Web:
  * Jeśli usługa sieci web ma wiele punkty końcowe dla tego samego powiązania, następnie łącznika nie poprawnie wykrył te punkty końcowe.
* Programu Lotus Domino łącznika:
  * Eksport atrybutu imię i nazwisko poczty w bazie danych zakończyło się niepowodzeniem.
  * Export, która zarówno dodania i usunięcia elementu członkowskiego z grupy eksportowane tylko dodanych elementów.
  * Jeśli dokument o wersji jest nieprawidłowy (isValid atrybut ma wartość false), a następnie łącznika kończy się niepowodzeniem.

## <a name="older-releases"></a>Starsze wersje
Przed marca 2016 łączników zostały wydane jako tematy pomocy technicznej.

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
Dowiedz się więcej o [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
