---
title: "Monit o zgodę nieoczekiwany po zalogowaniu się do aplikacji | Dokumentacja firmy Microsoft"
description: "Jak rozwiązywać problemy z, gdy użytkownik zobaczy monit o zgodę dla aplikacji, który jest zintegrowany z usługą Azure AD, która nie oczekiwano"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="15b8c-103">Monit o zgodę nieoczekiwany po zalogowaniu się do aplikacji</span><span class="sxs-lookup"><span data-stu-id="15b8c-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="15b8c-104">Wiele aplikacji, które integrują się z usługą Azure Active Directory wymaga uprawnień do różnych zasobów, aby można było uruchomić.</span><span class="sxs-lookup"><span data-stu-id="15b8c-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="15b8c-105">Jeśli te zasoby również są zintegrowane z usługą Azure Active Directory, uprawnienia dostępu do nich żądania przy użyciu platformy zgody usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15b8c-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="15b8c-106">Powoduje to zgody monit jest wyświetlany przy pierwszym uruchomieniu aplikacji jest używany, która często jest to jednorazowa operacja.</span><span class="sxs-lookup"><span data-stu-id="15b8c-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="15b8c-107">Scenariusze, w których użytkownicy widzą zgody monitów</span><span class="sxs-lookup"><span data-stu-id="15b8c-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="15b8c-108">Dodatkowe monity można oczekiwać w różnych scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="15b8c-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="15b8c-109">Zmieniono zestaw uprawnień wymaganych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="15b8c-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="15b8c-110">Administrator nie jest użytkownik, który pierwotnie zgodę na aplikacji, a teraz różnych (użytkownika niebędącego administratorem) używa aplikacji po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="15b8c-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="15b8c-111">Użytkownik, który pierwotnie zgodę na aplikację została administrator, ale nie one zgody w imieniu całej organizacji.</span><span class="sxs-lookup"><span data-stu-id="15b8c-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="15b8c-112">Aplikacja używa [zgody przyrostowych i dynamicznych](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) celu zażądania dodatkowych uprawnień po początkowym udzielono zgody.</span><span class="sxs-lookup"><span data-stu-id="15b8c-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="15b8c-113">Jest to często używane, gdy funkcje opcjonalne dodatkowe aplikacji wymaga uprawnień niż wymagany do obsługi funkcji linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="15b8c-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="15b8c-114">Zgody został odwołany po początkowym pozwolenia.</span><span class="sxs-lookup"><span data-stu-id="15b8c-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="15b8c-115">Deweloper skonfigurował aplikacji do wyświetlania monitów zgodę za każdym razem, gdy jest używany (Uwaga: to nie jest najlepszym rozwiązaniem).</span><span class="sxs-lookup"><span data-stu-id="15b8c-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15b8c-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15b8c-116">Next steps</span></span>

-   [<span data-ttu-id="15b8c-117">Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory (punkt końcowy 1.0)</span><span class="sxs-lookup"><span data-stu-id="15b8c-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="15b8c-118">Zakresy, uprawnienia i zgody w usłudze Azure Active Directory (punktu końcowego v2.0)</span><span class="sxs-lookup"><span data-stu-id="15b8c-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


