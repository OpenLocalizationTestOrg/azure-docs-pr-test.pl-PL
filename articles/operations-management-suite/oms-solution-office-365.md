---
title: "rozwiązanie aaaOffice 365 w Operations Management Suite (OMS) | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera szczegółowe informacje o konfiguracji i korzystanie z rozwiązania hello usługi Office 365 w OMS.  Zawiera szczegółowy opis rekordy hello usługi Office 365 w analizy dzienników."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>Rozwiązania Office 365 w Operations Management Suite (OMS)

![Logo usługi Office 365](media/oms-solution-office-365/icon.png)

Witaj rozwiązanie Office 365 dla Operations Management Suite (OMS) umożliwia toomonitor środowisku usługi Office 365 w analizy dzienników.  

- Monitorowanie aktywności użytkowników na Twoich wzorców użycia tooanalyze kont usługi Office 365 oraz w behawioralnej trendów. Na przykład można wyodrębnić scenariusze użycia określonego, takich jak pliki, które są udostępniane spoza organizacji lub hello najbardziej popularnych witryn programu SharePoint.
- Monitorowanie zmian konfiguracji tootrack działania administratora lub operacji wysokiego poziomu uprawnień.
- Wykrywanie i zbadaj zachowanie niechciane użytkownika, które można dostosować do własnych potrzeb organizacji.
- Prezentacja inspekcji i zgodności. Na przykład można monitorować operacji uzyskiwania dostępu do pliku na poufne pliki, które ułatwiają wykonywanie procesu hello inspekcji i zgodności.
- Rozwiązywania problemów operacyjnych przy użyciu pakietu OMS wyszukiwania na podstawie danych działania usługi Office 365 w organizacji.

## <a name="prerequisites"></a>Wymagania wstępne
Witaj poniżej znajduje się wymagane toothis poprzedniego rozwiązania jest zainstalowany i skonfigurowany.

- Organizacyjnej subskrypcji usługi Office 365.
- Poświadczenia dla konta użytkownika, który jest administratorem globalnym.
- dane inspekcji tooreceive, należy najpierw [należy skonfigurować inspekcję](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) w ramach subskrypcji usługi Office 365.  Należy pamiętać, że [inspekcji skrzynki pocztowej](https://technet.microsoft.com/library/dn879651.aspx) skonfigurowano oddzielnie.  Można nadal zainstalować hello rozwiązania i zbierać innych danych, jeśli inspekcja nie jest skonfigurowany.
 


## <a name="management-packs"></a>Pakiety administracyjne
To rozwiązanie nie instalować żadnych pakietów administracyjnych w podłączonych grup zarządzania.
  

## <a name="configuration"></a>Konfiguracja
Gdy [Dodaj subskrypcję tooyour rozwiązania hello usługi Office 365](../log-analytics/log-analytics-add-solutions.md), masz tooconnect on tooyour subskrypcji usługi Office 365.

1. Dodaj tooyour rozwiązania zarządzania alertami hello obszarem roboczym pakietu OMS za pomocą hello procesu opisanego w [dodać rozwiązania](../log-analytics/log-analytics-add-solutions.md).
2. Przejdź za**ustawienia** w portalu OMS hello.
3. W obszarze **połączonych źródeł**, wybierz pozycję **usługi Office 365**.
4. Polecenie **połączenie usługi Office 365**.<br>![Konstruktor usługi Office 365](media/oms-solution-office-365/configure.png)
5. Zaloguj się tooOffice 365 przy użyciu konta administratora globalnego dla Twojej subskrypcji. 
6. Hello subskrypcji zostaną wyświetlone z hello obciążeń, które rozwiązanie hello będzie monitorował.<br>![Konstruktor usługi Office 365](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>Zbieranie danych
### <a name="supported-agents"></a>Obsługiwani agenci
Hello rozwiązanie Office 365 nie pobierania danych z dowolnej hello [agentów OMS](../log-analytics/log-analytics-data-sources.md).  Pobiera on dane bezpośrednio z usługi Office 365.

### <a name="collection-frequency"></a>Częstotliwość zbierania
Usługi Office 365, wysyła [powiadomienia elementu webhook](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) z szczegółowe dane tooLog Analytics zawsze jest tworzony rekord.

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello
Po dodaniu hello usługi Office 365 rozwiązania tooyour obszarem roboczym pakietu OMS hello **usługi Office 365** kafelka zostanie dodany tooyour OMS z pulpitu nawigacyjnego. Ten Kafelek Wyświetla graficzną reprezentację hello liczby komputerów i liczba w danym środowisku i ich zgodności aktualizacji.<br><br>
![Kafelek podsumowania usługi Office 365](media/oms-solution-office-365/tile.png)  

Polecenie hello **usługi Office 365** hello tooopen kafelka **usługi Office 365** pulpitu nawigacyjnego.

![Pulpit nawigacyjny usługi Office 365](media/oms-solution-office-365/dashboard.png)  

pulpit nawigacyjny Hello zawiera kolumny hello w hello w poniższej tabeli. Każda kolumna zawiera listę hello top dziesięciu alertów według Liczba pasujących kolumny kryteria hello określenia zakresu zakresu i czasu. Można uruchomić wyszukiwania dziennika, która udostępnia hello całą listę, klikając Zobacz wszystkie u dołu hello hello kolumny lub przez kliknięcie nagłówka kolumny hello.

| Kolumna | Opis |
|:--|:--|
| Operacje | Zawiera informacje o hello aktywnych użytkowników z subskrypcji usługi Office 365 wszystkie monitorowane. Będzie również toosee stanie hello liczbę działań, które się tak zdarzyć w czasie.
| Exchange | Pokazuje podział hello działania serwera Exchange, takie jak uprawnienie Add-Mailbox lub Set-Mailbox. |
| Sharepoint | Pokazuje hello top działania czy użytkownicy wykonywać na dokumentów programu SharePoint. Gdy przechodzenie z tego kafelka hello strony wyszukiwania pokazuje hello szczegóły tych działań, takich jak dokument docelowy hello i hello lokalizację tego działania. Na przykład dla zdarzenia dostępu do pliku, będzie możliwe toosee hello dokument, który jest dostępny, jego nazwa skojarzone konto i adres IP. |
| Usługa Azure Active Directory | Zawiera użytkownika najwyższego działań, takich jak zresetować hasło użytkownika i prób logowania. Możesz przejść do szczegółów, będziesz toosee stanie hello szczegóły tych działań, takich jak hello stan wyniku. Najczęściej jest to przydatne, jeśli chcesz toomonitor podejrzanych działań w usłudze Azure Active Directory. |




## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics

Wszystkie rekordy w obszarze roboczym analizy dzienników hello przez rozwiązanie hello usługi Office 365 mają **typu** z **OfficeActivity**.  Witaj **OfficeWorkload** właściwość określa, które rekord hello usługi Office 365 odwołuje się zbyt Exchange, usługi AzureActiveDirectory, SharePoint lub usługi OneDrive.  Witaj **RecordType** właściwość określa typ hello operacji.  właściwości Hello będą się różnić dla poszczególnych typów operacji i przedstawiono w poniższych tabelach hello.

### <a name="common-properties"></a>Wspólne właściwości
Witaj następujące właściwości są wspólne rekordy tooall usługi Office 365.

| Właściwość | Opis |
|:--- |:--- |
| Typ | *OfficeActivity* |
| ClientIP | adres IP Hello hello urządzenia, który został użyty podczas hello działanie zostało zarejestrowane. adres IP Hello są wyświetlane w formacie adres IPv4 lub IPv6. |
| OfficeWorkload | Usługa Office 365 rekord hello odnosi się do.<br><br>Usługi AzureActiveDirectory<br>Exchange<br>Sharepoint|
| Operacja | Nazwa Hello hello działania użytkownika lub administratora.  |
| Identyfikatora organizacji | Witaj identyfikatora GUID dla dzierżawy usługi Office 365 w organizacji. Ta wartość będzie zawsze można hello takie same dla organizacji, niezależnie od tego, usługa hello usługi Office 365, w którym występuje. |
| recordType | Typ działania wykonywane. |
| ResultStatus | Wskazuje, czy akcja hello (hello określony w operacji właściwości) zakończyła się powodzeniem. Możliwe wartości to zakończyło się pomyślnie, PartiallySucceded lub nie powiodło się. Aktywność administratora programu Exchange, wartość hello jest wartość PRAWDA lub FAŁSZ. |
| Nazwa użytkownika | Witaj UPN (główna nazwa użytkownika) hello użytkownika, który wykonał hello akcję, która spowodowała rekordu hello są rejestrowane; na przykład my_name@my_domain_name. Należy pamiętać, że rejestruje działania wykonywane przez kont systemowych (np. SHAREPOINT\system lub NTAUTHORITY\SYSTEM) dostępne są również. | 
| UserKey | Alternatywny identyfikator użytkownika hello objęci hello właściwości identyfikatora użytkownika.  Na przykład ta właściwość jest wypełniana hello passport Unikatowy identyfikator (PUID) dla zdarzeń wykonywane przez użytkowników w programie SharePoint, usłudze OneDrive dla firm i Exchange. Ta właściwość może również określić hello tę samą wartość jak hello właściwości identyfikatora użytkownika dla zdarzenia występujące w innych usługach i wydarzeniach wykonywane przez kont systemowych|
| UserType | Typ Hello użytkownika, która jest wykonywana operacja hello.<br><br>Administrator<br>Aplikacja<br>DcAdmin<br>Regularne<br>Zarezerwowane<br>ServicePrincipal<br>System |


### <a name="azure-active-directory-base"></a>Azure Active Directory base
Hello następujące właściwości są wspólne tooall usługi Azure Active Directory rekordów.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Usługi AzureActiveDirectory |
| recordType     | Usługi AzureActiveDirectory |
| AzureActiveDirectory_EventType | Typ Hello zdarzenia usługi Azure AD. |
| właściwości rozszerzone | Witaj rozszerzone właściwości zdarzenia hello Azure AD. |


### <a name="azure-active-directory-account-logon"></a>Azure logowania konto usługi Active Directory
Te rekordy są tworzone, gdy użytkownika usługi Active Directory próbuje toolog na.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Usługi AzureActiveDirectory |
| recordType     | AzureActiveDirectoryAccountLogon |
| Aplikacja | Aplikacja Hello wyzwala zdarzenia logowania konta hello, takich jak Office 15. |
| Klient | Szczegółowe informacje o powitania klienta urządzenia, systemu operacyjnego urządzenia i przeglądarka na urządzeniu była używana w hello hello konto logowania zdarzeń. |
| stanu logowania | Ta właściwość jest bezpośrednio z OrgIdLogon.LoginStatus. Hello mapowania różnych interesujące niepowodzeń logowania może być wykonywane przez alerty algorytmów. |
| UserDomain | Witaj dzierżawy informacji o tożsamości (TII). | 


### <a name="azure-active-directory"></a>Usługa Azure Active Directory
Te rekordy są tworzone podczas dodatkami lub zmiany są wprowadzane tooAzure obiektów usługi Active Directory.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Usługi AzureActiveDirectory |
| recordType     | Usługi AzureActiveDirectory |
| AADTarget | Użytkownik Hello wykonanej akcji hello (określone przez właściwość operacji hello). |
| Aktora | Witaj użytkownika lub nazwy głównej usługi, która wykonana akcja hello. |
| ActorContextId | należy Hello GUID organizacji hello hello aktora. |
| ActorIpAddress | Witaj aktora adresu IP w formacie adres IPV4 lub IPV6. |
| InterSystemsId | Witaj identyfikator GUID, który śledzić akcje hello między składnikami w ramach usługi hello usługi Office 365. |
| IntraSystemId |   Witaj identyfikator GUID generowany przez akcję hello tootrack usługi Azure Active Directory. |
| SupportTicketId | powitania klienta obsługuje identyfikator biletu hello działań w sytuacjach "act na imieniu of". |
| TargetContextId | Witaj GUID organizacji hello hello wybrany użytkownik należy do. |


### <a name="data-center-security"></a>Zabezpieczeń w centrum danych
Te rekordy są tworzone na podstawie danych inspekcji zabezpieczeń w centrum danych.  

| Właściwość | Opis |
|:--- |:--- |
| EffectiveOrganization | Nazwa Hello hello dzierżawy, który hello podniesienia uprawnień/polecenia cmdlet był celem. |
| ElevationApprovedTime | Witaj sygnaturę czasową po została zatwierdzona hello podniesienia uprawnień. |
| ElevationApprover | Nazwa Hello manager firmy Microsoft. |
| ElevationDuration | czas trwania powitania dla hello, który był aktywny podniesienia uprawnień. |
| ElevationRequestId |  Unikatowy identyfikator dla hello żądania podniesienia uprawnień. |
| ElevationRole | Zażądano Hello roli hello podniesienia uprawnień funkcji. |
| ElevationTime | Witaj uruchomienie hello podniesienia uprawnień. |
| Godzina_rozpoczęcia | czas wykonywania poleceń cmdlet hello rozpoczęcia Hello. |


### <a name="exchange-admin"></a>Administrator programu Exchange
Te rekordy są tworzone podczas wprowadzania zmian konfiguracji tooExchange.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Exchange |
| recordType     | ExchangeAdmin |
| ExternalAccess |  Określa, czy polecenie cmdlet hello zostało uruchomione przez użytkowników w organizacji przez personel centrum danych firmy Microsoft lub konta usługi Centrum danych lub administratora delegowanego. Hello wartość FAŁSZ oznacza, że to polecenie cmdlet hello zostało uruchomione przez osobę będącą w Twojej organizacji. Hello wartość True wskazuje, że to polecenie cmdlet hello zostało uruchomione przez personel centrum danych, konto usługi Centrum danych lub administratora delegowanego. |
| ModifiedObjectResolvedName |  To jest przyjazna nazwa użytkownika hello hello obiektu, który został zmodyfikowany przez polecenie cmdlet hello. To jest rejestrowane tylko wtedy, gdy polecenie cmdlet hello modyfikuje hello obiektu. |
| Nazwa_organizacji | Nazwa Hello hello dzierżawy. |
| OriginatingServer | Nazwa Hello hello serwera, z którym hello wykonano polecenia cmdlet. |
| Parametry | Witaj nazw i wartości dla wszystkich parametrów, które były używane z polecenia cmdlet hello, który określono w hello właściwości operacji. |


### <a name="exchange-mailbox"></a>Skrzynek pocztowych programu Exchange
Te rekordy są tworzone podczas zmiany lub dodatki zostały wprowadzone tooExchange skrzynek pocztowych.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Exchange |
| recordType     | ExchangeItem |
| ClientInfoString | Informacje o powitania klienta poczty e-mail, które były używane tooperform hello operacji, takich jak wersja przeglądarki, wersja programu Outlook i informacje o urządzeniach przenośnych. |
| Client_IPAddress | adres IP Hello hello urządzenia, który został użyty podczas operacji hello został zapisany w dzienniku. adres IP Hello są wyświetlane w formacie adres IPv4 lub IPv6. |
| ClientMachineName | Nazwa komputera Hello obsługującego powitania klienta programu Outlook. |
| ClientProcessName | Hello klienta poczty e-mail, który był skrzynki pocztowej hello tooaccess używane. |
| ClientVersion | Wersja Hello powitania klienta poczty e-mail. |
| InternalLogonType | Zarezerwowany do użytku wewnętrznego. |
| Logon_Type | Wskazuje typ hello użytkownika, który dostęp do skrzynek pocztowych hello i wykonać operacji hello, który został zapisany w dzienniku. |
| LogonUserDisplayName |    Przyjazna nazwa Hello hello użytkownika, który wykonał operację hello. |
| LogonUserSid | Identyfikator SID użytkownika hello, który wykonał operację hello Hello. |
| MailboxGuid | Witaj GUID Exchange hello skrzynki pocztowej, którego próbował uzyskać dostęp. |
| MailboxOwnerMasterAccountSid | Skrzynka pocztowa właściciela konta głównego identyfikatora SID konta. |
| MailboxOwnerSid | Identyfikator SID właściciela pocztowej hello Hello. |
| MailboxOwnerUPN | adres e-mail Hello hello właściciela hello skrzynki pocztowej, którego próbował uzyskać dostęp. |


### <a name="exchange-mailbox-audit"></a>Inspekcji skrzynki pocztowej programu Exchange
Te rekordy są tworzone po utworzeniu wpisu inspekcji skrzynki pocztowej.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Exchange |
| recordType     | ExchangeItem |
| Element | Reprezentuje element hello, na które hello wykonano operację | 
| SendAsUserMailboxGuid | Hello GUID Exchange hello skrzynki pocztowej, który był dostęp do poczty e-mail toosend jako. |
| SendAsUserSmtp | Adres SMTP hello, użytkownik jest Personifikowany. |
| SendonBehalfOfUserMailboxGuid | Hello GUID Exchange hello skrzynki pocztowej, który był dostęp do poczty toosend zastępczy. |
| SendOnBehalfOfUserSmtp | Adresu SMTP użytkownika hello w imieniu którego hello poczty e-mail są wysyłane. |


### <a name="exchange-mailbox-audit-group"></a>Grupy inspekcji skrzynki pocztowej programu Exchange
Te rekordy są tworzone podczas zmiany lub dodatki zostały wprowadzone tooExchange grup.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Informacje o każdym elemencie hello grupy. |
| CrossMailboxOperations | Wskazuje, czy operacja hello związane z więcej niż jedną skrzynkę pocztową. |
| DestMailboxId | Ustawiona tylko wtedy, gdy parametr CrossMailboxOperations hello ma wartość PRAWDA. Określa hello pocztowej docelowy identyfikator GUID. |
| DestMailboxOwnerMasterAccountSid | Ustawiona tylko wtedy, gdy parametr CrossMailboxOperations hello ma wartość PRAWDA. Określa hello identyfikatora SID dla konta głównego hello identyfikator SID właściciela pocztowej hello docelowej. |
| DestMailboxOwnerSid | Ustawiona tylko wtedy, gdy parametr CrossMailboxOperations hello ma wartość PRAWDA. Określa hello SID hello docelowy pocztowej. |
| DestMailboxOwnerUPN | Ustawiona tylko wtedy, gdy parametr CrossMailboxOperations hello ma wartość PRAWDA. Określa hello UPN właściciela hello hello docelowy pocztowej. |
| DestFolder | folder docelowy powitania dla operacji, takich jak przeniesienie. |
| Folder | Hello folder, w której znajduje się grupa elementów. |
| Foldery |     Informacji o folderach źródła hello uwzględnionego w operacji; na przykład, jeśli foldery są zaznaczone, a następnie usuwany. |


### <a name="sharepoint-base"></a>Podstawa programu SharePoint
Te właściwości są wspólne tooall SharePoint rekordów.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Sharepoint |
| OfficeWorkload | Sharepoint |
| Źródła zdarzeń | Określa, czy wystąpiło zdarzenie w programie SharePoint. Możliwe wartości to SharePoint lub ObjectModel. |
| ItemType | Hello typ obiektu, który został dostępne lub zmodyfikowany. Zobacz tabeli ItemType hello szczegółowe informacje na temat hello typów obiektów. |
| MachineDomainInfo | Informacje o operacji synchronizacji urządzenia. Te informacje są dostarczane tylko wtedy, gdy znajduje się on na powitania żądania. |
| MachineId |   Informacje o operacji synchronizacji urządzenia. Te informacje są dostarczane tylko wtedy, gdy znajduje się on na powitania żądania. |
| Site_ | Witaj GUID hello lokalizacja hello plik lub folder, dostępne hello użytkownika. |
| Source_Name | Witaj jednostki, która wyzwoliła hello inspekcji operacji. Możliwe wartości to SharePoint lub ObjectModel. |
| Agent użytkownika | Informacje dotyczące użytkownika powitania klienta lub przeglądarki. Informacje te są dostarczane przez powitania klienta lub przeglądarki. |


### <a name="sharepoint-schema"></a>Schemat programu SharePoint
Te rekordy są tworzone podczas zmiany konfiguracji zostały wprowadzone tooSharePoint.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Sharepoint |
| OfficeWorkload | Sharepoint |
| CustomEvent | Opcjonalny ciąg dla niestandardowych zdarzeń. |
| Event_Data |  Opcjonalne ładunek dla niestandardowych zdarzeń. |
| ModifiedProperties | Właściwość Hello jest uwzględniony w zdarzenia administrator, takie jak dodanie użytkownika jako członka lokację lub grupy administracyjnej kolekcji witryn. Właściwość Hello zawiera nazwę hello hello właściwości, która została zmodyfikowana (na przykład hello administratora witryny grupy), hello nowe wartości hello właściwości (takie hello użytkownika, który został dodany jako administratora witryny), i hello poprzednią wartość hello zmodyfikować obiekt. |


### <a name="sharepoint-file-operations"></a>Operacje na plikach programu SharePoint
Te rekordy są tworzone w ramach operacji toofile odpowiedzi w programie SharePoint.

| Właściwość | Opis |
|:--- |:--- |
| OfficeWorkload | Sharepoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | rozszerzenie pliku Hello skopiować lub przenieść pliku. Ta właściwość jest wyświetlany tylko w przypadku zdarzeń FileCopied i FileMoved. |
| Parametr DestinationFileName | Nazwa Hello hello pliku, który jest skopiowany lub przeniesiony. Ta właściwość jest wyświetlany tylko w przypadku zdarzeń FileCopied i FileMoved. |
| DestinationRelativeUrl | adres URL Hello hello folderu docelowego, gdzie skopiować lub przenieść pliku. Kombinacja Hello hello wartości parametrów SiteURL, DestinationRelativeURL i parametr DestinationFileName jest hello taka sama jak wartość hello hello ObjectID właściwość, która jest hello pełnej nazwy ścieżki dla pliku hello, która została skopiowana. Ta właściwość jest wyświetlany tylko w przypadku zdarzeń FileCopied i FileMoved. |
| SharingType | Typ Hello uprawnienia, które zostały przypisane toohello użytkownika, który został udostępniony zasób hello udostępniania. Ten użytkownik jest identyfikowany przez parametr UserSharedWith hello. |
| Site_Url | adres URL Hello hello lokalizacja hello plik lub folder, dostępne hello użytkownika. |
| SourceFileExtension | rozszerzenie pliku Hello hello pliku, który uzyskał hello użytkownika. Ta właściwość jest pusta, jeśli obiekt hello uzyskano jest folderem. |
| SourceFileName |  Nazwa Hello hello pliku lub folderu dostępne hello użytkownika. |
| SourceRelativeUrl | adres URL Hello hello folderu, który zawiera plik hello dostępne hello użytkownika. Kombinacja Hello hello wartości parametrów SiteURL, SourceRelativeURL i SourceFileName hello jest hello taka sama jak wartość hello hello ObjectID właściwość, która jest hello pełnej nazwy ścieżki dla pliku hello dostępne hello użytkownika. |
| UserSharedWith |  Witaj użytkownika, który został udostępniony zasób. |




## <a name="sample-log-searches"></a>Przykładowe wyszukiwania dzienników
Witaj w poniższej tabeli zawiera przykładowy dziennik wyszukuje rekordów aktualizacji zebrane przez to rozwiązanie.

| Zapytanie | Opis |
| --- | --- |
|Liczba wszystkich operacji hello w ramach subskrypcji usługi Office 365 |"Typ = OfficeActivity | Pomiar count() przez operację " |
|Użycie witryny programu SharePoint|"Typ = OfficeActivity OfficeWorkload = programu sharepoint | Miara count() jako liczba wg SiteUrl | Sortowanie Count asc "|
|Operacje na plikach dostępu przez użytkownika typu|"Typ = OfficeActivity OfficeWorkload = sharepoint operacji = FileAccessed | Pomiar count() przez UserType "|
|Wyszukiwanie z określone słowo kluczowe|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|Monitor działań zewnętrznych na serwerze Exchange|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>Rozwiązywanie problemów

Jeśli rozwiązania usługi Office 365 nie zbiera danych zgodnie z oczekiwaniami, sprawdź jego stan w portalu OMS hello **ustawienia** -> **połączonych źródeł** -> **usługi Office 365** . Witaj w poniższej tabeli opisano każdy stan.

| Stan | Opis |
|:--|:--|
| Aktywne | Witaj subskrypcji usługi Office 365 jest aktywna i obciążenie hello jest pomyślnie połączono tooyour obszarem roboczym pakietu OMS. |
| Oczekujące | Hello subskrypcji usługi Office 365 jest aktywny, ale obciążenie hello nie jest jeszcze podłączony tooyour obszarem roboczym pakietu OMS pomyślnie. Hello po raz pierwszy połączyć subskrypcję usługi Office 365 hello wszystkich obciążeń hello będzie w tym stanie do momentu pomyślnym nawiązaniu połączenia. Zezwól na 24 godziny, aż wszystkie hello obciążeń tooswitch tooActive. |
| Nieaktywne | Witaj subskrypcji usługi Office 365 jest nieaktywny. Sprawdź stronę administracyjne usługi Office 365, aby uzyskać szczegółowe informacje. Po aktywowaniu subskrypcji usługi Office 365, odłączyć go z obszaru roboczego OMS i połączyć ją ponownie toostart odbierania danych. |



## <a name="next-steps"></a>Następne kroki
* Użyj dziennika wyszukiwania w [analizy dzienników](../log-analytics/log-analytics-log-searches.md) tooview szczegółowe dane aktualizacji.
* [Tworzenie własnych pulpity nawigacyjne](../log-analytics/log-analytics-dashboards.md) toodisplay ulubione zapytania wyszukiwania usługi Office 365.
* [Tworzenie alertów](../log-analytics/log-analytics-alerts.md) toobe aktywnego powiadomienia ważne działań usługi Office 365.  
