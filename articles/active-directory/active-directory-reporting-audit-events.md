---
title: "Zdarzenia raportowania inspekcji usługi Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1620d917acf5a2c36767b5b03750c405f3631ee2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Zdarzenia raportu inspekcji usługi Azure Active Directory
*Ta dokumentacja jest częścią [Przewodnika po raportach usługi Azure Active Directory](active-directory-reporting-guide.md).*

Azure Active Directory inspekcji raport pomaga klientom identyfikowanie uprzywilejowanych akcji, które wystąpiły w usłudze Azure Active Directory. Uprzywilejowane akcje obejmują zmiany podniesienia uprawnień (na przykład tworzenie roli lub resetowanie haseł), zmiana konfiguracji zasad (na przykład zasady haseł) lub zmiany w konfiguracji katalogu (na przykład zmiany ustawień federacyjnego domeny). Raporty dostarczają rekordu inspekcji dla nazwy zdarzenia aktora, kto wykonał akcję zasobu docelowego wpływ zmiany oraz Data i godzina (w formacie UTC). Klienci będą mogli pobrać listę zdarzeń inspekcji dla ich Azure Active Directory za pośrednictwem [Azure Portal](https://portal.azure.com/), zgodnie z opisem w [wyświetlanie dzienników inspekcji](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Lista zdarzenia raportów inspekcji
<!--- audit event descriptions should be in the past tense --->

| Zdarzenia | Opis zdarzenia |
| --- | --- |
| **Zdarzenia użytkownika** | |
| Dodaj użytkownika |Dodaje użytkownika do katalogu. |
| Usuń użytkownika |Usunąć użytkownika z katalogu. |
| Ustawianie właściwości licencji |Ustawianie właściwości licencji dla użytkowników w katalogu. |
| Resetowanie hasła użytkownika |Resetowanie hasła dla użytkownika w katalogu. |
| Zmień hasło użytkownika |Zmieniono hasło dla użytkownika w katalogu. |
| Licencja użytkownika zmiany |Zmienić licencji przypisana do użytkownika w katalogu. Aby sprawdzić, jakie licencje zostały zaktualizowane, spójrz na [aktualizacji użytkownika](#update-user-attributes) poniżej właściwości |
| Aktualizuj użytkownika |Zaktualizowano użytkownika w katalogu. [Zobacz poniżej](#update-user-attributes) dla atrybutów, które mogą zostać zaktualizowane. |
| Zestaw życie Zmienianie hasła użytkownika |Ustaw właściwość, która wymusza na użytkowniku zmiany hasła podczas logowania. |
| Zaktualizuj poświadczenia użytkownika |Użytkownik zmienił hasło |
| **Grupowanie zdarzeń** | |
| Dodaj grupę |Utworzyć grupę w katalogu. |
| Grupy aktualizacji |Zaktualizowano grupę w katalogu. Aby wyświetlić właściwości grupy, które zostały zaktualizowane, zapoznaj się [inspekcji właściwości grupy](#update-group-attributes) w poniższej sekcji |
| Usuwanie grupy |Usunąć grupę z katalogu. |
| CreateGroupSettings |Utworzona grupa ustawień |
| UpdateGroupSettings |Zaktualizowano ustawienia grupy. Aby zobaczyć, jakie ustawienia grupy zostały zaktualizowane, zapoznaj się [inspekcji właściwości grupy](#update-group-attributes) w poniższej sekcji |
| DeleteGroupSettings |Usunięto grupę ustawień |
| SetGroupLicense |Ustaw grupy licencji. |
| SetGroupManagedBy |Ustaw grupę, które mają być zarządzane przez użytkownika |
| AddGroupMember |Dodano członka do grupy |
| RemoveGroupMember |Usuwanie członka z grupy |
| AddGroupOwner |Właściciel dodany do grupy |
| RemoveGroupOwner |Właściciel usunięty z grupy |
| **Zdarzenia aplikacji** | |
| Dodaj nazwy głównej usługi |Dodać nazwy głównej usługi do katalogu. |
| Usuń nazwy głównej usługi |Nazwy głównej usługi usunięta z katalogu. |
| Dodaj poświadczenia główne usługi |Dodano poświadczenia do nazwy głównej usługi. |
| Usuń poświadczenia główne usługi |Usunięto poświadczeń z nazwy głównej usługi. |
| Dodaj wpis delegowania |Utworzony [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) w katalogu. |
| Wpis delegowania zestawu |Zaktualizowano [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) w katalogu. |
| Usuń wpis delegowania |Usunięte [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) w katalogu. |
| **Zdarzenia roli** | |
| Dodaj członka roli do roli |Dodaje użytkownika do roli katalogu. |
| Usuń członka roli z roli |Usunięty użytkownik z rolą katalogu. |
| AddRoleDefinition |Definicja roli dodany. |
| UpdateRoleDefinition |Zaktualizowano definicji roli. Aby zobaczyć, jakie ustawienia roli zostały zaktualizowane, zapoznaj się [inspekcji właściwości definicji roli](#update-role-definition-attributes) w poniższej sekcji |
| DeleteRoleDefinition |Usunąć definicji roli. |
| AddRoleAssignmentToRoleDefinition |Przypisanie roli dodane do definicji roli. |
| RemoveRoleAssignmentFromRoleDefinition |Przypisanie roli usuniętych z definicji roli. |
| AddRoleFromTemplate |Dodano rolę z szablonu. |
| UpdateRole |Zaktualizowano rolę. |
| AddRoleScopeMemberToRole |Dodano zakresami członka do roli. |
| RemoveRoleScopedMemberFromRole |Usunąć element członkowski w zakresie z roli. |
| **Zdarzenia urządzenia (wszystkie zdarzenia)** | |
| AddDevice |Dodane urządzenie. |
| UpdateDevice |Zaktualizowano urządzenia. Aby wyświetlić właściwości, które urządzenia zostały zaktualizowane, zapoznaj się [właściwości urządzenia Audited](#update-device-attributes) w poniższej sekcji |
| DeleteDevice |Usunięto urządzenie. |
| AddDeviceConfiguration |Konfiguracja dodanego urządzenia. |
| UpdateDeviceConfiguration |Konfiguracja zaktualizowanych urządzeniach. Aby wyświetlić właściwości konfiguracji urządzenia, które zostały zaktualizowane, zapoznaj się [właściwości konfiguracji urządzenia Audited](#update-device-configuration-attributes) w poniższej sekcji |
| DeleteDeviceConfiguration |Konfiguracja urządzenia usunięte. |
| AddRegisteredOwner |Dodano zarejestrowany właściciel do urządzenia. |
| AddRegisteredUsers |Dodani użytkownicy zarejestrowanych do urządzenia. |
| RemoveRegisteredOwner |Zarejestrowany właściciel należy usunąć z urządzenia. |
| RemoveRegisteredUsers |Usuń zarejestrowanych użytkowników z urządzeniami. |
| RemoveDeviceCredentials |Usuń poświadczenia urządzenia. |
| **Zdarzenia B2B** | |
| Przekazano zaprasza partii. |Administrator został przekazany plik zawierający zaproszenia, które mają być wysyłane do użytkowników z firm partnerskich. |
| Partii zaprasza przetworzone. |Plik zawierający zaproszeń do użytkowników z firm partnerskich została przetworzona. |
| Zaprosić użytkowników zewnętrznych. |Użytkownik zewnętrzny ma zaproszenie do katalogu. |
| Wykorzystaj zaprosić użytkowników zewnętrznych. |Użytkownik zewnętrzny ma zrealizowane ich zaproszenie do katalogu. |
| Dodaj użytkownika zewnętrznego do grupy. |Użytkownik zewnętrzny przypisano przynależności do grupy w katalogu. |
| Przypisz użytkowników zewnętrznych do aplikacji. |Użytkownik zewnętrzny przypisano bezpośredni dostęp do aplikacji. |
| Tworzenie wirusa dzierżawy. |Realizacji zaproszenia utworzono nowej dzierżawy w usłudze Azure AD. |
| Tworzenie użytkownika wirusa. |Użytkownik został utworzony w istniejącej dzierżawy w usłudze Azure AD przez realizacji zaproszenia. |
| **Jednostki administracyjne (wszystkie zdarzenia)** | |
| AddAdministrativeUnit |Dodaj jednostki administracyjnej. |
| UpdateAdministrativeUnit |Aktualizowanie jednostki administracyjnej. Aby wyświetlić właściwości jednostki administracyjne, które zostały zaktualizowane, zapoznaj się [właściwości jednostki administracyjne inspekcji](#update-administrative-unit-attributes) w poniższej sekcji |
| DeleteAdministrativeUnit |Usuń jednostki administracyjnej. |
| AddMemberToAdministrativeUnit |Dodaj członka do jednostki administracyjne. |
| RemoveMemberFromAdministrativeUnit |Usuń element członkowski z jednostki administracyjne. |
| **Katalog zdarzenia** | |
| Dodać partnera do firmy |Dodać partnera do katalogu. |
| Usunąć partnera firmy |Usunąć partnera z katalogu. |
| DemotePartner |Obniż poziom partnera. |
| Dodawanie domeny do firmy |Domeny dodawane do katalogu. |
| Usuwanie domen z firmy |Domena może być usunięta z katalogu. |
| Aktualizowanie domeny |Zaktualizowano do domeny w katalogu. Aby wyświetlić właściwości domeny, które zostały zaktualizowane, zapoznaj się [właściwości domeny inspekcji](#update-domain-attributes) w poniższej sekcji |
| Zestaw uwierzytelniania domeny |Zmienić domyślne ustawienie domeny dla firmy. |
| Ustaw informacje kontaktowe firmy |Ustawianie preferencji dotyczących kontaktu na poziomie przedsiębiorstwa. W tym adresów e-mail dla powiadomień marketing, a także techniczne dotyczące usług Microsoft Online Services. |
| Ustawienia federacji w domenie |Zaktualizowano ustawienia domeny federacyjnej. |
| Sprawdź domeny |Zweryfikować domeny w katalogu. |
| Sprawdź zweryfikowanej domeny poczty e-mail |Zweryfikować domeny w katalogu za pomocą Weryfikacja adresu e-mail. |
| Ustaw flagę DirSyncEnabled na firmy |Ustaw właściwość, która umożliwia katalogu dla usługi Azure AD Sync. |
| Ustaw zasady haseł |Ustaw ograniczenia długości i znak dla hasła użytkownika. |
| Ustaw informacje o firmie |Informacje o poziomie firmy zostały zaktualizowane. Zobacz [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) polecenia cmdlet programu PowerShell, aby uzyskać więcej informacji. |
| SetCompanyAllowedDataLocation |Zestaw firmy może lokalizacja danych. |
| SetCompanyDirSyncEnabled |Ustaw flagę DirSyncEnabled. |
| SetCompanyDirSyncFeature |Zestaw funkcji DirSync. |
| SetCompanyInformation |Informacje o firmie zestawu. |
| SetCompanyMultiNationalEnabled |Ustaw włączona funkcja międzynarodowej firmy. |
| SetDirectoryFeatureOnTenant |Ustawienia funkcji katalogu dzierżawcy. |
| SetTenantLicenseProperties |Ustaw właściwości licencji dzierżawy. |
| CreateCompanySettings |Tworzenie ustawień firmy |
| UpdateCompanySettings |Zaktualizuj ustawienia firmy. Aby wyświetlić właściwości firmy, które zostały zaktualizowane, zapoznaj się [właściwości firmy inspekcji](#update-company-attributes) w poniższej sekcji |
| DeleteCompanySettings |Usuń ustawienia firmy |
| SetAccidentalDeletionThreshold |Należy ustawić próg przypadkowego usunięcia. |
| SetRightsManagementProperties |Ustaw właściwości zarządzania prawami. |
| PurgeRightsManagementProperties |Przeczyść właściwości zarządzania prawami. |
| UpdateExternalSecrets |Aktualizowanie kluczy tajnych zewnętrznych |
| **Zdarzenia dotyczące zasad (wszystkie zdarzenia)** | |
| AddPolicy |Dodaj zasady. |
| UpdatePolicy |Aktualizacja zasad. |
| Usuń zasady |Usuń zasady. |
| AddDefaultPolicyApplication |Dodawanie zasad do aplikacji. |
| AddDefaultPolicyServicePrincipal |Dodawanie zasad do nazwy głównej usługi. |
| RemoveDefaultPolicyApplication |Usuń zasady z aplikacji. |
| RemoveDefaultPolicyServicePrincipal |Usuń zasady z nazwy głównej usługi. |
| RemovePolicyCredentials |Usuń poświadczenia zasad. |

## <a name="audit-report-retention"></a>Przechowywania raportów inspekcji

Aby uzyskać najnowsze informacje dotyczące przechowywania, zobacz [zasady przechowywania raportów usługi Azure Active Directory](active-directory-reporting-retention.md).


W przypadku klientów do przechowywania ich zdarzeń inspekcji przez dłuższy czas przechowywania interfejsu API raportowania można regularnie ściągnięcia zdarzeń inspekcji w magazynie danych. Zobacz [wprowadzenie do interfejsu API raportowania](active-directory-reporting-api-getting-started.md) szczegółowe informacje.

## <a name="properties-included-with-each-audit-event"></a>Właściwości dołączone do każdego zdarzenia inspekcji
| Właściwość | Opis |
| --- | --- |
| Data i godzina |Data i godzina wystąpienia zdarzenia inspekcji |
| Aktora |Użytkownika lub nazwy głównej usługi, który wykonał akcję |
| Akcja |Akcja, która została wykonana |
| docelowy |Użytkownika lub nazwy głównej usługi wykonanej akcji |

## <a name="update-user-attributes"></a>Atrybuty "Aktualizuj użytkownika"
Zdarzenie inspekcji "Aktualizacji użytkownika" zawiera dodatkowe informacje na temat atrybutów użytkowników, jakie zostały zaktualizowane. Dla każdego atrybutu zarówno poprzednią wartość, jak i nowa wartość jest dołączony.

| Atrybut | Opis |
| --- | --- |
| AccountEnabled |Użytkownicy mogą się logować. |
| AssignedLicense |Wszystkie licencje, które zostały przypisane do użytkownika. |
| AssignedPlan |Plany usługi wynikające z licencji przypisane do użytkownika. |
| LicenseAssignmentDetail |Szczegółowe informacje o licencji przypisane do użytkownika. Na przykład jeśli uczestniczyła oparte na grupach licencjonowania obejmuje to grupy, do której przyznano licencji. |
| Komórkowy |Telefon komórkowy użytkownika. |
| OtherMail |Adres alternatywny adres e-mail użytkownika. |
| OtherMobile |Użytkownika alternatywnych telefonu komórkowego. |
| StrongAuthenticationMethod |Z listy metod weryfikacji skonfigurowany przez użytkownika usługi Multi-Factor Authentication, takie jak wywołania głosowych, SMS lub weryfikacji kod z aplikacji mobilnej. |
| StrongAuthenticationRequirement |Jeśli uwierzytelnianie wieloskładnikowe jest wymuszana, włączona lub wyłączona dla tego użytkownika. |
| StrongAuthenticationUserDetails |Numer telefonu użytkownika, alternatywne telefonu i adresu e-mail używany podczas weryfikacji resetowania uwierzytelnianie wieloskładnikowe i hasło. |
| StrongAuthenticationPhoneAppDetail |Aplikacje phone forof szczegółów zarejestrowany na potrzeby logowania 2FA |
| TelephoneNumber |Numer telefonu użytkownika. |
| AlternativeSecurityId |Identyfikator alternatywny zabezpieczeń dla obiektu. |
| Wartość CreationType |Metoda tworzenia użytkownika (albo przez zaproszenie wirusa). |
| InviteTicket |Lista zaproszenia biletów dla użytkownika. |
| InviteReplyUrl |Lista adresów URL odpowiedzi po zaakceptowaniu zaproszenia. |
| InviteResources |Lista zasobów, do których Zaproszono użytkownika. |
| LastDirSyncTime |Czas ostatniego obiekt został zaktualizowany ze względu na synchronizowanie z autorytatywnych katalogu (nabywca, lokalnych). |
| MSExchRemoteRecipientType |Mapy MSO typów adresatów. Zobacz [typy odbiorcy MSO] https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx dla typów adresatów |
| PreferredDataLocation |Preferowaną lokalizację użytkownika, grupy, kontaktu, folder publiczny lub danych urządzenia. |
| ProxyAddresses |Adres, za pomocą której rozpoznano obiektu adresatów programu Exchange Server w systemie obcego poczty. |
| StsRefreshTokensValidFrom |Powoduje odświeżenie tokenu odwołania — wszystkie tokeny odświeżania STS wydanych przed tym razem są uznawane za wygasłe. |
| userPrincipalName |Nazwa UPN jest Internet stylu nazwy logowania dla użytkownika. |
| Wartości parametru UserState |Stan użytkownika oczekuje na zatwierdzenie/PendingAcceptance/zaakceptowany/PendingVerification. |
| UserStateChangedOn |Sygnatura czasowa ostatniej zmiany wartości parametru UserState. Użyty do wyzwolenia cyklu życia przepływów pracy. |
| UserType |Typ użytkownika. Element członkowski (0), gościa (1), Viral(2). |

## <a name="update-group-attributes"></a>Atrybuty "Grupa aktualizacji"
| Atrybut | Opis |
| --- | --- |
| Klasyfikacja |Klasyfikacja grupy Unified (o dużym znaczeniu Biznesowym, MBI itp.). |
| Opis |Czytelny dla człowieka opisową fraz o obiekcie. |
| Nazwa wyświetlana |Nazwa wyświetlana dla obiekt |
| DirSyncEnabled |Wskazuje, czy z autorytatywnych synchronizacji katalogu (nabywca, lokalnych). |
| GroupLicenseAssignment |Przypisanie licencji grupy |
| GroupType |Typ grupy, Unified (0) |
| IsMembershipRuleLocked |Wskazuje, że właściwość MembershipRule jest ustawiana przez usługę zarządzania grupami samoobsługi i nie może zostać zmienione przez użytkowników. Zastosowanie tylko do grup, których GroupType zawiera GroupType.DynamicMembership |
| IsPublic |Flaga wskazująca, czy grupa jest publiczny/prywatny. |
| LastDirSyncTime |Czas ostatniego obiekt został zaktualizowany w wyniku synchronizowanie z autorytatywnych katalogu (lokalnie klienta). |
| Poczta |Podstawowy adres e-mail |
| MailEnabled |Wskazuje, czy ta grupa ma obsługi poczty e-mail. |
| mailNickname |Moniker dla obiekt książki adresów, zwykle część nazwy e-mail poprzedniego "@" symbolu. |
| MembershipRule |Ciąg, przedstawiając kryteria używane przez usługę zarządzania grupami samoobsługi do określenia, które elementy Członkowskie powinny należeć do tej grupy. Zobacz też IsMembershipRuleLocked. Zastosowanie tylko do grup, których GroupType zawiera GroupType.DynamicMembership. |
| MembershipRuleProcessingState |Wartość wyliczenia zdefiniowanych przez usługę zarządzania grupami samoobsługi Definiowanie stanu członkostwa przetwarzania dla tej grupy. Zastosowanie tylko do grup, których GroupType zawiera GroupType.DynamicMembership. |
| ProxyAddresses |Adres, za pomocą której rozpoznano obiektu adresatów programu Exchange Server w systemie obcego poczty. |
| RenewedDateTime |Rekord sygnatury czasowej podczas ostatniego został odnowiony grupy. |
| Securityenabled musi |Wskazuje, czy członkostwo w grupie mogą wpływać na decyzje dotyczące autoryzacji. |
| WellKnownObject |Etykiety obiektu katalogu wyznaczenie go jako jeden z wstępnie zdefiniowanego zestawu. |

## <a name="update-device-attributes"></a>Atrybuty "Aktualizuj urządzenia"
| Atrybut | Opis |
| --- | --- |
| AccountEnabled |Wskazuje, czy podmiot zabezpieczeń może uwierzytelnić. |
| CloudAccountEnabled |Wskazuje, czy podmiot zabezpieczeń może uwierzytelnić. Gdy urządzenie jest zarządzany w siedzibie firmy i zapisywane przez usługę InTune. |
| CloudDeviceOSType |Typ urządzenia na podstawie systemu operacyjnego np. Windows RT, iOS. Gdy są ustawione przez usługi w chmurze (takich jak usługa Intune), ten atrybut staje się autorytatywne w katalogu dla DeviceOSType. |
| CloudDeviceOSVersion |Wersja systemu operacyjnego. Gdy są ustawione przez usługi w chmurze (takich jak usługa Intune), ten atrybut staje się autorytatywne w katalogu dla DeviceOSVersion. |
| CloudDisplayName |Wartość atrybutu LDAP Nazwa wyświetlana. Gdy są ustawione przez usługi w chmurze (takich jak usługa Intune), ten atrybut staje się autorytatywne w katalogu Nazwa wyświetlana. |
| CloudCreated |Wskazuje, czy obiekt został utworzony przez usługi w chmurze. |
| CompliantUntil |Do czasu, jaki urządzenie jest uznany za zgodnego. |
| DeviceMetadata |Niestandardowych metadanych dla urządzenia |
| DeviceObjectVersion |Ten atrybut służy do identyfikowania wersji schematu urządzenia. |
| DeviceOSType |Typ urządzenia na podstawie systemu operacyjnego np. Windows RT, iOS. Zapisane przez usługę rejestracji i mają zostać zaktualizowane przez zarządzania urządzeniami Przenośnymi zarządzania usługa lub STS jasny usługi zarządzania. |
| DeviceOSVersion |Wersja systemu operacyjnego. Zapisane przez usługę rejestracji i mają zostać zaktualizowane przez zarządzania urządzeniami Przenośnymi zarządzania usługa lub STS jasny usługi zarządzania. |
| DevicePhysicalIds |Wielowartościowy atrybut przeznaczone do przechowywania identyfikatorów urządzenia fizycznego. Może to obejmować identyfikatory systemu BIOS, modułu TPM odciski palców, sprzętu określonych identyfikatorów itp. |
| DirSyncEnabled |Wskazuje, czy z autorytatywnych (nabywca, lokalnie) synchronizacji katalogu. |
| Nazwa wyświetlana |Nazwa wyświetlana dla obiekt |
| IsCompliant |Ten atrybut służy do zarządzania stan zarządzania urządzeniem przenośnym urządzenia. |
| IsManaged |Ten atrybut służy wskazująca, że urządzenie jest zarządzane w chmurze zarządzanie urządzeniami przenośnymi. |
| LastDirSyncTime |Czas ostatniego obiekt został zaktualizowany ze względu na synchronizowanie z autorytatywnych katalogu (lokalnie klienta). |

## <a name="update-device-configuration-attributes"></a>Atrybuty "Aktualizuj konfigurację urządzenia"
| Atrybut | Opis |
| --- | --- |
| MaximumRegistrationInactivityPeriod |Maksymalna liczba dni, przez które urządzenie może być nieaktywne przed nią jest uważany za do usunięcia. |
| RegistrationQuota |Zasady pozwala ograniczyć liczbę dozwoloną dla pojedynczego użytkownika rejestracji urządzenia. |

## <a name="update-service-principal-configuration-attributes"></a>Atrybuty "Aktualizuj konfigurację główna usługi"
| Atrybut | Opis |
| --- | --- |
| AccountEnabled |Wskazuje, czy podmiot zabezpieczeń może uwierzytelnić. |
| Identyfikator AppPrincipalId |Tożsamość zewnętrznych, zdefiniowane przez aplikację dla podmiotu zabezpieczeń. |
| Nazwa wyświetlana |Nazwa wyświetlana dla obiekt |
| ServicePrincipalName |Główną nazwę usługi, zawierający "Nazwa/urząd" gdzie nazwa określa wartość klasy aplikacji, a urząd zawiera co najmniej nazwę hosta [: port] lub "name" określający identyfikator dla nazwy głównej usługi. |

## <a name="update-app-attributes"></a>Atrybuty "Aktualizuj aplikacji"
| Atrybut | Opis |
| --- | --- |
| AppAddress |Zbiór adresów (adresy URL przekierowania), które są przypisane do nazwy głównej usługi. |
| Identyfikator aplikacji |Identyfikator aplikacji w aplikacji |
| AppIdentifierUri |Aplikacja identyfikator URI, który identyfikuje aplikację.  Zazwyczaj jest adres URL dostępu do aplikacji. |
| AppLogoUrl |Adres url obrazu logo aplikacji, które są przechowywane w sieci CDN. |
| AvailableToOtherTenants |Wartość true, aplikacja jest aplikacją wielodostępne (tj. mogą być używane przez innych dzierżawców). |
| Nazwa wyświetlana |Nazwa wyświetlana nazwa aplikacji |
| Uprawnienia |Lista aplikacji uprawnień. |
| ExternalUserAccountDelegationsAllowed |Flaga wskazująca, czy aplikacja zasobów jest zaufany i można tworzyć wpisów delegowania dla kont użytkowników zewnętrznych. |
| GroupMembershipClaims |Członkostwo w grupie oświadczeń zasad. |
| PublicClient |Wartość true, jeśli klient nie może przechowywać tajne (tj. jawne klienta w OAuth2.0) |
| RecordConsentConditions |Typy warunków zgody, zgodnie z warunkami umowy: Brak (0), SilentConsentForPartnerManagedApp(1). Ta wartość będzie widoczne w schemacie interfejsu API programu Graph i mogą być tylko zestaw/zmieniony przez administratorów dzierżawy. |
| RequiredResourceAccess |Zawartości XML wartość właściwości RequiredResourceAccess. |
| Aplikacja sieci Web |Wartość true wskazuje, że ta aplikacja jest aplikacji sieci web. |
| WwwHomepage |Podstawowy strony sieci Web. |

## <a name="update-role-attributes"></a>Atrybuty "Aktualizuj rolę"
| Atrybut | Opis |
| --- | --- |
| AppAddress |Zbiór adresów (adresy URL przekierowania), które są przypisane do nazwy głównej usługi. |
| BelongsToFirstLoginObjectSet |Wartość true wskazuje, że ten obiekt należy do zestawu obiektów wymagane do włączenia logowania administratora pierwszy z nowym dzierżawcą. |
| Wbudowane |Wskazuje, czy okres istnienia obiektu jest własnością systemu. |
| Opis |Czytelny dla człowieka opisową fraz o obiekcie. |
| Nazwa wyświetlana |Nazwa wyświetlana dla obiekt |
| mailNickname |Moniker dla obiekt książki adresów, zwykle część nazwy e-mail poprzedniego "@" symbolu. |
| RoleDisabled |Wskazuje, czy rola powinny być ignorowane na potrzeby kontroli dostępu. |
| RoleTemplateId |Tożsamość szablonu roli. |
| ServiceInfo |Specyficzne dla usługi informacje inicjowania obsługi administracyjnej może być zużyte przez MOAC i/lub innych wystąpień usługi (typu tego samego lub innego usługi). |
| TaskSetScopeReference |Identyfikuje TaskSet i zestaw zakresy skojarzone z rolą lub szablonów RoleTemplate. |
| ValidationError |Informacje o opublikowane przez usługę federacyjną opisujące nieprzejściowego, specyficzne dla usługi błąd dotyczący właściwości lub łącze od działania administratora obiektu w celu rozwiązania. |
| WellKnownObject |Etykiety obiektu katalogu wyznaczenie go jako jeden z wstępnie zdefiniowanego zestawu. |

## <a name="update-role-definition-attributes"></a>Atrybuty "Aktualizuj definicji roli"
| Atrybut | Opis |
| --- | --- |
| AssignableScopes |Kolekcja zakresów autoryzacji, które można odwoływać się podczas przypisywania tej definicji RoleDefinition do podmiotu zabezpieczeń. |
| Nazwa wyświetlana |Nazwa wyświetlana dla obiekt |
| GrantedPermissions |Uprawnienia przyznane przez tej definicji RoleDefinition. |

## <a name="update-administrative-unit-attributes"></a>Atrybuty "Aktualizuj jednostki administracyjne"
| Atrybut | Opis |
| --- | --- |
| Opis |Ta właściwość jest aktualizowany po zmianie opis jednostki administracyjne. |
| Nazwa wyświetlana |Ta właściwość jest aktualizowany po zmianie nazwy jednostki administracyjne. |

## <a name="update-company-attributes"></a>Atrybuty "Firmy aktualizacji"
| Atrybut | Opis |
| --- | --- |
| AllowedDataLocation |Lokalizacja, w którym firmy użytkownicy mogą być udostępniane. |
| AuthorizedServiceInstance |Nazwy wystąpień usługi, do których można wdrożyć plan. |
| DirSyncEnabled |Wskazuje, czy z autorytatywnych (nabywca, lokalnie) synchronizacji katalogu. |
| DirSyncStatus |Wskazuje, czy synchronizacja adres książki obiektów w tym kontekście dzierżawy autorytatywne (klientów lokalnie) katalogu. rozszerzenie właściwości DirSyncEnabled obiektów firmy. |
| DirSyncFeatures |Flaga bitowa do śledzenia zestaw funkcji dirsync włączonych i wyłączonych dla dzierżawcy. |
| DirectoryFeatures |Funkcje katalogu włączone/wyłączone. |
| DirSyncConfiguration |Zawiera wszystkie specyficzne dla dzierżawy bieżącej konfiguracji narzędzia DirSync. |
| Nazwa wyświetlana |Nazwa wyświetlana dla obiekt |
| IsMnc |Flaga wartości logicznej ustawioną "wartość" ("true", jeśli firma jest włączona funkcja międzynarodową firmą. |
| ObjectSettings |Kolekcja ustawienia są stosowane w zakresie obiektu. |
| PartnerCommerceUrl |Adres URL do witryny commerce partnera. |
| PartnerHelpUrl |Adres URL witryny pomocy partnera. |
| PartnerSupportEmail |Adres URL do partnera adres e-mail pomocy technicznej. |
| PartnerSupportTelephone |Adres URL do partnera telefonu pomocy technicznej. |
| PartnerSupportUrl |Adres URL w witrynie pomocy technicznej partnera. |
| StrongAuthenticationDetails |Szczegółowe informacje związane z StrongAuthentication. |
| StrongAuthenticationPolicy |Silne uwierzytelnianie zasad dla firmy. |
| TechnicalNotificationMail |Adres e-Mail, aby powiadomić problemów technicznych dotyczących firmy. |
| TelephoneNumber |Numery telefonów, które są zgodne z ITU E.123 zalecenia. |
| TenantType |Typ dzierżawcy. Jeśli ta wartość nie jest określona, dzierżawcy jest firmą. W przeciwnym razie możliwe wartości to: MicrosoftSupport (0), SyndicatePartner (1), ValueAddedResellerPartnerDelegatedAdmin ResellerPartnerDelegatedAdmin (4) BreadthPartnerDelegatedAdmin (3) BreadthPartner [2] [5]. |
| VerifiedDomain |Zestaw nazw domen DNS, powiązany z firmy. |

## <a name="update-domain-attributes"></a>Atrybuty "Aktualizuj domeny"
| Atrybut | Opis |
| --- | --- |
| Możliwości |Bit flagi opisujące możliwości domeny, jeśli istnieje. |
| Domyślne |Wskazuje, czy domena jest wartością domyślną; na przykład UserPrincipalName domyślny sufiks gdy administrator tworzy nowego użytkownika w MOAC. |
| Początkowa |Wskazuje, czy domena jest domena początkowa dla firmy, przydzielony przez OCP. Domena początkowa jest unikatowy domeny podrzędne domeny Online firmy Microsoft; e.g.contoso3.microsoftonline.com. |
| LiveType |Typ odpowiedniego identyfikatora Windows Live przestrzeni nazw, jeśli istnieje. |
| Nazwa |Identyfikator dla punktu końcowego. |
| PasswordNotificationWindowDays |Liczba dni do wygaśnięcia hasła użytkownik zostanie powiadomiony. |
| PasswordValidityPeriodDays |Liczba dni, przez które hasła jest dobra dla, należy zmienić. |

Rekordy inspekcji są wymaganej kontrolki do wielu przepisy dotyczące zgodności. Dla klientów korzystających z usługi Azure Active Directory inspekcji raportu do spełnienia ich przepisy dotyczące zgodności zaleca się, że klient przesłać kopię tego tematu pomocy kopię raportu inspekcji wyeksportowanego przez klienta w celu lepszego objaśnienia szczegóły raportu. Audytor chcą poznać przepisy dotyczące zgodności, które Azure obecnie spełnia, bezpośrednie kontrolera do [strony zgodności](https://azure.microsoft.com/support/trust-center/compliance/) programu Microsoft Azure Trust Center.

