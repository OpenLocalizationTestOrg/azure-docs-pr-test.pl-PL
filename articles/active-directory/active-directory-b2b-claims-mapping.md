---
title: "mapowanie w usłudze Azure Active Directory oświadczeń użytkowników współpracy aaaB2B | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="b2947-103">Mapowanie w usłudze Azure Active Directory oświadczeń użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b2947-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="b2947-104">Dostosowywanie oświadczeń hello wydanych w tokenie SAML hello użytkowników współpracy B2B usługi Azure obsługuje usługi Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2947-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="b2947-105">Podczas uwierzytelniania użytkownika aplikacji toohello, usługa Azure AD wystawia aplikacji toohello tokenu SAML, który zawiera informacje (lub oświadczenia) dotyczące hello użytkownika, który unikatowo identyfikuje je.</span><span class="sxs-lookup"><span data-stu-id="b2947-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="b2947-106">Domyślnie w tym nazwę użytkownika, adres e-mail, imię i nazwisko użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="b2947-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="b2947-107">Umożliwia wyświetlenie i edytowanie hello oświadczenia wysyłane w hello aplikacji toohello tokenu SAML hello karcie atrybutów.</span><span class="sxs-lookup"><span data-stu-id="b2947-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="b2947-108">Istnieją dwie możliwe przyczyny, dlaczego może być konieczne tooedit hello oświadczeń wydanych w tokenie SAML hello.</span><span class="sxs-lookup"><span data-stu-id="b2947-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="b2947-109">Aplikacja Hello została zapisana toorequire inny zestaw oświadczeń identyfikatorów URI lub wartości oświadczeń</span><span class="sxs-lookup"><span data-stu-id="b2947-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="b2947-110">Aplikacja wymaga hello NameIdentifier oświadczeń toobe inną niż nazwa główna użytkownika hello przechowywane w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2947-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![Widok oświadczenia w tokenie SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="b2947-112">Aby informacji na temat sposobu tooadd i Edycja oświadczeń, zapoznaj się w tym artykule na dostosowanie oświadczenia, [Dostosowywanie oświadczeń wydanych w tokenie SAML hello wstępnie zintegrowanych aplikacji w usłudze Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="b2947-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="b2947-113">Do współpracy B2B użytkowników mapowania NameID i UPN dzierżawy między będą mogły ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="b2947-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b2947-114">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2947-114">Next steps</span></span>

<span data-ttu-id="b2947-115">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b2947-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b2947-116">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="b2947-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b2947-117">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b2947-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="b2947-118">Dodawanie roli tooa użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b2947-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="b2947-119">Delegowanie B2bB współpracy zaproszenia</span><span class="sxs-lookup"><span data-stu-id="b2947-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="b2947-120">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b2947-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="b2947-121">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2947-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="b2947-122">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b2947-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="b2947-123">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="b2947-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="b2947-124">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b2947-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="b2947-125">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b2947-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
