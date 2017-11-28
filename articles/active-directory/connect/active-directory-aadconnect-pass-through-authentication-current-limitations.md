---
title: "Azure AD Connect: Przekazywanego uwierzytelniania - bieżące ograniczenia | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello bieżących ograniczeń uwierzytelniania przekazywanego usługi Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Azure AD Connect przekazywanego uwierzytelniania, instalacji usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="2c0f9-104">Usługi Azure Active Directory przekazywanego uwierzytelniania: Bieżące ograniczenia</span><span class="sxs-lookup"><span data-stu-id="2c0f9-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="2c0f9-105">Azure AD przekazywanego uwierzytelniania jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="2c0f9-106">Jest bezpłatna funkcji i nie wymagają żadnych płatnej wersji usługi Azure AD toouse go.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-106">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="2c0f9-107">Przekazywanego uwierzytelniania jest dostępna tylko w Witaj świecie wystąpienia usługi Azure AD, a nie na [Niemcy Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) i [Microsoft Azure dla instytucji rządowych Cloud](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="2c0f9-107">Pass-through Authentication is only available in hello world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="2c0f9-108">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="2c0f9-108">Supported scenarios</span></span>

<span data-ttu-id="2c0f9-109">Hello następujące scenariusze są obsługiwane w wersji zapoznawczej:</span><span class="sxs-lookup"><span data-stu-id="2c0f9-109">hello following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="2c0f9-110">Użytkownik logowania do wszystkich aplikacji opartej na przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="2c0f9-111">Logowania użytkownika do aplikacji klienta usługi Office 365, które obsługują [nowoczesnego uwierzytelniania](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="2c0f9-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="2c0f9-112">Azure AD Join dla urządzeń z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="2c0f9-113">Obsługa programu Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="2c0f9-114">Nieobsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="2c0f9-114">Unsupported scenarios</span></span>

<span data-ttu-id="2c0f9-115">Hello są następujące scenariusze _nie_ obsługiwane w wersji zapoznawczej:</span><span class="sxs-lookup"><span data-stu-id="2c0f9-115">hello following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="2c0f9-116">Użytkownik logowania do aplikacji klienta starszej wersji pakietu Office (Office 2013 lub starszym).</span><span class="sxs-lookup"><span data-stu-id="2c0f9-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="2c0f9-117">Organizacje są zachęcani tooswitch toomodern uwierzytelniania, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-117">Organizations are encouraged tooswitch toomodern authentication, if possible.</span></span> <span data-ttu-id="2c0f9-118">Umożliwia obsługę uwierzytelniania przekazywanego nowoczesnego uwierzytelniania, ale również pomaga zabezpieczyć użytkownika kont przy użyciu narzędzia [dostępu warunkowego](../active-directory-conditional-access.md) funkcje takie jak uwierzytelnianie wieloskładnikowe (MFA).</span><span class="sxs-lookup"><span data-stu-id="2c0f9-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="2c0f9-119">Użytkownik logowania do usługi Skype dla firm klienta aplikacji, w tym usługi Skype dla firm 2016.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="2c0f9-120">Użytkownik logowania do programu PowerShell w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="2c0f9-121">Zalecane jest, użyj programu PowerShell w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2c0f9-122">Jako obejście nieobsługiwanych scenariuszy, Włącz synchronizacji skrótu hasła na powitania [funkcje opcjonalne](active-directory-aadconnect-get-started-custom.md#optional-features) w kreatorze Połącz hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on hello [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in hello Azure AD Connect wizard.</span></span> <span data-ttu-id="2c0f9-123">Synchronizacja skrótów haseł działa jako rezerwowe dla hello poprzedzających scenariusze _tylko_ (i _nie_ jako ogólnego tooPass do uwierzytelniania rezerwowego).</span><span class="sxs-lookup"><span data-stu-id="2c0f9-123">Password Hash Synchronization acts as a fallback for hello preceding scenarios _only_ (and _not_ as a generic fallback tooPass-through Authentication).</span></span> <span data-ttu-id="2c0f9-124">Jeśli nie potrzebujesz tych scenariuszy, wyłącz synchronizacji skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c0f9-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c0f9-125">Next steps</span></span>
- <span data-ttu-id="2c0f9-126">[**Szybki Start** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) — Uzyskaj i systemem Azure AD przekazywanego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="2c0f9-127">[**Nowości techniczne** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -zrozumieć sposób działania tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="2c0f9-128">[**Często zadawane pytania** ](active-directory-aadconnect-pass-through-authentication-faq.md) -odpowiedzi toofrequently zadawane pytania.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="2c0f9-129">[**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="2c0f9-130">[**Azure AD SSO bezproblemowe** ](active-directory-aadconnect-sso.md) — Dowiedz się więcej o tej funkcji uzupełniające.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="2c0f9-131">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="2c0f9-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
