---
title: "grupy aaaPopulate dynamicznie oparte na atrybutach obiektu w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak-aby toocreate zaawansowane zasady tym członkostwa grupy obsługiwane wyrażenie operatorami reguł i parametry."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 04813a42-d40a-48d6-ae96-15b7e5025884
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: fe22829118ed8f5137a619d93fa6f9bf80835863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="populate-groups-dynamically-based-on-object-attributes"></a>Wypełnianie grupy dynamicznie na podstawie obiektu atrybutów
Hello klasyczny portal Azure udostępnia hello tooenable możliwości bardziej złożonych opartych na atrybutach dynamiczne zarządzanie członkostwem w grupach usługi Azure Active Directory (Azure AD).  

Atrybuty zmiany użytkowników lub urządzeń, hello system ma wszystkie reguły grupy dynamicznej w toosee katalogu, jeśli spowoduje zmianę hello żadnej grupy dodaje lub usuwa. Jeśli użytkownik lub urządzenie spełnia zasady grupy, zostaną dodane jako członkiem tej grupy. Jeśli nie spełniają reguły hello, zostaną usunięte.

> [!NOTE]
> - Możesz skonfigurować reguły dynamicznego zarządzania członkostwem w grupach zabezpieczeń lub w grupach usługi Office 365.
>
> - Ta funkcja wymaga licencji usługi Azure AD Premium P1 dla każdego elementu członkowskiego tooat dodano co najmniej jedną dynamiczne grupy użytkowników.
>
> - Można utworzyć grupy dynamicznej dla urządzeń lub użytkowników, ale nie można utworzyć regułę, która zawiera zarówno obiektów użytkowników i urządzeń.

> - W momencie hello nie jest możliwe toocreate na będącej właścicielem, jeśli atrybuty użytkownika na podstawie grupy urządzeń. Urządzenie reguł członkostwa można tylko odwołanie do bezpośredniego atrybuty obiekty urządzeń w katalogu hello.

## <a name="toocreate-an-advanced-rule"></a>toocreate zaawansowanej reguły
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.
2. Wybierz hello **grup** kartę, a następnie otwórz hello grupę tooedit.
3. Wybierz hello **Konfiguruj** kartę, zaznacz hello **reguły zaawansowanej** opcji, a następnie wprowadź hello zaawansowane reguły do pola tekstowego hello.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Konstruowanie hello treści zaawansowanej reguły
reguły zaawansowanej Hello utworzonego dla hello dynamiczne zarządzanie członkostwem w grupach jest zasadniczo wyrażenie binarne, która składa się z trzech części i otrzymywania wyników w wyniku wartość true lub false. dostępne są następujące trzy części Hello:

* Lewy parametr
* Operator binarny.
* Stała prawo

Zakończenie reguły zaawansowanej wygląda podobnie toothis: (leftParameter binaryOperator "RightConstant"), gdzie hello otwierające i zamykające nawiasy są wymagane dla całego wyrażenia binarne hello, podwójne cudzysłowy są wymagane dla stała prawo hello i hello składni Lewy parametr hello jest user.property. Reguły zaawansowanej może zawierać więcej niż jednego wyrażenia binarne oddzielone hello- i, -, lub i - operatorów logicznych nie.
Witaj poniżej przedstawiono przykłady prawidłowo skonstruowanej reguł zaawansowanych:

* (user.department - eq "Sprzedaż")- lub (user.department - eq "Marketing")
* (user.department - eq "Sprzedaż")- i - nie (user.jobTitle — zawiera, "które integrują usługi")

Hello pełną listę obsługiwanych parametrów i operatorami reguł wyrażenia znajduje się w sekcjach poniżej.


Należy pamiętać, że właściwość hello musi być poprzedzona znakiem hello prawidłowy obiekt typu: użytkownik lub urządzenie.
Witaj poniżej reguły zakończy się niepowodzeniem sprawdzania poprawności hello: null — ne poczty

Reguła poprawne Hello mogą być następujące:

User.mail — ne wartości null

Całkowita długość Hello treści hello zaawansowane reguły nie może przekraczać 2048 znaków.

> [!NOTE]
> Parametry i wyrażeń regularnych operacji są bez uwzględniania wielkości liter.
> Ciągi zawierające oferty "powinny być zmienione znaczenie przy użyciu ' znaków, na przykład user.department - eq \`"Sprzedaż".
> Cudzysłowy należy używać tylko wartości typów ciągów i tylko oferty w języku angielskim.
>
>

## <a name="supported-expression-rule-operators"></a>Obsługiwane wyrażenie operatorami reguł
Hello Poniższa tabela zawiera listę wszystkich operatorów reguły wyrażenie hello obsługiwane i ich toobe składni używane w treści hello hello zaawansowanych reguł:

| Operator | Składnia |
| --- | --- |
| Nie równa się |-ne |
| równa się |-eq |
| Nie rozpoczyna się od |-notStartsWith |
| Rozpoczyna się od |-startsWith |
| Nie zawiera |-notContains |
| Contains |-zawiera |
| Nie pasują do siebie |-notMatch |
| dopasowanie |-zgodne |
| W | -w |
| Nie w | -notIn |

## <a name="operator-precedence"></a>Kolejność wykonywania działań

Wszystkich operatorów poniżej wymieniono na pierwszeństwo z niższym toohigher, operator w tym samym wierszu znajdują się w taki sam priorytet — żadnych - all - lub - i - nie - eq - No - startsWith — notStartsWith — zawiera - notContains — odpowiada notMatch — — w notIn —

Wszystkich operatorów można używać z lub bez prefiksu łącznik.

Należy pamiętać, że nawiasy nie są zawsze potrzebne tylko potrzebne nawias tooadd pierwszeństwo nie spełnia wymagań dotyczących na przykład:

   User.Department-eq "Marketing" — i user.country-eq "PL"

odpowiada to:

   (user.department-eq "Marketingowych") — a (user.country-eq "PL")

## <a name="using-hello--in-and--notin-operators"></a>Przy użyciu hello — w i notIn — operatory

Jeśli wartość hello toocompare atrybutu użytkownika przed szereg różnych wartości można użyć hello — w lub operatory - notIn. Oto przykład przy użyciu hello — w operatorze:

    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]

Należy zwrócić uwagę użycie hello hello "[" i "]" na powitania początek i koniec hello listy wartości. Warunek tooTrue hello wartość równa user.department jednej wartości hello liście hello.

## <a name="query-error-remediation"></a>Korygowanie błąd zapytania
Witaj Poniższa tabela zawiera listę potencjalnych błędów i w jaki sposób toocorrect je, jeśli występują one

| Błąd analizy zapytania | Błąd użycia | Poprawiony użycia |
| --- | --- | --- |
| Błąd: Atrybut nie jest obsługiwane. |(user.invalidProperty - eq "Value") |(user.department - eq "value")<br/>Właściwość powinna być zgodna z hello [obsługiwane listy właściwości](#supported-properties). |
| Błąd: Operator nie jest obsługiwany w atrybucie. |(user.accountEnabled — zawiera wartość true) |(user.accountEnabled - eq true)<br/>Właściwość jest typu boolean. Operatory obsługiwane hello (-eq lub - ne) na typ boolean z hello powyżej listy. |
| Błąd: Błąd kompilacji zapytania. |(user.department - eq "Sprzedaż") — a (user.department - eq "Marketing") (user.userPrincipalName-match "*@domain.ext") |(user.department - eq "Sprzedaż")- a (user.department - eq "Marketing")<br/>Operator logiczny powinna być zgodna z powyższej listy właściwości hello obsługiwane. (user.userPrincipalName-odpowiada ". *@domain.ext") lub (user.userPrincipalName-odpowiada "@domain.ext$") błąd w wyrażeniu regularnym. |
| Błąd: Wyrażenie binarne nie jest w prawidłowym formacie. |(user.department-eq "Sprzedaż") (user.department - eq "Sprzedaż") (user.department-eq "Sprzedaż") |(true - eq user.accountEnabled)- a (user.userPrincipalName — zawiera "alias@domain")<br/>Kwerenda ma wiele błędów. Nawias nie w odpowiednim miejscu. |
| Błąd: Wystąpił nieznany błąd podczas konfigurowania członkostwo dynamiczne. |(user.accountEnabled - eq "True" i user.userPrincipalName — zawiera "alias@domain") |(true - eq user.accountEnabled)- a (user.userPrincipalName — zawiera "alias@domain")<br/>Kwerenda ma wiele błędów. Nawias nie w odpowiednim miejscu. |

## <a name="supported-properties"></a>Obsługiwanych właściwości
wszystkie właściwości hello użytkownika, które można używać w zaawansowanych reguły są następujące Hello:

### <a name="properties-of-type-boolean"></a>Właściwości typu boolean
Dozwolonych operatorów

* -eq
* -ne

| Właściwości | Dozwolone wartości | Sposób użycia |
| --- | --- | --- |
| AccountEnabled |wartość true, false |true - eq user.accountEnabled |
| DirSyncEnabled |wartość true, false |true - eq user.dirSyncEnabled |

### <a name="properties-of-type-string"></a>Właściwości typu String
Dozwolonych operatorów

* -eq
* -ne
* -notStartsWith
* -StartsWith
* -zawiera
* -notContains
* -zgodne
* -notMatch
* -w
* -notIn

| Właściwości | Dozwolone wartości | Sposób użycia |
| --- | --- | --- |
| city |Dowolna wartość ciągu lub $null |(user.city - eq "value") |
| Kraju |Dowolna wartość ciągu lub $null |(user.country - eq "value") |
| Nazwa firmy | Dowolna wartość ciągu lub $null | (user.companyName - eq "value") |
| Dział |Dowolna wartość ciągu lub $null |(user.department - eq "value") |
| Nazwa wyświetlana |Dowolną wartością ciągu |(user.displayName - eq "value") |
| facsimileTelephoneNumber |Dowolna wartość ciągu lub $null |(user.facsimileTelephoneNumber - eq "value") |
| Imię |Dowolna wartość ciągu lub $null |(user.givenName - eq "value") |
| Stanowisko |Dowolna wartość ciągu lub $null |(user.jobTitle - eq "value") |
| Poczty |Dowolna wartość ciągu lub $null (adresu SMTP użytkownika hello) |(user.mail - eq "value") |
| mailNickName |Dowolną wartość ciągu (alias wiadomości powitania użytkownika) |(user.mailNickName - eq "value") |
| Telefon komórkowy |Dowolna wartość ciągu lub $null |(user.mobile - eq "value") |
| Identyfikator obiektu |Identyfikator GUID obiektu użytkownika hello |(user.objectId - eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | Lokalny identyfikator zabezpieczeń (SID) dla użytkowników, którzy są synchronizowane z lokalnej toohello chmury. |(user.onPremisesSecurityIdentifier - eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |Brak DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies - eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |Dowolna wartość ciągu lub $null |(user.physicalDeliveryOfficeName - eq "value") |
| KodPocztowy |Dowolna wartość ciągu lub $null |(user.postalCode - eq "value") |
| preferredLanguage |Kod ISO 639-1 |(user.preferredLanguage - eq "pl pl") |
| sipProxyAddress |Dowolna wartość ciągu lub $null |(user.sipProxyAddress - eq "value") |
| state |Dowolna wartość ciągu lub $null |(user.state - eq "value") |
| Adres |Dowolna wartość ciągu lub $null |(user.streetAddress - eq "value") |
| nazwisko |Dowolna wartość ciągu lub $null |(user.surname - eq "value") |
| TelephoneNumber |Dowolna wartość ciągu lub $null |(user.telephoneNumber - eq "value") |
| usageLocation |Kod kraju własną literą dwóch |(user.usageLocation - eq "PL") |
| userPrincipalName |Dowolną wartością ciągu |(user.userPrincipalName - eq "alias@domain") |
| UserType |element członkowski gościa $null |(user.userType - eq "Elementu członkowskiego") |

### <a name="properties-of-type-string-collection"></a>Właściwości typu kolekcji ciągów
Dozwolonych operatorów

* -zawiera
* -notContains

| Właściwości | Dozwolone wartości | Sposób użycia |
| --- | --- | --- |
| otherMails |Dowolną wartością ciągu |(user.otherMails — zawiera "alias@domain") |
| proxyAddresses |SMTP: alias@domain smtp:alias@domain |(user.proxyAddresses — zawiera "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>Właściwości wielu wartości
Dozwolonych operatorów

* -wszelkie (spełniony, gdy co najmniej jeden element w kolekcji hello spełnia warunek hello)
* -wszystkie (spełnione, gdy wszystkie elementy w kolekcji hello zgodne warunku hello)

| Właściwości | Wartości | Sposób użycia |
| --- | --- | --- |
| assignedPlans |Każdy obiekt w kolekcji hello uwidacznia następujące właściwości ciąg hello: capabilityStatus, usługi, servicePlanId |user.assignedPlans — wszystkie (assignedPlan.servicePlanId - eq "efb87545-963c-4e0d-99df-69c6916d9eb0"- i assignedPlan.capabilityStatus - eq "Włączone") |

Właściwości wielowartościowe są kolekcje obiektów hello tego samego typu. Można użyć - wszelkich i - wszystkie tooapply operatory tooone warunku lub wszystkich hello elementów w kolekcji hello odpowiednio. Na przykład:

assignedPlans jest właściwością wielu wartościach, która wyświetla wszystkie plany usługi przypisany użytkownik toohello. Witaj poniżej wyrażenie będzie Wybierz użytkowników, którzy mają hello usługi Exchange Online (Plan 2) usługa plan, który również jest w stanie włączone:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(identyfikator Guid hello identyfikuje plan usługi Exchange Online (Plan 2) hello).

> [!NOTE]
> Jest to przydatne w przypadku tooidentify wszystkich użytkowników dla którego usługi Office 365 (lub innych usług Microsoft Online) funkcja została włączona, na przykład tootarget z zestawu zasad.

Witaj poniższe wyrażenie będzie wybierz wszystkich użytkowników, którzy mają każdego planu usługi skojarzony z hello usługi Intune (określanego przez nazwę usługi "SCO"):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Użyj wartości Null

toospecify wartość null w regule, można użyć "null" lub $null. Przykład:

   User.mail — ne wartość null jest odpowiednikiem user.mail — ne $null

## <a name="extension-attributes-and-custom-attributes"></a>Atrybuty rozszerzenia oraz atrybuty niestandardowe
Atrybuty rozszerzenia oraz atrybuty niestandardowe są obsługiwane w regułach członkostwo dynamiczne.

Atrybuty rozszerzenia są synchronizowane z lokalną okna serwera AD i podejmij hello format "ExtensionAttributeX", gdzie X jest równa 1 – 15.
Oto przykład regułę, która używa atrybutu rozszerzenia

(user.extensionAttribute15 - eq "marketingowych")

Atrybuty niestandardowe są synchronizowane z lokalną AD systemu Windows Server lub połączonych SaaS aplikacji i hello hello formacie "user.extension_[GUID]\__ [Attribute]", gdzie [identyfikator GUID] jest unikatowy identyfikator hello w usłudze AAD aplikacji hello który Atrybut hello utworzone w usłudze AAD i [Attribute] jest hello nazwa atrybutu hello, ponieważ został on utworzony.
Na przykład regułę, która korzysta z atrybutem niestandardowym

User.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  

Witaj nazwie atrybutu niestandardowego można znaleźć w katalogu hello badając użytkowników atrybutu za pomocą Eksploratora wykres i wyszukiwania dla nazwy atrybutu hello.

## <a name="direct-reports-rule"></a>Reguła "Bezpośrednich podwładnych"
Można utworzyć grupę wszystkich bezpośrednich podwładnych menedżera. Menedżer hello bezpośrednich podwładnych zmiany w przyszłości hello, członkostwo w grupie hello zostanie automatycznie korygowane.

> [!NOTE]
> 1. Dla toowork reguły hello, upewnij się, że hello **identyfikator menedżera** właściwość została poprawnie ustawiona dla użytkowników w dzierżawie. Możesz sprawdzić hello bieżąca wartość dla użytkownika na ich **karta Profil**.
> 2. Ta reguła obsługuje tylko **bezpośredniego** raportów. Obecnie nie jest możliwe toocreate grupy zagnieżdżone hierarchii, np. grupy, która zawiera bezpośrednich podwładnych i ich raporty.

**tooconfigure hello grupy**

1. Wykonaj kroki 1 – 5 z sekcji [reguły zaawansowanej toocreate hello](#to-create-the-advanced-rule)i wybierz **Typ członkostwa** z **dynamiczne użytkownika**.
2. Na powitania **członkostwo dynamiczne reguły** bloku, wprowadź hello reguły z hello następującej składni:

    *Bezpośrednich podwładnych dla "{obectID_of_manager}"*

    Przykład prawidłowy reguły:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. Po zapisaniu hello reguły, wszyscy użytkownicy z hello określony ma zostać dodana wartość Identyfikatora Menedżera toohello grupy.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>Przy użyciu reguł toocreate atrybuty obiektów urządzeń
Można również utworzyć regułę, która wybiera obiekty urządzeń do członkostwa w grupie. Witaj następujące atrybuty urządzenia mogą być używane:

| Właściwości              | Dozwolone wartości                  | Sposób użycia                                                       |
|-------------------------|---------------------------------|-------------------------------------------------------------|
| AccountEnabled          | wartość true, false                      | (device.accountEnabled - eq true)                            |
| Nazwa wyświetlana             | Dowolną wartością ciągu                | (device.displayName - eq "Tomasz Iphone")                       |
| DeviceOSType            | Dowolną wartością ciągu                | (device.deviceOSType - eq "IOS")                             |
| DeviceOSVersion         | Dowolną wartością ciągu                | (urządzenia. OSVersion - eq "9.1")                                |
| deviceCategory          | Dowolną wartością ciągu                | (device.deviceCategory - eq "")                              |
| DeviceManufacturer      | Dowolną wartością ciągu                | (device.deviceManufacturer - eq "Microsoft")                 |
| DeviceModel             | Dowolną wartością ciągu                | (device.deviceModel - eq "IPhone 7 +")                        |
| deviceOwnership         | Dowolną wartością ciągu                | (device.deviceOwnership - eq "")                             |
| domainName              | Dowolną wartością ciągu                | (device.domainName - eq "contoso.com")                       |
| enrollmentProfileName   | Dowolną wartością ciągu                | (device.enrollmentProfileName - eq "")                       |
| isRooted                | wartość true, false                      | (device.deviceOSType - eq true)                              |
| managementType          | Dowolną wartością ciągu                | (device.managementType - eq "")                              |
| Jednostka organizacyjna      | Dowolną wartością ciągu                | (device.organizationalUnit - eq "")                          |
| deviceId                | Nieprawidłowy identyfikator urządzenia                | (device.deviceId - eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d") |
| Identyfikator obiektu                | Nieprawidłowa objectId AAD            | (device.objectId - eq "76ad43c9-32c5-45e8-a272-7b58b58f596d") |

> [!NOTE]
> Reguły te urządzenia nie można utworzyć za pomocą listy rozwijanej "Prosta reguła" hello w hello klasycznego portalu Azure.
>
>

## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Rozwiązywanie problemów z dynamiczne zarządzanie członkostwem w grupach](active-directory-accessmanagement-troubleshooting.md)
* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
