---
title: "Raport aktywności logowania w usłudze Azure usługi Active Directory dokumentacja interfejsu API | Dokumentacja firmy Microsoft"
description: "Odwołanie do API raport aktywności logowania usługi Azure Active Directory"
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
ms.openlocfilehash: d83f1a899ba38dab2c1c1661adede87db6f88c20
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="89b74-103">Raport aktywności logowania w usłudze Azure usługi Active Directory dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="89b74-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="89b74-104">Ten temat jest częścią zbiór tematów dotyczących usługi Azure Active Directory raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="89b74-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="89b74-105">Raportowanie na platformie Azure AD zapewnia interfejs API, który umożliwia dostęp do danych raport aktywności logowania za pomocą kodu lub narzędzia pokrewne.</span><span class="sxs-lookup"><span data-stu-id="89b74-105">Azure AD reporting provides you with an API that enables you to access sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="89b74-106">Zakres tego tematu jest dostarczają informacje na temat **API raport aktywności logowania w**.</span><span class="sxs-lookup"><span data-stu-id="89b74-106">The scope of this topic is to provide you with reference information about the **sign-in activity report API**.</span></span>

<span data-ttu-id="89b74-107">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="89b74-107">See:</span></span>

* <span data-ttu-id="89b74-108">[Działania logowania](active-directory-reporting-azure-portal.md#activity-reports) Aby uzyskać więcej informacji o pojęciach</span><span class="sxs-lookup"><span data-stu-id="89b74-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="89b74-109">[Wprowadzenie do usługi Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md) Aby uzyskać więcej informacji na temat raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="89b74-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="who-can-access-the-api-data"></a><span data-ttu-id="89b74-110">Kto ma dostęp do danych interfejsu API?</span><span class="sxs-lookup"><span data-stu-id="89b74-110">Who can access the API data?</span></span>
* <span data-ttu-id="89b74-111">Użytkownicy i nazwy główne usług w roli administratora zabezpieczeń lub czytnika zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="89b74-111">Users and Service Principals in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="89b74-112">Administratorzy globalni</span><span class="sxs-lookup"><span data-stu-id="89b74-112">Global Admins</span></span>
* <span data-ttu-id="89b74-113">Dowolną aplikację, która ma zezwolenie na dostęp do interfejsu API (autoryzacji aplikacji można skonfigurować tylko na podstawie uprawnienia administratora globalnego)</span><span class="sxs-lookup"><span data-stu-id="89b74-113">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="89b74-114">Konfigurowanie dostępu do interfejsów API zabezpieczeń, takich jak rejestrowanie zdarzeń dostępu aplikacji, należy użyć do dodawania aplikacji nazwy głównej usługi do roli zabezpieczeń czytnika następujące programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="89b74-114">To configure access for an application to access security APIs such as signin events, use the following PowerShell to add the applications Service Principal into the Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="89b74-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89b74-115">Prerequisites</span></span>
<span data-ttu-id="89b74-116">Aby uzyskać dostęp do tego raportu za pomocą interfejsu API raportowania, musi być:</span><span class="sxs-lookup"><span data-stu-id="89b74-116">To access this report through the reporting API, you must have:</span></span>

* <span data-ttu-id="89b74-117">[Edition usługi Azure Active Directory Premium P1 lub P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="89b74-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="89b74-118">Ukończono [wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="89b74-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="89b74-119">Uzyskiwanie dostępu do interfejsu API</span><span class="sxs-lookup"><span data-stu-id="89b74-119">Accessing the API</span></span>
<span data-ttu-id="89b74-120">Albo dostęp do tego interfejsu API za pomocą [Explorer wykres](https://graphexplorer2.cloudapp.net) albo programowo z użyciem, na przykład środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89b74-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="89b74-121">Aby PowerShell poprawnie interpretować składnia filtru OData używanym w wywołaniach AAD wykres REST, należy użyć backtick (alias: akcent) znaku "ucieczki" znaku $.</span><span class="sxs-lookup"><span data-stu-id="89b74-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="89b74-122">Znak backtick służy jako [znak ucieczki dla środowiska PowerShell](https://technet.microsoft.com/library/hh847755.aspx), umożliwiając PowerShell literału interpretacja znak $, i uniknąć skomplikowana go jako nazwę zmiennej środowiska PowerShell (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="89b74-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="89b74-123">Ten temat koncentruje się w Eksploratorze wykresu.</span><span class="sxs-lookup"><span data-stu-id="89b74-123">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="89b74-124">Na przykład środowiska PowerShell, zobacz [skrypt programu PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="89b74-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="89b74-125">Punkt końcowy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="89b74-125">API Endpoint</span></span>
<span data-ttu-id="89b74-126">Aby dostęp do tego interfejsu API przy użyciu następujących podstawowy identyfikator URI:</span><span class="sxs-lookup"><span data-stu-id="89b74-126">You can access this API using the following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="89b74-127">Ze względu na ilość danych ten interfejs API ma limit milion zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="89b74-127">Due to the volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="89b74-128">To wywołanie zwraca dane w partiach.</span><span class="sxs-lookup"><span data-stu-id="89b74-128">This call returns the data in batches.</span></span> <span data-ttu-id="89b74-129">Każdej z partii może zawierać maksymalnie 1000 rekordów.</span><span class="sxs-lookup"><span data-stu-id="89b74-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="89b74-130">Aby uzyskać kolejną partię rekordów, użyj łącze do następnej.</span><span class="sxs-lookup"><span data-stu-id="89b74-130">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="89b74-131">Pobierz [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informacji z pierwszego zestawu zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="89b74-131">Get the [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from the first set of returned records.</span></span> <span data-ttu-id="89b74-132">Pomiń token zostanie na końcu wynik ustawiona.</span><span class="sxs-lookup"><span data-stu-id="89b74-132">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="89b74-133">Filtry obsługiwane</span><span class="sxs-lookup"><span data-stu-id="89b74-133">Supported filters</span></span>
<span data-ttu-id="89b74-134">Liczba rekordów, które są zwracane przez interfejs API można zawęzić wywołaj w formularzu filtru.</span><span class="sxs-lookup"><span data-stu-id="89b74-134">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="89b74-135">Dla interfejsu API logowania związane z danych, obsługiwane są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="89b74-135">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="89b74-136">**$top =\<liczba rekordów, które ma zostać zwrócona\>**  — Aby ograniczyć liczbę zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="89b74-136">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="89b74-137">Jest to kosztowna operacja.</span><span class="sxs-lookup"><span data-stu-id="89b74-137">This is an expensive operation.</span></span> <span data-ttu-id="89b74-138">Nie należy używać tego filtru, aby zwrócić tysiące obiektów.</span><span class="sxs-lookup"><span data-stu-id="89b74-138">You should not use this filter if you want to return thousands of objects.</span></span>  
* <span data-ttu-id="89b74-139">**$filter =\<instrukcji filtru\>**  — Aby określić, na podstawie pól filtr obsługiwanych typu rekordów są dla Ciebie ważne</span><span class="sxs-lookup"><span data-stu-id="89b74-139">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="89b74-140">Operatory i pól filtr obsługiwane</span><span class="sxs-lookup"><span data-stu-id="89b74-140">Supported filter fields and operators</span></span>
<span data-ttu-id="89b74-141">Aby określić typ rekordów, które są dla Ciebie ważne, można utworzyć filtr instrukcję, która może zawierać jeden lub kombinację następujących pól Filtr:</span><span class="sxs-lookup"><span data-stu-id="89b74-141">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="89b74-142">[signinDateTime](#signindatetime) — określa datę lub zakres dat</span><span class="sxs-lookup"><span data-stu-id="89b74-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="89b74-143">[Identyfikator userId](#userid) — definiuje określonego użytkownika na podstawie identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89b74-143">[userId](#userid) - defines a specific user based the user's ID.</span></span>
* <span data-ttu-id="89b74-144">[userPrincipalName](#userprincipalname) — definiuje określonego użytkownika na podstawie użytkownika nazwa główna użytkownika (UPN)</span><span class="sxs-lookup"><span data-stu-id="89b74-144">[userPrincipalName](#userprincipalname) - defines a specific user based the user's user principal name (UPN)</span></span>
* <span data-ttu-id="89b74-145">[Identyfikator appId](#appid) — definiuje określonej aplikacji na podstawie Identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="89b74-145">[appId](#appid) - defines a specific app based the app's ID</span></span>
* <span data-ttu-id="89b74-146">[appDisplayName](#appdisplayname) — definiuje określonej aplikacji na podstawie nazwy wyświetlanej aplikacji</span><span class="sxs-lookup"><span data-stu-id="89b74-146">[appDisplayName](#appdisplayname) - defines a specific app based the app's display name</span></span>
* <span data-ttu-id="89b74-147">[stanu logowania](#loginStatus) — definiuje stan logowania (Powodzenie / błąd)</span><span class="sxs-lookup"><span data-stu-id="89b74-147">[loginStatus](#loginStatus) - defines the status of the logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="89b74-148">Podczas używania Eksploratora wykresu, trzeba mieć poprawną wielkość dla każdej litery jest pól filtr.</span><span class="sxs-lookup"><span data-stu-id="89b74-148">When using Graph Explorer, you the need to use the correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="89b74-149">Aby zawęzić zakres zwrócone dane, można tworzyć kombinacje obsługiwanych filtry i pola filtru.</span><span class="sxs-lookup"><span data-stu-id="89b74-149">To narrow down the scope of the returned data, you can build combinations of the supported filters and filter fields.</span></span> <span data-ttu-id="89b74-150">Na przykład następująca instrukcja zwraca górny 10 rekordów między 1 lipca 2016 i lipca 2016 6.:</span><span class="sxs-lookup"><span data-stu-id="89b74-150">For example, the following statement returns the top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="89b74-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="89b74-151">signinDateTime</span></span>
<span data-ttu-id="89b74-152">**Operatory obsługiwane**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="89b74-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="89b74-153">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="89b74-153">**Example**:</span></span>

<span data-ttu-id="89b74-154">Przy użyciu określonej daty</span><span class="sxs-lookup"><span data-stu-id="89b74-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="89b74-155">Przy użyciu zakresu dat</span><span class="sxs-lookup"><span data-stu-id="89b74-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="89b74-156">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="89b74-156">**Notes**:</span></span>

<span data-ttu-id="89b74-157">Parametr daty/godziny, powinna być w formacie UTC</span><span class="sxs-lookup"><span data-stu-id="89b74-157">The datetime parameter should be in the UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="89b74-158">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="89b74-158">userId</span></span>
<span data-ttu-id="89b74-159">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="89b74-159">**Supported operators**: eq</span></span>

<span data-ttu-id="89b74-160">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="89b74-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="89b74-161">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="89b74-161">**Notes**:</span></span>

<span data-ttu-id="89b74-162">Wartość Nazwa użytkownika jest wartość ciągu</span><span class="sxs-lookup"><span data-stu-id="89b74-162">The value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="89b74-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="89b74-163">userPrincipalName</span></span>
<span data-ttu-id="89b74-164">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="89b74-164">**Supported operators**: eq</span></span>

<span data-ttu-id="89b74-165">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="89b74-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="89b74-166">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="89b74-166">**Notes**:</span></span>

<span data-ttu-id="89b74-167">Wartość userPrincipalName jest wartość ciągu</span><span class="sxs-lookup"><span data-stu-id="89b74-167">The value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="89b74-168">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="89b74-168">appId</span></span>
<span data-ttu-id="89b74-169">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="89b74-169">**Supported operators**: eq</span></span>

<span data-ttu-id="89b74-170">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="89b74-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="89b74-171">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="89b74-171">**Notes**:</span></span>

<span data-ttu-id="89b74-172">Wartość Identyfikator appId jest wartość ciągu</span><span class="sxs-lookup"><span data-stu-id="89b74-172">The value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="89b74-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="89b74-173">appDisplayName</span></span>
<span data-ttu-id="89b74-174">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="89b74-174">**Supported operators**: eq</span></span>

<span data-ttu-id="89b74-175">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="89b74-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="89b74-176">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="89b74-176">**Notes**:</span></span>

<span data-ttu-id="89b74-177">Wartość ciągu jest wartością appDisplayName</span><span class="sxs-lookup"><span data-stu-id="89b74-177">The value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="89b74-178">stanu logowania</span><span class="sxs-lookup"><span data-stu-id="89b74-178">loginStatus</span></span>
<span data-ttu-id="89b74-179">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="89b74-179">**Supported operators**: eq</span></span>

<span data-ttu-id="89b74-180">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="89b74-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="89b74-181">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="89b74-181">**Notes**:</span></span>

<span data-ttu-id="89b74-182">Dostępne są dwie opcje dla stanu logowania: 0 - Sukces, 1 — błąd</span><span class="sxs-lookup"><span data-stu-id="89b74-182">There are two options for the loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="89b74-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89b74-183">Next steps</span></span>
* <span data-ttu-id="89b74-184">Czy chcesz wyświetlić przykłady filtrowane działań logowania?</span><span class="sxs-lookup"><span data-stu-id="89b74-184">Do you want to see examples for filtered sign-in activities?</span></span> <span data-ttu-id="89b74-185">Zapoznaj się z [przykłady raportu interfejsu API działania usługi Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="89b74-185">Check out the [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="89b74-186">Czy chcesz dowiedzieć się więcej na temat raportowania interfejsu API usługi Azure AD?</span><span class="sxs-lookup"><span data-stu-id="89b74-186">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="89b74-187">Zobacz [wprowadzenie do usługi Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="89b74-187">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

