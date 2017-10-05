---
title: Azure Active Directory audytu dokumentacja interfejsu API | Dokumentacja firmy Microsoft
description: "Jak rozpocząć pracę z interfejsem API inspekcji usługi Azure Active Directory"
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
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="4a2e3-103">Azure Active Directory audytu dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4a2e3-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="4a2e3-104">Ten temat jest częścią zbiór tematów dotyczących usługi Azure Active Directory raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="4a2e3-105">Raportowanie na platformie Azure AD zapewnia interfejs API, który umożliwia dostęp do danych inspekcji za pomocą kodu lub narzędzia pokrewne.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="4a2e3-106">Zakres tego tematu jest dostarczają informacje na temat **inspekcji interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="4a2e3-107">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-107">See:</span></span>

* <span data-ttu-id="4a2e3-108">[Dzienniki inspekcji](active-directory-reporting-azure-portal.md#activity-reports) Aby uzyskać więcej informacji o pojęciach</span><span class="sxs-lookup"><span data-stu-id="4a2e3-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="4a2e3-109">[Wprowadzenie do usługi Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md) Aby uzyskać więcej informacji na temat raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="4a2e3-110">W przypadku:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-110">For:</span></span>

- <span data-ttu-id="4a2e3-111">Często zadawane pytania, przeczytaj nasze [— często zadawane pytania](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="4a2e3-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="4a2e3-112">Problemy, sprawdź [pliku biletu pomocy technicznej](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="4a2e3-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="4a2e3-113">Kto ma dostęp do danych?</span><span class="sxs-lookup"><span data-stu-id="4a2e3-113">Who can access the data?</span></span>
* <span data-ttu-id="4a2e3-114">Użytkownicy w roli administratora zabezpieczeń lub czytelnika zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="4a2e3-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="4a2e3-115">Administratorzy globalni</span><span class="sxs-lookup"><span data-stu-id="4a2e3-115">Global Admins</span></span>
* <span data-ttu-id="4a2e3-116">Dowolną aplikację, która ma zezwolenie na dostęp do interfejsu API (autoryzacji aplikacji można skonfigurować tylko na podstawie uprawnienia administratora globalnego)</span><span class="sxs-lookup"><span data-stu-id="4a2e3-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a2e3-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4a2e3-117">Prerequisites</span></span>
<span data-ttu-id="4a2e3-118">Aby uzyskać dostęp do tego raportu za pomocą interfejsu API raportowania, należy skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="4a2e3-119">[Lepsze wersji lub Azure Active Directory bezpłatna](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="4a2e3-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="4a2e3-120">Ukończono [wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="4a2e3-121">Uzyskiwanie dostępu do interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4a2e3-121">Accessing the API</span></span>
<span data-ttu-id="4a2e3-122">Albo dostęp do tego interfejsu API za pomocą [Explorer wykres](https://graphexplorer2.cloudapp.net) albo programowo z użyciem, na przykład środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="4a2e3-123">Aby PowerShell poprawnie interpretować składnia filtru OData używanym w wywołaniach AAD wykres REST, należy użyć backtick (alias: akcent) znaku "ucieczki" znaku $.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="4a2e3-124">Znak backtick służy jako [znak ucieczki dla środowiska PowerShell](https://technet.microsoft.com/library/hh847755.aspx), umożliwiając PowerShell literału interpretacja znak $, i uniknąć skomplikowana go jako nazwę zmiennej środowiska PowerShell (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="4a2e3-125">Ten temat koncentruje się w Eksploratorze wykresu.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="4a2e3-126">Na przykład środowiska PowerShell, zobacz [skrypt programu PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="4a2e3-127">Punkt końcowy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="4a2e3-127">API Endpoint</span></span>
<span data-ttu-id="4a2e3-128">Aby dostęp do tego interfejsu API przy użyciu następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="4a2e3-129">Nie ma żadnego limitu liczby rekordów zwróconych przez interfejs API inspekcji usługi Azure AD (przy użyciu podział na strony OData).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="4a2e3-130">Do przechowywania ograniczenia dotyczące raportowania danych, zapoznaj się z [zasad przechowywania dotyczących okresu raportowania](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="4a2e3-131">To wywołanie zwraca dane w partiach.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-131">This call returns the data in batches.</span></span> <span data-ttu-id="4a2e3-132">Każdej z partii może zawierać maksymalnie 1000 rekordów.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="4a2e3-133">Aby uzyskać kolejną partię rekordów, użyj łącze do następnej.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="4a2e3-134">Pobierz informacje skiptoken z pierwszego zestawu zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="4a2e3-135">Pomiń token zostanie na końcu wynik ustawiona.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="4a2e3-136">Filtry obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4a2e3-136">Supported filters</span></span>
<span data-ttu-id="4a2e3-137">Liczba rekordów, które są zwracane przez interfejs API można zawęzić wywołaj w formularzu filtru.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="4a2e3-138">Dla interfejsu API logowania związane z danych, obsługiwane są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="4a2e3-139">**$top =\<liczba rekordów, które ma zostać zwrócona\>**  — Aby ograniczyć liczbę zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="4a2e3-140">Jest to kosztowna operacja.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-140">This is an expensive operation.</span></span> <span data-ttu-id="4a2e3-141">Nie należy używać tego filtru, aby zwrócić tysiące obiektów.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="4a2e3-142">**$filter =\<instrukcji filtru\>**  — Aby określić, na podstawie pól filtr obsługiwanych typu rekordów są dla Ciebie ważne</span><span class="sxs-lookup"><span data-stu-id="4a2e3-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="4a2e3-143">Operatory i pól filtr obsługiwane</span><span class="sxs-lookup"><span data-stu-id="4a2e3-143">Supported filter fields and operators</span></span>
<span data-ttu-id="4a2e3-144">Aby określić typ rekordów, które są dla Ciebie ważne, można utworzyć filtr instrukcję, która może zawierać jeden lub kombinację następujących pól Filtr:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="4a2e3-145">[Daty](#activitydate) — określa datę lub zakres dat</span><span class="sxs-lookup"><span data-stu-id="4a2e3-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="4a2e3-146">[Kategoria](#category) — definiuje chcesz filtrować według kategorii.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="4a2e3-147">[Element activityStatus](#activitystatus) — definiuje stan działania</span><span class="sxs-lookup"><span data-stu-id="4a2e3-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="4a2e3-148">[Właściwość activityType](#activitytype) — definiuje typ działania</span><span class="sxs-lookup"><span data-stu-id="4a2e3-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="4a2e3-149">[działanie](#activity) — definiuje działania w postaci ciągu</span><span class="sxs-lookup"><span data-stu-id="4a2e3-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="4a2e3-150">[nazwisko/aktora](#actorname) — definiuje aktora w formie nazwy aktora</span><span class="sxs-lookup"><span data-stu-id="4a2e3-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="4a2e3-151">[aktora/objectid](#actorobjectid) — definiuje aktora w postaci aktora o identyfikatorze</span><span class="sxs-lookup"><span data-stu-id="4a2e3-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="4a2e3-152">[aktora/nazwa upn](#actorupn) — definiuje aktora w postaci nazwy zasady aktora użytkownika (UPN)</span><span class="sxs-lookup"><span data-stu-id="4a2e3-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="4a2e3-153">[Nazwadocelowego/](#targetname) — definiuje obiekt docelowy w formie nazwy aktora</span><span class="sxs-lookup"><span data-stu-id="4a2e3-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="4a2e3-154">[docelowy/objectid](#targetobjectid) — definiuje obiekt docelowy w formie identyfikatora obiektu docelowego</span><span class="sxs-lookup"><span data-stu-id="4a2e3-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="4a2e3-155">[docelowy/nazwa upn](#targetupn) — definiuje aktora w postaci nazwy zasady aktora użytkownika (UPN)</span><span class="sxs-lookup"><span data-stu-id="4a2e3-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="4a2e3-156">Daty</span><span class="sxs-lookup"><span data-stu-id="4a2e3-156">activityDate</span></span>
<span data-ttu-id="4a2e3-157">**Operatory obsługiwane**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="4a2e3-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="4a2e3-158">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="4a2e3-159">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-159">**Notes**:</span></span>

<span data-ttu-id="4a2e3-160">Data i godzina powinny być w formacie UTC</span><span class="sxs-lookup"><span data-stu-id="4a2e3-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="4a2e3-161">category</span><span class="sxs-lookup"><span data-stu-id="4a2e3-161">category</span></span>

<span data-ttu-id="4a2e3-162">**Obsługiwane wartości**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-162">**Supported values**:</span></span>

| <span data-ttu-id="4a2e3-163">Kategoria</span><span class="sxs-lookup"><span data-stu-id="4a2e3-163">Category</span></span>                         | <span data-ttu-id="4a2e3-164">Wartość</span><span class="sxs-lookup"><span data-stu-id="4a2e3-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="4a2e3-165">Katalog podstawowy</span><span class="sxs-lookup"><span data-stu-id="4a2e3-165">Core Directory</span></span>                   | <span data-ttu-id="4a2e3-166">Katalog</span><span class="sxs-lookup"><span data-stu-id="4a2e3-166">Directory</span></span> |
| <span data-ttu-id="4a2e3-167">Samoobsługowe zarządzanie hasłami</span><span class="sxs-lookup"><span data-stu-id="4a2e3-167">Self-service Password Management</span></span> | <span data-ttu-id="4a2e3-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="4a2e3-168">SSPR</span></span>      |
| <span data-ttu-id="4a2e3-169">Samoobsługowe zarządzanie grupami</span><span class="sxs-lookup"><span data-stu-id="4a2e3-169">Self-service Group Management</span></span>    | <span data-ttu-id="4a2e3-170">GRUPAMI</span><span class="sxs-lookup"><span data-stu-id="4a2e3-170">SSGM</span></span>      |
| <span data-ttu-id="4a2e3-171">Aprowizacja kont</span><span class="sxs-lookup"><span data-stu-id="4a2e3-171">Account Provisioning</span></span>             | <span data-ttu-id="4a2e3-172">Sync</span><span class="sxs-lookup"><span data-stu-id="4a2e3-172">Sync</span></span>      |
| <span data-ttu-id="4a2e3-173">Automatyczne przenoszenie haseł</span><span class="sxs-lookup"><span data-stu-id="4a2e3-173">Automated Password Rollover</span></span>      | <span data-ttu-id="4a2e3-174">Automatyczne przenoszenie haseł</span><span class="sxs-lookup"><span data-stu-id="4a2e3-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="4a2e3-175">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="4a2e3-175">Identity Protection</span></span>              | <span data-ttu-id="4a2e3-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="4a2e3-176">IdentityProtection</span></span> |
| <span data-ttu-id="4a2e3-177">Zaproszeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="4a2e3-177">Invited Users</span></span>                    | <span data-ttu-id="4a2e3-178">Zaproszeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="4a2e3-178">Invited Users</span></span> |
| <span data-ttu-id="4a2e3-179">Usługa MIM</span><span class="sxs-lookup"><span data-stu-id="4a2e3-179">MIM Service</span></span>                      | <span data-ttu-id="4a2e3-180">Usługa MIM</span><span class="sxs-lookup"><span data-stu-id="4a2e3-180">MIM Service</span></span> |



<span data-ttu-id="4a2e3-181">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="4a2e3-181">**Supported operators**: eq</span></span>

<span data-ttu-id="4a2e3-182">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="4a2e3-183">Element ActivityStatus</span><span class="sxs-lookup"><span data-stu-id="4a2e3-183">activityStatus</span></span>

<span data-ttu-id="4a2e3-184">**Obsługiwane wartości**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-184">**Supported values**:</span></span>

| <span data-ttu-id="4a2e3-185">Stan działania</span><span class="sxs-lookup"><span data-stu-id="4a2e3-185">Activity Status</span></span> | <span data-ttu-id="4a2e3-186">Wartość</span><span class="sxs-lookup"><span data-stu-id="4a2e3-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="4a2e3-187">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="4a2e3-187">Success</span></span>         | <span data-ttu-id="4a2e3-188">0</span><span class="sxs-lookup"><span data-stu-id="4a2e3-188">0</span></span>     |
| <span data-ttu-id="4a2e3-189">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="4a2e3-189">Failure</span></span>         | <span data-ttu-id="4a2e3-190">- 1</span><span class="sxs-lookup"><span data-stu-id="4a2e3-190">- 1</span></span>   |

<span data-ttu-id="4a2e3-191">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="4a2e3-191">**Supported operators**: eq</span></span>

<span data-ttu-id="4a2e3-192">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="4a2e3-193">Właściwość activityType</span><span class="sxs-lookup"><span data-stu-id="4a2e3-193">activityType</span></span>
<span data-ttu-id="4a2e3-194">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="4a2e3-194">**Supported operators**: eq</span></span>

<span data-ttu-id="4a2e3-195">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="4a2e3-196">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-196">**Notes**:</span></span>

<span data-ttu-id="4a2e3-197">uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="4a2e3-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="4a2e3-198">Działanie</span><span class="sxs-lookup"><span data-stu-id="4a2e3-198">activity</span></span>
<span data-ttu-id="4a2e3-199">**Operatory obsługiwane**: eq, zawiera startsWith</span><span class="sxs-lookup"><span data-stu-id="4a2e3-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="4a2e3-200">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="4a2e3-201">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-201">**Notes**:</span></span>

<span data-ttu-id="4a2e3-202">uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="4a2e3-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="4a2e3-203">nazwisko/aktora</span><span class="sxs-lookup"><span data-stu-id="4a2e3-203">actor/name</span></span>
<span data-ttu-id="4a2e3-204">**Operatory obsługiwane**: eq, zawiera startsWith</span><span class="sxs-lookup"><span data-stu-id="4a2e3-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="4a2e3-205">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="4a2e3-206">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-206">**Notes**:</span></span>

<span data-ttu-id="4a2e3-207">Bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="4a2e3-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="4a2e3-208">aktora/objectId.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-208">actor/objectId</span></span>
<span data-ttu-id="4a2e3-209">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="4a2e3-209">**Supported operators**: eq</span></span>

<span data-ttu-id="4a2e3-210">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="4a2e3-211">Nazwa docelowego /</span><span class="sxs-lookup"><span data-stu-id="4a2e3-211">target/name</span></span>
<span data-ttu-id="4a2e3-212">**Operatory obsługiwane**: eq, zawiera startsWith</span><span class="sxs-lookup"><span data-stu-id="4a2e3-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="4a2e3-213">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="4a2e3-214">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-214">**Notes**:</span></span>

<span data-ttu-id="4a2e3-215">Bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="4a2e3-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="4a2e3-216">docelowy/nazwa upn</span><span class="sxs-lookup"><span data-stu-id="4a2e3-216">target/upn</span></span>
<span data-ttu-id="4a2e3-217">**Operatory obsługiwane**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="4a2e3-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="4a2e3-218">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="4a2e3-219">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-219">**Notes**:</span></span>

* <span data-ttu-id="4a2e3-220">Bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="4a2e3-220">Case-insensitive</span></span>
* <span data-ttu-id="4a2e3-221">Konieczne jest dodanie pełną przestrzeń nazw podczas wykonywania zapytania Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="4a2e3-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="4a2e3-222">docelowy/objectId.</span><span class="sxs-lookup"><span data-stu-id="4a2e3-222">target/objectId</span></span>
<span data-ttu-id="4a2e3-223">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="4a2e3-223">**Supported operators**: eq</span></span>

<span data-ttu-id="4a2e3-224">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="4a2e3-225">aktora/nazwa upn</span><span class="sxs-lookup"><span data-stu-id="4a2e3-225">actor/upn</span></span>
<span data-ttu-id="4a2e3-226">**Operatory obsługiwane**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="4a2e3-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="4a2e3-227">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="4a2e3-228">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="4a2e3-228">**Notes**:</span></span>

* <span data-ttu-id="4a2e3-229">Bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="4a2e3-229">Case-insensitive</span></span> 
* <span data-ttu-id="4a2e3-230">Konieczne jest dodanie pełną przestrzeń nazw podczas wykonywania zapytania Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="4a2e3-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="4a2e3-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4a2e3-231">Next Steps</span></span>
* <span data-ttu-id="4a2e3-232">Czy chcesz wyświetlić przykłady działań filtrowane systemu?</span><span class="sxs-lookup"><span data-stu-id="4a2e3-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="4a2e3-233">Zapoznaj się z [przykłady inspekcji interfejsu API usługi Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="4a2e3-234">Czy chcesz dowiedzieć się więcej na temat raportowania interfejsu API usługi Azure AD?</span><span class="sxs-lookup"><span data-stu-id="4a2e3-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="4a2e3-235">Zobacz [wprowadzenie do usługi Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4a2e3-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

