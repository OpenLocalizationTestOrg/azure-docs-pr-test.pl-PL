---
title: "Raport o zabezpieczeniach dotyczący użytkowników oflagowanych w związku z ryzykiem w portalu usługi Azure Active Directory | Microsoft Docs"
description: "Dowiedz się więcej o raporcie o zabezpieczeniach dotyczącym użytkowników oflagowanych w związku z ryzykiem w portalu usługi Azure Active Directory"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 04f15384a7cd0fa03300acdf159d371569ecf9fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="users-flagged-for-risk-security-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="142b4-103">Raport o zabezpieczeniach dotyczący użytkowników oflagowanych w związku z ryzykiem w portalu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="142b4-103">Users flagged for risk security report in the Azure Active Directory portal</span></span>

<span data-ttu-id="142b4-104">Dzięki raportom o zabezpieczeniach w usłudze Azure Active Directory (Azure AD) możesz uzyskać wgląd w prawdopodobieństwo naruszenia bezpieczeństwa kont użytkowników w środowisku.</span><span class="sxs-lookup"><span data-stu-id="142b4-104">With the security reports in the Azure Active Directory (Azure AD), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="142b4-105">Usługa Azure Active Directory wykrywa podejrzane akcje powiązane z kontami użytkowników.</span><span class="sxs-lookup"><span data-stu-id="142b4-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="142b4-106">Dla każdej wykrytej akcji jest tworzony wpis nazywany *zdarzeniem o podwyższonym ryzyku*.</span><span class="sxs-lookup"><span data-stu-id="142b4-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="142b4-107">Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="142b4-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="142b4-108">Za pomocą wykrytych zdarzeń o podwyższonym ryzyku obliczane są:</span><span class="sxs-lookup"><span data-stu-id="142b4-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="142b4-109">**Ryzykowne logowania** — ryzykowne logowanie jest wskaźnikiem próby logowania, które mogło zostać wykonane przez osobę, która nie jest prawowitym właścicielem konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="142b4-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="142b4-110">Aby uzyskać więcej informacji, zobacz [Ryzykowne logowania](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="142b4-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="142b4-111">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="142b4-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="142b4-112">Aby uzyskać więcej informacji, zobacz [Użytkownicy oflagowani w związku z ryzykiem](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="142b4-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="142b4-113">W witrynie Azure Portal raporty dotyczące zabezpieczeń można znaleźć w bloku **Azure Active Directory** w sekcji **Zabezpieczenia**.</span><span class="sxs-lookup"><span data-stu-id="142b4-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span>  

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="142b4-115">Jaka licencja usługi Azure AD jest wymagana w celu uzyskania dostępu do raportu zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="142b4-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="142b4-116">Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów użytkowników oflagowanych w związku z ryzykiem.</span><span class="sxs-lookup"><span data-stu-id="142b4-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="142b4-117">Jednak poziom szczegółowości raportu zależy od wersji:</span><span class="sxs-lookup"><span data-stu-id="142b4-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="142b4-118">W **usłudze Azure Active Directory w wersji Bezpłatna i Podstawowa** masz już dostęp do listy użytkowników oflagowanych w związku z ryzykiem.</span><span class="sxs-lookup"><span data-stu-id="142b4-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="142b4-119">Wersja **Azure Active Directory Premium 1** rozszerza ten model, umożliwiając również badanie niektórych podstawowych zdarzeń związanych z ryzykiem, które uwzględniono w poszczególnych raportach.</span><span class="sxs-lookup"><span data-stu-id="142b4-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="142b4-120">Wersja **Azure Active Directory Premium 2** oferuje najbardziej szczegółowe informacje na temat wszystkich zdarzeń o podwyższonym ryzyku i umożliwia konfigurowanie zasad zabezpieczeń, które automatycznie reagują na wystąpienie skonfigurowanych poziomów ryzyka.</span><span class="sxs-lookup"><span data-stu-id="142b4-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="142b4-121">Azure Active Directory — wersja Bezpłatna i Podstawowa</span><span class="sxs-lookup"><span data-stu-id="142b4-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="142b4-122">Raport dotyczący użytkowników oflagowanych w związku z ryzykiem w usłudze Azure Active Directory w wersji Bezpłatna i Podstawowa zapewnia listę kont użytkowników, których bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="142b4-122">The users flagged for risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="142b4-124">Wybranie użytkownika powoduje otwarcie bloku z danymi tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="142b4-124">Selecting a user opens the related user data blade.</span></span>
<span data-ttu-id="142b4-125">W przypadku narażonego użytkownika można przejrzeć jego historię logowania i w razie potrzeby zresetować hasło.</span><span class="sxs-lookup"><span data-stu-id="142b4-125">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span></span>

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="142b4-127">To okno dialogowe oferuje opcję:</span><span class="sxs-lookup"><span data-stu-id="142b4-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="142b4-128">Pobierania raportu</span><span class="sxs-lookup"><span data-stu-id="142b4-128">Download the report</span></span>

- <span data-ttu-id="142b4-129">Wyszukiwania użytkowników</span><span class="sxs-lookup"><span data-stu-id="142b4-129">Search users</span></span>

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="142b4-131">Azure Active Directory — wersje Premium</span><span class="sxs-lookup"><span data-stu-id="142b4-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="142b4-132">Raport dotyczący użytkowników oflagowanych w związku z ryzykiem w usłudze Azure Active Directory w wersjach Premium zawiera następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="142b4-132">The users flagged for risk report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="142b4-133">[Lista kont użytkowników](active-directory-identityprotection.md#users-flagged-for-risk), których bezpieczeństwo mogło zostać naruszone</span><span class="sxs-lookup"><span data-stu-id="142b4-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="142b4-134">Zagregowane informacje o wykrytych [typach zdarzeń o podwyższonym ryzyku](active-directory-identity-protection-risk-events.md)</span><span class="sxs-lookup"><span data-stu-id="142b4-134">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="142b4-135">Opcja pobrania raportu</span><span class="sxs-lookup"><span data-stu-id="142b4-135">An option to download the report</span></span>

- <span data-ttu-id="142b4-136">Opcja skonfigurowania [zasad podejmowania działań naprawczych dotyczących ryzyka związanego z użytkownikiem](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="142b4-136">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="142b4-138">Po wybraniu użytkownika jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="142b4-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="142b4-139">Otwieranie widoku wszystkich logowań.</span><span class="sxs-lookup"><span data-stu-id="142b4-139">Open the All sign-ins view</span></span>

- <span data-ttu-id="142b4-140">Resetowanie hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="142b4-140">Reset the user's password</span></span>

- <span data-ttu-id="142b4-141">Odrzucanie wszystkich zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="142b4-141">Dismiss all events</span></span>

- <span data-ttu-id="142b4-142">Badanie zgłoszonych zdarzeń o podwyższonym ryzyku dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="142b4-142">Investigate reported risk events for the user.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="142b4-144">Aby zbadać zdarzenia o podwyższonym ryzyku, wybierz zdarzenie z listy w celu otwarcia bloku **Szczegóły** dla tego zdarzenia o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="142b4-144">To investigate a risk event, select one from the list to open the **Details** blade for this risk event.</span></span> <span data-ttu-id="142b4-145">W bloku **Szczegóły** jest opcja [ręcznego zamknięcia zdarzenia o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually) lub ponownego aktywowania ręcznie zamkniętego zdarzenia o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="142b4-145">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="142b4-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="142b4-147">Next steps</span></span>

- <span data-ttu-id="142b4-148">Aby uzyskać więcej informacji na temat ochrony tożsamości w usłudze Azure Active Directory, zobacz [Ochrona tożsamości w usłudze Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="142b4-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

