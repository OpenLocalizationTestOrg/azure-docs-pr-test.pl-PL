---
title: "Raportowanie usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Zawiera ogólne omówienie raportów usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="382d5-103">Raporty w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="382d5-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="382d5-104">Dzięki raportom usługi Azure Active Directory możesz uzyskać szczegółowe informacje na temat działania środowiska.</span><span class="sxs-lookup"><span data-stu-id="382d5-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="382d5-105">dane podane Hello umożliwia:</span><span class="sxs-lookup"><span data-stu-id="382d5-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="382d5-106">Określać, jak usługi i aplikacje są wykorzystywane przez użytkowników</span><span class="sxs-lookup"><span data-stu-id="382d5-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="382d5-107">Wykrywanie potencjalnych zagrożeń wpływających na powitania kondycji środowiska</span><span class="sxs-lookup"><span data-stu-id="382d5-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="382d5-108">Rozwiązywać problemy uniemożliwiające użytkownikom wykonywanie pracy</span><span class="sxs-lookup"><span data-stu-id="382d5-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="382d5-109">Architektura raportowania Hello opiera się na dwóch głównych filarach:</span><span class="sxs-lookup"><span data-stu-id="382d5-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="382d5-110">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="382d5-110">Security reports</span></span>
- <span data-ttu-id="382d5-111">Raporty dotyczące działań</span><span class="sxs-lookup"><span data-stu-id="382d5-111">Activity reports</span></span>

![Raportowanie](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="382d5-113">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="382d5-113">Security reports</span></span>

<span data-ttu-id="382d5-114">Hello raporty dotyczące zabezpieczeń w usłudze Azure Active Directory pomocy można tooprotect tożsamości organizacji.</span><span class="sxs-lookup"><span data-stu-id="382d5-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="382d5-115">W usłudze Azure Active Directory istnieją dwa typy raportów dotyczących zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="382d5-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="382d5-116">**Oflagowani użytkownicy ryzyka** — z hello [użytkownicy oflagowani zagrożenia zabezpieczeń raportu](active-directory-reporting-security-user-at-risk.md), zapoznaj się z omówieniem, kont użytkowników, które może być zagrożone.</span><span class="sxs-lookup"><span data-stu-id="382d5-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="382d5-117">**Ryzykowne logowania** — z hello [raport ryzykowne logowania zabezpieczeń](active-directory-reporting-security-risky-sign-ins.md), możesz uzyskać wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która jest nie hello uzasadnionych właściciela konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="382d5-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="382d5-118">**Jakie licencji usługi Azure AD potrzebujesz tooaccess raport zabezpieczeń?**</span><span class="sxs-lookup"><span data-stu-id="382d5-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="382d5-119">Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów użytkowników oflagowanych w związku z ryzykiem oraz ryzykownych logowań.</span><span class="sxs-lookup"><span data-stu-id="382d5-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="382d5-120">Jednak hello poziom szczegółowości raportu różni się między wersjami hello:</span><span class="sxs-lookup"><span data-stu-id="382d5-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="382d5-121">W hello **wersje usługi Azure Active Directory wolnego i Basic**, otrzymasz listę oflagowane ryzyka i ryzykowne logowania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="382d5-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="382d5-122">Witaj **Azure Active Directory Premium 1** edition rozszerza tego modelu, należy również włączyć tooexamine niektóre hello podstawowy zdarzenia ryzyka, które zostały wykryte dla każdego raportu.</span><span class="sxs-lookup"><span data-stu-id="382d5-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="382d5-123">Witaj **Azure Active Directory Premium 2** edition udostępnia program hello najbardziej szczegółowe informacje na temat hello podstawowy zdarzenia o podwyższonym ryzyku i pozwala także tooconfigure zasady zabezpieczeń, które automatycznie odpowiadać tooconfigured poziomów ryzyka.</span><span class="sxs-lookup"><span data-stu-id="382d5-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="382d5-124">Raporty dotyczące działań</span><span class="sxs-lookup"><span data-stu-id="382d5-124">Activity reports</span></span>

<span data-ttu-id="382d5-125">W usłudze Azure Active Directory istnieją dwa typy raportów dotyczących działań:</span><span class="sxs-lookup"><span data-stu-id="382d5-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="382d5-126">**Dzienniki inspekcji** — Witaj [dzienniki inspekcji, raport aktywności](active-directory-reporting-activity-audit-logs.md) zapewnia dostęp do historii toohello każde zadanie wykonywane w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="382d5-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="382d5-127">**Logowania** — z hello [raport aktywności logowania](active-directory-reporting-activity-sign-ins.md), można określić, kto wykonał zadania hello zgłoszone przez raport dzienniki inspekcji hello.</span><span class="sxs-lookup"><span data-stu-id="382d5-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="382d5-128">Witaj **dzienniki inspekcji, raport** umożliwia rekordów działania systemu zgodności.</span><span class="sxs-lookup"><span data-stu-id="382d5-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="382d5-129">Między innymi hello pod warunkiem, że dane pozwala tooaddress typowych scenariuszy takich jak:</span><span class="sxs-lookup"><span data-stu-id="382d5-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="382d5-130">Ktoś jest w mojej dzierżawy otrzymano grupy administracyjnej tooan dostępu.</span><span class="sxs-lookup"><span data-stu-id="382d5-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="382d5-131">Kto udzielił tej osobie prawa dostępu?</span><span class="sxs-lookup"><span data-stu-id="382d5-131">Who gave them access?</span></span> 

- <span data-ttu-id="382d5-132">Chcę tooknow hello listę Użytkownicy logujący się do określonej aplikacji od czasu I ostatnio został załadowany hello aplikacji i mają tooknow, jeśli jest również sposób</span><span class="sxs-lookup"><span data-stu-id="382d5-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="382d5-133">Chcę tooknow ile hasła resetuje są wykonywane w mojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="382d5-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="382d5-134">**Jakie licencji usługi Azure AD potrzebujesz raportu dzienniki inspekcji hello tooaccess?**</span><span class="sxs-lookup"><span data-stu-id="382d5-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="382d5-135">Raport dotyczący dzienniki inspekcji Hello jest dostępna dla funkcji, do których posiadasz licencje.</span><span class="sxs-lookup"><span data-stu-id="382d5-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="382d5-136">Jeśli masz licencję dla określonych funkcji, masz również dostęp toohello informacje dziennika inspekcji.</span><span class="sxs-lookup"><span data-stu-id="382d5-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="382d5-137">Aby uzyskać więcej informacji, zobacz **porównanie funkcji ogólnie dostępna hello wolne, Basic i Premium Edition** w [usługi Azure Active Directory, funkcje i możliwości](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="382d5-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="382d5-138">Witaj **raport aktywności logowania** tootoofind umożliwia odpowiedzi tooquestions, takich jak:</span><span class="sxs-lookup"><span data-stu-id="382d5-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="382d5-139">Co to jest hello logowania wzorzec użytkownika?</span><span class="sxs-lookup"><span data-stu-id="382d5-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="382d5-140">Ilu użytkowników zalogowało się w ciągu tygodnia?</span><span class="sxs-lookup"><span data-stu-id="382d5-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="382d5-141">Co to jest hello stan tych logowania?</span><span class="sxs-lookup"><span data-stu-id="382d5-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="382d5-142">**Czy licencji usługi Azure AD, jakie muszą tooaccess hello raport aktywności logowania?**</span><span class="sxs-lookup"><span data-stu-id="382d5-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="382d5-143">tooaccess hello raport aktywności logowania, dzierżawy musi mieć licencji usługi Azure AD Premium skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="382d5-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="382d5-144">Dostęp programowy</span><span class="sxs-lookup"><span data-stu-id="382d5-144">Programmatic access</span></span>

<span data-ttu-id="382d5-145">W interfejsie użytkownika toohello dodanie raportowania usługi Azure Active Directory zapewnia [dostęp programistyczny](active-directory-reporting-api-getting-started-azure-portal.md) toohello danych raportowania.</span><span class="sxs-lookup"><span data-stu-id="382d5-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="382d5-146">Hello dane z tych raportów mogą być bardzo przydatne tooyour aplikacji, takich jak systemów SIEM, inspekcji i narzędzia do analizy biznesowej.</span><span class="sxs-lookup"><span data-stu-id="382d5-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="382d5-147">interfejsy API zapewniają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API raportowania Hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="382d5-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="382d5-148">Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.</span><span class="sxs-lookup"><span data-stu-id="382d5-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="382d5-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="382d5-149">Next steps</span></span>

<span data-ttu-id="382d5-150">Więcej informacji na temat hello tooknow różne typy raportów w usłudze Azure Active Directory, zobacz:</span><span class="sxs-lookup"><span data-stu-id="382d5-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="382d5-151">Raport dotyczący użytkowników oflagowanych w związku z ryzykiem</span><span class="sxs-lookup"><span data-stu-id="382d5-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="382d5-152">Raport dotyczący ryzykownych logowań</span><span class="sxs-lookup"><span data-stu-id="382d5-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="382d5-153">Raport dotyczący dzienników inspekcji</span><span class="sxs-lookup"><span data-stu-id="382d5-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="382d5-154">Raport dotyczący dzienników logowania</span><span class="sxs-lookup"><span data-stu-id="382d5-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="382d5-155">Więcej informacji na temat uzyskiwania dostępu do raportowania danych przy użyciu interfejsu API raportowania hello hello hello tooknow, zobacz:</span><span class="sxs-lookup"><span data-stu-id="382d5-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="382d5-156">Wprowadzenie do korzystania z hello interfejsem API raportowania usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="382d5-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png