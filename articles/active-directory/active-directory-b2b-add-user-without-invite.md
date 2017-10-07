---
title: "Współpraca aaaAdd B2B użytkowników tooAzure usługi Active Directory bez zaproszenia | Dokumentacja firmy Microsoft"
description: "Możesz pozwolić, aby dodać inne gościa tooyour użytkowników usługi Azure AD bez realizowanie zaproszenie w usłudze Azure Active Directory B2B współpracy użytkownika gościa."
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="f4dad-103">Dodaj gości współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="f4dad-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="f4dad-104">Może pozwolić użytkownikowi, takie jak partnera reprezentatywny, tooadd użytkownicy z organizacji tooyour partnera hello bez konieczności zrealizowane toobe zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="f4dad-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="f4dad-105">Wszystko, co należy wykonać to nadać temu użytkownikowi uprawnień wyliczenia w katalogu hello, którego używasz hello partnera org.</span><span class="sxs-lookup"><span data-stu-id="f4dad-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="f4dad-106">Udziel tych uprawnień, gdy:</span><span class="sxs-lookup"><span data-stu-id="f4dad-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="f4dad-107">Użytkownik w organizacji hosta hello (na przykład WoodGrove) zaprasza jeden użytkownik z organizacji partnerskiej hello (na przykład Sam@litware.com) jako Gość.</span><span class="sxs-lookup"><span data-stu-id="f4dad-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="f4dad-108">Witaj, Administratorze w organizacji hosta hello konfiguruje zasady, które umożliwia Sam tooidentify i dodać inni użytkownicy z organizacji partnerskiej hello (Litware).</span><span class="sxs-lookup"><span data-stu-id="f4dad-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="f4dad-109">Teraz Sam można dodawać innych użytkowników z katalogu WoodGrove toohello Litware, grupy lub aplikacji bez konieczności zrealizowane toobe zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="f4dad-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="f4dad-110">Jeśli Sam ma hello wyliczenie odpowiednie uprawnienia w Litware, jego odbywa się automatycznie.</span><span class="sxs-lookup"><span data-stu-id="f4dad-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="f4dad-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4dad-111">Next steps</span></span>

<span data-ttu-id="f4dad-112">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="f4dad-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f4dad-113">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="f4dad-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f4dad-114">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="f4dad-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="f4dad-115">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="f4dad-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="f4dad-116">elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="f4dad-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="f4dad-117">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="f4dad-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="f4dad-118">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="f4dad-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="f4dad-119">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f4dad-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="f4dad-120">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="f4dad-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="f4dad-121">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="f4dad-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="f4dad-122">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="f4dad-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="f4dad-123">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4dad-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)