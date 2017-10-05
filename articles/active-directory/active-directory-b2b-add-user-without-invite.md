---
title: "Dodawanie użytkowników współpracy B2B do usługi Azure Active Directory bez zaproszenia | Dokumentacja firmy Microsoft"
description: "Możesz pozwolić, aby dodać inne gości do usługi Azure AD bez realizowanie zaproszenie w usłudze Azure Active Directory B2B współpracy użytkownika gościa."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 91b9477cdb679851e7d8d2942c06999a05f64e46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="0f3b8-103">Dodaj gości współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="0f3b8-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="0f3b8-104">Można zezwolić użytkownikowi, takich jak przedstawiciela partnera, aby dodać użytkowników od partnera do organizacji bez konieczności zaproszenia do zostać zrealizowane.</span><span class="sxs-lookup"><span data-stu-id="0f3b8-104">You can allow a user, such as a partner representative, to add users from the partner to your organization without needing invitations to be redeemed.</span></span> <span data-ttu-id="0f3b8-105">Wszystko, co należy wykonać to nadać temu użytkownikowi wyliczenie uprawnienia w katalogu używanego org. partnera</span><span class="sxs-lookup"><span data-stu-id="0f3b8-105">All you must do is grant that user enumeration privileges in the directory you're using for the partner org.</span></span> 

<span data-ttu-id="0f3b8-106">Udziel tych uprawnień, gdy:</span><span class="sxs-lookup"><span data-stu-id="0f3b8-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="0f3b8-107">Użytkownik w organizacji hosta (na przykład WoodGrove) zaprasza jeden użytkownik z organizacji partnerskiej (na przykład Sam@litware.com) jako Gość.</span><span class="sxs-lookup"><span data-stu-id="0f3b8-107">A user in the host organization (for example, WoodGrove) invites one user from the partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="0f3b8-108">Administrator w organizacji hosta ustawienie zasad, które umożliwiają Sam do identyfikowania i dodać inni użytkownicy z organizacji partnerskiej (Litware).</span><span class="sxs-lookup"><span data-stu-id="0f3b8-108">The admin in the host organization sets up policies that allow Sam to identify and add other users from the partner organization (Litware).</span></span>
3. <span data-ttu-id="0f3b8-109">Teraz Sam można dodawać innych użytkowników z Litware do katalogu WoodGrove, grupy lub aplikacji bez konieczności zaproszenia do zostać zrealizowane.</span><span class="sxs-lookup"><span data-stu-id="0f3b8-109">Now Sam can add other users from Litware to the WoodGrove directory, groups, or applications without needing invitations to be redeemed.</span></span> <span data-ttu-id="0f3b8-110">Jeśli Sam ma wyliczenie odpowiednie uprawnienia w Litware, odbywa się automatycznie.</span><span class="sxs-lookup"><span data-stu-id="0f3b8-110">If Sam has the appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="0f3b8-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0f3b8-111">Next steps</span></span>

<span data-ttu-id="0f3b8-112">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0f3b8-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="0f3b8-113">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="0f3b8-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="0f3b8-114">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="0f3b8-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="0f3b8-115">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="0f3b8-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="0f3b8-116">Elementy współpracy B2B zaproszenie</span><span class="sxs-lookup"><span data-stu-id="0f3b8-116">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="0f3b8-117">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0f3b8-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="0f3b8-118">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="0f3b8-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="0f3b8-119">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="0f3b8-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="0f3b8-120">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="0f3b8-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="0f3b8-121">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="0f3b8-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="0f3b8-122">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0f3b8-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="0f3b8-123">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f3b8-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)