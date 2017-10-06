---
title: 'Licencjonowanie: Azure AD SSPR | Dokumentacja firmy Microsoft'
description: "Azure AD samoobsługowego resetowania hasła wymagania licencyjne"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="f7227-103">Wymagania dotyczące usługi Azure AD samoobsługi hasła licencjonowania resetowania</span><span class="sxs-lookup"><span data-stu-id="f7227-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="f7227-104">Aby Azure resetowania hasła AD toofunction możesz **musi mieć co najmniej jedną licencję przypisane w Twojej organizacji**.</span><span class="sxs-lookup"><span data-stu-id="f7227-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="f7227-105">Firma Microsoft nie wymuszają licencjonowania na środowisko resetowania hasła hello na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7227-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="f7227-106">toomaintain zgodności z umowy licencyjnej firmy Microsoft, należy tooassign licencji tooany użytkowników korzystających z funkcji premium.</span><span class="sxs-lookup"><span data-stu-id="f7227-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="f7227-107">**Tylko użytkownicy w chmurze** -usługi Office 365 (O365) żadnego płatnej SKU lub Azure AD podstawowa</span><span class="sxs-lookup"><span data-stu-id="f7227-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="f7227-108">**Chmura** i/lub **lokalnych użytkowników** -Azure AD Premium P1 lub P2 pakietu Enterprise Mobility + Security (EMS) i Secure produktywności przedsiębiorstwa (p)</span><span class="sxs-lookup"><span data-stu-id="f7227-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="f7227-109">Licencjami wymaganymi do zapisywania zwrotnego haseł</span><span class="sxs-lookup"><span data-stu-id="f7227-109">Licenses required for password writeback</span></span>

<span data-ttu-id="f7227-110">Zapisywanie zwrotne haseł toouse, użytkownik musi mieć jeden z powitania od licencji przypisanych w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="f7227-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="f7227-111">Usługa Azure AD — warstwa Premium P1</span><span class="sxs-lookup"><span data-stu-id="f7227-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="f7227-112">Usługa Azure AD — warstwa Premium P2</span><span class="sxs-lookup"><span data-stu-id="f7227-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="f7227-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="f7227-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="f7227-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="f7227-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="f7227-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="f7227-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="f7227-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="f7227-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="f7227-117">Plany licencjonowania usługi Office 365 autonomiczny **nie obsługują funkcji zapisywania zwrotnego haseł** i wymagać hello poprzedzających plany toowork tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f7227-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="f7227-118">Dodatkowe informacje o licencji, wraz z kosztami znajduje się na powitania po stron</span><span class="sxs-lookup"><span data-stu-id="f7227-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="f7227-119">Usługi Azure site cennik usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7227-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="f7227-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="f7227-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="f7227-121">Bezpieczne produktywności Enterprise</span><span class="sxs-lookup"><span data-stu-id="f7227-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="f7227-122">Włącz grupy lub użytkownika na podstawie licencjonowania</span><span class="sxs-lookup"><span data-stu-id="f7227-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="f7227-123">Teraz usługi Azure AD obsługuje oparte na grupach licencjonowania, dzięki czemu administratorzy tooassign licencji w zbiorczego tooa grupy użytkowników, a nie przypisywanie pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="f7227-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="f7227-124">Przypisać, sprawdź i rozwiąż problemy z licencjami</span><span class="sxs-lookup"><span data-stu-id="f7227-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="f7227-125">Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="f7227-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="f7227-126">Przed tooa użytkownika można przypisać licencji, hello administrator musi określać właściwość "Lokalizacji użytkowania" hello na powitania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7227-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="f7227-127">Można wykonać przypisania licencji użytkownika > Profil > w sekcji Ustawienia w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f7227-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="f7227-128">**Korzystając z przypisanie do grupy licencji, wszyscy użytkownicy bez użycia lokalizacji określonej dziedziczą hello lokalizację katalogu hello.**</span><span class="sxs-lookup"><span data-stu-id="f7227-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7227-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7227-129">Next steps</span></span>

<span data-ttu-id="f7227-130">Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7227-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="f7227-131">[**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7227-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="f7227-132">[**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami</span><span class="sxs-lookup"><span data-stu-id="f7227-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="f7227-133">[**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj</span><span class="sxs-lookup"><span data-stu-id="f7227-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="f7227-134">[**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.</span><span class="sxs-lookup"><span data-stu-id="f7227-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="f7227-135">[**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="f7227-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="f7227-136">[**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa</span><span class="sxs-lookup"><span data-stu-id="f7227-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="f7227-137">[**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak?</span><span class="sxs-lookup"><span data-stu-id="f7227-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="f7227-138">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="f7227-138">Why?</span></span> <span data-ttu-id="f7227-139">Co?</span><span class="sxs-lookup"><span data-stu-id="f7227-139">What?</span></span> <span data-ttu-id="f7227-140">Gdzie?</span><span class="sxs-lookup"><span data-stu-id="f7227-140">Where?</span></span> <span data-ttu-id="f7227-141">Kto?</span><span class="sxs-lookup"><span data-stu-id="f7227-141">Who?</span></span> <span data-ttu-id="f7227-142">Kiedy?</span><span class="sxs-lookup"><span data-stu-id="f7227-142">When?</span></span> <span data-ttu-id="f7227-143">-Tooquestions tooask chciał zawsze odpowiada</span><span class="sxs-lookup"><span data-stu-id="f7227-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="f7227-144">[**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR</span><span class="sxs-lookup"><span data-stu-id="f7227-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

