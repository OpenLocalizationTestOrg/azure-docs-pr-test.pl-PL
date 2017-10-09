---
title: "działanie aaaSign raportów w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Wprowadzenie działanie toosign raportów w portalu usługi Azure Active Directory hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="8cf07-103">Raporty aktywności logowania w portalu usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="8cf07-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="8cf07-104">Z usługi Azure Active Directory (Azure AD) raportowania w programie hello [portalu Azure](https://portal.azure.com), można uzyskać informacji hello należy toodetermine jak robi środowiska.</span><span class="sxs-lookup"><span data-stu-id="8cf07-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="8cf07-105">Hello raportowania architektury w usłudze Azure Active Directory obejmuje hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="8cf07-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="8cf07-106">**Działanie**</span><span class="sxs-lookup"><span data-stu-id="8cf07-106">**Activity**</span></span> 
    - <span data-ttu-id="8cf07-107">**Działania logowania** — informacje na temat użycia hello zarządzanych aplikacji i aktywności logowania użytkowników</span><span class="sxs-lookup"><span data-stu-id="8cf07-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="8cf07-108">**Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu.</span><span class="sxs-lookup"><span data-stu-id="8cf07-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="8cf07-109">**Bezpieczeństwo**</span><span class="sxs-lookup"><span data-stu-id="8cf07-109">**Security**</span></span> 
    - <span data-ttu-id="8cf07-110">**Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8cf07-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="8cf07-111">Aby uzyskać więcej informacji, zobacz Ryzykowne logowania.</span><span class="sxs-lookup"><span data-stu-id="8cf07-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="8cf07-112">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="8cf07-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="8cf07-113">Aby uzyskać więcej informacji, zobacz Użytkownicy oflagowani w związku z ryzykiem.</span><span class="sxs-lookup"><span data-stu-id="8cf07-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="8cf07-114">Ten temat zawiera omówienie hello logowania działań.</span><span class="sxs-lookup"><span data-stu-id="8cf07-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="8cf07-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8cf07-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="8cf07-116">Kto ma dostęp do danych hello?</span><span class="sxs-lookup"><span data-stu-id="8cf07-116">Who can access hello data?</span></span>
* <span data-ttu-id="8cf07-117">Użytkowników w roli administratora zabezpieczeń lub czytnika zabezpieczeń hello</span><span class="sxs-lookup"><span data-stu-id="8cf07-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="8cf07-118">Administratorzy globalni</span><span class="sxs-lookup"><span data-stu-id="8cf07-118">Global Admins</span></span>
* <span data-ttu-id="8cf07-119">Dowolny użytkownik (inny niż administrator) może uzyskać dostęp do danych na temat własnych logowań</span><span class="sxs-lookup"><span data-stu-id="8cf07-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="8cf07-120">Jakie licencji usługi Azure AD potrzebujesz tooaccess logowania działania?</span><span class="sxs-lookup"><span data-stu-id="8cf07-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="8cf07-121">Dzierżawy musi mieć licencję programu Azure AD Premium, skojarzone z nim toosee hello nawet wszystkich działań logowania raportu</span><span class="sxs-lookup"><span data-stu-id="8cf07-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="8cf07-122">Działania związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="8cf07-122">Signs-in activities</span></span>

<span data-ttu-id="8cf07-123">Informacje hello dostarczone przez użytkownika hello logowania raportu można znaleźć tooquestions odpowiedzi, takich jak:</span><span class="sxs-lookup"><span data-stu-id="8cf07-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="8cf07-124">Co to jest hello logowania wzorzec użytkownika?</span><span class="sxs-lookup"><span data-stu-id="8cf07-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="8cf07-125">Ilu użytkowników zalogowało się w ciągu tygodnia?</span><span class="sxs-lookup"><span data-stu-id="8cf07-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="8cf07-126">Co to jest hello stan tych logowania?</span><span class="sxs-lookup"><span data-stu-id="8cf07-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="8cf07-127">Pierwszy wpis punktu tooall logowania działań dane są **logowania** w sekcji działania hello **usługi Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="8cf07-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="8cf07-128">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/61.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="8cf07-129">Dziennik inspekcji zawiera domyślny widok listy, który pokazuje:</span><span class="sxs-lookup"><span data-stu-id="8cf07-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="8cf07-130">Witaj użytkownikowi</span><span class="sxs-lookup"><span data-stu-id="8cf07-130">hello related user</span></span>
- <span data-ttu-id="8cf07-131">Użytkownik hello aplikacji Hello jest zalogowany do</span><span class="sxs-lookup"><span data-stu-id="8cf07-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="8cf07-132">Witaj stan logowania</span><span class="sxs-lookup"><span data-stu-id="8cf07-132">hello sign-in status</span></span>
- <span data-ttu-id="8cf07-133">czas logowania Hello</span><span class="sxs-lookup"><span data-stu-id="8cf07-133">hello sign-in time</span></span>

<span data-ttu-id="8cf07-134">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/41.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="8cf07-135">Można dostosować widok listy hello klikając **kolumn** hello w pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="8cf07-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="8cf07-136">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/19.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="8cf07-137">To pozwala toodisplay dodatkowe pola lub usuń pola, które są już wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="8cf07-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="8cf07-138">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/42.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="8cf07-139">Po kliknięciu elementu w widoku listy hello, otrzymasz wszystkich dostępnych informacji o nim.</span><span class="sxs-lookup"><span data-stu-id="8cf07-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="8cf07-140">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/43.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="8cf07-141">Filtrowanie działań związanych z logowaniem</span><span class="sxs-lookup"><span data-stu-id="8cf07-141">Filtering sign-in activities</span></span>

<span data-ttu-id="8cf07-142">toonarrow dół hello zgłoszone poziom tooa danych czy działa dla Ciebie, dane można filtrować hello logowania przy użyciu hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="8cf07-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="8cf07-143">Przedział czasu</span><span class="sxs-lookup"><span data-stu-id="8cf07-143">Time interval</span></span>
- <span data-ttu-id="8cf07-144">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="8cf07-144">User</span></span>
- <span data-ttu-id="8cf07-145">Aplikacja</span><span class="sxs-lookup"><span data-stu-id="8cf07-145">Application</span></span>
- <span data-ttu-id="8cf07-146">Klient</span><span class="sxs-lookup"><span data-stu-id="8cf07-146">Client</span></span>
- <span data-ttu-id="8cf07-147">Stan logowania</span><span class="sxs-lookup"><span data-stu-id="8cf07-147">Sign-in status</span></span>

<span data-ttu-id="8cf07-148">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/44.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="8cf07-149">Witaj **interwał czasu** filtru umożliwia tooyou toodefine przedział czasu dla hello zwróciła dane.</span><span class="sxs-lookup"><span data-stu-id="8cf07-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="8cf07-150">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="8cf07-150">Possible values are:</span></span>

- <span data-ttu-id="8cf07-151">1 miesiąc</span><span class="sxs-lookup"><span data-stu-id="8cf07-151">1 month</span></span>
- <span data-ttu-id="8cf07-152">7 dni</span><span class="sxs-lookup"><span data-stu-id="8cf07-152">7 days</span></span>
- <span data-ttu-id="8cf07-153">24 godziny</span><span class="sxs-lookup"><span data-stu-id="8cf07-153">24 hours</span></span>
- <span data-ttu-id="8cf07-154">Niestandardowy</span><span class="sxs-lookup"><span data-stu-id="8cf07-154">Custom</span></span>

<span data-ttu-id="8cf07-155">Po wybraniu niestandardowego przedziału czasu możesz skonfigurować godzinę rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="8cf07-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="8cf07-156">Witaj **użytkownika** filtru pozwala toospecify hello nazwy lub hello główna nazwa użytkownika (UPN) użytkownika hello są dla Ciebie ważne.</span><span class="sxs-lookup"><span data-stu-id="8cf07-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="8cf07-157">Witaj **aplikacji** filtr włącza nazwa hello toospecify aplikacji hello są dla Ciebie ważne.</span><span class="sxs-lookup"><span data-stu-id="8cf07-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="8cf07-158">Witaj **klienta** filtr włącza toospecify informacji na temat urządzeń hello są dla Ciebie ważne.</span><span class="sxs-lookup"><span data-stu-id="8cf07-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="8cf07-159">Witaj **stan logowania** filtr włącza tooselect hello następującego filtru:</span><span class="sxs-lookup"><span data-stu-id="8cf07-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="8cf07-160">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="8cf07-160">All</span></span>
- <span data-ttu-id="8cf07-161">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="8cf07-161">Success</span></span>
- <span data-ttu-id="8cf07-162">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="8cf07-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="8cf07-163">Skróty działań związanych z logowaniem</span><span class="sxs-lookup"><span data-stu-id="8cf07-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="8cf07-164">Ponadto tooAzure usługi Active Directory, hello portalu Azure zapewnia dwa danych działania toosign w punkty wejścia dodatkowe:</span><span class="sxs-lookup"><span data-stu-id="8cf07-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="8cf07-165">Użytkownicy i grupy</span><span class="sxs-lookup"><span data-stu-id="8cf07-165">Users and groups</span></span>
- <span data-ttu-id="8cf07-166">Aplikacje dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="8cf07-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="8cf07-167">Działania związane z logowaniem użytkowników i grup</span><span class="sxs-lookup"><span data-stu-id="8cf07-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="8cf07-168">Informacje hello dostarczone przez użytkownika hello logowania raportu można znaleźć tooquestions odpowiedzi, takich jak:</span><span class="sxs-lookup"><span data-stu-id="8cf07-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="8cf07-169">Co to jest hello logowania wzorzec użytkownika?</span><span class="sxs-lookup"><span data-stu-id="8cf07-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="8cf07-170">Ilu użytkowników zalogowało się w ciągu tygodnia?</span><span class="sxs-lookup"><span data-stu-id="8cf07-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="8cf07-171">Co to jest hello stan tych logowania?</span><span class="sxs-lookup"><span data-stu-id="8cf07-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="8cf07-172">Dane toothis punktu wejścia jest wykres logowania użytkownika hello w hello **omówienie** w obszarze **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8cf07-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="8cf07-173">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/45.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="8cf07-174">Witaj użytkownika logowania wykres przedstawia tygodniowy agregacji znaku dodatków dla wszystkich użytkowników w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="8cf07-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="8cf07-175">Domyślna Hello hello okres to 30 dni.</span><span class="sxs-lookup"><span data-stu-id="8cf07-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="8cf07-176">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/46.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="8cf07-177">Po kliknięciu w dniu wykresie hello logowania otrzymasz szczegółową listę hello logowania działań w tym dniu.</span><span class="sxs-lookup"><span data-stu-id="8cf07-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="8cf07-178">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/41.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="8cf07-179">Każdy wiersz w oferuje listę działań logowania hello hello szczegółowe informacje na temat hello wybrane logowania takich jak:</span><span class="sxs-lookup"><span data-stu-id="8cf07-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="8cf07-180">Kto się zalogował?</span><span class="sxs-lookup"><span data-stu-id="8cf07-180">Who has signed in?</span></span>
* <span data-ttu-id="8cf07-181">Jaka była hello powiązane UPN?</span><span class="sxs-lookup"><span data-stu-id="8cf07-181">What was hello related UPN?</span></span>
* <span data-ttu-id="8cf07-182">Jakie aplikacja została docelowy hello logowania hello?</span><span class="sxs-lookup"><span data-stu-id="8cf07-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="8cf07-183">Co to jest hello adres IP logowania hello?</span><span class="sxs-lookup"><span data-stu-id="8cf07-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="8cf07-184">Jaki był stan hello logowania hello?</span><span class="sxs-lookup"><span data-stu-id="8cf07-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="8cf07-185">Witaj **logowania** opcja umożliwia pełny przegląd sesje logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8cf07-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="8cf07-186">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/51.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="8cf07-187">Użycie zarządzanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="8cf07-187">Usage of managed applications</span></span>

<span data-ttu-id="8cf07-188">Dzięki widokowi skoncentrowanemu na aplikacji w ramach danych logowania można uzyskać odpowiedzi na pytania, takie jak:</span><span class="sxs-lookup"><span data-stu-id="8cf07-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="8cf07-189">Kto korzysta z aplikacji?</span><span class="sxs-lookup"><span data-stu-id="8cf07-189">Who is using my applications?</span></span>
* <span data-ttu-id="8cf07-190">Co to jest pierwsze 3 aplikacji hello w organizacji?</span><span class="sxs-lookup"><span data-stu-id="8cf07-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="8cf07-191">Ostatnio została wdrożona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="8cf07-191">I have recently rolled out an application.</span></span> <span data-ttu-id="8cf07-192">W jaki sposób działa?</span><span class="sxs-lookup"><span data-stu-id="8cf07-192">How is it doing?</span></span>

<span data-ttu-id="8cf07-193">Dane toothis punktu wejścia jest pierwsze 3 aplikacji hello w Twojej organizacji w raporcie ostatnich 30 dni hello w hello **omówienie** w obszarze **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8cf07-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="8cf07-194">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/64.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="8cf07-195">Hello aplikacji użycia wykresu co tydzień agregacji logowania dla aplikacji 3 pierwszych w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="8cf07-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="8cf07-196">Domyślna Hello hello okres to 30 dni.</span><span class="sxs-lookup"><span data-stu-id="8cf07-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="8cf07-197">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/47.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="8cf07-198">Jeśli chcesz, można ustawić fokusu hello na określonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8cf07-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="8cf07-199">![Raportowanie](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Raportowanie")</span><span class="sxs-lookup"><span data-stu-id="8cf07-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="8cf07-200">Po kliknięciu w dniu wykresie użycia aplikacji hello otrzymasz szczegółową listę hello logowania działań.</span><span class="sxs-lookup"><span data-stu-id="8cf07-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="8cf07-201">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/48.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="8cf07-202">Witaj **logowania** opcja umożliwia pełny przegląd wszystkich aplikacji tooyour zdarzenia logowania.</span><span class="sxs-lookup"><span data-stu-id="8cf07-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="8cf07-203">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/49.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="8cf07-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="8cf07-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8cf07-204">Next steps</span></span>

<span data-ttu-id="8cf07-205">Więcej informacji na temat aktywności logowania kody błędów tooknow, zobacz hello [logowania kody błędów raportu działania w portalu usługi Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="8cf07-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

