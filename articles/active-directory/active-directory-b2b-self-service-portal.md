---
title: "Zapisywania się do portalu usługi Azure Active Directory B2B współpracy | Dokumentacja firmy Microsoft"
description: "Współpraca B2B usługi Azure Active Directory wspiera relacje między firmami, umożliwiając partnerom biznesowym selektywne uzyskiwanie dostępu do Twoich aplikacji firmowych"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 307373c75bbb87cec683f7a3097f8f159c9d5e61
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="d0af8-103">Portal samoobsługowy do zapisywania do współpracy B2B usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0af8-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="d0af8-104">Klienci umożliwiają wykonywanie wielu z wbudowanych funkcji, które są dostępne za pośrednictwem naszego administrator IT [portalu Azure](https://portal.azure.com) i naszych [panelu dostępu aplikacji](https://myapps.microsoft.com) dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="d0af8-104">Customers can do a lot with the built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="d0af8-105">Ale możemy również pamiętać, że firmy muszą dostosować przepływ pracy dołączania użytkowników B2B do potrzeb organizacji.</span><span class="sxs-lookup"><span data-stu-id="d0af8-105">But we are also aware that businesses need to customize the onboarding workflow for B2B users to fit their organization’s needs.</span></span> <span data-ttu-id="d0af8-106">Można wykonać z [interfejsach API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="d0af8-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="d0af8-107">W dyskusjach ze specjalistami z naszych klientów widzimy się, że jeden wspólny wjazd należy przede wszystkim innym.</span><span class="sxs-lookup"><span data-stu-id="d0af8-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="d0af8-108">Zapraszanie organizacji może nie wiedzieć, wcześniej, którzy są poszczególne zewnętrznych współpracowników którzy potrzebują dostępu do zasobów.</span><span class="sxs-lookup"><span data-stu-id="d0af8-108">The inviting organization may not know ahead of time who the individual external collaborators are who need access to their resources.</span></span> <span data-ttu-id="d0af8-109">Chcieli sposób dla użytkowników z firm partnerskich o zarejestrowanie się przy użyciu zestawu zasad, które kontroluje zaproszenia organizacji.</span><span class="sxs-lookup"><span data-stu-id="d0af8-109">They wanted a way for users from partner companies to  sign themselves up with a set of policies that the inviting organization controls.</span></span> <span data-ttu-id="d0af8-110">Ten scenariusz jest możliwe za pośrednictwem naszych interfejsów API, dlatego firma Microsoft opublikowane projektu w witrynie Github, która została właśnie tę: [przykładowy projekt Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="d0af8-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="d0af8-111">Naszych projektu Github pokazano, jak organizacji można użyć naszych interfejsów API i zapewnienia opartych na zasadach, Samoobsługowe możliwość zapisywania do swoich zaufanych partnerów, z zasadami, które określają aplikacje, które mogą uzyskiwać dostęp do.</span><span class="sxs-lookup"><span data-stu-id="d0af8-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine the apps they can access.</span></span> <span data-ttu-id="d0af8-112">Użytkowników z firm partnerskich można uzyskać dostęp do zasobów, gdy to konieczne, bezpieczne, bez konieczności zaproszenia organizacji ręcznie dołączyć je.</span><span class="sxs-lookup"><span data-stu-id="d0af8-112">Partner users can get access to resources when they need them, securely, without requiring the inviting organization to manually onboard them.</span></span> <span data-ttu-id="d0af8-113">Możesz z łatwością wdrożyć projekt do subskrypcji platformy Azure wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d0af8-113">You can easily deploy the project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="d0af8-114">Jako — kod</span><span class="sxs-lookup"><span data-stu-id="d0af8-114">As-is code</span></span>

<span data-ttu-id="d0af8-115">Należy pamiętać, ten kod jest udostępniana jako próbka do zaprezentowania użycia zaproszenie usługi Azure Active Directory B2B interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d0af8-115">Remember that this code is made available as a sample to demonstrate usage of the Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="d0af8-116">Powinny zostać dostosowane przez zespół deweloperów lub partnera i należy ją sprawdzić przed wdrożeniem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d0af8-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0af8-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0af8-117">Next steps</span></span>

<span data-ttu-id="d0af8-118">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d0af8-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="d0af8-119">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="d0af8-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d0af8-120">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="d0af8-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="d0af8-121">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="d0af8-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="d0af8-122">Elementy współpracy B2B zaproszenie</span><span class="sxs-lookup"><span data-stu-id="d0af8-122">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="d0af8-123">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="d0af8-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="d0af8-124">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="d0af8-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="d0af8-125">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d0af8-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="d0af8-126">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="d0af8-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="d0af8-127">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="d0af8-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="d0af8-128">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="d0af8-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="d0af8-129">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0af8-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)