---
title: "Usługa Azure Active Directory raportowania opóźnienia | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o ilość czasu, jaki zajmuje zdarzeń do raportowania w portalu usługi Azure"
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
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="937d1-103">Usługa Azure Active Directory opóźnienia raportowania</span><span class="sxs-lookup"><span data-stu-id="937d1-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="937d1-104">Z [raportowania](active-directory-preview-explainer.md) w usłudze Azure Active Directory, możesz uzyskać wszystkie informacje, należy określić, jak robi środowiska.</span><span class="sxs-lookup"><span data-stu-id="937d1-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="937d1-105">Ilość czasu, jaki zajmuje dane raportowania były wyświetlane w portalu Azure jest nazywana opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="937d1-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="937d1-106">Ten temat zawiera informacje opóźnienia raportowania wszystkie kategorie w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="937d1-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="937d1-107">Raporty dotyczące działań</span><span class="sxs-lookup"><span data-stu-id="937d1-107">Activity reports</span></span>

<span data-ttu-id="937d1-108">Istnieją dwa obszary działania raportowania:</span><span class="sxs-lookup"><span data-stu-id="937d1-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="937d1-109">**Działania związane z logowaniem** — informacje na temat użycia zarządzanych aplikacji i działania użytkownika związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="937d1-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="937d1-110">**Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu</span><span class="sxs-lookup"><span data-stu-id="937d1-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="937d1-111">Poniższa tabela zawiera informacje opóźnienia raporty aktywności.</span><span class="sxs-lookup"><span data-stu-id="937d1-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="937d1-112">Raport</span><span class="sxs-lookup"><span data-stu-id="937d1-112">Report</span></span> | <span data-ttu-id="937d1-113">Minimalne</span><span class="sxs-lookup"><span data-stu-id="937d1-113">Minimum</span></span> | <span data-ttu-id="937d1-114">Średnia</span><span class="sxs-lookup"><span data-stu-id="937d1-114">Average</span></span> | <span data-ttu-id="937d1-115">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="937d1-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="937d1-116">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="937d1-116">Audit logs</span></span>             | <span data-ttu-id="937d1-117">30 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-117">30 minutes</span></span>  | <span data-ttu-id="937d1-118">45 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-118">45 Minutes</span></span> | <span data-ttu-id="937d1-119">1 godzina</span><span class="sxs-lookup"><span data-stu-id="937d1-119">1 hour</span></span>     |
| <span data-ttu-id="937d1-120">Logowania</span><span class="sxs-lookup"><span data-stu-id="937d1-120">Sign-ins</span></span>               | <span data-ttu-id="937d1-121">15 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-121">15 minutes</span></span>  | <span data-ttu-id="937d1-122">15 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-122">15 minutes</span></span> | <span data-ttu-id="937d1-123">2 godziny *</span><span class="sxs-lookup"><span data-stu-id="937d1-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="937d1-124">W przypadku niektórych danych operacji logowania pochodzących ze starszych wersji aplikacji pakietu Office dane raportowania mogą pojawić się po 8 godzinach.</span><span class="sxs-lookup"><span data-stu-id="937d1-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="937d1-125">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="937d1-125">Security reports</span></span>

<span data-ttu-id="937d1-126">Istnieją dwa obszary raportowania zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="937d1-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="937d1-127">**Ryzykowne logowania** — ryzykowne logowanie jest wskaźnikiem próby logowania, które mogło zostać wykonane przez osobę, która nie jest prawowitym właścicielem konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="937d1-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="937d1-128">**Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.</span><span class="sxs-lookup"><span data-stu-id="937d1-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="937d1-129">Poniższa tabela zawiera informacje opóźnienia raporty dotyczące zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="937d1-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="937d1-130">Raport</span><span class="sxs-lookup"><span data-stu-id="937d1-130">Report</span></span> | <span data-ttu-id="937d1-131">Minimalne</span><span class="sxs-lookup"><span data-stu-id="937d1-131">Minimum</span></span> | <span data-ttu-id="937d1-132">Średnia</span><span class="sxs-lookup"><span data-stu-id="937d1-132">Average</span></span> | <span data-ttu-id="937d1-133">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="937d1-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="937d1-134">Narażeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="937d1-134">Users at risk</span></span>          | <span data-ttu-id="937d1-135">5 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-135">5 minutes</span></span>   | <span data-ttu-id="937d1-136">15 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-136">15 minutes</span></span>  | <span data-ttu-id="937d1-137">2 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-137">2 hours</span></span>  |
| <span data-ttu-id="937d1-138">Ryzykowne logowania</span><span class="sxs-lookup"><span data-stu-id="937d1-138">Risky sign-ins</span></span>         | <span data-ttu-id="937d1-139">5 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-139">5 minutes</span></span>   | <span data-ttu-id="937d1-140">15 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-140">15 minutes</span></span>  | <span data-ttu-id="937d1-141">2 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="937d1-142">Zdarzenia ryzyka</span><span class="sxs-lookup"><span data-stu-id="937d1-142">Risk events</span></span>

<span data-ttu-id="937d1-143">Usługi Azure Active Directory korzysta z algorytmów uczenia maszynowego adaptacyjną i heurystyki do wykrycia podejrzanych działań, które są związane z kontami użytkowników.</span><span class="sxs-lookup"><span data-stu-id="937d1-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="937d1-144">Każdy wykryty podejrzane działania są przechowywane w zdarzenia o nazwie ryzyko rekordu.</span><span class="sxs-lookup"><span data-stu-id="937d1-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="937d1-145">W poniższej tabeli wymieniono informacje opóźnienie dla zdarzeń o podwyższonym ryzyku.</span><span class="sxs-lookup"><span data-stu-id="937d1-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="937d1-146">Raport</span><span class="sxs-lookup"><span data-stu-id="937d1-146">Report</span></span> | <span data-ttu-id="937d1-147">Minimalne</span><span class="sxs-lookup"><span data-stu-id="937d1-147">Minimum</span></span> | <span data-ttu-id="937d1-148">Średnia</span><span class="sxs-lookup"><span data-stu-id="937d1-148">Average</span></span> | <span data-ttu-id="937d1-149">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="937d1-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="937d1-150">Logowania z anonimowych adresów IP</span><span class="sxs-lookup"><span data-stu-id="937d1-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="937d1-151">5 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-151">5 minutes</span></span> |<span data-ttu-id="937d1-152">15 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-152">15 Minutes</span></span> |<span data-ttu-id="937d1-153">2 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-153">2 hours</span></span> |
| <span data-ttu-id="937d1-154">Logowania z nieznanych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="937d1-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="937d1-155">5 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-155">5 minutes</span></span> |<span data-ttu-id="937d1-156">15 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-156">15 Minutes</span></span> |<span data-ttu-id="937d1-157">2 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-157">2 hours</span></span> |
| <span data-ttu-id="937d1-158">Użytkownicy z ujawnionymi poświadczeniami</span><span class="sxs-lookup"><span data-stu-id="937d1-158">Users with leaked credentials</span></span> |<span data-ttu-id="937d1-159">2 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-159">2 hours</span></span> |<span data-ttu-id="937d1-160">4 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-160">4 hours</span></span> |<span data-ttu-id="937d1-161">8 godzin</span><span class="sxs-lookup"><span data-stu-id="937d1-161">8 hours</span></span> |
| <span data-ttu-id="937d1-162">Niemożliwa podróż do nietypowych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="937d1-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="937d1-163">5 minut</span><span class="sxs-lookup"><span data-stu-id="937d1-163">5 minutes</span></span> |<span data-ttu-id="937d1-164">1 godzina</span><span class="sxs-lookup"><span data-stu-id="937d1-164">1 hour</span></span> |<span data-ttu-id="937d1-165">8 godzin</span><span class="sxs-lookup"><span data-stu-id="937d1-165">8 hours</span></span>  |
| <span data-ttu-id="937d1-166">Logowania z zainfekowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="937d1-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="937d1-167">2 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-167">2 hours</span></span> |<span data-ttu-id="937d1-168">4 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-168">4 hours</span></span> |<span data-ttu-id="937d1-169">8 godzin</span><span class="sxs-lookup"><span data-stu-id="937d1-169">8 hours</span></span>  |
| <span data-ttu-id="937d1-170">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="937d1-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="937d1-171">2 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-171">2 hours</span></span> |<span data-ttu-id="937d1-172">4 godziny</span><span class="sxs-lookup"><span data-stu-id="937d1-172">4 hours</span></span> |<span data-ttu-id="937d1-173">8 godzin</span><span class="sxs-lookup"><span data-stu-id="937d1-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="937d1-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="937d1-174">Next steps</span></span>

<span data-ttu-id="937d1-175">Jeśli chcesz dowiedzieć się więcej na temat raportów działania w portalu Azure, zobacz:</span><span class="sxs-lookup"><span data-stu-id="937d1-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="937d1-176">Działania logowania raportów w portalu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="937d1-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="937d1-177">Raporty dotyczące działania inspekcji w portalu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="937d1-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="937d1-178">Jeśli chcesz dowiedzieć się więcej o raporty dotyczące zabezpieczeń w portalu Azure, zobacz:</span><span class="sxs-lookup"><span data-stu-id="937d1-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="937d1-179">Użytkownicy ryzyka raport zabezpieczeń w portalu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="937d1-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="937d1-180">Raport ryzykowne logowania w portalu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="937d1-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="937d1-181">Jeśli chcesz dowiedzieć się więcej na temat zdarzeń o podwyższonym ryzyku, zobacz [zdarzenia o podwyższonym ryzyku usługi Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="937d1-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
