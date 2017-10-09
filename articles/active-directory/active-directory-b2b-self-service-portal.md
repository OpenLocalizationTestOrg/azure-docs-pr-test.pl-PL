---
title: "portalu tworzenia konta usługi aaaSelf współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Współpraca z usługą Azure Active Directory B2B obsługuje relacji między firmami przez włączenie dostępu tooselectively partnerów biznesowych aplikacji firmowych"
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
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="7c769-103">Portal samoobsługowy do zapisywania do współpracy B2B usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c769-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="7c769-104">Klienci mogą wykonywanie wielu hello wbudowane funkcje, które są dostępne za pośrednictwem naszego administrator IT [portalu Azure](https://portal.azure.com) i naszych [panelu dostępu aplikacji](https://myapps.microsoft.com) dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="7c769-104">Customers can do a lot with hello built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="7c769-105">Ale możemy również pamiętać, że firmy muszą przepływ pracy dołączania hello toocustomize dla toofit użytkowników B2B potrzeb organizacji.</span><span class="sxs-lookup"><span data-stu-id="7c769-105">But we are also aware that businesses need toocustomize hello onboarding workflow for B2B users toofit their organization’s needs.</span></span> <span data-ttu-id="7c769-106">Można wykonać z [interfejsach API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="7c769-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="7c769-107">W dyskusjach ze specjalistami z naszych klientów widzimy się, że jeden wspólny wjazd należy przede wszystkim innym.</span><span class="sxs-lookup"><span data-stu-id="7c769-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="7c769-108">Witaj zapraszanie organizacji może nie wiedzieć wcześniejsze kto hello poszczególnych zewnętrznych współpracowników są, który muszą uzyskać dostęp do zasobów tootheir.</span><span class="sxs-lookup"><span data-stu-id="7c769-108">hello inviting organization may not know ahead of time who hello individual external collaborators are who need access tootheir resources.</span></span> <span data-ttu-id="7c769-109">Chcieli sposób dla użytkowników z firm partnerskich zbyt Zarejestruj się z zestawem zasad tego hello zapraszanie formanty organizacji.</span><span class="sxs-lookup"><span data-stu-id="7c769-109">They wanted a way for users from partner companies too sign themselves up with a set of policies that hello inviting organization controls.</span></span> <span data-ttu-id="7c769-110">Ten scenariusz jest możliwe za pośrednictwem naszych interfejsów API, dlatego firma Microsoft opublikowane projektu w witrynie Github, która została właśnie tę: [przykładowy projekt Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="7c769-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="7c769-111">Nasze projektu Github pokazano, jak organizacji można użyć naszych interfejsów API i podaj opartych na zasadach, Samoobsługowe możliwość zapisywania do zaufanych partnerów z zasad określających hello aplikacje, które mogą uzyskiwać dostęp do.</span><span class="sxs-lookup"><span data-stu-id="7c769-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine hello apps they can access.</span></span> <span data-ttu-id="7c769-112">Użytkowników z firm partnerskich można uzyskać dostępu tooresources, gdy to konieczne, bezpieczne, bez konieczności hello zapraszanie dołączyć toomanually organizacji je.</span><span class="sxs-lookup"><span data-stu-id="7c769-112">Partner users can get access tooresources when they need them, securely, without requiring hello inviting organization toomanually onboard them.</span></span> <span data-ttu-id="7c769-113">Możesz z łatwością wdrożyć hello projektu do subskrypcji platformy Azure wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7c769-113">You can easily deploy hello project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="7c769-114">Jako — kod</span><span class="sxs-lookup"><span data-stu-id="7c769-114">As-is code</span></span>

<span data-ttu-id="7c769-115">Należy pamiętać, ten kod jest udostępniana jako przykładowe zastosowanie toodemonstrate zaproszenia hello Azure Active Directory B2B interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="7c769-115">Remember that this code is made available as a sample toodemonstrate usage of hello Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="7c769-116">Powinny zostać dostosowane przez zespół deweloperów lub partnera i należy ją sprawdzić przed wdrożeniem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="7c769-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c769-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c769-117">Next steps</span></span>

<span data-ttu-id="7c769-118">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="7c769-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="7c769-119">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="7c769-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="7c769-120">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="7c769-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="7c769-121">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="7c769-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="7c769-122">elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c769-122">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="7c769-123">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c769-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="7c769-124">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="7c769-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="7c769-125">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="7c769-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="7c769-126">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="7c769-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="7c769-127">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c769-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="7c769-128">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="7c769-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="7c769-129">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c769-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)