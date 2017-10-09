---
title: "działanie aaaFind raporty w programie hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofind działania usługi Azure Active Directory raporty w programie hello portalu Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="15624-103">Znajdź raporty aktywności w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="15624-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="15624-104">Jeśli przenosisz z hello Azure toohello portalu klasycznego portalu Azure, możesz uzyskać nowy przeglądać dzienniki aktywności w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15624-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="15624-105">W ostatnie [wpis w blogu](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), możemy wyjaśniają, jak widać, dzienniki aktywności w kontekście hello zasobu hello pracuje w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15624-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="15624-106">W tym artykule opisano sposób toofind zgłasza, że używane w hello klasycznego portalu Azure w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15624-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="15624-107">Co nowego</span><span class="sxs-lookup"><span data-stu-id="15624-107">What's new</span></span>

<span data-ttu-id="15624-108">Raporty w hello klasycznego portalu Azure są podzielone na kategorie:</span><span class="sxs-lookup"><span data-stu-id="15624-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="15624-109">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="15624-109">Security reports</span></span>
2.  <span data-ttu-id="15624-110">Raporty dotyczące działań</span><span class="sxs-lookup"><span data-stu-id="15624-110">Activity reports</span></span>
3.  <span data-ttu-id="15624-111">Raporty zintegrowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="15624-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="15624-112">Działanie i raporty zintegrowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="15624-112">Activity and integrated app reports</span></span>

<span data-ttu-id="15624-113">Kontekstowa raportowania w programie hello portalu Azure, istniejących raportów są scalane w ramach jednego widoku.</span><span class="sxs-lookup"><span data-stu-id="15624-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="15624-114">Jednej podstawowej interfejsu API zawiera hello danych toohello widok.</span><span class="sxs-lookup"><span data-stu-id="15624-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="15624-115">Ten widok na powitania toosee **usługi Azure Active Directory** bloku, w obszarze **działania**, wybierz pozycję **dzienniki inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="15624-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="15624-116">![Dzienniki inspekcji](./media/active-directory-reporting-migration/482.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="15624-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="15624-117">następujące raporty Hello są konsolidowane w tym widoku:</span><span class="sxs-lookup"><span data-stu-id="15624-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="15624-118">Raport dotyczący inspekcji</span><span class="sxs-lookup"><span data-stu-id="15624-118">Audit report</span></span>
-   <span data-ttu-id="15624-119">Działania związane z resetowaniem haseł</span><span class="sxs-lookup"><span data-stu-id="15624-119">Password reset activity</span></span>
-   <span data-ttu-id="15624-120">Aktywność rejestracji resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="15624-120">Password reset registration activity</span></span>
-   <span data-ttu-id="15624-121">Raport aktywności grup samoobsługi</span><span class="sxs-lookup"><span data-stu-id="15624-121">Self-service groups activity</span></span>
-   <span data-ttu-id="15624-122">Zmiany nazwy grupy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="15624-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="15624-123">Działanie aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="15624-123">Account provisioning activity</span></span>
-   <span data-ttu-id="15624-124">Stan przerzucania hasła</span><span class="sxs-lookup"><span data-stu-id="15624-124">Password rollover status</span></span>
-   <span data-ttu-id="15624-125">Błędy aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="15624-125">Account provisioning errors</span></span>


<span data-ttu-id="15624-126">Raport użycia aplikacji Hello został ulepszony, znajduje się w hello **logowania** widoku.</span><span class="sxs-lookup"><span data-stu-id="15624-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="15624-127">Ten widok na powitania toosee **usługi Azure Active Directory** bloku, w obszarze **działania**, wybierz pozycję **logowania**.</span><span class="sxs-lookup"><span data-stu-id="15624-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="15624-128">![Widok logowania](./media/active-directory-reporting-migration/483.png "wyświetlić logowania")</span><span class="sxs-lookup"><span data-stu-id="15624-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="15624-129">Witaj **logowania** widok zawiera sesje logowania użytkownika. Można użyć tych informacji tooget aplikacji użycia informacji.</span><span class="sxs-lookup"><span data-stu-id="15624-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="15624-130">Również można wyświetlić informacje na temat wykorzystania aplikacji w hello **aplikacje dla przedsiębiorstw** omówienie w hello **ZARZĄDZAJ** sekcji.</span><span class="sxs-lookup"><span data-stu-id="15624-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="15624-131">![Aplikacje dla przedsiębiorstw](./media/active-directory-reporting-migration/484.png "aplikacje dla przedsiębiorstw")</span><span class="sxs-lookup"><span data-stu-id="15624-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="15624-132">Dostęp do określonego raportu</span><span class="sxs-lookup"><span data-stu-id="15624-132">Access a specific report</span></span>

<span data-ttu-id="15624-133">Mimo że hello portalu Azure oferuje pojedynczego widoku, także zapoznanie się z określonych raportów.</span><span class="sxs-lookup"><span data-stu-id="15624-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="15624-134">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="15624-134">Audit logs</span></span>

<span data-ttu-id="15624-135">W odpowiedzi toocustomer opinii w hello portalu Azure, można użyć zaawansowanych filtrowania tooaccess hello żądane dane.</span><span class="sxs-lookup"><span data-stu-id="15624-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="15624-136">Jest jeden filtr, można użyć *kategorii działań*, który wyświetla listę różnych typów hello działania logowania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15624-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="15624-137">toonarrow powoduje toowhat, którego szukasz, możesz wybrać kategorię.</span><span class="sxs-lookup"><span data-stu-id="15624-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="15624-138">Na przykład jeśli interesuje Cię tylko resetuje powiązane hasło usługi tooself działań, możesz wybrać hello **Samoobsługowe zarządzanie hasłami** kategorii.</span><span class="sxs-lookup"><span data-stu-id="15624-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="15624-139">kategorie Hello, dostępne są oparte na powitania zasób, który użytkownik pracuje w.</span><span class="sxs-lookup"><span data-stu-id="15624-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="15624-140">![Opcje kategorii na stronie dzienniki inspekcji filtru hello](./media/active-directory-reporting-migration/06.png "opcje kategorii na stronie dzienniki inspekcji filtru hello")</span><span class="sxs-lookup"><span data-stu-id="15624-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="15624-141">Kategorie działań:</span><span class="sxs-lookup"><span data-stu-id="15624-141">Activity categories include:</span></span>

- <span data-ttu-id="15624-142">Katalog podstawowy</span><span class="sxs-lookup"><span data-stu-id="15624-142">Core Directory</span></span>
- <span data-ttu-id="15624-143">Samoobsługowe zarządzanie hasłami</span><span class="sxs-lookup"><span data-stu-id="15624-143">Self-service Password Management</span></span>
- <span data-ttu-id="15624-144">Samoobsługowe zarządzanie grupami</span><span class="sxs-lookup"><span data-stu-id="15624-144">Self-service Group Management</span></span>
- <span data-ttu-id="15624-145">Aprowizacja kont</span><span class="sxs-lookup"><span data-stu-id="15624-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="15624-146">Użycie aplikacji</span><span class="sxs-lookup"><span data-stu-id="15624-146">Application usage</span></span>

<span data-ttu-id="15624-147">tooview szczegółowe informacje dotyczące użycia aplikacji dla wszystkich aplikacji lub tylko jednej aplikacji w obszarze **działania**, wybierz pozycję **logowania**. wyniki hello toonarrow, można filtrować według nazwy użytkownika lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15624-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="15624-148">![Filtr zdarzeń logowania strony](./media/active-directory-reporting-migration/07.png "strony filtr rejestrowania zdarzeń")</span><span class="sxs-lookup"><span data-stu-id="15624-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="15624-149">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="15624-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="15624-150">Raporty nietypowe działanie usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="15624-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="15624-151">Zabezpieczeń nietypowe działania usługi Azure AD raportów z klasycznego portalu Azure hello zostać skonsolidowane tooprovide można z nich, widokiem centralnej.</span><span class="sxs-lookup"><span data-stu-id="15624-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="15624-152">Ten widok przedstawia wszystkie zdarzenia związane z zabezpieczeniami ryzyka może wykrywać i raport dotyczący usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15624-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="15624-153">Witaj w poniższej tabeli wymieniono raporty dotyczące zabezpieczeń nietypowych działań hello Azure AD i odpowiednie typy zdarzeń ryzyko w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15624-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="15624-154">Raport nietypowych działań w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="15624-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="15624-155">Typ zdarzenia ryzyka ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="15624-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="15624-156">Użytkownicy z ujawnionymi poświadczeniami</span><span class="sxs-lookup"><span data-stu-id="15624-156">Users with leaked credentials</span></span> | <span data-ttu-id="15624-157">Ujawnione poświadczenia</span><span class="sxs-lookup"><span data-stu-id="15624-157">Leaked credentials</span></span> |
| <span data-ttu-id="15624-158">Nieregularne działania związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="15624-158">Irregular sign-in activity</span></span> | <span data-ttu-id="15624-159">Niemożliwa podróż tooatypical lokalizacji</span><span class="sxs-lookup"><span data-stu-id="15624-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="15624-160">Logowania z urządzeń, które mogą być zainfekowane</span><span class="sxs-lookup"><span data-stu-id="15624-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="15624-161">Logowania z zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="15624-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="15624-162">Logowania z nieznanych źródeł</span><span class="sxs-lookup"><span data-stu-id="15624-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="15624-163">Logowania z anonimowych adresów IP</span><span class="sxs-lookup"><span data-stu-id="15624-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="15624-164">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="15624-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="15624-165">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="15624-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="15624-166">Logowania z nieznanych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="15624-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="15624-167">Raporty powitania po zabezpieczeń nietypowe działania usługi Azure AD nie są uwzględniane jako zdarzenia ryzyka w hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="15624-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="15624-168">Logowania po wielokrotnych niepowodzeniach</span><span class="sxs-lookup"><span data-stu-id="15624-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="15624-169">Logowania z wielu lokalizacji geograficznych</span><span class="sxs-lookup"><span data-stu-id="15624-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="15624-170">Te raporty są nadal dostępne w hello klasycznego portalu Azure, ale zostaną wycofane w czasie w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="15624-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="15624-171">Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="15624-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="15624-172">Zdarzenia wykrytego ryzyka</span><span class="sxs-lookup"><span data-stu-id="15624-172">Detected risk events</span></span>

<span data-ttu-id="15624-173">W portalu Azure hello, można dostęp do raportów o zdarzeniach wykryte zagrożenie na powitania **usługi Azure Active Directory** bloku, w obszarze **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="15624-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="15624-174">Zdarzenia wykrytego ryzyka są śledzone w hello następujące raporty:</span><span class="sxs-lookup"><span data-stu-id="15624-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="15624-175">Zagrożonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="15624-175">Users at Risk</span></span>
- <span data-ttu-id="15624-176">Ryzykowne logowania</span><span class="sxs-lookup"><span data-stu-id="15624-176">Risky Sign-ins</span></span>

<span data-ttu-id="15624-177">![Raporty dotyczące zabezpieczeń](./media/active-directory-reporting-migration/04.png "raporty dotyczące zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="15624-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="15624-178">Aby uzyskać więcej informacji o raportach zabezpieczeń zobacz:</span><span class="sxs-lookup"><span data-stu-id="15624-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="15624-179">Użytkownicy ryzyka raport zabezpieczeń w portalu usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="15624-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="15624-180">Ryzykowne raportu logowania w portalu usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="15624-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="15624-181">Raporty dotyczące działań w hello klasycznego portalu Azure a hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="15624-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="15624-182">w tej sekcji tabela Hello zawiera listę istniejących raportów w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15624-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="15624-183">Ponadto opisano, jak wprowadzasz hello tych samych informacji w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15624-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="15624-184">tooview wszystkie inspekcja danych na powitania **usługi Azure Active Directory** bloku, w obszarze **działania**, przejdź zbyt**dzienniki inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="15624-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="15624-185">![Dzienniki inspekcji](./media/active-directory-reporting-migration/61.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="15624-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="15624-186">klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="15624-186">Azure classic portal</span></span>                 | <span data-ttu-id="15624-187">toofind w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="15624-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="15624-188">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="15624-188">Audit logs</span></span>                           | <span data-ttu-id="15624-189">Dla **kategorii działań**, wybierz pozycję **katalogu Core**.</span><span class="sxs-lookup"><span data-stu-id="15624-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="15624-190">Działania związane z resetowaniem haseł</span><span class="sxs-lookup"><span data-stu-id="15624-190">Password reset activity</span></span>              | <span data-ttu-id="15624-191">Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**.</span><span class="sxs-lookup"><span data-stu-id="15624-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="15624-192">Aktywność rejestracji resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="15624-192">Password reset registration activity</span></span> | <span data-ttu-id="15624-193">Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**.</span><span class="sxs-lookup"><span data-stu-id="15624-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="15624-194">Raport aktywności grup samoobsługi</span><span class="sxs-lookup"><span data-stu-id="15624-194">Self-service groups activity</span></span>         | <span data-ttu-id="15624-195">Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie grupami**.</span><span class="sxs-lookup"><span data-stu-id="15624-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="15624-196">Działanie aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="15624-196">Account provisioning activity</span></span>        | <span data-ttu-id="15624-197">Aby uzyskać **kategorii działań**, wybierz pozycję **Inicjowanie obsługi konta użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="15624-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="15624-198">Stan przerzucania hasła</span><span class="sxs-lookup"><span data-stu-id="15624-198">Password rollover status</span></span>             | <span data-ttu-id="15624-199">Aby uzyskać **kategorii działań**, wybierz pozycję **automatycznego przerzucania hasła aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="15624-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="15624-200">Błędy aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="15624-200">Account provisioning errors</span></span>          | <span data-ttu-id="15624-201">Aby uzyskać **kategorii działań**, wybierz pozycję **Inicjowanie obsługi konta użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="15624-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="15624-202">Zmiany nazwy grupy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="15624-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="15624-203">Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**.</span><span class="sxs-lookup"><span data-stu-id="15624-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="15624-204">Dla **typu zasobu działania**, wybierz pozycję **grupy**.</span><span class="sxs-lookup"><span data-stu-id="15624-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="15624-205">Aby uzyskać **źródło działania**, wybierz pozycję **grup usługi Office 365**.</span><span class="sxs-lookup"><span data-stu-id="15624-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="15624-206">tooview hello **użycia aplikacji** raportu na powitania **usługi Azure Active Directory** bloku, w obszarze **ZARZĄDZAJ**, wybierz pozycję **aplikacje dla przedsiębiorstw**, a następnie wybierz **logowania**.</span><span class="sxs-lookup"><span data-stu-id="15624-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="15624-207">![Raport logowania aplikacji przedsiębiorstwa](./media/active-directory-reporting-migration/199.png "raport logowania aplikacji przedsiębiorstwa")</span><span class="sxs-lookup"><span data-stu-id="15624-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="15624-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15624-208">Next steps</span></span>

<span data-ttu-id="15624-209">Omówienie raportowania patrz hello [raportowania usługi Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15624-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
