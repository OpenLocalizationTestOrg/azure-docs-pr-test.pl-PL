---
title: "Znajdź raporty dotyczące działań w portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak znaleźć raporty działania usługi Azure Active Directory w portalu Azure."
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
ms.openlocfilehash: f1875582476c3817b9eb0082b6548cc15043cb98
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="c6e85-103">Znajdź raporty dotyczące działań w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6e85-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="c6e85-104">Jeśli przenosisz z klasycznego portalu Azure w portalu Azure, możesz uzyskać wygląda na dzienniki aktywności w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6e85-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="c6e85-105">W ostatnie [wpis w blogu](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), możemy wyjaśniają, jak widać, dzienniki aktywności w kontekście zasobów pracuje w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e85-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span></span> <span data-ttu-id="c6e85-106">W tym artykule opisano firma Microsoft, jak można znaleźć raporty, które były używane w klasycznym portalu Azure w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e85-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="c6e85-107">Co nowego</span><span class="sxs-lookup"><span data-stu-id="c6e85-107">What's new</span></span>

<span data-ttu-id="c6e85-108">Raporty w klasycznym portalu Azure są podzielone na kategorie:</span><span class="sxs-lookup"><span data-stu-id="c6e85-108">Reports in the Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="c6e85-109">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c6e85-109">Security reports</span></span>
2.  <span data-ttu-id="c6e85-110">Raporty dotyczące działań</span><span class="sxs-lookup"><span data-stu-id="c6e85-110">Activity reports</span></span>
3.  <span data-ttu-id="c6e85-111">Raporty zintegrowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="c6e85-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="c6e85-112">Działanie i raporty zintegrowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="c6e85-112">Activity and integrated app reports</span></span>

<span data-ttu-id="c6e85-113">Kontekstowa raportowanie w portalu Azure, istniejących raportów są scalane w ramach jednego widoku.</span><span class="sxs-lookup"><span data-stu-id="c6e85-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="c6e85-114">Jeden podstawowy interfejs API udostępnia dane do widoku.</span><span class="sxs-lookup"><span data-stu-id="c6e85-114">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="c6e85-115">Do wyświetlenia tego widoku na **usługi Azure Active Directory** bloku, w obszarze **działania**, wybierz pozycję **dzienniki inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="c6e85-116">![Dzienniki inspekcji](./media/active-directory-reporting-migration/482.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="c6e85-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="c6e85-117">Następujące raporty są konsolidowane w tym widoku:</span><span class="sxs-lookup"><span data-stu-id="c6e85-117">The following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="c6e85-118">Raport dotyczący inspekcji</span><span class="sxs-lookup"><span data-stu-id="c6e85-118">Audit report</span></span>
-   <span data-ttu-id="c6e85-119">Działania związane z resetowaniem haseł</span><span class="sxs-lookup"><span data-stu-id="c6e85-119">Password reset activity</span></span>
-   <span data-ttu-id="c6e85-120">Aktywność rejestracji resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="c6e85-120">Password reset registration activity</span></span>
-   <span data-ttu-id="c6e85-121">Raport aktywności grup samoobsługi</span><span class="sxs-lookup"><span data-stu-id="c6e85-121">Self-service groups activity</span></span>
-   <span data-ttu-id="c6e85-122">Zmiany nazwy grupy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="c6e85-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="c6e85-123">Działanie aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="c6e85-123">Account provisioning activity</span></span>
-   <span data-ttu-id="c6e85-124">Stan przerzucania hasła</span><span class="sxs-lookup"><span data-stu-id="c6e85-124">Password rollover status</span></span>
-   <span data-ttu-id="c6e85-125">Błędy aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="c6e85-125">Account provisioning errors</span></span>


<span data-ttu-id="c6e85-126">Raport użycia aplikacji zostały rozszerzone i znajduje się w **logowania** widoku.</span><span class="sxs-lookup"><span data-stu-id="c6e85-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="c6e85-127">Aby wyświetlić ten widok na **usługi Azure Active Directory** bloku, w obszarze **działania**, wybierz pozycję **logowania**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="c6e85-128">![Widok logowania](./media/active-directory-reporting-migration/483.png "wyświetlić logowania")</span><span class="sxs-lookup"><span data-stu-id="c6e85-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="c6e85-129">**Logowania** widok zawiera sesje logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6e85-129">The **Sign-ins** view includes all user sign-ins.</span></span> <span data-ttu-id="c6e85-130">Aby uzyskać informacje na temat wykorzystania aplikacji, można użyć tych informacji.</span><span class="sxs-lookup"><span data-stu-id="c6e85-130">You can use this information to get application usage information.</span></span> <span data-ttu-id="c6e85-131">Możesz również przeglądać informacje użycia aplikacji w **aplikacje dla przedsiębiorstw** omówienie w **ZARZĄDZAJ** sekcji.</span><span class="sxs-lookup"><span data-stu-id="c6e85-131">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="c6e85-132">![Aplikacje dla przedsiębiorstw](./media/active-directory-reporting-migration/484.png "aplikacje dla przedsiębiorstw")</span><span class="sxs-lookup"><span data-stu-id="c6e85-132">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="c6e85-133">Dostęp do określonego raportu</span><span class="sxs-lookup"><span data-stu-id="c6e85-133">Access a specific report</span></span>

<span data-ttu-id="c6e85-134">Mimo że portalu Azure oferuje pojedynczego widoku, także zapoznanie się z określonych raportów.</span><span class="sxs-lookup"><span data-stu-id="c6e85-134">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="c6e85-135">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="c6e85-135">Audit logs</span></span>

<span data-ttu-id="c6e85-136">W odpowiedzi na opinie klientów, w portalu Azure możesz użyć filtrowania zaawansowanego dostępu do danych, które mają.</span><span class="sxs-lookup"><span data-stu-id="c6e85-136">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="c6e85-137">Jest jeden filtr, można użyć *kategorii działań*, który zawiera różne typy aktywności logowania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6e85-137">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="c6e85-138">Aby ograniczyć wyniki do czego szukasz, możesz wybrać kategorię.</span><span class="sxs-lookup"><span data-stu-id="c6e85-138">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="c6e85-139">Na przykład, jeśli interesuje Cię tylko działania związane z resetowanie haseł samoobsługi, można wybierać **Samoobsługowe zarządzanie hasłami** kategorii.</span><span class="sxs-lookup"><span data-stu-id="c6e85-139">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="c6e85-140">Kategorie dostępne są oparte na zasób, do którego użytkownik pracuje w.</span><span class="sxs-lookup"><span data-stu-id="c6e85-140">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="c6e85-141">![Na stronie dzienniki inspekcji filtr kategorii opcje](./media/active-directory-reporting-migration/06.png "opcje kategorii na stronie dzienniki inspekcji filtru")</span><span class="sxs-lookup"><span data-stu-id="c6e85-141">![Category options on the Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="c6e85-142">Kategorie działań:</span><span class="sxs-lookup"><span data-stu-id="c6e85-142">Activity categories include:</span></span>

- <span data-ttu-id="c6e85-143">Katalog podstawowy</span><span class="sxs-lookup"><span data-stu-id="c6e85-143">Core Directory</span></span>
- <span data-ttu-id="c6e85-144">Samoobsługowe zarządzanie hasłami</span><span class="sxs-lookup"><span data-stu-id="c6e85-144">Self-service Password Management</span></span>
- <span data-ttu-id="c6e85-145">Samoobsługowe zarządzanie grupami</span><span class="sxs-lookup"><span data-stu-id="c6e85-145">Self-service Group Management</span></span>
- <span data-ttu-id="c6e85-146">Aprowizacja kont</span><span class="sxs-lookup"><span data-stu-id="c6e85-146">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="c6e85-147">Użycie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c6e85-147">Application usage</span></span>

<span data-ttu-id="c6e85-148">Aby wyświetlić szczegóły dotyczące użycia aplikacji dla wszystkich aplikacji lub tylko jednej aplikacji w obszarze **działania**, wybierz pozycję **logowania**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-148">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**.</span></span> <span data-ttu-id="c6e85-149">Aby zawęzić wyniki, można filtrować według nazwy użytkownika lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6e85-149">To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="c6e85-150">![Filtr zdarzeń logowania strony](./media/active-directory-reporting-migration/07.png "strony filtr rejestrowania zdarzeń")</span><span class="sxs-lookup"><span data-stu-id="c6e85-150">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="c6e85-151">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c6e85-151">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="c6e85-152">Raporty nietypowe działanie usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6e85-152">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="c6e85-153">Azure AD nietypowego działania zabezpieczeń raportów z klasycznego portalu Azure zostały skonsolidowane dostarczają jeden, widok centralnej.</span><span class="sxs-lookup"><span data-stu-id="c6e85-153">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span></span> <span data-ttu-id="c6e85-154">Ten widok przedstawia wszystkie zdarzenia związane z zabezpieczeniami ryzyka może wykrywać i raport dotyczący usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6e85-154">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="c6e85-155">Następujące tabeli list programu Azure AD nietypowego działania zabezpieczeń raportów i odpowiednie typy zdarzeń ryzyko w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e85-155">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="c6e85-156">Raport nietypowych działań w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6e85-156">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="c6e85-157">Typ zdarzenia ryzyka ochrony tożsamości</span><span class="sxs-lookup"><span data-stu-id="c6e85-157">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="c6e85-158">Użytkownicy z ujawnionymi poświadczeniami</span><span class="sxs-lookup"><span data-stu-id="c6e85-158">Users with leaked credentials</span></span> | <span data-ttu-id="c6e85-159">Ujawnione poświadczenia</span><span class="sxs-lookup"><span data-stu-id="c6e85-159">Leaked credentials</span></span> |
| <span data-ttu-id="c6e85-160">Nieregularne działania związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="c6e85-160">Irregular sign-in activity</span></span> | <span data-ttu-id="c6e85-161">Niemożliwa podróż do nietypowych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="c6e85-161">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="c6e85-162">Logowania z urządzeń, które mogą być zainfekowane</span><span class="sxs-lookup"><span data-stu-id="c6e85-162">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="c6e85-163">Logowania z zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="c6e85-163">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="c6e85-164">Logowania z nieznanych źródeł</span><span class="sxs-lookup"><span data-stu-id="c6e85-164">Sign-ins from unknown sources</span></span> | <span data-ttu-id="c6e85-165">Logowania z anonimowych adresów IP</span><span class="sxs-lookup"><span data-stu-id="c6e85-165">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="c6e85-166">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="c6e85-166">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="c6e85-167">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="c6e85-167">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="c6e85-168">Logowania z nieznanych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="c6e85-168">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="c6e85-169">Następujące zabezpieczeń usługi Azure AD w nietypowych działań raporty nie są uwzględniane jako zdarzenia ryzyka w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="c6e85-169">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="c6e85-170">Logowania po wielokrotnych niepowodzeniach</span><span class="sxs-lookup"><span data-stu-id="c6e85-170">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="c6e85-171">Logowania z wielu lokalizacji geograficznych</span><span class="sxs-lookup"><span data-stu-id="c6e85-171">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="c6e85-172">Te raporty są nadal dostępne w klasycznym portalu Azure, ale zostaną wycofane w czasie w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c6e85-172">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span></span>

<span data-ttu-id="c6e85-173">Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="c6e85-173">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="c6e85-174">Zdarzenia wykrytego ryzyka</span><span class="sxs-lookup"><span data-stu-id="c6e85-174">Detected risk events</span></span>

<span data-ttu-id="c6e85-175">W portalu Azure, możesz mogą uzyskiwać dostęp do raportów o zdarzeniach wykryte zagrożenie **usługi Azure Active Directory** bloku, w obszarze **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-175">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="c6e85-176">Zdarzenia wykrytego ryzyka są śledzone w następujące raporty:</span><span class="sxs-lookup"><span data-stu-id="c6e85-176">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="c6e85-177">Zagrożonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="c6e85-177">Users at Risk</span></span>
- <span data-ttu-id="c6e85-178">Ryzykowne logowania</span><span class="sxs-lookup"><span data-stu-id="c6e85-178">Risky Sign-ins</span></span>

<span data-ttu-id="c6e85-179">![Raporty dotyczące zabezpieczeń](./media/active-directory-reporting-migration/04.png "raporty dotyczące zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="c6e85-179">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="c6e85-180">Aby uzyskać więcej informacji o raportach zabezpieczeń zobacz:</span><span class="sxs-lookup"><span data-stu-id="c6e85-180">For more information about security reports, see:</span></span>

- [<span data-ttu-id="c6e85-181">Użytkownicy ryzyka raport zabezpieczeń w portalu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6e85-181">Users at Risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="c6e85-182">Ryzykowne raportu logowania w portalu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6e85-182">Risky Sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a><span data-ttu-id="c6e85-183">Raporty dotyczące działań w klasycznym portalu Azure, a portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6e85-183">Activity reports in the Azure classic portal vs. the Azure portal</span></span>

<span data-ttu-id="c6e85-184">W tej sekcji tabela zawiera listę istniejących raportów w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e85-184">The table in this section lists existing reports in the Azure classic portal.</span></span> <span data-ttu-id="c6e85-185">Opisuje również, jak te same informacje można uzyskać w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6e85-185">It also describes how you can get the same information in the Azure portal.</span></span>

<span data-ttu-id="c6e85-186">Aby wyświetlić wszystkich danych inspekcji, na **usługi Azure Active Directory** bloku, w obszarze **działania**, przejdź do **dzienniki inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-186">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span></span>

<span data-ttu-id="c6e85-187">![Dzienniki inspekcji](./media/active-directory-reporting-migration/61.png "Dzienniki inspekcji")</span><span class="sxs-lookup"><span data-stu-id="c6e85-187">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="c6e85-188">klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="c6e85-188">Azure classic portal</span></span>                 | <span data-ttu-id="c6e85-189">Aby znaleźć w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6e85-189">To find in the Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="c6e85-190">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="c6e85-190">Audit logs</span></span>                           | <span data-ttu-id="c6e85-191">Dla **kategorii działań**, wybierz pozycję **katalogu Core**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-191">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="c6e85-192">Działania związane z resetowaniem haseł</span><span class="sxs-lookup"><span data-stu-id="c6e85-192">Password reset activity</span></span>              | <span data-ttu-id="c6e85-193">Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-193">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="c6e85-194">Aktywność rejestracji resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="c6e85-194">Password reset registration activity</span></span> | <span data-ttu-id="c6e85-195">Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-195">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="c6e85-196">Raport aktywności grup samoobsługi</span><span class="sxs-lookup"><span data-stu-id="c6e85-196">Self-service groups activity</span></span>         | <span data-ttu-id="c6e85-197">Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie grupami**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-197">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="c6e85-198">Działanie aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="c6e85-198">Account provisioning activity</span></span>        | <span data-ttu-id="c6e85-199">Aby uzyskać **kategorii działań**, wybierz pozycję **Inicjowanie obsługi konta użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-199">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="c6e85-200">Stan przerzucania hasła</span><span class="sxs-lookup"><span data-stu-id="c6e85-200">Password rollover status</span></span>             | <span data-ttu-id="c6e85-201">Aby uzyskać **kategorii działań**, wybierz pozycję **automatycznego przerzucania hasła aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-201">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="c6e85-202">Błędy aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="c6e85-202">Account provisioning errors</span></span>          | <span data-ttu-id="c6e85-203">Aby uzyskać **kategorii działań**, wybierz pozycję **Inicjowanie obsługi konta użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-203">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="c6e85-204">Zmiany nazwy grupy usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="c6e85-204">Office365 Group Name Changes</span></span>         | <span data-ttu-id="c6e85-205">Aby uzyskać **kategorii działań**, wybierz pozycję **Samoobsługowe zarządzanie hasłami**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-205">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="c6e85-206">Dla **typu zasobu działania**, wybierz pozycję **grupy**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-206">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="c6e85-207">Aby uzyskać **źródło działania**, wybierz pozycję **grup usługi Office 365**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-207">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="c6e85-208">Aby wyświetlić **użycia aplikacji** raportu na **usługi Azure Active Directory** bloku, w obszarze **ZARZĄDZAJ**, wybierz pozycję **aplikacje dla przedsiębiorstw**, a następnie wybierz **logowania**.</span><span class="sxs-lookup"><span data-stu-id="c6e85-208">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="c6e85-209">![Raport logowania aplikacji przedsiębiorstwa](./media/active-directory-reporting-migration/199.png "raport logowania aplikacji przedsiębiorstwa")</span><span class="sxs-lookup"><span data-stu-id="c6e85-209">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6e85-210">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6e85-210">Next steps</span></span>

<span data-ttu-id="c6e85-211">Omówienie funkcji raportowania można znaleźć w temacie [Raporty w usłudze Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c6e85-211">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
