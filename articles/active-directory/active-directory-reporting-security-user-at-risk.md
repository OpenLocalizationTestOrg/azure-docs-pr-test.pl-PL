---
title: "aaaUsers oflagowane zagrożenia zabezpieczeń raportu w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat użytkowników hello oflagowane zagrożenia zabezpieczeń raportu w portalu usługi Azure Active Directory hello"
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
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="5cfee-103">Użytkownicy oflagowani zagrożenia zabezpieczeń raportu w portalu usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="5cfee-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="5cfee-104">Z raportami zabezpieczeń hello w hello Azure Active Directory (Azure AD) możesz uzyskać wgląd w prawdopodobieństwo hello kont użytkowników z naruszonymi zabezpieczeniami w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="5cfee-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="5cfee-105">Usługa Azure Active Directory wykryje podejrzanych działań, które są powiązane tooyour kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5cfee-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="5cfee-106">Dla każdej wykrytej akcji jest tworzony wpis nazywany *zdarzeniem o podwyższonym ryzyku*.</span><span class="sxs-lookup"><span data-stu-id="5cfee-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="5cfee-107">Aby uzyskać więcej informacji, zobacz [Zdarzenia o podwyższonym ryzyku w usłudze Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="5cfee-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="5cfee-108">Witaj wykrył, że zdarzenia o podwyższonym ryzyku są używane toocalculate:</span><span class="sxs-lookup"><span data-stu-id="5cfee-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="5cfee-109">**Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cfee-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="5cfee-110">Aby uzyskać więcej informacji, zobacz [Ryzykowne logowania](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="5cfee-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="5cfee-111">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="5cfee-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="5cfee-112">Aby uzyskać więcej informacji, zobacz [Użytkownicy oflagowani w związku z ryzykiem](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="5cfee-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="5cfee-113">W portalu Azure hello, można znaleźć zabezpieczeń hello raport dotyczący hello **usługi Azure Active Directory** bloku w hello **zabezpieczeń** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5cfee-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="5cfee-115">Jakie licencji usługi Azure AD potrzebujesz tooaccess raport zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="5cfee-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="5cfee-116">Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów użytkowników oflagowanych w związku z ryzykiem.</span><span class="sxs-lookup"><span data-stu-id="5cfee-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="5cfee-117">Jednak hello poziom szczegółowości raportu różni się między wersjami hello:</span><span class="sxs-lookup"><span data-stu-id="5cfee-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="5cfee-118">W hello **wersje usługi Azure Active Directory wolnego i Basic**, otrzymasz listę użytkowników z ustawioną flagą ryzyka.</span><span class="sxs-lookup"><span data-stu-id="5cfee-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="5cfee-119">Witaj **Azure Active Directory Premium 1** edition rozszerza tego modelu, należy również włączyć tooexamine niektóre hello podstawowy zdarzenia ryzyka, które zostały wykryte dla każdego raportu.</span><span class="sxs-lookup"><span data-stu-id="5cfee-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="5cfee-120">Hello **Azure Active Directory Premium 2** edition zapewnia hello bardziej szczegółowe informacje o wszystkich zdarzeniach ryzyka podstawowej i umożliwia tooconfigure zasady zabezpieczeń, które automatycznie odpowiadać tooconfigured ryzyka poziomy.</span><span class="sxs-lookup"><span data-stu-id="5cfee-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="5cfee-121">Azure Active Directory — wersja Bezpłatna i Podstawowa</span><span class="sxs-lookup"><span data-stu-id="5cfee-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="5cfee-122">Użytkownicy Hello oflagowane ryzyka raportu w wersji bezpłatnej i podstawowa usługi Azure Active Directory hello udostępnia listę kont użytkowników, które zostały naruszone.</span><span class="sxs-lookup"><span data-stu-id="5cfee-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="5cfee-124">Wybór użytkownika zostanie otwarty blok danych użytkownikowi hello.</span><span class="sxs-lookup"><span data-stu-id="5cfee-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="5cfee-125">Dla użytkowników, którzy są narażeni na ataki można sprawdzić hello użytkownika logowania historii i zresetuj hasło hello, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5cfee-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="5cfee-127">To okno dialogowe oferuje opcję:</span><span class="sxs-lookup"><span data-stu-id="5cfee-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="5cfee-128">Pobierz raport hello</span><span class="sxs-lookup"><span data-stu-id="5cfee-128">Download hello report</span></span>

- <span data-ttu-id="5cfee-129">Wyszukiwania użytkowników</span><span class="sxs-lookup"><span data-stu-id="5cfee-129">Search users</span></span>

![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="5cfee-131">Azure Active Directory — wersje Premium</span><span class="sxs-lookup"><span data-stu-id="5cfee-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="5cfee-132">Użytkownicy Hello oflagowane ryzyka raportu w wersji premium hello Azure Active Directory umożliwia:</span><span class="sxs-lookup"><span data-stu-id="5cfee-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="5cfee-133">[Lista kont użytkowników](active-directory-identityprotection.md#users-flagged-for-risk), których bezpieczeństwo mogło zostać naruszone</span><span class="sxs-lookup"><span data-stu-id="5cfee-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="5cfee-134">Zagregowane informacje o hello [ryzyka typów zdarzeń](active-directory-identity-protection-risk-events.md) zostały wykryte</span><span class="sxs-lookup"><span data-stu-id="5cfee-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="5cfee-135">Opcja toodownload hello raportu</span><span class="sxs-lookup"><span data-stu-id="5cfee-135">An option toodownload hello report</span></span>

- <span data-ttu-id="5cfee-136">Opcja tooconfigure [zasady korygowania ryzyka użytkownika](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="5cfee-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="5cfee-138">Po wybraniu użytkownika jest dla niego wyświetlany szczegółowy widok raportu, który umożliwia wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="5cfee-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="5cfee-139">Wyświetl wszystkie sesje logowania hello otwarte</span><span class="sxs-lookup"><span data-stu-id="5cfee-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="5cfee-140">Resetowanie hasła użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="5cfee-140">Reset hello user's password</span></span>

- <span data-ttu-id="5cfee-141">Odrzucanie wszystkich zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="5cfee-141">Dismiss all events</span></span>

- <span data-ttu-id="5cfee-142">Zbadaj zdarzenia zgłoszone ryzyka dla hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cfee-142">Investigate reported risk events for hello user.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="5cfee-144">tooinvestigate zdarzenia ryzyka, wybierz jeden z hello listy tooopen hello **szczegóły** bloku dla tego zdarzenia ryzyka.</span><span class="sxs-lookup"><span data-stu-id="5cfee-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="5cfee-145">Na powitania **szczegóły** bloku masz hello opcja tooeither [ręcznie zamknąć zdarzenie ryzyka](active-directory-identityprotection.md#closing-risk-events-manually) lub ponownym uaktywnieniem zdarzeń ryzyka ręcznie zamknięty.</span><span class="sxs-lookup"><span data-stu-id="5cfee-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Ryzykowne logowania](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="5cfee-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5cfee-147">Next steps</span></span>

- <span data-ttu-id="5cfee-148">Aby uzyskać więcej informacji na temat ochrony tożsamości w usłudze Azure Active Directory, zobacz [Ochrona tożsamości w usłudze Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="5cfee-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

