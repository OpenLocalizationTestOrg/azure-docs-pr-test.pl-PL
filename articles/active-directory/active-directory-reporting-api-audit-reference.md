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
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="a2485-103">Azure Active Directory audytu dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a2485-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="a2485-104">Ten temat jest częścią zbiór tematów dotyczących usługi Azure Active Directory hello raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a2485-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="a2485-105">Raportowanie na platformie Azure AD zapewnia interfejs API, który umożliwia dane inspekcji tooaccess za pomocą kodu lub narzędzia pokrewne.</span><span class="sxs-lookup"><span data-stu-id="a2485-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="a2485-106">Witaj zakres tego tematu jest tooprovide o informacje na temat hello **inspekcji interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="a2485-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="a2485-107">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="a2485-107">See:</span></span>

* <span data-ttu-id="a2485-108">[Dzienniki inspekcji](active-directory-reporting-azure-portal.md#activity-reports) Aby uzyskać więcej informacji o pojęciach</span><span class="sxs-lookup"><span data-stu-id="a2485-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="a2485-109">[Wprowadzenie do korzystania z usługi Azure Active Directory interfejsu API raportowania hello](active-directory-reporting-api-getting-started.md) uzyskać więcej informacji o hello raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a2485-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="a2485-110">W przypadku:</span><span class="sxs-lookup"><span data-stu-id="a2485-110">For:</span></span>

- <span data-ttu-id="a2485-111">Często zadawane pytania, przeczytaj nasze [— często zadawane pytania](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a2485-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="a2485-112">Problemy, sprawdź [pliku biletu pomocy technicznej](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="a2485-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="a2485-113">Kto ma dostęp do danych hello?</span><span class="sxs-lookup"><span data-stu-id="a2485-113">Who can access hello data?</span></span>
* <span data-ttu-id="a2485-114">Użytkowników w roli administratora zabezpieczeń lub czytnika zabezpieczeń hello</span><span class="sxs-lookup"><span data-stu-id="a2485-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="a2485-115">Administratorzy globalni</span><span class="sxs-lookup"><span data-stu-id="a2485-115">Global Admins</span></span>
* <span data-ttu-id="a2485-116">Żadnych aplikacji, który ma API hello tooaccess autoryzacji (autoryzacji aplikacji można skonfigurować tylko na podstawie uprawnienia administratora globalnego)</span><span class="sxs-lookup"><span data-stu-id="a2485-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2485-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a2485-117">Prerequisites</span></span>
<span data-ttu-id="a2485-118">W kolejności tooaccess to raportu za pomocą hello interfejsu API raportowania, musi mieć:</span><span class="sxs-lookup"><span data-stu-id="a2485-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="a2485-119">[Lepsze wersji lub Azure Active Directory bezpłatna](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="a2485-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="a2485-120">Ukończono hello [interfejsu API raportowania hello Azure AD tooaccess wymagania wstępne](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="a2485-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="a2485-121">Uzyskiwanie dostępu do interfejsu API hello</span><span class="sxs-lookup"><span data-stu-id="a2485-121">Accessing hello API</span></span>
<span data-ttu-id="a2485-122">Ten interfejs API może albo dostęp za pośrednictwem hello [Explorer wykres](https://graphexplorer2.cloudapp.net) albo programowo z użyciem, na przykład środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2485-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="a2485-123">W kolejności dla PowerShell toocorrectly zinterpretować składnia filtru OData hello używanym w wywołaniach REST Graph usługi AAD, należy użyć hello backtick (alias: akcent) znaków zbyt "" hello $ znak ucieczki.</span><span class="sxs-lookup"><span data-stu-id="a2485-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="a2485-124">znak backtick Hello służy jako [znak ucieczki dla środowiska PowerShell](https://technet.microsoft.com/library/hh847755.aspx), umożliwiając PowerShell toodo literału Interpretacja znaku $ hello i uniknąć skomplikowana go jako nazwę zmiennej środowiska PowerShell (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="a2485-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="a2485-125">Witaj w tym temacie koncentruje się na powitania Explorer wykresu.</span><span class="sxs-lookup"><span data-stu-id="a2485-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="a2485-126">Na przykład środowiska PowerShell, zobacz [skrypt programu PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="a2485-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="a2485-127">Punkt końcowy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a2485-127">API Endpoint</span></span>
<span data-ttu-id="a2485-128">Aby dostęp do tego interfejsu API przy użyciu hello następującego identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="a2485-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="a2485-129">Nie ma żadnego limitu na powitania liczbę rekordów zwróconych przez interfejs API inspekcji hello Azure AD (przy użyciu podział na strony OData).</span><span class="sxs-lookup"><span data-stu-id="a2485-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="a2485-130">Do przechowywania ograniczenia dotyczące raportowania danych, zapoznaj się z [zasad przechowywania dotyczących okresu raportowania](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="a2485-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="a2485-131">To wywołanie zwraca dane hello w partiach.</span><span class="sxs-lookup"><span data-stu-id="a2485-131">This call returns hello data in batches.</span></span> <span data-ttu-id="a2485-132">Każdej z partii może zawierać maksymalnie 1000 rekordów.</span><span class="sxs-lookup"><span data-stu-id="a2485-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="a2485-133">tooget hello następnej partii rekordów, użyj hello łącze do następnej.</span><span class="sxs-lookup"><span data-stu-id="a2485-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="a2485-134">Pobierz informacje skiptoken hello z pierwszego zestawu hello zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="a2485-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="a2485-135">token Pomiń Hello będzie na końcu hello hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="a2485-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="a2485-136">Filtry obsługiwane</span><span class="sxs-lookup"><span data-stu-id="a2485-136">Supported filters</span></span>
<span data-ttu-id="a2485-137">Można zawęzić hello liczba rekordów, które są zwracane przez interfejs API wywołaj w formularzu filtru.</span><span class="sxs-lookup"><span data-stu-id="a2485-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="a2485-138">Dla interfejsu API logowania obsługiwane są powiązane dane, hello następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="a2485-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="a2485-139">**$top =\<zwracana liczba rekordów toobe\>**  -toolimit hello liczba zwróconych rekordów.</span><span class="sxs-lookup"><span data-stu-id="a2485-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="a2485-140">Jest to kosztowna operacja.</span><span class="sxs-lookup"><span data-stu-id="a2485-140">This is an expensive operation.</span></span> <span data-ttu-id="a2485-141">Nie należy używać tego filtru, jeśli chcesz tooreturn tysięcy obiektów.</span><span class="sxs-lookup"><span data-stu-id="a2485-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="a2485-142">**$filter =\<instrukcji filtru\>**  -toospecify na podstawie hello pól filtr obsługiwanych, typu hello rekordów są dla Ciebie ważne</span><span class="sxs-lookup"><span data-stu-id="a2485-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="a2485-143">Operatory i pól filtr obsługiwane</span><span class="sxs-lookup"><span data-stu-id="a2485-143">Supported filter fields and operators</span></span>
<span data-ttu-id="a2485-144">typu hello toospecify rekordy, które są dla Ciebie ważne, można utworzyć filtr instrukcję, która może zawierać jeden lub kombinację hello kolejnych pól Filtr:</span><span class="sxs-lookup"><span data-stu-id="a2485-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="a2485-145">[Daty](#activitydate) — określa datę lub zakres dat</span><span class="sxs-lookup"><span data-stu-id="a2485-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="a2485-146">[Kategoria](#category) — definiuje hello kategorii ma być toofilter.</span><span class="sxs-lookup"><span data-stu-id="a2485-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="a2485-147">[Element activityStatus](#activitystatus) — definiuje hello stan działania</span><span class="sxs-lookup"><span data-stu-id="a2485-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="a2485-148">[Właściwość activityType](#activitytype) — definiuje typ hello działania</span><span class="sxs-lookup"><span data-stu-id="a2485-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="a2485-149">[działanie](#activity) — definiuje działania hello jako ciąg</span><span class="sxs-lookup"><span data-stu-id="a2485-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="a2485-150">[nazwisko/aktora](#actorname) — definiuje hello aktora w formie nazwy hello aktora</span><span class="sxs-lookup"><span data-stu-id="a2485-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="a2485-151">[aktora/objectid](#actorobjectid) — definiuje hello aktora w postaci hello aktora o identyfikatorze</span><span class="sxs-lookup"><span data-stu-id="a2485-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="a2485-152">[aktora/nazwa upn](#actorupn) — definiuje hello aktora w postaci nazwy zasady aktora hello użytkownika (UPN)</span><span class="sxs-lookup"><span data-stu-id="a2485-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="a2485-153">[Nazwadocelowego/](#targetname) — definiuje hello docelowego w formie nazwy hello aktora</span><span class="sxs-lookup"><span data-stu-id="a2485-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="a2485-154">[docelowy/objectid](#targetobjectid) — definiuje hello docelowego w postaci ID elementu docelowego hello</span><span class="sxs-lookup"><span data-stu-id="a2485-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="a2485-155">[docelowy/nazwa upn](#targetupn) — definiuje hello aktora w postaci nazwy zasady aktora hello użytkownika (UPN)</span><span class="sxs-lookup"><span data-stu-id="a2485-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="a2485-156">Daty</span><span class="sxs-lookup"><span data-stu-id="a2485-156">activityDate</span></span>
<span data-ttu-id="a2485-157">**Operatory obsługiwane**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="a2485-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="a2485-158">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="a2485-159">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="a2485-159">**Notes**:</span></span>

<span data-ttu-id="a2485-160">Data i godzina powinny być w formacie UTC</span><span class="sxs-lookup"><span data-stu-id="a2485-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="a2485-161">category</span><span class="sxs-lookup"><span data-stu-id="a2485-161">category</span></span>

<span data-ttu-id="a2485-162">**Obsługiwane wartości**:</span><span class="sxs-lookup"><span data-stu-id="a2485-162">**Supported values**:</span></span>

| <span data-ttu-id="a2485-163">Kategoria</span><span class="sxs-lookup"><span data-stu-id="a2485-163">Category</span></span>                         | <span data-ttu-id="a2485-164">Wartość</span><span class="sxs-lookup"><span data-stu-id="a2485-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="a2485-165">Katalog podstawowy</span><span class="sxs-lookup"><span data-stu-id="a2485-165">Core Directory</span></span>                   | <span data-ttu-id="a2485-166">Katalog</span><span class="sxs-lookup"><span data-stu-id="a2485-166">Directory</span></span> |
| <span data-ttu-id="a2485-167">Samoobsługowe zarządzanie hasłami</span><span class="sxs-lookup"><span data-stu-id="a2485-167">Self-service Password Management</span></span> | <span data-ttu-id="a2485-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="a2485-168">SSPR</span></span>      |
| <span data-ttu-id="a2485-169">Samoobsługowe zarządzanie grupami</span><span class="sxs-lookup"><span data-stu-id="a2485-169">Self-service Group Management</span></span>    | <span data-ttu-id="a2485-170">GRUPAMI</span><span class="sxs-lookup"><span data-stu-id="a2485-170">SSGM</span></span>      |
| <span data-ttu-id="a2485-171">Aprowizacja kont</span><span class="sxs-lookup"><span data-stu-id="a2485-171">Account Provisioning</span></span>             | <span data-ttu-id="a2485-172">Sync</span><span class="sxs-lookup"><span data-stu-id="a2485-172">Sync</span></span>      |
| <span data-ttu-id="a2485-173">Automatyczne przenoszenie haseł</span><span class="sxs-lookup"><span data-stu-id="a2485-173">Automated Password Rollover</span></span>      | <span data-ttu-id="a2485-174">Automatyczne przenoszenie haseł</span><span class="sxs-lookup"><span data-stu-id="a2485-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="a2485-175">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a2485-175">Identity Protection</span></span>              | <span data-ttu-id="a2485-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="a2485-176">IdentityProtection</span></span> |
| <span data-ttu-id="a2485-177">Zaproszeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="a2485-177">Invited Users</span></span>                    | <span data-ttu-id="a2485-178">Zaproszeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="a2485-178">Invited Users</span></span> |
| <span data-ttu-id="a2485-179">Usługa MIM</span><span class="sxs-lookup"><span data-stu-id="a2485-179">MIM Service</span></span>                      | <span data-ttu-id="a2485-180">Usługa MIM</span><span class="sxs-lookup"><span data-stu-id="a2485-180">MIM Service</span></span> |



<span data-ttu-id="a2485-181">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="a2485-181">**Supported operators**: eq</span></span>

<span data-ttu-id="a2485-182">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="a2485-183">Element ActivityStatus</span><span class="sxs-lookup"><span data-stu-id="a2485-183">activityStatus</span></span>

<span data-ttu-id="a2485-184">**Obsługiwane wartości**:</span><span class="sxs-lookup"><span data-stu-id="a2485-184">**Supported values**:</span></span>

| <span data-ttu-id="a2485-185">Stan działania</span><span class="sxs-lookup"><span data-stu-id="a2485-185">Activity Status</span></span> | <span data-ttu-id="a2485-186">Wartość</span><span class="sxs-lookup"><span data-stu-id="a2485-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="a2485-187">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="a2485-187">Success</span></span>         | <span data-ttu-id="a2485-188">0</span><span class="sxs-lookup"><span data-stu-id="a2485-188">0</span></span>     |
| <span data-ttu-id="a2485-189">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="a2485-189">Failure</span></span>         | <span data-ttu-id="a2485-190">- 1</span><span class="sxs-lookup"><span data-stu-id="a2485-190">- 1</span></span>   |

<span data-ttu-id="a2485-191">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="a2485-191">**Supported operators**: eq</span></span>

<span data-ttu-id="a2485-192">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="a2485-193">Właściwość activityType</span><span class="sxs-lookup"><span data-stu-id="a2485-193">activityType</span></span>
<span data-ttu-id="a2485-194">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="a2485-194">**Supported operators**: eq</span></span>

<span data-ttu-id="a2485-195">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="a2485-196">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="a2485-196">**Notes**:</span></span>

<span data-ttu-id="a2485-197">uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="a2485-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="a2485-198">Działanie</span><span class="sxs-lookup"><span data-stu-id="a2485-198">activity</span></span>
<span data-ttu-id="a2485-199">**Operatory obsługiwane**: eq, zawiera startsWith</span><span class="sxs-lookup"><span data-stu-id="a2485-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="a2485-200">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="a2485-201">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="a2485-201">**Notes**:</span></span>

<span data-ttu-id="a2485-202">uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="a2485-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="a2485-203">nazwisko/aktora</span><span class="sxs-lookup"><span data-stu-id="a2485-203">actor/name</span></span>
<span data-ttu-id="a2485-204">**Operatory obsługiwane**: eq, zawiera startsWith</span><span class="sxs-lookup"><span data-stu-id="a2485-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="a2485-205">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="a2485-206">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="a2485-206">**Notes**:</span></span>

<span data-ttu-id="a2485-207">Bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="a2485-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="a2485-208">aktora/objectId.</span><span class="sxs-lookup"><span data-stu-id="a2485-208">actor/objectId</span></span>
<span data-ttu-id="a2485-209">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="a2485-209">**Supported operators**: eq</span></span>

<span data-ttu-id="a2485-210">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="a2485-211">Nazwa docelowego /</span><span class="sxs-lookup"><span data-stu-id="a2485-211">target/name</span></span>
<span data-ttu-id="a2485-212">**Operatory obsługiwane**: eq, zawiera startsWith</span><span class="sxs-lookup"><span data-stu-id="a2485-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="a2485-213">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="a2485-214">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="a2485-214">**Notes**:</span></span>

<span data-ttu-id="a2485-215">Bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="a2485-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="a2485-216">docelowy/nazwa upn</span><span class="sxs-lookup"><span data-stu-id="a2485-216">target/upn</span></span>
<span data-ttu-id="a2485-217">**Operatory obsługiwane**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="a2485-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="a2485-218">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="a2485-219">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="a2485-219">**Notes**:</span></span>

* <span data-ttu-id="a2485-220">Bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="a2485-220">Case-insensitive</span></span>
* <span data-ttu-id="a2485-221">Podczas wykonywania zapytania Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity konieczne tooadd hello pełna w przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="a2485-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="a2485-222">docelowy/objectId.</span><span class="sxs-lookup"><span data-stu-id="a2485-222">target/objectId</span></span>
<span data-ttu-id="a2485-223">**Operatory obsługiwane**: eq</span><span class="sxs-lookup"><span data-stu-id="a2485-223">**Supported operators**: eq</span></span>

<span data-ttu-id="a2485-224">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="a2485-225">aktora/nazwa upn</span><span class="sxs-lookup"><span data-stu-id="a2485-225">actor/upn</span></span>
<span data-ttu-id="a2485-226">**Operatory obsługiwane**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="a2485-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="a2485-227">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a2485-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="a2485-228">**Uwagi dotyczące**:</span><span class="sxs-lookup"><span data-stu-id="a2485-228">**Notes**:</span></span>

* <span data-ttu-id="a2485-229">Bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="a2485-229">Case-insensitive</span></span> 
* <span data-ttu-id="a2485-230">Podczas wykonywania zapytania Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity konieczne tooadd hello pełna w przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="a2485-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="a2485-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2485-231">Next Steps</span></span>
* <span data-ttu-id="a2485-232">Czy chcesz toosee przykłady działań filtrowane systemu?</span><span class="sxs-lookup"><span data-stu-id="a2485-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="a2485-233">Zapoznaj się z hello [przykłady inspekcji interfejsu API usługi Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a2485-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="a2485-234">Czy chcesz, aby tooknow więcej informacji na temat interfejsu API raportowania hello Azure AD?</span><span class="sxs-lookup"><span data-stu-id="a2485-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="a2485-235">Zobacz [wprowadzenie hello Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a2485-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

