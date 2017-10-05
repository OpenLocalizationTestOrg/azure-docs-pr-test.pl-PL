---
title: "Na podstawie atrybutów dynamiczne członkostwo w grupie w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Tworzenie zaawansowanych reguł w tym członkostwa grupy dynamicznej obsługiwane wyrażenie operatorami reguł i parametry."
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
ms.openlocfilehash: f4d9a08551d616ff98bc8734cbeec01d6e0d04ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a>Utwórz zasady na podstawie atrybutów dynamiczne członkostwo w grupie w usłudze Azure Active Directory
W usłudze Azure Active Directory (Azure AD) można utworzyć reguł zaawansowanych, aby włączyć złożonych opartych na atrybutach dynamiczne zarządzanie członkostwem w grupach. W tym artykule szczegółowo atrybuty i składni, aby utworzyć reguły członkostwa dynamicznych dla użytkowników lub urządzeń.

Po zmianie wszystkie atrybuty użytkowników lub urządzeń, system ocenia wszystkie reguły dynamicznej grupy w katalogu, aby sprawdzić, czy spowoduje zmianę żadnej grupy dodaje lub usuwa. Jeśli użytkownik lub urządzenie spełnia zasady grupy, zostaną dodane jako członkiem tej grupy. Jeśli nie spełniają reguły, zostaną usunięte.

> [!NOTE]
> - Możesz skonfigurować reguły dynamicznego zarządzania członkostwem w grupach zabezpieczeń lub w grupach usługi Office 365.
>
> - Ta funkcja wymaga licencji usługi Azure AD Premium P1 dla każdego użytkownika został dodany do co najmniej jednej grupy dynamicznej.
>
> - Można utworzyć grupy dynamicznej dla urządzeń lub użytkowników, ale nie można utworzyć regułę, która zawiera zarówno obiektów użytkowników i urządzeń.

> - W tej chwili nie jest możliwe tworzenie grupy urządzeń w oparciu będącej właścicielem, jeśli atrybuty użytkownika. Reguły członkostwa urządzenie może odwoływać się tylko natychmiastowe atrybutów obiektów urządzeń w katalogu.

## <a name="to-create-an-advanced-rule"></a>Aby utworzyć regułę zaawansowane
1. Zaloguj się do [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym lub administratorem konta użytkownika.
2. Wybierz **użytkowników i grup**.
3. Wybierz **wszystkich grup**.

   ![Otwieranie bloku grupy](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. W **wszystkich grup**, wybierz pozycję **nową grupę**.

   ![Dodaj nową grupę](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. Na **grupy** bloku, wprowadź nazwę i opis dla nowej grupy. Wybierz **Typ członkostwa** albo **dynamiki** lub **dynamiczne urządzenia**, w zależności od tego, czy chcesz utworzyć regułę dla użytkowników lub urządzeń, a następnie wybierz **Zapytania dynamiczne dodawanie**. Dla atrybutów używana dla reguł urządzenia, zobacz [do tworzenia reguł obiekty urządzeń przy użyciu atrybutów](#using-attributes-to-create-rules-for-device-objects).

   ![Dodaj regułę członkostwo dynamiczne](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. Na **członkostwo dynamiczne reguły** bloku, wprowadź reguły do **członkostwo dynamiczne dodawanie reguły zaawansowanej** , naciśnij klawisz Enter, a następnie wybierz **Utwórz** u dołu blok.
7. Wybierz **Utwórz** na **grupy** bloku, aby utworzyć grupę.

## <a name="constructing-the-body-of-an-advanced-rule"></a>Konstruowanie treści zaawansowanej reguły
Zaawansowane zasady, która można tworzyć dla dynamiczne zarządzanie członkostwem w grupach jest zasadniczo wyrażenie binarne, która składa się z trzech części i otrzymywania wyników w wyniku wartość true lub false. Dostępne są następujące trzy części:

* Lewy parametr
* Operator binarny.
* Stała prawo

Zakończenie reguły zaawansowanej wygląda podobnie do następującej: (leftParameter binaryOperator "RightConstant"), gdzie otwierające i zamykające są opcjonalne dla całego wyrażenia binarne, podwójne cudzysłowy są opcjonalne również tylko wymagane przez prawo stała gdy jest ciąg i user.property jest składnia lewy parametr. Reguły zaawansowanej może zawierać więcej niż jednego wyrażenia binarne oddzielone i, -, lub i - operatorów logicznych nie.

Poniżej przedstawiono przykłady prawidłowo skonstruowanej reguł zaawansowanych:
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
Pełna lista obsługiwanych parametrów i operatorami reguł wyrażenia znajduje się w sekcjach poniżej. Dla atrybutów używana dla reguł urządzenia, zobacz [do tworzenia reguł obiekty urządzeń przy użyciu atrybutów](#using-attributes-to-create-rules-for-device-objects).

Całkowita długość treści zaawansowane reguły nie może przekraczać 2048 znaków.

> [!NOTE]
> Operacje ciągu i wyrażeń regularnych nie jest uwzględniana. Można także przeprowadzić sprawdzenia wartości Null, za pomocą $null jako stała, na przykład, user.department - eq $null.
> Ciągi zawierające oferty "powinny być zmienione znaczenie przy użyciu ' znaków, na przykład user.department - eq \`"Sprzedaż".

## <a name="supported-expression-rule-operators"></a>Obsługiwane wyrażenie operatorami reguł
W poniższej tabeli wymieniono wszystkie operatory obsługiwane wyrażenie reguły i ich składni, które mają być użyte w treści zaawansowanych reguł:

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

Poniżej przedstawiono wszystkie operatory na pierwszeństwo z niższym wyższy. Operatory w tym samym wierszu znajdują się w taki sam priorytet:
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
Wszystkich operatorów można używać z lub bez prefiksu łącznik. Nawiasy są wymagane tylko wtedy, gdy priorytet nie spełnia wymagań.
Na przykład:
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
odpowiada to:
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-the--in-and--notin-operators"></a>Przy użyciu w i notIn — operatory

Jeśli chcesz porównać wartości atrybutu użytkownika przed szereg różnych wartości można użyć w lub operatory - notIn. Oto przykład przy użyciu w operatorze:
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
Zwróć uwagę na użycie "[" i "]" na początku i na końcu listy wartości. Ten warunek ma wartość True, wartość równa user.department jednej z wartości na liście.


## <a name="query-error-remediation"></a>Korygowanie błąd zapytania
W poniższej tabeli przedstawiono potencjalne błędy i popraw je, jeśli występują one jak

| Błąd analizy zapytania | Błąd użycia | Poprawiony użycia |
| --- | --- | --- |
| Błąd: Atrybut nie jest obsługiwane. |(user.invalidProperty - eq "Value") |(user.department - eq "value")<br/>Właściwość powinna być zgodna z [obsługiwane listy właściwości](#supported-properties). |
| Błąd: Operator nie jest obsługiwany w atrybucie. |(user.accountEnabled — zawiera wartość true) |(user.accountEnabled - eq true)<br/>Właściwość jest typu boolean. Operatory obsługiwane (-eq lub - ne) na typ boolean z powyższej listy. |
| Błąd: Błąd kompilacji zapytania. |(user.department - eq "Sprzedaż") — a (user.department - eq "Marketing") (user.userPrincipalName-match "*@domain.ext") |(user.department - eq "Sprzedaż")- a (user.department - eq "Marketing")<br/>Operator logiczny powinna być zgodna z powyższej listy obsługiwanych właściwości. (user.userPrincipalName-odpowiada ". *@domain.ext") lub (user.userPrincipalName-odpowiada "@domain.ext$") błąd w wyrażeniu regularnym. |
| Błąd: Wyrażenie binarne nie jest w prawidłowym formacie. |(user.department-eq "Sprzedaż") (user.department - eq "Sprzedaż") (user.department-eq "Sprzedaż") |(true - eq user.accountEnabled)- a (user.userPrincipalName — zawiera "alias@domain")<br/>Kwerenda ma wiele błędów. Nawias nie w odpowiednim miejscu. |
| Błąd: Wystąpił nieznany błąd podczas konfigurowania członkostwo dynamiczne. |(user.accountEnabled - eq "True" i user.userPrincipalName — zawiera "alias@domain") |(true - eq user.accountEnabled)- a (user.userPrincipalName — zawiera "alias@domain")<br/>Kwerenda ma wiele błędów. Nawias nie w odpowiednim miejscu. |

## <a name="supported-properties"></a>Obsługiwanych właściwości
Wszystkie właściwości użytkownika, które można używać w zaawansowanych reguły są następujące:

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
| Poczty |Dowolna wartość ciągu lub $null (adresu SMTP użytkownika) |(user.mail - eq "value") |
| mailNickName |Dowolną wartość ciągu (poczty alias użytkownika) |(user.mailNickName - eq "value") |
| Telefon komórkowy |Dowolna wartość ciągu lub $null |(user.mobile - eq "value") |
| Identyfikator obiektu |Identyfikator GUID obiektu użytkownika |(user.objectId - eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | Lokalny identyfikator zabezpieczeń (SID) dla użytkowników, którzy zostały zsynchronizowane z lokalnymi do chmury. |(user.onPremisesSecurityIdentifier - eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
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

* -wszelkie (spełnione po co najmniej jeden element w kolekcji odpowiada warunek)
* -wszystkie (spełnione, kiedy wszystkie elementy w kolekcji zgodne z warunkiem)

| Właściwości | Wartości | Sposób użycia |
| --- | --- | --- |
| assignedPlans |Każdy obiekt w kolekcji udostępnia następujące właściwości ciągu: capabilityStatus, usługi, servicePlanId |user.assignedPlans — wszystkie (assignedPlan.servicePlanId - eq "efb87545-963c-4e0d-99df-69c6916d9eb0"- i assignedPlan.capabilityStatus - eq "Włączone") |

Właściwości wielowartościowe są kolekcje obiektów tego samego typu. Można użyć — wszystkie — wszystkie operatory i do zastosowania warunku, odpowiednio do jednego lub wszystkich elementów w kolekcji. Na przykład:

assignedPlans jest właściwością wielu wartościach, która wyświetla wszystkie plany usługi przypisane do użytkownika. Poniżej wyrażenie będzie Wybierz użytkowników, którzy mają usługi Exchange Online (Plan 2) planu obsługi, który jest również w stanie włączone:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(Identyfikator Guid identyfikuje planie usługi Exchange Online (Plan 2)).

> [!NOTE]
> Jest to przydatne, jeśli chcesz zidentyfikować wszystkich użytkowników, dla którego usługi Office 365 (lub innych usług Microsoft Online) funkcja została włączona, na przykład, do których zestaw zasad.

Poniższe wyrażenie będzie wybierz wszystkich użytkowników, którzy mają wszystkie planu usług, który jest skojarzony z usługą Intune (określanego przez nazwę usługi "SCO"):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Użyj wartości Null

Aby określić wartości null w regule, można użyć "null" lub $null. Przykład:
```
   user.mail –ne null
```
jest odpowiednikiem
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a>Atrybuty rozszerzenia oraz atrybuty niestandardowe
Atrybuty rozszerzenia oraz atrybuty niestandardowe są obsługiwane w regułach członkostwo dynamiczne.

Atrybuty rozszerzenia są synchronizowane z lokalną okna serwera AD i mieć format "ExtensionAttributeX", gdzie X jest równa 1 – 15.
Oto przykład regułę, która używa atrybutu rozszerzenia
```
(user.extensionAttribute15 -eq "Marketing")
```
Atrybuty niestandardowe są synchronizowane z lokalną AD systemu Windows Server lub połączonych aplikacji SaaS i format "user.extension_[GUID]\__ [Attribute]", gdzie [identyfikator GUID] jest unikatowy identyfikator aplikacji, która utworzyła w usłudze AAD atrybut w usłudze AAD i [Attribute] jest nazwa atrybutu, ponieważ został on utworzony.
Na przykład regułę, która korzysta z atrybutem niestandardowym
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
Nazwa atrybutu niestandardowego można znaleźć w katalogu, badając użytkowników atrybutu za pomocą Eksploratora wykres i wyszukiwania dla nazwy atrybutu.

## <a name="direct-reports-rule"></a>Reguła "Bezpośrednich podwładnych"
Można utworzyć grupę wszystkich bezpośrednich podwładnych menedżera. Menedżera bezpośrednich podwładnych zmiany w przyszłości, członkostwo w grupie zostanie automatycznie dostosowana.

> [!NOTE]
> 1. Aby reguła mogła działać, upewnij się, że **identyfikator menedżera** właściwość została poprawnie ustawiona dla użytkowników w dzierżawie. Bieżąca wartość dla użytkownika można sprawdzić na ich **karta Profil**.
> 2. Ta reguła obsługuje tylko **bezpośredniego** raportów. Obecnie nie jest możliwe tworzenie grupy zagnieżdżone hierarchii, np. grupy, która zawiera bezpośrednich podwładnych i ich raporty.

**Aby skonfigurować grupę**

1. Wykonaj kroki 1 – 5 z sekcji [do tworzenia zaawansowanych reguł](#to-create-the-advanced-rule)i wybierz **Typ członkostwa** z **dynamiczne użytkownika**.
2. Na **członkostwo dynamiczne reguły** bloku, wprowadź regułę przy użyciu następującej składni:

    *Bezpośrednich podwładnych dla "{obectID_of_manager}"*

    Przykład prawidłowy reguły:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is the objectID of the manager. The object ID can be found on manager's **Profile tab**.
3. Po zapisaniu reguły, wszyscy użytkownicy z określoną wartością Identyfikator menedżera zostanie dodany do grupy.

## <a name="using-attributes-to-create-rules-for-device-objects"></a>Aby utworzyć zasady obiekty urządzeń przy użyciu atrybutów
Można również utworzyć regułę, która wybiera obiekty urządzeń do członkostwa w grupie. Następujące atrybuty urządzenia mogą być używane.

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
 managementType | Zarządzanie urządzeniami Przenośnymi (dla urządzeń przenośnych)<br>Komputer (w przypadku komputerów zarządzanych przez agenta Komputerami z usługą Intune) | (device.managementType - eq "MDM")
 Jednostka organizacyjna | dowolną wartością ciągu pasującego do nazwy jednostki organizacyjnej, ustawione przez lokalnej usługi Active Directory | (device.organizationalUnit - eq "Komputerów Stanów Zjednoczonych")
 deviceId | prawidłowy identyfikator urządzenia usługi Azure AD | (device.deviceId - eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")
 Identyfikator obiektu | Identyfikator obiektu: nieprawidłowy usługi Azure AD |  (device.objectId 76ad43c9-32c5-45e8-a272-7b58b58f596d - eq")




## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o grupach w usłudze Azure Active Directory.

* [Zobacz istniejących grup](active-directory-groups-view-azure-portal.md)
* [Utwórz nową grupę i dodawanie członków](active-directory-groups-create-azure-portal.md)
* [Zarządzanie ustawieniami grupy](active-directory-groups-settings-azure-portal.md)
* [Zarządzanie członkostwami grup](active-directory-groups-membership-azure-portal.md)
* [Dynamiczne reguły dla użytkowników w grupie zarządzania](active-directory-groups-dynamic-membership-azure-portal.md)
