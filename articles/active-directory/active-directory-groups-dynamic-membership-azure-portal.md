---
title: "na podstawie aaaAttribute dynamiczne członkostwo w grupie w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toocreate zaawansowane zasady członkostwa w grupie dynamicznej łącznie z operatorami reguł obsługiwane wyrażenie i parametrami."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fb434cc2-9a91-4ebf-9753-dd81e289787e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cd06ed70433eff65401c67d7351d5dcc12a9dd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a>Utwórz zasady na podstawie atrybutów dynamiczne członkostwo w grupie w usłudze Azure Active Directory
W usłudze Azure Active Directory (Azure AD) można utworzyć reguły zaawansowane tooenable złożonych opartych na atrybutach dynamiczne zarządzanie członkostwem w grupach. W tym artykule szczegółowo hello atrybuty i składni toocreate członkostwo dynamiczne reguły dla użytkowników lub urządzeń.

Atrybuty zmiany użytkowników lub urządzeń, hello system ma wszystkie reguły grupy dynamicznej w toosee katalogu, jeśli spowoduje zmianę hello żadnej grupy dodaje lub usuwa. Jeśli użytkownik lub urządzenie spełnia zasady grupy, zostaną dodane jako członkiem tej grupy. Jeśli nie spełniają reguły hello, zostaną usunięte.

> [!NOTE]
> - Możesz skonfigurować reguły dynamicznego zarządzania członkostwem w grupach zabezpieczeń lub w grupach usługi Office 365.
>
> - Ta funkcja wymaga licencji usługi Azure AD Premium P1 dla każdego elementu członkowskiego tooat dodano co najmniej jedną dynamiczne grupy użytkowników.
>
> - Można utworzyć grupy dynamicznej dla urządzeń lub użytkowników, ale nie można utworzyć regułę, która zawiera zarówno obiektów użytkowników i urządzeń.

> - W momencie hello nie jest możliwe toocreate na będącej właścicielem, jeśli atrybuty użytkownika na podstawie grupy urządzeń. Urządzenie reguł członkostwa można tylko odwołanie do bezpośredniego atrybuty obiekty urządzeń w katalogu hello.

## <a name="toocreate-an-advanced-rule"></a>toocreate zaawansowanej reguły
1. Zaloguj się toohello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym lub administratorem konta użytkownika.
2. Wybierz **użytkowników i grup**.
3. Wybierz **wszystkich grup**.

   ![Otwieranie hello grup bloku](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. W **wszystkich grup**, wybierz pozycję **nową grupę**.

   ![Dodaj nową grupę](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. Na powitania **grupy** bloku, wprowadź nazwę i opis dla nowej grupy hello. Wybierz **Typ członkostwa** albo **dynamiki** lub **dynamiczne urządzenia**, w zależności od tego, czy ma być toocreate regułę dla użytkowników lub urządzeń, a następnie wybierz **Zapytania dynamiczne dodawanie**. Dla atrybutów hello używana dla reguł urządzenia, zobacz [przy użyciu reguł toocreate atrybuty obiektów urządzeń](#using-attributes-to-create-rules-for-device-objects).

   ![Dodaj regułę członkostwo dynamiczne](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. Na powitania **członkostwo dynamiczne reguły** bloku wejścia reguły hello **członkostwo dynamiczne dodawanie reguły zaawansowanej** , naciśnij klawisz Enter, a następnie wybierz **Utwórz** u dołu hello Witaj bloku.
7. Wybierz **Utwórz** na powitania **grupy** grupy hello toocreate bloku.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Konstruowanie hello treści zaawansowanej reguły
reguły zaawansowanej Hello utworzonego dla hello dynamiczne zarządzanie członkostwem w grupach jest zasadniczo wyrażenie binarne, która składa się z trzech części i otrzymywania wyników w wyniku wartość true lub false. dostępne są następujące trzy części Hello:

* Lewy parametr
* Operator binarny.
* Stała prawo

Zakończenie reguły zaawansowanej wygląda podobnie toothis: (leftParameter binaryOperator "RightConstant"), gdzie hello otwierające i zamykające nawiasy są opcjonalne dla całego wyrażenia binarne hello, podwójne cudzysłowy są opcjonalne również tylko wymagane przez prawo hello Stała przypadku parametry i składnia hello parametru po lewej stronie powitania jest user.property. Reguły zaawansowanej może zawierać więcej niż jednego wyrażenia binarne oddzielone hello- i, -, lub i - operatorów logicznych nie.

Witaj poniżej przedstawiono przykłady prawidłowo skonstruowanej reguł zaawansowanych:
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
Hello pełną listę obsługiwanych parametrów i operatorami reguł wyrażenia znajduje się w sekcjach poniżej. Dla atrybutów hello używana dla reguł urządzenia, zobacz [przy użyciu reguł toocreate atrybuty obiektów urządzeń](#using-attributes-to-create-rules-for-device-objects).

Całkowita długość Hello treści hello zaawansowane reguły nie może przekraczać 2048 znaków.

> [!NOTE]
> Operacje ciągu i wyrażeń regularnych nie jest uwzględniana. Można także przeprowadzić sprawdzenia wartości Null, za pomocą $null jako stała, na przykład, user.department - eq $null.
> Ciągi zawierające oferty "powinny być zmienione znaczenie przy użyciu ' znaków, na przykład user.department - eq \`"Sprzedaż".

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

Poniżej przedstawiono wszystkie operatory według priorytetu z niższym toohigher. Operatory w tym samym wierszu znajdują się w taki sam priorytet:
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
Wszystkich operatorów można używać z lub bez prefiksu łącznik hello. Nawiasy są wymagane tylko wtedy, gdy priorytet nie spełnia wymagań.
Na przykład:
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
odpowiada to:
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-hello--in-and--notin-operators"></a>Przy użyciu hello — w i notIn — operatory

Jeśli wartość hello toocompare atrybutu użytkownika przed szereg różnych wartości można użyć hello — w lub operatory - notIn. Oto przykład przy użyciu hello — w operatorze:
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
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
```
   user.mail –ne null
```
jest odpowiednikiem
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a>Atrybuty rozszerzenia oraz atrybuty niestandardowe
Atrybuty rozszerzenia oraz atrybuty niestandardowe są obsługiwane w regułach członkostwo dynamiczne.

Atrybuty rozszerzenia są synchronizowane z lokalną okna serwera AD i podejmij hello format "ExtensionAttributeX", gdzie X jest równa 1 – 15.
Oto przykład regułę, która używa atrybutu rozszerzenia
```
(user.extensionAttribute15 -eq "Marketing")
```
Atrybuty niestandardowe są synchronizowane z lokalną AD systemu Windows Server lub połączonych SaaS aplikacji i hello hello formacie "user.extension_[GUID]\__ [Attribute]", gdzie [identyfikator GUID] jest unikatowy identyfikator hello w usłudze AAD aplikacji hello który Atrybut hello utworzone w usłudze AAD i [Attribute] jest hello nazwa atrybutu hello, ponieważ został on utworzony.
Na przykład regułę, która korzysta z atrybutem niestandardowym
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
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
Można również utworzyć regułę, która wybiera obiekty urządzeń do członkostwa w grupie. można Hello następujące atrybuty urządzeń.

 Atrybut urządzenia  | Wartości | Przykład
 ----- | ----- | ----------------
 AccountEnabled | wartość true, false | (device.accountEnabled - eq true)
 Nazwa wyświetlana | Dowolną wartością ciągu |(device.displayName - eq "Tomasz Iphone")
 DeviceOSType | Dowolną wartością ciągu | (device.deviceOSType - eq "IOS")
 DeviceOSVersion | Dowolną wartością ciągu | (urządzenia. OSVersion - eq "9.1")
 deviceCategory | Nazwa kategorii prawidłowe urządzenie | (device.deviceCategory - eq "BYOD")
 DeviceManufacturer | Dowolną wartością ciągu | (device.deviceManufacturer - eq "Samsung")
 DeviceModel | Dowolną wartością ciągu | (device.deviceModel - eq "iPad lotniczego")
 deviceOwnership | Osobiste, firma | (device.deviceOwnership - eq "Firmy")
 domainName | Dowolną wartością ciągu | (device.domainName - eq "contoso.com")
 enrollmentProfileName | Nazwa profilu rejestracji urządzeń firmy Apple | (device.enrollmentProfileName - eq "DEP iPhone")
 isRooted | wartość true, false | (device.isRooted - eq true)
 managementType | Zarządzanie urządzeniami Przenośnymi (dla urządzeń przenośnych)<br>Komputer (w przypadku komputerów zarządzanych przez agenta Komputerami z usługą Intune hello) | (device.managementType - eq "MDM")
 Jednostka organizacyjna | dowolną wartością ciągu pasujących do nazwy hello hello jednostki organizacyjnej, ustawione przez lokalnej usługi Active Directory | (device.organizationalUnit - eq "Komputerów Stanów Zjednoczonych")
 deviceId | prawidłowy identyfikator urządzenia usługi Azure AD | (device.deviceId - eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")
 Identyfikator obiektu | Identyfikator obiektu: nieprawidłowy usługi Azure AD |  (device.objectId 76ad43c9-32c5-45e8-a272-7b58b58f596d - eq")




## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o grupach w usłudze Azure Active Directory.

* [Zobacz istniejących grup](active-directory-groups-view-azure-portal.md)
* [Utwórz nową grupę i dodawanie członków](active-directory-groups-create-azure-portal.md)
* [Zarządzanie ustawieniami grupy](active-directory-groups-settings-azure-portal.md)
* [Zarządzanie członkostwami grup](active-directory-groups-membership-azure-portal.md)
* [Dynamiczne reguły dla użytkowników w grupie zarządzania](active-directory-groups-dynamic-membership-azure-portal.md)
