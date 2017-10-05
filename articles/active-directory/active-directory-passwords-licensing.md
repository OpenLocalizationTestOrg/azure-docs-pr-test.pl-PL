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
ms.openlocfilehash: 936134bddad19964f809a17f200ebbeed5aa853c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="8aa28-103">Wymagania dotyczące usługi Azure AD samoobsługi hasła licencjonowania resetowania</span><span class="sxs-lookup"><span data-stu-id="8aa28-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="8aa28-104">Aby resetowania hasła programu Azure AD, funkcji możesz **musi mieć co najmniej jedną licencję przypisane w Twojej organizacji**.</span><span class="sxs-lookup"><span data-stu-id="8aa28-104">In order for Azure AD Password Reset to function, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="8aa28-105">Firma Microsoft nie wymuszają licencjonowania na środowisku resetowania hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8aa28-105">We do not enforce per-user licensing on the password reset experience.</span></span> <span data-ttu-id="8aa28-106">Aby zachować zgodność z umowy licencyjnej firmy Microsoft, należy przypisać licencje do użytkowników korzystających z funkcji premium.</span><span class="sxs-lookup"><span data-stu-id="8aa28-106">To maintain compliance with your Microsoft licensing agreement, you need to assign licenses to any users that use premium features.</span></span>

* <span data-ttu-id="8aa28-107">**Tylko użytkownicy w chmurze** -usługi Office 365 (O365) żadnego płatnej SKU lub Azure AD podstawowa</span><span class="sxs-lookup"><span data-stu-id="8aa28-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="8aa28-108">**Chmura** i/lub **lokalnych użytkowników** -Azure AD Premium P1 lub P2 pakietu Enterprise Mobility + Security (EMS) i Secure produktywności przedsiębiorstwa (p)</span><span class="sxs-lookup"><span data-stu-id="8aa28-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="8aa28-109">Licencjami wymaganymi do zapisywania zwrotnego haseł</span><span class="sxs-lookup"><span data-stu-id="8aa28-109">Licenses required for password writeback</span></span>

<span data-ttu-id="8aa28-110">Aby użyć funkcji zapisywania zwrotnego haseł, musi mieć jedną z poniższych licencji przypisane w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="8aa28-110">To use password writeback, you must have one of the following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="8aa28-111">Usługa Azure AD — warstwa Premium P1</span><span class="sxs-lookup"><span data-stu-id="8aa28-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="8aa28-112">Usługa Azure AD — warstwa Premium P2</span><span class="sxs-lookup"><span data-stu-id="8aa28-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="8aa28-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="8aa28-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="8aa28-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="8aa28-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="8aa28-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="8aa28-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="8aa28-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="8aa28-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="8aa28-117">Plany licencjonowania usługi Office 365 autonomiczny **nie obsługują funkcji zapisywania zwrotnego haseł** i muszą mieć jedną z powyższych planów ta funkcja działała.</span><span class="sxs-lookup"><span data-stu-id="8aa28-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of the preceding plans for this functionality to work.</span></span>

<span data-ttu-id="8aa28-118">Dodatkowe informacje o licencji, wraz z kosztami można znaleźć na następujących stronach</span><span class="sxs-lookup"><span data-stu-id="8aa28-118">Additional licensing info including costs can be found on the following pages</span></span>

* [<span data-ttu-id="8aa28-119">Usługi Azure site cennik usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="8aa28-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="8aa28-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="8aa28-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="8aa28-121">Bezpieczne produktywności Enterprise</span><span class="sxs-lookup"><span data-stu-id="8aa28-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="8aa28-122">Włącz grupy lub użytkownika na podstawie licencjonowania</span><span class="sxs-lookup"><span data-stu-id="8aa28-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="8aa28-123">Teraz usługi Azure AD obsługuje oparte na grupach licencjonowania, dzięki czemu administratorzy Aby przypisać licencje zbiorczo do grupy użytkowników, a nie przypisywanie pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="8aa28-123">Azure AD now supports group-based licensing allowing administrators to assign licenses in bulk to a group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="8aa28-124">Przypisać, sprawdź i rozwiąż problemy z licencjami</span><span class="sxs-lookup"><span data-stu-id="8aa28-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="8aa28-125">Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="8aa28-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="8aa28-126">Zanim można przypisać licencję do użytkownika, administrator musi określić właściwość "Lokalizacji użytkowania" użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8aa28-126">Before a license can be assigned to a user, the administrator must specify the “Usage location” property on the user.</span></span> <span data-ttu-id="8aa28-127">Można wykonać przypisania licencji użytkownika > Profil > w sekcji Ustawienia w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa28-127">Assignment of licenses can be done under User > Profile > Settings section in the Azure portal.</span></span> <span data-ttu-id="8aa28-128">**Korzystając z przypisanie do grupy licencji, wszyscy użytkownicy bez użycia lokalizacji określonej dziedziczą lokalizację katalogu.**</span><span class="sxs-lookup"><span data-stu-id="8aa28-128">**When using group license assignment, any users without a usage location specified inherit the location of the directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="8aa28-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8aa28-129">Next steps</span></span>

<span data-ttu-id="8aa28-130">Poniższe linki dają dostęp do dodatkowych informacji dotyczących resetowania haseł za pomocą usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8aa28-130">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="8aa28-131">[**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="8aa28-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="8aa28-132">[**Dane**](active-directory-passwords-data.md) — Omówienie wymaganych danych i sposobu ich wykorzystania w zarządzaniu hasłami</span><span class="sxs-lookup"><span data-stu-id="8aa28-132">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="8aa28-133">[**Wdrażanie**](active-directory-passwords-best-practices.md) — Planowanie funkcji samoobsługowego resetowania haseł i jej wdrażanie dla użytkowników przy użyciu znajdujących się tu wytycznych</span><span class="sxs-lookup"><span data-stu-id="8aa28-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="8aa28-134">[**Dostosowywanie**](active-directory-passwords-customize.md) — Dostosowywanie wyglądu i działania środowiska samoobsługowego resetowania haseł dla firmy</span><span class="sxs-lookup"><span data-stu-id="8aa28-134">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="8aa28-135">[**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="8aa28-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="8aa28-136">[**Szczegóły techniczne**](active-directory-passwords-how-it-works.md) — Informacje o tym, co dzieje się za kulisami tej funkcji i jak ona działa</span><span class="sxs-lookup"><span data-stu-id="8aa28-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="8aa28-137">[**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak?</span><span class="sxs-lookup"><span data-stu-id="8aa28-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="8aa28-138">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="8aa28-138">Why?</span></span> <span data-ttu-id="8aa28-139">Co?</span><span class="sxs-lookup"><span data-stu-id="8aa28-139">What?</span></span> <span data-ttu-id="8aa28-140">Gdzie?</span><span class="sxs-lookup"><span data-stu-id="8aa28-140">Where?</span></span> <span data-ttu-id="8aa28-141">Kto?</span><span class="sxs-lookup"><span data-stu-id="8aa28-141">Who?</span></span> <span data-ttu-id="8aa28-142">Kiedy?</span><span class="sxs-lookup"><span data-stu-id="8aa28-142">When?</span></span> <span data-ttu-id="8aa28-143">— Odpowiedzi na wszystkie nurtujące Cię pytania</span><span class="sxs-lookup"><span data-stu-id="8aa28-143">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="8aa28-144">[**Rozwiązywanie problemów**](active-directory-passwords-troubleshoot.md) — Informacje o tym, jak rozwiązywać typowe problemy z samoobsługowym resetowaniem haseł</span><span class="sxs-lookup"><span data-stu-id="8aa28-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

