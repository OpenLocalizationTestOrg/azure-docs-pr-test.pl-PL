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
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="b2d47-103">Raport aktywności logowania w usłudze Azure usługi Active Directory dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b2d47-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="b2d47-104">Ten temat jest częścią zbiór tematów dotyczących usługi Azure Active Directory hello raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b2d47-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="b2d47-105">Raportowanie na platformie Azure AD zapewnia interfejs API, który umożliwia danych raportu działań logowania tooaccess przy użyciu kodu lub narzędzia pokrewne.</span><span class="sxs-lookup"><span data-stu-id="b2d47-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="b2d47-106">Witaj zakres tego tematu jest tooprovide o informacje na temat hello **API raport aktywności logowania w**.</span><span class="sxs-lookup"><span data-stu-id="b2d47-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="b2d47-107">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="b2d47-107">See:</span></span>

* <span data-ttu-id="b2d47-108">[Działania logowania](active-directory-reporting-azure-portal.md#activity-reports) Aby uzyskać więcej informacji o pojęciach</span><span class="sxs-lookup"><span data-stu-id="b2d47-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="b2d47-109">[Wprowadzenie do korzystania z usługi Azure Active Directory interfejsu API raportowania hello](active-directory-reporting-api-getting-started.md) uzyskać więcej informacji o hello raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b2d47-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="b2d47-110">Kto ma dostęp do danych interfejsu API hello?</span><span class="sxs-lookup"><span data-stu-id="b2d47-110">Who can access hello API data?</span></span>
* <span data-ttu-id="b2d47-111">Użytkownicy i nazwy główne usług w roli administratora zabezpieczeń lub czytnika zabezpieczeń hello</span><span class="sxs-lookup"><span data-stu-id="b2d47-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="b2d47-112">Administratorzy globalni</span><span class="sxs-lookup"><span data-stu-id="b2d47-112">Global Admins</span></span>
* <span data-ttu-id="b2d47-113">Żadnych aplikacji, który ma API hello tooaccess autoryzacji (autoryzacji aplikacji można skonfigurować tylko na podstawie uprawnienia administratora globalnego)</span><span class="sxs-lookup"><span data-stu-id="b2d47-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="b2d47-114">tooconfigure dostępu dla aplikacji tooaccess zabezpieczeń interfejsów API takie jak rejestrowanie zdarzeń, użyj powitania po aplikacji hello tooadd programu PowerShell nazwę główną usługi do roli zabezpieczeń czytnika hello</span><span class="sxs-lookup"><span data-stu-id="b2d47-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="b2d47-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2d47-115">Prerequisites</span></span>
<span data-ttu-id="b2d47-116">Ten raport za pośrednictwem hello raportowania interfejsu API, musisz mieć tooaccess:</span><span class="sxs-lookup"><span data-stu-id="b2d47-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="b2d47-117">[Edition usługi Azure Active Directory Premium P1 lub P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="b2d47-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="b2d47-118">Ukończono hello [interfejsu API raportowania hello Azure AD tooaccess wymagania wstępne](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="b2d47-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="b2d47-119">Uzyskiwanie dostępu do interfejsu API hello</span><span class="sxs-lookup"><span data-stu-id="b2d47-119">Accessing hello API</span></span>
<span data-ttu-id="b2d47-120">Ten interfejs API może albo dostęp za pośrednictwem hello [Explorer wykres](https://graphexplorer2.cloudapp.net) albo programowo z użyciem, na przykład środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2d47-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="b2d47-121">W kolejności dla PowerShell toocorrectly zinterpretować składnia filtru OData hello używanym w wywołaniach REST Graph usługi AAD, należy użyć hello backtick (alias: akcent) znaków zbyt "" hello $ znak ucieczki.</span><span class="sxs-lookup"><span data-stu-id="b2d47-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="b2d47-122">znak backtick Hello służy jako [znak ucieczki dla środowiska PowerShell](https://technet.microsoft.com/library/hh847755.aspx), umożliwiając PowerShell toodo literału Interpretacja znaku $ hello i uniknąć skomplikowana go jako nazwę zmiennej środowiska PowerShell (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="b2d47-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="b2d47-123">Witaj w tym temacie koncentruje się na powitania Explorer wykresu.</span><span class="sxs-lookup"><span data-stu-id="b2d47-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="b2d47-124">Na przykład środowiska PowerShell, zobacz [skrypt programu PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="b2d47-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="b2d47-125">Punkt końcowy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b2d47-125">API Endpoint</span></span>
<span data-ttu-id="b2d47-126">Aby dostęp do tego interfejsu API przy użyciu powitania po podstawowy identyfikator URI:</span><span class="sxs-lookup"><span data-stu-id="b2d47-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="b2d47-127">Powodu toohello ilość danych ten interfejs API ma limit milion zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="b2d47-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="b2d47-128">To wywołanie zwraca dane hello w partiach.</span><span class="sxs-lookup"><span data-stu-id="b2d47-128">This call returns hello data in batches.</span></span> <span data-ttu-id="b2d47-129">Każdej z partii może zawierać maksymalnie 1000 rekordów.</span><span class="sxs-lookup"><span data-stu-id="b2d47-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="b2d47-130">tooget hello następnej partii rekordów, użyj hello łącze do następnej.</span><span class="sxs-lookup"><span data-stu-id="b2d47-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="b2d47-131">Pobierz hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informacji z pierwszego zestawu hello zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="b2d47-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="b2d47-132">token Pomiń Hello będzie na końcu hello hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="b2d47-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="b2d47-133">Filtry obsługiwane</span><span class="sxs-lookup"><span data-stu-id="b2d47-133">Supported filters</span></span>
<span data-ttu-id="b2d47-134">Można zawęzić hello liczba rekordów, które są zwracane przez interfejs API wywołaj w formularzu filtru.</span><span class="sxs-lookup"><span data-stu-id="b2d47-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="b2d47-135">Dla interfejsu API logowania obsługiwane są powiązane dane, hello następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="b2d47-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="b2d47-136">**$top =\<zwracana liczba rekordów toobe\>**  -toolimit hello liczba zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="b2d47-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="b2d47-137">Jest to kosztowna operacja.</span><span class="sxs-lookup"><span data-stu-id="b2d47-137">This is an expensive operation.</span></span> <span data-ttu-id="b2d47-138">Nie należy używać tego filtru, jeśli chcesz tooreturn tysięcy obiektów.</span><span class="sxs-lookup"><span data-stu-id="b2d47-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="b2d47-139">**$filter =\<instrukcji filtru\>**  -toospecify na podstawie hello pól filtr obsługiwanych, typu hello rekordów są dla Ciebie ważne</span><span class="sxs-lookup"><span data-stu-id="b2d47-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="b2d47-140">Operatory i pól filtr obsługiwane</span><span class="sxs-lookup"><span data-stu-id="b2d47-140">Supported filter fields and operators</span></span>
<span data-ttu-id="b2d47-141">typu hello toospecify rekordy, które są dla Ciebie ważne, można utworzyć filtr instrukcję, która może zawierać jeden lub kombinację hello kolejnych pól Filtr:</span><span class="sxs-lookup"><span data-stu-id="b2d47-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="b2d47-142">[signinDateTime](#signindatetime) — określa datę lub zakres dat</span><span class="sxs-lookup"><span data-stu-id="b2d47-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="b2d47-143">[Identyfikator userId](#userid) — definiuje określonego użytkownika na podstawie hello identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b2d47-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="b2d47-144">[userPrincipalName](#userprincipalname) — definiuje użytkownika hello określonego użytkownika na podstawie nazwa główna użytkownika (UPN)</span><span class="sxs-lookup"><span data-stu-id="b2d47-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="b2d47-145">[Identyfikator appId](#appid) — definiuje identyfikator aplikacji hello specyficzne dla aplikacji na podstawie</span><span class="sxs-lookup"><span data-stu-id="b2d47-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="b2d47-146">[appDisplayName](#appdisplayname) — definiuje nazwę wyświetlaną aplikacji hello specyficzne dla aplikacji na podstawie</span><span class="sxs-lookup"><span data-stu-id="b2d47-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="b2d47-147">[stanu logowania](#loginStatus) — definiuje stan hello hello logowania (Powodzenie / błąd)</span><span class="sxs-lookup"><span data-stu-id="b2d47-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="b2d47-148">Podczas używania Eksploratora wykresu, możesz hello muszą hello toouse poprawne, że w przypadku każdej litery jest pól filtr.</span><span class="sxs-lookup"><span data-stu-id="b2d47-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="b2d47-149">toonarrow dół hello zakres hello zwrócił dane, można utworzyć kombinacje hello obsługiwane filtry i pola filtru.</span><span class="sxs-lookup"><span data-stu-id="b2d47-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="b2d47-150">Na przykład hello następująca instrukcja rekordy hello top 10 między 1 lipca 2016 i lipca 2016 6:</span><span class="sxs-lookup"><span data-stu-id="b2d47-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="b2d47-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="b2d47-151">signinDateTime</span></span>
<span data-ttu-id="b2d47-152">**Operatory obsługiwane**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="b2d47-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="b2d47-153">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-153">**Example**:</span></span>

<span data-ttu-id="b2d47-154">Przy użyciu określonej daty</span><span class="sxs-lookup"><span data-stu-id="b2d47-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="b2d47-155">Przy użyciu zakresu dat</span><span class="sxs-lookup"><span data-stu-id="b2d47-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="b2d47-156">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-156">**Notes**:</span></span>

<span data-ttu-id="b2d47-157">Parametr typu datetime Hello powinien być w formacie UTC hello</span><span class="sxs-lookup"><span data-stu-id="b2d47-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="b2d47-158">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="b2d47-158">userId</span></span>
<span data-ttu-id="b2d47-159">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="b2d47-159">**Supported operators**: eq</span></span>

<span data-ttu-id="b2d47-160">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="b2d47-161">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-161">**Notes**:</span></span>

<span data-ttu-id="b2d47-162">wartość ciągu jest Hello wartość identyfikatora userId</span><span class="sxs-lookup"><span data-stu-id="b2d47-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="b2d47-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b2d47-163">userPrincipalName</span></span>
<span data-ttu-id="b2d47-164">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="b2d47-164">**Supported operators**: eq</span></span>

<span data-ttu-id="b2d47-165">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="b2d47-166">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-166">**Notes**:</span></span>

<span data-ttu-id="b2d47-167">wartość Hello userPrincipalName jest wartość ciągu</span><span class="sxs-lookup"><span data-stu-id="b2d47-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="b2d47-168">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="b2d47-168">appId</span></span>
<span data-ttu-id="b2d47-169">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="b2d47-169">**Supported operators**: eq</span></span>

<span data-ttu-id="b2d47-170">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="b2d47-171">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-171">**Notes**:</span></span>

<span data-ttu-id="b2d47-172">wartość Hello identyfikator appId jest wartość ciągu</span><span class="sxs-lookup"><span data-stu-id="b2d47-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="b2d47-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="b2d47-173">appDisplayName</span></span>
<span data-ttu-id="b2d47-174">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="b2d47-174">**Supported operators**: eq</span></span>

<span data-ttu-id="b2d47-175">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="b2d47-176">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-176">**Notes**:</span></span>

<span data-ttu-id="b2d47-177">wartość Hello appDisplayName jest wartość ciągu</span><span class="sxs-lookup"><span data-stu-id="b2d47-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="b2d47-178">stanu logowania</span><span class="sxs-lookup"><span data-stu-id="b2d47-178">loginStatus</span></span>
<span data-ttu-id="b2d47-179">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="b2d47-179">**Supported operators**: eq</span></span>

<span data-ttu-id="b2d47-180">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="b2d47-181">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="b2d47-181">**Notes**:</span></span>

<span data-ttu-id="b2d47-182">Dostępne są dwie opcje dla stanu logowania hello: 0 - Sukces, 1 — błąd</span><span class="sxs-lookup"><span data-stu-id="b2d47-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="b2d47-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2d47-183">Next steps</span></span>
* <span data-ttu-id="b2d47-184">Czy chcesz przykłady toosee filtrowane działań logowania?</span><span class="sxs-lookup"><span data-stu-id="b2d47-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="b2d47-185">Zapoznaj się z hello [przykłady raportu interfejsu API działania usługi Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2d47-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="b2d47-186">Czy chcesz, aby tooknow więcej informacji na temat interfejsu API raportowania hello Azure AD?</span><span class="sxs-lookup"><span data-stu-id="b2d47-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="b2d47-187">Zobacz [wprowadzenie hello Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b2d47-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

