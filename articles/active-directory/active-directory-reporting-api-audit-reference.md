---
title: "aaaAzure usługi Active Directory audytu dokumentacja interfejsu API | Dokumentacja firmy Microsoft"
description: "Jak tooget pracę z hello interfejs API inspekcji usługi Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Azure Active Directory audytu dokumentacja interfejsu API
Ten temat jest częścią zbiór tematów dotyczących usługi Azure Active Directory hello raportowania interfejsu API.  
Raportowanie na platformie Azure AD zapewnia interfejs API, który umożliwia dane inspekcji tooaccess za pomocą kodu lub narzędzia pokrewne.
Witaj zakres tego tematu jest tooprovide o informacje na temat hello **inspekcji interfejsu API**.

Zobacz:

* [Dzienniki inspekcji](active-directory-reporting-azure-portal.md#activity-reports) Aby uzyskać więcej informacji o pojęciach

* [Wprowadzenie do korzystania z usługi Azure Active Directory interfejsu API raportowania hello](active-directory-reporting-api-getting-started.md) uzyskać więcej informacji o hello raportowania interfejsu API.


W przypadku:

- Często zadawane pytania, przeczytaj nasze [— często zadawane pytania](active-directory-reporting-faq.md) 

- Problemy, sprawdź [pliku biletu pomocy technicznej](active-directory-troubleshooting-support-howto.md) 


## <a name="who-can-access-hello-data"></a>Kto ma dostęp do danych hello?
* Użytkowników w roli administratora zabezpieczeń lub czytnika zabezpieczeń hello
* Administratorzy globalni
* Żadnych aplikacji, który ma API hello tooaccess autoryzacji (autoryzacji aplikacji można skonfigurować tylko na podstawie uprawnienia administratora globalnego)

## <a name="prerequisites"></a>Wymagania wstępne
W kolejności tooaccess to raportu za pomocą hello interfejsu API raportowania, musi mieć:

* [Lepsze wersji lub Azure Active Directory bezpłatna](active-directory-editions.md)
* Ukończono hello [interfejsu API raportowania hello Azure AD tooaccess wymagania wstępne](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Uzyskiwanie dostępu do interfejsu API hello
Ten interfejs API może albo dostęp za pośrednictwem hello [Explorer wykres](https://graphexplorer2.cloudapp.net) albo programowo z użyciem, na przykład środowiska PowerShell. W kolejności dla PowerShell toocorrectly zinterpretować składnia filtru OData hello używanym w wywołaniach REST Graph usługi AAD, należy użyć hello backtick (alias: akcent) znaków zbyt "" hello $ znak ucieczki. znak backtick Hello służy jako [znak ucieczki dla środowiska PowerShell](https://technet.microsoft.com/library/hh847755.aspx), umożliwiając PowerShell toodo literału Interpretacja znaku $ hello i uniknąć skomplikowana go jako nazwę zmiennej środowiska PowerShell (ie: $filter).

Witaj w tym temacie koncentruje się na powitania Explorer wykresu. Na przykład środowiska PowerShell, zobacz [skrypt programu PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>Punkt końcowy interfejsu API
Aby dostęp do tego interfejsu API przy użyciu hello następującego identyfikatora URI:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Nie ma żadnego limitu na powitania liczbę rekordów zwróconych przez interfejs API inspekcji hello Azure AD (przy użyciu podział na strony OData).
Do przechowywania ograniczenia dotyczące raportowania danych, zapoznaj się z [zasad przechowywania dotyczących okresu raportowania](active-directory-reporting-retention.md).

To wywołanie zwraca dane hello w partiach. Każdej z partii może zawierać maksymalnie 1000 rekordów.  
tooget hello następnej partii rekordów, użyj hello łącze do następnej. Pobierz informacje skiptoken hello z pierwszego zestawu hello zwróconych rekordów. token Pomiń Hello będzie na końcu hello hello zestawu wyników.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Filtry obsługiwane
Można zawęzić hello liczba rekordów, które są zwracane przez interfejs API wywołaj w formularzu filtru.  
Dla interfejsu API logowania obsługiwane są powiązane dane, hello następujące filtry:

* **$top =\<zwracana liczba rekordów toobe\>**  -toolimit hello liczba zwróconych rekordów. Jest to kosztowna operacja. Nie należy używać tego filtru, jeśli chcesz tooreturn tysięcy obiektów.     
* **$filter =\<instrukcji filtru\>**  -toospecify na podstawie hello pól filtr obsługiwanych, typu hello rekordów są dla Ciebie ważne

## <a name="supported-filter-fields-and-operators"></a>Operatory i pól filtr obsługiwane
typu hello toospecify rekordy, które są dla Ciebie ważne, można utworzyć filtr instrukcję, która może zawierać jeden lub kombinację hello kolejnych pól Filtr:

* [Daty](#activitydate) — określa datę lub zakres dat
* [Kategoria](#category) — definiuje hello kategorii ma być toofilter.
* [Element activityStatus](#activitystatus) — definiuje hello stan działania
* [Właściwość activityType](#activitytype) — definiuje typ hello działania
* [działanie](#activity) — definiuje działania hello jako ciąg  
* [nazwisko/aktora](#actorname) — definiuje hello aktora w formie nazwy hello aktora
* [aktora/objectid](#actorobjectid) — definiuje hello aktora w postaci hello aktora o identyfikatorze   
* [aktora/nazwa upn](#actorupn) — definiuje hello aktora w postaci nazwy zasady aktora hello użytkownika (UPN) 
* [Nazwadocelowego/](#targetname) — definiuje hello docelowego w formie nazwy hello aktora
* [docelowy/objectid](#targetobjectid) — definiuje hello docelowego w postaci ID elementu docelowego hello  
* [docelowy/nazwa upn](#targetupn) — definiuje hello aktora w postaci nazwy zasady aktora hello użytkownika (UPN)   

- - -
### <a name="activitydate"></a>Daty
**Operatory obsługiwane**: eq, ge, le, gt, lt

**Przykład**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Uwagi dotyczące**:

Data i godzina powinny być w formacie UTC

- - -
### <a name="category"></a>category

**Obsługiwane wartości**:

| Kategoria                         | Wartość     |
| :--                              | ---       |
| Katalog podstawowy                   | Katalog |
| Samoobsługowe zarządzanie hasłami | SSPR      |
| Samoobsługowe zarządzanie grupami    | GRUPAMI      |
| Aprowizacja kont             | Sync      |
| Automatyczne przenoszenie haseł      | Automatyczne przenoszenie haseł |
| Identity Protection              | IdentityProtection |
| Zaproszeni użytkownicy                    | Zaproszeni użytkownicy |
| Usługa MIM                      | Usługa MIM |



**Operatory obsługiwane**: eq

**Przykład**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>Element ActivityStatus

**Obsługiwane wartości**:

| Stan działania | Wartość |
| :--             | ---   |
| Powodzenie         | 0     |
| Niepowodzenie         | - 1   |

**Operatory obsługiwane**: eq

**Przykład**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>Właściwość activityType
**Operatory obsługiwane**: eq

**Przykład**:

    $filter=activityType eq 'User'    

**Uwagi dotyczące**:

uwzględniana wielkość liter

- - -
### <a name="activity"></a>Działanie
**Operatory obsługiwane**: eq, zawiera startsWith

**Przykład**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Uwagi dotyczące**:

uwzględniana wielkość liter

- - -
### <a name="actorname"></a>nazwisko/aktora
**Operatory obsługiwane**: eq, zawiera startsWith

**Przykład**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Uwagi dotyczące**:

Bez uwzględniania wielkości liter

- - -
### <a name="actorobjectid"></a>aktora/objectId.
**Operatory obsługiwane**: eq

**Przykład**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>Nazwa docelowego /
**Operatory obsługiwane**: eq, zawiera startsWith

**Przykład**:

    $filter=targets/any(t: t/name eq 'some name')    

**Uwagi dotyczące**:

Bez uwzględniania wielkości liter

- - -
### <a name="targetupn"></a>docelowy/nazwa upn
**Operatory obsługiwane**: eq, startsWith

**Przykład**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Uwagi dotyczące**:

* Bez uwzględniania wielkości liter
* Podczas wykonywania zapytania Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity konieczne tooadd hello pełna w przestrzeni nazw

- - -
### <a name="targetobjectid"></a>docelowy/objectId.
**Operatory obsługiwane**: eq

**Przykład**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>aktora/nazwa upn
**Operatory obsługiwane**: eq, startsWith

**Przykład**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Uwagi dotyczące**:

* Bez uwzględniania wielkości liter 
* Podczas wykonywania zapytania Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity konieczne tooadd hello pełna w przestrzeni nazw

- - -
## <a name="next-steps"></a>Następne kroki
* Czy chcesz toosee przykłady działań filtrowane systemu? Zapoznaj się z hello [przykłady inspekcji interfejsu API usługi Azure Active Directory](active-directory-reporting-api-audit-samples.md).
* Czy chcesz, aby tooknow więcej informacji na temat interfejsu API raportowania hello Azure AD? Zobacz [wprowadzenie hello Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).

