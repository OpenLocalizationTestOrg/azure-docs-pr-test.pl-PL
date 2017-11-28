---
title: "AAA wystąpił nieoczekiwany błąd podczas wykonywania aplikacji tooan zgody | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono błędów, które mogą wystąpić w trakcie procesu hello zgodę tooan aplikacji i co można zrobić o nich"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a><span data-ttu-id="3310c-103">Wystąpił nieoczekiwany błąd podczas wykonywania zgody tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="3310c-103">Unexpected error when performing consent tooan application</span></span>

<span data-ttu-id="3310c-104">W tym artykule omówiono błędów, które mogą wystąpić w trakcie procesu hello zgodę tooan aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3310c-104">This article discusses errors that can occur during hello process of consenting tooan application.</span></span> <span data-ttu-id="3310c-105">Jeśli jesteś rozwiązywanie nieoczekiwany zgody monity nie zawiera komunikaty o błędach, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="3310c-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="3310c-106">Wiele aplikacji, które integrują się z usługą Azure Active Directory wymaga uprawnienia tooaccess innych zasobów w kolejności toofunction.</span><span class="sxs-lookup"><span data-stu-id="3310c-106">Many applications that integrate with Azure Active Directory require permissions tooaccess other resources in order toofunction.</span></span> <span data-ttu-id="3310c-107">Jeśli te zasoby są również zintegrowane z usługą Azure Active Directory, tooaccess uprawnień, ich jest często żądana za pomocą wspólnego hello zgoda framework.</span><span class="sxs-lookup"><span data-stu-id="3310c-107">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is often requested using hello common consent framework.</span></span> 

<span data-ttu-id="3310c-108">Powoduje to monit o zgodę będzie wyświetlany, którego działanie ma zazwyczaj miejsce powitania po raz pierwszy aplikacja jest używana, ale może również wystąpić w kolejnych za pomocą aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3310c-108">This results in a consent prompt being displayed, which generally occurs hello first time an application is used but can also occur on a subsequent use of hello application.</span></span>

<span data-ttu-id="3310c-109">Określone warunki musi mieć wartość true dla uprawnienia toohello tooconsent użytkownika, który wymaga aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3310c-109">Certain conditions must be true for a user tooconsent toohello permissions an application requires.</span></span> <span data-ttu-id="3310c-110">Jeśli te warunki nie są spełnione, mogą wystąpić różne błędy.</span><span class="sxs-lookup"><span data-stu-id="3310c-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="3310c-111">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="3310c-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="3310c-112">Błąd uprawnień nie Autoryzowano żądania</span><span class="sxs-lookup"><span data-stu-id="3310c-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="3310c-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; żąda jedno lub więcej uprawnień, które nie są autoryzowane toogrant.</span><span class="sxs-lookup"><span data-stu-id="3310c-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized toogrant.</span></span> <span data-ttu-id="3310c-114">Skontaktuj się z administratorem, który można wyrazić zgodę toothis aplikacji w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="3310c-114">Contact an administrator, who can consent toothis application on your behalf.</span></span>

<span data-ttu-id="3310c-115">Ten błąd występuje, gdy użytkownik, który nie jest administratorem firmy próbuje toouse aplikacji, która żąda uprawnienia, których może udzielić tylko administrator.</span><span class="sxs-lookup"><span data-stu-id="3310c-115">This error occurs when a user who is not a company administrator attempts toouse an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="3310c-116">Ten błąd można rozwiązać przez administratora udzielanie dostępu toohello aplikacji w imieniu swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="3310c-116">This error can be resolved by an administrator granting access toohello application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="3310c-117">Zasady uniemożliwiają udzielanie uprawnień błąd</span><span class="sxs-lookup"><span data-stu-id="3310c-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="3310c-118">**AADSTS90093:** administrator &lt;tenantDisplayName&gt; ustawił zasadę, która uniemożliwia udzielanie &lt;Nazwa aplikacji&gt; hello żąda uprawnień.</span><span class="sxs-lookup"><span data-stu-id="3310c-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; hello permissions it is requesting.</span></span> <span data-ttu-id="3310c-119">Skontaktuj się z administratorem &lt;tenantDisplayName&gt;, który można przyznać uprawnień toothis aplikacji w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="3310c-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions toothis app on your behalf.</span></span>

<span data-ttu-id="3310c-120">Ten błąd występuje, gdy administrator firmy wyłącza możliwość hello tooapplications tooconsent użytkowników, a następnie użytkownik bez uprawnień administratora próbuje toouse aplikację, która wymaga zgody.</span><span class="sxs-lookup"><span data-stu-id="3310c-120">This error occurs when a company administrator turns off hello ability for users tooconsent tooapplications, then a non-administrator user attempts toouse an application that requires consent.</span></span> <span data-ttu-id="3310c-121">Ten błąd można rozwiązać przez administratora udzielanie dostępu toohello aplikacji w imieniu swojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="3310c-121">This error can be resolved by an administrator granting access toohello application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="3310c-122">Problem tymczasowy błąd</span><span class="sxs-lookup"><span data-stu-id="3310c-122">Intermittent problem error</span></span>
* <span data-ttu-id="3310c-123">**AADSTS90090:** prawdopodobnie wystąpił problem tymczasowy rejestrowania uprawnienia hello podjęto zbyt toogrant&lt;clientAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="3310c-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording hello permissions you attempted toogrant too&lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="3310c-124">Spróbuj ponownie później.</span><span class="sxs-lookup"><span data-stu-id="3310c-124">try again later.</span></span>

<span data-ttu-id="3310c-125">Ten błąd wskazuje, że wystąpił problem po stronie usługi tymczasowymi.</span><span class="sxs-lookup"><span data-stu-id="3310c-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="3310c-126">Można go rozwiązać przez podejmowanie próby tooconsent toohello ponownie aplikację.</span><span class="sxs-lookup"><span data-stu-id="3310c-126">It can be resolved by attempting tooconsent toohello application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="3310c-127">Zasób nie jest dostępny błąd</span><span class="sxs-lookup"><span data-stu-id="3310c-127">Resource not available error</span></span>
* <span data-ttu-id="3310c-128">**AADSTS65005:** aplikacji hello &lt;clientAppDisplayName&gt; wymagane uprawnienia tooaccess zasobu &lt;resourceAppDisplayName&gt; jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="3310c-128">**AADSTS65005:** hello app &lt;clientAppDisplayName&gt; requested permissions tooaccess a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="3310c-129">Skontaktuj się z deweloperem aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3310c-129">Contact hello application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="3310c-130">Zasób nie jest dostępna w błąd dzierżawy</span><span class="sxs-lookup"><span data-stu-id="3310c-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="3310c-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; żąda dostępu do zasobów tooa &lt;resourceAppDisplayName&gt; które nie są dostępne w Twojej organizacji &lt; tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="3310c-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access tooa resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="3310c-132">Upewnij się, że ten zasób jest dostępny, lub skontaktuj się z administratorem &lt;tenantDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="3310c-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="3310c-133">Błąd niezgodności uprawnień</span><span class="sxs-lookup"><span data-stu-id="3310c-133">Permissions mismatch error</span></span>
* <span data-ttu-id="3310c-134">**AADSTS65005:** aplikacji hello żądany zasób tooaccess zgody &lt;resourceAppDisplayName&gt;.</span><span class="sxs-lookup"><span data-stu-id="3310c-134">**AADSTS65005:** hello app requested consent tooaccess resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="3310c-135">To żądanie nie powiodło się, ponieważ nie jest zgodny, jak aplikacja hello zostało wstępnie skonfigurowane podczas rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3310c-135">This request failed because it does not match how hello app was pre-configured during app registration.</span></span> <span data-ttu-id="3310c-136">Skontaktuj się z hello aplikacji vendor.* *</span><span class="sxs-lookup"><span data-stu-id="3310c-136">Contact hello app vendor.**</span></span>

<span data-ttu-id="3310c-137">Wszystkie błędy występują, jeśli aplikacja hello użytkownik próbuje toois tooconsent żąda uprawnienia tooaccess aplikacji zasobów, której nie można znaleźć w katalogu organizacji hello (dzierżawcy).</span><span class="sxs-lookup"><span data-stu-id="3310c-137">These errors all occur when hello application a user is trying tooconsent toois requesting permissions tooaccess a resource application that cannot be found in hello organization’s directory (tenant).</span></span> <span data-ttu-id="3310c-138">Taka sytuacja może wystąpić z kilku powodów:</span><span class="sxs-lookup"><span data-stu-id="3310c-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="3310c-139">Deweloper aplikacji Hello klienta ma ich stosowania nieprawidłowo skonfigurowane, powodowania toorequest dostępu tooan nieprawidłowy zasób.</span><span class="sxs-lookup"><span data-stu-id="3310c-139">hello client application developer has configured their application incorrectly, causing it toorequest access tooan invalid resource.</span></span> <span data-ttu-id="3310c-140">W takim przypadku Deweloper aplikacji hello należy zaktualizować konfigurację hello powitania klienta aplikacji tooresolve ten problem.</span><span class="sxs-lookup"><span data-stu-id="3310c-140">In this case, hello application developer must update hello configuration of hello client application tooresolve this issue.</span></span>

-   <span data-ttu-id="3310c-141">Nazwy głównej usługi reprezentujący hello docelowego zasobu aplikacji nie istnieje w organizacji hello lub istniał w przeszłości hello, ale została usunięta.</span><span class="sxs-lookup"><span data-stu-id="3310c-141">A Service Principal representing hello target resource application does not exist in hello organization, or existed in hello past but has been removed.</span></span> <span data-ttu-id="3310c-142">Ten problem, nazwy głównej usługi hello zasobów aplikacji musi być udostępnione w organizacji hello tak powitania klienta aplikacji można zażądać uprawnień tooit tooresolve.</span><span class="sxs-lookup"><span data-stu-id="3310c-142">tooresolve this issue, a Service Principal for hello resource application must be provisioned in hello organization so hello client application can request permissions tooit.</span></span> <span data-ttu-id="3310c-143">Może to wystąpić w różne sposoby, w zależności od typu hello aplikacji, w tym:</span><span class="sxs-lookup"><span data-stu-id="3310c-143">This can happen in an number of ways, depending on hello type of application, including:</span></span>

    -   <span data-ttu-id="3310c-144">Uzyskiwanie subskrypcji dla aplikacji zasobów hello (Firma Microsoft opublikowała aplikacji)</span><span class="sxs-lookup"><span data-stu-id="3310c-144">Acquiring a subscription for hello resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="3310c-145">Zgodę toohello zasobów aplikacji</span><span class="sxs-lookup"><span data-stu-id="3310c-145">Consenting toohello resource application</span></span>

    -   <span data-ttu-id="3310c-146">Udzielanie uprawnień aplikacji hello za pośrednictwem hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3310c-146">Granting hello application permissions via hello Azure Portal</span></span>

    -   <span data-ttu-id="3310c-147">Dodawanie aplikacji hello z hello galerii aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3310c-147">Adding hello application from hello Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="3310c-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3310c-148">Next steps</span></span> 

[<span data-ttu-id="3310c-149">Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory (punkt końcowy v1)</span><span class="sxs-lookup"><span data-stu-id="3310c-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="3310c-150">Zakresy, uprawnienia i zgody w hello Azure Active Directory (punktu końcowego v2.0)</span><span class="sxs-lookup"><span data-stu-id="3310c-150">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


