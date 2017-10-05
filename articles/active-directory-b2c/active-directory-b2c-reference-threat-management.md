---
title: "Usługa Azure Active Directory B2C: Zagrożenia zarządzania | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat techniki wykrywanie i zapobieganie atakom typu \"odmowa usługi\" i prób złamania hasła w usłudze Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="ef0b1-103">Usługa Azure Active Directory B2C: Zarządzanie zagrożeniami</span><span class="sxs-lookup"><span data-stu-id="ef0b1-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="ef0b1-104">Zarządzanie zagrożeniami obejmuje planowanie dotyczące ochrony przed atakami systemu i sieci.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="ef0b1-105">Ataki typu "odmowa usługi" może spowodować zasobów niedostępny uprawnionych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="ef0b1-106">Złamania hasła prowadzić do nieautoryzowanego dostępu do zasobów.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="ef0b1-107">Usługa Azure Active Directory B2C (Azure AD B2C) ma wbudowane funkcje, które mogą pomóc chronić dane przed zagrożeniami tych na wiele sposobów.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="ef0b1-108">Ataki typu "odmowa usługi"</span><span class="sxs-lookup"><span data-stu-id="ef0b1-108">Denial-of-service attacks</span></span>

<span data-ttu-id="ef0b1-109">Azure AD B2C używa wykrywanie i zapobieganie technik, takich jak pliki cookie SYN i limitów szybkości i połączenia w celu ochrony zasobów przed atakami typu "odmowa usługi".</span><span class="sxs-lookup"><span data-stu-id="ef0b1-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="ef0b1-110">Złamania hasła</span><span class="sxs-lookup"><span data-stu-id="ef0b1-110">Password attacks</span></span>

<span data-ttu-id="ef0b1-111">Usługa Azure AD B2C ma również techniki środki zaradcze w przypadku złamania hasła.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="ef0b1-112">Środki zaradcze obejmuje ataków siłowych hasła i słownikowymi hasła.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="ef0b1-113">Hasła, które są ustawiane przez użytkowników muszą być rozsądnych złożonych.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="ef0b1-114">Za pomocą różnych sygnałów, usługi Azure AD B2C analizuje integralności żądań.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="ef0b1-115">Usługa Azure AD B2C jest przeznaczona do inteligentnie rozróżnianie uprawnionych użytkowników przed hakerami i zakłócanych.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="ef0b1-116">Usługi Azure AD B2C udostępnia zaawansowane strategii blokady konta oparte na wprowadzone w prawdopodobieństwo ataku hasła.</span><span class="sxs-lookup"><span data-stu-id="ef0b1-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="ef0b1-117">Aby uzyskać więcej informacji, odwiedź stronę [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="ef0b1-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
