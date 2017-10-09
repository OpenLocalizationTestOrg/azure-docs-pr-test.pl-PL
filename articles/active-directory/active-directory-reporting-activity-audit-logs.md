---
title: "działanie aaaAudit raportów w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Raporty dotyczące działań w portalu usługi Azure Active Directory hello inspekcji toohello wprowadzenie"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="74e9b-103">Raporty dotyczące działań w portalu usługi Azure Active Directory hello inspekcji</span><span class="sxs-lookup"><span data-stu-id="74e9b-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="74e9b-104">Z raportowaniem w usłudze Azure Active Directory (Azure AD), można uzyskać informacji hello potrzebne toodetermine jak robi środowiska.</span><span class="sxs-lookup"><span data-stu-id="74e9b-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="74e9b-105">Witaj raportowania architektury w usłudze Azure AD składa się z hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="74e9b-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="74e9b-106">**Działanie**</span><span class="sxs-lookup"><span data-stu-id="74e9b-106">**Activity**</span></span> 
    - <span data-ttu-id="74e9b-107">**Działania logowania** — informacje na temat użycia hello zarządzanych aplikacji i aktywności logowania użytkowników</span><span class="sxs-lookup"><span data-stu-id="74e9b-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="74e9b-108">**Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu.</span><span class="sxs-lookup"><span data-stu-id="74e9b-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="74e9b-109">**Bezpieczeństwo**</span><span class="sxs-lookup"><span data-stu-id="74e9b-109">**Security**</span></span> 
    - <span data-ttu-id="74e9b-110">**Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="74e9b-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="74e9b-111">Aby uzyskać więcej informacji, zobacz Ryzykowne logowania.</span><span class="sxs-lookup"><span data-stu-id="74e9b-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="74e9b-112">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="74e9b-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="74e9b-113">Aby uzyskać więcej informacji, zobacz Użytkownicy oflagowani w związku z ryzykiem.</span><span class="sxs-lookup"><span data-stu-id="74e9b-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="74e9b-114">Ten temat zawiera omówienie hello inspekcji działań.</span><span class="sxs-lookup"><span data-stu-id="74e9b-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="74e9b-115">Kto ma dostęp do danych hello?</span><span class="sxs-lookup"><span data-stu-id="74e9b-115">Who can access hello data?</span></span>
* <span data-ttu-id="74e9b-116">Użytkowników w roli administratora zabezpieczeń lub czytnika zabezpieczeń hello</span><span class="sxs-lookup"><span data-stu-id="74e9b-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="74e9b-117">Administratorzy globalni</span><span class="sxs-lookup"><span data-stu-id="74e9b-117">Global Admins</span></span>
* <span data-ttu-id="74e9b-118">Poszczególni użytkownicy (inni niż administratorzy) mogą wyświetlać dane na temat własnych działań</span><span class="sxs-lookup"><span data-stu-id="74e9b-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="74e9b-119">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="74e9b-119">Audit logs</span></span>

<span data-ttu-id="74e9b-120">Hello dzienników inspekcji w usłudze Azure Active Directory zawierają rekordy działania systemu dla zgodności.</span><span class="sxs-lookup"><span data-stu-id="74e9b-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="74e9b-121">Pierwszy tooall w punkcie wejścia inspekcja danych jest **dzienniki inspekcji** w hello **działania** sekcji **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74e9b-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="74e9b-122">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/61.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="74e9b-123">Dziennik inspekcji zawiera domyślny widok listy, który pokazuje:</span><span class="sxs-lookup"><span data-stu-id="74e9b-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="74e9b-124">Witaj Data i godzina wystąpienia hello</span><span class="sxs-lookup"><span data-stu-id="74e9b-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="74e9b-125">Witaj inicjatora / aktora (*kto*) działania</span><span class="sxs-lookup"><span data-stu-id="74e9b-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="74e9b-126">Witaj działania (*co*)</span><span class="sxs-lookup"><span data-stu-id="74e9b-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="74e9b-127">docelowy Hello</span><span class="sxs-lookup"><span data-stu-id="74e9b-127">hello target</span></span>

<span data-ttu-id="74e9b-128">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/18.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="74e9b-129">Można dostosować widok listy hello klikając **kolumn** hello w pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="74e9b-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="74e9b-130">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/19.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="74e9b-131">To pozwala toodisplay dodatkowe pola lub usuń pola, które są już wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="74e9b-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="74e9b-132">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/21.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="74e9b-133">Po kliknięciu elementu w widoku listy hello, otrzymasz wszystkich dostępnych informacji o nim.</span><span class="sxs-lookup"><span data-stu-id="74e9b-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="74e9b-134">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/22.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="74e9b-135">Dzienniki inspekcji filtrowania</span><span class="sxs-lookup"><span data-stu-id="74e9b-135">Filtering audit logs</span></span>

<span data-ttu-id="74e9b-136">toonarrow dół hello zgłoszone poziom tooa danych czy działa dla Ciebie, dane można filtrować hello inspekcji przy użyciu hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="74e9b-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="74e9b-137">Zakres dat</span><span class="sxs-lookup"><span data-stu-id="74e9b-137">Date range</span></span>
- <span data-ttu-id="74e9b-138">Zainicjowane przez (aktor)</span><span class="sxs-lookup"><span data-stu-id="74e9b-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="74e9b-139">Kategoria</span><span class="sxs-lookup"><span data-stu-id="74e9b-139">Category</span></span>
- <span data-ttu-id="74e9b-140">Typ zasobu działania</span><span class="sxs-lookup"><span data-stu-id="74e9b-140">Activity resource type</span></span>
- <span data-ttu-id="74e9b-141">Działanie</span><span class="sxs-lookup"><span data-stu-id="74e9b-141">Activity</span></span>

<span data-ttu-id="74e9b-142">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/23.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="74e9b-143">Witaj **zakresu dat** filtru umożliwia tooyou toodefine przedział czasu dla hello zwróciła dane.</span><span class="sxs-lookup"><span data-stu-id="74e9b-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="74e9b-144">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="74e9b-144">Possible values are:</span></span>

- <span data-ttu-id="74e9b-145">1 miesiąc</span><span class="sxs-lookup"><span data-stu-id="74e9b-145">1 month</span></span>
- <span data-ttu-id="74e9b-146">7 dni</span><span class="sxs-lookup"><span data-stu-id="74e9b-146">7 days</span></span>
- <span data-ttu-id="74e9b-147">24 godziny</span><span class="sxs-lookup"><span data-stu-id="74e9b-147">24 hours</span></span>
- <span data-ttu-id="74e9b-148">Niestandardowy</span><span class="sxs-lookup"><span data-stu-id="74e9b-148">Custom</span></span>

<span data-ttu-id="74e9b-149">Po wybraniu niestandardowego przedziału czasu możesz skonfigurować godzinę rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="74e9b-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="74e9b-150">Witaj **inicjowane przez** filtr włącza toodefine możesz aktora nazwy lub jej uniwersalnych głównej nazwy (UPN).</span><span class="sxs-lookup"><span data-stu-id="74e9b-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="74e9b-151">Witaj **kategorii** filtr włącza tooselect hello następującego filtru:</span><span class="sxs-lookup"><span data-stu-id="74e9b-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="74e9b-152">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="74e9b-152">All</span></span>
- <span data-ttu-id="74e9b-153">Kategoria podstawowa</span><span class="sxs-lookup"><span data-stu-id="74e9b-153">Core category</span></span>
- <span data-ttu-id="74e9b-154">Katalog podstawowy</span><span class="sxs-lookup"><span data-stu-id="74e9b-154">Core directory</span></span>
- <span data-ttu-id="74e9b-155">Samoobsługowe zarządzanie hasłami</span><span class="sxs-lookup"><span data-stu-id="74e9b-155">Self-service password management</span></span>
- <span data-ttu-id="74e9b-156">Samoobsługowe zarządzanie grupami</span><span class="sxs-lookup"><span data-stu-id="74e9b-156">Self-service group management</span></span>
- <span data-ttu-id="74e9b-157">Aprowizacja kont — automatyczne przerzucanie haseł</span><span class="sxs-lookup"><span data-stu-id="74e9b-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="74e9b-158">Zaproszeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="74e9b-158">Invited users</span></span>
- <span data-ttu-id="74e9b-159">Usługa MIM</span><span class="sxs-lookup"><span data-stu-id="74e9b-159">MIM service</span></span>
- <span data-ttu-id="74e9b-160">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="74e9b-160">Identity Protection</span></span>
- <span data-ttu-id="74e9b-161">B2C</span><span class="sxs-lookup"><span data-stu-id="74e9b-161">B2C</span></span>

<span data-ttu-id="74e9b-162">Witaj **typu zasobu działania** filtr włącza tooselect jedną z następujących hello filtry:</span><span class="sxs-lookup"><span data-stu-id="74e9b-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="74e9b-163">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="74e9b-163">All</span></span> 
- <span data-ttu-id="74e9b-164">Grupa</span><span class="sxs-lookup"><span data-stu-id="74e9b-164">Group</span></span>
- <span data-ttu-id="74e9b-165">Katalog</span><span class="sxs-lookup"><span data-stu-id="74e9b-165">Directory</span></span>
- <span data-ttu-id="74e9b-166">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="74e9b-166">User</span></span>
- <span data-ttu-id="74e9b-167">Aplikacja</span><span class="sxs-lookup"><span data-stu-id="74e9b-167">Application</span></span>
- <span data-ttu-id="74e9b-168">Zasady</span><span class="sxs-lookup"><span data-stu-id="74e9b-168">Policy</span></span>
- <span data-ttu-id="74e9b-169">Urządzenie</span><span class="sxs-lookup"><span data-stu-id="74e9b-169">Device</span></span>
- <span data-ttu-id="74e9b-170">Inne</span><span class="sxs-lookup"><span data-stu-id="74e9b-170">Other</span></span>

<span data-ttu-id="74e9b-171">Po wybraniu **grupy** jako **typu zasobu działania**, Pobierz kategorii dodatkowy filtr, który umożliwia tooalso podaj **źródła**:</span><span class="sxs-lookup"><span data-stu-id="74e9b-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="74e9b-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="74e9b-172">Azure AD</span></span>
- <span data-ttu-id="74e9b-173">O365</span><span class="sxs-lookup"><span data-stu-id="74e9b-173">O365</span></span>


<span data-ttu-id="74e9b-174">Witaj **działania** filtru jest oparta na powitania kategorii i wybór typów zasobów działania podejmowane.</span><span class="sxs-lookup"><span data-stu-id="74e9b-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="74e9b-175">Można wybrać określonego mają toosee lub wybierz wszystkie działania.</span><span class="sxs-lookup"><span data-stu-id="74e9b-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="74e9b-176">Można pobrać listy hello wszystkich działań inspekcji przy użyciu interfejsu API programu Graph https://graph.windows.net/$ hello tenantdomain/działań/auditActivityTypes? api-version = beta, gdzie $tenantdomain = nazwę domeny, lub zobacz artykuł toohello [inspekcji raportu zdarzenia](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="74e9b-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="74e9b-177">Skróty dzienników inspekcji</span><span class="sxs-lookup"><span data-stu-id="74e9b-177">Audit logs shortcuts</span></span>

<span data-ttu-id="74e9b-178">Ponadto zbyt**usługi Azure Active Directory**, hello Azure portal udostępnia dwa dodatkowe punkty wejścia tooaudit danych:</span><span class="sxs-lookup"><span data-stu-id="74e9b-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="74e9b-179">Użytkownicy i grupy</span><span class="sxs-lookup"><span data-stu-id="74e9b-179">Users and groups</span></span>
- <span data-ttu-id="74e9b-180">Aplikacje dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="74e9b-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="74e9b-181">Dzienniki inspekcji użytkowników i grup</span><span class="sxs-lookup"><span data-stu-id="74e9b-181">Users and groups audit logs</span></span>

<span data-ttu-id="74e9b-182">Z użytkownika i raporty dotyczące inspekcji na podstawie grupy można uzyskać odpowiedzi tooquestions, takich jak:</span><span class="sxs-lookup"><span data-stu-id="74e9b-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="74e9b-183">Jakie rodzaje aktualizacje zostały zastosowane hello użytkowników?</span><span class="sxs-lookup"><span data-stu-id="74e9b-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="74e9b-184">Ilu użytkowników zostało zmienionych?</span><span class="sxs-lookup"><span data-stu-id="74e9b-184">How many users were changed?</span></span>

- <span data-ttu-id="74e9b-185">Ile haseł zostało zmienionych?</span><span class="sxs-lookup"><span data-stu-id="74e9b-185">How many passwords were changed?</span></span>

- <span data-ttu-id="74e9b-186">Jakich zmian dokonał administrator w katalogu?</span><span class="sxs-lookup"><span data-stu-id="74e9b-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="74e9b-187">Co to są hello grup, które zostały dodane?</span><span class="sxs-lookup"><span data-stu-id="74e9b-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="74e9b-188">Czy istnieją grupy, w których dokonano zmiany członkostwa?</span><span class="sxs-lookup"><span data-stu-id="74e9b-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="74e9b-189">Zostały zmienione hello właścicieli grupy?</span><span class="sxs-lookup"><span data-stu-id="74e9b-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="74e9b-190">Jakie licencje zostały przypisane tooa grupy lub użytkownika?</span><span class="sxs-lookup"><span data-stu-id="74e9b-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="74e9b-191">Jeśli chcesz tooreview inspekcji dane, które są powiązane toousers i grup, można znaleźć widok filtrowany w obszarze **dzienniki inspekcji** w hello **działania** sekcji hello **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="74e9b-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="74e9b-192">Ten punkt wejścia ma wartość **Użytkownicy i grupy** wstępnie wybraną dla opcji **Typ zasobu działania**.</span><span class="sxs-lookup"><span data-stu-id="74e9b-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="74e9b-193">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/93.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="74e9b-194">Dzienniki inspekcji aplikacji dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="74e9b-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="74e9b-195">Raporty dotyczące inspekcji, z aplikacji, możesz uzyskać tooquestions odpowiedzi, takich jak:</span><span class="sxs-lookup"><span data-stu-id="74e9b-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="74e9b-196">Co to są aplikacje hello, które zostały dodane lub zaktualizowane?</span><span class="sxs-lookup"><span data-stu-id="74e9b-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="74e9b-197">Co to są aplikacje hello, które zostały usunięte?</span><span class="sxs-lookup"><span data-stu-id="74e9b-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="74e9b-198">Czy usługa w ramach aplikacji została zmieniona?</span><span class="sxs-lookup"><span data-stu-id="74e9b-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="74e9b-199">Zostały zmienione nazwy aplikacji hello?</span><span class="sxs-lookup"><span data-stu-id="74e9b-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="74e9b-200">Kto udzielił zgody tooan aplikacji?</span><span class="sxs-lookup"><span data-stu-id="74e9b-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="74e9b-201">Jeśli chcesz tooreview inspekcji dane, które są powiązane tooyour aplikacji, można znaleźć widok filtrowany w obszarze **dzienniki inspekcji** w hello **działania** sekcji hello **aplikacje dla przedsiębiorstw**  bloku.</span><span class="sxs-lookup"><span data-stu-id="74e9b-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="74e9b-202">Ten punkt wejścia ma wartość **Aplikacje dla przedsiębiorstw** wstępnie wybraną dla opcji **Typ zasobu działania**.</span><span class="sxs-lookup"><span data-stu-id="74e9b-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="74e9b-203">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/134.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="74e9b-204">Można filtrować tego widoku dalsze dół toojust **grup** lub po prostu **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="74e9b-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="74e9b-205">![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/25.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="74e9b-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="74e9b-206">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74e9b-206">Next steps</span></span>

<span data-ttu-id="74e9b-207">Omówienie raportowania patrz hello [raportowania usługi Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="74e9b-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

