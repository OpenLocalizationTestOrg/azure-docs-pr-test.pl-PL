---
title: "monit o zgodę aaaUnexpected przy logowaniu się w aplikacji tooan | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot, gdy użytkownik zobaczy monit o zgodę aplikacja jest zintegrowana z usługą Azure AD, która nie oczekiwano"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="90558-103">Monit o zgodę nieoczekiwany przy logowaniu się w aplikacji tooan</span><span class="sxs-lookup"><span data-stu-id="90558-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="90558-104">Wiele aplikacji, które integrują się z usługą Azure Active Directory wymaga uprawnień toovarious zasobów w kolejności toorun.</span><span class="sxs-lookup"><span data-stu-id="90558-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="90558-105">Jeśli te zasoby są również zintegrowane z usługą Azure Active Directory, wymagany jest ich za pomocą usługi Azure AD hello tooaccess uprawnienia zgoda framework.</span><span class="sxs-lookup"><span data-stu-id="90558-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="90558-106">Powoduje to monit o zgodę pokazywane powitania po raz pierwszy jest używana w aplikacji, która często jest to jednorazowa operacja.</span><span class="sxs-lookup"><span data-stu-id="90558-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="90558-107">Scenariusze, w których użytkownicy widzą zgody monitów</span><span class="sxs-lookup"><span data-stu-id="90558-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="90558-108">Dodatkowe monity można oczekiwać w różnych scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="90558-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="90558-109">zestaw uprawnień wymaganych przez aplikację hello Hello zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="90558-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="90558-110">Hello użytkownika, który pierwotnie zgodę toohello aplikacji nie jest administratorem, a teraz różnych (użytkownika niebędącego administratorem) korzysta z aplikacji hello powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="90558-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="90558-111">Witaj użytkownika, który pierwotnie zgodę toohello aplikacji zostało administrator, ale nie wyrazili zgody w imieniu hello całej organizacji.</span><span class="sxs-lookup"><span data-stu-id="90558-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="90558-112">Aplikacja Hello używa [zgody przyrostowych i dynamicznych](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest dodatkowe uprawnienia po początkowym udzielono zgody.</span><span class="sxs-lookup"><span data-stu-id="90558-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="90558-113">Jest to często używane, gdy funkcje opcjonalne dodatkowe aplikacji wymaga uprawnień niż wymagany do obsługi funkcji linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="90558-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="90558-114">Zgody został odwołany po początkowym pozwolenia.</span><span class="sxs-lookup"><span data-stu-id="90558-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="90558-115">Deweloper Hello skonfigurował toorequire aplikacji hello monit o zgodę za każdym razem, gdy jest używany (Uwaga: to nie jest najlepszym rozwiązaniem).</span><span class="sxs-lookup"><span data-stu-id="90558-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90558-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90558-116">Next steps</span></span>

-   [<span data-ttu-id="90558-117">Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory (punkt końcowy 1.0)</span><span class="sxs-lookup"><span data-stu-id="90558-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="90558-118">Zakresy, uprawnienia i zgody w hello Azure Active Directory (punktu końcowego v2.0)</span><span class="sxs-lookup"><span data-stu-id="90558-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


