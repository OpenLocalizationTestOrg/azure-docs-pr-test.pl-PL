---
title: "Mapowanie w usłudze Azure Active Directory oświadczeń użytkowników współpracy B2B | Dokumentacja firmy Microsoft"
description: "mapowanie odwołania do usługi Azure Active Directory B2B współpracy oświadczeń"
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
ms.openlocfilehash: 5f8559450b24effd40a38879aeae3a8dd03944a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="94878-103">Mapowanie w usłudze Azure Active Directory oświadczeń użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="94878-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="94878-104">Dostosowywanie oświadczeń wydanych w tokenie SAML dla użytkowników współpracy B2B usługi Azure obsługuje usługi Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94878-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="94878-105">Podczas uwierzytelniania użytkownika do aplikacji, usługi Azure AD wystawia SAML token aplikacja, która zawiera informacje (lub oświadczenia) dotyczące użytkownika, który unikatowo identyfikuje je.</span><span class="sxs-lookup"><span data-stu-id="94878-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="94878-106">Domyślnie w tym nazwę użytkownika, adres e-mail, imię i nazwisko użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94878-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="94878-107">Umożliwia wyświetlenie i edytowanie oświadczenia wysyłane w tokenie SAML do aplikacji na karcie atrybutów.</span><span class="sxs-lookup"><span data-stu-id="94878-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="94878-108">Istnieją dwie możliwe przyczyny, dlaczego konieczne może być Edycja oświadczeń wydanych w tokenie SAML.</span><span class="sxs-lookup"><span data-stu-id="94878-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="94878-109">Aplikacja została zapisana wymagają innego zestawu oświadczeń identyfikatorów URI lub wartości oświadczeń</span><span class="sxs-lookup"><span data-stu-id="94878-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="94878-110">Aplikacja wymaga oświadczeń NameIdentifier inny niż nazwa główna użytkownika przechowywane w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94878-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![Widok oświadczenia w tokenie SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="94878-112">Aby uzyskać informacje o tym, jak dodawać i edytować oświadczenia, zapoznaj się z tego artykułu na dostosowanie oświadczenia, [Dostosowywanie oświadczeń wydanych w tokenie SAML dla wstępnie zintegrowanych aplikacji w usłudze Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="94878-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="94878-113">Do współpracy B2B użytkowników mapowania NameID i UPN dzierżawy między będą mogły ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="94878-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="94878-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94878-114">Next steps</span></span>

<span data-ttu-id="94878-115">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="94878-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="94878-116">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="94878-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="94878-117">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="94878-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="94878-118">Dodawanie do roli użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="94878-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="94878-119">Delegowanie B2bB współpracy zaproszenia</span><span class="sxs-lookup"><span data-stu-id="94878-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="94878-120">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="94878-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="94878-121">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="94878-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="94878-122">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="94878-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="94878-123">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="94878-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="94878-124">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="94878-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="94878-125">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="94878-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
