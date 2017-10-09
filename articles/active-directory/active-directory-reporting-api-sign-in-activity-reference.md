---
title: "raport aktywności aaaAzure logowania usługi Active Directory dokumentacja interfejsu API | Dokumentacja firmy Microsoft"
description: "Dokumentacja dotycząca raport aktywności hello logowania w usłudze Azure Active Directory interfejsu API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Raport aktywności logowania w usłudze Azure usługi Active Directory dokumentacja interfejsu API
Ten temat jest częścią zbiór tematów dotyczących usługi Azure Active Directory hello raportowania interfejsu API.  
Raportowanie na platformie Azure AD zapewnia interfejs API, który umożliwia danych raportu działań logowania tooaccess przy użyciu kodu lub narzędzia pokrewne.
Witaj zakres tego tematu jest tooprovide o informacje na temat hello **API raport aktywności logowania w**.

Zobacz:

* [Działania logowania](active-directory-reporting-azure-portal.md#activity-reports) Aby uzyskać więcej informacji o pojęciach
* [Wprowadzenie do korzystania z usługi Azure Active Directory interfejsu API raportowania hello](active-directory-reporting-api-getting-started.md) uzyskać więcej informacji o hello raportowania interfejsu API.


## <a name="who-can-access-hello-api-data"></a>Kto ma dostęp do danych interfejsu API hello?
* Użytkownicy i nazwy główne usług w roli administratora zabezpieczeń lub czytnika zabezpieczeń hello
* Administratorzy globalni
* Żadnych aplikacji, który ma API hello tooaccess autoryzacji (autoryzacji aplikacji można skonfigurować tylko na podstawie uprawnienia administratora globalnego)

tooconfigure dostępu dla aplikacji tooaccess zabezpieczeń interfejsów API takie jak rejestrowanie zdarzeń, użyj powitania po aplikacji hello tooadd programu PowerShell nazwę główną usługi do roli zabezpieczeń czytnika hello

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Wymagania wstępne
Ten raport za pośrednictwem hello raportowania interfejsu API, musisz mieć tooaccess:

* [Edition usługi Azure Active Directory Premium P1 lub P2](active-directory-editions.md)
* Ukończono hello [interfejsu API raportowania hello Azure AD tooaccess wymagania wstępne](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Uzyskiwanie dostępu do interfejsu API hello
Ten interfejs API może albo dostęp za pośrednictwem hello [Explorer wykres](https://graphexplorer2.cloudapp.net) albo programowo z użyciem, na przykład środowiska PowerShell. W kolejności dla PowerShell toocorrectly zinterpretować składnia filtru OData hello używanym w wywołaniach REST Graph usługi AAD, należy użyć hello backtick (alias: akcent) znaków zbyt "" hello $ znak ucieczki. znak backtick Hello służy jako [znak ucieczki dla środowiska PowerShell](https://technet.microsoft.com/library/hh847755.aspx), umożliwiając PowerShell toodo literału Interpretacja znaku $ hello i uniknąć skomplikowana go jako nazwę zmiennej środowiska PowerShell (ie: $filter).

Witaj w tym temacie koncentruje się na powitania Explorer wykresu. Na przykład środowiska PowerShell, zobacz [skrypt programu PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>Punkt końcowy interfejsu API
Aby dostęp do tego interfejsu API przy użyciu powitania po podstawowy identyfikator URI:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



Powodu toohello ilość danych ten interfejs API ma limit milion zwróconych rekordów. 

To wywołanie zwraca dane hello w partiach. Każdej z partii może zawierać maksymalnie 1000 rekordów.  
tooget hello następnej partii rekordów, użyj hello łącze do następnej. Pobierz hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informacji z pierwszego zestawu hello zwróconych rekordów. token Pomiń Hello będzie na końcu hello hello zestawu wyników.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Filtry obsługiwane
Można zawęzić hello liczba rekordów, które są zwracane przez interfejs API wywołaj w formularzu filtru.  
Dla interfejsu API logowania obsługiwane są powiązane dane, hello następujące filtry:

* **$top =\<zwracana liczba rekordów toobe\>**  -toolimit hello liczba zwróconych rekordów. Jest to kosztowna operacja. Nie należy używać tego filtru, jeśli chcesz tooreturn tysięcy obiektów.  
* **$filter =\<instrukcji filtru\>**  -toospecify na podstawie hello pól filtr obsługiwanych, typu hello rekordów są dla Ciebie ważne

## <a name="supported-filter-fields-and-operators"></a>Operatory i pól filtr obsługiwane
typu hello toospecify rekordy, które są dla Ciebie ważne, można utworzyć filtr instrukcję, która może zawierać jeden lub kombinację hello kolejnych pól Filtr:

* [signinDateTime](#signindatetime) — określa datę lub zakres dat
* [Identyfikator userId](#userid) — definiuje określonego użytkownika na podstawie hello identyfikatora użytkownika.
* [userPrincipalName](#userprincipalname) — definiuje użytkownika hello określonego użytkownika na podstawie nazwa główna użytkownika (UPN)
* [Identyfikator appId](#appid) — definiuje identyfikator aplikacji hello specyficzne dla aplikacji na podstawie
* [appDisplayName](#appdisplayname) — definiuje nazwę wyświetlaną aplikacji hello specyficzne dla aplikacji na podstawie
* [stanu logowania](#loginStatus) — definiuje stan hello hello logowania (Powodzenie / błąd)

> [!NOTE]
> Podczas używania Eksploratora wykresu, możesz hello muszą hello toouse poprawne, że w przypadku każdej litery jest pól filtr.
> 
> 

toonarrow dół hello zakres hello zwrócił dane, można utworzyć kombinacje hello obsługiwane filtry i pola filtru. Na przykład hello następująca instrukcja rekordy hello top 10 między 1 lipca 2016 i lipca 2016 6:

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**Operatory obsługiwane**: eq, ge, le, gt, lt

**Przykład**:

Przy użyciu określonej daty

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



Przy użyciu zakresu dat    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**Uwagi dotyczące**:

Parametr typu datetime Hello powinien być w formacie UTC hello 

- - -
### <a name="userid"></a>Nazwa użytkownika
**Operatory obsługiwane**: eq

**Przykład**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Uwagi dotyczące**:

wartość ciągu jest Hello wartość identyfikatora userId

- - -
### <a name="userprincipalname"></a>userPrincipalName
**Operatory obsługiwane**: eq

**Przykład**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Uwagi dotyczące**:

wartość Hello userPrincipalName jest wartość ciągu

- - -
### <a name="appid"></a>Identyfikator aplikacji
**Operatory obsługiwane**: eq

**Przykład**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Uwagi dotyczące**:

wartość Hello identyfikator appId jest wartość ciągu

- - -
### <a name="appdisplayname"></a>appDisplayName
**Operatory obsługiwane**: eq

**Przykład**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Uwagi dotyczące**:

wartość Hello appDisplayName jest wartość ciągu

- - -
### <a name="loginstatus"></a>stanu logowania
**Operatory obsługiwane**: eq

**Przykład**:

    $filter=loginStatus+eq+'1'  


**Uwagi dotyczące**:

Dostępne są dwie opcje dla stanu logowania hello: 0 - Sukces, 1 — błąd

- - -
## <a name="next-steps"></a>Następne kroki
* Czy chcesz przykłady toosee filtrowane działań logowania? Zapoznaj się z hello [przykłady raportu interfejsu API działania usługi Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).
* Czy chcesz, aby tooknow więcej informacji na temat interfejsu API raportowania hello Azure AD? Zobacz [wprowadzenie hello Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).

