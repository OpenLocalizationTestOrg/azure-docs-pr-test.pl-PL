---
title: "Raporty dotyczące logowań w portalu usługi Azure Active Directory | Microsoft Docs"
description: "Wprowadzenie do raportów dotyczących logowań w portalu Azure Active Directory"
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
ms.openlocfilehash: b9e61950654ba427b09dd608d354589a0804aaa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="aeae8-103">Raporty dotyczące logowań w portalu Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aeae8-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="aeae8-104">Dzięki raportom usługi Azure Active Directory (Azure AD) w witrynie [Azure Portal](https://portal.azure.com) możesz uzyskać wszystkie informacje, które pomogą ustalić, jak działa środowisko.</span><span class="sxs-lookup"><span data-stu-id="aeae8-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="aeae8-105">Architektura raportowania w usłudze Azure Active Directory obejmuje następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="aeae8-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="aeae8-106">**Działanie**</span><span class="sxs-lookup"><span data-stu-id="aeae8-106">**Activity**</span></span> 
    - <span data-ttu-id="aeae8-107">**Działania związane z logowaniem** — informacje na temat użycia zarządzanych aplikacji i działania użytkownika związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="aeae8-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="aeae8-108">**Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu.</span><span class="sxs-lookup"><span data-stu-id="aeae8-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="aeae8-109">**Bezpieczeństwo**</span><span class="sxs-lookup"><span data-stu-id="aeae8-109">**Security**</span></span> 
    - <span data-ttu-id="aeae8-110">**Ryzykowne logowania** — ryzykowne logowanie jest wskaźnikiem próby logowania, które mogło zostać wykonane przez osobę, która nie jest prawowitym właścicielem konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aeae8-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="aeae8-111">Aby uzyskać więcej informacji, zobacz Ryzykowne logowania.</span><span class="sxs-lookup"><span data-stu-id="aeae8-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="aeae8-112">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="aeae8-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="aeae8-113">Aby uzyskać więcej informacji, zobacz Użytkownicy oflagowani w związku z ryzykiem.</span><span class="sxs-lookup"><span data-stu-id="aeae8-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="aeae8-114">Ten temat zawiera przegląd działań dotyczących logowania.</span><span class="sxs-lookup"><span data-stu-id="aeae8-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="aeae8-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="aeae8-115">Pre-requisite</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="aeae8-116">Kto ma dostęp do danych?</span><span class="sxs-lookup"><span data-stu-id="aeae8-116">Who can access the data?</span></span>
* <span data-ttu-id="aeae8-117">Użytkownicy w roli administratora zabezpieczeń lub czytelnika zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="aeae8-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="aeae8-118">Administratorzy globalni</span><span class="sxs-lookup"><span data-stu-id="aeae8-118">Global Admins</span></span>
* <span data-ttu-id="aeae8-119">Dowolny użytkownik (inny niż administrator) może uzyskać dostęp do danych na temat własnych logowań</span><span class="sxs-lookup"><span data-stu-id="aeae8-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="aeae8-120">Jaka licencja usługi Azure AD jest wymagana w celu uzyskania dostępu do informacji dotyczących logowania?</span><span class="sxs-lookup"><span data-stu-id="aeae8-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="aeae8-121">Dzierżawca musi mieć skojarzoną licencję usługi Azure AD w wersji Premium, aby wyświetlić pełny raport o wszystkich operacjach logowania</span><span class="sxs-lookup"><span data-stu-id="aeae8-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="aeae8-122">Działania związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="aeae8-122">Signs-in activities</span></span>

<span data-ttu-id="aeae8-123">Dzięki informacjom zawartym w raporcie logowania użytkownika można uzyskać odpowiedzi na pytania, takie jak:</span><span class="sxs-lookup"><span data-stu-id="aeae8-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="aeae8-124">Co to jest wzorzec logowania użytkownika?</span><span class="sxs-lookup"><span data-stu-id="aeae8-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="aeae8-125">Ilu użytkowników zalogowało się w ciągu tygodnia?</span><span class="sxs-lookup"><span data-stu-id="aeae8-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="aeae8-126">Jaki jest stan tych logowań?</span><span class="sxs-lookup"><span data-stu-id="aeae8-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="aeae8-127">Pierwszym punktem wejścia do wszystkich danych dotyczących logowania jest pozycja **Logowania** w sekcji Działania usługi **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="aeae8-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span>


<span data-ttu-id="aeae8-128">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/61.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="aeae8-129">Dziennik inspekcji zawiera domyślny widok listy, który pokazuje:</span><span class="sxs-lookup"><span data-stu-id="aeae8-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="aeae8-130">powiązanego użytkownika;</span><span class="sxs-lookup"><span data-stu-id="aeae8-130">the related user</span></span>
- <span data-ttu-id="aeae8-131">aplikację, do której zalogował się użytkownik;</span><span class="sxs-lookup"><span data-stu-id="aeae8-131">the application the user has signed-in to</span></span>
- <span data-ttu-id="aeae8-132">stan logowania;</span><span class="sxs-lookup"><span data-stu-id="aeae8-132">the sign-in status</span></span>
- <span data-ttu-id="aeae8-133">czas logowania.</span><span class="sxs-lookup"><span data-stu-id="aeae8-133">the sign-in time</span></span>

<span data-ttu-id="aeae8-134">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/41.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="aeae8-135">Możesz dostosować widok listy, klikając pozycję **Kolumny** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="aeae8-135">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="aeae8-136">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/19.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="aeae8-137">Dzięki temu możesz wyświetlić dodatkowe pola lub usunąć pola, które są już wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="aeae8-137">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="aeae8-138">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/42.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="aeae8-139">Klikając pozycję w widoku listy, możesz uzyskać wszystkie szczegóły na jej temat.</span><span class="sxs-lookup"><span data-stu-id="aeae8-139">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="aeae8-140">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/43.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="aeae8-141">Filtrowanie działań związanych z logowaniem</span><span class="sxs-lookup"><span data-stu-id="aeae8-141">Filtering sign-in activities</span></span>

<span data-ttu-id="aeae8-142">Aby zawęzić zgłaszane dane do odpowiedniego poziomu, możesz odfiltrować dane logowania przy użyciu następujących pól:</span><span class="sxs-lookup"><span data-stu-id="aeae8-142">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="aeae8-143">Przedział czasu</span><span class="sxs-lookup"><span data-stu-id="aeae8-143">Time interval</span></span>
- <span data-ttu-id="aeae8-144">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="aeae8-144">User</span></span>
- <span data-ttu-id="aeae8-145">Aplikacja</span><span class="sxs-lookup"><span data-stu-id="aeae8-145">Application</span></span>
- <span data-ttu-id="aeae8-146">Klient</span><span class="sxs-lookup"><span data-stu-id="aeae8-146">Client</span></span>
- <span data-ttu-id="aeae8-147">Stan logowania</span><span class="sxs-lookup"><span data-stu-id="aeae8-147">Sign-in status</span></span>

<span data-ttu-id="aeae8-148">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/44.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="aeae8-149">Filtr **Przedział czasu** umożliwia zdefiniowanie przedziału czasu dla zwracanych danych.</span><span class="sxs-lookup"><span data-stu-id="aeae8-149">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="aeae8-150">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="aeae8-150">Possible values are:</span></span>

- <span data-ttu-id="aeae8-151">1 miesiąc</span><span class="sxs-lookup"><span data-stu-id="aeae8-151">1 month</span></span>
- <span data-ttu-id="aeae8-152">7 dni</span><span class="sxs-lookup"><span data-stu-id="aeae8-152">7 days</span></span>
- <span data-ttu-id="aeae8-153">24 godziny</span><span class="sxs-lookup"><span data-stu-id="aeae8-153">24 hours</span></span>
- <span data-ttu-id="aeae8-154">Niestandardowy</span><span class="sxs-lookup"><span data-stu-id="aeae8-154">Custom</span></span>

<span data-ttu-id="aeae8-155">Po wybraniu niestandardowego przedziału czasu możesz skonfigurować godzinę rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="aeae8-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="aeae8-156">Filtr **Użytkownik** umożliwia określenie nazwy lub głównej nazwy użytkownika (UPN, user principal name) dla żądanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aeae8-156">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="aeae8-157">Filtr **Aplikacja** umożliwia określenie nazwy żądanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aeae8-157">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="aeae8-158">Filtr **Klient** umożliwia określenie informacji dotyczących żądanego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="aeae8-158">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="aeae8-159">Filtr **Stan logowania** umożliwia wybranie jednego z następujących filtrów:</span><span class="sxs-lookup"><span data-stu-id="aeae8-159">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="aeae8-160">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="aeae8-160">All</span></span>
- <span data-ttu-id="aeae8-161">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="aeae8-161">Success</span></span>
- <span data-ttu-id="aeae8-162">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="aeae8-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="aeae8-163">Skróty działań związanych z logowaniem</span><span class="sxs-lookup"><span data-stu-id="aeae8-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="aeae8-164">Poza usługą Azure Active Directory witryna Azure Portal zapewnia dwa dodatkowe punkty wejścia do danych dotyczących działań związanych z logowaniem:</span><span class="sxs-lookup"><span data-stu-id="aeae8-164">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="aeae8-165">Użytkownicy i grupy</span><span class="sxs-lookup"><span data-stu-id="aeae8-165">Users and groups</span></span>
- <span data-ttu-id="aeae8-166">Aplikacje dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="aeae8-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="aeae8-167">Działania związane z logowaniem użytkowników i grup</span><span class="sxs-lookup"><span data-stu-id="aeae8-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="aeae8-168">Dzięki informacjom zawartym w raporcie logowania użytkownika można uzyskać odpowiedzi na pytania, takie jak:</span><span class="sxs-lookup"><span data-stu-id="aeae8-168">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="aeae8-169">Co to jest wzorzec logowania użytkownika?</span><span class="sxs-lookup"><span data-stu-id="aeae8-169">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="aeae8-170">Ilu użytkowników zalogowało się w ciągu tygodnia?</span><span class="sxs-lookup"><span data-stu-id="aeae8-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="aeae8-171">Jaki jest stan tych logowań?</span><span class="sxs-lookup"><span data-stu-id="aeae8-171">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="aeae8-172">Punktem wyjścia do tych danych jest wykres logowania użytkownika znajdujący się w sekcji **Przegląd** w obszarze **Użytkownicy i grupy**.</span><span class="sxs-lookup"><span data-stu-id="aeae8-172">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="aeae8-173">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/45.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="aeae8-174">Wykres logowania użytkownika przedstawia tygodniowe agregacje logowań dla wszystkich użytkowników w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="aeae8-174">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="aeae8-175">Domyślny okres to 30 dni.</span><span class="sxs-lookup"><span data-stu-id="aeae8-175">The default for the time period is 30 days.</span></span>

<span data-ttu-id="aeae8-176">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/46.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="aeae8-177">Po kliknięciu dnia na wykresie logowania zostanie wyświetlona szczegółowa lista działań związanych z logowaniem dla tego dnia.</span><span class="sxs-lookup"><span data-stu-id="aeae8-177">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="aeae8-178">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/41.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="aeae8-179">Każdy wiersz na liście działań związanych z logowaniem zapewnia szczegółowe informacje o wybranym logowaniu, takie jak:</span><span class="sxs-lookup"><span data-stu-id="aeae8-179">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="aeae8-180">Kto się zalogował?</span><span class="sxs-lookup"><span data-stu-id="aeae8-180">Who has signed in?</span></span>
* <span data-ttu-id="aeae8-181">Jaka była nazwa główna użytkownika?</span><span class="sxs-lookup"><span data-stu-id="aeae8-181">What was the related UPN?</span></span>
* <span data-ttu-id="aeae8-182">Do której aplikacji się logowano?</span><span class="sxs-lookup"><span data-stu-id="aeae8-182">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="aeae8-183">Jaki jest adres IP komputera, z którego się logowano?</span><span class="sxs-lookup"><span data-stu-id="aeae8-183">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="aeae8-184">Jaki był stan logowania?</span><span class="sxs-lookup"><span data-stu-id="aeae8-184">What was the status of the sign-in?</span></span>

<span data-ttu-id="aeae8-185">Opcja **Logowania** umożliwia pełny przegląd logowań wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="aeae8-185">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="aeae8-186">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/51.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="aeae8-187">Użycie zarządzanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="aeae8-187">Usage of managed applications</span></span>

<span data-ttu-id="aeae8-188">Dzięki widokowi skoncentrowanemu na aplikacji w ramach danych logowania można uzyskać odpowiedzi na pytania, takie jak:</span><span class="sxs-lookup"><span data-stu-id="aeae8-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="aeae8-189">Kto korzysta z aplikacji?</span><span class="sxs-lookup"><span data-stu-id="aeae8-189">Who is using my applications?</span></span>
* <span data-ttu-id="aeae8-190">Jakie są 3 najczęściej używane aplikacje w organizacji?</span><span class="sxs-lookup"><span data-stu-id="aeae8-190">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="aeae8-191">Ostatnio została wdrożona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="aeae8-191">I have recently rolled out an application.</span></span> <span data-ttu-id="aeae8-192">W jaki sposób działa?</span><span class="sxs-lookup"><span data-stu-id="aeae8-192">How is it doing?</span></span>

<span data-ttu-id="aeae8-193">Punktem wyjścia do tych danych są 3 najczęściej używane aplikacje w organizacji uwzględnione w raporcie z ostatnich 30 dni znajdującym się w sekcji **Przegląd** w obszarze **Aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="aeae8-193">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="aeae8-194">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/64.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="aeae8-195">Wykres użycia aplikacji przedstawia tygodniowe agregacje logowań 3 najczęściej używanych aplikacji w danym czasie.</span><span class="sxs-lookup"><span data-stu-id="aeae8-195">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="aeae8-196">Domyślny okres to 30 dni.</span><span class="sxs-lookup"><span data-stu-id="aeae8-196">The default for the time period is 30 days.</span></span>

<span data-ttu-id="aeae8-197">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/47.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="aeae8-198">Jeśli chcesz, możesz ustawić fokus na konkretnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aeae8-198">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="aeae8-199">![Raportowanie](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Raportowanie")</span><span class="sxs-lookup"><span data-stu-id="aeae8-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="aeae8-200">Po kliknięciu dnia na wykresie użycia aplikacji zostanie wyświetlona szczegółowa lista działań związanych z logowaniem.</span><span class="sxs-lookup"><span data-stu-id="aeae8-200">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="aeae8-201">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/48.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="aeae8-202">Opcja **Logowania** umożliwia pełny przegląd zdarzeń logowania do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aeae8-202">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="aeae8-203">![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/49.png "Działania związane z logowaniem")</span><span class="sxs-lookup"><span data-stu-id="aeae8-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="aeae8-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aeae8-204">Next steps</span></span>

<span data-ttu-id="aeae8-205">Jeśli chcesz dowiedzieć się więcej na temat kodów błędów działań związanych z logowaniem, zobacz [Kody błędów w raportach działań związanych z logowaniem w portalu usługi Azure Active Directory](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="aeae8-205">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

