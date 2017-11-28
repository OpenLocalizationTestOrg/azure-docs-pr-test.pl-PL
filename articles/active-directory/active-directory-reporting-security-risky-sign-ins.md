---
title: "Raport dotyczący ryzykownych logowań w portalu usługi Azure Active Directory | Microsoft Docs"
description: "Dowiedz się więcej o raporcie dotyczącym ryzykownych logowań w portalu usługi Azure Active Directory"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 45a6f63bd920c9a70c25b8dfae084ea030256cf4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="risky-sign-ins-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="02cee-103">Raport dotyczący ryzykownych logowań w portalu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02cee-103">Risky sign-ins report in the Azure Active Directory portal</span></span>

<span data-ttu-id="02cee-104">Dzięki raportom o zabezpieczeniach w usłudze Azure Active Directory (Azure AD) możesz uzyskać wgląd w prawdopodobieństwo naruszenia bezpieczeństwa kont użytkowników w środowisku.</span><span class="sxs-lookup"><span data-stu-id="02cee-104">With the security reports in Azure Active Directory (Azure AD) you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="02cee-105">Usługa Azure AD wykrywa podejrzane akcje powiązane z kontami użytkowników.</span><span class="sxs-lookup"><span data-stu-id="02cee-105">Azure AD detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="02cee-106">Dla każdej wykrytej akcji jest tworzony wpis nazywany *zdarzeniem o podwyższonym ryzyku*.</span><span class="sxs-lookup"><span data-stu-id="02cee-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="02cee-107">Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="02cee-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="02cee-108">Za pomocą wykrytych zdarzeń o podwyższonym ryzyku obliczane są:</span><span class="sxs-lookup"><span data-stu-id="02cee-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="02cee-109">**Ryzykowne logowania** — ryzykowne logowanie jest wskaźnikiem próby logowania, które mogło zostać wykonane przez osobę, która nie jest prawowitym właścicielem konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02cee-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="02cee-110">Aby uzyskać więcej informacji, zobacz [Ryzykowne logowania](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="02cee-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="02cee-111">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="02cee-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="02cee-112">Aby uzyskać więcej informacji, zobacz [Użytkownicy oflagowani w związku z ryzykiem](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="02cee-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="02cee-113">W witrynie [Azure Portal](https://portal.azure.com) raporty dotyczące zabezpieczeń można znaleźć w bloku **Azure Active Directory** w sekcji **Zabezpieczenia**.</span><span class="sxs-lookup"><span data-stu-id="02cee-113">In [the Azure portal](https://portal.azure.com), you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span> 

![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="02cee-115">Jaka licencja usługi Azure AD jest wymagana w celu uzyskania dostępu do raportu zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="02cee-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="02cee-116">Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów ryzykownych logowań.</span><span class="sxs-lookup"><span data-stu-id="02cee-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="02cee-117">Jednak poziom szczegółowości raportu zależy od wersji:</span><span class="sxs-lookup"><span data-stu-id="02cee-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="02cee-118">W **usłudze Azure Active Directory w wersji Bezpłatna i Podstawowa** masz już dostęp do listy ryzykownych logowań.</span><span class="sxs-lookup"><span data-stu-id="02cee-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="02cee-119">Wersja **Azure Active Directory Premium 1** rozszerza ten model, umożliwiając również badanie niektórych podstawowych zdarzeń związanych z ryzykiem, które uwzględniono w poszczególnych raportach.</span><span class="sxs-lookup"><span data-stu-id="02cee-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="02cee-120">Wersja **Azure Active Directory Premium 2** oferuje najbardziej szczegółowe informacje na temat wszystkich zdarzeń o podwyższonym ryzyku i umożliwia konfigurowanie zasad zabezpieczeń, które automatycznie reagują na wystąpienie skonfigurowanych poziomów ryzyka.</span><span class="sxs-lookup"><span data-stu-id="02cee-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="02cee-121">Azure Active Directory — wersja Bezpłatna i Podstawowa</span><span class="sxs-lookup"><span data-stu-id="02cee-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="02cee-122">Usługa Azure Active Directory w wersji Bezpłatna i Podstawowa zapewnia listę wykrytych ryzykownych logowań dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="02cee-122">The Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="02cee-123">W tym raporcie znajdują się następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="02cee-123">This report lists:</span></span>

- <span data-ttu-id="02cee-124">**Użytkownik** — nazwa użytkownika użyta podczas logowania</span><span class="sxs-lookup"><span data-stu-id="02cee-124">**User** - The name of the user that was used during the sign-in operation</span></span>
- <span data-ttu-id="02cee-125">**IP** — adres IP urządzenia, którego użyto do nawiązania połączenia z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02cee-125">**IP** - The IP address of the device that was used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="02cee-126">**Lokalizacja** — lokalizacja, z której nawiązano połączenie z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02cee-126">**Location** - The location used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="02cee-127">**Godzina logowania** — godzina, o której przeprowadzono logowanie</span><span class="sxs-lookup"><span data-stu-id="02cee-127">**Sign-in time** - The time when the sign-in was performed</span></span>
- <span data-ttu-id="02cee-128">**Stan** — stan logowania</span><span class="sxs-lookup"><span data-stu-id="02cee-128">**Status** - The status of the sign-in</span></span>


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="02cee-130">Na podstawie badania ryzykownego logowania możesz przekazać usłudze Azure Active Directory swoją reakcję w postaci następujących akcji:</span><span class="sxs-lookup"><span data-stu-id="02cee-130">Based on your investigation of the risky sign-in, you can provide feedback to Azure Active Directory in form of the following actions:</span></span>

- <span data-ttu-id="02cee-131">Rozwiąż</span><span class="sxs-lookup"><span data-stu-id="02cee-131">Resolve</span></span>
- <span data-ttu-id="02cee-132">Oznacz jako wynik fałszywie dodatni</span><span class="sxs-lookup"><span data-stu-id="02cee-132">Mark as false positive</span></span>
- <span data-ttu-id="02cee-133">Zignoruj</span><span class="sxs-lookup"><span data-stu-id="02cee-133">Ignore</span></span>
- <span data-ttu-id="02cee-134">Uaktywnij ponownie</span><span class="sxs-lookup"><span data-stu-id="02cee-134">Reactivate</span></span>

![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="02cee-136">Aby uzyskać więcej informacji, zobacz [Ręczne zamykanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="02cee-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="02cee-137">Ten raport oferuje opcję:</span><span class="sxs-lookup"><span data-stu-id="02cee-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="02cee-138">Wyszukiwania zasobów</span><span class="sxs-lookup"><span data-stu-id="02cee-138">Searh resources</span></span>
- <span data-ttu-id="02cee-139">Pobierania danych raportu</span><span class="sxs-lookup"><span data-stu-id="02cee-139">Download the report data</span></span>


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="02cee-141">Azure Active Directory — wersje Premium</span><span class="sxs-lookup"><span data-stu-id="02cee-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="02cee-142">Raport dotyczący ryzykownych logowań w usłudze Azure Active Directory w wersjach Premium zawiera następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="02cee-142">The risky sign-ins report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="02cee-143">Zagregowane informacje o wykrytych [typach zdarzeń o podwyższonym ryzyku](active-directory-identity-protection-risk-events.md)</span><span class="sxs-lookup"><span data-stu-id="02cee-143">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="02cee-144">Opcja pobrania raportu</span><span class="sxs-lookup"><span data-stu-id="02cee-144">An option to download the report</span></span>


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="02cee-146">Po wybraniu zdarzenia o podwyższonym ryzyku jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="02cee-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="02cee-147">Skonfigurowanie [zasad podejmowania działań naprawczych dotyczących ryzyka związanego z użytkownikiem](active-directory-identityprotection.md#user-risk-security-policy).</span><span class="sxs-lookup"><span data-stu-id="02cee-147">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="02cee-148">Przeglądanie i wykrywanie osi czasu dla zdarzenia o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="02cee-148">Review the detection timeline for the risk event</span></span>  

- <span data-ttu-id="02cee-149">Przeglądanie listy użytkowników, dla których wykryto konkretne zdarzenie o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="02cee-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="02cee-150">[Ręczne zamykanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually) lub ponowne aktywowanie ręcznie zamkniętych zdarzeń o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="02cee-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="02cee-152">Po wybraniu użytkownika jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="02cee-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="02cee-153">Otwieranie widoku wszystkich logowań.</span><span class="sxs-lookup"><span data-stu-id="02cee-153">Open the All sign-ins view</span></span>

- <span data-ttu-id="02cee-154">Resetowanie hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02cee-154">Reset the user's password</span></span>

- <span data-ttu-id="02cee-155">Odrzucanie wszystkich zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="02cee-155">Dismiss all events</span></span>

- <span data-ttu-id="02cee-156">Badanie zgłoszonych zdarzeń o podwyższonym ryzyku dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02cee-156">Investigate reported risk events for the user.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="02cee-158">Aby zbadać zdarzenie o podwyższonym ryzyku, wybierz je z listy.</span><span class="sxs-lookup"><span data-stu-id="02cee-158">To investigate a risk event, select one from the list.</span></span>  
<span data-ttu-id="02cee-159">Spowoduje to otwarcie bloku **Szczegóły** dla tego zdarzenia o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="02cee-159">This opens the **Details** blade for this risk event.</span></span> <span data-ttu-id="02cee-160">W bloku **Szczegóły** jest opcja [ręcznego zamknięcia zdarzenia o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually) lub ponownego aktywowania ręcznie zamkniętego zdarzenia o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="02cee-160">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="02cee-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02cee-162">Next steps</span></span>

- <span data-ttu-id="02cee-163">Aby uzyskać więcej informacji na temat ochrony tożsamości w usłudze Azure Active Directory, zobacz [Ochrona tożsamości w usłudze Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="02cee-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

