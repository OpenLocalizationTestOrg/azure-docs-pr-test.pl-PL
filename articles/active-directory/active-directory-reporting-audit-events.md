---
title: "zdarzenia raportów inspekcji usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Przeprowadzono inspekcję zdarzeń, które są dostępne do wyświetlania i pobierania z usługą Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Zdarzenia raportu inspekcji usługi Azure Active Directory
*Niniejsza dokumentacja jest częścią hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).*

Hello Azure Active Directory inspekcji raport pomaga klientom identyfikowanie uprzywilejowanych akcji, które wystąpiły w usłudze Azure Active Directory. Uprzywilejowanych akcji obejmują zmiany podniesienia uprawnień (na przykład tworzenie roli lub resetowanie haseł), zmiana konfiguracji zasad (na przykład zasady haseł) lub zmiany konfiguracji toodirectory (na przykład zmiany toodomain federacyjnego ustawienia). Witaj raporty zawierają hello rekordu inspekcji dla nazwy zdarzenia hello, aktora hello, który wykonał akcję hello, zasobu docelowego hello wpływ zmiany hello i hello daty i czasu (UTC). Klienci są w stanie tooretrieve hello listę zdarzeń inspekcji dla ich Azure Active Directory za pośrednictwem hello [Azure Portal](https://portal.azure.com/), zgodnie z opisem w [wyświetlanie dzienników inspekcji](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Lista zdarzenia raportów inspekcji
<!--- audit event descriptions should be in hello past tense --->

| Zdarzenia | Opis zdarzenia |
| --- | --- |
| **Zdarzenia użytkownika** | |
| Dodaj użytkownika |Dodać katalog toohello użytkowników. |
| Usuń użytkownika |Usunąć użytkownika z katalogu hello. |
| Ustawianie właściwości licencji |Ustawianie właściwości licencji powitania dla użytkownika w katalogu hello. |
| Resetowanie hasła użytkownika |Resetowanie hasła hello użytkownika w katalogu hello. |
| Zmień hasło użytkownika |Witaj hasło dla użytkownika w katalogu hello zmienione. |
| Licencja użytkownika zmiany |Zmienić hello licencją tooa użytkownika w katalogu hello. licencje, które zostały zaktualizowane, poszukać na powitania toosee [aktualizacji użytkownika](#update-user-attributes) poniżej właściwości |
| Aktualizuj użytkownika |Zaktualizowano użytkownika w katalogu hello. [Zobacz poniżej](#update-user-attributes) dla atrybutów, które mogą zostać zaktualizowane. |
| Zestaw życie Zmienianie hasła użytkownika |Ustaw właściwość hello toochange użytkownika hasła podczas logowania. |
| Zaktualizuj poświadczenia użytkownika |Hasło użytkownika hello zmienione |
| **Grupowanie zdarzeń** | |
| Dodaj grupę |Utworzyć grupę w katalogu hello. |
| Grupy aktualizacji |Zaktualizowano grupę w katalogu hello. toosee właściwości grupy, które zostały zaktualizowane, można znaleźć zbyt[inspekcji właściwości grupy](#update-group-attributes) w poniższej sekcji hello |
| Usuwanie grupy |Usunąć grupę z hello katalogu. |
| CreateGroupSettings |Utworzona grupa ustawień |
| UpdateGroupSettings |Zaktualizowano ustawienia grupy. toosee, jakie ustawienia grupy zostały zaktualizowane, można znaleźć zbyt[inspekcji właściwości grupy](#update-group-attributes) w poniższej sekcji hello |
| DeleteGroupSettings |Usunięto grupę ustawień |
| SetGroupLicense |Ustaw grupy licencji. |
| SetGroupManagedBy |Ustaw grupę toobe zarządzanych przez użytkownika |
| AddGroupMember |Dodano element członkowski toogroup |
| RemoveGroupMember |Usuwanie członka z grupy |
| AddGroupOwner |Dodano właściciela toogroup |
| RemoveGroupOwner |Właściciel usunięty z grupy |
| **Zdarzenia aplikacji** | |
| Dodaj nazwy głównej usługi |Dodać katalog główny toohello usługi. |
| Usuń nazwy głównej usługi |Usunięte nazwy głównej usługi z hello katalogu. |
| Dodaj poświadczenia główne usługi |Nazwy głównej usługi tooa dodano poświadczeń. |
| Usuń poświadczenia główne usługi |Usunięto poświadczeń z nazwy głównej usługi. |
| Dodaj wpis delegowania |Utworzony [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) w katalogu hello. |
| Wpis delegowania zestawu |Zaktualizowano [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) w katalogu hello. |
| Usuń wpis delegowania |Usunięte [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) w katalogu hello. |
| **Zdarzenia roli** | |
| Dodaj tooRole członek roli |Dodaje rolę użytkownika tooa katalogu. |
| Usuń członka roli z roli |Usunięty użytkownik z rolą katalogu. |
| AddRoleDefinition |Definicja roli dodany. |
| UpdateRoleDefinition |Zaktualizowano definicji roli. toosee ustawienia ról zostały zaktualizowane, można znaleźć zbyt[inspekcji właściwości definicji roli](#update-role-definition-attributes) w poniższej sekcji hello |
| DeleteRoleDefinition |Usunąć definicji roli. |
| AddRoleAssignmentToRoleDefinition |Dodano definicji toorole przypisania roli. |
| RemoveRoleAssignmentFromRoleDefinition |Przypisanie roli usuniętych z definicji roli. |
| AddRoleFromTemplate |Dodano rolę z szablonu. |
| UpdateRole |Zaktualizowano rolę. |
| AddRoleScopeMemberToRole |Dodano toorole zakresami elementu członkowskiego. |
| RemoveRoleScopedMemberFromRole |Usunąć element członkowski w zakresie z roli. |
| **Zdarzenia urządzenia (wszystkie zdarzenia)** | |
| AddDevice |Dodane urządzenie. |
| UpdateDevice |Zaktualizowano urządzenia. toosee właściwości, które urządzenia zostały zaktualizowane, można znaleźć zbyt[właściwości urządzenia Audited](#update-device-attributes) w poniższej sekcji hello |
| DeleteDevice |Usunięto urządzenie. |
| AddDeviceConfiguration |Konfiguracja dodanego urządzenia. |
| UpdateDeviceConfiguration |Konfiguracja zaktualizowanych urządzeniach. toosee właściwości konfiguracji urządzenia, które zostały zaktualizowane, można znaleźć zbyt[właściwości konfiguracji urządzenia Audited](#update-device-configuration-attributes) w poniższej sekcji hello |
| DeleteDeviceConfiguration |Konfiguracja urządzenia usunięte. |
| AddRegisteredOwner |Dodano toodevice zarejestrowany właściciel. |
| AddRegisteredUsers |Dodano toodevice zarejestrowanych użytkowników. |
| RemoveRegisteredOwner |Zarejestrowany właściciel należy usunąć z urządzenia. |
| RemoveRegisteredUsers |Usuń zarejestrowanych użytkowników z urządzeniami. |
| RemoveDeviceCredentials |Usuń poświadczenia urządzenia. |
| **Zdarzenia B2B** | |
| Przekazano zaprasza partii. |Administrator został przekazany plik zawierający toobe zaproszenia wysyłane toopartner użytkowników. |
| Partii zaprasza przetworzone. |Plik zawierający użytkowników toopartner zaproszenia został przetworzony. |
| Zaprosić użytkowników zewnętrznych. |Użytkownik zewnętrzny został zaproszony toohello katalogu. |
| Wykorzystaj zaprosić użytkowników zewnętrznych. |Użytkownik zewnętrzny ma zrealizowane ich katalogu toohello zaproszenia. |
| Dodaj toogroup użytkownika zewnętrznego. |Członkostwo grupy tooa w katalogu hello został przypisany użytkownik zewnętrzny. |
| Przypisz tooapplication użytkownika zewnętrznego. |Bezpośredni dostęp do aplikacji tooan został przypisany użytkownik zewnętrzny. |
| Tworzenie wirusa dzierżawy. |Realizacji zaproszenia hello utworzono nowej dzierżawy w usłudze Azure AD. |
| Tworzenie użytkownika wirusa. |Użytkownik został utworzony w istniejącej dzierżawy w usłudze Azure AD przez hello zaproszenia realizacji. |
| **Jednostki administracyjne (wszystkie zdarzenia)** | |
| AddAdministrativeUnit |Dodaj jednostki administracyjnej. |
| UpdateAdministrativeUnit |Aktualizowanie jednostki administracyjnej. toosee właściwości jednostki administracyjne, które zostały zaktualizowane, można znaleźć zbyt[właściwości jednostki administracyjne inspekcji](#update-administrative-unit-attributes) w poniższej sekcji hello |
| DeleteAdministrativeUnit |Usuń jednostki administracyjnej. |
| AddMemberToAdministrativeUnit |Dodaj element członkowski tooadministrative jednostki. |
| RemoveMemberFromAdministrativeUnit |Usuń element członkowski z jednostki administracyjne. |
| **Katalog zdarzenia** | |
| Dodaj toocompany partnera |Dodaje katalogu toohello partnera. |
| Usunąć partnera firmy |Usunąć partnera z hello katalogu. |
| DemotePartner |Obniż poziom partnera. |
| Dodaj toocompany domeny |Dodaje katalogu toohello domeny. |
| Usuwanie domen z firmy |Domena może być usunięta z katalogu hello. |
| Aktualizowanie domeny |Zaktualizowano domeny hello katalogu. toosee właściwości domeny, które zostały zaktualizowane, można znaleźć zbyt[właściwości domeny inspekcji](#update-domain-attributes) w poniższej sekcji hello |
| Zestaw uwierzytelniania domeny |Zmienić domyślne ustawienie domeny hello hello firmy. |
| Ustaw informacje kontaktowe firmy |Ustawianie preferencji dotyczących kontaktu na poziomie przedsiębiorstwa. W tym adresów e-mail dla powiadomień marketing, a także techniczne dotyczące usług Microsoft Online Services. |
| Ustawienia federacji w domenie |Zaktualizowano ustawienia Federacji hello domeny. |
| Sprawdź domeny |Zweryfikować domeny hello katalogu. |
| Sprawdź zweryfikowanej domeny poczty e-mail |Zweryfikować domeny na powitania katalogu przy użyciu Weryfikacja adresu e-mail. |
| Ustaw flagę DirSyncEnabled na firmy |Ustaw właściwość hello, która umożliwia katalogu dla usługi Azure AD Sync. |
| Ustaw zasady haseł |Ustaw ograniczenia długości i znak dla hasła użytkownika. |
| Ustaw informacje o firmie |Informacje o poziomie firmy hello zaktualizowane. Zobacz hello [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) polecenia cmdlet programu PowerShell, aby uzyskać więcej informacji. |
| SetCompanyAllowedDataLocation |Zestaw firmy może lokalizacja danych. |
| SetCompanyDirSyncEnabled |Ustaw flagę DirSyncEnabled. |
| SetCompanyDirSyncFeature |Zestaw funkcji DirSync. |
| SetCompanyInformation |Informacje o firmie zestawu. |
| SetCompanyMultiNationalEnabled |Ustaw włączona funkcja międzynarodowej firmy. |
| SetDirectoryFeatureOnTenant |Ustawienia funkcji katalogu dzierżawcy. |
| SetTenantLicenseProperties |Ustaw właściwości licencji dzierżawy. |
| CreateCompanySettings |Tworzenie ustawień firmy |
| UpdateCompanySettings |Zaktualizuj ustawienia firmy. toosee właściwości firmy, które zostały zaktualizowane, można znaleźć zbyt[właściwości firmy inspekcji](#update-company-attributes) w poniższej sekcji hello |
| DeleteCompanySettings |Usuń ustawienia firmy |
| SetAccidentalDeletionThreshold |Należy ustawić próg przypadkowego usunięcia. |
| SetRightsManagementProperties |Ustaw właściwości zarządzania prawami. |
| PurgeRightsManagementProperties |Przeczyść właściwości zarządzania prawami. |
| UpdateExternalSecrets |Aktualizowanie kluczy tajnych zewnętrznych |
| **Zdarzenia dotyczące zasad (wszystkie zdarzenia)** | |
| AddPolicy |Dodaj zasady. |
| UpdatePolicy |Aktualizacja zasad. |
| Usuń zasady |Usuń zasady. |
| AddDefaultPolicyApplication |Dodaj tooapplication zasad. |
| AddDefaultPolicyServicePrincipal |Dodaj zasady tooservice principal. |
| RemoveDefaultPolicyApplication |Usuń zasady z aplikacji. |
| RemoveDefaultPolicyServicePrincipal |Usuń zasady z nazwy głównej usługi. |
| RemovePolicyCredentials |Usuń poświadczenia zasad. |

## <a name="audit-report-retention"></a>Przechowywania raportów inspekcji

Aby hello najnowsze informacje dotyczące przechowywania, zobacz [zasady przechowywania raportów usługi Azure Active Directory](active-directory-reporting-retention.md).


W przypadku klientów do przechowywania ich zdarzeń inspekcji przez dłuższy czas przechowywania hello interfejsu API raportowania może być zdarzeń inspekcji ściągania tooregularly używanych w magazynie danych. Zobacz [wprowadzenie hello interfejsu API raportowania](active-directory-reporting-api-getting-started.md) szczegółowe informacje.

## <a name="properties-included-with-each-audit-event"></a>Właściwości dołączone do każdego zdarzenia inspekcji
| Właściwość | Opis |
| --- | --- |
| Data i godzina |Wystąpił Hello datę i godzinę, które hello zdarzeń inspekcji |
| Aktora |Witaj użytkownika lub nazwy głównej usługi, która wykonana akcja hello |
| Akcja |Witaj akcję, która została wykonana |
| docelowy |Witaj użytkownika lub nazwy głównej usługi, który hello akcja została wykonana na |

## <a name="update-user-attributes"></a>Atrybuty "Aktualizuj użytkownika"
zdarzenie inspekcji Hello "użytkownik aktualizacji" zawiera dodatkowe informacje na temat atrybutów użytkowników, jakie zostały zaktualizowane. Dla każdego atrybutu zarówno hello poprzednią wartość i nową wartość hello jest dołączony.

| Atrybut | Opis |
| --- | --- |
| AccountEnabled |Hello użytkownicy mogą się logować. |
| AssignedLicense |Wszystkie licencje, które zostały przypisane do użytkownika toohello. |
| AssignedPlan |Planów usługi wynikające z licencji hello przypisany użytkownik toohello. |
| LicenseAssignmentDetail |Szczegółowe informacje o licencji przypisany użytkownik toohello. Na przykład jeśli uczestniczyła oparte na grupach licencjonowania to obejmować grupy hello przyznanych hello licencji. |
| Komórkowy |Telefon komórkowy Hello użytkownika. |
| OtherMail |Witaj adres alternatywny adres e-mail użytkownika. |
| OtherMobile |Witaj użytkownika alternatywnych telefonu komórkowego. |
| StrongAuthenticationMethod |Z listy metod weryfikacji skonfigurowany przez użytkownika hello uwierzytelnianie wieloskładnikowe, takie jak wywołania głosowych, SMS lub weryfikacji kod z aplikacji mobilnej. |
| StrongAuthenticationRequirement |Jeśli uwierzytelnianie wieloskładnikowe jest wymuszana, włączona lub wyłączona dla tego użytkownika. |
| StrongAuthenticationUserDetails |Hello użytkownika telefonu numer telefonu number, alternatywnych i wiadomości e-mail adres używany przez uwierzytelnianie wieloskładnikowe i weryfikacji resetowania hasła. |
| StrongAuthenticationPhoneAppDetail |Aplikacje phone forof szczegółów zarejestrowany tooperform 2FA logowania |
| TelephoneNumber |numer telefonu użytkownika Hello. |
| AlternativeSecurityId |Identyfikator alternatywny zabezpieczeń dla obiektu hello. |
| Wartość CreationType |Metoda tworzenia użytkownika hello, (albo przez zaproszenie wirusa). |
| InviteTicket |Lista biletów zaproszenia na powitania użytkownika. |
| InviteReplyUrl |Lista adresów URL tooreply po zaakceptowaniu zaproszenia. |
| InviteResources |Lista zasobów toowhich hello użytkownika zostali zaproszeni. |
| LastDirSyncTime |Czas ostatniej hello obiektu aktualizacji ze względu na synchronizowanie z hello autorytatywne (nabywca, lokalna) katalogu. |
| MSExchRemoteRecipientType |Mapuje tooMSO typy odbiorcy. Odwołuje się zbyt https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx [typy odbiorcy MSO] dla typów adresatów |
| PreferredDataLocation |Witaj Preferowana lokalizacja hello użytkownika, grupy, kontaktu folderu publicznego lub danych urządzenia. |
| ProxyAddresses |adres Hello za pomocą której rozpoznano obiektu adresatów programu Exchange Server w systemie obcego poczty. |
| StsRefreshTokensValidFrom |Powoduje odświeżenie tokenu odwołania — wszystkie tokeny odświeżania STS wydanych przed tym razem są uznawane za wygasłe. |
| userPrincipalName |Witaj nazwę UPN, która jest Internet stylu nazwy logowania dla użytkownika. |
| Wartości parametru UserState |Stan użytkownika oczekuje na zatwierdzenie/PendingAcceptance/zaakceptowany/PendingVerification. |
| UserStateChangedOn |Sygnatura czasowa ostatniego tooUserState zmiany. Używane tootrigger cyklu życia w przepływach pracy. |
| UserType |Typ użytkownika. Element członkowski (0), gościa (1), Viral(2). |

## <a name="update-group-attributes"></a>Atrybuty "Grupa aktualizacji"
| Atrybut | Opis |
| --- | --- |
| Klasyfikacja |Klasyfikacja Hello grupy Unified (o dużym znaczeniu Biznesowym, MBI itp.). |
| Opis |Czytelny dla człowieka opisową fraz o hello obiektu. |
| Nazwa wyświetlana |Nazwa wyświetlana Hello obiektu |
| DirSyncEnabled |Wskazuje, czy z autorytatywnych synchronizacji katalogu (nabywca, lokalnych). |
| GroupLicenseAssignment |Przypisanie licencji grupy |
| GroupType |Typ grupy, Unified (0) |
| IsMembershipRuleLocked |Wskazuje, że hello właściwości MembershipRule jest ustawiony przez usługę zarządzania grupami samoobsługi hello i nie może zostać zmienione przez użytkowników. Dotyczy tylko toogroups, gdzie GroupType obejmuje GroupType.DynamicMembership |
| IsPublic |Flaga tooindicate, jeśli grupa hello jest publiczny/prywatny. |
| LastDirSyncTime |Czas ostatniego hello obiektu został zaktualizowany w wyniku synchronizowanie z autorytatywnych hello (lokalnie klienta) katalogu. |
| Poczta |Podstawowy adres e-mail |
| MailEnabled |Wskazuje, czy ta grupa ma obsługi poczty e-mail. |
| mailNickname |Moniker dla obiekt książki adresów, zwykle hello część nazwy e-mail poprzedzających hello "@" symbolu. |
| MembershipRule |Ciąg hello kryteriów używanych przez toodetermine usługi Zarządzanie grupami samoobsługi hello wyrażenia elementów członkowskich, które powinny należeć toothis grupy. Zobacz też IsMembershipRuleLocked. Dotyczy tylko toogroups gdzie GroupType obejmuje GroupType.DynamicMembership. |
| MembershipRuleProcessingState |Wartość wyliczenia zdefiniowanych przez usługę zarządzania grupami samoobsługi hello definiowaniu stanu hello członkostwa przetwarzania dla tej grupy. Dotyczy tylko toogroups gdzie GroupType obejmuje GroupType.DynamicMembership. |
| ProxyAddresses |adres Hello za pomocą której rozpoznano obiektu adresatów programu Exchange Server w systemie obcego poczty. |
| RenewedDateTime |Rekord sygnatury czasowej podczas ostatniego został odnowiony grupy. |
| Securityenabled musi |Wskazuje, czy członkostwo w grupie hello mogą wpływać na decyzje dotyczące autoryzacji. |
| WellKnownObject |Etykiety obiektu katalogu wyznaczenie go jako jeden z wstępnie zdefiniowanego zestawu. |

## <a name="update-device-attributes"></a>Atrybuty "Aktualizuj urządzenia"
| Atrybut | Opis |
| --- | --- |
| AccountEnabled |Wskazuje, czy podmiot zabezpieczeń może uwierzytelnić. |
| CloudAccountEnabled |Wskazuje, czy podmiot zabezpieczeń może uwierzytelnić. Gdy urządzenie hello jest zarządzany w siedzibie firmy i zapisywane przez usługę InTune. |
| CloudDeviceOSType |Typ urządzenia hello oparte na powitania systemu operacyjnego, np. Windows RT, iOS. Kiedy ustawione przez usługi w chmurze (takich jak usługa Intune), ten atrybut staje się w katalogu hello autorytatywne dla DeviceOSType. |
| CloudDeviceOSVersion |Wersja hello systemu operacyjnego. Kiedy ustawione przez usługi w chmurze (takich jak usługa Intune), ten atrybut staje się w katalogu hello autorytatywne dla DeviceOSVersion. |
| CloudDisplayName |Wartość atrybutu LDAP hello Nazwa wyświetlana. Gdy są ustawione przez usługi w chmurze (takich jak usługa Intune), ten atrybut staje się autorytatywne w katalogu hello Nazwa wyświetlana. |
| CloudCreated |Wskazuje, czy obiekt hello został utworzony przez usługi w chmurze. |
| CompliantUntil |Do czasu, jaki urządzenie jest uznany za zgodnego. |
| DeviceMetadata |Niestandardowych metadanych dla hello urządzenia |
| DeviceObjectVersion |Ten atrybut jest wersją schematu hello tooidentify używane hello urządzenia. |
| DeviceOSType |Typ urządzenia hello oparte na powitania systemu operacyjnego, np. Windows RT, iOS. Napisane przez hello usługi rejestracji i zamierzonego toobe zaktualizowane przez hello MDM zarządzania usługi STS światła lub usługi zarządzania. |
| DeviceOSVersion |Wersja hello systemu operacyjnego. Napisane przez hello usługi rejestracji i zamierzonego toobe zaktualizowane przez hello MDM zarządzania usługi STS światła lub usługi zarządzania. |
| DevicePhysicalIds |Wielowartościowy atrybut przeznaczony toostore identyfikatory hello urządzenia fizycznego. Może to obejmować identyfikatory systemu BIOS, modułu TPM odciski palców, sprzętu określonych identyfikatorów itp. |
| DirSyncEnabled |Wskazuje, czy z autorytatywnych (nabywca, lokalnie) synchronizacji katalogu. |
| Nazwa wyświetlana |Nazwa wyświetlana Hello obiektu |
| IsCompliant |Ten atrybut jest stan zarządzania urządzeniem przenośnym hello używane toomanage hello urządzenia. |
| IsManaged |Ten atrybut służy tooindicate hello urządzenie jest zarządzane przez chmurze zarządzanie urządzeniami przenośnymi. |
| LastDirSyncTime |Czas ostatniej hello obiektu aktualizacji ze względu na synchronizowanie z autorytatywnych hello (lokalnie klienta) katalogu. |

## <a name="update-device-configuration-attributes"></a>Atrybuty "Aktualizuj konfigurację urządzenia"
| Atrybut | Opis |
| --- | --- |
| MaximumRegistrationInactivityPeriod |Hello maksymalna liczba dni korzystania z urządzenia może być nieaktywne, zanim zostanie to uznane za do usunięcia. |
| RegistrationQuota |Zasada używana toolimit hello liczbę dozwoloną dla pojedynczego użytkownika rejestracji urządzenia. |

## <a name="update-service-principal-configuration-attributes"></a>Atrybuty "Aktualizuj konfigurację główna usługi"
| Atrybut | Opis |
| --- | --- |
| AccountEnabled |Wskazuje, czy podmiot zabezpieczeń może uwierzytelnić. |
| Identyfikator AppPrincipalId |Tożsamość zewnętrznych, zdefiniowane przez aplikację dla podmiotu zabezpieczeń. |
| Nazwa wyświetlana |Nazwa wyświetlana Hello obiektu |
| ServicePrincipalName |Główną nazwę usługi, zawierający "Nazwa/urząd" gdzie nazwa określa wartość klasy aplikacji, a urząd zawiera co najmniej nazwę hosta [: port] lub "name", który określa identyfikator hello nazwy głównej usługi. |

## <a name="update-app-attributes"></a>Atrybuty "Aktualizuj aplikacji"
| Atrybut | Opis |
| --- | --- |
| AppAddress |zestaw Hello adresów (adresy URL przekierowania), które są przypisane tooa nazwy głównej usługi. |
| Identyfikator aplikacji |Identyfikator aplikacji hello aplikacji |
| AppIdentifierUri |Aplikacja identyfikator URI, który identyfikuje aplikacji hello.  Zazwyczaj jest adres URL dostępu do aplikacji hello. |
| AppLogoUrl |adres url Hello obraz logo aplikacji hello przechowywane w sieci CDN. |
| AvailableToOtherTenants |Aplikacja hello wartość true, to wielodostępne (tj. mogą być używane przez innych dzierżawców). |
| Nazwa wyświetlana |Nazwa wyświetlana nazwa aplikacji Hello |
| Uprawnienia |Lista aplikacji uprawnień. |
| ExternalUserAccountDelegationsAllowed |Flaga wskazująca, czy aplikacja zasobów jest zaufany i można tworzyć wpisów delegowania dla kont użytkowników zewnętrznych. |
| GroupMembershipClaims |członkostwo w grupie Hello oświadczeń zasad. |
| PublicClient |Wartość true, jeśli powitania klienta nie może przechowywać tajne (tj. jawne klienta w OAuth2.0) |
| RecordConsentConditions |Typy warunków zgody, zgodnie z definicją hello warunków umów: Brak (0), SilentConsentForPartnerManagedApp(1). Ta wartość będzie widoczne w schemacie interfejsu API programu Graph hello i mogą być tylko zestaw/zmieniony przez administratorów dzierżawy. |
| RequiredResourceAccess |Zawartości XML wartość hello RequiredResourceAccess właściwości. |
| Aplikacja sieci Web |Wartość true wskazuje, że ta aplikacja jest aplikacji sieci web. |
| WwwHomepage |Witaj głównej strony sieci Web. |

## <a name="update-role-attributes"></a>Atrybuty "Aktualizuj rolę"
| Atrybut | Opis |
| --- | --- |
| AppAddress |zestaw Hello adresów (adresy URL przekierowania), które są przypisane tooa nazwy głównej usługi. |
| BelongsToFirstLoginObjectSet |Wartość true wskazuje, że ten obiekt należy toohello zestaw obiektów tooenable wymagana nazwa logowania Witaj, Administratorze pierwszy z nowym dzierżawcą. |
| Wbudowane |Wskazuje, czy okres istnienia obiektu hello jest własnością hello systemu. |
| Opis |Czytelny dla człowieka opisową fraz o hello obiektu. |
| Nazwa wyświetlana |Nazwa wyświetlana Hello obiektu |
| mailNickname |Moniker dla obiekt książki adresów, zwykle hello część nazwy e-mail poprzedzających hello "@" symbolu. |
| RoleDisabled |Wskazuje, czy rola hello powinny być ignorowane na potrzeby kontroli dostępu. |
| RoleTemplateId |Tożsamość hello szablonu roli. |
| ServiceInfo |Specyficzne dla usługi udostępniania informacji, które może być zużyte przez MOAC i/lub innych wystąpień usługi (z hello tych samych lub różnych typów usług). |
| TaskSetScopeReference |Identyfikuje TaskSet i zestaw zakresy skojarzone z rolą lub szablonów RoleTemplate. |
| ValidationError |Informacje o opublikowane przez usługę federacyjną opisujące nieprzejściowego, specyficzne dla usługi błąd dotyczący właściwości hello lub Połącz z tooresolve działania administratora obiektu. |
| WellKnownObject |Etykiety obiektu katalogu wyznaczenie go jako jeden z wstępnie zdefiniowanego zestawu. |

## <a name="update-role-definition-attributes"></a>Atrybuty "Aktualizuj definicji roli"
| Atrybut | Opis |
| --- | --- |
| AssignableScopes |Kolekcja zakresów autoryzacji, które można odwoływać się podczas przypisywania tego podmiotu zabezpieczeń tooa definicji RoleDefinition. |
| Nazwa wyświetlana |Nazwa wyświetlana Hello obiektu |
| GrantedPermissions |Uprawnienia przyznane przez tej definicji RoleDefinition. |

## <a name="update-administrative-unit-attributes"></a>Atrybuty "Aktualizuj jednostki administracyjne"
| Atrybut | Opis |
| --- | --- |
| Opis |Ta właściwość jest aktualizowany po zmianie hello opis jednostki administracyjne. |
| Nazwa wyświetlana |Ta właściwość jest aktualizowany po zmianie nazwy hello jednostki administracyjne. |

## <a name="update-company-attributes"></a>Atrybuty "Firmy aktualizacji"
| Atrybut | Opis |
| --- | --- |
| AllowedDataLocation |Lokalizacja, w których hello firmy użytkownicy mogą toobe udostępnione. |
| AuthorizedServiceInstance |Nazwy toowhich wystąpień usługi planu może wdrożyć. |
| DirSyncEnabled |Wskazuje, czy z autorytatywnych (nabywca, lokalnie) synchronizacji katalogu. |
| DirSyncStatus |Wskazuje, czy synchronizacja adres książki obiektów w tym kontekście dzierżawy autorytatywne (klientów lokalnie) katalogu. rozszerzenia hello DirSyncEnabled właściwości obiektów firmy. |
| DirSyncFeatures |Bit flagi śledzenie tookeep zestawu funkcji dirsync włączonych i wyłączonych hello dzierżawcy. |
| DirectoryFeatures |Funkcje katalogu włączone/wyłączone. |
| DirSyncConfiguration |Zawiera wszystkie narzędzia DirSync konfiguracji określonych toohello bieżącą dzierżawą. |
| Nazwa wyświetlana |Nazwa wyświetlana Hello obiektu |
| IsMnc |Flaga wartości logicznej firmy hello zbyt "wartość true", jeśli zestaw jest włączone dla funkcji międzynarodową firmą hello. |
| ObjectSettings |Kolekcja zakresie toohello odpowiednie ustawienia hello obiektu. |
| PartnerCommerceUrl |Witryna handlowa partnera toohello adresu URL. |
| PartnerHelpUrl |Witryna pomocy partnera toohello adresu URL. |
| PartnerSupportEmail |Adres URL toohello partnera adres e-mail pomocy technicznej. |
| PartnerSupportTelephone |Adres URL toohello partnera telefonu pomocy technicznej. |
| PartnerSupportUrl |Adres URL toohello partnera witrynę pomocy technicznej. |
| StrongAuthenticationDetails |Szczegóły dotyczące tooStrongAuthentication. |
| StrongAuthenticationPolicy |Silne uwierzytelnianie zasad dla firmy hello. |
| TechnicalNotificationMail |Wiadomości e-Mail adres toonotify problemów technicznych dotyczących tooa firmy. |
| TelephoneNumber |Numery telefonów, które są zgodne z hello ITU zalecenie E.123. |
| TenantType |Typ Hello dzierżawcy. Jeśli ta wartość nie jest określona, dzierżawy hello jest firma. W przeciwnym razie możliwe wartości to: MicrosoftSupport (0), SyndicatePartner (1), ValueAddedResellerPartnerDelegatedAdmin ResellerPartnerDelegatedAdmin (4) BreadthPartnerDelegatedAdmin (3) BreadthPartner [2] [5]. |
| VerifiedDomain |Zestaw nazw domen DNS powiązany tooa firmy. |

## <a name="update-domain-attributes"></a>Atrybuty "Aktualizuj domeny"
| Atrybut | Opis |
| --- | --- |
| Możliwości |Bit flagi opisujące możliwości hello domeny hello ewentualne. |
| Domyślne |Wskazuje, czy domena hello jest wartość domyślna hello; na przykład hello domyślne UserPrincipalName sufiks gdy administrator tworzy nowego użytkownika w MOAC. |
| Początkowa |Wskazuje, czy domeny hello jest domena początkowa hello firmy hello przydzielony przez OCP. domena początkowa Hello jest unikatowy domeny podrzędne domeny Online firmy Microsoft; e.g.contoso3.microsoftonline.com. |
| LiveType |Typ hello odpowiedniego identyfikatora Windows Live przestrzeni nazw, jeśli istnieją. |
| Nazwa |Identyfikator dla punktu końcowego hello. |
| PasswordNotificationWindowDays |Witaj liczba dni do wygaśnięcia hasła użytkownika hello zostaje powiadomiony. |
| PasswordValidityPeriodDays |Witaj liczbę dni ważności hasła jest dobra dla, należy zmienić. |

Rekordy inspekcji są wymaganej kontrolki do wielu przepisy dotyczące zgodności. W przypadku klientów przy użyciu hello Azure Active Directory inspekcji raport toomeet ich przepisy dotyczące zgodności zaleca się powitania klienta przesyłania kopię tego tematu Pomocy z kopią powitania klienta hello wyeksportowany raport dotyczący inspekcji toohelp wyjaśnić hello raportu szczegółowe informacje. Jeżeli audytor hello toounderstand hello przepisy dotyczące zgodności obecnie spełniających Azure, bezpośrednie hello audytora toohello [strony zgodności](https://azure.microsoft.com/support/trust-center/compliance/) z hello Microsoft Azure Trust Center.

