---
title: "Wypełnianie grupy dynamicznie oparte na atrybutach obiektu w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak — do obiektu tworzenie zaawansowanych reguł w tym członkostwa grupy obsługiwane wyrażenie operatorami reguł i parametry."
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
ms.openlocfilehash: b9b5ddf42958a2b4e241d0252101d979009e7dc0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="populate-groups-dynamically-based-on-object-attributes"></a>Wypełnianie grupy dynamicznie na podstawie obiektu atrybutów
Klasyczny portal Azure udostępnia możliwość włączenia bardziej złożonych opartych na atrybutach dynamiczne zarządzanie członkostwem w grupach usługi Azure Active Directory (Azure AD).  

Po zmianie wszystkie atrybuty użytkowników lub urządzeń, system ocenia wszystkie reguły dynamicznej grupy w katalogu, aby sprawdzić, czy spowoduje zmianę żadnej grupy dodaje lub usuwa. Jeśli użytkownik lub urządzenie spełnia zasady grupy, zostaną dodane jako członkiem tej grupy. Jeśli nie spełniają reguły, zostaną usunięte.

> [!NOTE]
> - Możesz skonfigurować reguły dynamicznego zarządzania członkostwem w grupach zabezpieczeń lub w grupach usługi Office 365.
>
> - Ta funkcja wymaga licencji usługi Azure AD Premium P1 dla każdego użytkownika został dodany do co najmniej jednej grupy dynamicznej.
>
> - Można utworzyć grupy dynamicznej dla urządzeń lub użytkowników, ale nie można utworzyć regułę, która zawiera zarówno obiektów użytkowników i urządzeń.

> - W tej chwili nie jest możliwe tworzenie grupy urządzeń w oparciu będącej właścicielem, jeśli atrybuty użytkownika. Reguły członkostwa urządzenie może odwoływać się tylko natychmiastowe atrybutów obiektów urządzeń w katalogu.

## <a name="to-create-an-advanced-rule"></a>Aby utworzyć regułę zaawansowane
1. W [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.
2. Wybierz **grup** karcie, a następnie otwórz grupę, którą chcesz edytować.
3. Wybierz **Konfiguruj** wybierz opcję **reguły zaawansowanej** opcji, a następnie wprowadź zaawansowane reguły do pola tekstowego.

## <a name="constructing-the-body-of-an-advanced-rule"></a>Konstruowanie treści zaawansowanej reguły
Zaawansowane zasady, która można tworzyć dla dynamiczne zarządzanie członkostwem w grupach jest zasadniczo wyrażenie binarne, która składa się z trzech części i otrzymywania wyników w wyniku wartość true lub false. Dostępne są następujące trzy części:

* Lewy parametr
* Operator binarny.
* Stała prawo

Zakończenie reguły zaawansowanej wygląda podobnie do następującej: (leftParameter binaryOperator "RightConstant"), gdzie otwierające i zamykające są wymagane do całego wyrażenia binarne, podwójne cudzysłowy są wymagane dla prawo stała oraz składni Lewy parametr jest user.property. Reguły zaawansowanej może zawierać więcej niż jednego wyrażenia binarne oddzielone i, -, lub i - operatorów logicznych nie.
Poniżej przedstawiono przykłady prawidłowo skonstruowanej reguł zaawansowanych:

* (user.department - eq "Sprzedaż")- lub (user.department - eq "Marketing")
* (user.department - eq "Sprzedaż")- i - nie (user.jobTitle — zawiera, "które integrują usługi")

Pełna lista obsługiwanych parametrów i operatorami reguł wyrażenia znajduje się w sekcjach poniżej.


Należy pamiętać, że właściwość musi być poprzedzona znakiem prawidłowy obiekt typu: użytkownik lub urządzenie.
Poniżej reguły zakończy się niepowodzeniem sprawdzania poprawności: null — ne poczty

Prawidłowa reguła będzie:

User.mail — ne wartości null

Całkowita długość treści zaawansowane reguły nie może przekraczać 2048 znaków.

> [!NOTE]
> Parametry i wyrażeń regularnych operacji są bez uwzględniania wielkości liter.
> Ciągi zawierające oferty "powinny być zmienione znaczenie przy użyciu ' znaków, na przykład user.department - eq \`"Sprzedaż".
> Cudzysłowy należy używać tylko wartości typów ciągów i tylko oferty w języku angielskim.
>
>

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

Wszystkich operatorów poniżej wymieniono na pierwszeństwo z niższych do wyższych, operator w tym samym wierszu znajdują się w taki sam priorytet — żadnych - all - lub - i - nie - eq - No - startsWith — notStartsWith — zawiera - notContains — odpowiada notMatch — — w notIn —

Wszystkich operatorów można używać z lub bez prefiksu łącznik.

Należy pamiętać, że nawiasy nie są wymagane zawsze konieczne jest dodanie nawias pierwszeństwo nie spełnia wymagań dotyczących na przykład:

   User.Department-eq "Marketing" — i user.country-eq "PL"

odpowiada to:

   (user.department-eq "Marketingowych") — a (user.country-eq "PL")

## <a name="using-the--in-and--notin-operators"></a>Przy użyciu w i notIn — operatory

Jeśli chcesz porównać wartości atrybutu użytkownika przed szereg różnych wartości można użyć w lub operatory - notIn. Oto przykład przy użyciu w operatorze:

    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]

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

   User.mail — ne wartość null jest odpowiednikiem user.mail — ne $null

## <a name="extension-attributes-and-custom-attributes"></a>Atrybuty rozszerzenia oraz atrybuty niestandardowe
Atrybuty rozszerzenia oraz atrybuty niestandardowe są obsługiwane w regułach członkostwo dynamiczne.

Atrybuty rozszerzenia są synchronizowane z lokalną okna serwera AD i mieć format "ExtensionAttributeX", gdzie X jest równa 1 – 15.
Oto przykład regułę, która używa atrybutu rozszerzenia

(user.extensionAttribute15 - eq "marketingowych")

Atrybuty niestandardowe są synchronizowane z lokalną AD systemu Windows Server lub połączonych aplikacji SaaS i format "user.extension_[GUID]\__ [Attribute]", gdzie [identyfikator GUID] jest unikatowy identyfikator aplikacji, która utworzyła w usłudze AAD atrybut w usłudze AAD i [Attribute] jest nazwa atrybutu, ponieważ został on utworzony.
Na przykład regułę, która korzysta z atrybutem niestandardowym

User.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  

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
Można również utworzyć regułę, która wybiera obiekty urządzeń do członkostwa w grupie. Można to następujące atrybuty:

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
> Reguły te urządzenia nie można utworzyć za pomocą listy rozwijanej "Prosta reguła" w klasycznym portalu Azure.
>
>

## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Rozwiązywanie problemów z dynamiczne zarządzanie członkostwem w grupach](active-directory-accessmanagement-troubleshooting.md)
* [Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
