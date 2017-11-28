---
title: "opóźnienia raportowania usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello ilość czasu, jaki zajmuje raporty tooshow zdarzenia w portalu Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="b7c1d-103">Usługa Azure Active Directory opóźnienia raportowania</span><span class="sxs-lookup"><span data-stu-id="b7c1d-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="b7c1d-104">Z [raportowania](active-directory-preview-explainer.md) w hello Azure Active Directory, możesz uzyskać wszystkie informacje hello należy toodetermine jak robi środowiska.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="b7c1d-105">Hello ilość czasu, jaki zajmuje raportowania danych tooshow się w portalu Azure hello jest także znana jako czas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="b7c1d-106">Ten temat zawiera informacje opóźnienia hello hello wszystkie kategorie raportowania hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="b7c1d-107">Raporty dotyczące działań</span><span class="sxs-lookup"><span data-stu-id="b7c1d-107">Activity reports</span></span>

<span data-ttu-id="b7c1d-108">Istnieją dwa obszary działania raportowania:</span><span class="sxs-lookup"><span data-stu-id="b7c1d-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="b7c1d-109">**Działania logowania** — informacje na temat użycia hello zarządzanych aplikacji i aktywności logowania użytkowników</span><span class="sxs-lookup"><span data-stu-id="b7c1d-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="b7c1d-110">**Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu</span><span class="sxs-lookup"><span data-stu-id="b7c1d-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="b7c1d-111">w poniższej tabeli Hello zawiera informacje opóźnienia hello raporty aktywności.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="b7c1d-112">Raport</span><span class="sxs-lookup"><span data-stu-id="b7c1d-112">Report</span></span> | <span data-ttu-id="b7c1d-113">Minimalne</span><span class="sxs-lookup"><span data-stu-id="b7c1d-113">Minimum</span></span> | <span data-ttu-id="b7c1d-114">Średnia</span><span class="sxs-lookup"><span data-stu-id="b7c1d-114">Average</span></span> | <span data-ttu-id="b7c1d-115">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="b7c1d-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b7c1d-116">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="b7c1d-116">Audit logs</span></span>             | <span data-ttu-id="b7c1d-117">30 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-117">30 minutes</span></span>  | <span data-ttu-id="b7c1d-118">45 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-118">45 Minutes</span></span> | <span data-ttu-id="b7c1d-119">1 godzina</span><span class="sxs-lookup"><span data-stu-id="b7c1d-119">1 hour</span></span>     |
| <span data-ttu-id="b7c1d-120">Logowania</span><span class="sxs-lookup"><span data-stu-id="b7c1d-120">Sign-ins</span></span>               | <span data-ttu-id="b7c1d-121">15 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-121">15 minutes</span></span>  | <span data-ttu-id="b7c1d-122">15 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-122">15 minutes</span></span> | <span data-ttu-id="b7c1d-123">2 godziny *</span><span class="sxs-lookup"><span data-stu-id="b7c1d-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="b7c1d-124">W przypadku niektórych danych działania logowania pochodzące z aplikacji starszej wersji pakietu office może potrwać too8 godzin hello raporty tooshow danych.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="b7c1d-125">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="b7c1d-125">Security reports</span></span>

<span data-ttu-id="b7c1d-126">Istnieją dwa obszary raportowania zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="b7c1d-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="b7c1d-127">**Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="b7c1d-128">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="b7c1d-129">Witaj w poniższej tabeli znajdują się informacje opóźnienia hello zabezpieczeń raportów.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="b7c1d-130">Raport</span><span class="sxs-lookup"><span data-stu-id="b7c1d-130">Report</span></span> | <span data-ttu-id="b7c1d-131">Minimalne</span><span class="sxs-lookup"><span data-stu-id="b7c1d-131">Minimum</span></span> | <span data-ttu-id="b7c1d-132">Średnia</span><span class="sxs-lookup"><span data-stu-id="b7c1d-132">Average</span></span> | <span data-ttu-id="b7c1d-133">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="b7c1d-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b7c1d-134">Narażeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="b7c1d-134">Users at risk</span></span>          | <span data-ttu-id="b7c1d-135">5 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-135">5 minutes</span></span>   | <span data-ttu-id="b7c1d-136">15 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-136">15 minutes</span></span>  | <span data-ttu-id="b7c1d-137">2 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-137">2 hours</span></span>  |
| <span data-ttu-id="b7c1d-138">Ryzykowne logowania</span><span class="sxs-lookup"><span data-stu-id="b7c1d-138">Risky sign-ins</span></span>         | <span data-ttu-id="b7c1d-139">5 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-139">5 minutes</span></span>   | <span data-ttu-id="b7c1d-140">15 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-140">15 minutes</span></span>  | <span data-ttu-id="b7c1d-141">2 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="b7c1d-142">Zdarzenia ryzyka</span><span class="sxs-lookup"><span data-stu-id="b7c1d-142">Risk events</span></span>

<span data-ttu-id="b7c1d-143">Usługa Azure Active Directory korzysta z adaptacyjną machine learning algorytmów i heurystyki toodetect podejrzane akcji, które są powiązane tooyour kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="b7c1d-144">Każdy wykryty podejrzane działania są przechowywane w zdarzenia o nazwie ryzyko rekordu.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="b7c1d-145">Witaj w poniższej tabeli znajdują się informacje opóźnienia hello dla zdarzeń o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="b7c1d-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="b7c1d-146">Raport</span><span class="sxs-lookup"><span data-stu-id="b7c1d-146">Report</span></span> | <span data-ttu-id="b7c1d-147">Minimalne</span><span class="sxs-lookup"><span data-stu-id="b7c1d-147">Minimum</span></span> | <span data-ttu-id="b7c1d-148">Średnia</span><span class="sxs-lookup"><span data-stu-id="b7c1d-148">Average</span></span> | <span data-ttu-id="b7c1d-149">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="b7c1d-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b7c1d-150">Logowania z anonimowych adresów IP</span><span class="sxs-lookup"><span data-stu-id="b7c1d-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="b7c1d-151">5 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-151">5 minutes</span></span> |<span data-ttu-id="b7c1d-152">15 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-152">15 Minutes</span></span> |<span data-ttu-id="b7c1d-153">2 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-153">2 hours</span></span> |
| <span data-ttu-id="b7c1d-154">Logowania z nieznanych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="b7c1d-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="b7c1d-155">5 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-155">5 minutes</span></span> |<span data-ttu-id="b7c1d-156">15 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-156">15 Minutes</span></span> |<span data-ttu-id="b7c1d-157">2 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-157">2 hours</span></span> |
| <span data-ttu-id="b7c1d-158">Użytkownicy z ujawnionymi poświadczeniami</span><span class="sxs-lookup"><span data-stu-id="b7c1d-158">Users with leaked credentials</span></span> |<span data-ttu-id="b7c1d-159">2 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-159">2 hours</span></span> |<span data-ttu-id="b7c1d-160">4 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-160">4 hours</span></span> |<span data-ttu-id="b7c1d-161">8 godzin</span><span class="sxs-lookup"><span data-stu-id="b7c1d-161">8 hours</span></span> |
| <span data-ttu-id="b7c1d-162">Niemożliwa podróż tooatypical lokalizacji</span><span class="sxs-lookup"><span data-stu-id="b7c1d-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="b7c1d-163">5 minut</span><span class="sxs-lookup"><span data-stu-id="b7c1d-163">5 minutes</span></span> |<span data-ttu-id="b7c1d-164">1 godzina</span><span class="sxs-lookup"><span data-stu-id="b7c1d-164">1 hour</span></span> |<span data-ttu-id="b7c1d-165">8 godzin</span><span class="sxs-lookup"><span data-stu-id="b7c1d-165">8 hours</span></span>  |
| <span data-ttu-id="b7c1d-166">Logowania z zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="b7c1d-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="b7c1d-167">2 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-167">2 hours</span></span> |<span data-ttu-id="b7c1d-168">4 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-168">4 hours</span></span> |<span data-ttu-id="b7c1d-169">8 godzin</span><span class="sxs-lookup"><span data-stu-id="b7c1d-169">8 hours</span></span>  |
| <span data-ttu-id="b7c1d-170">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="b7c1d-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="b7c1d-171">2 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-171">2 hours</span></span> |<span data-ttu-id="b7c1d-172">4 godziny</span><span class="sxs-lookup"><span data-stu-id="b7c1d-172">4 hours</span></span> |<span data-ttu-id="b7c1d-173">8 godzin</span><span class="sxs-lookup"><span data-stu-id="b7c1d-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="b7c1d-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7c1d-174">Next steps</span></span>

<span data-ttu-id="b7c1d-175">Jeśli chcesz tooknow więcej informacji na temat hello raporty aktywności w hello portalu Azure, zobacz:</span><span class="sxs-lookup"><span data-stu-id="b7c1d-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="b7c1d-176">Raporty aktywności logowania w portalu usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b7c1d-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="b7c1d-177">Raporty dotyczące działań w portalu usługi Azure Active Directory hello inspekcji</span><span class="sxs-lookup"><span data-stu-id="b7c1d-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="b7c1d-178">Więcej informacji na temat hello raporty dotyczące zabezpieczeń w portalu Azure hello tooknow, zobacz:</span><span class="sxs-lookup"><span data-stu-id="b7c1d-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="b7c1d-179">Użytkownicy ryzyka raport zabezpieczeń w portalu usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b7c1d-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="b7c1d-180">Raport ryzykowne logowania w portalu usługi Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b7c1d-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="b7c1d-181">Aby uzyskać więcej informacji na temat zdarzeń o podwyższonym ryzyku tooknow zobacz [zdarzenia o podwyższonym ryzyku usługi Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="b7c1d-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
