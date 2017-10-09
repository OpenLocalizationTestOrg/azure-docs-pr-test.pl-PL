---
title: "aaaRisky raport logowania w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello raportu ryzykowne logowania w portalu usługi Azure Active Directory hello"
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
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="a974d-103">Raport ryzykowne logowania w portalu usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="a974d-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="a974d-104">Z hello raporty dotyczące zabezpieczeń w usłudze Azure Active Directory (Azure AD) można uzyskać wgląd w prawdopodobieństwo hello kont użytkowników ze złamanymi zabezpieczeniami w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="a974d-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="a974d-105">Usługi Azure AD wykrycia podejrzanych działań, które są powiązane tooyour kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a974d-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="a974d-106">Dla każdej wykrytej akcji jest tworzony wpis nazywany *zdarzeniem o podwyższonym ryzyku*.</span><span class="sxs-lookup"><span data-stu-id="a974d-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="a974d-107">Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="a974d-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="a974d-108">Witaj wykrył, że zdarzenia o podwyższonym ryzyku są używane toocalculate:</span><span class="sxs-lookup"><span data-stu-id="a974d-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="a974d-109">**Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a974d-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="a974d-110">Aby uzyskać więcej informacji, zobacz [Ryzykowne logowania](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="a974d-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="a974d-111">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="a974d-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="a974d-112">Aby uzyskać więcej informacji, zobacz [Użytkownicy oflagowani w związku z ryzykiem](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="a974d-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="a974d-113">W [hello portalu Azure](https://portal.azure.com), można znaleźć zabezpieczeń hello raport dotyczący hello **usługi Azure Active Directory** bloku w hello **zabezpieczeń** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a974d-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="a974d-115">Jakie licencji usługi Azure AD potrzebujesz tooaccess raport zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="a974d-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="a974d-116">Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów ryzykownych logowań.</span><span class="sxs-lookup"><span data-stu-id="a974d-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="a974d-117">Jednak hello poziom szczegółowości raportu różni się między wersjami hello:</span><span class="sxs-lookup"><span data-stu-id="a974d-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="a974d-118">W hello **wersje usługi Azure Active Directory wolnego i Basic**, już uzyskać listę ryzykowne logowania.</span><span class="sxs-lookup"><span data-stu-id="a974d-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="a974d-119">Witaj **Azure Active Directory Premium 1** edition rozszerza tego modelu, należy również włączyć tooexamine niektóre hello podstawowy zdarzenia ryzyka, które zostały wykryte dla każdego raportu.</span><span class="sxs-lookup"><span data-stu-id="a974d-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="a974d-120">Witaj **Azure Active Directory Premium 2** edition udostępnia program hello najbardziej szczegółowe informacje o wszystkich zdarzeniach ryzyka podstawowej i pozwala także tooconfigure zasady zabezpieczeń, które automatycznie odpowiadać tooconfigured poziomów ryzyka.</span><span class="sxs-lookup"><span data-stu-id="a974d-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="a974d-121">Azure Active Directory — wersja Bezpłatna i Podstawowa</span><span class="sxs-lookup"><span data-stu-id="a974d-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="a974d-122">wersje podstawowe i Hello Azure Active Directory wolnego Podaj listę ryzykowne sesje logowania, które zostały wykryte dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a974d-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="a974d-123">W tym raporcie znajdują się następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="a974d-123">This report lists:</span></span>

- <span data-ttu-id="a974d-124">**Użytkownik** — Witaj nazwa hello użytkownika, który był używany podczas operacji logowania hello</span><span class="sxs-lookup"><span data-stu-id="a974d-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="a974d-125">**IP** — Witaj adres IP urządzenia hello, który był używany tooconnect tooAzure usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="a974d-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="a974d-126">**Lokalizacja** — lokalizacja hello używana tooAzure tooconnect usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="a974d-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="a974d-127">**Czas logowania** — czas hello podczas logowania hello została wykonana</span><span class="sxs-lookup"><span data-stu-id="a974d-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="a974d-128">**Stan** — Witaj stan logowania hello</span><span class="sxs-lookup"><span data-stu-id="a974d-128">**Status** - hello status of hello sign-in</span></span>


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="a974d-130">W oparciu o badaniu z hello ryzykowne logowania, można podać tooAzure opinii usługi Active Directory w postaci hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="a974d-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="a974d-131">Rozwiąż</span><span class="sxs-lookup"><span data-stu-id="a974d-131">Resolve</span></span>
- <span data-ttu-id="a974d-132">Oznacz jako wynik fałszywie dodatni</span><span class="sxs-lookup"><span data-stu-id="a974d-132">Mark as false positive</span></span>
- <span data-ttu-id="a974d-133">Zignoruj</span><span class="sxs-lookup"><span data-stu-id="a974d-133">Ignore</span></span>
- <span data-ttu-id="a974d-134">Uaktywnij ponownie</span><span class="sxs-lookup"><span data-stu-id="a974d-134">Reactivate</span></span>

![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="a974d-136">Aby uzyskać więcej informacji, zobacz [Ręczne zamykanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="a974d-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="a974d-137">Ten raport oferuje opcję:</span><span class="sxs-lookup"><span data-stu-id="a974d-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="a974d-138">Wyszukiwania zasobów</span><span class="sxs-lookup"><span data-stu-id="a974d-138">Searh resources</span></span>
- <span data-ttu-id="a974d-139">Pobierz dane raportu hello</span><span class="sxs-lookup"><span data-stu-id="a974d-139">Download hello report data</span></span>


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="a974d-141">Azure Active Directory — wersje Premium</span><span class="sxs-lookup"><span data-stu-id="a974d-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="a974d-142">Witaj ryzykowne logowania raportu w wersji premium hello Azure Active Directory umożliwia:</span><span class="sxs-lookup"><span data-stu-id="a974d-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="a974d-143">Zagregowane informacje o hello [ryzyka typów zdarzeń](active-directory-identity-protection-risk-events.md) zostały wykryte</span><span class="sxs-lookup"><span data-stu-id="a974d-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="a974d-144">Opcja toodownload hello raportu</span><span class="sxs-lookup"><span data-stu-id="a974d-144">An option toodownload hello report</span></span>


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="a974d-146">Po wybraniu zdarzenia o podwyższonym ryzyku jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a974d-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="a974d-147">Opcja tooconfigure [zasady korygowania ryzyka użytkownika](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="a974d-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="a974d-148">Przejrzyj oś czasu wykrywania hello hello ryzyka zdarzeń</span><span class="sxs-lookup"><span data-stu-id="a974d-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="a974d-149">Przeglądanie listy użytkowników, dla których wykryto konkretne zdarzenie o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="a974d-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="a974d-150">[Ręczne zamykanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection.md#closing-risk-events-manually) lub ponowne aktywowanie ręcznie zamkniętych zdarzeń o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="a974d-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="a974d-152">Po wybraniu użytkownika jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a974d-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="a974d-153">Wyświetl wszystkie sesje logowania hello otwarte</span><span class="sxs-lookup"><span data-stu-id="a974d-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="a974d-154">Resetowanie hasła użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="a974d-154">Reset hello user's password</span></span>

- <span data-ttu-id="a974d-155">Odrzucanie wszystkich zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="a974d-155">Dismiss all events</span></span>

- <span data-ttu-id="a974d-156">Zbadaj zdarzenia zgłoszone ryzyka dla hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a974d-156">Investigate reported risk events for hello user.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="a974d-158">tooinvestigate zdarzenia ryzyka, wybierz z listy hello.</span><span class="sxs-lookup"><span data-stu-id="a974d-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="a974d-159">Spowoduje to otwarcie hello **szczegóły** bloku dla tego zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="a974d-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="a974d-160">Na powitania **szczegóły** bloku masz hello opcja tooeither [ręcznie zamknąć zdarzenie ryzyka](active-directory-identityprotection.md#closing-risk-events-manually) lub ponownym uaktywnieniem zdarzeń ryzyka ręcznie zamknięty.</span><span class="sxs-lookup"><span data-stu-id="a974d-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="a974d-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a974d-162">Next steps</span></span>

- <span data-ttu-id="a974d-163">Aby uzyskać więcej informacji na temat ochrony tożsamości w usłudze Azure Active Directory, zobacz [Ochrona tożsamości w usłudze Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="a974d-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

